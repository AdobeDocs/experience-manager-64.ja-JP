---
title: コンテンツフラグメントモデル
seo-title: Content Fragment Models
description: コンテンツフラグメントモデルは、構造化コンテンツを含むコンテンツフラグメントの作成に使用されます。
seo-description: Content Fragment Models are used to create content fragments with structured content.
uuid: 59176a32-1255-4a46-ad00-344bde843ea6
content-type: reference
topic-tags: content-fragments
products: SG_EXPERIENCEMANAGER/6.4/ASSETS
discoiquuid: 45e67357-4524-4d25-b5f1-21182b8e803c
exl-id: 39ed07ec-54a6-4387-8435-e891726c411c
feature: Content Fragments
role: User
source-git-commit: c5b816d74c6f02f85476d16868844f39b4c47996
workflow-type: tm+mt
source-wordcount: '725'
ht-degree: 63%

---

# コンテンツフラグメントモデル {#content-fragment-models}

>[!CAUTION]
>
>AEM 6.4 の拡張サポートは終了し、このドキュメントは更新されなくなりました。 詳細は、 [技術サポート期間](https://helpx.adobe.com/jp/support/programs/eol-matrix.html). サポートされているバージョンを見つける [ここ](https://experienceleague.adobe.com/docs/?lang=ja).

>[!CAUTION]
>
>一部のコンテンツフラグメント機能には、 [AEM 6.4 Service Pack 2(6.4.2.0) 以降](../release-notes/sp-release-notes.md).

コンテンツフラグメントモデルは、[コンテンツフラグメント](content-fragments.md)のコンテンツの構造を定義します。

## コンテンツフラグメントモデルの有効化 {#enable-content-fragment-models}

>[!CAUTION]
>
>を有効にしない場合、 **[!UICONTROL コンテンツフラグメントモデル]**、 **[!UICONTROL 作成]** 新しいモデルを作成する際に、オプションは使用できません。

コンテンツフラグメントモデルを有効にするには、次の操作が必要です。

* 設定マネージャーでのコンテンツフラグメントモデルの使用の有効化
* アセットフォルダーへの設定の適用

### Configuration Manager でコンテンツフラグメントモデルを有効にする {#enable-content-fragment-models-in-configuration-manager}

[新しいコンテンツフラグメントモデルを作成する](#creating-a-content-fragment-model)には、最初に設定マネージャーを使用してコンテンツフラグメントモデルを有効にする&#x200B;**必要があります**。

1. **[!UICONTROL ツール]**／**[!UICONTROL 一般]**&#x200B;に移動し、**[!UICONTROL 設定ブラウザー]**&#x200B;を開きます。
   * 詳しくは、[設定ブラウザーのドキュメント](/help/sites-administering/configurations.md)を参照してください。
1. Web サイトに適した場所を選択します。
1. 「**[!UICONTROL 作成]**」を使用してダイアログを開き、次の操作をおこないます。

   1. 「**[!UICONTROL タイトル]**」を指定します。
   1. 「**[!UICONTROL コンテンツフラグメントモデル]**」を選択して、そのモデルを使用できるようにします。

   ![cfm-6420-09](assets/cfm-6420-09.png)

1. 「**[!UICONTROL 作成]**」を選択して、定義を保存します。

### アセットフォルダーへの設定の適用 {#apply-the-configuration-to-your-assets-folder}

**[!UICONTROL グローバル]**&#x200B;設定をコンテンツフラグメントモデルに対して有効にした場合、ユーザーが作成したあらゆるモデルを任意のアセットフォルダーで使用できます。

他の設定（グローバル以外）を同等のアセットフォルダーで使用するには、接続を定義する必要があります。そのためには、適切なフォルダーの「**[!UICONTROL フォルダーのプロパティ]**」の「**[!UICONTROL クラウドサービス]**」タブで「**[!UICONTROL 設定]**」を使用します。

## コンテンツフラグメントモデルの作成 {#creating-a-content-fragment-model}

1. **[!UICONTROL ツール]**／**[!UICONTROL アセット]**&#x200B;に移動し、**[!UICONTROL コンテンツフラグメントモデル]**&#x200B;を開きます。
1. 次に該当するフォルダーに移動します。 [設定](#enable-content-fragment-models).
1. 用途 **[!UICONTROL 作成]** をクリックしてウィザードを開きます。

   >[!CAUTION]
   >
   >[コンテンツフラグメントモデルの使用が有効になっていない](#enable-content-fragment-models)場合、「**作成**」オプションは使用できません。

1. 「**[!UICONTROL モデルタイトル]**」を指定します。必要に応じて、「**[!UICONTROL 説明]**」を追加することもできます。

   ![cfm-6420-10](assets/cfm-6420-10.png)

1. 用途 **[!UICONTROL 作成]** 空のモデルを保存します。 アクションの成功を示すメッセージが表示されます。このメッセージで、 **[!UICONTROL 開く]** をクリックして、モデルを直ちに編集するか、 **[!UICONTROL 完了]** コンソールに戻ります。

## コンテンツフラグメントモデルの定義 {#defining-your-content-fragment-model}

コンテンツフラグメントモデルは、生成されるコンテンツフラグメントの構造を効果的に定義します。 モデルエディターを使用して、次の必須フィールドを追加し、設定できます。

>[!CAUTION]
>
>既存のコンテンツフラグメントモデルを編集すると、依存するフラグメントが影響を受ける可能性があります。

1. **[!UICONTROL ツール]**／**[!UICONTROL アセット]**&#x200B;に移動し、**[!UICONTROL コンテンツフラグメントモデル]**&#x200B;を開きます。

1. コンテンツフラグメントモデルが含まれているフォルダーに移動します。
1. 必要なモデルを **[!UICONTROL 編集]** 用に開きます。クイック操作を使用するか、モデルを選択してツールバーから操作を選択します。

   モデルエディターを開くと、次の内容が表示されます。

   * 左：フィールドが既に定義されています
   * 右：フィールドの作成に使用できる&#x200B;**[!UICONTROL データタイプ]**（およびフィールドの作成後に使用する&#x200B;**[!UICONTROL プロパティ]**）

   >[!NOTE]
   >
   >フィールドが **必須**、 **ラベル** 左側のウィンドウに示された部分にアスタリスク (**&amp;ast;**) をクリックします。

   ![cfm-6420-12](assets/cfm-6420-12.png)

1. **フィールドを追加するには**

   * 必要なデータタイプをフィールドの必要な場所にドラッグします。

   ![cfm-6420-11](assets/cfm-6420-11.png)

   * フィールドがモデルに追加されると、その特定のデータタイプに対して定義できる&#x200B;**プロパティ**&#x200B;が右側のパネルに表示されます。ここで、そのフィールドに必要な項目を定義することができます。次に例を示します。

   ![cfm-6420-13](assets/cfm-6420-13.png)

1. **フィールドを削除するには**

   必須フィールドを選択し、ごみ箱アイコンをクリックまたはタップします。 この操作の確認が求められます。

   ![cf-32](assets/cf-32.png)

1. 必要なフィールドをすべて追加してプロパティを定義したら、「**[!UICONTROL 保存]**」を使用して定義を保存します。次に例を示します。

   ![cfm-6420-14](assets/cfm-6420-14.png)

## コンテンツフラグメントモデルの削除 {#deleting-a-content-fragment-model}

>[!CAUTION]
>
>コンテンツフラグメントモデルを削除すると、依存するフラグメントに影響を与える場合があります。

コンテンツフラグメントモデルを削除するには：

1. **[!UICONTROL ツール]**／**[!UICONTROL アセット]**&#x200B;に移動し、**[!UICONTROL コンテンツフラグメントモデル]**&#x200B;を開きます。

1. コンテンツフラグメントモデルが含まれているフォルダーに移動します。
1. モデルを選択し、その後に **[!UICONTROL 削除]** をクリックします。

   >[!NOTE]
   >
   >モデルが参照されている場合は、警告が表示されます。 適切な行動を取る。

## コンテンツフラグメントモデルの公開 {#publishing-a-content-fragment-model}

コンテンツフラグメントモデルは、そのモデルに依存するコンテンツフラグメントの公開時または公開前に公開する必要があります。

コンテンツフラグメントモデルを公開するには：

1. **[!UICONTROL ツール]**／**[!UICONTROL アセット]**&#x200B;に移動し、**[!UICONTROL コンテンツフラグメントモデル]**&#x200B;を開きます。

1. コンテンツフラグメントモデルが含まれているフォルダーに移動します。
1. モデルを選択し、次にツールバーの「**[!UICONTROL 公開]**」を選択します。

   >[!NOTE]
   >
   >まだ公開されていないモデルのコンテンツフラグメントを公開すると、選択リストにそのことが示され、モデルがフラグメントと共に公開されます。
