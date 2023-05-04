---
title: モバイルデバイス用のページのオーサリング
seo-title: Authoring a Page for Mobile Devices
description: モバイル用にオーサリングする際に、複数のエミュレーターを切り替えて、エンドユーザーに表示される内容を確認できます
seo-description: When authoring for mobile, you can switch between several emulators to see what the end-user sees
uuid: a7a1ba68-d608-4819-88d1-0dab5955d3f4
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.4/SITES
content-type: reference
topic-tags: site-features
discoiquuid: 9554cdb3-b604-4d50-9760-89b9e7a7755f
exl-id: 97f0b0d2-7d7b-4a90-a4e5-348a306e1622
source-git-commit: c5b816d74c6f02f85476d16868844f39b4c47996
workflow-type: tm+mt
source-wordcount: '261'
ht-degree: 39%

---

# モバイルデバイス用のページのオーサリング {#authoring-a-page-for-mobile-devices}

>[!CAUTION]
>
>AEM 6.4 の拡張サポートは終了し、このドキュメントは更新されなくなりました。 詳細は、 [技術サポート期間](https://helpx.adobe.com/jp/support/programs/eol-matrix.html). サポートされているバージョンを見つける [ここ](https://experienceleague.adobe.com/docs/?lang=ja).

モバイルページをオーサリングする場合、ページはモバイルデバイスをエミュレートする方法で表示されます。 ページの作成時に、複数のエミュレーターを切り替えて、ページにアクセスする際にエンドユーザーに表示される内容を確認できます。

デバイスは、ページをレンダリングするデバイスの機能に応じて、カテゴリ機能、スマート、タッチにグループ化されます。 エンドユーザーがモバイルページにアクセスすると、AEMはデバイスを検出し、そのデバイスグループに対応する表現を送信します。

>[!NOTE]
>
>既存の標準サイトに基づいたモバイルサイトを作成するには、標準サイトのライブコピーを作成します。（[様々なチャネル用のライブコピーを作成する](/help/sites-administering/msm-livecopy.md)を参照）。
>
>AEM 開発者は、新しいデバイスグループを作成できます（「[デバイスグループフィルターの作成](/help/sites-developing/groupfilters.md)」を参照）。

次の手順を使用して、モバイルページをオーサリングします。

1. グローバルナビゲーションから&#x200B;**サイト**&#x200B;コンソールを開きます。
1. **We.Retail**／**アメリカ合衆国**／**英語**&#x200B;のページを開きます。

1. **プレビュー**&#x200B;モードに切り替えます。
1. ページ上部のデバイスアイコンをクリックして、目的のエミュレーターに切り替えます。
1. コンポーネントブラウザーからページにコンポーネントをドラッグ&amp;ドロップします。

ページは次のようになります。

![mobileipademu](assets/mobileipademu.png)

>[!NOTE]
>
>モバイルデバイスからオーサーインスタンスのページが要求されると、エミュレーターは無効になります。
