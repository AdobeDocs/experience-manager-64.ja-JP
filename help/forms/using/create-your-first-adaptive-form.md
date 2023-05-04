---
title: 最初のアダプティブフォームを作成する
seo-title: Create your first adaptive form
description: ここでは、インタラクティブでレスポンシブな高機能のフォームを作成する方法について説明します。
seo-description: Learn to create business class, interactive, and responsive forms.
page-status-flag: de-activated
uuid: 62f5222c-c787-46be-95fa-a701aa0e6115
topic-tags: introduction
discoiquuid: 4e247e70-c50a-4571-8ac1-fbbb07100262
feature: Adaptive Forms
exl-id: f634a73a-e720-4a38-a459-6ddbe4fdc565
source-git-commit: c5b816d74c6f02f85476d16868844f39b4c47996
workflow-type: tm+mt
source-wordcount: '986'
ht-degree: 37%

---

# 最初のアダプティブフォームを作成する {#do-not-publish-create-your-first-adaptive-form}

>[!CAUTION]
>
>AEM 6.4 の拡張サポートは終了し、このドキュメントは更新されなくなりました。 詳細は、 [技術サポート期間](https://helpx.adobe.com/jp/support/programs/eol-matrix.html). サポートされているバージョンを見つける [ここ](https://experienceleague.adobe.com/docs/?lang=ja).

![01-create-first-adaptive-form-hero-image](assets/01-create-first-adaptive-form-hero-image.png)

## はじめに {#introduction}

モバイル対応の **フォームエクスペリエンス** これにより、登録が簡単になり、エンゲージメントが向上し、所要時間が短縮されます。 **アダプティブフォーム** 君にぴったりだ アダプティブフォームは、モバイル、自動化、分析に優れたフォームエクスペリエンスを提供します。 レスポンシブでインタラクティブなフォームを簡単に作成し、自動プロセスを使用して管理タスクや繰り返しタスクを減らし、データ分析を使用してフォームの顧客体験を改善し、パーソナライズできます。

このチュートリアルでは、アダプティブフォームを作成するためのエンドツーエンドのフレームワークを提供します。 このチュートリアルは、1 つのユースケースと複数のガイドに整理されています。 各ガイドでは、このチュートリアルで作成するアダプティブフォームに新しい機能を学習し、追加する方法について説明します。 各ガイドの後に、作業用のアダプティブフォームが作成されています。 アダプティブフォームの作成に関するガイドを利用できます。 その後のガイドは近日中に提供される予定です。 このチュートリアルを完了すると、次の操作を実行できるようになります。

* アダプティブフォームとフォームのデータモデルを作成します。
* アダプティブフォームのスタイルを設定します。
* アダプティブフォームのルールエディターを使用して、ビジネスルールを作成します。
* アダプティブフォームをテストして発行します。

![create-daptive-form-workflow](assets/create-daptive-form-workflow.png)

このジャーニーは、まず使用例を学ぶことから始まります。

Web サイトは、多様な顧客向けの様々な製品を提供しています。 顧客がポータルを参照し、製品を選択して注文します。 すべての顧客がアカウントを作成し、配送先と請求先の住所を提供します。 既存のお客様、Sara Rose は、配送先住所を Web サイトに追加しようとしています。 この web サイトには、配送先住所を追加および更新できるオンラインフォームが用意されています。

この Web サイトはAdobe Experience Manager(AEM) 上で動作し、データのキャプチャと処理にAEM Formsを使用します。 アドレスの追加と更新のフォームは、アダプティブフォームです。 Web サイトは、顧客の詳細をデータベースに保存します。 住所の追加と更新を行うフォームを使用して、有効な住所を取得して表示します。また、アダプティブフォームを使用して、更新された新しいアドレスを受け取ります。

### 前提条件 {#prerequisite}

* AEM オーサーインスタンスをセットアップします。
* [AEM Forms アドオン](/help/forms/using/installing-configuring-aem-forms-osgi.md)をオーサーインスタンスにインストールします。
* JDBC データベースドライバー（JAR ファイル）をデータベースプロバイダーから取得します。このチュートリアルに記載されている例は、MySQL データベースに基づいています。これらの例では、Oracle の [MySQL JDBC データベースドライバー](https://dev.mysql.com/downloads/connector/j/5.1.html)を使用しています。

* 以下に示すフィールドを使用して、顧客データを含むデータベースを設定します。 アダプティブフォームの作成にデータベースが必要なわけではありません。 このチュートリアルでは、データベースを使用して、AEM Formsのフォームデータモデルと永続性機能を表示します。

![adaptiveformdata](assets/adaptiveformdata.png)

## 手順 1：アダプティブフォームを作成する {#step-create-an-adaptive-form}

![03-create-adaptive-form-main-image_small_new](assets/03-create-adaptive-form-main-image_small_new.png)

アダプティブフォームは、新世代の、魅力的で、レスポンシブで、動的で、アダプティブなフォームです。 アダプティブフォームを使用すると、パーソナライズされたターゲットエクスペリエンスを提供することができます。 AEM Formsには、アダプティブフォームを作成するためのドラッグ&amp;ドロップ WYSIWYG エディターが用意されています。 アダプティブフォームについて詳しくは、「[アダプティブフォームのオーサリングの概要](/help/forms/using/introduction-forms-authoring.md)」を参照してください。

ゴール:

* 顧客が配送先住所を追加するためのアダプティブフォームを作成する
* 顧客の情報を表示して保存するためのアダプティブフォームフィールドのレイアウトを設定する
* フォームコンテンツが記載されたメールを送信するためのアクションを作成する
* アダプティブフォームのプレビューと送信を行う

[ ](create-adaptive-form.md)

## 手順 2：フォームデータモデルを作成する {#step-create-form-data-model}

![05-create-form-data-model-main_small](assets/05-create-form-data-model-main_small.png)

フォームデータモデルを使用すると、アダプティブフォームを異なるデータソースに接続することができます。 例えば、AEMユーザープロファイル、RESTful Web サービス、SOAP ベースの Web サービス、OData サービス、リレーショナルデータベースなどです。 フォームデータモデルは、接続されたデータソースで使用できるビジネスエンティティとサービスの統合データ表現スキーマです。 フォームデータモデルをアダプティブフォームと共に使用して、接続されたデータソースのデータを取得、更新、削除、および追加することができます。

ゴール:

* Web サイトのデータベースインスタンス（MySQL データベース）をデータソースとして設定する
* MySQL データベースをデータソースとして使用してフォームデータモデルを作成する
* データモデルオブジェクトをフォームデータモデルに追加する
* フォームデータモデルの読み取りサービスと書き込みサービスを設定する
* テストデータを使用して、フォームデータモデルと設定済みサービスをテストする

[ ](create-form-data-model.md)

## 手順 3：アダプティブフォームのフィールドにルールを適用する {#step-apply-rules-to-adaptive-form-fields}

![07-apply-rules-to-adaptive-form_small](assets/07-apply-rules-to-adaptive-form_small.png)

アダプティブフォームには、アダプティブフォームオブジェクトにルールを書き込むためのエディターが用意されています。これらのルールは、フォームオブジェクト上でトリガーできるアクションを定義します。それらのアクションは、プリセットされた条件、ユーザー入力、およびフォーム上のユーザーアクションに基づいてトリガーされます。ルールを適用することにより、フォームのフィールドに短時間で正確に情報を入力できるようになります。

ゴール:

* ルールを作成してアダプティブフォームフィールドに適用する
* ルールを使用してフォームデータモデルサービスをトリガーし、データベースのデータを更新する

## 手順 4：アダプティブフォームのスタイルを設定する {#step-style-your-adaptive-form}

![09-Style-your-adaptive-form_small](assets/09-Style-your-adaptive-form_small.png)

アダプティブフォームには、アダプティブフォームのテーマを作成するためのテーマと[エディター](/help/forms/using/themes.md)が用意されています。テーマには、コンポーネントやパネルのスタイル設定の詳細が含まれており、異なるフォームでテーマを再利用できます。 スタイルには、背景色、状態色、透明度、配置、サイズなどのプロパティが含まれます。テーマをフォームに適用すると、指定したスタイルがフォームの対応するコンポーネントに反映されます。 アダプティブフォームは、フォーム固有のスタイルのインラインスタイルもサポートしています。

ゴール:

* 標準搭載のテーマをアダプティブフォームに適用する
* テーマエディターを使用してアダプティブフォームのテーマを作成する
* カスタムテーマに web フォントを使用する

[ ](style-your-adaptive-form.md)

## 手順 5：アダプティブフォームをテストする {#step-test-your-adaptive-form}

![11-test-your-adaptive-form](assets/11-test-your-adaptive-form.png)

アダプティブフォームは、顧客とのやり取りを行う上で欠かすことができないものです。アダプティブフォームを変更したら、すべての変更点をテストすることが重要です。しかし、フォームのすべてのフィールドをテストするのは面倒な作業です。AEM Formsは、アダプティブフォームのテストを自動化する SDK(Calvin SDK) を提供します。 Calvin を使用すると、Web ブラウザーでアダプティブフォームを自動的にテストすることができます。

ゴール:

* Calvin SDK のインストール
* アドレス変更フォームのテストスイートとテストケースの作成

SDK について詳しくは、 [AEMアダプティブフォームでの自動テストの使用](/help/forms/using/calvin.md).

## 手順 6：アダプティブフォームをパブリッシュする {#step-publish-your-adaptive-form}

![12-publish-your-adaptive-form-_small](assets/12-publish-your-adaptive-form-_small.png)

アダプティブフォームは、AEMに含まれるスタンドアロンフォーム（シングルページアプリケーション）として発行することができます [サイトページ](/help/forms/using/embed-adaptive-form-aem-sites.md)またはを使用してAEMサイトにリスト [Forms Portal](/help/forms/using/introduction-publishing-forms.md).

目標：

* アダプティブフォームを単一ページアプリケーションとして発行する
