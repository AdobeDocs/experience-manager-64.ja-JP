---
title: アセットのカスタマイズと拡張
description: アセット共有とアセットエディターのカスタマイズと拡張をおこなう方法について説明します。これにより、ユーザーに合わせたインターフェイスと一連の機能が提供されます。
contentOwner: AG
feature: Developer Tools
role: Developer
exl-id: 0291690b-874a-483d-901f-f02cb6d8ab28
source-git-commit: c5b816d74c6f02f85476d16868844f39b4c47996
workflow-type: tm+mt
source-wordcount: '293'
ht-degree: 45%

---

# アセットのカスタマイズと拡張 {#customizing-and-extending-assets}

>[!CAUTION]
>
>AEM 6.4 の拡張サポートは終了し、このドキュメントは更新されなくなりました。 詳細は、 [技術サポート期間](https://helpx.adobe.com/jp/support/programs/eol-matrix.html). サポートされているバージョンを見つける [ここ](https://experienceleague.adobe.com/docs/?lang=ja).

アセットエディターは、Adobe Enterprise Manager の web サイトのユーザーがリポジトリー内のデジタルアセットを検索、表示および操作するために使用する主要なアクセスポイントです。

[!DNL Experience Manager] の開発者は、アセットエディターを様々な方法でカスタマイズして拡張し、ユーザーに合わせたインターフェイスと一連の機能を提供できます。

以下の領域における機能について、カスタマイズまたは拡張できます。

* [アセットエディターの拡張](asseteditorx.md)
* [Assets 検索の拡張](searchx.md)
* [メディアハンドラーとワークフローを使用したアセットの処理](media-handlers.md)
* [Assets と Activity Stream の統合](extending-activity-stream.md)
* [Assets プロキシ開発](proxy.md)
* [ImageMagick の設定のベストプラクティス](best-practices-for-imagemagick.md)

## ルックアンドフィールのカスタマイズ {#customizing-the-look-and-feel}

アセットエディターの外観と操作性に関する以下の特性をカスタマイズできます。

* ロゴ：インターフェイスには、独自の組織のロゴを追加できます。
* 色とフォント：インターフェイスで使用する色とフォントを変更できます。
* HTMLコード：より徹底的なカスタマイズを行うには、インターフェイスを定義する基になるHTMLコードを変更します。

## レンディションのカスタマイズ {#customizing-renditions}

[!DNL Experience Manager Assets] の用語では、レンディションとは、アセットが表示されるフォームを指します。一般に、特定のアセットに複数のレンディションが含まれる場合があります。 例えば、フルカラー画像の場合は、元のサイズのレンディションと、縮小されたサイズのレンディション、縮小された後グレースケールに変換されたレンディションがあります。

特定のアセットが使用可能なレンディションは、カスタマイズしたり、新しく作成したりできます。
