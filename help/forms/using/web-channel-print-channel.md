---
title: 印刷チャネルと Web チャネル
seo-title: Print channel and web channel
description: 印刷チャネルテンプレートを読み込み、Web チャネルテンプレートを作成して有効にする
seo-description: Importing print channel templates and creating and enabling web channel templates
uuid: 19e6ffab-00d2-4084-9ee7-9643b11eb6c6
topic-tags: interactive-communications
products: SG_EXPERIENCEMANAGER/6.4/FORMS
discoiquuid: 71bba66a-3cac-445b-9941-aa4bcf9b2160
feature: Interactive Communication
exl-id: cb7a8e96-4440-47ec-b506-275d5acc774e
source-git-commit: bd94d3949f0117aa3e1c9f0e84f7293a5d6b03b4
workflow-type: tm+mt
source-wordcount: '698'
ht-degree: 96%

---

# 印刷チャネルと Web チャネル {#print-channel-and-web-channel}

印刷チャネルテンプレートを読み込み、Web チャネルテンプレートを作成して有効にする

インタラクティブ通信は、印刷チャネルと Web チャネルという 2 つのチャネルを使用して配信することができます。印刷チャネルは、PDF や紙ベースの通信手段（保険料の支払いを通知する印刷書類など）を作成する場合に使用され、Web チャネルは、オンライン情報（Web サイト上で表示されるクレジットカードの取引明細など）を配信する場合に使用されます。

インタラクティブ通信の作成者は、ドキュメントフラグメントや画像などのアセットを再利用して、印刷バージョンと web バージョンの両方でインタラクティブ通信を作成できます。

[インタラクティブ通信を作成](/help/forms/using/create-interactive-communication.md)する場合の前提条件として、印刷チャネルまたは web チャネル（またはその両方）のテンプレートがサーバー上に存在している必要があります。テンプレートの作成者は、AEM で web チャネルのテンプレートを作成できますが、印刷チャネルテンプレート（XDP）は Adobe Forms Designer で作成して、サーバーにアップロードします。

## 印刷チャネル {#printchannel}

印刷チャネルのインタラクティブ通信では、XFA フォームのテンプレートである XDP を使用します。XDP は Adobe Forms Designer でデザインします。印刷チャネルのテンプレートを作成する方法については、[レイアウトデザイン](/help/forms/using/layout-design-details.md)を参照してください。インタラクティブ通信内で印刷チャネルのテンプレートを使用するには、そのテンプレートを AEM Forms サーバーにアップロードする必要があります。

### インタラクティブ通信の印刷チャネルテンプレートのアップロード {#upload-interactive-communication-print-channel-template}

テンプレートをアップロードするには、forms-user グループのメンバーになっている必要があります。印刷チャネルテンプレート（XDP）を AEM Forms にアップロードするには、以下の手順を実行します。

1. **[!UICONTROL Forms]**／**[!UICONTROL Forms とドキュメント]**&#x200B;を選択します。

1. **[!UICONTROL 作成]**／**[!UICONTROL ファイルのアップロード]**&#x200B;をタップします。

   目的の印刷チャネルテンプレート（XDP）に移動して選択し、「**[!UICONTROL 開く]**」をタップします。

## Web チャネル {#web-channel}

テンプレートの作成者と管理者は、テンプレートの作成、編集、有効化を行うことができます。それ以外のユーザーが Web テンプレートを作成できるようにするには、そのユーザーに対して権限を設定する必要があります。詳しくは、[ユーザー、グループ、アクセス権限の管理](/help/sites-administering/user-group-ac-admin.md)を参照してください。

### Web チャネルテンプレートの作成 {#authoring-web-channel-template}

Web チャネルテンプレートを作成するには、最初にテンプレートフォルダーを作成する必要があります。テンプレートフォルダー内に web チャネルテンプレートを作成したら、そのテンプレートを有効にする必要があります。これにより、Forms ユーザーがそのテンプレートを使用して、インタラクティブ通信の web チャネルを作成できるようになります。

Web チャネルテンプレートを作成するには、以下の手順を実行します。

1. インタラクティブ通信の web チャネルテンプレートを保存するためのテンプレートフォルダーを作成します（まだ作成されていない場合）。詳しくは、[編集可能なページテンプレート](/help/sites-developing/page-templates-editable.md)の「テンプレートフォルダー」を参照してください。

   1. タップ **[!UICONTROL ツール]** ![tools-1](assets/tools-1.png) > **[!UICONTROL 設定ブラウザー]**.
      * 詳しくは、[](/help/sites-administering/configurations.md)設定ブラウザーのドキュメントを参照してください。
   1. 設定ブラウザーページで、「**[!UICONTROL 作成]**」をタップします。
   1. 設定作成ダイアログでフォルダーのタイトルを入力し、「**[!UICONTROL 編集可能テンプレート]**」を選択して「**[!UICONTROL 作成]**」をタップします。

      フォルダーが作成され、設定ブラウザーのページに表示されます。

1. 目的のテンプレートフォルダーに移動して、web テンプレートを作成します。

   1. 次を選択して、適切なテンプレートフォルダーに移動します。 **[!UICONTROL ツール]** > **[!UICONTROL テンプレート/フォルダー]**.
   1. 「**[!UICONTROL 作成]**」をタップします。
   1. 「**[!UICONTROL インタラクティブ通信 - Web チャネル]**」を選択して「**[!UICONTROL 次へ]**」をタップします。
   1. テンプレートのタイトルと説明を入力して「**[!UICONTROL 作成]**」をタップします。

      テンプレートが作成されダイアログが表示されます。

   1. 「**[!UICONTROL 開く]**」をタップして、作成したテンプレートをテンプレートエディターで開きます。

      テンプレートエディターが表示されます。

      ![webchanneltemplate](assets/webchanneltemplate.png)

      テンプレートの作成者は、テンプレートの作成や編集を行う際に、様々な要素を定義することができます。テンプレートの作成と編集は、ページの作成に似ています。詳しくは、[ページテンプレートの作成](/help/sites-authoring/templates.md)の「テンプレートの編集 - テンプレート作成者」を参照してください。

1. このテンプレートを使用してインタラクティブ通信を作成できるようにするには、このテンプレートを有効にします。

   1. タップ **[!UICONTROL ツール]** ![tools-1](assets/tools-1.png) > **[!UICONTROL テンプレート]**.
   1. 目的のテンプレートに移動して選択し、「**[!UICONTROL 有効]**」をタップしてから、アラートメッセージ内の「**[!UICONTROL 有効]**」をタップします。

      これでテンプレートが有効になり、テンプレートのステータスとして「有効」が表示されます。新しく作成した Web チャネルテンプレートを使用して、インタラクティブ通信を作成することができます。

### 「印刷チャネルを Web チャネルのマスターとして使用する」オプション {#print-channel-as-master-for-web-channel}

インタラクティブ通信を作成する際に、「印刷チャネルを Web チャネルのマスターとして使用する」オプションを選択すると、印刷チャネルに同期された Web チャネルを作成することができます。印刷チャネルを Web チャネルのマスターとして使用すると、Web チャネルに連結されたコンテンツ、継承設定、データが印刷チャネルから取得され、印刷チャネルに対する変更内容が Web チャネルに反映されます。ただし、インタラクティブ通信の作成者は、必要に応じて、Web チャネル内の特定のコンポーネントの継承設定を解除することができます。

![printweb_2-2](assets/printweb_2-2.png)
