---
title: スマートコンテンツサービスを使用してアセットのタグ付けを設定します。
description: スマートコンテンツサービスを使用して、 [!DNL Adobe Experience Manager] でスマートタグと拡張スマートタグを設定する方法について説明します。
contentOwner: AG
feature: Smart Tags,Tagging
role: Admin
exl-id: 11c5dd92-f824-41d2-9ab2-b32bdeae01b6
source-git-commit: bd65633e85226659df99da1d3834fa18a89de11e
workflow-type: tm+mt
source-wordcount: '1304'
ht-degree: 78%

---

# スマートコンテンツサービスを使用したアセットのタグ付けの設定 {#configure-asset-tagging-using-the-smart-content-service}

統合可能な [!DNL Adobe Experience Manager] を使用してスマートコンテンツサービスを使用する [!DNL Adobe Developer Console]. この設定を使用して、内からスマートコンテンツサービスにアクセスします [!DNL Experience Manager].

>[!NOTE]
>
>* スマートコンテンツサービスは、新しく使用できなくなりました [!DNL Experience Manager Assets] オンプレミス型の顧客。 既にこの機能を有効にしているオンプレミス版のお客様は、引き続きスマートコンテンツサービスを使用できます。
>* スマートコンテンツサービスは既存のユーザーが利用できます [!DNL Experience Manager Assets] Managed Servicesをご利用のお客様（この機能を既に有効にしています）。
>* 新規 [!DNL Experience Manager Assets] Managed Servicesのお客様は、この記事に記載されている手順に従ってスマートコンテンツサービスを設定できます。


この記事では、スマートコンテンツサービスの設定に必要となる以下の主要なタスクについて詳しく説明します。バックエンドでは、 [!DNL Experience Manager] サーバーが、 [!DNL Adobe Developer Console] ゲートウェイを使用して、要求をスマートコンテンツサービスに転送する必要があります。

1. [ でスマートコンテンツサービス設定を作成して、公開鍵を生成します。](#obtain-public-certificate)[!DNL Experience Manager]OAuth 統合用の[公開証明書を取得します](#obtain-public-certificate)。

1. [Adobe 開発者コンソールで統合を作成](#create-adobe-i-o-integration)し、生成した公開鍵をアップロードします。

1. [デプロイメントの設定](#configure-smart-content-service) から API キーやその他の資格情報を使用する [!DNL Adobe Developer Console].

1. [設定をテストします](#validate-the-configuration)。

1. オプションで、[アセットアップロード時の自動タグ付けを有効化します](#enable-smart-tagging-in-the-update-asset-workflow-optional)。

## 前提条件 {#prerequisites}

スマートコンテンツサービスを使用する前に、次の点を確認して、で統合を作成します。 [!DNL Adobe Developer Console]:

* 組織の管理者権限を持つ Adobe ID アカウントがあること。

* お客様の組織でスマートコンテンツサービスが有効になっている。

上記に加えて、拡張スマートタグを有効にするには、最新のもインストールしてください [Experience Managerサービスパック](https://helpx.adobe.com/jp/experience-manager/aem-releases-updates.html).

## スマートコンテンツサービス設定を作成して公開証明書を取得する {#obtain-public-certificate}

公開証明書を使用すると、でプロファイルを認証できます。 [!DNL Adobe Developer Console].

1. [!DNL Experience Manager] ユーザーインターフェイスで、**[!UICONTROL ツール]**／**[!UICONTROL Cloud Services]**／**[!UICONTROL 従来の Cloud Services]** にアクセスします。

1. クラウドサービスページで、「**[!UICONTROL アセットのスマートタグ]**」の「**[!UICONTROL 今すぐ設定]**」をクリックします。

1. **[!UICONTROL 設定を作成]**&#x200B;ダイアログで、スマートタグ設定のタイトルと名前を指定します。「**[!UICONTROL 作成]**」をクリックします。

1. **[!UICONTROL AEM スマートコンテンツサービス]**&#x200B;ダイアログで、以下の値を使用します。

   **[!UICONTROL サービス URL]**: `https://smartcontent.adobe.io/<region where your Experience Manager author instance is hosted>`

   （例：`https://smartcontent.adobe.io/apac`）。次を指定できます。 `na`, `emea`、または `apac` :Experience Managerオーサーインスタンスがホストされる地域。

   >[!NOTE]
   >
   >2022 年 9 月 1 日より前にExperience Manager管理サービスがプロビジョニングされている場合は、次のサービス URL を使用します。
   >`https://mc.adobe.io/marketingcloud/smartcontent`

   **[!UICONTROL 認証サーバー]**: `https://ims-na1.adobelogin.com`

   その他のフィールドは現時点では空白のままにします（後で指定します）。「**[!UICONTROL OK]**」をクリックします。

   ![コンテンツサービスの URL を指定するための Experience Manager スマートコンテンツサービスダイアログ](assets/aem_scs.png)


   *図：コンテンツサービスの URL を指定するためのスマートコンテンツサービスダイアログ*

   >[!NOTE]
   >
   >[!UICONTROL サービス URL] として提供された URL は、ブラウザーからアクセスできず、404 エラーが発生します。設定は、[!UICONTROL サービス URL] パラメーターの同じ値で正常に動作します。サービスの全体的なステータスとメンテナンススケジュールについては、[https://status.adobe.com](https://status.adobe.com) を参照してください。

1. 「**[!UICONTROL OAuth 統合用の公開証明書をダウンロード]**」をクリックし、公開証明書ファイル `AEM-SmartTags.crt` をダウンロードします。

   ![スマートタグ付けサービス用に作成された設定の表現](assets/smart-tags-download-public-cert.png)


   *図：スマートタグサービスの設定*

### 証明書の有効期限が切れた場合の再設定 {#certrenew}

証明書の有効期限が切れると、証明書は信頼されなくなります。期限切れの証明書は更新できません。新しい証明書を追加するには、以下の手順に従います。

1. [!DNL Experience Manager] デプロイメントに管理者としてログインします。**[!UICONTROL ツール]**／**[!UICONTROL セキュリティ]**／**[!UICONTROL ユーザー]**&#x200B;をクリックします。

1. **[!UICONTROL dam-update-service]** ユーザーを見つけてクリックします。「**[!UICONTROL キーストア]**」タブをクリックします。

1. 証明書の有効期限が切れた既存の **[!UICONTROL similaritysearch]** キーストアを削除します。「**[!UICONTROL 保存して閉じる]**」をクリックします。

   ![キーストアの既存の similaritysearch エントリを削除して新しいセキュリティ証明書を追加](assets/smarttags_delete_similaritysearch_keystore.png)

   *図：キーストアの既存の `similaritysearch` エントリを削除して新しいセキュリティ証明書を追加.*

1. **[!UICONTROL ツール]**／**[!UICONTROL クラウドサービス]**／**[!UICONTROL 従来のクラウドサービス]**&#x200B;に移動します。**[!UICONTROL アセットのスマートタグ]**／**[!UICONTROL 設定を表示]**／**[!UICONTROL 利用可能な設定]**&#x200B;をクリックします。必要な設定をクリックします。

1. 公開証明書をダウンロードするには、「**[!UICONTROL OAuth 統合用の公開証明書をダウンロード]**」をクリックします。

1. [https://console.adobe.io](https://console.adobe.io) にアクセスし、**[!UICONTROL 統合]**&#x200B;ページで既存のスマートコンテンツサービスに移動します。新しい証明書をアップロードします。詳しくは、[Adobe 開発者コンソール統合の作成](#create-adobe-i-o-integration)の手順を参照してください。

## Adobe 開発者コンソール統合の作成 {#create-adobe-i-o-integration}

スマートコンテンツサービス API を使用するには、Adobe 開発者コンソールで統合を作成して、[!UICONTROL API キー]（Adobe 開発者コンソール統合の[!UICONTROL クライアント ID] フィールドで生成）、[!UICONTROL テクニカルアカウント ID]、[!UICONTROL 組織 ID]、および[!UICONTROL クライアント秘密鍵]を、[!DNL Experience Manager] のクラウド設定の [!UICONTROL Assets スマートタグサービス設定]用に取得します。

1. ブラウザーで [https://console.adobe.io](https://console.adobe.io/) にアクセスします。適切なアカウントを選択し、関連付けられた組織の役割がシステム管理者であることを確認します。

1. 任意の名前でプロジェクトを作成します。「**[!UICONTROL API を追加]**」をクリックします。

1. **[!UICONTROL API を追加]**&#x200B;ページで、「**[!UICONTROL Experience Cloud]**」、「**[!UICONTROL スマートコンテンツ]**」の順に選択します。「**[!UICONTROL 次へ]**」をクリックします。

1. 「**[!UICONTROL 公開鍵をアップロード]**」を選択します。[!DNL Experience Manager]からダウンロードした証明書ファイルを指定します。[!UICONTROL 公開鍵が正常にアップロード]されたというメッセージが表示されます。「**[!UICONTROL 次へ]**」をクリックします。

   [!UICONTROL 新しいサービスアカウント（JWT）秘密鍵証明書を作成]ページには、設定したサービスアカウントの公開鍵が表示されます。

1. 「**[!UICONTROL 次へ]**」をクリックします。

1. **[!UICONTROL 製品プロファイルを選択]**&#x200B;ページで、「**[!UICONTROL スマートコンテンツサービス]**」を選択します。「**[!UICONTROL 設定済み API を保存]**」をクリックします。

   設定に関する詳細情報がページに表示されます。このページを開いたままにしてこれらの値をコピーし、[!DNL Experience Manager] のクラウド設定の「[!UICONTROL Assets スマートタグサービス設定]」に追加して、スマートタグを設定します。

   ![「概要」タブで、統合について指定した情報を確認できます。](assets/integration_details.png)

   *図：Adobe 開発者コンソールの統合の詳細*

## スマートコンテンツサービスの設定 {#configure-smart-content-service}

統合を設定するには、Adobe 開発者コンソール統合から、[!UICONTROL テクニカルアカウント ID]、[!UICONTROL 組織 ID]、[!UICONTROL クライアント秘密鍵]、および[!UICONTROL クライアント ID] の各フィールドの値を使用します。スマートタグのクラウド設定を作成すると、[!DNL Experience Manager] デプロイメントからの API 要求を認証できるようになります。

1. [!DNL Experience Manager] で、**[!UICONTROL ツール／クラウドサービス／従来のクラウドサービス]**&#x200B;に移動して、[!UICONTROL クラウドサービス]コンソールを開きます。

1. 「**[!UICONTROL アセットのスマートタグ]**」で、上記で作成した設定を開きます。サービスの設定ページで、「**[!UICONTROL 編集]**」をクリックします。

1. **[!UICONTROL AEM スマートコンテンツサービス]**&#x200B;ダイアログで、「**[!UICONTROL サービス URL]**」および「**[!UICONTROL 認証サーバー]**」フィールドに事前入力された値を使用します。

1. [Adobe 開発者コンソールの統合](#create-adobe-i-o-integration)で生成した次の値を使用して、[!UICONTROL API キー]、[!UICONTROL テクニカルアカウント ID]、[!UICONTROL 組織 ID]、および[!UICONTROL クライアント秘密鍵]の各フィールドにコピーします。

   | [!UICONTROL アセットのスマートタグサービス設定] | [!DNL Adobe Developer Console] 統合フィールド |
   |--- |--- |
   | [!UICONTROL API キー] | [!UICONTROL クライアント ID] |
   | [!UICONTROL テクニカルアカウント ID] | [!UICONTROL テクニカルアカウント ID] |
   | [!UICONTROL 組織 ID] | [!UICONTROL 組織 ID] |
   | [!UICONTROL クライアントの秘密鍵] | [!UICONTROL クライアント秘密鍵] |

## 設定の検証 {#validate-the-configuration}

設定が完了したら、JMX MBean を使用して設定を検証します。 検証するには、次の手順に従います。

1. [!DNL Experience Manager] サーバー （`https://[aem_server]:[port]`）にアクセスします。

1. **[!UICONTROL ツール／操作／Web コンソール]**&#x200B;に移動して、OSGi コンソールを開きます。**[!UICONTROL メイン／JMX]** をクリックします。

1. 「**[!UICONTROL com.day.cq.dam.similaritysearch.internal.impl]**」をクリックします。**[!UICONTROL SimilaritySearch Miscellaneous Tasks]** が開きます。

1. 「**[!UICONTROL validateConfigs()]**」をクリックします。**[!UICONTROL 設定を検証]**&#x200B;ダイアログで、「**[!UICONTROL 起動]**」をクリックします。

   同じダイアログに検証結果が表示されます。

## DAM アセットの更新ワークフローでのスマートタグの有効化（オプション） {#enable-smart-tagging-in-the-update-asset-workflow-optional}

1. [!DNL Experience Manager] で、**[!UICONTROL ツール]**／**[!UICONTROL ワークフロー]**／**[!UICONTROL モデル]**&#x200B;に移動します。

1. **[!UICONTROL ワークフローモデル]**&#x200B;ページで、「**[!UICONTROL DAM アセットの更新]**」ワークフローモデルを選択します。

1. ツールバーの「**[!UICONTROL 編集]**」をクリックします。

1. サイドパネルを展開して、ステップを表示します。「DAM ワークフロー」セクションの「**[!UICONTROL スマートタグアセット]**」ステップをドラッグして、「**[!UICONTROL サムネールを処理]**」ステップの後に配置します。

   ![「DAM アセットの更新」ワークフローで「サムネールを処理」ステップの後に「スマートタグアセット」ステップを追加](assets/smart-tag-in-dam-update-asset-workflow.png)

   *図：「[!UICONTROL DAM アセットの更新]」ワークフローで「サムネールを処理」ステップの後に「スマートタグアセット」ステップを追加。*

1. そのステップを編集モードで開きます。「**[!UICONTROL 詳細設定]**」で、「**[!UICONTROL ハンドラー処理の設定]**」オプションが選択されていることを確認します。

   ![DAM アセットの更新ワークフローを設定して、スマートタグステップを追加する](assets/smart-tag-step-properties-workflow1.png)


   *図：DAM アセットの更新ワークフローを設定して、スマートタグステップを追加する*

1. 自動タグ付けのステップに失敗してもワークフローを完了させたい場合は、「**[!UICONTROL 引数]**」タブで「**[!UICONTROL エラーを無視]**」を選択します。

   ![DAM アセットの更新ワークフローを設定してスマートタグステップを追加し、ハンドラー処理の設定を選択する](assets/smart-tag-step-properties-workflow2.png)


   *図：DAM アセットの更新ワークフローを設定してスマートタグステップを追加し、ハンドラー処理の設定を選択する*

   フォルダーでスマートタグが有効になっているかに関わらずアップロード時にアセットをタグ付けするには、「**[!UICONTROL スマートタグフラグを無視]**」を選択します。

   ![DAM アセットの更新ワークフローを設定してスマートタグステップを追加し、「スマートタグフラグを無視」を選択する](assets/smart-tag-step-properties-workflow3.png)


   *図：スマートタグステップを追加するための DAM アセットの更新ワークフローを設定し、「スマートタグフラグを無視」を選択します。*

1. 「**[!UICONTROL OK]**」をクリックして、プロセスステップを閉じ、ワークフローを保存します。

>[!MORELIKETHIS]
>
>* [スマートタグの管理](managing-smart-tags.md)
>* [スマートタグの概要とスマートタグのトレーニング方法](enhanced-smart-tags.md)
>* [スマートコンテンツサービスのトレーニングに関するガイドラインとルール](smart-tags-training-guidelines.md)

