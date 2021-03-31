---
title: Smart Content Serviceを使用してアセットのタグ付けを設定します。
description: Smart Content Serviceを使用して、 [!DNL Adobe Experience Manager]でスマートタグを設定し、高度なスマートタグを設定する方法を説明します。
contentOwner: AG
feature: スマートタグ，タグ付け
role: Administrator
translation-type: tm+mt
source-git-commit: 29e3cd92d6c7a4917d7ee2aa8d9963aa16581633
workflow-type: tm+mt
source-wordcount: '1216'
ht-degree: 47%

---


# Smart Content Service {#configure-asset-tagging-using-the-smart-content-service}を使用してアセットタグを設定

[!DNL Adobe Experience Manager]は、[!DNL Adobe Developer Console]を使用してSmart Content Serviceと統合できます。 [!DNL Experience Manager]内からSmart Content Serviceにアクセスするには、この設定を使用します。

この記事では、スマートコンテンツサービスの設定に必要となる以下の主要なタスクについて詳しく説明します。バックエンドで、[!DNL Experience Manager]サーバーは、要求をSmart Content Serviceに転送する前に、[!DNL Adobe Developer Console]ゲートウェイを使用してサービス資格情報を認証します。

1. [ でスマートコンテンツサービス設定を作成して、公開鍵を生成します。](#obtain-public-certificate)[!DNL Experience Manager]OAuth 統合用の[公開証明書を取得します](#obtain-public-certificate)。

1. [Adobe 開発者コンソールで統合を作成](#create-adobe-i-o-integration)し、生成した公開鍵をアップロードします。

1. [から取得したAPIキーと他の秘密鍵証明書を使用して、](#configure-smart-content-service) デプロイを設定 [!DNL Adobe Developer Console]します。

1. [設定をテストします](#validate-the-configuration)。

1. 必要に応じて、[アセットのアップロード時に自動タグ付けを有効にする](#enable-smart-tagging-in-the-update-asset-workflow-optional)。

## 前提条件 {#prerequisites}

Smart Content Serviceを使用する前に、次の手順を実行して[!DNL Adobe Developer Console]上に統合を作成します。

* 組織の管理者権限を持つ Adobe ID アカウントがあること。

* Smart Content Serviceが組織で有効になっている。

拡張スマートタグを有効にするには、上記に加えて、最新の[Experience Managerサービスパック](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/aem-releases-updates.html?lang=ja)もインストールします。

## 公開証明書を取得するためのSmart Content Service設定の作成{#obtain-public-certificate}

公開証明書を使用すると、[!DNL Adobe Developer Console]でプロファイルを認証できます。

1. [!DNL Experience Manager]ユーザーインターフェイスで、**[!UICONTROL ツール]**/**[!UICONTROL Cloud Services]**/**[!UICONTROL レガシーCloud Services]**&#x200B;にアクセスします。

1. Cloud Servicesページで、「**[!UICONTROL アセットのスマートタグ]**」の下の「今すぐ設定&#x200B;]**」をクリックします。**[!UICONTROL 

1. **[!UICONTROL 設定を作成]**&#x200B;ダイアログで、スマートタグ設定のタイトルと名前を指定します。「**[!UICONTROL 作成]**」をクリックします。

1. **[!UICONTROL AEM スマートコンテンツサービス]**&#x200B;ダイアログで、以下の値を使用します。

   **[!UICONTROL サービス URL]**: `https://mc.adobe.io/marketingcloud/smartcontent`

   **[!UICONTROL 認証サーバー]**: `https://ims-na1.adobelogin.com`

   その他のフィールドは現時点では空白のままにします（後で指定します）。「**[!UICONTROL OK]**」をクリックします。

   ![コンテンツサービスURLを提供するExperience Managerスマートコンテンツサービスダイアログ](assets/aem_scs.png)


   *図：コンテンツサービスURLを提供する「Smart Content Service」ダイアログ*

   >[!NOTE]
   >
   >[!UICONTROL サービスURL]として指定されたURLは、ブラウザーを介してアクセスできず、404エラーが発生します。 この設定は、[!UICONTROL Service URL]パラメーターと同じ値で正常に機能します。 全体的なサービスの状態とメンテナンスのスケジュールについては、[https://status.adobe.com](https://status.adobe.com)を参照してください。

1. 「**[!UICONTROL OAuth統合用の公開証明書をダウンロード]**」をクリックし、公開証明書ファイル`AEM-SmartTags.crt`をダウンロードします。

   ![スマートタグ付けサービス用に作成された設定の表現](assets/smart-tags-download-public-cert.png)


   *図：スマートタグサービスの設定*

### 証明書の有効期限が切れた場合に再設定{#certrenew}

証明書の有効期限が切れると、信頼されなくなります。 期限切れの証明書は更新できません。新しい証明書を追加するには、以下の手順に従います。

1. [!DNL Experience Manager] デプロイメントに管理者としてログインします。**[!UICONTROL ツール]**／**[!UICONTROL セキュリティ]**／**[!UICONTROL ユーザー]**&#x200B;をクリックします。

1. **[!UICONTROL dam-update-service]** ユーザーを見つけてクリックします。「**[!UICONTROL キーストア]**」タブをクリックします。

1. 証明書の有効期限が切れた既存の **[!UICONTROL similaritysearch]** キーストアを削除します。「**[!UICONTROL 保存して閉じる]**」をクリックします。

   ![キーストア内の既存の類似性検索エントリを削除し、新しいセキュリティ証明書を追加します](assets/smarttags_delete_similaritysearch_keystore.png)

   *図：キーストアの既存の `similaritysearch` エントリを削除して新しいセキュリティ証明書を追加.*

1. **[!UICONTROL ツール]**／**[!UICONTROL クラウドサービス]**／**[!UICONTROL 従来のクラウドサービス]**&#x200B;に移動します。**[!UICONTROL アセットのスマートタグ]**／**[!UICONTROL 設定を表示]**／**[!UICONTROL 利用可能な設定]**&#x200B;をクリックします。必要な設定をクリックします。

1. 公開証明書をダウンロードするには、「**[!UICONTROL OAuth 統合用の公開証明書をダウンロード]**」をクリックします。

1. [https://console.adobe.io](https://console.adobe.io) にアクセスし、**[!UICONTROL 統合]**&#x200B;ページで既存のスマートコンテンツサービスに移動します。新しい証明書をアップロードします。詳しくは、[Adobe開発者コンソール統合の作成](#create-adobe-i-o-integration)の手順を参照してください。

## Adobe開発者コンソール統合の作成{#create-adobe-i-o-integration}

Smart Content Service APIを使用するには、Adobe開発者コンソールで統合を作成して、[!UICONTROL APIキー](Adobe開発者コンソール統合の[!UICONTROL CLIENT ID]フィールドで生成)、[!UICONTROL 技術的なアカウントID]、[!UICONTROL ORGANIZATIONを取得します[!UICONTROL アセットのスマートタグサービス設定]のID]と[!UICONTROL CLIENT SECRET]（[!DNL Experience Manager]のクラウド設定）。

1. ブラウザーで [https://console.adobe.io](https://console.adobe.io/) にアクセスします。適切なアカウントを選択し、関連付けられた組織の役割がシステム管理者であることを確認します。

1. 任意の名前でプロジェクトを作成します。「**[!UICONTROL API を追加]**」をクリックします。

1. **[!UICONTROL 追加API]**&#x200B;ページで、**[!UICONTROL Experience Cloud]**&#x200B;を選択し、**[!UICONTROL スマートコンテンツ]**&#x200B;を選択します。 「**[!UICONTROL 次へ]**」をクリックします。

1. 「**[!UICONTROL 公開鍵をアップロード]**」を選択します。[!DNL Experience Manager]からダウンロードした証明書ファイルを指定します。[!UICONTROL 公開鍵が正常にアップロード]されたというメッセージが表示されます。「**[!UICONTROL 次へ]**」をクリックします。

   [!UICONTROL 新しいサービスアカウント（JWT）秘密鍵証明書を作成]ページには、設定したサービスアカウントの公開鍵が表示されます。

1. 「**[!UICONTROL 次へ]**」をクリックします。

1. **[!UICONTROL 製品プロファイルを選択]**&#x200B;ページで、「**[!UICONTROL スマートコンテンツサービス]**」を選択します。「**[!UICONTROL 設定済み API を保存]**」をクリックします。

   設定に関する詳細情報がページに表示されます。このページを開いたままにして、スマートタグを設定するには、[!DNL Experience Manager]のクラウド設定の[!UICONTROL Assets Smart Tagging Service Settings]にこれらの値をコピーして追加します。

   ![「概要」タブで、統合について指定した情報を確認できます。](assets/integration_details.png)

   *図：Adobeデベロッパーコンソールの統合の詳細*

## スマートコンテンツサービスの設定 {#configure-smart-content-service}

統合を設定するには、Adobeデベロッパーコンソール統合の[!UICONTROL TECHNICAL ACCOUNT ID]、[!UICONTROL ORGANIZATION ID]、[!UICONTROL CLIENT SECRET]および[!UICONTROL CLIENT ID]フィールドの値を使用します。 Smart Tagsクラウド設定を作成すると、[!DNL Experience Manager]デプロイメントからAPIリクエストを認証できます。

1. [!DNL Experience Manager]で、**[!UICONTROL ツール/Cloud Service/レガシーCloud Services]**&#x200B;に移動し、[!UICONTROL Cloud Services]コンソールを開きます。

1. 「**[!UICONTROL アセットのスマートタグ]**」で、上記で作成した設定を開きます。サービスの設定ページで、「**[!UICONTROL 編集]**」をクリックします。

1. **[!UICONTROL AEM スマートコンテンツサービス]**&#x200B;ダイアログで、「**[!UICONTROL サービス URL]**」および「**[!UICONTROL 認証サーバー]**」フィールドに事前入力された値を使用します。

1. [!UICONTROL Apiキー]、[!UICONTROL テクニカルアカウントID]、[!UICONTROL 組織ID]、[!UICONTROL クライアントシークレット]の各フィールドに対して、[Adobe開発者コンソール](#create-adobe-i-o-integration)で生成された以下の値をコピーして使用します。

   | [!UICONTROL アセットのスマートタグサービス設定] | [!DNL Adobe Developer Console] 統合フィールド |
   |--- |--- |
   | [!UICONTROL API キー] | [!UICONTROL クライアントID] |
   | [!UICONTROL テクニカルアカウント ID] | [!UICONTROL テクニカルアカウントID] |
   | [!UICONTROL 組織 ID] | [!UICONTROL 組織ID] |
   | [!UICONTROL クライアントの秘密鍵] | [!UICONTROL CLIENT SECRET] |

## 設定の検証 {#validate-the-configuration}

設定が完了したら、JMX MBeanを使用して設定を検証します。 検証するには、次の手順に従います。

1. `https://[aem_server]:[port]`の[!DNL Experience Manager]サーバーにアクセスします。

1. **[!UICONTROL ツール／操作／Web コンソール]**&#x200B;に移動して、OSGi コンソールを開きます。**[!UICONTROL メイン／JMX]** を選択します。

1. 「**[!UICONTROL com.day.cq.dam.similaritysearch.internal.impl]**」をクリックします。**[!UICONTROL 類似性検索のその他のタスク]**&#x200B;を開きます。

1. 「**[!UICONTROL validateConfigs()]**」をクリックします。**[!UICONTROL 設定を検証]**&#x200B;ダイアログで、**[!UICONTROL 呼び出し]**&#x200B;をクリックします。

   検証結果は、同じダイアログに表示されます。

## DAMアセット更新ワークフローでのスマートタグの有効化（オプション） {#enable-smart-tagging-in-the-update-asset-workflow-optional}

1. [!DNL Experience Manager]で、**[!UICONTROL ツール]** > **[!UICONTROL ワークフロー]** > **[!UICONTROL モデル]**&#x200B;に移動します。

1. **[!UICONTROL ワークフローモデル]**&#x200B;ページで、「**[!UICONTROL DAM アセットの更新]**」ワークフローモデルを選択します。

1. ツールバーの「**[!UICONTROL 編集]**」をクリックします。

1. サイドパネルを展開して、ステップを表示します。「DAM ワークフロー」セクションの「**[!UICONTROL スマートタグアセット]**」ステップをドラッグして、「**[!UICONTROL サムネールを処理]**」ステップの後に配置します。

   ![「DAM アセットの更新」ワークフローで「サムネールを処理」ステップの後に「スマートタグアセット」ステップを追加](assets/smart-tag-in-dam-update-asset-workflow.png)

   *図：「DAM アセットの更新」ワークフローで「サムネールを処理」ステップの後に「スマートタグアセット」ステップを追加。*

1. そのステップを編集モードで開きます。「**[!UICONTROL 詳細設定]**」で、「**[!UICONTROL ハンドラー処理の設定]**」オプションが選択されていることを確認します。

   ![DAM更新アセットワークフローの設定とスマートタグ手順の追加](assets/smart-tag-step-properties-workflow1.png)


   *図：DAM更新アセットワークフローの設定とスマートタグ手順の追加*

1. 自動タグ付けのステップに失敗してもワークフローを完了させたい場合は、「**[!UICONTROL 引数]**」タブで「**[!UICONTROL エラーを無視]**」を選択します。

   ![DAMアセットの更新ワークフローを設定し、スマートタグ手順を追加してハンドラーの設定を選択します](assets/smart-tag-step-properties-workflow2.png)


   *図：DAMアセットの更新ワークフローを設定し、スマートタグ手順を追加してハンドラーの設定を選択します*

   フォルダーでスマートタグが有効になっているかに関わらずアップロード時にアセットをタグ付けするには、「**[!UICONTROL スマートタグフラグを無視]**」を選択します。

   ![DAM Update Assetワークフローを設定し、スマートタグ手順を追加して、「スマートタグフラグを無視」を選択します](assets/smart-tag-step-properties-workflow3.png)


   *図：DAM Update Assetワークフローを設定し、スマートタグ手順を追加して、「スマートタグフラグを無視」を選択します*

1. 「**[!UICONTROL OK]**」をクリックして、プロセスステップを閉じ、ワークフローを保存します。

>[!MORELIKETHIS]
>
>* [スマートタグの管理](managing-smart-tags.md)
>* [スマートタグの概要とトレーニング方法](enhanced-smart-tags.md)
>* [Smart Content Serviceをトレーニングするためのガイドラインとルール](smart-tags-training-guidelines.md)

