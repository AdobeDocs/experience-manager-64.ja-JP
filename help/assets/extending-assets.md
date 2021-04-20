---
title: アセットのカスタマイズと拡張
description: アセット共有とアセットエディターをカスタマイズおよび拡張する方法について説明します。これにより、ユーザーに合わせたインターフェイスと一連の機能が提供されます。
contentOwner: AG
feature: Developer Tools
role: Developer
translation-type: tm+mt
source-git-commit: 4acf159ae1b9923a9c93fa15faa38c7f4bc9f759
workflow-type: tm+mt
source-wordcount: '264'
ht-degree: 94%

---


# アセットのカスタマイズと拡張 {#customizing-and-extending-assets}

アセットエディターは、Adobe Enterprise Manager（AEM）Web サイトのユーザーがリポジトリ内のデジタルアセットを検索、表示および操作するために使用する主要なアクセスポイントです。

AEM 開発者は、アセットエディターを様々な方法でカスタマイズして拡張し、独自に対応したインターフェイスと機能のセットをユーザーに提供できます。

以下の領域における機能について、カスタマイズまたは拡張できます。

* [アセットエディターの拡張](asseteditorx.md)
* [Assets の検索機能の拡張](searchx.md)
* [メディアハンドラーとワークフローを使用したアセットの処理](media-handlers.md)
* [Assets とアクティビティストリームの統合](extending-activity-stream.md)
* [Assets のプロキシ開発](proxy.md)
* [ImageMagick の設定のベストプラクティス](best-practices-for-imagemagick.md)

## 外観と操作性のカスタマイズ  {#customizing-the-look-and-feel}

アセットエディタのルック&amp;フィールの次の要素はカスタマイズ可能です。

* ロゴ：組織の独自のロゴをインターフェイスに追加できます。
* 色およびフォント：インターフェイスで使用される色およびフォントを変更できます。
* HTML コード：より完全にカスタマイズするために、インターフェイス定義の基盤となる HTML コードを変更できます。

## レンディションのカスタマイズ  {#customizing-renditions}

AEM Assets の用語では、レンディションとは、アセットの表示形式のことを指します。通常、特定のアセットは、複数のレンディションを持つ場合があります。例えば、フルカラー画像は、1 つのレンディションをオリジナルのサイズで保持し、別のレンディションを縮小サイズで、さらに別のレンディションを縮小されグレースケールに変換された状態で保持している場合があります。

特定のアセットを利用できるレンディションは、カスタマイズできます。また、新しいレンディションを作成することもできます。
