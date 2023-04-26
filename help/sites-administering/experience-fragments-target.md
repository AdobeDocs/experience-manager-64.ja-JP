---
title: エクスペリエンスフラグメントとの Target 統合
seo-title: Target Integration with Experience Fragments
description: エクスペリエンスフラグメントとの Target 統合
seo-description: Target Integration with Experience Fragments
uuid: 621f57d4-3b8d-49ea-b193-8530c8fbd74e
contentOwner: carlino
products: SG_EXPERIENCEMANAGER/6.4/SITES
topic-tags: integration
content-type: reference
discoiquuid: 6911c8e3-b12c-466e-8255-5dcd09557d35
exl-id: dbde3cb6-4132-4462-bd4c-0e4439110e2e
source-git-commit: bd94d3949f0117aa3e1c9f0e84f7293a5d6b03b4
workflow-type: tm+mt
source-wordcount: '647'
ht-degree: 39%

---

# エクスペリエンスフラグメントとの Target 統合{#target-integration-with-experience-fragments}

>[!NOTE]
>
>この機能を使用するには、 [AEM 6.4 Service Pack 2(6.4.2.0)](/help/release-notes/sp-release-notes.md) または後で。

書き出し可能 [エクスペリエンスフラグメント](/help/sites-authoring/experience-fragments.md)(Adobe Experience Manager(AEM) で作成 ) からAdobe Targetへ 書き出したエクスペリエンスフラグメントは、Target アクティビティのオファーとして使用し、幅広くエクスペリエンスをテストおよびパーソナライズできます。これにより、AEMの使いやすさと機能を、Target の強力な自動インテリジェンス (AI) 機能と機械学習 (ML) 機能と組み合わせることができます。

## 前提条件 {#prerequisites}

様々なアクションが必要です。

1. AEM と Target を統合する必要があります。詳しくは、 [Adobe Targetとの統合](/help/sites-administering/target.md) を参照してください。
1. エクスペリエンスフラグメントはオーサーインスタンスから書き出されるので、次の操作を行う必要があります。 [Link Externalizer の設定](/help/sites-developing/externalizer.md) オーサーインスタンス上でリンクが外部化されていることを確認します。

## クラウド設定の追加 {#add-the-cloud-configuration}

フラグメントを書き出す前に、 **クラウド設定** 対象 **Adobe Target** をフラグメントまたはフォルダーに追加します。

1. **エクスペリエンスフラグメント**&#x200B;コンソールに移動します。
1. 適切なフォルダーまたはフラグメントの&#x200B;**ページのプロパティ**&#x200B;を開きます。

   >[!NOTE]
   >
   >クラウド設定をエクスペリエンスフラグメントの親フォルダーに追加した場合、設定はすべての子に継承されます。
   >
   >クラウド設定をエクスペリエンスフラグメント自体に追加した場合、設定はすべてのバリエーションに継承されます。

1. 「**クラウドサービス**」タブを選択します。

1. の下 **Cloud Service設定**&#x200B;を選択します。 **Adobe Target** 」をドロップダウンリストから選択します。
1. の下 **Adobe Target**、適切な設定を選択します。

1. **保存して閉じる**。

##  Target へのエクスペリエンスフラグメントの書き出し {#exporting-an-experience-fragment-to-target}

>[!NOTE]
>
>画像などのメディアアセットの場合、参照のみが Target に書き出されます。 アセット自体はAEM Assetsに保存されたままで、AEMパブリッシュインスタンスから配信されます。
>
>このため、Target に書き出す前に、エクスペリエンスフラグメントと関連するすべてのアセットを公開する必要があります。

（クラウド設定を指定した後に）エクスペリエンスフラグメントをAEMから Target に書き出すには、次の手順を実行します。

1. エクスペリエンスフラグメントコンソールに移動します。
1. ターゲットに書き出すエクスペリエンスフラグメントを選択します。

   >[!NOTE]
   >
   >エクスペリエンスフラグメント Web バリエーションにする必要があります。

1. タップまたはクリック **Adobe Targetに書き出し**.

   >[!NOTE]
   >
   >エクスペリエンスフラグメントが既に書き出されている場合は、**Adobe Target でアップデート** を選択します。

1. タップまたはクリック **公開せずに書き出し** または **公開** 必要に応じて。

   >[!NOTE]
   >
   >「**公開**」を選択すると、エクスペリエンスフラグメントがすぐに公開され、Target に送信されます。

1. 確認ダイアログで「**OK**」をタップ／クリックします。

   エクスペリエンスフラグメントは Target に送信されているはずです。

>[!NOTE]
>
>または、ページエディターで、 [ページ情報](/help/sites-authoring/author-environment-tools.md#page-information) メニュー

##  Target でのエクスペリエンスフラグメントの使用 {#using-your-experience-fragments-in-target}

ここまでのタスクを完了すると、エクスペリエンスフラグメントが Target のオファーページに表示されます。ご覧ください [特定の Target ドキュメント](https://experiencecloud.adobe.com/resources/help/ja_JP/target/target/aem-experience-fragments.html) そこで何を達成できるかを学ぶために

##  Target に書き出し済みのエクスペリエンスフラグメントの削除 {#deleting-an-experience-fragment-already-exported-to-target}

Target に書き出し済みのエクスペリエンスフラグメントを削除すると、そのフラグメントが既に Target のオファーで使用されている場合に問題が発生する可能性があります。フラグメントコンテンツがAEMによって配信されるので、フラグメントを削除すると、オファーが使用できなくなります。

このような状況を回避するには、次の手順に従います。

* エクスペリエンスフラグメントが現在アクティビティで使用されていない場合、AEMを使用すると、警告メッセージを表示せずにフラグメントを削除できます。
* エクスペリエンスフラグメントが現在 Target のアクティビティで使用されている場合、フラグメントを削除するとアクティビティに影響が及ぶ可能性があると、AEM ユーザーに警告メッセージが表示されます。

   AEMのエラーメッセージは、ユーザーによるエクスペリエンスフラグメントの削除（強制）を禁止していません。 エクスペリエンスフラグメントが削除された場合は、次のような結果になります。

   * AEM エクスペリエンスフラグメントを使用した Target オファーで望ましくない動作が見られる場合があります。

      * エクスペリエンスフラグメント HTML が Target にプッシュされたため、オファーが引き続きレンダリングされる可能性があります。
      * 参照されているアセットが AEM でも削除されている場合、エクスペリエンスフラグメント内の参照はどれも正しく機能しない可能性があります。
   * 当然ながら、エクスペリエンスフラグメントが AEM には存在しないため、さらに変更することは不可能です。
