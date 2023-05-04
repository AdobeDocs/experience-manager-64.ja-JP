---
title: AEM Forms がフォームデータを JEE 上の AEM Forms プロセスに送信するための設定
seo-title: Configuring AEM Forms to submit form data to an AEM Forms on JEE process
description: AEM Formsを使用すると、フォームデータを処理するために、アダプティブフォームを JEE 上のAEM Formsプロセスと統合することができます。
seo-description: AEM Forms allows you to integrate adaptive forms with AEM Forms on JEE processes for processing form data.
uuid: ee7ea442-d604-4520-9af5-ad40ec4927a1
content-type: reference
products: SG_EXPERIENCEMANAGER/6.4/FORMS
topic-tags: Configuration
discoiquuid: 03619a67-d1ea-4b80-b1a6-0c65a9e9212f
role: Admin
exl-id: 260e405e-f59c-4aea-b83f-53ee103df94e
source-git-commit: c5b816d74c6f02f85476d16868844f39b4c47996
workflow-type: tm+mt
source-wordcount: '362'
ht-degree: 54%

---

# AEM Forms がフォームデータを JEE 上の AEM Forms プロセスに送信するための設定 {#configuring-aem-forms-to-submit-form-data-to-an-aem-forms-on-jee-process}

>[!CAUTION]
>
>AEM 6.4 の拡張サポートは終了し、このドキュメントは更新されなくなりました。 詳細は、 [技術サポート期間](https://helpx.adobe.com/jp/support/programs/eol-matrix.html). サポートされているバージョンを見つける [ここ](https://experienceleague.adobe.com/docs/?lang=ja).

アダプティブフォームは、さらに処理するためのデータを JEE 上のAEM Formsプロセスに送信する機能をサポートしています。 JEE 上のAEM Formsプロセスのトリガーを、送信済みフォームから使用可能なデータと共に実行できます。 次の手順を実行して、AEM Forms インスタンスがアダプティブフォームを AEM Forms on JEE プロセスに送信できるようにします。

## AEM Formsサーバーの設定 {#configure-your-aem-forms-server}

次の手順を実行して、AEM forms サーバーが JEE 上のAEM Formsサーバーにデータを送信できるようにします。

1. AEM web コンソールの設定ページ（https://[*host*]:[*port*]/system/console/configMgr）に移動します。

1. **Adobe LiveCycle Client SDK Configuration** コンポーネントを見つけてクリックします。
1. JEE 上のAEM Formsサーバーの設定サーバー URL、ユーザー名、パスワードをクリックして編集します。
1. 設定を確認し、「**保存**」をクリックします。

![Adobe LiveCycle Client SDK 設定](assets/clientsdkconfiguration.jpg)

## LiveCycle プロセスのフィールドへのデータのマッピング {#map-data-with-process-fields}

AEM Formsを設定したら、送信済みフォームのデータ XML と添付ファイルを、JEE 上のAEM Formsプロセスのフィールドにマッピングします。 次の手順を実行します。

1. AEM Web 設定コンソールで、「 」をクリックして **ガイドLiveCycleプロセスロケーターと呼び出し元** 設定。
1. 以下のパラメーターを指定します。

   * **データ xml パラメーターの名前**（必須）：送信されたデータを処理する必要がある AEM Forms on JEE プロセスの XML プロパティファイルを指定します。デフォルト値は **dataxml** です。
   * **Name of the file attachments parameter**（オプション）：JEE 上の AEM Forms プロセスで処理する必要のあるドキュメントオブジェクトのリストを指定します。デフォルト値は **fileAttachmentsList** です。

1. 設定を確認し、「**保存**」をクリックします。

![Guide LiveCycle Process Locator and Invoker](assets/test3.jpg)

設定が完了すると、「フォームワークフローへの送信」送信アクションには、指定した XML データパラメーターを含む JEE 上の AEM Forms サーバープロセスが一覧表示されます。
