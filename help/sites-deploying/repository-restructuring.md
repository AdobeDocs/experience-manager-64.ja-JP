---
title: AEM 6.4 におけるリポジトリの再構築
seo-title: Repository Restructuring in AEM 6.4
description: AEM 6.4 におけるリポジトリ再構築の基礎と基本的な考え方について説明します。
seo-description: Learn about the basics and reasoning behind the repository restructuring in AEM 6.4
uuid: e9cd3e88-e352-44a8-9b97-69488d3267cb
contentOwner: chaikels
products: SG_EXPERIENCEMANAGER/6.4/SITES
content-type: reference
topic-tags: repo_restructuring
discoiquuid: fc879b0b-823b-4bdc-aaa6-36f53a33fb22
feature: Upgrading
exl-id: 6ff5a23a-c9b5-49ca-87b2-ba01eaf48a9f
source-git-commit: cda63b9ece88d8172fa4d9817e315c9cff88c224
workflow-type: tm+mt
source-wordcount: '537'
ht-degree: 78%

---

# AEM 6.4 におけるリポジトリの再構築{#repository-restructuring-in-aem}

## はじめに {#introduction}

AEM 6.4 以前は、顧客コードは、JCR の予期しない領域にデプロイされていましたが、アップグレード時に変更される可能性がありました。 このため、正式なAEMリリースでは、カスタムコード、設定またはコンテンツが上書きされることがよくありました。 逆に、カスタムのコードや設定やコンテンツが AEM の製品コードやコンテンツを上書きしてしまい、製品の機能が損なわれることもありました。

AEM 製品コードとカスタムコードの階層を明確に記述すれば、このような競合を回避できます。

そのために、AEM 6.4 以降のリリースで引き続き、コンテンツは/etc からリポジトリ内の他のフォルダーに再構築されます。また、次の大まかなルールに従って、コンテンツの移動先に関するガイドラインも追加されます。

* AEM 製品コードは必ず /libs 下に配置されます。このフォルダーをカスタムコードで上書きしてはなりません。
* カスタムコードは/apps、/content および/conf に配置する必要があります

## 6.4 へのアップグレード時の影響 {#impact-on-upgrades}

AEM 6.4 にアップグレードすると、/etc の下にあるコンテンツの大部分がリポジトリ内の他のフォルダーに複製されます。これらの新しい場所は、コンテンツが優先的に参照される場所になります。ただし、AEM 6.4 にアップグレードしても /etc フォルダー内の以前の場所との下位互換性を保つことができるようにあらゆる試みがおこなわれてきた結果、ほとんどの場合、顧客のアプリケーションで変更が活発に（多くの場合、手動で）おこなわれるまでは、AEM コードで古い場所が引き続き参照されます。スケジュールの観点からは、変更は次の 2 つのカテゴリに分かれます。

* 6.4 へのアップグレード時におこなう変更 - /etc 再構築に伴う一部の変更は下位互換性がないので、AEM 6.4 へのアップグレードの一環として変更を計画し実行してください。
* 6.5 へのアップグレードまでにおこなう変更 - /etc 再構築に伴う大部分の変更は、今後のアップグレードまで先送りすることができます。既に述べたように、顧客へのリリースの一環として変更が実行されるまで、AEM 6.4 コードでは古い場所を引き続き参照します。どうしても変更が必要になるようなスケジュールはありませんが、6.5 へのアップグレードまでには変更をおこなうことをお勧めします。今後提供される機能では、新しい場所を参照することが前提になる可能性があるからです。また、所定の機能のドキュメントは、慣例的に新しい場所を参照することになるので、古い場所がまだ使用されていると、混乱が生じるおそれがあります。

### 再構築の手引き {#restructuring-guidance}

AEM 6.4 へのアップグレードを計画している場合は、作業量を評価するために以下のソリューションごとのページを参照してください。

* [すべての AEM ソリューションに共通のリポジトリ再構築](/help/sites-deploying/all-repository-restructuring-in-aem-6-4.md)
* [AEM Sites のリポジトリ再構築](/help/sites-deploying/sites-repository-restructuring-in-aem-6-4.md)
* [AEM Assetsリポジトリの再構築](https://experienceleague.adobe.com/docs/experience-manager-64/deploying/restructuring/repository-restructuring.html?lang=ja)
* [AEM Assets Dynamic Media のリポジトリ再構築](/help/sites-deploying/dynamicmedia-repository-restructuring-in-aem-6-4.md)
* [AEM Formsリポジトリの再構築](/help/sites-deploying/forms-repository-restructuring-in-aem-6-4.md)
* [AEM Communitiesリポジトリの再構築](/help/sites-deploying/communities-repository-restructuring-in-aem-6-4.md)
* [AEM Commerce のリポジトリ再構築](/help/sites-deploying/ecommerce-repository-restructuring-in-aem-6-4.md)

各ページは、必要な変更の緊急度に応じて 2 つの節に分かれます。「6.4 へのアップグレード時におこなう変更」で説明している作業はすべて、AEM 6.4 へのアップグレードプロジェクトの一環として取り組んでください。「6.5 へのアップグレードまでにおこなう変更」で説明している作業はすべて、次のアップグレードまで任意に先送りすることができます。

ページの各項目には、「再構築の手引き」フィールドが含まれています。ここには、新しい 6.4   以前/etc フォルダーに配置されていたコンテンツで、新しい場所が参照されるようにリポジトリモデルを作成します。 追加の「メモ」フィールドには、有用な関連情報が記載されています。
