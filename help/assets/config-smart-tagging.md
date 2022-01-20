---
title: スマートコンテンツサービスを使用してアセットのタグ付けを設定します。
description: でスマートタグと拡張スマートタグを設定する方法について説明します。 [!DNL Adobe Experience Manager]スマートコンテンツサービスを使用して作成されます。
contentOwner: AG
feature: Smart Tags,Tagging
role: Admin
exl-id: 11c5dd92-f824-41d2-9ab2-b32bdeae01b6
source-git-commit: 5d96c09ef764b02e08dcdf480da1ee18f4d9a30c
workflow-type: tm+mt
source-wordcount: '1212'
ht-degree: 48%

---

# スマートコンテンツサービスを使用したアセットのタグ付けの設定 {#configure-asset-tagging-using-the-smart-content-service}

統合可能な [!DNL Adobe Experience Manager] を使用してスマートコンテンツサービスを使用する [!DNL Adobe Developer Console]. この設定を使用して、内からスマートコンテンツサービスにアクセスします [!DNL Experience Manager].

この記事では、スマートコンテンツサービスの設定に必要となる以下の主要なタスクについて詳しく説明します。バックエンドでは、 [!DNL Experience Manager] サーバーが、 [!DNL Adobe Developer Console] ゲートウェイを使用して、要求をスマートコンテンツサービスに転送する必要があります。

1. [ でスマートコンテンツサービス設定を作成して、公開鍵を生成します。](#obtain-public-certificate)[!DNL Experience Manager]OAuth 統合用の[公開証明書を取得します](#obtain-public-certificate)。

1. [Adobe 開発者コンソールで統合を作成](#create-adobe-i-o-integration)し、生成した公開鍵をアップロードします。

1. [デプロイメントの設定](#configure-smart-content-service) から API キーやその他の資格情報を使用する [!DNL Adobe Developer Console].

1. [設定をテストします](#validate-the-configuration)。

1. オプションで、 [アセットのアップロード時に自動タグ付けを有効にする](#enable-smart-tagging-in-the-update-asset-workflow-optional).

## 前提条件 {#prerequisites}

スマートコンテンツサービスを使用する前に、次の点を確認して、で統合を作成します。 [!DNL Adobe Developer Console]:

* 組織の管理者権限を持つ Adobe ID アカウントがあること。

* お客様の組織でスマートコンテンツサービスが有効になっている。

上記に加えて、拡張スマートタグを有効にするには、最新のもインストールしてください [Experience Managerサービスパック](https://helpx.adobe.com/jp/experience-manager/aem-releases-updates.html).

## スマートコンテンツサービス設定を作成して公開証明書を取得する {#obtain-public-certificate}

公開証明書を使用すると、でプロファイルを認証できます。 [!DNL Adobe Developer Console].

1. 内 [!DNL Experience Manager] ユーザーインターフェイス、アクセス **[!UICONTROL ツール]** > **[!UICONTROL Cloud Services]** > **[!UICONTROL 従来のCloud Services]**.

1. Cloud Servicesページで、 **[!UICONTROL 今すぐ設定]** under **[!UICONTROL アセットのスマートタグ]**.

1. **[!UICONTROL 設定を作成]**&#x200B;ダイアログで、スマートタグ設定のタイトルと名前を指定します。「**[!UICONTROL 作成]**」をクリックします。

1. **[!UICONTROL AEM スマートコンテンツサービス]**&#x200B;ダイアログで、以下の値を使用します。

   **[!UICONTROL サービス URL]**: `https://mc.adobe.io/marketingcloud/smartcontent`

   **[!UICONTROL 認証サーバー]**: `https://ims-na1.adobelogin.com`

   その他のフィールドは現時点では空白のままにします（後で指定します）。「**[!UICONTROL OK]**」をクリックします。

   ![コンテンツサービス URL を提供するExperience Managerスマートコンテンツサービスダイアログ](assets/aem_scs.png)


   *図：コンテンツサービス URL を提供するスマートコンテンツサービスダイアログ*

   >[!NOTE]
   >
   >指定された URL [!UICONTROL サービス URL] はブラウザーからアクセスできず、404 エラーが生成されます。 この設定は、 [!UICONTROL サービス URL] パラメーター。 サービスの全体的なステータスとメンテナンススケジュールについては、 [https://status.adobe.com](https://status.adobe.com).

1. クリック **[!UICONTROL OAuth 統合用の公開証明書をダウンロード]**、および公開証明書ファイルをダウンロードします。 `AEM-SmartTags.crt`.

   ![スマートタグ付けサービス用に作成された設定の表現](assets/smart-tags-download-public-cert.png)


   *図：スマートタグサービスの設定*

### 証明書の有効期限が切れた場合の再設定 {#certrenew}

証明書の有効期限が切れると、証明書は信頼されなくなります。 期限切れの証明書は更新できません。新しい証明書を追加するには、以下の手順に従います。

1. [!DNL Experience Manager] デプロイメントに管理者としてログインします。**[!UICONTROL ツール]**／**[!UICONTROL セキュリティ]**／**[!UICONTROL ユーザー]**&#x200B;をクリックします。

1. **[!UICONTROL dam-update-service]** ユーザーを見つけてクリックします。「**[!UICONTROL キーストア]**」タブをクリックします。

1. 証明書の有効期限が切れた既存の **[!UICONTROL similaritysearch]** キーストアを削除します。「**[!UICONTROL 保存して閉じる]**」をクリックします。

   ![キーストアの既存の similaritysearch エントリを削除して新しいセキュリティ証明書を追加](assets/smarttags_delete_similaritysearch_keystore.png)

   *図：キーストアの既存の `similaritysearch` エントリを削除して新しいセキュリティ証明書を追加.*

1. **[!UICONTROL ツール]**／**[!UICONTROL クラウドサービス]**／**[!UICONTROL 従来のクラウドサービス]**&#x200B;に移動します。**[!UICONTROL アセットのスマートタグ]**／**[!UICONTROL 設定を表示]**／**[!UICONTROL 利用可能な設定]**&#x200B;をクリックします。必要な設定をクリックします。

1. 公開証明書をダウンロードするには、「**[!UICONTROL OAuth 統合用の公開証明書をダウンロード]**」をクリックします。

1. [https://console.adobe.io](https://console.adobe.io) にアクセスし、**[!UICONTROL 統合]**&#x200B;ページで既存のスマートコンテンツサービスに移動します。新しい証明書をアップロードします。詳しくは、 [Adobe開発者コンソール統合の作成](#create-adobe-i-o-integration).

## Adobe開発者コンソール統合の作成 {#create-adobe-i-o-integration}

スマートコンテンツサービス API を使用するには、統合開発者コンソールでAdobeを作成して、 [!UICONTROL API キー] ( で生成 [!UICONTROL クライアント ID] Adobe開発者コンソール統合のフィールド )、 [!UICONTROL テクニカルアカウント ID], [!UICONTROL 組織 ID]、および [!UICONTROL クライアント秘密鍵] 対象 [!UICONTROL アセットのスマートタグサービス設定] クラウド設定の [!DNL Experience Manager].

1. ブラウザーで [https://console.adobe.io](https://console.adobe.io/) にアクセスします。適切なアカウントを選択し、関連付けられた組織の役割がシステム管理者であることを確認します。

1. 任意の名前でプロジェクトを作成します。「**[!UICONTROL API を追加]**」をクリックします。

1. **[!UICONTROL API を追加]**&#x200B;ページで、「**[!UICONTROL Experience Cloud]**」、「**[!UICONTROL スマートコンテンツ]**」の順に選択します。「**[!UICONTROL 次へ]**」をクリックします。

1. 「**[!UICONTROL 公開鍵をアップロード]**」を選択します。[!DNL Experience Manager]からダウンロードした証明書ファイルを指定します。[!UICONTROL 公開鍵が正常にアップロード]されたというメッセージが表示されます。「**[!UICONTROL 次へ]**」をクリックします。

   [!UICONTROL 新しいサービスアカウント（JWT）秘密鍵証明書を作成]ページには、設定したサービスアカウントの公開鍵が表示されます。

1. 「**[!UICONTROL 次へ]**」をクリックします。

1. **[!UICONTROL 製品プロファイルを選択]**&#x200B;ページで、「**[!UICONTROL スマートコンテンツサービス]**」を選択します。「**[!UICONTROL 設定済み API を保存]**」をクリックします。

   設定に関する詳細情報がページに表示されます。このページを開いたままにして、これらの値をコピーし、 [!UICONTROL アセットのスマートタグサービス設定] クラウド設定の [!DNL Experience Manager] スマートタグを設定するには：

   ![「概要」タブで、統合について指定した情報を確認できます。](assets/integration_details.png)

   *図：統合の詳細 (Adobe開発者コンソール )*

## スマートコンテンツサービスの設定 {#configure-smart-content-service}

統合を設定するには、 [!UICONTROL テクニカルアカウント ID], [!UICONTROL 組織 ID], [!UICONTROL クライアント秘密鍵]、および [!UICONTROL クライアント ID] 開発者コンソール統合Adobeのフィールド。 スマートタグクラウド設定を作成すると、 [!DNL Experience Manager] デプロイメント。

1. In [!DNL Experience Manager]に移動します。 **[!UICONTROL ツール/Cloud Service/従来のCloud Services]** 開く [!UICONTROL Cloud Services] コンソール。

1. 「**[!UICONTROL アセットのスマートタグ]**」で、上記で作成した設定を開きます。サービスの設定ページで、「**[!UICONTROL 編集]**」をクリックします。

1. **[!UICONTROL AEM スマートコンテンツサービス]**&#x200B;ダイアログで、「**[!UICONTROL サービス URL]**」および「**[!UICONTROL 認証サーバー]**」フィールドに事前入力された値を使用します。

1. フィールド [!UICONTROL API キー], [!UICONTROL テクニカルアカウント ID], [!UICONTROL 組織 ID]、および [!UICONTROL クライアント秘密鍵]をコピーして、 [Adobe開発者コンソールの統合](#create-adobe-i-o-integration).

   | [!UICONTROL アセットのスマートタグサービス設定] | [!DNL Adobe Developer Console] 統合フィールド |
   |--- |--- |
   | [!UICONTROL API キー] | [!UICONTROL クライアント ID] |
   | [!UICONTROL テクニカルアカウント ID] | [!UICONTROL テクニカルアカウント ID] |
   | [!UICONTROL 組織 ID] | [!UICONTROL 組織 ID] |
   | [!UICONTROL クライアントの秘密鍵] | [!UICONTROL クライアント秘密鍵] |

## 設定の検証 {#validate-the-configuration}

設定が完了したら、JMX MBean を使用して設定を検証します。 検証するには、次の手順に従います。

1. 次にアクセス： [!DNL Experience Manager] サーバー： `https://[aem_server]:[port]`.

1. **[!UICONTROL ツール／操作／Web コンソール]**&#x200B;に移動して、OSGi コンソールを開きます。**[!UICONTROL メイン／JMX]** を選択します。

1. 「**[!UICONTROL com.day.cq.dam.similaritysearch.internal.impl]**」をクリックします。開く **[!UICONTROL 類似性検索のその他のタスク]**.

1. 「**[!UICONTROL validateConfigs()]**」をクリックします。内 **[!UICONTROL 設定を検証]** ダイアログ、クリック **[!UICONTROL 呼び出し]**.

   検証結果は、同じダイアログに表示されます。

## DAM アセットの更新ワークフローでのスマートタグの有効化（オプション） {#enable-smart-tagging-in-the-update-asset-workflow-optional}

1. In [!DNL Experience Manager]に移動します。 **[!UICONTROL ツール]** > **[!UICONTROL ワークフロー]** > **[!UICONTROL モデル]**.

1. **[!UICONTROL ワークフローモデル]**&#x200B;ページで、「**[!UICONTROL DAM アセットの更新]**」ワークフローモデルを選択します。

1. ツールバーの「**[!UICONTROL 編集]**」をクリックします。

1. サイドパネルを展開して、ステップを表示します。「DAM ワークフロー」セクションの「**[!UICONTROL スマートタグアセット]**」ステップをドラッグして、「**[!UICONTROL サムネールを処理]**」ステップの後に配置します。

   ![「DAM アセットの更新」ワークフローで「サムネールを処理」ステップの後に「スマートタグアセット」ステップを追加](assets/smart-tag-in-dam-update-asset-workflow.png)

   *図：「DAM アセットの更新」ワークフローで「サムネールを処理」ステップの後に「スマートタグアセット」ステップを追加。*

1. そのステップを編集モードで開きます。「**[!UICONTROL 詳細設定]**」で、「**[!UICONTROL ハンドラー処理の設定]**」オプションが選択されていることを確認します。

   ![「DAM アセットの更新」ワークフローを設定し、スマートタグステップを追加する](assets/smart-tag-step-properties-workflow1.png)


   *図：「DAM アセットの更新」ワークフローを設定し、スマートタグステップを追加する*

1. 自動タグ付けのステップに失敗してもワークフローを完了させたい場合は、「**[!UICONTROL 引数]**」タブで「**[!UICONTROL エラーを無視]**」を選択します。

   ![スマートタグステップを追加し、ハンドラー処理の設定を選択するための DAM アセットの更新ワークフローを設定](assets/smart-tag-step-properties-workflow2.png)


   *図：スマートタグステップを追加し、ハンドラー処理の設定を選択するための DAM アセットの更新ワークフローを設定*

   フォルダーでスマートタグが有効になっているかに関わらずアップロード時にアセットをタグ付けするには、「**[!UICONTROL スマートタグフラグを無視]**」を選択します。

   ![スマートタグステップを追加するための DAM アセットの更新ワークフローを設定し、「スマートタグフラグを無視」を選択します。](assets/smart-tag-step-properties-workflow3.png)


   *図：スマートタグステップを追加するための DAM アセットの更新ワークフローを設定し、「スマートタグフラグを無視」を選択します。*

1. 「**[!UICONTROL OK]**」をクリックして、プロセスステップを閉じ、ワークフローを保存します。

>[!MORELIKETHIS]
>
>* [スマートタグの管理](managing-smart-tags.md)
>* [スマートタグの概要とスマートタグのトレーニング方法](enhanced-smart-tags.md)
>* [スマートコンテンツサービスのトレーニングに関するガイドラインとルール](smart-tags-training-guidelines.md)

