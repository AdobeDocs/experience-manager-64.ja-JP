---
title: Apache Maven を使用して AEM プロジェクトをビルドする方法
description: このドキュメントでは、Apache Maven に基づくAEMプロジェクトをセットアップする方法について説明します
exl-id: 6ae0e387-468b-4cea-9e3f-0816d67b7621
source-git-commit: c5b816d74c6f02f85476d16868844f39b4c47996
workflow-type: tm+mt
source-wordcount: '183'
ht-degree: 72%

---

# Apache Maven を使用して AEM プロジェクトをビルドする方法 {#how-to-build-aem-projects-using-apache-maven}

>[!CAUTION]
>
>AEM 6.4 の拡張サポートは終了し、このドキュメントは更新されなくなりました。 詳細は、 [技術サポート期間](https://helpx.adobe.com/jp/support/programs/eol-matrix.html). サポートされているバージョンを見つける [ここ](https://experienceleague.adobe.com/docs/?lang=ja).

AEM 6.4 は、オンプレミス実装と AMS 実装の最新の AEM プロジェクトアーキタイプで実装されているパッケージ管理とプロジェクト構造の最新のベストプラクティスに従っています。

>[!TIP]
>
>詳しくは、以下を参照してください。
>
>* 最新の AEM プロジェクトの構造化方法について詳しくは、AEM as a Cloud Service ドキュメントの [AEM プロジェクトの構造](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/aem-project-content-package-structure.html?lang=ja)に関する記事を参照してください。
>* アーキタイプを使用して新しい AEM プロジェクトを開始する方法について詳しくは、[AEM プロジェクトのアーキタイプ](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html?lang=ja)に関するドキュメントを参照してください。
>* AEM アプリケーションのデプロイ方法について詳しくは、AEM as a Cloud Service ドキュメントの [Adobe Content Package Maven Plugin](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developer-tools/maven-plugin.html#developer-tools) に関する記事を参照してください。
>
>3 つのドキュメントはすべて AEM 6.4 に適用されます。
