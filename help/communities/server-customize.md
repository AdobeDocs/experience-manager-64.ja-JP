---
title: サーバー側のカスタマイズ
seo-title: Server-side Customization
description: AEM Communitiesのサーバー側のカスタマイズ
seo-description: Customizing server-side in AEM Communities
uuid: 5e9bc6bf-69dc-414c-a4bd-74a104d7bd8f
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.4/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: df5416ec-5c63-481b-99ed-9e5a91df2432
exl-id: fbe2a617-e926-4842-a3bc-8d193bd367dc
source-git-commit: c5b816d74c6f02f85476d16868844f39b4c47996
workflow-type: tm+mt
source-wordcount: '927'
ht-degree: 2%

---

# サーバー側のカスタマイズ {#server-side-customization}

>[!CAUTION]
>
>AEM 6.4 の拡張サポートは終了し、このドキュメントは更新されなくなりました。 詳細は、 [技術サポート期間](https://helpx.adobe.com/jp/support/programs/eol-matrix.html). サポートされているバージョンを見つける [ここ](https://experienceleague.adobe.com/docs/?lang=ja).

| **[⇐機能の基本事項](essentials.md)** | **[クライアント側のカスタマイズ ⇒](client-customize.md)** |
|---|---|
|  | **[SCF Handlebars ヘルパー ⇒](handlebars-helpers.md)** |

## Java API {#java-apis}

>[!NOTE]
>
>Communities API のパッケージの場所は、あるメジャーリリースから次のリリースにアップグレードする際に変更される場合があります。

### SocialComponent インターフェイス {#socialcomponent-interface}

SocialComponents は、AEM Communities機能のリソースを表す POJO です。 各 SocialComponent は、リソースが正確に表されるように、クライアントにデータを提供する公開された GETters を持つ特定の resourceType を表すのが理想的です。 必要に応じて、すべてのビジネスロジックとビューロジックは SocialComponent にカプセル化されます。サイト訪問者のセッション情報も含まれます。

このインターフェイスは、リソースを表すのに必要な GETter の基本的なセットを定義します。 重要な点は、インターフェイスがマップを規定することです&lt;string object=&quot;&quot;> Handlebars テンプレートをレンダリングし、リソースのGETJSON エンドポイントを公開するために必要な getAsMap() および String toJSONString() メソッド。

すべての SocialComponent クラスがインターフェイスを実装する必要があります `com.adobe.cq.social.scf.SocialComponent`

### SocialCollectionComponent インターフェイス {#socialcollectioncomponent-interface}

SocialCollectionComponent インターフェイスは、 SocialComponent インターフェイスを拡張して、他のリソースの集まりであるリソースをより適切に表すようにします。

すべての SocialCollectionComponent クラスは、インターフェイスcom.adobe.cq.social.scf.SocialCollectionComponent を実装する必要があります

### SocialComponentFactory インターフェイス {#socialcomponentfactory-interface}

SocialComponentFactory（ファクトリ）は、SocialComponent をフレームワークに登録します。 ファクトリは、特定の resourceType に対して使用可能な SocialComponents とその優先順位付け&amp;ast をフレームワークに知らせる手段を提供します。複数の SocialComponents が識別された場合。

SocialComponentFactory は、選択した SocialComponent のインスタンスを作成し、ID プラクティスを使用して SocialComponent が必要とするすべての依存関係をファクトリから挿入できるようにします。

SocialComponentFactory は OSGi サービスで、コンストラクターを通じて SocialComponent に渡すことができる他の OSGi サービスにアクセスできます。

すべての SocialComponentFactory クラスがインターフェイスを実装する必要があります `com.adobe.cq.social.scf.SocialComponentFactory`

SocialComponentFactory.getPriority() メソッドの実装では、getResourceType() が返す、指定された resourceType に対してファクトリが使用されるように、最も高い値を返す必要があります。

### SocialComponentFactoryManager インターフェイス {#socialcomponentfactorymanager-interface}

SocialComponentFactoryManager（マネージャー）は、フレームワークに登録されているすべての SocialComponents を管理し、特定のリソース (resourceType) に使用する SocialComponentFactory を選択します。 特定の resourceType にファクトリが登録されていない場合、マネージャは指定されたリソースに最も近いスーパータイプを持つファクトリを返します。

SocialComponentFactoryManager は OSGi サービスで、コンストラクターを通じて SocialComponent に渡すことができる他の OSGi サービスにアクセスできます。

OSGi サービスへのハンドルは、を呼び出すことで取得されます `com.adobe.cq.social.scf.SocialComponentFactoryManager`

### HTTP API -POSTリクエスト {#http-api-post-requests}

#### PostOperation クラス {#postoperation-class}

HTTP APIPOSTエンドポイントは、 `SlingPostOperation`インターフェイス（パッケージ） `org.apache.sling.servlets.post`) をクリックします。

この `PostOperation`エンドポイント実装セット `sling.post.operation`を、操作の応答先の値に設定します。 :operation パラメーターがその値に設定されているすべてのPOSTリクエストが、この実装クラスに委任されます。

この `PostOperation`を呼び出します。 `SocialOperation`：操作に必要なアクションを実行します。

この `PostOperation`が `SocialOperation`を返し、適切な応答をクライアントに返します。

#### SocialOperation クラス {#socialoperation-class}

各 `SocialOperation`endpoint は AbstractSocialOperation クラスを拡張し、メソッドをオーバーライドします。 `performOperation().`このメソッドは、操作を完了し、 `SocialOperationResult`または `OperationException`。この場合、メッセージ付きの HTTP エラーステータスが、通常の JSON 応答または成功 HTTP ステータスコードの代わりに返されます。

拡張ガイド `AbstractSocialOperation`～の再利用を可能にする `SocialComponents`をクリックして JSON 応答を送信します。

#### SocialOperationResult クラス {#socialoperationresult-class}

この `SocialOperationResult`クラスは、 `SocialOperation`およびは、 `SocialComponent`、HTTP ステータスコード、および HTTP ステータスメッセージ。

この `SocialComponent`操作の影響を受けたリソースを表します。

作成操作の場合、 `SocialComponent`次に含まれる `SocialOperationResult`作成したリソースを表し、「更新」操作の場合は、操作によって変更されたリソースを表します。 いいえ `SocialComponent`は、削除操作に対して返されます。

使用される成功 HTTP ステータスコードは次のとおりです。

* 作成操作の場合は 201
* 200（更新操作用）
* 削除操作の場合は 204

#### OperationException クラス {#operationexception-class}

An `OperationExcepton`は、リクエストが有効でない場合、または内部エラー、無効なパラメーター値、不適切な権限などの他のエラーが発生した場合に、操作の実行時にスローされます。 An `OperationException`は、HTTP ステータスコードとエラーメッセージで構成され、 `PostOperatoin`.

#### OperationService クラス {#operationservice-class}

ソーシャルコンポーネントフレームワークでは、操作を実行するビジネスロジックを `SocialOperation`クラスに委任する代わりに、OSGi サービスに委任することもできます。 ビジネスロジックに OSGi サービスを使用すると、 `SocialComponent`に基づいて、 `SocialOperation`エンドポイント（他のコードと統合され、異なるビジネスロジックが適用される）

すべて `OperationService`クラスを拡張 `AbstractOperationService`を使用すると、実行中の操作に関連付けることのできる追加の拡張機能を使用できます。 サービス内の各操作は、 `SocialOperation`クラス。 この `OperationExtensions`クラスは、操作の実行中に、メソッドを呼び出すことで呼び出すことができます

* `performBeforeActions()`
事前チェック/前処理および検証を許可
* `performAfterActions()`
リソースをさらに変更したり、カスタムイベントやワークフローなどを呼び出したりできます

#### OperationExtension クラス {#operationextension-class}

`OperationExtension`クラスは、操作に挿入できるカスタムコードで、ビジネスニーズに合わせて操作をカスタマイズできます。 コンポーネントの消費者は、動的かつ増分的にコンポーネントに機能を追加できます。 拡張/フックパターンを使用すると、開発者は拡張機能自体にのみ焦点を当て、操作やコンポーネント全体をコピーして上書きする必要がなくなります。

## サンプルコード {#sample-code}

サンプルコードは、 [Adobe Marketing Cloud GitHub](https://github.com/Adobe-Marketing-Cloud) リポジトリ。 次のいずれかのプレフィックスが付いたプロジェクトを検索します。 `aem-communities` または `aem-scf`.

## ベストプラクティス {#best-practices}

次を表示： [コーディングのガイドライン](code-guide.md) AEM Communities開発者向けの様々なコーディングガイドラインおよびベストプラクティスに関する節を参照してください。

関連トピック [UGC 用ストレージリソースプロバイダー (SRP)](srp.md) ユーザー生成コンテンツへのアクセスについて説明します。

| **[⇐機能の基本事項](essentials.md)** | **[クライアント側のカスタマイズ ⇒](client-customize.md)** |
|---|---|
|  | **[SCF Handlebars ヘルパー ⇒](handlebars-helpers.md)** |
