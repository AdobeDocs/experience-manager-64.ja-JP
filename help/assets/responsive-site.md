---
title: レスポンシブサイト用に最適化された画像の配信
description: Dynamic Mediaのレスポンシブコード機能を使用して最適化された画像を配信する方法
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.4/ASSETS
topic-tags: dynamic-media
content-type: reference
discoiquuid: 5edcc765-c374-4368-a0d9-e02a713a24f2
exl-id: 36bb526c-a6d9-4296-8318-97ac72d6b3ba
feature: Publishing
role: User
source-git-commit: c5b816d74c6f02f85476d16868844f39b4c47996
workflow-type: tm+mt
source-wordcount: '370'
ht-degree: 80%

---

# レスポンシブサイト用に最適化された画像の配信 {#delivering-optimized-images-for-a-responsive-site}

>[!CAUTION]
>
>AEM 6.4 の拡張サポートは終了し、このドキュメントは更新されなくなりました。 詳細は、 [技術サポート期間](https://helpx.adobe.com/jp/support/programs/eol-matrix.html). サポートされているバージョンを見つける [ここ](https://experienceleague.adobe.com/docs/?lang=ja).

レスポンシブサービング用のコードを Web 開発者と共有する場合は、レスポンシブコード機能を使用します。レスポンシブ（**[!UICONTROL RESS]**）コードをクリップボードにコピーして、Web 開発者と共有することができます。

この機能は、Web サイトがサードパーティの WCM で稼動する場合に有効です。ただし、Web サイトが AEM で稼動する場合は、オフサイトの Image Server が画像をレンダリングして Web ページに提供します。

関連トピック [Web ページへのビデオビューアの埋め込み。](embed-code.md)

[Web アプリケーションへの URL のリンク](linking-urls-to-yourwebapplication.md)も参照してください。

**レスポンシブサイトに最適化された画像を配信するには**：

1. レスポンシブコードを提供する画像の場所に移動して、ドロップダウンメニューで「**[!UICONTROL レンディション]**」をタップします。

   ![chlimage_1-408](assets/chlimage_1-408.png)

1. レスポンシブ画像プリセットを選択します。「**[!UICONTROL URL]**」ボタンと「**[!UICONTROL RESS]**」ボタンが表示されます。

   ![chlimage_1-409](assets/chlimage_1-409.png)

   >[!NOTE]
   >
   >「**[!UICONTROL URL]**」ボタンまたは「**[!UICONTROL RESS]**」ボタンを使用可能にするには、選択したアセット&#x200B;*と*&#x200B;選択した画像プリセットまたはビューアプリセットを公開する必要があります。
   >
   >Dynamic Media - ハイブリッドモードでは、画像プリセットを手動で公開する必要があります。Dynamic Media - Scene7 モードでは、画像プリセットが自動的に公開されます。

1. 「**[!UICONTROL RESS]**」をタップします。

   ![chlimage_1-410](assets/chlimage_1-410.png)

1. **[!UICONTROL レスポンシブ画像を埋め込み]**&#x200B;ダイアログボックスで、レスポンシブコードテキストを選択してコピーし Web サイトに貼り付けて、レスポンシブアセットにアクセスします。
1. 埋め込みコード内のデフォルトのブレークポイントを編集し、コード内で直接レスポンシブ Web サイトのブレークポイントに一致させます。 また、異なるページのブレークポイントで、異なる解像度の画像が配信されることをテストします。

## HTTP/2 による Dynamic Media アセットの配信 {#using-http-to-delivery-your-dynamic-media-assets}

HTTP/2 は、ブラウザーとサーバーの通信方法を改善する、新しく更新された web プロトコルです。情報の転送を高速化し、必要な処理能力を削減します。Dynamic Media アセットの配信は HTTP/2 を使用して行うことができ、応答時間と読み込み時間を短縮できます。

Dynamic Media アカウントでの HTTP/2 の使用方法について詳しくは、[コンテンツの HTTP/2 配信](http2.md)を参照してください。
