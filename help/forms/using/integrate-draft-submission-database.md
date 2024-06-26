---
title: ドラフトと送信コンポーネントとデータベースの統合のサンプル
seo-title: Sample for integrating drafts & submissions component with database
description: ドラフトと送信コンポーネントをデータベースに統合するためのカスタマイズされたデータサービスとメタデータサービスの参照実装。
seo-description: Reference implementation of customized data and metadata services to integrate drafts and submissions component with a database.
uuid: ccdb900e-2c2e-4ed3-8a88-5c97aa0092a1
content-type: reference
products: SG_EXPERIENCEMANAGER/6.4/FORMS
topic-tags: publish
discoiquuid: da96d3d8-a338-470a-8d20-55ea39bd15bf
exl-id: 4d13d69b-1fe6-4fb6-9e3e-3ad0c5ffb829
source-git-commit: c5b816d74c6f02f85476d16868844f39b4c47996
workflow-type: tm+mt
source-wordcount: '1503'
ht-degree: 43%

---

# ドラフトと送信コンポーネントとデータベースの統合のサンプル {#sample-for-integrating-drafts-submissions-component-with-database}

>[!CAUTION]
>
>AEM 6.4 の拡張サポートは終了し、このドキュメントは更新されなくなりました。 詳細は、 [技術サポート期間](https://helpx.adobe.com/jp/support/programs/eol-matrix.html). サポートされているバージョンを見つける [ここ](https://experienceleague.adobe.com/docs/?lang=ja).

## サンプルの概要 {#sample-overview}

AEM Forms Portal のドラフトと送信コンポーネントを使用すると、ユーザーはフォームをドラフトとして保存し、任意のデバイスから後で送信できます。 また、ユーザーは、ポータル上で送信済みのフォームを表示することもできます。 この機能を有効にするために、AEM Formsでは、ユーザーがフォームに入力したデータと、ドラフトおよび送信済みフォームに関連付けられたフォームメタデータを保存するデータおよびメタデータサービスを提供しています。 このデータは、デフォルトで CRX リポジトリに保存されます。 ただし、ユーザーがAEMパブリッシュインスタンスを通じてフォームを操作する場合は、通常はエンタープライズファイアウォールの外部にあり、より安全で信頼性の高いデータストレージをカスタマイズする必要が生じる場合があります。

このドキュメントで説明するサンプルは、ドラフトと送信コンポーネントをデータベースに統合するためにカスタマイズされたデータサービスとメタデータサービスのリファレンス実装です。 このサンプル実装で使用されるデータベースは次のとおりです。 **MySQL 5.6.24**. ただし、ドラフトと送信コンポーネントは、任意のデータベースに統合できます。

>[!NOTE]
>
>* このドキュメントで説明する例と設定は MySQL 5.6.24 に基づいているので、データベースシステムに合わせて適切に置き換える必要があります。
>* 最新バージョンのAEM Formsアドオンパッケージがインストールされていることを確認してください。 使用可能なパッケージの一覧については、 [AEM Formsリリース](https://helpx.adobe.com/jp/aem-forms/kb/aem-forms-releases.html) 記事。
>* サンプルパッケージは、アダプティブフォーム送信アクションでのみ機能します。


## サンプルのセットアップおよび設定 {#set-up-and-configure-the-sample}

すべてのオーサーインスタンスとパブリッシュインスタンスで、次の手順を実行し、サンプルをインストールして設定します。

1. パッケージ **aem-fp-db-integration-sample-pkg-6.1.2.zip** をファイルシステムにダウンロードします。

   データベース統合用のサンプルパッケージ

[ファイルを入手](assets/aem-fp-db-integration-sample-pkg-6.1.2.zip)

1. AEM パッケージマネージャー（https://[*host*]:[*port*]/crx/packmgr/）に移動します。
1. 「**[!UICONTROL パッケージをアップロード]**」をクリックします。

1. パッケージ **aem-fp-db-integration-sample-pkg-6.1.2.zip** を参照して選択し、「**[!UICONTROL OK]**」をクリックします。
1. クリック **[!UICONTROL インストール]** をクリックします。
1. **[!UICONTROL AEM web コンソール設定]**
ページ（https://[*host*]:[*port*]/system/console/configMgr）に移動します。
1. **[!UICONTROL Forms Portal Draft and Submission Configuration]** をクリックし、編集モードで開きます。

1. 次の表の説明に従って、プロパティの値を指定します。

   | **プロパティ** | **説明** | **値** |
   |---|---|---|
   | Forms Portal Draft Data Service | ドラフトデータサービスの識別子 | formsportal.sampledataservice |
   | Forms Portal Draft Metadata Service | ドラフトメタデータサービスの識別子 | formsportal.samplemetadataservice |
   | Forms Portal データ送信サービス | 送信データサービスの識別子 | formsportal.sampledataservice |
   | Forms Portal 送信メタデータサービス | 送信メタデータサービスの識別子 | formsportal.samplemetadataservice |
   | Forms Portal 保留中の署名データサービス | 保留中署名データサービスの識別子 | formsportal.sampledataservice |
   | Forms Portal 保留中の署名メタデータサービス | 保留中署名メタデータサービスの識別子 | formsportal.samplemetadataservice |

   >[!NOTE]
   >
   >サービスは、`aem.formsportal.impl.prop` キーの値として以下に記述されている名前によって解決されます。

   ```java
   @Service(value = {SubmitDataService.class, DraftDataService.class})
   @Property(name = "aem.formsportal.impl.prop", value = "formsportal.sampledataservice")
   @Service(value = { SubmitMetadataService.class, DraftMetadataService.class })
   @Property(name = "aem.formsportal.impl.prop", value = "formsportal.samplemetadataservice")
   ```

   データテーブルとメタデータテーブルの名前を変更できます。

   メタデータテーブルに別の名前を指定するには：

   * Web コンソール設定で、「 Forms Portal Metadata Service Sample Implementation 」を探してクリックします。 データソース、メタデータ/追加のメタデータテーブル名の値を変更できます。

   データテーブルに別の名前を指定するには、次の手順に従います。

   * Web コンソール設定で、「 Forms Portal Data Service Sample Implementation 」を探してクリックします。 データソースとデータテーブル名の値は変更できます。
   >[!NOTE]
   >
   >テーブル名を変更する場合は、テーブル名をフォームポータル設定に入力してください。

1. 他の設定はそのままにし、「**[!UICONTROL 保存]**」をクリックします。

1. データベース接続は、Apache Sling Connection Pooled Data Source 経由で実行できます。
1. Apache Sling 接続の場合は、を探してクリックし、を開きます。 **[!UICONTROL Apache Sling 接続プールに入れられたデータソース]** Web コンソール設定の編集モード 次の表の説明に従って、プロパティの値を指定します。

<table> 
 <tbody> 
  <tr> 
   <td><strong>プロパティ</strong></td> 
   <td><strong>値</strong></td> 
  </tr> 
  <tr> 
   <td>データソース名</td> 
   <td><p>データソースプールからドライバーをフィルタリングするためのデータソース名</p> <p><strong>注意： </strong><em>このサンプル実装環境では、データソース名として FormsPortal を使用しています。</em></p> </td> 
  </tr> 
  <tr> 
   <td>JDBC driver class</td> 
   <td>com.mysql.jdbc.Driver</td> 
  </tr> 
  <tr> 
   <td>JDBC 接続 URI<br /> </td> 
   <td>jdbc:mysql://[<em>host</em>]:[<em>port</em>]/[<em>schema_name</em>]</td> 
  </tr> 
  <tr> 
   <td>ユーザー名</td> 
   <td>データベーステーブルでアクションを認証および実行するためのユーザー名</td> 
  </tr> 
  <tr> 
   <td>パスワード</td> 
   <td>ユーザー名に関連付けられたパスワード</td> 
  </tr> 
  <tr> 
   <td>トランザクションの分離</td> 
   <td>READ_COMMITTED</td> 
  </tr> 
  <tr> 
   <td>最大アクティブ接続数</td> 
   <td>1000</td> 
  </tr> 
  <tr> 
   <td>最大アイドル接続数</td> 
   <td>100</td> 
  </tr> 
  <tr> 
   <td>最小アイドル接続</td> 
   <td>10</td> 
  </tr> 
  <tr> 
   <td>初期サイズ</td> 
   <td>10</td> 
  </tr> 
  <tr> 
   <td>最大待機時間</td> 
   <td>100000</td> 
  </tr> 
  <tr> 
   <td>借りてテスト</td> 
   <td>チェック</td> 
  </tr> 
  <tr> 
   <td>待機中にテスト</td> 
   <td>チェック</td> 
  </tr> 
  <tr> 
   <td>検証クエリ</td> 
   <td>値の例は SELECT 1(mysql)、select 1 from dual(oracle)、SELECT 1(MS Sql Server) (validationQuery) です。</td> 
  </tr> 
  <tr> 
   <td>検証クエリのタイムアウト</td> 
   <td>10000</td> 
  </tr> 
 </tbody> 
</table>

>[!NOTE]
>
> * MySQL 用の JDBC ドライバーは、サンプルには付属していません。 JDBC 接続プールの設定に必要な情報を提供し、プロビジョニングを完了していることを確認します。
> * 同じデータベースを使用するようにオーサーインスタンスとパブリッシュインスタンスを指定します。 JDBC 接続 URI フィールドの値は、すべてのオーサーインスタンスとパブリッシュインスタンスで同じにする必要があります。
   >


1. 他の設定はそのままにし、「**[!UICONTROL 保存]**」をクリックします。

1. データベーススキーマに既にテーブルがある場合は、次の手順に進んでください。

   データベーススキーマにテーブルがまだない場合は、次の SQL ステートメントを実行して、データベーススキーマ内にデータ、メタデータおよび追加のメタデータ用の別々のテーブルを作成します。

   >[!NOTE]
   >
   >オーサーインスタンスとパブリッシュインスタンス用に異なるデータベースを必要としない。 すべてのオーサーインスタンスとパブリッシュインスタンスで同じデータベースを使用します。

   **データ表用の SQL ステートメント**

   ```sql
   CREATE TABLE `data` (
   `owner` varchar(255) DEFAULT NULL,
   `data` longblob,
   `metadataId` varchar(45) DEFAULT NULL,
   `id` varchar(45) NOT NULL,
   PRIMARY KEY (`id`)
   ) ENGINE=InnoDB DEFAULT CHARSET=utf8;
   ```

   **メタデータ表用の SQL ステートメント**

   ```sql
   CREATE TABLE `metadata` ( 
   `formPath` varchar(1000) DEFAULT NULL,
   `formType` varchar(100) DEFAULT NULL,
   `description` text,
   `formName` varchar(255) DEFAULT NULL,
   `owner` varchar(255) DEFAULT NULL,
   `enableAnonymousSave` varchar(45) DEFAULT NULL,
   `renderPath` varchar(1000) DEFAULT NULL,
   `nodeType` varchar(45) DEFAULT NULL,
   `charset` varchar(45) DEFAULT NULL,
   `userdataID` varchar(45) DEFAULT NULL,
   `status` varchar(45) DEFAULT NULL,
   `formmodel` varchar(45) DEFAULT NULL,
   `markedForDeletion` varchar(45) DEFAULT NULL,
   `showDorClass` varchar(255) DEFAULT NULL,
   `sling:resourceType` varchar(1000) DEFAULT NULL,
   `attachmentList` longtext,
   `draftID` varchar(45) DEFAULT NULL,
   `submitID` varchar(45) DEFAULT NULL,
   `id` varchar(60) NOT NULL,
   `profile` varchar(255) DEFAULT NULL,
   `submitUrl` varchar(1000) DEFAULT NULL,
   `xdpRef` varchar(1000) DEFAULT NULL,
   `agreementId` varchar(255) DEFAULT NULL,
   `nextSigners` varchar(255) DEFAULT NULL,
   `eSignStatus` varchar(45) DEFAULT NULL,
   `pendingSignID` varchar(45) DEFAULT NULL,
   `agreementDataId` varchar(255) DEFAULT NULL,
   `enablePortalSubmit` varchar(45) DEFAULT NULL,
   `submitType` varchar(45) DEFAULT NULL,
   `dataType` varchar(45) DEFAULT NULL,
   `jcr:lastModified` varchar(45) DEFAULT NULL,
   PRIMARY KEY (`id`),
   UNIQUE KEY `ID_UNIQUE` (`id`)
   ) ENGINE=InnoDB DEFAULT CHARSET=utf8;
   ```

   **追加メタデータテーブル用の SQL ステートメント**

   ```sql
   CREATE TABLE `additionalmetadatatable` (
   `value` text,
   `key` varchar(255) NOT NULL,
   `id` varchar(60) NOT NULL,
   PRIMARY KEY (`id`,`key`),
   CONSTRAINT ‘additionalmetadatatable_fk’ FOREIGN KEY (`id`) REFERENCES `metadata` (`id`) ON DELETE CASCADE
   ) ENGINE=InnoDB DEFAULT CHARSET=utf8;
   ```

   **コメントテーブル用の SQL ステートメント**

   ```sql
   CREATE TABLE `commenttable` (
   `commentId` varchar(255) DEFAULT NULL,
   `comment` text DEFAULT NULL,
   `ID` varchar(255) DEFAULT NULL,
   `commentowner` varchar(255) DEFAULT NULL,
   `time` varchar(255) DEFAULT NULL);
   ```

1. データベーススキーマに既にテーブル（data、metadata および additionalmetadatatable）がある場合は、次の altertable クエリを実行します。

   **データテーブルを変更する SQL ステートメント**

   ```sql
   ALTER TABLE `data` CHANGE `owner` `owner` VARCHAR(255) CHARACTER SET utf8 COLLATE utf8_general_ci NULL DEFAULT NULL;
   ```

   **メタデータテーブルを変更する SQL ステートメント**

   ```sql
   ALTER TABLE metadata add markedForDeletion varchar(45) DEFAULT NULL
   ```

   >[!NOTE]
   >
   >ALTER TABLE metadata add クエリがすでに実行済みで、markedfordeletion 列がテーブルにある場合は、このクエリを実行すると失敗します。

   ```sql
   ALTER TABLE metadata add agreementId varchar(255) DEFAULT NULL,
   add nextSigners varchar(255) DEFAULT NULL, 
   add eSignStatus varchar(45) DEFAULT NULL,
   add pendingSignID varchar(45) DEFAULT NULL,
   add agreementDataId varchar(255) DEFAULT NULL,
   add enablePortalSubmit varchar(45) DEFAULT NULL,
   add submitType varchar(45) DEFAULT NULL,
   add dataType varchar(45) DEFAULT NULL;
   ```

   ```sql
   ALTER TABLE `metadata` CHANGE `formPath` `formPath` VARCHAR(1000) CHARACTER SET utf8 COLLATE utf8_general_ci NULL DEFAULT NULL,
   CHANGE `formType` `formType` VARCHAR(100) CHARACTER SET utf8 COLLATE utf8_general_ci NULL DEFAULT NULL,
   CHANGE `description` `description` TEXT CHARACTER SET utf8 COLLATE utf8_general_ci NULL DEFAULT NULL,
   CHANGE `formName` `formName` VARCHAR(255) CHARACTER SET utf8 COLLATE utf8_general_ci NULL DEFAULT NULL,
   CHANGE `owner` `owner` VARCHAR(255) CHARACTER SET utf8 COLLATE utf8_general_ci NULL DEFAULT NULL,
   CHANGE `renderPath` `renderPath` VARCHAR(1000) CHARACTER SET utf8 COLLATE utf8_general_ci NULL DEFAULT NULL,
   CHANGE `showDorClass` `showDorClass` VARCHAR(255) CHARACTER SET utf8 COLLATE utf8_general_ci NULL DEFAULT NULL,
   CHANGE `sling:resourceType` `sling:resourceType` VARCHAR(1000) CHARACTER SET utf8 COLLATE utf8_general_ci NULL DEFAULT NULL,
   CHANGE `profile` `profile` VARCHAR(255) CHARACTER SET utf8 COLLATE utf8_general_ci NULL DEFAULT NULL,
   CHANGE `submitUrl` `submitUrl` VARCHAR(1000) CHARACTER SET utf8 COLLATE utf8_general_ci NULL DEFAULT NULL,
   CHANGE `xdpRef` `xdpRef` VARCHAR(1000) CHARACTER SET utf8 COLLATE utf8_general_ci NULL DEFAULT NULL;
   ```

   **additionalmetadatatable テーブルを変更する SQL ステートメント**

   ```sql
   ALTER TABLE `additionalmetadatatable` CHANGE `value` `value` TEXT CHARACTER SET utf8 COLLATE utf8_general_ci NULL DEFAULT NULL, CHANGE `key` `key` VARCHAR(255) CHARACTER SET utf8 COLLATE utf8_general_ci NOT NULL;
   ```

サンプル実装が設定され、すべてのデータとメタデータをデータベースに保存しながら、ドラフトと送信をリストするのに使用できます。 次に、サンプルでデータサービスとメタデータサービスがどのように設定されているかを見てみましょう。

## mysql-connector-java-5.1.39-bin.jar ファイルをインストールする {#install-mysql-connector-java-bin-jar-file}

すべてのオーサーインスタンスとパブリッシュインスタンスで、次の手順を実行し、mysql-connector-java-5.1.39-bin.jar ファイルをインストールします。

1. `https://[server]:[port]/system/console/depfinder` にアクセスして com.mysql.jdbc パッケージを検索します。
1. 「次による書き出し」列で、パッケージがバンドルで書き出されているかどうかを確認します。

   パッケージがバンドルで書き出されていない場合は、先に進みます。

1. `https://[server]:[port]/system/console/bundles` に移動して「**[!UICONTROL Install/Update]**」をクリックします。
1. 「**[!UICONTROL ファイルを選択]**」をクリックし、mysql-connector-java-5.1.39-bin.jar を探して選択します。また、「**[!UICONTROL Start Bundle]**」チェックボックスと「**[!UICONTROL Refresh Packages]**」チェックボックスを選択します。
1. 「**[!UICONTROL Install」または「Update]**」をクリックします。完了したら、サーバーを再起動します。
1. （*Windows のみ*）オペレーティングシステムのシステムファイアウォールをオフにします。

## フォームポータルデータおよびメタデータサービスのサンプルコード {#sample-code-for-forms-portal-data-and-metadata-service}

次の zip ファイルには、データおよびメタデータサービスインターフェイスの `FormsPortalSampleDataServiceImpl` および `FormsPortalSampleMetadataServiceImpl`（実装クラス）が含まれます。また、上記で述べた実装クラスのコンパイルに必要なすべてのクラスが含まれます。

[ファイルを入手](assets/sample_package.zip)

## ファイル名の長さを検証  {#verify-length-of-the-file-name}

Forms Portal のデータベース実装では、追加のメタデータテーブルを使用します。 このテーブルには、テーブルのキーと id 列に基づく複合プライマリキーが含まれます。 MySQL では、255 文字までのプライマリキーを使用できます。 次のクライアント側検証スクリプトを使用して、ファイルウィジェットに添付されるファイル名の長さを検証できます。 検証は、ファイルが添付されると実行されます。 次の手順で指定したスクリプトは、ファイル名が 150（拡張子を含む）より大きい場合に、メッセージを表示します。 スクリプトを変更して、異なる文字数でチェックできます。

次の手順を実行して、 [クライアントライブラリ](/help/sites-developing/clientlibs.md) スクリプトを使用します。

1. CRXDE にログインし、 /etc/clientlibs/に移動します。
1. タイプのノードの作成 **cq:ClientLibraryFolder** ノード名を指定します。 （例：`validation`）。

   「**[!UICONTROL すべて保存]**」をクリックします。

1. ノードを右クリックして「**[!UICONTROL 新しいファイルを作成]**」をクリックし、.txt の拡張子を付けてファイルを作成します。例えば、`js.txt` です。新しく作成した .txt ファイルに次のコードを追加して、「**[!UICONTROL すべて保存]**」をクリックします。

   ```
   #base=util 
    util.js
   ```

   上記コードの場合、`util` はフォルダーの名前で、`util.js` フォルダーにあるファイルの `util` 名です。`util` フォルダーと `util.js` ファイルはこの後に続く手順で作成されます。

1. 手順 2 で作成した `cq:ClientLibraryFolder` ノードを右クリックし、「作成／フォルダーの作成」を選択します。`util` という名前のフォルダーを作成します。「**[!UICONTROL すべて保存]**」をクリックします。`util` フォルダーを右クリックし、「作成／ファイルを作成」を選択します。`util.js` という名前のファイルを作成します。「**[!UICONTROL すべて保存]**」をクリックします。

1. util.js ファイルに次のコードを追加して、「**[!UICONTROL すべて保存]**」をクリックします。このコードでファイル名の長さを検証します。

   ```
   /*
    * ADOBE CONFIDENTIAL
    * ___________________
    *
    * Copyright 2016 Adobe Systems Incorporated
    * All Rights Reserved.
    *
    * NOTICE:  All information contained herein is, and remains
    * the property of Adobe Systems Incorporated and its suppliers,
    * if any.  The intellectual and technical concepts contained
    * herein are proprietary to Adobe Systems Incorporated and its
    * suppliers and may be covered by U.S. and Foreign Patents,
    * patents in process, and are protected by trade secret or copyright law.
    * Dissemination of this information or reproduction of this material
    * is strictly forbidden unless prior written permission is obtained
    * from Adobe Systems Incorporated.
    *
    */
   (function () {
       var connectWithGuideBridge = function (gb) {
           gb.connect(function () {
               //For first time load
               window.guideBridge.on("elementValueChanged" , function(event, payload) {
           var component = payload.target; // Field whose value has changed
                   if(component.name == 'fileAttachment' && component.parent) {
                       var fileItems = $('#'+payload.target.parent.id).find(".guide-fu-fileItem");
                       for (i = 0;i<fileItems.length;i++) {
                           var filename = $(fileItems[i]).find(".guide-fu-fileName").text();
                           //check whether it is previously attached file or a newly  attached one
                           if(filename.length > 150 && filename.indexOf("fp.attach.jsp") < 0) {
                               window.alert("filename is larger than 150 : "+filename);
                                $(fileItems[i]).find(".guide-fu-fileClose.close").click();
                           }
                       }
                   }
   
      });
           });
       };
   
       if (window.guideBridge) {
           connectWithGuideBridge(window.guideBridge);
       } else {
           window.addEventListener("bridgeInitializeStart", function (event) {
               connectWithGuideBridge(event.detail.guideBridge);
           });
       }
   })();
   ```

   >[!NOTE]
   >
   >このスクリプトは、標準 (OOTB) 添付ウィジェットコンポーネント用です。 OOTB 添付ウィジェットをカスタマイズした場合は、上記のスクリプトを変更して、それぞれの変更を組み込みます。

1. 手順 2 で作成したフォルダーに次のプロパティを追加し、「 」をクリックします。 **[!UICONTROL すべて保存]**.

   * **[!UICONTROL 名前：]** categories

   * **[!UICONTROL タイプ：]** String

   * **[!UICONTROL 値：]** fp.validation

   * **[!UICONTROL マルチオプション：]** Enabled

1. `/libs/fd/af/runtime/clientlibs/guideRuntime` に移動し、`fp.validation` 値を embed プロパティに追加します。****

1. /libs/fd/af/runtime/clientlibs/guideRuntimeWithXFA に移動し、`fp.validation` 値を embed プロパティに追加します。****

   >[!NOTE]
   >
   >guideRuntime および guideRuntimeWithXfa クライアントライブラリの代わりにカスタムクライアントライブラリを使用している場合、カテゴリ名を使用してこの手順で作成したクライアントライブラリを、実行時にロードしたカスタムライブラリに埋め込みます。

1. 「**[!UICONTROL すべて保存」をクリックします。]** ここで、ファイル名が拡張子を含めて 150 文字を超えるとメッセージが表示されます。
