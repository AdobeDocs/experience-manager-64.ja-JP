---
title: Dynamic Media の制限
description: 画像セットやスピンセットを作成したり、PDF をアップロードしたりする際の、ベストプラクティスと適用される制限について説明します。また、Dynamic Media でサポートしていない web ブラウザーとオペレーティングシステムの組み合わせについても学びます。
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/Dynamic-Media-Classic
geptopics: SG_SCENESEVENONDEMAND_PK/categories/ecatalogs
feature: Dynamic Media Classic,Asset Management,Image Sets,Spin Sets,eCatalog
role: User
exl-id: 0269ff24-582b-40f8-95e3-3ff4ac3a792f
source-git-commit: c5b816d74c6f02f85476d16868844f39b4c47996
workflow-type: tm+mt
source-wordcount: '271'
ht-degree: 84%

---

# Dynamic Media の制限

>[!CAUTION]
>
>AEM 6.4 の拡張サポートは終了し、このドキュメントは更新されなくなりました。 詳細は、 [技術サポート期間](https://helpx.adobe.com/jp/support/programs/eol-matrix.html). サポートされているバージョンを見つける [ここ](https://experienceleague.adobe.com/docs/?lang=ja).

次のセクションでは、Dynamic Media の制限について説明します。

このトピックには、次のセクションが含まれます。

* [アセットタイプに関する Dynamic Media のベストプラクティスと適用される制限](#best-practice-enforced-limits)
* [Dynamic Media でサポートしていない web ブラウザーとオペレーティングシステムの組み合わせ](#unsupported-browser-os)

## アセットタイプに関する Dynamic Media のベストプラクティスと適用される制限 {#best-practice-enforced-limits}

アドビでは、スピンセットや画像セットを作成したり、ページ抽出用に PDF をアップロードしたりする際、次のベストプラクティスを推奨し、次の制限を適用します。

| アセット - 制限タイプ | ベストプラクティス | 適用される制限 |
| --- | --- | --- |
| **画像** - 画像あたりのスマート切り抜き数 | 5 | 100 |
| **すべてのセット** - 1 セットあたりの重複アセット数 | 重複なし | 20 |
| **すべてのセット** - 1 セットあたりの最大アセット数 | 1 セットあたり 5～10 個の画像 | 1000 |
| **スピンセット** - 2D セットあたりの最大行数／列数 | 1 セットあたり 12～18 個の画像 | 1000 |
| **PDF** - 抽出対象となる PDF の最大ページ数 |  | 100（すべての PDF 用） |

<!-- See also [Dynamic Media limitations](/help/assets/limitations.md). -->

## Dynamic Media でサポートしていない web ブラウザーとオペレーティングシステムの組み合わせ {#unsupported-browser-os}

Dynamic Mediaでは、次の Web ブラウザーとオペレーティングシステムの組み合わせをサポートしていません。

* Internet Explorer 11 と Windows 7
* Internet Explorer 11 と Windows 8.1
* Internet Explorer 11 と Windows Phone 8.1
* Internet Explorer 11 と Windows Phone 8.1 Update
* Safari 6 と iOS 6.0.1
* Safari 7 と iOS 7.1
* Safari 7 と OS X 10.9 Mavericks
* Safari 8 と iOS 8.4
* Safari 8 と OS X 10.10 Yosemite

<!-- ## End of support for TLS 1.0 and 1.1 {#tls}

CQDOC-19433 (original ticket)
and CQDOC-19792 (removed as per this ticket December 5, 2022)

Effective September 30, 2022, Adobe Dynamic Media will end support for the following:

* TLS (Transport Layer Security) 1.0 and 1.1
* The following weak ciphers in TLS 1.2:
  * `TLS_ECDHE_RSA_WITH_AES_256_CBC_SHA384`
  * `TLS_ECDHE_RSA_WITH_AES_256_CBC_SHA`
  * `TLS_RSA_WITH_AES_256_GCM_SHA384`
  * `TLS_RSA_WITH_AES_256_CBC_SHA256`
  * `TLS_RSA_WITH_AES_256_CBC_SHA`
  * `TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA256`
  * `TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA`
  * `TLS_RSA_WITH_AES_128_GCM_SHA256`
  * `TLS_RSA_WITH_AES_128_CBC_SHA256`
  * `TLS_RSA_WITH_AES_128_CBC_SHA`
  * `TLS_RSA_WITH_CAMELLIA_256_CBC_SHA`
  * `TLS_RSA_WITH_CAMELLIA_128_CBC_SHA`
  * `TLS_ECDHE_RSA_WITH_3DES_EDE_CBC_SHA`
  * `TLS_RSA_WITH_SDES_EDE_CBC_SHA` -->
