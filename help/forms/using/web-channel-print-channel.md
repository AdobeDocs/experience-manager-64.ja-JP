---
title: 印刷チャネルと Web チャネル
seo-title: Print channel and web channel
description: 印刷チャネルテンプレートの読み込み、Web チャネルテンプレートの作成と有効化
seo-description: Importing print channel templates and creating and enabling web channel templates
uuid: 19e6ffab-00d2-4084-9ee7-9643b11eb6c6
topic-tags: interactive-communications
products: SG_EXPERIENCEMANAGER/6.4/FORMS
discoiquuid: 71bba66a-3cac-445b-9941-aa4bcf9b2160
feature: Interactive Communication
exl-id: cb7a8e96-4440-47ec-b506-275d5acc774e
source-git-commit: c5b816d74c6f02f85476d16868844f39b4c47996
workflow-type: tm+mt
source-wordcount: '734'
ht-degree: 50%

---

# 印刷チャネルと Web チャネル {#print-channel-and-web-channel}

>[!CAUTION]
>
>AEM 6.4 の拡張サポートは終了し、このドキュメントは更新されなくなりました。 詳細は、 [技術サポート期間](https://helpx.adobe.com/jp/support/programs/eol-matrix.html). サポートされているバージョンを見つける [ここ](https://experienceleague.adobe.com/docs/?lang=ja).

印刷チャネルテンプレートの読み込み、Web チャネルテンプレートの作成と有効化

インタラクティブ通信は、次の 2 つのチャネルを通じて配信できます。印刷と web。 印刷チャネルは、保険料の支払いを促す印刷済みレターなどのPDFや紙の通信を作成するために使用され、Web チャネルは、Web サイト上のクレジットカード明細などのオンラインエクスペリエンスを配信するために使用されます。

インタラクティブ通信の作成者は、ドキュメントフラグメントや画像などのアセットを再利用して、印刷バージョンと web バージョンの両方でインタラクティブ通信を作成できます。

[インタラクティブ通信を作成](/help/forms/using/create-interactive-communication.md)する場合の前提条件として、印刷チャネルまたは web チャネル（またはその両方）のテンプレートがサーバー上に存在している必要があります。テンプレートの作成者は、AEM で web チャネルのテンプレートを作成できますが、印刷チャネルテンプレート（XDP）は Adobe Forms Designer で作成して、サーバーにアップロードします。

## 印刷チャネル {#printchannel}

印刷チャネルのインタラクティブ通信では、XFA フォームのテンプレートである XDP を使用します。XDP は Adobe Forms Designer でデザインします。印刷チャネルのテンプレートを作成する方法については、[レイアウトデザイン](/help/forms/using/layout-design-details.md)を参照してください。インタラクティブ通信内で印刷チャネルのテンプレートを使用するには、そのテンプレートを AEM Forms サーバーにアップロードする必要があります。

### インタラクティブ通信の印刷チャネルテンプレートのアップロード {#upload-interactive-communication-print-channel-template}

テンプレートをアップロードするには、forms-user グループのメンバーである必要があります。 次の手順を使用して、印刷チャネルテンプレート (XDP) をAEM Formsにアップロードします。

1. **[!UICONTROL Forms]**／**[!UICONTROL Forms とドキュメント]**&#x200B;を選択します。

1. **[!UICONTROL 作成]**／**[!UICONTROL ファイルのアップロード]**&#x200B;をタップします。

   目的の印刷チャネルテンプレート（XDP）に移動して選択し、「**[!UICONTROL 開く]**」をタップします。

## Web チャネル {#web-channel}

テンプレート作成者と管理者は、Web テンプレートの作成、編集、有効化をおこなうことができます。 他のユーザーが Web テンプレートを作成できるようにするには、権限を付与する必要があります。 詳しくは、[ユーザー、グループ、アクセス権限の管理](/help/sites-administering/user-group-ac-admin.md)を参照してください。

### Web チャネルテンプレートのオーサリング {#authoring-web-channel-template}

Web チャネルテンプレートを作成するには、まずテンプレートフォルダーを作成する必要があります。 テンプレートフォルダー内に web チャネルテンプレートを作成したら、そのテンプレートを有効にする必要があります。これにより、Forms ユーザーがそのテンプレートを使用して、インタラクティブ通信の web チャネルを作成できるようになります。

Web チャネルテンプレートを作成するには、以下の手順を実行します。

1. インタラクティブ通信の web チャネルテンプレートを保存するためのテンプレートフォルダーを作成します（まだ作成されていない場合）。詳しくは、[編集可能なページテンプレート](/help/sites-developing/page-templates-editable.md)の「テンプレートフォルダー」を参照してください。

   1. タップ **[!UICONTROL ツール]** ![tools-1](assets/tools-1.png) > **[!UICONTROL 設定ブラウザー]**.
      * 詳しくは、[設定ブラウザーのドキュメント](/help/sites-administering/configurations.md)を参照してください。
   1. 設定ブラウザーページで、「**[!UICONTROL 作成]**」をタップします。
   1. 設定作成ダイアログでフォルダーのタイトルを入力し、「**[!UICONTROL 編集可能テンプレート]**」を選択して「**[!UICONTROL 作成]**」をタップします。

      フォルダーが作成され、設定ブラウザーのページに表示されます。

1. 目的のテンプレートフォルダーに移動して、web テンプレートを作成します。

   1. 次を選択して、適切なテンプレートフォルダーに移動します。 **[!UICONTROL ツール]** > **[!UICONTROL テンプレート/フォルダー]**.
   1. 「**[!UICONTROL 作成]**」をタップします。
   1. 「**[!UICONTROL インタラクティブ通信 - Web チャネル]**」を選択して「**[!UICONTROL 次へ]**」をタップします。
   1. テンプレートのタイトルと説明を入力して「**[!UICONTROL 作成]**」をタップします。

      テンプレートが作成されダイアログが表示されます。

   1. タップ **[!UICONTROL 開く]** をクリックして、作成したテンプレートをテンプレートエディターで開きます。

      テンプレートエディタが表示されます。

      ![webchanneltemplate](assets/webchanneltemplate.png)

      テンプレートを作成または編集する際には、テンプレート作成者が定義できる様々な要素があります。 テンプレートの作成や編集は、ページのオーサリングと似ています。 詳しくは、[ページテンプレートの作成](/help/sites-authoring/templates.md)の「テンプレートの編集 - テンプレート作成者」を参照してください。

1. このテンプレートを使用してインタラクティブ通信を作成できるようにするには、このテンプレートを有効にします。

   1. タップ **[!UICONTROL ツール]** ![tools-1](assets/tools-1.png) > **[!UICONTROL テンプレート]**.
   1. 目的のテンプレートに移動して選択し、「**[!UICONTROL 有効]**」をタップしてから、アラートメッセージ内の「**[!UICONTROL 有効]**」をタップします。

      テンプレートが有効になり、そのステータスが「有効」と表示されます。 次に、新しく作成した Web チャネルテンプレートを使用するインタラクティブ通信の作成に進むことができます。

### Web チャネルのマスターとしてチャネルを印刷 {#print-channel-as-master-for-web-channel}

インタラクティブ通信の作成時に、作成者はこのオプションを選択して、印刷チャネルと同期して Web チャネルを作成できます。 印刷チャネルを Web チャネルのマスターとして使用すると、Web チャネルのコンテンツ、継承、データ連結が印刷チャネルから派生し、印刷チャネルで行われた変更が Web チャネルに反映される可能性があります。 ただし、インタラクティブ通信の作成者は、必要に応じて、Web チャネル内の特定のコンポーネントの継承を解除できます。

![printweb_2-2](assets/printweb_2-2.png)
