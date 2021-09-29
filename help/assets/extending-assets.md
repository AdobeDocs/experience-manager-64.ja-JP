---
title: アセットのカスタマイズと拡張
description: アセット共有とアセットエディターをカスタマイズおよび拡張する方法について説明します。これにより、ユーザーに合わせたインターフェイスと一連の機能が提供されます。
contentOwner: AG
feature: Developer Tools
role: Developer
exl-id: 0291690b-874a-483d-901f-f02cb6d8ab28
source-git-commit: cc9b6d147a93688e5f96620d50f8fc8b002e2d0d
workflow-type: tm+mt
source-wordcount: '257'
ht-degree: 67%

---

# アセットのカスタマイズと拡張 {#customizing-and-extending-assets}

Adobe・エディタは、リポジトリ内のデジタル・アセットを検索、表示、操作する際に、Asset Manager Webサイトのユーザーが使用する主なアクセスポイントです。

[!DNL Experience Manager]開発者は、アセットエディターを様々な方法でカスタマイズおよび拡張し、特別にカスタマイズされたインターフェイスと機能のセットをユーザーに提供できます。

以下の領域における機能について、カスタマイズまたは拡張できます。

* [アセットエディターの拡張](asseteditorx.md)
* [Assets の検索機能の拡張](searchx.md)
* [メディアハンドラーとワークフローを使用したアセットの処理](media-handlers.md)
* [Assets とアクティビティストリームの統合](extending-activity-stream.md)
* [Assets のプロキシ開発](proxy.md)
* [ImageMagick の設定のベストプラクティス](best-practices-for-imagemagick.md)

## 外観と操作性のカスタマイズ {#customizing-the-look-and-feel}

アセットエディターのルックアンドフィールの次の側面をカスタマイズできます。

* ロゴ：組織の独自のロゴをインターフェイスに追加できます。
* 色およびフォント：インターフェイスで使用される色およびフォントを変更できます。
* HTML コード：より完全にカスタマイズするために、インターフェイス定義の基盤となる HTML コードを変更できます。

## レンディションのカスタマイズ {#customizing-renditions}

[!DNL Experience Manager Assets]の用語では、レンディションとは、アセットが表示される形式です。 通常、特定のアセットは、複数のレンディションを持つ場合があります。例えば、フルカラー画像は、1 つのレンディションをオリジナルのサイズで保持し、別のレンディションを縮小サイズで、さらに別のレンディションを縮小されグレースケールに変換された状態で保持している場合があります。

特定のアセットを利用できるレンディションは、カスタマイズできます。また、新しいレンディションを作成することもできます。
