---
title: SCF サンドボックスの作成
seo-title: SCF サンドボックスの作成
description: このチュートリアルは、AEM の知識がなく、SCF コンポーネントの使用に興味を持っている開発者を主な対象としています。手順に従いながら SCF サンドボックスサイトの作成を進めることができます
seo-description: このチュートリアルは、AEM の知識がなく、SCF コンポーネントの使用に興味を持っている開発者を主な対象としています。手順に従いながら SCF サンドボックスサイトの作成を進めることができます
uuid: ee52e670-e1e6-4bcd-9548-c963142e6704
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.4/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: e1b5c25d-cbdd-421c-b81a-feb6039610a3
exl-id: f8cd2866-6e4d-47e6-b9aa-c2190b0b1b7b
source-git-commit: bd94d3949f0117aa3e1c9f0e84f7293a5d6b03b4
workflow-type: tm+mt
source-wordcount: '528'
ht-degree: 55%

---

# SCF サンドボックスの作成  {#create-an-scf-sandbox}


AEM 6.1 Communities 以降では、サンドボックスをすばやく作成するのに最も簡単な方法は、コミュニティサイトを作成することです。[AEM Communitiesの概要](getting-started.md)を参照してください。

開発者にとっても便利なツールとして、コミュニティコンポーネントガイド[もあります。コミュニティコンポーネントガイド](components-guide.md)では、コミュニティコンポーネントと機能の調査と迅速なプロトタイピングを行うことができます。

Webサイトの作成の演習は、コミュニティ機能を含むAEM Webサイトの構造を理解するのに役立ちます。また、[ソーシャルコンポーネントフレームワーク(SCF)](scf.md)の操作を調べる簡単なページも提供します。

このチュートリアルは、AEM の知識がなく、SCF コンポーネントの使用に興味を持っている開発者を主な対象としています。手順に従いながら SCF サンドボックスサイトの作成を進めることができます（ナビゲーション、ロゴ、検索、ツールバー、子ページのリスト表示など、サイト構造に焦点を当てた「[完全に機能するインターネットWebサイトを作成する方法](../../help/sites-developing/website.md)」のチュートリアルと同様）。

オーサーインスタンスで開発を行い、パブリッシュインスタンスでサイトを試してみるのがベストです。

このチュートリアルは次の手順で構成されています。

* [Web サイト構造のセットアップ](setup-website.md)
* [初期サンドボックスアプリケーション](initial-app.md)
* [初期サンドボックスコンテンツ](initial-content.md)
* [サンドボックスアプリケーションの開発](develop-app.md)
* [clientlib の追加](add-clientlibs.md)
* [サンドボックスコンテンツの開発](develop-content.md)

>[!CAUTION]
>
>このチュートリアルでは、[コミュニティサイトコンソール](sites-console.md)を使用して作成するような機能を持つコミュニティサイトは作成しません。例えば、このチュートリアルでは、ログイン、自己登録、[ソーシャルログイン](social-login.md)、メッセージング、プロファイルなどの設定方法については説明しません。
>
>単純なコミュニティサイトが必要な場合は、[サンプルページの作成](create-sample-page.md)のチュートリアルに従ってください。

## 前提条件 {#prerequisites}

このチュートリアルでは、[最新リリース](deploy-communities.md#latest-releases)の Communities を備えた 1 つの AEM オーサーと 1 つの AEM パブリッシュインスタンスがインストールされていることを前提としています。

次に、AEM プラットフォームを初めて使用する開発者にとって役立つリンクをいくつか紹介します。

* [はじめに](../../help/sites-deploying/deploy.md#getting-started)  - AEMインスタンスのデプロイ

   * [基本](../../help/sites-developing/the-basics.md)  - Webサイトおよび機能の開発者向け
   * [作成者の最初の手順](../../help/sites-authoring/first-steps.md)  — ページコンテンツのオーサリング

## CRXDE Lite 開発環境の使用 {#using-crxde-lite-development-environment}

AEM 開発者は、オーサーインスタンス上の [CRXDE Lite](../../help/sites-developing/developing-with-crxde-lite.md) 開発環境で多くの時間を費やすことになります。CRXDE Liteは、CRXリポジトリへのアクセスを制限しません。 クラシックUIツールとタッチ操作対応UIコンソールを使用すると、CRXリポジトリの特定の部分に対して、より構造化されたアクセスが可能になります。

管理者権限でサインインした後、さまざまな方法で CRXDE Lite にアクセスできます。

1. グローバルナビゲーションから、ナビゲーション&#x200B;**[!UICONTROL ツール/CRXDE Lite]**&#x200B;を選択します。

   ![chlimage_1-350](assets/chlimage_1-350.png)

2. [クラシックUIのようこそページ](http://localhost:4502/welcome.html)から、下にスクロールして、右側のパネルの「**[!UICONTROL CRXDE Lite]**」をクリックします。

   ![chlimage_1-351](assets/chlimage_1-351.png)

3. `CRXDE Lite`を直接参照します。`<server>:<port>/crx/de`

   例えば、ローカルのオーサーインスタンスの場合は、次のようになります。` [http://localhost:4502/crx/de](http://localhost:4502/crx/de)`

CRXDE Lite を使用するには、開発者または管理者権限でサインインする必要があります。デフォルトのlocalhostインスタンスの場合、

* `username: admin`
* `password: admin`


**このロ** グインがタイムアウトするので、CRXDe Liteのツールバーの右端にあるプルダウンを使用して定期的に再ログインする必要があります。

ログインしていない状態では、JCR リポジトリをナビゲートしたり、編集／保存操作を実行したりすることはできません。

******&#x200B;疑わしい場合は、ログインし直してください。

![chlimage_1-352](assets/chlimage_1-352.png)
