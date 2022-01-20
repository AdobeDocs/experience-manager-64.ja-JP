---
title: SRP と UGC の基本事項
seo-title: SRP and UGC Essentials
description: ストレージリソースプロバイダーとユーザー生成コンテンツの概要
seo-description: Storage resource provider and user-generated content overview
uuid: a4ee8725-f554-4fcf-ac1e-34878d6c02f8
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.4/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 0763f236-5648-49e9-8a24-dbc8f4c77ee3
exl-id: 45b9d418-0ecb-44c9-8091-b9ce29ba730b
source-git-commit: bd94d3949f0117aa3e1c9f0e84f7293a5d6b03b4
workflow-type: tm+mt
source-wordcount: '728'
ht-degree: 59%

---

# SRP と UGC の基本事項 {#srp-and-ugc-essentials}

## はじめに {#introduction}

ストレージリソースプロバイダー（SRP）および SRP とユーザー生成コンテンツ（UGC）との関係について詳しくは、[コミュニティコンテンツストレージ](working-with-srp.md)および[ストレージリソースプロバイダーの概要](srp.md)を参照してください。

ドキュメントのこの節では、SRP および UGC に関する基本情報について説明します。

## StorageResourceProvider API {#storageresourceprovider-api}

SocialResourceProvider API（SRP API）は、様々な Sling リソースプロバイダー API の拡張です。ページネーションとアトミックな増分のサポートが含まれます（集計とスコアリングに役立ちます）。

日付、有用性、投票数などによる並べ替えが必要なので、SCF コンポーネントにはクエリが必要です。すべての SRP オプションには、バケット化に依存しない柔軟なクエリメカニズムがあります。

SRP 格納場所には、コンポーネントのパスが組み込まれます。SRP API は常に UGC にアクセスするために使用する必要があります。ルートパスは、ASRP、MSRP、JSRP など、選択した SRP オプションに応じて異なるからです。

SRP API は、抽象クラスではなくインターフェイスです。新しいリリースにアップグレードする際に、内部実装に対する今後の改善のメリットが失われるので、カスタム実装を軽くおこなわないでください。

SRP API を使用するための手段は、提供されるユーティリティ（SocialResourceUtilities パッケージで見つかるものなど）です。

AEM 6.0 以前からアップグレードする場合、すべての SRP の UGC の移行が必要になります。そのために、オープンソースのツールを使用できます。詳しくは、 [AEM Communities 6.3 へのアップグレード](upgrade.md).

>[!NOTE]
>
>以前は、UGC にアクセスするためのユーティリティは SocialUtils パッケージ内にありましたが、このパッケージはなくなりました。
>
>代わりのユーティリティについては、[SocialUtils リファクタリング](socialutils.md)を参照してください。

## UGC にアクセスするためのユーティリティメソッド {#utility-method-to-access-ugc}

UGC にアクセスするには、SRP から UGC へのアクセスに適したパスを返し、SocialUtils にあった廃止されたメソッドに替わる、SocialResourceUtilities パッケージのメソッドを使用します。

以下に、サーブレットでの resourceToUGCStoragePath() メソッドの使用の最小限の例を示します。

```java
import com.adobe.cq.social.srp.utilities.api.SocialResourceUtilities;

@Reference
private SocialResourceUtilities socialResourceUtilities;

@Override
protected void doGet(final SlingHttpServletRequest request, final SlingHttpServletResponse response) throws ServletException, IOException {
  String ugcPath = socialResourceUtilities.resourceToUGCStoragePath(request.getResource());
  // rest of servlet
}
```

その他の SocialUtils の代替については、[SocialUtils のリファクタリング](socialutils.md)を参照してください。

コーディングのガイドラインについては、[SRP による UGC へのアクセス](accessing-ugc-with-srp.md)を参照してください。

>[!CAUTION]
>
>resourceToUGCStoragePath() が返すパスは、次には適していません。 [ACL チェック](srp.md#for-access-control-acls).

## ACL にアクセスするためのユーティリティメソッド {#utility-method-to-access-acls}

一部の SRP 実装（ASRP や MSRP など）では、コミュニティコンテンツは ACL 検証が提供されないデータベースに格納されます。シャドウノードは、ACL を適用できるローカルリポジトリ内の場所を提供します。

SRP API を使用すると、すべての SRP オプションによって、すべての CRUD 操作の前にシャドウの場所の同じチェックが実行されます。

ACL をチェックするには、リソースの UGC に適用される権限のチェックに適したパスを返すメソッドを使用します。

以下に、サーブレットでの resourceToACLPath() メソッドの使用の単純な例を示します。

```java
import com.adobe.cq.social.srp.utilities.api.SocialResourceUtilities;

@Reference
private SocialResourceUtilities socialResourceUtilities;

@Override
protected void doGet(final SlingHttpServletRequest request, final SlingHttpServletResponse response) throws ServletException, IOException {
  String aclPath = socialResourceUtilities.resourceToACLPath(request.getResource());
  // rest of servlet
}
```

>[!CAUTION]
>
>resourceToACLPath() から返されるパスは、次には適していません。 [UGC へのアクセス](#utility-method-to-access-acls) それ自体。

## UGC 関連の格納場所 {#ugc-related-storage-locations}

格納場所に関する以下の説明は、JSRP または MSRP を使用した開発時に役立つ場合があります。JSRP ([CRXDE Lite](../../help/sites-developing/developing-with-crxde-lite.md)) および MSRP（MongoDB ツール）

**コンポーネントの場所**

メンバーがパブリッシュ環境で UGC を入力する場合、AEM サイトの一部としてのコンポーネントとやり取りしています。

このようなコンポーネントの例として、 [コメントコンポーネント](http://localhost:4502/content/community-components/en/comments.html) が [コミュニティコンポーネントガイド](components-guide.md) サイト。 ローカルリポジトリ内のコメントノードへのパスは次のとおりです。

* コンポーネントパス= */content/community-components/en/comments/jcr:content/content/includable/comments*

**シャドウノードの場所**

UGC の作成によって、必要な ACL が適用される[シャドウノード](srp.md#about-shadow-nodes-in-jcr)も作成されます。ローカルリポジトリ内の対応するシャドウノードへのパスは、シャドウノードのルートパスの前にコンポーネントパスを指定した結果です。

* ルートパス= /content/usergenerated
* コメントのシャドウノード= /content/usergenerated/content/community-components/en/comments/jcr:content/content/includable/comments

**UGC の場所**

UGC はこれらの場所のどちらにも作成されず、SRP API を呼び出す[ユーティリティメソッド](#utility-method-to-access-ugc)の使用によってのみアクセスする必要があります。

* ルートパス= /content/usergenerated/asi/srp-choice
* JSRP の UGC ノード= /content/usergenerated/asi/jcr/content/community-components/en/comments/jcr:content/content/includable/comments/srzd-let_it_be_

** JSRP の場合、UGC ノードはそれが入力された AEM インスタンス（オーサーまたはパブリッシュ）上にのみ存在することに注意してください。**&#x200B;パブリッシュインスタンスで入力した場合、作成者のモデレートコンソールからモデレートを実行することはできません。

## 関連情報 {#related-information}

* [ストレージリソースプロバイダの概要](srp.md)  — 概要とリポジトリ使用の概要
* [SRP を使用した UGC へのアクセス](accessing-ugc-with-srp.md)  — コーディングガイドライン
* [SocialUtils リファクタリング](socialutils.md)  — 廃止されたユーティリティメソッドを現在の SRP ユーティリティメソッドにマッピングする
