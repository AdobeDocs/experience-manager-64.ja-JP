---
title: エクスペリエンスフラグメントとのTarget 統合
seo-title: エクスペリエンスフラグメントとのTarget 統合
description: エクスペリエンスフラグメントとのTarget 統合
seo-description: エクスペリエンスフラグメントとのTarget 統合
uuid: 621f57d4-3b8d-49ea-b193-8530c8fbd74e
contentOwner: carlino
products: SG_EXPERIENCEMANAGER/6.4/SITES
topic-tags: integration
content-type: reference
discoiquuid: 6911c8e3-b12c-466e-8255-5dcd09557d35
translation-type: tm+mt
source-git-commit: 4e5d3c0ae71f601bcf39fa768c8b5ac86decc1eb
workflow-type: tm+mt
source-wordcount: '657'
ht-degree: 76%

---


# エクスペリエンスフラグメントとのTarget 統合{#target-integration-with-experience-fragments}

>[!NOTE]
>
>この機能には、[AEM 6.4 Service Pack 2 (6.4.2.0)](/help/release-notes/sp-release-notes.md)以降が必要です。

Adobe Target 向けに Adobe Experience Manager（AEM）で作成された[エクスペリエンスフラグメント](/help/sites-authoring/experience-fragments.md)を書き出すことができます。書き出したエクスペリエンスフラグメントは、Target アクティビティのオファーとして使用し、幅広くエクスペリエンスをテストおよびパーソナライズできます。これにより、AEM の使いやすさおよび機能性と、Target の強力な自動インテリジェンス（AI）機能および機械学習（ML）機能を組み合わせることができます。

## 前提条件 {#prerequisites}

様々なアクションが必要です。

1. AEM を Target と統合する必要があります。詳しくは、[Adobe Targetとの統合](/help/sites-administering/target.md)を参照してください。
1. エクスペリエンスフラグメントはオーサーインスタンスから書き出されるので、リンクが公開インスタンスに対して確実に外部化されるように、オーサーインスタンスに [Link Externalizer を設定する](/help/sites-developing/externalizer.md)必要があります。

## 追加クラウド設定{#add-the-cloud-configuration}

フラグメントを書き出す前に、**Adobe Target**&#x200B;の&#x200B;**クラウド設定**&#x200B;をフラグメントまたはフォルダーに追加する必要があります。

1. **エクスペリエンスフラグメント**&#x200B;コンソールに移動します。
1. 適切なフォルダーまたはフラグメントの&#x200B;**ページのプロパティ**&#x200B;を開きます。

   >[!NOTE]
   >
   >クラウド設定をエクスペリエンスフラグメントの親フォルダーに追加すると、設定はすべての子に継承されます。
   >
   >クラウド設定をエクスペリエンスフラグメント自体に追加すると、設定はすべての変更によって継承されます。

1. 「**クラウドサービス**」タブを選択します。

1. **クラウドサービス設定**&#x200B;のドロップダウンリストから、**Adobe Target** を選択します。
1. **Adobe Target**&#x200B;の下で、適切な設定を選択します。

1. **保存して閉じます**。

## Target へのエクスペリエンスフラグメントの書き出し  {#exporting-an-experience-fragment-to-target}

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
   >「**発行**」を選択すると、エクスペリエンスフラグメントが直ちに発行され、ターゲットに送信されます。

1. 確認ダイアログで「**OK**」をタップまたはクリックします。

   エクスペリエンスフラグメントは Target に送信されているはずです。

>[!NOTE]
>
>あるいは、[ページ情報](/help/sites-authoring/author-environment-tools.md#page-information)メニューの同等のコマンドを使用して、ページエディターから書き出しを実行することもできます。

## Target でのエクスペリエンスフラグメントの使用  {#using-your-experience-fragments-in-target}

上記のタスクを実行した後、エクスペリエンスフラグメントはターゲットのオファーページに表示されます。 Target 側でできることを詳しく知るには、[Target に特化したドキュメント](https://experiencecloud.adobe.com/resources/help/en_US/target/target/aem-experience-fragments.html)を参照してください。

## Target に書き出し済みのエクスペリエンスフラグメントの削除 {#deleting-an-experience-fragment-already-exported-to-target}

Target に書き出し済みのエクスペリエンスフラグメントを削除すると、そのフラグメントがすでに Target のオファーで使用されている場合に問題が発生する可能性があります。フラグメントのコンテンツが AEM によって配信されているため、フラグメントを削除するとオファーが使用できなくなります。

そのような状況を避けるためには：

* エクスペリエンスフラグメントが現在アクティビティで使用されていない場合、AEM はユーザーに警告メッセージなしでフラグメントを削除することを許可します。
* エクスペリエンスフラグメントが現在ターゲットのアクティビティで使用されている場合、フラグメントを削除するとアクティビティに影響が及ぶ可能性があると、AEM ユーザーに警告メッセージが表示されます。

   AEM のエラーメッセージは、ユーザーがエクスペリエンスフラグメントを（強制的に）削除することを禁止するものではありません。エクスペリエンスフラグメントを削除する場合：

   * AEMエクスペリエンスフラグメントを含むターゲットオファーで、意図しない動作が表示される場合があります。

      * エクスペリエンスフラグメントのHTMLがターゲットにプッシュされたので、オファーは引き続きレンダリングされる可能性が高くなります。
      * AEMで参照アセットも削除された場合、エクスペリエンスフラグメント内の参照が正しく機能しない可能性があります。
   * もちろん、エクスペリエンスフラグメントに対するそれ以上の変更は、そのエクスペリエンスフラグメントがAEMに存在しなくなったので、不可能です。


