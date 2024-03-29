---
title: メールマーケティング
seo-title: E-mail Marketing
description: 電子メールマーケティング（ニュースレターなど）は、コンテンツをリードにプッシュする際に使用する、あらゆるマーケティングキャンペーンの重要な要素です。 AEMでは、既存のAEMコンテンツからニュースレターを作成したり、ニュースレター専用の新しいコンテンツを追加したりできます。
seo-description: E-mail marketing (for example, newsletters) are an important part of any marketing campaign as you use them to push content to your leads. In AEM, you can create newsletters from existing AEM content as well as add new content, specific to the newsletters.
uuid: 798e06cd-64dd-4a8d-8a7a-9a7ba80045f6
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.4/SITES
topic-tags: personalization
content-type: reference
discoiquuid: eb72f934-4b0f-4a71-b2a2-3ddf78db8c3c
exl-id: 5e97f7bd-d668-423d-9f65-7dcc8fb1943a
source-git-commit: c5b816d74c6f02f85476d16868844f39b4c47996
workflow-type: tm+mt
source-wordcount: '1762'
ht-degree: 22%

---

# メールマーケティング {#e-mail-marketing}

>[!CAUTION]
>
>AEM 6.4 の拡張サポートは終了し、このドキュメントは更新されなくなりました。 詳細は、 [技術サポート期間](https://helpx.adobe.com/jp/support/programs/eol-matrix.html). サポートされているバージョンを見つける [ここ](https://experienceleague.adobe.com/docs/?lang=ja).

>[!NOTE]
>
>Adobeは、AEM SMTP サービスから送信されるオープン/バウンス済みの E メールをさらに強化する予定はありません。\
>[Adobe Campaign や、Adobe Campaign と AEM の統合環境を活用](/help/sites-administering/campaign.md)することをお勧めします。

電子メールマーケティング（ニュースレターなど）は、コンテンツをリードにプッシュする際に使用する、あらゆるマーケティングキャンペーンの重要な要素です。 AEMでは、既存のAEMコンテンツからニュースレターを作成したり、ニュースレター専用の新しいコンテンツを追加したりできます。

作成後は、（ワークフローを使用して）即座に、またはスケジュールされた別の時間に、特定のユーザーグループにニュースレターを送信することができます。 また、ユーザーは選択した形式でニュースレターを購読することができます。

また、AEMでは、トピックの管理、ニュースレターのアーカイブ、ニュースレターの統計の表示など、ニュースレターの機能を管理できます。

>[!NOTE]
>
>「Geometrixx」では、ニュースレターテンプレートによって E メールエディターが自動的に開きます。 E メールエディターは、E メールを送信する他のテンプレート（招待など）で使用できます。 ページの継承元が次の場所にある場合は、電子メールエディターが表示されます。 **mcm/components/newsletter/page**.

このドキュメントでは、AEMでのニュースレターの作成の基本について説明します。 電子メールマーケティングの使い方の詳細については、次のドキュメントを参照してください。

* [効果的なニュースレターのランディングページの作成 ](/help/sites-classic-ui-authoring/classic-personalization-campaigns-email-landingpage.md)
* [購読の管理 ](/help/sites-classic-ui-authoring/classic-personalization-campaigns-email-subscriptions.md)
* [メールサービスプロバイダーへのメールの公開](/help/sites-classic-ui-authoring/classic-personalization-campaigns-email-newsletters.md)
* [バウンスメールの追跡](/help/sites-classic-ui-authoring/classic-personalization-campaigns-email-tracking-bounces.md)

>[!NOTE]
>
>E メールプロバイダーを更新し、フライトテストを実行するか、ニュースレターを送信する場合、ニュースレターが最初にパブリッシュインスタンスにパブリッシュされないか、パブリッシュインスタンスが使用できない場合、これらの操作は失敗します。 ニュースレターを必ず公開し、発行インスタンスが起動して実行されていることを確認してください。

## ニュースレターエクスペリエンスの作成 {#creating-a-newsletter-experience}

>[!NOTE]
>
>電子メール通知は、osgi 設定を使用して設定する必要があります。 詳しくは、 [電子メール通知の設定](/help/sites-administering/notification.md)

1. 左側のウィンドウで新しいキャンペーンを選択するか、右側のウィンドウで新しいキャンペーンをダブルクリックします。

1. 次のアイコンを使用して、リスト表示を選択します。

   ![](do-not-localize/mcm_icon_listview-1.png)

1. クリック **新規…**

   次の項目を指定できます。 **タイトル**, **名前** 作成するエクスペリエンスのタイプ。この例では、ニュースレターです。

   ![mcm_createnewsletter](assets/mcm_createnewsletter.png)

1. 「**作成**」をクリックします。

1. 新しいダイアログが直ちに開きます。 ここで、ニュースレターのプロパティを入力できます。

   「**デフォルトの受信者リスト**」は、ニュースレターのタッチポイントを構成するので、必須のフィールドです（リストについて詳しくは、[リストの使用](/help/sites-classic-ui-authoring/classic-personalization-campaigns.md#workingwithlists)を参照してください）。

   ![mcm_newnewnewsletterdialog](assets/mcm_newnewsletterdialog.png)

   * **送信元の名前**

      ニュースレターの送信者として表示させる名前です。

   * **送信元のアドレス**

      ニュースレターの送信者として表示させるメールアドレス。

   * **件名**

      ニュースレターの件名です。

   * **返信先**

      送信されたニュースレターへの返信先として使用されるメールアドレスです。

   * **説明**

      ニュースレターの説明。

   * **オンタイム**

      ニュースレターを送信するオンタイム。

   * **デフォルトの受信者リスト**

      ニュースレターを受け取るデフォルトのリストです。
   これらは、後から **プロパティ…** ダイアログ。

1. 「**OK**」をクリックして保存します。

## ニュースレターへのコンテンツの追加 {#adding-content-to-newsletters}

動的コンテンツを含むコンテンツを、AEMコンポーネントと同様にニュースレターに追加できます。 Geometrixxでは、ニュースレターテンプレートには、ニュースレター内のコンテンツの追加と変更に使用できる特定のコンポーネントが含まれています。

1. MCM で、 **キャンペーン** タブをタブに移動し、コンテンツの追加または編集を行うニュースレターをダブルクリックします。 ニュースレターが開きます。

1. コンポーネントが表示されない場合は、デザインビューに移動し、編集を開始する前に必要なコンポーネント（ニュースレターコンポーネントなど）を有効にします。
1. 必要に応じて、新しいテキスト、画像、またはその他のコンポーネントを入力します。 Geometrixxの例では、次の 4 つのコンポーネントを使用できます。「テキスト」、「画像」、「見出し」、「2 列」。 設定に応じて、ニュースレターに含まれるコンポーネントの数が異なる場合があります。

   >[!NOTE]
   >
   >変数を使用して、ニュースレターをパーソナライズします。 Geometrixxニュースレターでは、変数をテキストコンポーネントで使用できます。 変数の値は、ユーザープロファイルの情報から継承されます。

   ![mcm_newsletter_content](assets/mcm_newsletter_content.png)

1. 変数を挿入するには、リストから変数を選択し、 **挿入**. 変数は、プロファイルから入力されます。

## ニュースレターのパーソナライズ {#personalizing-newsletters}

ニュースレターをパーソナライズするには、Geometrixx内のニュースレターのテキストコンポーネントに事前定義済みの変数を挿入します。 変数の値は、ユーザープロファイルの情報から継承されます。

また、ClientContext を使用してプロファイルを読み込むことで、ニュースレターがパーソナライズされる仕組みをシミュレートすることもできます。

ニュースレターをパーソナライズして外観をシミュレートするには：

1. MCM で、設定をカスタマイズするニュースレターを開きます。

1. パーソナライズするテキストコンポーネントを開きます。

1. 変数を表示する場所にカーソルを置き、ドロップダウンリストから変数を選択して、 **挿入**. 必要な数の変数に対してこの操作を行い、「 **OK**.

   ![mcm_newsletter_variables](assets/mcm_newsletter_variables.png)

1. 送信時に変数がどのように表示されるかをシミュレートするには、Ctrl + Alt + c キーを押して ClientContext を開き、「 」を選択します。 **読み込み**. プロファイルを読み込むユーザーをリストから選択し、「 」をクリックします。 **OK**.

   読み込んだプロファイルの情報によって変数が設定されます。

   ![mc_newsletter_testvariables](assets/mc_newsletter_testvariables.png)

## 様々なメールクライアントでのニュースレターのテスト {#testing-newsletters-in-different-e-mail-clients}

>[!NOTE]
>
>ニュースレターを送信する前に、`http://localhost:4502/system/console/configMgr` で Day CQ Link Externalizer の OSGi 設定を確認してください。
>
>デフォルトでは、このパラメーターの値は `localhost:4502` です。稼動しているインスタンスのポートが変更されている場合は操作を完了できません。

共通のメールクライアントを切り替えて、ニュースレターがリードにどのように表示されるかを確認します。デフォルトでは、選択した電子メールクライアントがない状態でニュースレターが開きます。

現在、次の電子メールクライアントでニュースレターを表示できます。

* Yahoo メール
* Gmail
* Hotmail
* サンダーバード
* Microsoft Outlook 2007
* Apple Mail

クライアントを切り替えるには、対応するアイコンをクリックして、その電子メールクライアントでニュースレターを表示します。

1. MCM で、設定をカスタマイズするニュースレターを開きます。

1. 上部のバーの電子メールクライアントをクリックして、そのクライアントでのニュースレターの表示を確認します。

   ![chlimage_1-167](assets/chlimage_1-167.png)

1. 確認するその他のメールクライアントについて、この手順を繰り返します。

   ![chlimage_1-168](assets/chlimage_1-168.png)

## ニュースレター設定のカスタマイズ {#customizing-newsletter-settings}

ニュースレターを送信できるのは許可されたユーザーのみですが、次の項目をカスタマイズする必要があります。

* 件名。ユーザーが E メールを開き、ニュースレターがスパムとしてマークされないようにするために使用します。
* ユーザーが指定したアドレスから電子メールを受け取れるように、送信元アドレス (noreply@geometrixx.comなど )。

ニュースレターの設定をカスタマイズするには：

1. MCM で、設定をカスタマイズするニュースレターを開きます。

   ![mcm_newsletter_open](assets/mcm_newsletter_open.png)

1. ニュースレターの上部にある「**設定**」をクリックします。

   ![mcm_newsletter_settings](assets/mcm_newsletter_settings.png)

   1. 次を入力します。 **送信者** 電子メールアドレス
   1. を変更します。 **件名** 電子メールの（必要に応じて）。
   1. を選択します。 **デフォルトの受信者リスト** 」をドロップダウンリストから選択します。
   1. 「**OK**」をクリックします。

   ニュースレターをテストまたは送信すると、受信者は指定された電子メールアドレスと件名を含む電子メールを受信します。

## ニュースレターのフライトテスト {#flight-testing-newsletters}

フライトテストは必須ではありませんが、ニュースレターを送信する前に、必要に応じて表示されるかどうかをテストする必要があります。

フライトテストでは、次の操作を実行できます。

* でニュースレターを確認します。 [対象となるすべてのクライアント](#testing-newsletters-in-different-e-mail-clients).
* メールサーバーが正しく設定されていることを検証します。
* E メールがスパムとしてフラグ付けされているかどうかを判断します。 （受信者のリストに自分を含めてください）。

>[!NOTE]
>
>E メールプロバイダーを更新し、フライトテストを実行するか、ニュースレターを送信する場合、ニュースレターが最初にパブリッシュインスタンスにパブリッシュされないか、パブリッシュインスタンスが使用できない場合、これらの操作は失敗します。 ニュースレターを必ず公開し、発行インスタンスが起動して実行されていることを確認してください。

ニュースレターをフライトするには：

1. MCM で、テストして送信するニュースレターを開きます。

1. ニュースレターの上部で、 **テスト** 送信前にテストする場合。

   ![mcm_newsletter_testsettings](assets/mcm_newsletter_testsettings.png)

1. ニュースレターを送信するテストメールアドレスを入力し、 **送信**. プロファイルを変更する場合は、ClientContext に別のプロファイルを読み込みます。 これを行うには、Ctrl + Alt + c キーを押し、「読み込み」を選択してプロファイルを読み込みます。

## ニュースレターの送信 {#sending-newsletters}

ニュースレターまたはリストからニュースレターを送信できます。 両方の手順について説明します。

>[!NOTE]
>
>ニュースレターを送信する前に、`http://localhost:4502/system/console/configMgr` で Day CQ Link Externalizer の OSGi 設定を確認してください。
>
>デフォルトでは、このパラメーターの値は `localhost:4502` です。稼動しているインスタンスのポートが変更されている場合は操作を完了できません。

>[!NOTE]
>
>E メールプロバイダーを更新し、フライトテストを実行するか、ニュースレターを送信する場合、ニュースレターが最初にパブリッシュインスタンスにパブリッシュされないか、パブリッシュインスタンスが使用できない場合、これらの操作は失敗します。 ニュースレターを必ず公開し、発行インスタンスが起動して実行されていることを確認してください。

### キャンペーンからのニュースレターの送信 {#sending-newsletters-from-a-campaign}

キャンペーン内からニュースレターを送信するには：

1. MCM で、送信するニュースレターを開きます。

   >[!NOTE]
   >
   >送信する前に、ニュースレターの件名と発信元のメールアドレスが、[設定のカスタマイズ](#customizing-newsletter-settings)を使用してカスタマイズされていることを確認します。
   >
   >送信する前に、ニュースレターの[フライトテスト](#flight-testing-newsletters)を行うことをお勧めします。

1. ニュースレターの上部で、 **送信**. ニュースレターウィザードが開きます。

1. 受信者のリストで、ニュースレターを受信するリストを選択し、 **次へ**.

   ![mcm_newslettersend](assets/mcm_newslettersend.png)

1. 設定が完了しました。 クリック **送信** 実際にニュースレターを送信する場合。

   ![mcm_newslettersendconfirm](assets/mcm_newslettersendconfirm.png)

   >[!NOTE]
   >
   >自分が受信者の 1 人であることを確認して、ニュースレターが受信されたことを確認します。

### リストからのニュースレターの送信 {#sending-newsletters-from-a-list}

リストからニュースレターを送信するには：

1. MCM で、 **リスト** をクリックします。

   >[!NOTE]
   >
   >送信する前に、ニュースレターの件名と発信元のメールアドレスが、[設定のカスタマイズ](#customizing-newsletter-settings)を使用してカスタマイズされていることを確認します。リストから送信する場合、ニュースレターはテストできません。ニュースレターから送信する場合は、[フライトテスト](#flight-testing-newsletters)を実行できます。

1. ニュースレターの送信先であるリードリストの横にあるチェックボックスをオンにします。

1. **ツール**&#x200B;メニューの「**ニュースレターを送信**」を選択します。**ニュースレターを送信**&#x200B;ウィンドウが開きます。

   ![mcm_newslettersendfromlist](assets/mcm_newslettersendfromlist.png)

1. 「**ニュースレター**」フィールドで、送信するニュースレターを選択し、「**次へ**」をクリックします。

   ![mcm_newslettersenddialog](assets/mcm_newslettersenddialog.png)

1. 設定が完了しました。 クリック **送信** 選択したニュースレターを指定したリードのリストに送信します。

   ![mcm_newslettersenddialog_confirmation](assets/mcm_newslettersenddialog_confirmation.png)

   ニュースレターは選択した受信者に送信されます。

## ニュースレターの購読 {#subscribing-to-a-newsletter}

この節では、ニュースレターを購読する方法について説明します。

### ニュースレターの購読 {#subscribing-to-a-newsletter-1}

( 例としてGeometrixxWeb サイトを使用して ) ニュースレターを購読するには：

1. クリック **Web サイト** をクリックし、Geometrixx **ツールバー** そしてそれを開きます。

   ![chlimage_1-169](assets/chlimage_1-169.png)

1. Geometrixxニュースレター **新規登録** フィールドに電子メールアドレスを入力し、 **新規登録**. これで、ニュースレターを購読しました。
