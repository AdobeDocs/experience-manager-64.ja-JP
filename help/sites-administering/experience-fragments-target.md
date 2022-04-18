---
title: エクスペリエンスフラグメントとのTarget 統合
seo-title: Target Integration with Experience Fragments
description: エクスペリエンスフラグメントとのTarget 統合
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
ht-degree: 90%

---

# エクスペリエンスフラグメントとのTarget 統合{#target-integration-with-experience-fragments}

>[!NOTE]
>
>この機能を使用するには、 [AEM 6.4 Service Pack 2(6.4.2.0)](/help/release-notes/sp-release-notes.md) または後で。

Adobe Target 向けに Adobe Experience Manager（AEM）で作成された[エクスペリエンスフラグメント](/help/sites-authoring/experience-fragments.md)を書き出すことができます。書き出したエクスペリエンスフラグメントは、Target アクティビティのオファーとして使用し、幅広くエクスペリエンスをテストおよびパーソナライズできます。これにより、AEM の使いやすさおよび機能性と、Target の強力な自動インテリジェンス（AI）機能および機械学習（ML）機能を組み合わせることができます。

## 前提条件 {#prerequisites}

様々なアクションが必要です。

1. AEM を Target と統合する必要があります。詳しくは、 [Adobe Targetとの統合](/help/sites-administering/target.md) を参照してください。
1. エクスペリエンスフラグメントはオーサーインスタンスから書き出されるので、リンクが公開インスタンスに対して確実に外部化されるように、オーサーインスタンスに [Link Externalizer を設定する](/help/sites-developing/externalizer.md)必要があります。

## クラウド設定の追加 {#add-the-cloud-configuration}

フラグメントを書き出す前に、 **クラウド設定** 対象 **Adobe Target** をフラグメントまたはフォルダーに追加します。

1. **エクスペリエンスフラグメント**&#x200B;コンソールに移動します。
1. 適切なフォルダーまたはフラグメントの&#x200B;**ページプロパティ**&#x200B;を開きます。

   >[!NOTE]
   >
   >クラウド設定をエクスペリエンスフラグメントの親フォルダーに追加すると、設定はすべての子に継承されます。
   >
   >クラウド設定をエクスペリエンスフラグメント自体に追加すると、設定はすべての変更によって継承されます。

1. **クラウドサービス**&#x200B;タブを選択します。

1. **クラウドサービス設定**&#x200B;のドロップダウンリストから、**Adobe Target** を選択します。
1. の下 **Adobe Target**、適切な設定を選択します。

1. **保存して閉じます**。

##  Target へのエクスペリエンスフラグメントの書き出し {#exporting-an-experience-fragment-to-target}

>[!NOTE]
>
>画像などのメディアアセットでは、参照のみが Target に書き出されます。アセット自体は AEM Assets に格納されたままで、AEM パブリッシュインスタンスから配信されます。
>
>このため、エクスペリエンスフラグメントは、すべての関連アセットと共に、Target に書き出す前に公開する必要があります。

AEM から Target にエクスペリエンスフラグメントを書き出すには（クラウド設定を指定した後）：

1. エクスペリエンスフラグメントコンソールに移動します。
1. Target に書き出すエクスペリエンスフラグメントを選択します。

   >[!NOTE]
   >
   >エクスペリエンスフラグメント Web のバリエーションである必要があります。

1. **Adobe Target に書き出し**&#x200B;をタップ／クリックします。

   >[!NOTE]
   >
   >エクスペリエンスフラグメントがすでに書き出されている場合は、**Adobe Target でアップデート** を選択します。

1. 要求に応じて&#x200B;**公開せずに書き出し**&#x200B;または&#x200B;**公開**&#x200B;をタップ／クリックします。

   >[!NOTE]
   >
   >「**公開**」を選択すると、エクスペリエンスフラグメントがすぐに公開され、Target に送信されます。

1. 確認ダイアログで「**OK**」をタップ／クリックします。

   エクスペリエンスフラグメントは Target に送信されているはずです。

>[!NOTE]
>
>あるいは、[ページ情報](/help/sites-authoring/author-environment-tools.md#page-information)メニューの同等のコマンドを使用して、ページエディターから書き出しを実行することもできます。

##  Target でのエクスペリエンスフラグメントの使用 {#using-your-experience-fragments-in-target}

ここまでのタスクを完了すると、エクスペリエンスフラグメントが Target のオファーページに表示されます。Target 側でできることを詳しく知るには、[Target に特化したドキュメント](https://experiencecloud.adobe.com/resources/help/ja_JP/target/target/aem-experience-fragments.html)を参照してください。

##  Target に書き出し済みのエクスペリエンスフラグメントの削除 {#deleting-an-experience-fragment-already-exported-to-target}

Target に書き出し済みのエクスペリエンスフラグメントを削除すると、そのフラグメントがすでに Target のオファーで使用されている場合に問題が発生する可能性があります。フラグメントのコンテンツが AEM によって配信されているため、フラグメントを削除するとオファーが使用できなくなります。

そのような状況を避けるためには：

* エクスペリエンスフラグメントが現在アクティビティで使用されていない場合、AEM はユーザーに警告メッセージなしでフラグメントを削除することを許可します。
* エクスペリエンスフラグメントが現在ターゲットのアクティビティで使用されている場合、フラグメントを削除するとアクティビティに影響が及ぶ可能性があると、AEM ユーザーに警告メッセージが表示されます。

   AEM のエラーメッセージは、ユーザーがエクスペリエンスフラグメントを（強制的に）削除することを禁止するものではありません。エクスペリエンスフラグメントが削除された場合

   * AEM エクスペリエンスフラグメントを使用した Target オファーで望ましくない動作が見られる場合があります。

      * エクスペリエンスフラグメント HTML が Target にプッシュされたため、オファーは引き続きレンダリングされる可能性があります。
      * 参照されているアセットが AEM でも削除されている場合、エクスペリエンスフラグメント内の参照はすべて正しく機能しない可能性があります。
   * 当然ながら、エクスペリエンスフラグメントは AEM にはもう存在しないため、さらに変更することは不可能です。
