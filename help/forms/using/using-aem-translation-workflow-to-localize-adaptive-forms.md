---
title: AEM 翻訳ワークフローを使用したアダプティブフォームとレコードのドキュメントのローカライズ
seo-title: Using AEM translation workflow to localize adaptive forms and document of record
description: AEM 翻訳ワークフローを使用してアダプティブフォームとレコードのドキュメントをローカライズする方法について説明します。
seo-description: Learn to use AEM translation workflows to localize adaptive forms and document of record.
uuid: 6c87a283-0203-4cf7-989a-3770ddbbbd6e
content-type: reference
topic-tags: develop
discoiquuid: f5642571-9657-4ca1-93c5-4ae2eb91e967
noindex: true
feature: Adaptive Forms
exl-id: 5d0dcf4d-8995-4547-acb1-4917696af95e
source-git-commit: bd94d3949f0117aa3e1c9f0e84f7293a5d6b03b4
workflow-type: tm+mt
source-wordcount: '753'
ht-degree: 94%

---

# AEM 翻訳ワークフローを使用したアダプティブフォームとレコードのドキュメントのローカライズ {#using-aem-translation-workflow-to-localize-adaptive-forms-and-document-of-record}

フォームのローカライズにより、様々な地域の幅広い対象者に向けてフォームを提供できるようになります。アダプティブフォームおよびレコードのドキュメントをローカライズするには、Adobe Experience Manager 翻訳ワークフローが役立ちます。アダプティブフォームのローカライズには、**機械翻訳**&#x200B;または&#x200B;**人による翻訳**&#x200B;を使用することができます。

この記事では、アダプティブフォームおよびレコードのドキュメントに対する AEM 翻訳ワークフローの使用手順を説明します。

## 機械翻訳によるアダプティブフォームおよびレコードのドキュメントのローカライズ {#localizing-an-adaptive-form-and-document-of-record-using-machine-translation}

機械翻訳サービスを使用すると、アダプティブフォームおよびレコードのドキュメントを即座に翻訳することができます。AEM Forms では、機械翻訳に Microsoft Translator の体験版を使用することが事前に定義されています。アダプティブフォームおよびレコードのドキュメントの機械翻訳を有効にするには、次の手順を実行します。

1. AEM Forms UI 上でフォームを選択し、「**辞書の追加**」オプションをタップします。
1. **辞書を翻訳プロジェクトに追加**&#x200B;画面で、「**新しい翻訳プロジェクトを作成**」または「**既存の翻訳プロジェクトを追加**」オプションを選択します。
1. 「**プロジェクトタイトル**」フィールドでタイトルを指定します。例：`Government Reference Site - German locale.`
1. 「**ターゲット言語**」フィールドでロケールを指定し（例えば `German(de)` と入力します）、「**完了**」をクリックします。ロケールは複数指定できます。フォームが「**ターゲット言語**」フィールドで指定されたすべてのロケールに翻訳されます。
1. 辞書が追加された際のダイアログボックスで、「**プロジェクトを開く**」をクリックします。プロジェクト画面で、新しく作成されたプロジェクトを開きます。
1. **翻訳の概要**&#x200B;タイルの下部にある「**三点リーダー**」をクリックします。翻訳の概要画面が開きます。
1. **翻訳の概要**&#x200B;画面の上部にある「**編集**」アイコンをクリックします。「**翻訳**」タブを開き、**翻訳方法**&#x200B;画面で機械翻訳を選択します。適切な&#x200B;**翻訳プロバイダー**&#x200B;と&#x200B;**クラウド設定**&#x200B;を選択します。画面の上部にある「**完了**」アイコンをクリックします。
1. **翻訳ジョブ**&#x200B;タイルで ![aem62forms_downarrow](assets/aem62forms_downarrow.png) アイコンをクリックし、「**開始**」をクリックします。タイルのステータスがドラフトに変わります。翻訳を完了すると、ステータスは&#x200B;**レビューへの準備完了**&#x200B;に変わります。数分待ってからページを更新し、ステータスを確認してください。
1. **翻訳ジョブ**&#x200B;タイルのステータスが&#x200B;**レビューへの準備完了**&#x200B;に変わったことを確認できたら、ブラウザーウィンドウでフォームを開きます。ローカライズバージョンのフォームが表示されます。

   >[!NOTE]
   >
   >* ブラウザーウィンドウでローカライズバージョンのフォームを開く前に、ブラウザーのロケールがフォームと同じロケールに設定されていることを確認してください。例えば、フォームがドイツ語（de）に翻訳されているときは、ブラウザーのロケールをドイツ語（de）に設定します。
   >* アダプティブフォームのコンポーネントは、右から左 (RTL) 言語をサポートしていません。 （例：ヘブライ語）。


   アダプティブフォームと共に、自動生成されるレコードのドキュメントもローカライズされます。

   レコードのドキュメントの設定と構成について詳しくは、以下を参照してください。

[レコードのドキュメントのテンプレート設定](/help/forms/using/generate-document-of-record-for-non-xfa-based-adaptive-forms.md#p-document-of-record-template-configuration-p)

[レコードのドキュメントの設定](/help/forms/using/generate-document-of-record-for-non-xfa-based-adaptive-forms.md#p-document-of-record-settings-p)

1. [レコードのドキュメントのブランディング情報をカスタマイズ](/help/forms/using/generate-document-of-record-for-non-xfa-based-adaptive-forms.md)し、ブラウザーのロケールを、機械語を使用してアダプティブフォームをローカライズしたのと同じ言語に設定します。ブラウザーのロケールは、レコードのドキュメントにあるブランディング情報のローカライズに役立ちます。
1. ローカライズされたレコードのドキュメントを表示するには、「プレビューを生成」をタップします。レコードのドキュメントPDFが生成され、ブラウザーの新しいタブで開きます。

## 人による翻訳を使用したアダプティブフォームおよびレコードのドキュメントのローカライズ {#localizing-an-adaptive-form-and-its-document-of-record-using-human-translation}

人による翻訳を使用すると、コンテンツは翻訳プロバイダーに送信され専門の翻訳者によって翻訳が行われます。完了すると、翻訳コンテンツが返されて、AEM に読み込まれます。翻訳プロバイダーが AEM と統合されると、AEM と翻訳プロバイダーとの間でコンテンツが自動的に送信されます。

翻訳の際には、専門の翻訳者各自の間で XLIFF 形式のファイルが含まれている辞書が共有されます。この辞書には、各ロケールに対して個別の XLIFF ファイルが含まれます。各 XLIFF には、エンドユーザーに表示されるテキストと、対応するローカライズ済みのテキストのプレースホルダ―が含まれます。

人による翻訳を使用してフォームとレコードのドキュメントをローカライズするには、次の手順を実行します。

1. [AEM を翻訳プロバイダーサービスに接続](/help/sites-administering/tc-tic.md)して、[翻訳統合フレームワーク設定を作成](/help/sites-administering/tc-tic.md)します。

1. 翻訳サービスとフレームワークの設定に[言語マスターのページを関連付け](/help/sites-administering/tc-tic.md)ます。

1. 翻訳する[コンテンツのタイプを特定](/help/sites-administering/tc-rules.md)します。

1. [翻訳するコンテンツを準備](/help/sites-administering/tc-prep.md)します。そのためには、言語マスターをオーサリングして、言語コピーのルートページを作成します。

1. [翻訳プロジェクトを作成](/help/sites-administering/tc-manage.md)して、翻訳するコンテンツを収集し、翻訳プロセスを準備します。

1. 翻訳プロジェクトを使用して、[コンテンツの翻訳プロセスを管理](/help/sites-administering/tc-manage.md)します。

>[!NOTE]
>
>* アダプティブフォームのコンポーネントは、右から左 (RTL) 言語をサポートしていません。 （例：ヘブライ語）。
>

