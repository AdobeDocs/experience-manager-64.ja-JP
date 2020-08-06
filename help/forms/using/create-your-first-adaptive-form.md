---
title: 最初のアダプティブフォームを作成する
seo-title: 最初のアダプティブフォームを作成する
description: 'ここでは、インタラクティブでレスポンシブな高機能のフォームを作成する方法について説明します。 '
seo-description: 'ここでは、インタラクティブでレスポンシブな高機能のフォームを作成する方法について説明します。 '
page-status-flag: de-activated
uuid: 62f5222c-c787-46be-95fa-a701aa0e6115
topic-tags: introduction
discoiquuid: 4e247e70-c50a-4571-8ac1-fbbb07100262
translation-type: tm+mt
source-git-commit: fae6d621ad61a26db99994482c16c9d9a5f88ad9
workflow-type: tm+mt
source-wordcount: '967'
ht-degree: 83%

---


# 最初のアダプティブフォームを作成する {#do-not-publish-create-your-first-adaptive-form}

![01-create-first-adaptive-form-hero-image](assets/01-create-first-adaptive-form-hero-image.png)

## 概要 {#introduction}

**アダプティブフォーム**&#x200B;は、登録が簡単で効率が高く、作業時間を削減できる、モバイルデバイスに適した&#x200B;**フォーム機能**&#x200B;です。アダプティブフォームは、モバイル、自動化、分析に適したフォームエクスペリエンスを提供します。自然に依存していて相互に関係のないフォームを簡単に作成でき、自動プロセスを使用して管理や繰り返しのタスクを減らし、データ分析を使用して、ユーザーがフォームに対する体験を改善しパーソナライズできます。

このチュートリアルでは、アダプティブフォームを作成するためのエンドツーエンドのフレームワークについて説明します。このチュートリアルは、1 つのユースケースと複数のガイドから構成されています。各ガイドでは、このチュートリアルで作成するアダプティブフォームと、このアダプティブフォームに追加する新しい機能について説明します。すべてのガイドに、作業用アダプティブフォームが用意されています。アダプティブフォームを作成するためのガイドも用意されています。その他のガイドについても、間もなく公開する予定になっています。このチュートリアルを完了すると、次の操作を実行できるようになります。

* アダプティブフォームとフォームデータモデルを作成する。
* アダプティブフォームのスタイルを設定する。
* アダプティブフォームのルールエディタ－を使用してビジネスルールを作成する。
* アダプティブフォームをテストしてパブリッシュする。

![create-daptive-form-workflow](assets/create-daptive-form-workflow.png)

最初に、このチュートリアルで使用するユースケースについて説明します。

さまざまな顧客に対応するため、幅広い製品を提供する Web サイトがあります。顧客はこの Web サイトのポータルを閲覧し、製品を選択して注文します。すべての顧客がアカウントを作成し、配送先の住所と請求先の住所を入力します。既存の顧客である Sara Rose は、Web サイトに配送先住所を追加しようとしています。Webサイトには、配送先住所の追加や更新を行うためのオンラインフォームが用意されています。

この Web サイトは Adobe Experience Manager（AEM）上で稼働し、AEM Forms を使用してデータの取得と処理を行います。住所の追加とフォームの更新は、アダプティブフォームを使用して行います。データベース内の顧客情報は Web サイト上に保存されます。利用可能なアドレスを取得して表示する際に、アドレスの追加と更新のフォームを使用します。 また、アダプティブフォームを使用して、更新後の住所と新しい住所を入力します。

### 前提条件 {#prerequisite}

* AEM オーサーインスタンスをセットアップします。
* [AEM Forms アドオン](/help/forms/using/installing-configuring-aem-forms-osgi.md)をオーサーインスタンスにインストールします。
* JDBC データベースドライバー（JAR ファイル）をデータベースプロバイダーから取得します。Examples in the tutorial are based on MySQL database and use Oracle&#39;s [MySQL JDBC database driver](https://dev.mysql.com/downloads/connector/j/5.1.html).

* 以下に示すフィールドを使用して、顧客データを保存するデータベースをセットアップします。アダプティブフォームを作成する場合、データベースは必須ではありません。このチュートリアルではデータベースを使用して、AEM Forms のフォームデータモデルと永続性機能を表示します。

![adaptiveformdata](assets/adaptiveformdata.png)

## 手順 1：アダプティブフォームを作成する {#step-create-an-adaptive-form}

![03-create-adaptive-form-main-image_small_new](assets/03-create-adaptive-form-main-image_small_new.png)

アダプティブフォームは、レスポンシブで動的な特性を持つ、柔軟性の高い次世代型の高機能なフォームです。アダプティブフォームにより、エクスペリエンスをターゲット用にカスタマイズすることができます。AEM Forms には、ドラッグアンドドロップ操作でアダプティブフォームを作成するための WYSIWYG エディターが用意されています。アダプティブフォームについて詳しくは、「[アダプティブフォームのオーサリングの概要](/help/forms/using/introduction-forms-authoring.md)」を参照してください。

ゴール:

* 顧客が配送先住所を追加するためのアダプティブフォームを作成する
* 顧客の情報を表示して保存するためのアダプティブフォームフィールドのレイアウトを設定する
* フォームコンテンツが記載された電子メールを送信するためのアクションを作成する
* アダプティブフォームのプレビューと送信を行う

   [ ![see-the-guide-sm](assets/see-the-guide-sm.png)](create-adaptive-form.md)

## 手順 2：フォームデータモデルを作成する {#step-create-form-data-model}

![05-create-form-data-model-main_small](assets/05-create-form-data-model-main_small.png)

フォームデータモデルにより、アダプティブフォームを複数の異なるデータソースに接続することができます。例えば、AEM ユーザープロファイル、RESTful Web サービス、SOAP ベースの Web サービス、OData サービス、関連データベースなどに接続することができます。フォームデータモデルは、接続されたデータソースで使用可能なビジネスエンティティとサービスの統一されたデータ表現スキーマです。フォームデータモデルをアダプティブフォームとともに使用すると、接続されたデータソースに対して、データの取得、更新、削除、追加を行うことができます。

ゴール:

* データソースとして Web サイトのデータベースインスタンス（MySQL データベース）を設定する
* MySQL データベースをデータソースとして使用して、フォームデータモデルを作成する
* データモデルオブジェクトをフォームデータモデルに追加する
* フォームデータモデルの読み取りサービスと書き込みサービスを設定する
* テストデータを使用して、フォームデータモデルと設定済みサービスをテストする

   [ ![see-the-guide-sm](assets/see-the-guide-sm.png)](create-form-data-model.md)

## 手順 3：アダプティブフォームのフィールドにルールを適用する {#step-apply-rules-to-adaptive-form-fields}

![07-apply-rules-to-adaptive-form_small](assets/07-apply-rules-to-adaptive-form_small.png)

アダプティブフォームには、アダプティブフォームオブジェクトにルールを書き込むためのエディターが用意されています。これらのルールは、フォームオブジェクト上でトリガされるアクションを定義します。それらのアクションは、事前定義された条件、ユーザ入力、およびフォーム上のユーザーアクションに基づいてトリガされます。ルールを適用することにより、フォームのフィールドに短時間で正確に情報を入力できるようになります。

ゴール:

* ルールを作成してアダプティブフォームのフィールドに適用する
* ルールを使用してフォームデータモデルサービスをトリガーし、データベースのデータを更新する

## 手順 4：アダプティブフォームのスタイルを設定する {#step-style-your-adaptive-form}

![09-Style-your-adaptive-form_small](assets/09-Style-your-adaptive-form_small.png)

Adaptive forms provide themes and an [editor](/help/forms/using/themes.md) to create themes for the adaptive forms. テーマには、コンポーネントとパネルの詳細なスタイル設定が含まれています。様々なフォームでテーマを再利用することができます。スタイルには、背景色、状態を表す色、透明度、配置、サイズなどのプロパティが含まれています。テーマをフォームに適用すると、指定したスタイルがフォームの対応コンポーネントに反映されます。アダプティブフォームは、フォーム専用スタイルのインラインスタイル設定をサポートしています。

ゴール:

* 初期設定済みテーマをアダプティブフォームに適用する
* テーマエディターを使用して、アダプティブフォームのテーマを作成する
* カスタムテーマでのWebフォントの使用

   [ ![see-the-guide-sm](assets/see-the-guide-sm.png)](style-your-adaptive-form.md)

## 手順 5：アダプティブフォームをテストする {#step-test-your-adaptive-form}

![アダプティブフォームの11テスト](assets/11-test-your-adaptive-form.png)

アダプティブフォームは、顧客とのやり取りを行う上で欠かすことができないものです。アダプティブフォームで行った変更をすべて反映させて、アダプティブフォームをテストすることが重要です。 しかし、フォームのすべてのフィールドをテストするのは面倒な作業です。AEM Formsは、アダプティブフォームのテストを自動化するSDK(Calvin SDK)を提供しています。 Calvin を使用すると、Web ブラウザーでアダプティブフォームを自動的にテストすることができます。

ゴール:

* Calvin SDK をインストールする
* アドレスフォームを変更するためのテストスイートとテストケースを作成する

To learn about SDK, see [Using Automated Tests with AEM Adaptive Form](/help/forms/using/calvin.md).

## 手順 6：アダプティブフォームをパブリッシュする {#step-publish-your-adaptive-form}

![12-publish-your-adaptive-form-_small](assets/12-publish-your-adaptive-form-_small.png)

アダプティブフォームは、AEMの [サイトページ](/help/forms/using/embed-adaptive-form-aem-sites.md)に含めることも、[フォームポータル](/help/forms/using/introduction-publishing-forms.md)を使用する AEM サイトに表示して、スタンドアロン形式（単一ページのアプリケーション）としてパブリッシュすることもできます。

ゴール:

* アダプティブフォームを単一ページアプリケーションとしてパブリッシュする

