---
title: 互換性パッケージ
seo-title: 互換性パッケージ
description: '互換性パッケージを AEM Forms 6.4 にインストールすると、AEM Forms 6.3 および非推奨になったアダプティブォームテンプレートとページから Correspondence Management アセットを使用できます '
seo-description: 互換性パッケージを AEM Forms 6.4 にインストールすると、AEM Forms 6.3 および非推奨になったアダプティブォームテンプレートとページから Correspondence Management アセットを使用できます
uuid: e50b1ff9-c357-422a-8da8-a791ff805317
contentOwner: gtalwar
products: SG_EXPERIENCEMANAGER/6.4/FORMS
topic-tags: correspondence-management, installing
geptopics: SG_AEMFORMS/categories/jee
discoiquuid: 38a80992-2eda-4535-89af-0de34b1a9686
translation-type: tm+mt
source-git-commit: a172fc329a2f73b563690624dc361aefdcb5397e
workflow-type: tm+mt
source-wordcount: '387'
ht-degree: 86%

---


# 互換性パッケージのインストール{#compatibility-package}

互換性パッケージを AEM Forms 6.4 にインストールすると、AEM Forms 6.3 および非推奨になったアダプティブォームテンプレートとページから Correspondence Management アセットを使用できます

## 概要 {#overview}

AEM Forms 6.4 で顧客通信を作成するためのデフォルトかつ推奨のアプローチは、インタラクティブ通信です。AEM 6.3 Forms および AEM 6.2 Forms のレターを引き続き使用するには、[AEMFD 互換性パッケージ](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq640/fd/AEM-FORMS-6.4-COMPAT)をインストールする必要があります。

AEMFD 互換性パッケージを使用すると、AEM Forms 6.4 で AEM Forms 6.3 および 6.2 の以下のアセットを使用できます。

* AEM Forms 6.3 および 6.2 で作成したドキュメントフラグメント
* レター
* データディクショナリ
* アダプティブフォームの非推奨になったテンプレートおよびページ

詳しくは、[互換性パッケージ](/help/forms/using/compatibility-package.md#assetsmadecompatible)をインストールして、AEM Forms6.4と互換性のあるアセットを参照してください。

## AEM Forms 6.4 で AEM Forms 6.3 と 6.2 のアセットのサポートを追加する {#add-support-for-aem-forms-and-assets-in-aem-forms}

アップグレードを実行した後、AEMFD 互換性パッケージをインストールしてアセットに 6.4 との互換性を持たせるには、以下を実行します。

[AEM互換パッケージ](/help/sites-deploying/backward-compatibility.md)がプレインストールされていることを確認します。

1. [互換性パッケージ](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq640/fd/AEM-FORMS-6.4-COMPAT)をインストールします。

   パッケージのアップロードおよびインストールについて詳しくは、「[パッケージの作業方法](/help/sites-administering/package-manager.md)」を参照してください。

1. ログの状態が安定したら、サーバーを再起動します。
1. アセットに 6.4 との互換性を持たせるには、移行ユーティリティを使用します。

   詳しくは、[移行ユーティリティ](/help/forms/using/migration-utility.md)を参照してください。

## 互換性パッケージをインストールすることにより AEM Forms 6.4 と互換性を持つようになったアセット {#assetsmadecompatible}

互換性パッケージをインストールすると、次のアセットとテンプレートをAEM Forms6.4と互換性のあるものにすることができます。

* AEM 6.3 以前の Correspondence Management アセット

   * [レター](/help/forms/using/create-letter.md)
   * [データディクショナリ](/help/forms/using/data-dictionary.md)
   * ドキュメントフラグメント

* アダプティブフォームの非推奨になったテンプレート

   * /libs/fd/af/templates/blankTemplate2
   * /libs/fd/af/templates/simpleEnrollmentTemplate
   * /libs/fd/af/templates/simpleEnrollmentTemplate2
   * /libs/fd/af/templates/surveyTemplate
   * /libs/fd/af/templates/surveyTemplate2
   * /libs/fd/af/templates/tabbedEnrollmentTemplate
   * /libs/fd/af/templates/tabbedEnrollmentTemplate2
   * /libs/fd/afaddon/templates/advancedEnrollmentTemplate
   * /libs/fd/afaddon/templates/advancedEnrollmentTemplate2

* アダプティブフォームの非推奨になったページ

   * /libs/fd/af/components/page/survey
   * /libs/fd/af/components/page/tabbedenrollment
   * /libs/fd/afaddon/components/page/advancedenrollment

