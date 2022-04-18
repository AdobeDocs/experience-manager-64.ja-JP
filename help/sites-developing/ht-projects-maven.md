---
title: Apache Maven を使用して AEM プロジェクトをビルドする方法
description: このドキュメントでは、Apache Maven に基づく AEM プロジェクトを設定する方法について説明します
exl-id: 6ae0e387-468b-4cea-9e3f-0816d67b7621
source-git-commit: cda63b9ece88d8172fa4d9817e315c9cff88c224
workflow-type: tm+mt
source-wordcount: '151'
ht-degree: 94%

---

# Apache Maven を使用して AEM プロジェクトをビルドする方法 {#how-to-build-aem-projects-using-apache-maven}

AEM 6.4 は、オンプレミス実装と AMS 実装の最新の AEM プロジェクトアーキタイプで実装されているパッケージ管理とプロジェクト構造の最新のベストプラクティスに従っています。

>[!TIP]
>
>詳しくは、以下を参照してください。
>
>* 最新の AEM プロジェクトの構造化方法について詳しくは、AEM as a Cloud Service ドキュメントの [AEM プロジェクトの構造](https://docs.adobe.com/content/help/ja-JP/experience-manager-cloud-service/implementing/developing/aem-project-content-package-structure.html)に関する記事を参照してください。
>* アーキタイプを使用して新しい AEM プロジェクトを開始する方法について詳しくは、[AEM プロジェクトのアーキタイプ](https://docs.adobe.com/content/help/ja-JP/experience-manager-core-components/using/developing/archetype/overview.html)に関するドキュメントを参照してください。
>* AEM アプリケーションのデプロイ方法について詳しくは、AEM as a Cloud Service ドキュメントの [Adobe Content Package Maven Plugin](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developer-tools/maven-plugin.html#developer-tools) に関する記事を参照してください。
>
>3 つのドキュメントはすべて AEM 6.4 に適用されます。
