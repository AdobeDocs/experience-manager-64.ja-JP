---
title: Document Security によって保護された PDF ドキュメントと Microsoft Office ドキュメントを AEM で検索可能にする
seo-title: Enable AEM to search document security protected PDF and Microsoft Office documents
description: 'ネイティブ AEM 検索を有効にし、DRM 保護された PDF ドキュメントで全テキストの検索を実行する方法について説明します。  '
seo-description: Learn how to enable native AEM search to perform full-text search on DRM protected PDF documents.
uuid: dba882f8-bad4-4122-a0df-03cf087afb23
content-type: reference
geptopics: SG_AEMFORMS/categories/working_with_document_security
products: SG_EXPERIENCEMANAGER/6.4/FORMS
discoiquuid: 7eebef08-83b9-4b56-90ec-35ab3b0c27e8
noindex: true
feature: Document Security
exl-id: dbf97dc1-cf05-4d45-859e-60ff01186e51
source-git-commit: bd94d3949f0117aa3e1c9f0e84f7293a5d6b03b4
workflow-type: tm+mt
source-wordcount: '643'
ht-degree: 100%

---

# Document Security によって保護された PDF ドキュメントと Microsoft Office ドキュメントを AEM で検索可能にする{#enable-aem-to-search-document-security-protected-pdf-and-microsoft-office-documents}

Adobe Experience Manager には、AEM に保存された様々なアセットを検索し、その場所を特定するためのユーザーインターフェイスが用意されています。ネイティブ検索機能を使用して AEM アセットを検索し共通して使用されるドキュメント形式（プレーンテキストファイル、Microsoft Office ドキュメント、PDF ドキュメントなど）でテキスト検索を実行することができます。ネイティブ検索を拡張して有効にし、DRM 保護された PDF ドキュメントと Microsoft Office ドキュメントで全テキストの検索を実行できるようにすることも可能です。

次の手順を実行し、Document Security によって保護された PDF ドキュメントと Microsoft Office ドキュメントを AEM で検索可能にします。

## 事前準備 {#before-you-start}

* AEM Forms Document Security をインストールして設定します。
* sun.util.calendar パッケージを&#x200B;**デシリアライゼーションファイアウォール設定の許可リストに追加します。**&#x200B;設定は `https://[server]:[port]/system/console/configMgr` にリストされます。
* すべての AEM バンドルが正常に実行していることを確認します。バンドルは `https://[server]:[port]/system/console/bundles` にリストされます。アクティブ状態になっていないバンドルが存在する場合、数分間待ってからバンドルの状態を確認してください。

## AEM Forms Workflow（JEE 上の AEM Forms）内での安全な接続の確立 {#establish-a-secure-connection-within-aem-forms-workflow-aem-forms-on-jee}

安全な接続は、JEE 上の AEM Forms と、同じサーバー上で実行している OSGi サービスとの間の情報の流れをシームレスにします。次のいずれかの方法を使用して安全な接続を確立します。

* JEE 上の AEM Forms の管理者資格情報を使用した AEM Forms Client SDK Bundle の設定
* 相互認証を使用した AEM Forms Client SDK Bundle の設定

### JEE 上の AEM Forms の管理者資格情報を使用した AEM Forms Client SDK Bundle の設定 {#configure-aem-forms-client-sdk-bundle-with-aem-forms-on-jee-admin-credentials}

1. AEM Configuration Manager を開き、管理者としてログインします。デフォルトの URL は https://&lt;serverName>:&lt;port>/lc/system/console/configMgr です。
1. AEM Forms Client SDK Bundle を探して開きます。次の各プロパティの値を指定します。

   * **サーバー URL**：JEE サーバー上の AEM Forms の HTTP URL を指定します。HTTPS 経由の通信を可能にするには、-Djavax.net.ssl.trustStore=&lt;JEE キーストアファイル上の AEM Forms のパス> のパラメーターを使用して、JEE サーバー上の AEM Forms を再起動します。
   * **サービス名**：指定されたサービスの一覧に RightsManagementService を追加します。
   * **ユーザー名：** JEE サーバー上の AEM Forms からの呼び出しの開始に使用される JEE アカウントの AEM Forms のユーザー名を指定します。指定したアカウントは、JEE サーバー上の AEM Forms で Document Services を呼び出すことができる権限が付与されている必要があります。
   * **パスワード**：「ユーザー名」フィールドに表示される JEE 上の AEM Forms アカウントのパスワードを指定します。

   「**保存**」をクリックします。AEM は、Document Security によって保護された PDF ドキュメントと Microsoft Office ドキュメントの検索が有効になっています。

### 相互認証を使用した AEM Forms Client SDK Bundle の設定 {#configure-aem-forms-client-sdk-bundle-using-mutual-authentication}

1. JEE 上の AEM Forms の相互認証を有効にします。詳しくは、「[CAC および相互認証](https://helpx.adobe.com/jp/livecycle/kb/cac-mutual-authentication.html)」を参照してください。
1. AEM Configuration Manager を開き、管理者としてログインします。デフォルトの URL は https://&lt;serverName>:&lt;port>/lc/system/console/configMgr です。
1. AEM Forms Client SDK Bundle を探して開きます。次の各プロパティの値を指定します。

   * **サーバー URL**：JEE サーバー上の AEM Forms の HTTPS URL を指定します。HTTPS 経由の通信を可能にするには、-Djavax.net.ssl.trustStore=&lt;JEE キーストアファイル上の AEM Forms のパス> のパラメーターを使用して、JEE サーバー上の AEM Forms を再起動します。
   * **2way SSL の有効化**：「2way SSL の有効化」オプションを有効にします。
   * **キーストアファイル URL**：キーストアファイルの URL を指定します。
   * **TrustStore ファイル URL**：Truststore ファイルの URL を指定します。
   * **キーストアパスワード**：キーストアファイルのパスワードを指定します。
   * **TrustStore パスワード**：Truststore ファイルのパスワードを指定します。
   * **サービス名**：指定されたサービスの一覧に RightsManagementService を追加します。

   「**保存**」をクリックします。AEM は、Document Security によって保護された PDF ドキュメントと Microsoft Office ドキュメントの検索が有効になっています。

## サンプルポリシーで保護された PDF ドキュメントまたは Microsoft Office ドキュメントのインデックス作成 {#index-a-sample-policy-protected-pdf-or-microsoft-office-document}

1. 管理者として AEM Assets にログインします。
1. AEM Digital Asset Manager でフォルダーを作成し、新しく作成したフォルダーにポリシーで保護された PDF ドキュメントまたは Microsoft Office ドキュメントをアップロードします。これで AEM 検索を使用してポリシーで保護されたドキュメントのコンテンツを検索できます。検索したテキストを含むドキュメントが返されます。
