---
title: ブログの基本事項
seo-title: Blog Essentials
description: ブログの概要
seo-description: Blog overview
uuid: ce0885de-6276-47a2-8f6c-358f0beb2b89
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.4/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: de8d0e6d-827b-45fe-a538-d3fe1dec8427
exl-id: 8cff0b7b-c120-462f-8fce-13822073eabb
source-git-commit: c5b816d74c6f02f85476d16868844f39b4c47996
workflow-type: tm+mt
source-wordcount: '478'
ht-degree: 5%

---

# ブログの基本事項 {#blog-essentials}

>[!CAUTION]
>
>AEM 6.4 の拡張サポートは終了し、このドキュメントは更新されなくなりました。 詳細は、 [技術サポート期間](https://helpx.adobe.com/jp/support/programs/eol-matrix.html). サポートされているバージョンを見つける [ここ](https://experienceleague.adobe.com/docs/?lang=ja).

AEM 6.1 Communities 以降、ブログはコミュニティアクティビティとなります。 ブログ記事は、パブリッシュ環境から投稿されるようになりました。以前は、ブログ記事はオーサー環境でのみ作成し、公開できました。

権限を持つメンバーに制限されない限り、すべてのコミュニティメンバーがブログ記事を作成できるようになりました。

このページでは、ブログ機能の操作に関する基本情報を提供します。

>[!NOTE]
>
>ブログ機能の基盤となるインフラストラクチャは、ジャーナル機能です。

## クライアント側の基本事項 {#essentials-for-client-side}

ブログ機能は、 [ブログ機能](functions.md#blog-function) または、オーサリング編集モードでコンポーネントをページに追加します。

### ブログ {#blog}

<table> 
 <tbody>
  <tr>
   <td> <strong>resourceType</strong></td> 
   <td>social/journal/components/hbs/journal</td> 
  </tr>
  <tr>
   <td> <a href="scf.md#add-or-include-a-communities-component"><strong>包含可能な</strong></a></td> 
   <td>いいえ</td> 
  </tr>
  <tr>
   <td> <a href="clientlibs.md"><strong>clientllibs</strong></a></td> 
   <td>cq.ckeditor<br /> cq.social.hbs.voting<br /> cq.social.hbs.journal</td> 
  </tr>
  <tr>
   <td> <strong>テンプレート</strong></td> 
   <td> /libs/social/journal/components/hbs/journal/journal.hbs<br /> /libs/social/journal/components/hbs/entry_topic/list-item.hbs</td> 
  </tr>
  <tr>
   <td> <strong>css</strong></td> 
   <td> /libs/social/journal/components/hbs/journal/clientlibs/journal.css</td> 
  </tr>
  <tr>
   <td><strong> properties</strong></td> 
   <td>参照 <a href="blog-feature.md">ブログ機能</a></td> 
  </tr>
 </tbody>
</table>

### ブログのサイドバー {#blog-sidebar}

| **resourceType** | social/journal/components/hbs/sidebar |
|---|---|
| [**包含可能な**](scf.md#add-or-include-a-communities-component) | いいえ |
| [**clientllibs**](clientlibs.md) | cq.social.hbs.journal_sidebar |
| **テンプレート** | /libs/social/journal/components/hbs/sidebar/sidebar.hbs |
| **css** | /libs/social/journal/components/hbs/sidebar/clientlibs/sidebar.css |
| **プロパティ** | 参照 [ブログ機能](blog-feature.md) |

* [クライアント側のカスタマイズ](client-customize.md)

## サーバー側の基本事項 {#essentials-for-server-side}

* [ブログ API](https://helpx.adobe.com/experience-manager/6-4/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/journal/client/api/package-summary.html)

* [ブログエンドポイント](https://helpx.adobe.com/experience-manager/6-4/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/journal/client/endpoints/package-summary.html)

* [サーバー側のカスタマイズ](server-customize.md)

### ブログ機能 {#blog-function}

を含むコミュニティサイト構造 [Bog 関数](functions.md#blog-function) は設定されます `Blog` および `Blog Sidebar` コンポーネント。 ブログ機能は、 [権限を持つメンバーユーザーグループ](users.md#privileged-members-group).

### ブログエントリ (UGC) へのアクセス {#accessing-blog-entries-ugc}

UGC は、モデレートの標準的な方法の 1 つを使用してモデレートする必要があります。\
詳しくは、 [ユーザー生成コンテンツのモデレート](moderate-ugc.md).

AEM 6.1 Communities 以降では、 [共通店](working-with-srp.md) UGC の場合は、選択したストレージオプション（ASRP、MSRP、JSRP など）に関係なく、プログラムで UGC にアクセスできます。

**リポジトリ内の UGC の場所と形式は、警告なしで変更される場合があります**.

以下を参照してください。

* [ストレージリソースプロバイダの概要](srp.md)  — 概要とリポジトリ使用の概要
* [SRP と UGC の基本事項](srp-and-ugc.md) - SRP ユーティリティメソッドと例
* [SRP を使用した UGC へのアクセス](accessing-ugc-with-srp.md)  — コーディングガイドライン
* [SocialUtils リファクタリング](socialutils.md)  — 非推奨のユーティリティメソッドを現在の SRP ユーティリティメソッドにマッピングします

## プライマリ発行者 {#primary-publisher}

デプロイメントがパブリッシュファームの場合は、パブリッシュ予定の記事をポーリングするプライマリパブリッシャーを特定する必要があります。

詳しくは、 [プライマリ発行者](deploy-communities.md#primary-publisher) を参照してください。

## リッチメディアの許可 {#allowing-rich-media}

AEMプラットフォームは、XSS 攻撃を防ぐために、他の Web サイトからのリンクをブロックします。詳しくは、

* [クロスサイトスクリプティング (XSS) に対するProtect](../../help/sites-developing/security.md#protect-against-cross-site-scripting-xss)

AEM 6.2 以降では、手動で行う必要があった変更がデフォルトの AntiSamy 設定ファイルに含まれています。

リッチメディアは、 `Embed Media from External Sites` アイコン：  ![chlimage_1-471](assets/chlimage_1-471.png)
