---
title: Document Security によって保護された PDF ドキュメントを AEM で検索可能にする
seo-title: Enable AEM to search document security protected PDF documents
description: DRM 保護されたドキュメントでネイティブAEM検索を有効にして全文検索を実行する方法をPDFします。
seo-description: Learn how to enable native AEM search to perform full-text search on DRM protected PDF documents.
uuid: c743cda3-252f-4c1f-8d94-e6d26d91dcd8
contentOwner: khsingh
content-type: reference
products: SG_EXPERIENCEMANAGER/6.4/FORMS
geptopics: SG_AEMFORMS/categories/working_with_document_security
discoiquuid: 759068fa-dc1b-4cf5-bc7b-62b8c5464831
feature: Document Security
exl-id: c405c69b-3588-4701-8f36-1ea0680e056d
source-git-commit: c5b816d74c6f02f85476d16868844f39b4c47996
workflow-type: tm+mt
source-wordcount: '696'
ht-degree: 48%

---

# Document Security によって保護された PDF ドキュメントを AEM で検索可能にする {#enable-aem-to-search-document-security-protected-pdf-documents}

>[!CAUTION]
>
>AEM 6.4 の拡張サポートは終了し、このドキュメントは更新されなくなりました。 詳細は、 [技術サポート期間](https://helpx.adobe.com/jp/support/programs/eol-matrix.html). サポートされているバージョンを見つける [ここ](https://experienceleague.adobe.com/docs/?lang=ja).

AEM検索では、AEMアセットを検索および検索し、プレーンテキストファイル、Microsoft Office ドキュメント、PDFドキュメントなど、一般的に使用される様々なドキュメント形式でテキスト検索を実行できます。 ネイティブ検索を拡張して、フルテキスト検索を実行することもできます [AEM Document Security で保護されたPDFドキュメント](/help/forms/using/admin-help/document-security.md). AEMがドキュメントに対して全文検索を実行できるようにするには、次の手順を実行します。

1. 安全な接続の確立
1. ポリシーで保護されたサンプルPDFドキュメントのインデックス作成

## 前提条件 {#prerequisites}

* OSGi 上で AEM Forms を使用している場合：

   * [AEM Forms Document Security Indexer パッケージ](https://helpx.adobe.com/jp/aem-forms/kb/aem-forms-releases.html)を AEM Forms サーバーにインストールします。
   * JEE サーバー上で AEM Forms が起動して実行されていること、および Document Security が JEE サーバー上の対応する AEM Forms にインストールされていることを確認します。保護されたドキュメントのインデックスを作成するには、JEE サーバー上の AEM Form が必要です。

* JEE サーバー上で AEM Forms のみを使用している場合、Indexer パッケージはすでにインストールされています。
* すべてのバンドルが正常に実行していることを確認します。アクティブ状態になっていないバンドルが存在する場合は、すべてのバンドルが起動して実行されるまで待ちます。

   * OSGi 上のAEM Formsの場合、バンドルは次の場所にリストされます。 `https://[server]:[port]/system/console/bundles`.
   * JEE 上のAEM Formsの場合、バンドルは次の場所に一覧表示されます。 `https://[server]:[port]/[context-path]/system/console/bundles`. 例：`http://localhost:8080/lc/system/console/bundles`

* *sun.util.calendar* パッケージを許可リストに追加します。パッケージを許可リストに追加するには、次の手順を実行します。

   1. AEM web コンソールを開きます。URL は `https://[server]:[port]/system/console/configMgr` です。。
   1. **デシリアライゼーションファイアウォール設定**&#x200B;を探して開きます。
   1. sun.util.calendar パッケージを「ホワイトリストに登録されたクラスまたはパッケージのプレフィックス」フィールドに追加し、 **保存**.

## AEM Forms JEE と OSGi スタック間の安全な接続の確立 {#establish-a-secure-connection-between-aem-forms-jee-and-osgi-stacks}

次のいずれかの方法を使用して、安全な接続を確立できます。

* JEE 上のAEM Formsの管理者資格情報を使用して、AdobeLiveCycleClient SDK Bundle を設定します。
* 相互認証を使用した Adobe LiveCycle Client SDK Bundle の設定

### JEE 上のAEM Formsの管理者資格情報を使用して、AdobeLiveCycleClient SDK Bundle を設定します。 {#configure-adobe-livecycle-client-sdk-bundle-with-aem-forms-on-jee-admin-credentials}

1. AEM web コンソールを開きます。URL は `https://[server]:[port]/system/console/configMgr` です。。
1. を探して開きます。 **AdobeLiveCycleクライアント SDK バンドル**. 次のフィールドの値を指定します。

   * **サーバー URL**：JEE サーバー上の AEM Forms の HTTPS URL を指定します。HTTPS 経由の通信を可能にするには、-Djavax.net.ssl.trustStore=&lt;JEE キーストアファイル上の AEM Forms のパス> のパラメータで AEM サーバーを再起動します。
   * **サービス名**：指定されたサービスの一覧に RightsManagementService を追加します。
   * **ユーザー名**：AEM サーバーからの呼び出しの開始に使用される JEE 上の AEM Forms アカウントのユーザー名を指定します。指定したアカウントには、JEE 上のAEM Formsサーバーで Document Services を開始する権限が必要です。
   * **パスワード**:「ユーザー名」フィールドで説明した JEE 上のAEM Formsアカウントのパスワードを指定します。

   「**保存**」をクリックします。AEMは、Document Security で保護されたPDFドキュメントを検索できます。

### 相互認証を使用した Adobe LiveCycle Client SDK Bundle の設定 {#configure-adobe-livecycle-client-sdk-bundle-using-mutual-authentication}

1. JEE 上のAEM Formsの相互認証を有効にします。 詳しくは、 [CAC と相互認証](https://helpx.adobe.com/jp/livecycle/kb/cac-mutual-authentication.html).
1. AEM web コンソールを開きます。URL は `https://[server]:[port]/system/console/configMgr` です。。
1. を探して開きます。 **AdobeLiveCycleクライアント SDK** バンドル。 次のプロパティの値を指定します。

   * **サーバー URL**：JEE サーバー上の AEM Forms の HTTPS URL を指定します。HTTPS 経由の通信を有効にするには、 -Djavax.net.ssl.trustStore=&lt;path of=&quot;&quot; aem=&quot;&quot; forms=&quot;&quot; on=&quot;&quot; jee=&quot;&quot; keystore=&quot;&quot; file=&quot;&quot;> パラメーター。
   * **2way SSL の有効化**：「2way SSL の有効化」オプションを有効にします。
   * **キーストアファイル URL**：キーストアファイルの URL を指定します。
   * **TrustStore ファイル URL**：Truststore ファイルの URL を指定します.
   * **キーストアパスワード**：キーストアファイルのパスワードを指定します。
   * **TrustStore パスワード**：Truststore ファイルのパスワードを指定します。
   * **サービス名**：指定されたサービスの一覧に RightsManagementService を追加します。

   「**保存**」をクリックします。AEMは Document Security で保護されたドキュメントを検索するために有効になります。PDF

## ポリシーで保護されたサンプルPDFドキュメントのインデックス作成 {#index-a-sample-policy-protected-pdf-document}

1. 管理者として AEM Assets にログインします。
1. AEM Digital Asset Manager でフォルダーを作成し、新しく作成したフォルダーにポリシーで保護されたPDFドキュメントをアップロードします。

   これで、AEM検索を使用して、ポリシーで保護されたドキュメントを検索できるようになりました。
