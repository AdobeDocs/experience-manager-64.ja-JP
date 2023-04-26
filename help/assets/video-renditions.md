---
title: ビデオレンディション
description: ビデオレンディション
contentOwner: AG
feature: Video,Renditions
role: User
exl-id: 9fc93034-e83a-42b5-901d-7867b4a850a8
source-git-commit: 1e3cd6ce3138113721183439f7cfb9daed6e0e58
workflow-type: tm+mt
source-wordcount: '220'
ht-degree: 77%

---

# ビデオレンディション {#video-renditions}

Adobe Experience Manager Assets では、様々な形式（OGG、FLV など）のビデオアセット用のビデオレンディションが生成されます。

AEM Assetsは、メディアアセットの静的レンディションと動的レンディション（DM エンコードされたレンディション）をサポートしています。

静的レンディションは、FFMPEG（システムパスにインストールされ、使用できるもの）を使用してネイティブに生成され、コンテンツリポジトリに保存されます。

DM エンコードされたレンディションは、プロキシサーバーに保存され、実行時に提供されます。

AEM Assets では、クライアント側でのこのようなレンディションの再生をサポートしています。

特定のビデオアセットのレンディションを表示するには、アセットのページを開いて、グローバルナビゲーションアイコンをタップします。次に、リストから「**[!UICONTROL レンディション]**」を選択します。

![chlimage_1-478](assets/chlimage_1-478.png)

ビデオレンディションのリストが&#x200B;**[!UICONTROL レンディション]**&#x200B;パネルに表示されます。

![chlimage_1-479](assets/chlimage_1-479.png)

DM エンコードされたレンディションのプロキシサーバーを設定するには、次の手順を実行します。 [Dynamic Media Cloud Services を設定します。](config-dynamic.md)

必要なパラメーターを持つビデオレンディションを生成するには、 [対応するビデオプロファイルを作成する](video-profiles.md).

プロキシサーバーを設定し、ビデオプロファイルを作成したら、このビデオプリセットを処理プロファイルに追加して、その処理プロファイルをフォルダーに適用することができます。

>[!NOTE]
>
>Internet Explorer 11 の OGG および WAV ファイルでは、オーディオ再生は機能しません。 拡張子 OGG または WAV を持つアセットの場合、アセットの詳細ページに「無効なソース」というエラーメッセージが表示されます。
>
>MS Edge および iPad では、OGG ファイルは再生できません。サポートされていない形式であるというエラーが表示されます。
