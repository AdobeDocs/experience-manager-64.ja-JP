---
title: AEM 6.4 における後方互換性
seo-title: AEM 6.4 における後方互換性
description: アプリケーションおよび設定の AEM 6.4 との互換性を維持する方法について説明します。
seo-description: アプリケーションおよび設定の AEM 6.4 との互換性を維持する方法について説明します。
uuid: 2fa8525e-7f3b-4096-ac85-01c2c76bc9ac
contentOwner: sarchiz
products: SG_EXPERIENCEMANAGER/6.4/SITES
topic-tags: upgrading
content-type: reference
discoiquuid: 5e76fe09-4d37-4c8c-8baf-97e75689bd26
feature: Upgrading
translation-type: tm+mt
source-git-commit: 75312539136bb53cf1db1de03fc0f9a1dca49791
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---


# AEM 6.4 における後方互換性{#backward-compatibility-in-aem}

## 概要 {#overview}

>[!NOTE]
>
>互換性パッケージの範囲外のコンテンツおよび設定の変更のリストについては、[AEM 6.4](/help/sites-deploying/repository-restructuring.md)の「リポジトリの再構築」を参照してください。

AEM 6.4では、すべての機能が下位互換性を考慮して開発されています。

ほとんどの場合、AEM 6.3 を実行しているお客様は、アップグレードの際にコードやカスタマイズの修正をおこなう必要はありません。AEM 6.1および6.2のお客様は、6.3へのアップグレード時に直面する以上の中断点の変更はありません。

例外的に機能の後方互換性を維持できない場合は、6.3 の互換パッケージをインストールすることで、バンドルおよびコンテンツの後方互換性を確保できます（ダウンロード場所について詳しくは、以下の「設定方法」を参照してください）。この互換性パッケージは、AEM 6.3に準拠したアプリケーションの互換性を復元します。

互換パッケージを使用すると、AEM を互換モードで実行でき、新しい AEM 機能に対するカスタム開発を先送りできます。

>[!NOTE]
>
>互換パッケージは、AEM 6.4 での互換性を確保するために必要な開発作業を先送りする一時的なソリューションであり、アップグレード後すぐに開発をおこなって互換性の問題に対応することができない場合の最終手段としてのみ使用をお勧めします。6.4 をベースにしたカスタム開発を進め、6.4 のすべての機能を利用できるようになったら、ネイティブモードに切り替えて、互換パッケージをアンインストールすることを強くお勧めします。

![screen_shot_2018-04-05at43339pm](assets/screen_shot_2018-04-05at43339pm.png)

互換パッケージには、**ルーティング有効**&#x200B;と&#x200B;**ルーティング無効**&#x200B;の 2 つのモードがあります。

これにより、AEM 6.4 は次の 3 つのモードで実行できます。

**ネイティブモード：**

ネイティブモードは、AEM 6.4 のすべての新機能を使用したいお客様、およびすべての新機能のカスタマイズ作業をおこなうための開発をする準備ができているお客様用です。

これは、アップグレード後すぐにアプリケーションの調整をおこなう必要がある可能性があることを意味します。

**互換モード：ルーティング有効で互換パッケージをインストール**

互換モードは、後方互換性のないインターフェイスのカスタマイズがあるお客様用です。これにより、互換モードで AEM を実行でき、カスタムコードの一部と互換性のない新しい AEM 機能に関するカスタム開発を先送りできます。

**レガシーモード：ルーティング無効で互換パッケージをインストール**

レガシーモードは、互換パッケージで移行された AEM のレガシーコードまたは廃止されたコードに基づくカスタムインターフェイスを持つお客様用です。

![image2018-2-12_23-58-37](assets/image2018-2-12_23-58-37.png)

## 設定方法 {#how-to-set-up}

AEM 6.3互換パッケージは、Package Managerを使用してパッケージとしてインストールできます。 [AEM 6.3 Compatibility Packageは、Software Distribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq640/compatpack/aem-compat-cq64-to-cq63)サイトからダウンロードできます。

互換パッケージがインストールされると、次に示すように、OSGI 設定のスイッチを使用して、ルーティングを有効または無効にできます。

![screen_shot_2017-11-27at122421pm](assets/screen_shot_2017-11-27at122421pm.png)

互換パッケージがインストールされて設定されると、各機能は選択された互換モードに基づいて使用されるようになります。
