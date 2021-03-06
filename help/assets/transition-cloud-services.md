---
title: フォルダーへの翻訳クラウドサービスの適用
description: フォルダーへの翻訳クラウドサービスの適用
contentOwner: AG
feature: Translation
role: Admin
exl-id: 87883a3f-db95-41f4-b0aa-cdaeb7e6f555
source-git-commit: 1e3cd6ce3138113721183439f7cfb9daed6e0e58
workflow-type: tm+mt
source-wordcount: '395'
ht-degree: 97%

---

# フォルダーへの翻訳クラウドサービスの適用 {#applying-translation-cloud-services-to-folders}

Adobe Experience Manager では、選択した翻訳プロバイダーのクラウドベースの翻訳サービスを利用して、要件に基づいてアセットを確実に翻訳できます。

翻訳クラウドサービスをアセットフォルダーに直接適用できるので、翻訳ワークフローの間もずっとアセットを利用できます。

## 翻訳サービスの適用 {#applying-the-translation-services}

翻訳クラウドサービスをアセットフォルダーに直接適用すると、翻訳ワークフローの作成または変更時に翻訳サービスを設定する必要がなくなります。

1. Assets UI から翻訳サービスを適用するフォルダーを選択します。
1. ツールバーの「**[!UICONTROL プロパティ]**」アイコンをクリックまたはタップして、**[!UICONTROL フォルダーのプロパティ]**&#x200B;ページを表示します。

   ![chlimage_1-215](assets/chlimage_1-215.png)

1. 「**[!UICONTROL クラウドサービス]**」タブに移動します。
1. 「クラウドサービスの設定」リストから目的の翻訳プロバイダーを選択します。例えば、Microsoft の翻訳サービスを利用する場合は、「**[!UICONTROL Microsoft Translator]**」を選択します。

   ![chlimage_1-216](assets/chlimage_1-216.png)

1. 翻訳プロバイダーのコネクタを選択します。

   ![chlimage_1-217](assets/chlimage_1-217.png)

1. ツールバーの「**[!UICONTROL 保存]**」をクリックまたはタップし、「**[!UICONTROL OK]**」をクリックしてダイアログを閉じます。翻訳サービスがフォルダーに適用されます。

## カスタム翻訳コネクタの適用  {#applying-custom-translation-connector}

翻訳ワークフローで使用する翻訳サービスにカスタムコネクタを適用する場合、カスタムコネクタを適用するには、まずパッケージマネージャーからコネクタをインストールします。次に、クラウドサービスコンソールからコネクタを設定します。コネクタを設定すると、[翻訳サービスの適用](transition-cloud-services.md#applying-the-translation-services)で説明されている「クラウドサービス」タブのコネクタのリストに表示されるようになります。カスタムコネクタを適用し、翻訳ワークフローを実行すると、翻訳プロジェクトの「**[!UICONTROL 翻訳の概要]**」タイルの「**[!UICONTROL プロバイダー]**」と「**[!UICONTROL メソッド]**」という見出しの下にコネクタの詳細が表示されます。

1. パッケージマネージャーからコネクタをインストールします。
1. 次をクリックまたはタップします。 [!DNL Experience Manager] ロゴをクリックし、に移動します。 **[!UICONTROL ツール/導入/Cloud Services]**.
1. インストールしたコネクタを&#x200B;**[!UICONTROL クラウドサービス]**&#x200B;ページの「**[!UICONTROL サードパーティのサービス]**」の下で探します。

   ![chlimage_1-218](assets/chlimage_1-218.png)

1. 「**[!UICONTROL 今すぐ設定]**」リンクをクリックまたはタップして、**[!UICONTROL 設定を作成]**&#x200B;ダイアログを開きます。

   ![chlimage_1-219](assets/chlimage_1-219.png)

1. コネクタのタイトルと名前を指定して、「**[!UICONTROL 作成]**」をクリックまたはタップします。[翻訳サービスの適用](#applying-the-translation-services)のステップ 5 で説明されている「**[!UICONTROL クラウドサービス]**」タブのコネクタリストにカスタムコネクタが表示されます。
1. カスタムコネクタを適用したら、[翻訳プロジェクトの作成](translation-projects.md)で説明されている翻訳ワークフローを実行します。**[!UICONTROL プロジェクト]**&#x200B;コンソールで、翻訳プロジェクトの「**[!UICONTROL 翻訳の概要]**」タイルに表示されているコネクタの詳細を確認します。

   ![chlimage_1-220](assets/chlimage_1-220.png)
