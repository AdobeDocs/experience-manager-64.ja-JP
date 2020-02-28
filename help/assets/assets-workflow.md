---
title: デジタルアセットの処理にワークフローを適用
description: AEM Assetsのアセット、フォルダー、コレクションにワークフローを適用してデジタルアセットを処理する方法について説明します。
contentOwner: AG
translation-type: tm+mt
source-git-commit: 0d70a672a2944e2c03b54beb3b5f734136792ab1

---


# アセットへのワークフローの適用 {#applying-workflows-to-assets}

ワークフローをデジタルアセットに適用する方法は、Web サイトページに適用する場合と同様です。AEM におけるワークフローの作成と使用について詳しくは、[ワークフローの開始](../sites-authoring/workflows-participating.md)を参照してください。

デジタルアセットでワークフローを使用して、アセットのアクティベートや透かしの作成などをおこないます。アセットのワークフローの多くは自動的にオンになります。例えば、画像の編集後にレンディションを自動的に作成するワークフローは、自動的にオンになります。

アクティベーションのリクエストやアクティベーション解除のリクエストなど、クラシック UI で使用可能なワークフローがタッチ操作対応 UI で使用できない場合は、[ワークフローモデルをタッチ UI で使用可能にする](../sites-developing/workflows-models.md#make-workflow-models-available-in-touchui)を参照してください。

## AEM アセットへのワークフローの適用 {#applying-a-workflow-to-an-aem-asset}

AEM アセットへのワークフローの適用について詳しくは、[アセットでのワークフローの開始](managing-assets-touch-ui.md#starting-a-workflow-on-an-asset)を参照してください。

## 複数のアセットへのワークフローの適用 {#applying-a-workflow-to-multiple-assets}

1. Assets コンソールから、ワークフローを開始するアセットの場所へ移動して、アセットを選択します。
1. Click the GlobalNav icon, and the choose **[!UICONTROL Timeline]** from the menu to display the timeline.

   ![chlimage_1-136](assets/chlimage_1-136.png)

1. Click the **[!UICONTROL Actions]** (arrow) icon at the bottom.

   ![chlimage_1-137](assets/chlimage_1-137.png)

1. 「**[!UICONTROL ワークフローを開始]**」をクリックします。
1. **[!UICONTROL ワークフローを開始]**&#x200B;ダイアログで、リストからワークフローモデルを選択します。

   ![chlimage_1-138](assets/chlimage_1-138.png)

1. （オプション）ワークフローインスタンスを参照するために使用するワークフローのタイトルを指定します。
1. ダイアログで「**[!UICONTROL 開始]**」をクリックし、次に「**[!UICONTROL 確認]**」をクリックします。選択したすべてのアセットでワークフローが実行されます。

## 複数のフォルダーへのワークフローの適用 {#applying-a-workflow-to-multiple-folders}

ワークフローを複数のフォルダーに適用する手順は、複数のアセットに適用する手順と似ています。Assets コンソールでフォルダーを選択し、[複数のアセットへのワークフローの適用](assets-workflow.md#applying-a-workflow-to-multiple-assets)の手順 2 から 7 までを実行します。

## コレクションへのワークフローの適用 {#applying-a-workflow-to-a-collection}

For details of applying a workflow to a collection, see [Running a workflow on a collection](managing-collections-touch-ui.md#running-a-workflow-on-a-collection).
