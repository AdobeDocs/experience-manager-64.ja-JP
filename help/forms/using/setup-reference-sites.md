---
title: AEM Forms リファレンスサイトのセットアップおよび設定
seo-title: AEM Forms リファレンスサイトのセットアップおよび設定
description: AEM Forms のリファレンスサイトでは、AEM Forms を使用して、組織内にエンドツーエンドのワークフローを実装する方法を参照することができます。
seo-description: AEM Forms のリファレンスサイトでは、AEM Forms を使用して、組織内にエンドツーエンドのワークフローを実装する方法を参照することができます。
uuid: 087d58a1-d84e-49ac-a82d-4e7fc708f00f
content-type: reference
products: SG_EXPERIENCEMANAGER/6.4/FORMS
topic-tags: introduction
discoiquuid: 2feb4a9c-57ad-4c6b-a572-0047bc409bbb
translation-type: tm+mt
source-git-commit: 8b5a3e1f6616c3a07da91e4347596961ac4a8e22

---


# AEM Forms リファレンスサイトのセットアップおよび設定 {#set-up-and-configure-aem-forms-reference-sites}

AEM Forms のリファレンスサイトでは、金融サービス業界や各種行政機関が AEM Forms をどのように使用して、複雑なトランザクションを、場所、時間、デバイスを問わないシンプルで魅力的なデジタルサービスに変換しているかについて紹介しています。

We.Finance と We.Gov のリファレンスサイトでは、実生活における使用例が紹介されています。最初の操作から通信やトランザクションの管理に至るまで、既存の顧客や見込み顧客に対して、カスタマイズされたコスト効率の高い方法でサービスを提供しています。

AEM Forms のリファレンスサイトでは、以下に示す AEM Forms の主要な機能を参照することができます。

* 魅力的でレスポンシブなアダプティブフォームとインタラクティブな通信のオーサリング体験をシンプル化。
* Interactive Communicationsを使用すると、デバイスの設定とレイアウトに合わせて、インタラクティブでパーソナライズされたレスポンシブな顧客通信を作成できます。
* データを統合して各種のデータソースに接続し、データをフォームに事前に取り込み、フォームデータモデル経由でフォームを送信。
* ビジネスの各種プロセスとワークフローを自動化するためのフォームワークフロー。
* 高度なユーザーデータ管理および処理機能。
* アダプティブフォームに安全に署名して送信するための Adobe Sign との統合。
* ターゲットを設定したレコメンデーションを提供し、フォームからの ROI を最大化する A/B テストを実行するための Adobe Target との統合。
* フォームとキャンペーンのパフォーマンスを計測し、十分な情報を得た上で意志決定を行うための Adobe Analytics との統合。
* フォーム入力の操作性が向上。

リファレンスサイトには、独自のアセットを作成するためのテンプレートとして使用可能なアセットが用意されています。これらのアセットは、繰り返し使用することができます。

* アダプティブフォームに安全に署名して送信するための Adobe Sign との統合。

* アダプティブフォームに安全に署名して送信するための Adobe Sign との統合。

## リファレンスサイトの設定手順と前提条件 {#prerequisites-and-steps-to-set-up-reference-sites}

リファレンスサイトを設定する前に、次の事項を確認します。

* **AEMの基本**

   AEM quickStart、AEM Formsアドオンパッケージ、リファレンスサイトパッケージ。 See [AEM Forms releases](https://helpx.adobe.com/aem-forms/kb/aem-forms-releases.html) for add-on and reference sites packages details.

* **SMTP サービス** 任意の SMTP サービスを使用することができます。

* **Adobe sign開発者アカウントおよびAdobe Sign APIアプリケーション**

   デジタル署名機能を使用するには、Adobe sign開発者アカウントが必要です。 詳しくは、「[Adobe Sign](https://acrobat.adobe.com/us/en/why-adobe/developer-form.html)」を参照してください。

* AEM Formsと統合するMicrosoft Dynamics 365の実行中のインスタンス。 リファレンスサイトを実行するには、サンプルデータをMicrosoft Dynamicsインスタンスに読み込み、リファレンスサイトで使用される対話型通信に事前入力します。
* Formsアドオンパッケージを含むAEM 6.4の実行中のインスタンス。 詳しくは、「[AEM Forms のインストールと設定](https://helpx.adobe.com/experience-manager/6-3/forms/using/installing-configuring-aem-forms-osgi.html)」を参照してください。

リファレンスサイトのセットアップと構成を行うには、以下の手順を実行します。以下に記載されているとおりの順序で実行することをお勧めします。

<table> 
 <tbody> 
  <tr> 
   <th><strong>ステップ</strong></th> 
   <th><strong>設定</strong></th> 
   <th><strong>メモ</strong></th> 
  </tr> 
  <tr> 
   <td><a href="#installaemforms">AEM Forms のインストールと設定</a></td> 
   <td>オーサーインスタンスとパブリッシュインスタンス</td> 
   <td>AEM Forms のオーサーインスタンスとパブリッシュインスタンスをインストールして設定を行います。</td> 
  </tr> 
  <tr> 
   <td><a href="#ssl">SSL の設定</a></td> 
   <td>オーサーインスタンスとパブリッシュインスタンス<br /> </td> 
   <td>Adobe Sign とのセキュアな通信を行うために、SSL 経由の HTTP を有効にします。</td> 
  </tr> 
  <tr> 
   <td><p><a href="#externalizer">Day CQ Link Externalizer の設定</a></p> </td> 
   <td>オーサーインスタンスとパブリッシュインスタンス<br /> </td> 
   <td><p>リファレンスサイトの使用例では、異なるトランザクションの電子メールを配信しています。この設定は、電子メールでニュースレターを配信する場合に必要になります。この設定により、URL と画像でパブリッシュインスタンスが参照されるようになります。 </p> </td> 
  </tr> 
  <tr> 
   <td><a href="#cqmail">Day CQ 電子メールサービスを設定する</a></td> 
   <td>オーサーインスタンスとパブリッシュインスタンス</td> 
   <td>電子メールによる通信を行う場合は、この設定が必要になります。</td> 
  </tr> 
  <tr> 
   <td><a href="#xss">デフォルトの XSS 設定の上書き</a></td> 
   <td>公開</td> 
   <td>XSSセキュリティでブロックされている$、{、}文字を上書きするために使用します。</td> 
  </tr> 
  <tr> 
   <td><a href="#aemds">AEM DS の設定</a></td> 
   <td>作成者</td> 
   <td>パブリッシュインスタンスでのフォーム送信と、オーサーインスタンスでのプロセスワークフローについて、AEM DS を設定します。</td> 
  </tr> 
  <tr> 
   <td><a href="#refsite">リファレンスサイトパッケージのデプロイメント</a></td> 
   <td>作成者</td> 
   <td>AEM Forms のオーサーインスタンスに、リファレンスサイトパッケージをデプロイします。</td> 
  </tr> 
  <tr> 
   <td><a href="/help/forms/using/setup-reference-sites.md#optional-import-sample-data-into-microsoft-dynamics">サンプルデータを Microsoft Dynamics に読み込む</a></td> 
   <td>オーサーインスタンスとパブリッシュインスタンス</td> 
   <td>クレジットカード申し込み、住宅ローン申し込み、住宅保険申し込みチュートリアル用のサンプルデータのインポート</td> 
  </tr> 
  <tr> 
   <td><a href="/help/forms/using/setup-reference-sites.md#configure-oauth-cloud-service-for-microsoft-dynamics">OAuth クラウドサービスを Microsoft Dynamics 用に設定する</a></td> 
   <td>オーサーインスタンスとパブリッシュインスタンス</td> 
   <td>AEM formsでOAuthクラウドサービスを設定して、AEM FormsとMicrosoft Dynamics間の通信を有効にします。 </td> 
  </tr> 
  <tr> 
   <td><a href="#scheduler">Adobe Sign スケジューラーの設定</a></td> 
   <td>オーサーインスタンスとパブリッシュインスタンス<br /> </td> 
   <td>ステータスを 2 秒間隔で確認するようにスケジューラーの設定を変更します。</td> 
  </tr> 
  <tr> 
   <td><a href="#sign-service">リファレンスサイトの Adobe Sign クラウドサービスの設定</a></td> 
   <td>オーサーインスタンスとパブリッシュインスタンス<br /> </td> 
   <td>リファレンスサイトパッケージに付属している設定を、有効な資格情報で設定し直す必要があります。</td> 
  </tr> 
  <tr> 
   <td><a href="#anonymous">匿名ユーザー用のフォーム共通設定サービスの構成</a></td> 
   <td>公開</td> 
   <td>この設定では、匿名ユーザーに対して、送信、署名、およびレコードの生成のドキュメントを許可します。</td> 
  </tr> 
  <tr> 
   <td><a href="#fdm">フォームデータモデルに対する REST サービス Swagger ファイルの修正</a></td> 
   <td>オーサーインスタンスとパブリッシュインスタンス<br /> </td> 
   <td>現在の環境に合わせてサービスを修正します。</td> 
  </tr> 
 </tbody> 
</table>

## AEM Forms のインストールと設定 {#install-and-configure-aem-forms}

Install and deploy AEM Forms as described in [Installing and configuring AEM Forms on OSGi](/help/forms/using/installing-configuring-aem-forms-osgi.md).

>[!NOTE]
>
>複数のパブリッシュインスタンスが存在する場合や、オーサーインスタンスとパブリッシュインスタンスが異なるマシン上に存在する場合は、複製エージェントと逆複製エージェントを設定してください。

## SSL の設定 {#ssl}

Adobe Sign サーバーとの通信を行うには、SSL を設定する必要があります。For detailed steps, see [Enabling HTTP Over SSL](/help/sites-administering/ssl-by-default.md).

>[!CAUTION]
>
>Do not configure force SSL on `/etc/map` folder.

## Day CQ Link Externalizer の設定 {#externalizer}

In AEM, the **Externalizer** is an OSGI service that allows you to programmatically transform a resource path (e.g. /path/to/my/page) into an external and absolute URL (for example, https://www.mycompany.com/path/to/my/page) by prefixing the path with a pre-configured DNS. 詳しくは、「[URL の外部化](/help/sites-developing/externalizer.md)」を参照してください。

>[!CAUTION]
>
>SSL で自己署名証明書を使用する場合は、HTTPS URL を外部化しないでください。
>
>また、ローカルサーバーの場合は、サーバーのホスト名ではなく localhost を使用してください。

オーサーインスタンスとパブリッシュインスタンスの両方で、以下の手順を実行します。

1. Go to OSGi Configuration at https://&lt;*hostname>*:&lt;*port>*/system/console/configMgr.
1. Find and tap **[!UICONTROL Day CQ Link Externalizer]** configuration.

   設定を編集するための Day CQ Link Externalizer ダイアログが表示されます。

1. Day CQ Link Externalizer ダイアログの「ドメイン」フィールドで、以下の操作を実行します。

   * オーサーインスタンスで、外部システムからアクセス可能な発行 URL を指定します。例えば、ホスト名や発行用の Web サーバーを指定します。
   * パブリッシュインスタンスで、オーサー URL と発行 URL の両方を指定します。

1. オーサーインスタンスとパブリッシュインスタンスの両方で、「ドメイン」フィールドにローカルサーバーの URL が指定されていることを確認します。
1. 「**[!UICONTROL 保存]**」をタップします。すべてのサービスが再開されるまで待ちます。

## Day CQ 電子メールサービスの設定 {#cqmail}

リファレンスサイトの実装では、ユーザーがフォームに入力して送信した場合に電子メールをサンプルユーザーに送信する必要があります。Day CQ 電子メールサービスを設定して SMTP サービスの詳細を指定することにより、顧客に対して電子メールを自動的に送信することができます。詳しくは、「[電子メール通知の設定](/help/sites-administering/notification.md)」を参照してください。

パブリッシュインスタンスで以下の手順を実行して、電子メールサービスを設定します。

1. Go to OSGi Configuration at https://&lt;*hostname>*:&lt;*port>*/system/console/configMgr.
1. Find and tap **[!UICONTROL Day CQ Mail Service]** to open it for configuration.
1. SMTP サーバーのホスト名とポートの値を入力します。
1. 「**[!UICONTROL 保存]**」をタップします。

>[!NOTE]
>
>社内の SMTP サービスを使用することも、Gmail などのパブリックサービスを使用することもできます。SMTP サービスの設定方法については、SMTP サービスのマニュアルを参照してください。

## デフォルトの XSS 設定の上書き {#xss}

We.Finance リファレンスサイトの電子メールテンプレートには、電子メール内で使用するカスタマイズされた各種リンクが用意されています。These links have placeholder as `${placeholder}`. プレースホルダーは、電子メールの送信前に実際の値に置き換えられます。AEM のデフォルトの XSS 保護設定では、HTML コンテンツ内の URL に波括弧（**{ }**）を使用できません。ただし、パブリッシュインスタンスで以下の手順を実行することにより、デフォルトの設定を上書きすることができます。

1. にコピ `/libs/cq/xssprotection/config.xml` ーしま `/apps/cq/xssprotection/config.xml`す。
1. 開く `/apps/cq/xssprotection/config.xml`.
1. In the `common-regexps` section, modify the `onsiteURL` entry as follows and save the file.

   `<regexp name="onsiteURL" value="([\p{L}\p{N}\\\.\#@\$\{\}%\+&;\-_~,\?=/!\*\(\)]*|\#(\w)+)"/>`

>[!NOTE]
>
>Curly braces (**{ }**) are included as accepted characters in the URL in HTML content.

SMTP サーバーを設定したら、Sarah Rose のペルソナを使ってフォームに入力し、下書きとして保存します。下書きとして保存する場合、電子メールを使用してその下書きを受信するオプションがあります。「**電子メールを送信**」ボタンをタップして、アプリケーションのドラフトのリンクが記載された電子メールを受信すれば、電子メールが正しく設定されています。Sarah の資格情報を使用してログインし、下書きを参照できることを確認してください。

## AEM DS の設定 {#aemds}

リファレンスサイトの使用例では、電子メール通信の発行インスタンスでAEM DSサービスの設定が必要です。 発行インスタンスでAEM DS Serviceを設定する詳しい手順については、AEM DS設定の設定を [参照してください](/help/forms/using/configuring-the-processing-server-url-.md)。

AEM Formsリファレンスサイトの場合、AEM DS Settings Serviceで、処理サーバーのURLではなく、パブリッシュサーバーのURLを指定します。

>[!CAUTION]
>
>Do not put `/lc` in the processing server URL if you are configuring it for AEM Forms OSGi.

## リファレンスサイトパッケージのデプロイメント {#refsite}

パッケージ共有を使用して、以下のリファレンスサイトパッケージをインストールします。

* [AEM-FORMS-6.4-FSI-REF-SITE](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq640/fd/AEM-FORMS-6.4-FSI-REF-SITE)
* [AEM-FORMS-6.4-GOV-REF-SITE](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq640/fd/AEM-FORMS-6.4-GOV-REF-SITE)

To learn more about how to use packages and package share, see [How to Work With Packages](/help/sites-administering/package-manager.md).

パッケージをインストールして、オーサーインスタンスとパブリッシュインスタンスを開始したら、ブラウザーで以下の URL にアクセスします。

* `https://[server]:[port]/wegov`
* `https://[server]:[port]/wefinance`

インストールが正常に完了すると、We.Gov と We.Finance のリファレンスサイトのランディングページにアクセスできるようになります。

## (Optional) Import sample data into Microsoft Dynamics {#optional-import-sample-data-into-microsoft-dynamics}

住宅ローン申込書および自動保険申込書リファレンスサイトは、Microsoft Dynamicsのレコードを使用するように構成されています。 リファレンスサイトパッケージは、Microsoft Dynamicsにインポートしてリファレンスサイトを実行できるカスタムエンティティとサンプルレコードをインストールします。 サンプルデータを移行して設定するには、次の手順を実行します。

自動保険申込用にカスタム・エンティティをインポートする手順は、次のとおりです。

1. Download the **WeFinanceAutoInsurance_1_0.zip** solution package from `https://[server]:[port]/content/aemforms-refsite-collaterals/we-finance/auto-insurance/ms-dynamics/WeFinanceAutoInsurance_1_0.zip` on your AEM author instance.
1. Microsoft Dynamicsインスタンスで、設定メニューの「ソリュー **[!UICONTROL ション]** 」に移動し **[!UICONTROL 、「読み込み]** 」をクリ **[!UICONTROL ックします]**。 パッケージを選択して読み込みます。

自動保険申込用にカスタム・エンティティをインポートする手順は、次のとおりです。

1. https:// **author** :[port/content/aemforms-refsite-collaterals/we-finance/home-mortgage/ms-dynamics/AEMFormsFSIRefsite_1_0.zipからAEMFormsFSIRefsite_1_0.zipパッケージをダウンロードし]ます[]。 パッケージを選択して読み込みます。

1. Microsoft Dynamicsインスタンスで、設定メニューの「ソリュー **[!UICONTROL ション]** 」に移動し **[!UICONTROL 、「読み込み]** 」をクリ **[!UICONTROL ックします]**。 パッケージを選択して読み込みます。

顧客および保険証券レコードをインポートする手順は、次のとおりです。

1. Download the **We.Finance Customers.csv, We.Finance Auto Insurance Renewals.csv**, and **home mortgage** data files from the following locations on your AEM author instance:

   * `https://[server]:[port/content/aemforms-refsite-collaterals/we-finance/auto-insurance/ms-dynamics/We.Finance Customers.csv`
   * `https://[server]:[port/content/aemforms-refsite-collaterals/we-finance/auto-insurance/ms-dynamics/We.Finance Auto Insurance Renewals.csv`
   * `https://[server]:[port]/content/aemforms-refsite-collaterals/we-finance/home-mortgage/ms-dynamics/Sarah%20Rose%20Contact.csv`

1. Microsoft Dynamicsインスタンスで、次の操作を行います。

   * Go to **[!UICONTROL Sales > We.Finance Customers]** and click **[!UICONTROL Import]**.
   * Go to **[!UICONTROL Sales > We.Finance Auto Insurance]** and click **[!UICONTROL Import]**.
   * Go to **[!UICONTROL Sales > We.Finance Home Mortgage]**  and click **[!UICONTROL Import]**.

## OAuth クラウドサービスを Microsoft Dynamics 用に設定する {#configure-oauth-cloud-service-for-microsoft-dynamics}

AEM formsでOAuthクラウドサービスを設定して、AEM FormsとMicrosoft Dynamics間の通信を有効にします。 AEM作成者インスタンスと発行インスタンスでOAuthクラウドサービスを設定するには、次の手順を実行します。

1. On AEM author instance, go to **[!UICONTROL Tools > Cloud Services > Data Sources > global]**. 「Dynamics統合 **[!UICONTROL をリファレンス]** 」アイコンをタップし、「プロパティ」を **[!UICONTROL タップしま]**&#x200B;す。
1. Microsoft Azure Active Directory のアカウントに移動します。登録済みアプリケーションの「**[!UICONTROL 応答 URL]**」設定に、コピーしたクラウドサービス設定の URL を追加します。設定を保存します。
1. In the Authentication Settings tab, specify **[!UICONTROL Service Root]**, **[!UICONTROL Client Id]**, **[!UICONTROL Client Secret]**, and **[!UICONTROL Resource URL]** for your Microsoft Dynamics instance. Click **[!UICONTROL Connect to OAuth]** that redirects to the Microsoft Dynamics login page.
1. ログイン情報を入力します。ログインすると、AEM Formsクラウドサービスの設定ページにリダイレクトされます。 「**[!UICONTROL 保存して閉じる]**」をクリックします。クラウドサービス設定が保存されます。
1. Go to **[!UICONTROL Forms > Data Integrations > We.Finance]**. 「自動保険(Dynamics)」を選択し、「編集」をクリックします。 Microsoft Dynamicsエンティティは、「データソース」タブの下に表示されます。 すべてのエンティティがMicrosoft Dynamicsから取得され、データソースタブの下に表示されるまで待ちます。
1. Select the **[!UICONTROL AutoInsuranceRenewal entity]** and click **[!UICONTROL Test Model Object]**. In the input request section, specify the value for customer ID as “900001” and click **[!UICONTROL Test]**. 「出力」セクションには、顧客ID 900001用にMicrosoft Dynamicsから取得したレコードが表示されます。
1. In the input request section, specify the value for customer ID as “900001” and click **[!UICONTROL Test]**. 「出力」セクションには、顧客ID 900001用にMicrosoft Dynamicsから取得したレコードが表示されます。
1. 発行インスタンスで手順1 ～ 6を繰り返します。

## Adobe Sign スケジューラーの設定 {#scheduler}

オーサーインスタンスとパブリッシュインスタンスの両方で以下の手順を実行します。

1. Go to AEM Web Configuration console at `https://[server]:[host]/system/console/configMgr`.
1. Find and tap **[!UICONTROL Adobe Sign Configuration Service]** to open it for configuration.
1. ステー **[!UICONTROL タス更新スケジューラの式]****を0 0/2 &amp;ast；に設定&amp;ast;&amp;ast;?**。

   >[!NOTE]
   >
   >上記のようにスケジューラーを設定すると、Adobe Sign サービスのステータスが 2 分間隔で確認されます。

1. 「**[!UICONTROL 保存]**」をタップします。

## リファレンスサイトの Adobe Sign クラウドサービスの設定 {#sign-service}

オーサーインスタンスとパブリッシュインスタンスの両方で以下の手順を実行します。

1. Go to **[!UICONTROL Tools > Cloud Services > Adobe Sign > global]**. 「 **[!UICONTROL AEM Formsリファレンスサイトの署名]** 」を選択し、「プロパティ」をタ **[!UICONTROL ップしま]**&#x200B;す。

   >[!CAUTION]
   >
   >https://[host]:[ssl_port]/mnt/overlay/adobesign/cloudservices/adobesign/properties.html URLが、Adobe Sign APIアプリケーションのOAuth設定のリダイレクトURLリストに追加されていることを確認します。

1. クライアント ID と、Adobe Sign アプリケーション OAuth 設定の秘密鍵を指定します。
1. (Optional) Select the **[!UICONTROL Enable Adobe Sign for attachments also]** option, and tap **[!UICONTROL Connect to Adobe Sign]**. この操作により、アダプティブフォームの添付ファイルが、署名用に送信された対応する Adobe Sign ドキュメントに添付されます。
1. Tap **[!UICONTROL Connect to Adobe Sign]** and log in with your Adobe Sign credentials.

## フォーム共通設定サービスの構成 {#anonymous}

匿名ユーザーによるアクセスを許可するには、パブリッシュインスタンス上で以下の手順を実行します。

1. Go to AEM Web Configuration console at `https://[server]:[port]/system/console/configMgr`.
1. Find and tap **[!UICONTROL Forms Common Configuration Service]** to open it for configuration.
1. Configure the **[!UICONTROL Allow]** field for **[!UICONTROL All Users]**.
1. 「**[!UICONTROL 保存]**」をタップします。

## フォームデータモデルに対する REST サービスの修正 {#fdm}

オーサーインスタンスとパブリッシュインスタンスの両方で以下の手順を実行します。

1. CRXDE()に移動しま `https://[server]:[port]/crx/de/index.jsp`す。
1. /conf/global/settings/cloudconfigs/fdm/roi-rest/jcr:content/swaggerFileに移動し **、swaggerファイルを開きます** 。
1. 環境に応じてホストとポートの設定を更新します。
1. 設定を保存します。
1. (作成者&#x200B;**のみ**)ツール** **[!UICONTROL /サービス&#x200B;**/データソース**/**グローバルク&#x200B;**ラウ**]**&#x200B;ドインスタンスに移動します。 「 **[!UICONTROL roi-rest]** 」を選択し、「プロパティ」をタ **[!UICONTROL ップします]**。 「認証 **[!UICONTROL 設定]** 」をタップし、「認 **[!UICONTROL 証の種類]** 」を「基 **[!UICONTROL 本認証」に設定します]**。 サービ `admin`スにア `admin`クセスするためのユーザー名/パスワードを/と指定します。 Tap **[!UICONTROL Save &amp; Close]**.

## Marketing cloudとの統合 {#integrate-with-marketing-cloud}

AEM FormsをAdobe AnalyticsおよびAdobe targetと統合できます。 Adobe Analyticsはアダプティブフォームのレポートを生成し、パフォーマンスを分析するのに役立ちますが、Adobe targetはパーソナライズされたエクスペリエンスを提供し、アダプティブフォームのA/Bテストを実行するのに役立ちます。

AEM FormsでAdobe AnalyticsとAdobe targetを設定するには、次の手順を実行します。

### Adobe Analytics の設定 {#configure-adobe-analytics}

AEM Forms を Adobe Analytics に統合することで、フォームやドキュメントに顧客がどう対応するか監視および分析できます。問題のある領域を特定して修正し、コンバージョン率を上げるための対策を行うのに役立ちます。

この機能をリファレンスサイトで使用するには、「[分析とレポートの設定](/help/forms/using/configure-analytics-forms-documents.md)」の手順に従って、Analytics アカウントを設定します。

レポートを生成するために、シードデータはリファレンスサイトにバンドルされます。 シードデータを使用する前に、次の操作を行います。

1. AEMクラウドサービスでWe.FinanceおよびWe.Gov解析の設定が使用可能であることを確認します。 クラウドサービスは、次のいずれかの方法で検索できます。

   * ツール/ク **[!UICONTROL ラウドサービス/レガシーのクラウドサービスに移動するか]** 、https://&lt;host>:&lt;port>/libs/cq/core/content/tools/cloudservices.htmlを参照します。
   * In the **[!UICONTROL Cloud Services]** page, under **[!UICONTROL Adobe Analytics]** section, click `Show Configurations`. We.FinanceおよびWe.Govの設定が利用可能です。 クリックして設定を開きます。設定ページで「**[!UICONTROL 編集]**」をクリックします。有効な会社名、ユーザー名、共有暗号鍵（パスワード）およびデータセンターを入力し、「Analyticsに接続」 **[!UICONTROL をクリックします]**。 接続が成功したときのダイアログが表示されたら、設定ダ **[!UICONTROL イアログで]** 「OK」をクリックします。 Analyticsとレポートの設定の説明に従って、Analytics設定でフレ [ームワークを設定します](/help/forms/using/configure-analytics-forms-documents.md)。

1. https://&lt;*host*>:&lt;*port*>/system/console/configMgrに移動し、次の操作を行います。

   * In the **[!UICONTROL Web Console Configuration]** page, find and click **[!UICONTROL AEM Forms Analytics Configuration]**.
   * AEM Forms Analytics設定ダ **[!UICONTROL イアログの「SiteCatalystフレームワーク]** 」フィールドで、「we-finance(we-finance)」または「we-gov(we-gov)」を選択します。
   * 「**[!UICONTROL 保存]**」をクリックして、ページを更新します。

1. https://&lt;ホスト>:&lt;ポート>/aem/formsのForms Managerに移動し、次の操作を行います。

   * We.FinanceまたはWe.Govフォルダーを開き、レポートを表示するフォームを選択します。
   * アクションツールバーで「Analyticsを有効にする」をクリックします。 フォームの分析を有効にしたら、「Analytics レポート」をクリックします。空白のレポートが生成されたことを確認できます。空白のレポートが生成された後、デモ用の分析レポートを生成するには、リファレンスサイトパッケージに付属のシードデータを提供する必要があります。
   リファレンスサイトでは、クレジットカード、住宅ローン、チャイルドサポートの使用例のシードデータを使用して分析レポートを提供します。 シードデータの設定については、 [We.Financeリファレンスサイトのチュートリアル](/help/forms/using/finance-reference-site-walkthrough.md) 、 [We.Govリファレンスサイトのチュートリアルを参照してください](/help/forms/using/gov-reference-site-walkthrough.md)。

### Target の設定 {#configure-target}

リファレンスサイトでは、アダプティブドキュメントにターゲットを設定し、パーソナライズしたコンテンツを含めるための AEM Forms と Adobe Target の統合を紹介しています。さらに、アダプティブフォームの A/B テストを作成することもできます。

リファレンスサイトで統合を利用するには、AEM で次のように Target を設定します。

1. Start the author quickstart with the jvm argument `-Dabtesting.enabled=true` to enable A/B testing on the server.

   **注意**:AEMインスタンスがJBossで実行され、自動インストールからサービスとして開始される場合は、ファイルの次のエントリに `-Dabtesting.enabled=true` パラメーターを追加 `jboss\bin\standalone.conf.bat` します。

   `set "JAVA_OPTS=%JAVA_OPTS% -Dadobeidp.serverName=server1 -Dfile.encoding=utf8 -Djava.net.preferIPv4Stack=true -Dabtesting.enabled=true"`

1. Access https://&lt;*hostname*>:&lt;*port*>/libs/cq/core/content/tools/cloudservices.html.

1. In the **[!UICONTROL Adobe Target]** section, click **[!UICONTROL Show Configurations]**. We.Finance target設定が利用可能であることがわかります。 クリックして設定を開きます。設定ページで「**[!UICONTROL 編集]**」をクリックします。The **[!UICONTROL Edit Component]** dialog for the configuration opens.

1. Target アカウントに関連付けるクライアントコード、電子メール、パスワードを指定します。APIタイプを **[!UICONTROL RESTとして選択します]**。
1. 「**[!UICONTROL Adobe Target に接続]**」をクリックします。Targetアカウントが正常に設定されたら、「 **[!UICONTROL OK」をクリックします]**。 パッケージ化された設定にTarget Frameworkが含まれていることがわかります。

1. Go to https://&lt;*hostname*>:&lt;*port*>/system/console/configMgr.

1. 「**[!UICONTROL AEM Forms Target の設定]**」をクリックします。
1. Targetフレームワークを選択します。
1. 「**[!UICONTROL Target URLs]**」フィールドに、AEM Forms への URL を指定します。For example: https://&lt;*hostname*>:&lt;*port*>.

1. 「**[!UICONTROL 保存]**」をクリックします。

クレジットカード申し込みと住宅ローン申し込みの使用例では、A/Bテストの実行方法とデモ用のレポートの表示方法を示します。 チュートリアルについては、 [We.Financeリファレンスサイトのチュートリアルを参照してください](/help/forms/using/finance-reference-site-walkthrough.md)。

## 次の手順 {#next-step}

これで、リファレンスサイトを利用するための設定がすべて完了しました。リファレンスサイトのワークフローと手順についての詳細は以下を参照してください。

* [We.Finance リファレンスサイトのチュートリアル](/help/forms/using/finance-reference-site-walkthrough.md)
* [We.Gov リファレンスサイトのチュートリアル](/help/forms/using/gov-reference-site-walkthrough.md)

* [従業員セルフサービスリファレンスサイトのチュートリアル](/help/forms/using/employee-self-service-reference-site.md)

