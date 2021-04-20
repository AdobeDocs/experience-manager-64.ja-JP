---
title: ビデオレンディション
description: ビデオレンディション
contentOwner: AG
feature: Video,Renditions
role: Business Practitioner
translation-type: tm+mt
source-git-commit: 29e3cd92d6c7a4917d7ee2aa8d9963aa16581633
workflow-type: tm+mt
source-wordcount: '225'
ht-degree: 99%

---


# ビデオレンディション {#video-renditions}

Adobe Experience Manager (AEM) Assets では、様々な形式（OGG、FLV など）のビデオアセット用のビデオレンディションを生成します。

AEM Assets では、メディアアセットの静的レンディションと動的レンディション（DM エンコードされたレンディション）がサポートされています。

静的レンディションは、FFMPEG（システムパスにインストールされ、使用できるもの）を使用してネイティブに生成され、コンテンツリポジトリに保存されます。

DM エンコードされたレンディションは、プロキシサーバーに保存され、実行時に提供されます。

AEM Assets では、クライアント側でのこのようなレンディションの再生をサポートしています。

特定のビデオアセットのレンディションを表示するには、アセットのページを開いて、グローバルナビゲーションアイコンをタップします。次に、リストから「**[!UICONTROL レンディション]**」を選択します。

![chlimage_1-478](assets/chlimage_1-478.png)

ビデオレンディションのリストが&#x200B;**[!UICONTROL レンディション]**&#x200B;パネルに表示されます。

![chlimage_1-479](assets/chlimage_1-479.png)

DM エンコードされたレンディションのプロキシサーバーを設定するには、[Dynamic Media クラウドサービス](config-dynamic.md)を設定します。

必要なパラメーターを指定してビデオレンディションを生成するには、[対応するビデオプロファイルを作成](video-profiles.md)します。

プロキシサーバーを設定し、ビデオプロファイルを作成したら、このビデオプリセットを処理プロファイルに追加して、その処理プロファイルをフォルダーに適用することができます。

>[!NOTE]
>
>Internet Explorer 11 では、OGG および WAV ファイルのオーディオは再生できません。拡張子 OGG または WAV を持つアセットの場合、アセットの詳細ページに「無効なソース」というエラーメッセージが表示されます。
>
>MS Edge および iPad では、OGG ファイルは再生できません。サポートされていない形式であるというエラーが表示されます。
