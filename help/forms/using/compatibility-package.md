---
title: 互換性パッケージ
seo-title: Compatibility Package
description: 互換性パッケージをAEM Forms 6.4 にインストールすると、AEM Forms 6.3 および廃止されたアダプティブフォームテンプレートとページの Correspondence Management アセットを使用できます。
seo-description: Installing the Compatibility package on AEM Forms 6.4 allows you to use the Correspondence Management assets from AEM Forms 6.3 and deprecated adaptive forms templates and pages
uuid: e50b1ff9-c357-422a-8da8-a791ff805317
contentOwner: gtalwar
products: SG_EXPERIENCEMANAGER/6.4/FORMS
topic-tags: correspondence-management, installing
geptopics: SG_AEMFORMS/categories/jee
discoiquuid: 38a80992-2eda-4535-89af-0de34b1a9686
role: Admin
exl-id: 0bfa0e65-c4cd-4c37-b42b-bff1b777a7be
source-git-commit: e608249c3f95f44fdc14b100910fa11ffff5ee32
workflow-type: tm+mt
source-wordcount: '344'
ht-degree: 36%

---

# 互換性パッケージをインストール {#compatibility-package}

互換性パッケージをAEM Forms 6.4 にインストールすると、AEM Forms 6.3 および廃止されたアダプティブフォームテンプレートとページの Correspondence Management アセットを使用できます。

## 概要 {#overview}

AEM Forms 6.4 で顧客との通信を作成する場合は、デフォルトで推奨される方法です。AEM 6.3 FormsとAEM 6.2 Formsのレターを引き続き使用する場合は、 [AEMFD 互換性パッケージ](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html?lang=ja).

AEMFD 互換性パッケージを使用すると、AEM Forms 6.4 上のAEM Forms 6.3 および 6.2 の次のアセットを使用できます。

* AEM Forms 6.3 および 6.2 で作成されたドキュメントフラグメント
* レター
* データディクショナリ
* アダプティブフォームの非推奨のテンプレートとページ

詳細については、[互換性パッケージをインストールすることにより AEM Forms 6.4 と互換性を持つようになったアセット](/help/forms/using/compatibility-package.md#assetsmadecompatible)を参照してください。

## AEM Forms 6.4 でのAEM Forms 6.3 および 6.2 アセットのサポートの追加 {#add-support-for-aem-forms-and-assets-in-aem-forms}

アップグレードを実行した後、AEMFD 互換性パッケージをインストールしてアセットに 6.4 との互換性を持たせるには、以下を実行します。

[AEM 互換性パッケージ](/help/sites-deploying/backward-compatibility.md)が事前にインストールされていることを確認します。

1. のインストール [互換性パッケージ](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html?lang=ja).

   パッケージのアップロードとインストールについて詳しくは、 [パッケージの操作方法](/help/sites-administering/package-manager.md).

1. ログが安定したら、サーバーを再起動します。
1. アセットに 6.4 との互換性を持たせるには、移行ユーティリティを使用します。

   詳しくは、[移行ユーティリティ](/help/forms/using/migration-utility.md)を参照してください。

## 互換性パッケージをインストールすることにより AEM Forms 6.4 と互換性を持つようになったアセット {#assetsmadecompatible}

互換性パッケージをインストールすると、以下のアセットとテンプレートに AEM Forms 6.4 との互換性を保持できます。

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

* アダプティブフォームの非推奨ページ：

   * /libs/fd/af/components/page/survey
   * /libs/fd/af/components/page/tabbedenrollment
   * /libs/fd/afaddon/components/page/advancedenrollment
