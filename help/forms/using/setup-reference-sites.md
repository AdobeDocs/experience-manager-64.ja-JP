---
title: AEM Forms リファレンスサイトのセットアップおよび設定
seo-title: Set up and configure AEM Forms reference sites
description: AEM Forms のリファレンスサイトでは、AEM Forms を使用して、組織内にエンドツーエンドのワークフローを実装する方法を参照することができます。
seo-description: AEM Forms reference sites showcase how you can use AEM Forms to implement end-to-end workflow in an organization.
uuid: 087d58a1-d84e-49ac-a82d-4e7fc708f00f
content-type: reference
products: SG_EXPERIENCEMANAGER/6.4/FORMS
topic-tags: introduction
discoiquuid: 2feb4a9c-57ad-4c6b-a572-0047bc409bbb
exl-id: 9c5d956c-06bc-4428-afcd-02b4f81b802f
source-git-commit: e608249c3f95f44fdc14b100910fa11ffff5ee32
workflow-type: tm+mt
source-wordcount: '2911'
ht-degree: 46%

---

# AEM Forms リファレンスサイトのセットアップおよび設定 {#set-up-and-configure-aem-forms-reference-sites}

AEM Forms のリファレンスサイトでは、金融サービス業界や各種行政機関が AEM Forms をどのように使用して、複雑なトランザクションを、場所、時間、デバイスを問わないシンプルで魅力的なデジタルサービスに変換しているかについて紹介しています。

We.Finance と We.Gov のリファレンスサイトでは、実生活における使用例が紹介されています。最初の操作から通信やトランザクションの管理に至るまで、既存の顧客や見込み顧客に対して、カスタマイズされたコスト効率の高い方法でサービスを提供しています。

AEM Forms のリファレンスサイトでは、以下に示す AEM Forms の主要な機能を参照することができます。

* 魅力的でレスポンシブなアダプティブフォームとインタラクティブ通信のオーサリングエクスペリエンスを簡素化。
* インタラクティブ通信：デバイスの設定やレイアウトに合わせて、インタラクティブでパーソナライズされたレスポンシブな顧客通信を作成します。
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

リファレンスサイトを設定する前に、次の点を確認してください。

* **AEM essentials**

   AEM QuickStart、AEM Formsアドオンパッケージおよびリファレンスサイトパッケージ。 アドオンおよびリファレンスサイトパッケージの詳細については、[AEM Formsリリース](https://helpx.adobe.com/jp/aem-forms/kb/aem-forms-releases.html)を参照してください。

* **SMTP サービス** 任意の SMTP サービスを使用することができます。

* **Adobe Sign開発者アカウントとAdobe Sign APIアプリケーション**

   デジタル署名機能を使用するには、Adobe Sign開発者アカウントが必要です。 詳しくは、「[Adobe Sign](https://acrobat.adobe.com/jp/ja/why-adobe/developer-form.html)」を参照してください。

* AEM Formsと統合するMicrosoft Dynamics 365の実行中のインスタンス。 リファレンスサイトを実行するには、サンプルデータをMicrosoft Dynamicsインスタンスに読み込み、リファレンスサイトで使用するインタラクティブ通信を事前に入力します。
* Formsアドオンパッケージを含むAEM 6.4の実行インスタンス。 詳しくは、「[AEM Forms のインストールと設定](installing-configuring-aem-forms-osgi.md)」を参照してください。

リファレンスサイトのセットアップと構成を行うには、以下の手順を実行します。以下に記載されているとおりの順序で実行することをお勧めします。

<table> 
 <tbody> 
  <tr> 
   <th><strong>ステップ</strong></th> 
   <th><strong> の設定</strong></th> 
   <th><strong>備考</strong></th> 
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
   <td>xssセキュリティによってブロックされている$、{、}文字を上書きするために使用します。</td> 
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
   <td>クレジットカード申し込み、住宅ローン申し込み、住宅保険申し込みのチュートリアル用のサンプルデータをインポートします。</td> 
  </tr> 
  <tr> 
   <td><a href="/help/forms/using/setup-reference-sites.md#configure-oauth-cloud-service-for-microsoft-dynamics">OAuth クラウドサービスを Microsoft Dynamics 用に設定する</a></td> 
   <td>オーサーインスタンスとパブリッシュインスタンス</td> 
   <td>AEM FormsでOAuthクラウドサービスを設定して、AEM FormsとMicrosoft Dynamics間の通信を有効にします。 </td> 
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
   <td>この設定により、匿名ユーザーに対して送信、署名、レコードのドキュメントを生成できます。</td> 
  </tr> 
  <tr> 
   <td><a href="#fdm">フォームデータモデルに対する REST サービス Swagger ファイルの修正</a></td> 
   <td>オーサーインスタンスとパブリッシュインスタンス<br /> </td> 
   <td>現在の環境に合わせてサービスを修正します。</td> 
  </tr> 
 </tbody> 
</table>

## AEM Forms のインストールと設定 {#install-and-configure-aem-forms}

「[OSGi](/help/forms/using/installing-configuring-aem-forms-osgi.md)へのAEM Formsのインストールと設定」の説明に従って、AEM Formsをインストールしてデプロイします。

>[!NOTE]
>
>複数のパブリッシュインスタンスが存在する場合や、オーサーインスタンスとパブリッシュインスタンスが異なるマシン上に存在する場合は、複製エージェントと逆複製エージェントを設定してください。

## SSL の設定 {#ssl}

Adobe Sign サーバーとの通信を行うには、SSL を設定する必要があります。詳細な手順については、[HTTP over SSLの有効化](/help/sites-administering/ssl-by-default.md)を参照してください。

>[!CAUTION]
>
>`/etc/map`フォルダーで強制SSLを設定しないでください。

## Day CQ Link Externalizer の設定 {#externalizer}

AEMの&#x200B;**Externalizer**&#x200B;は、事前に設定されたDNSでパスを接頭辞として付け、リソースパス（例えば、/path/to/my/page）を外部および絶対URL(例えば、https://www.mycompany.com/path/to/my/page)にプログラムで変換できるOSGIサービスです。 詳しくは、「[URL の外部化](/help/sites-developing/externalizer.md)」を参照してください。

>[!CAUTION]
>
>SSL で自己署名証明書を使用する場合は、HTTPS URL を外部化しないでください。
>
>また、ローカルサーバーの場合は、サーバーのホスト名ではなく localhost を使用してください。

オーサーインスタンスとパブリッシュインスタンスの両方で、以下の手順を実行します。

1. OSGi設定(https://&lt;*hostname>*:*port>*/system/console/configMgr)に移動します。
1. **[!UICONTROL Day CQ Link Externalizer]**&#x200B;設定を探してタップします。

   設定を編集するための Day CQ Link Externalizer ダイアログが表示されます。

1. Day CQ Link Externalizer ダイアログの「ドメイン」フィールドで、以下の操作を実行します。

   * オーサーインスタンスで、外部システムからアクセス可能な発行 URL を指定します。例えば、ホスト名や発行用の Web サーバーを指定します。
   * パブリッシュインスタンスで、オーサー URL と発行 URL の両方を指定します。

1. オーサーインスタンスとパブリッシュインスタンスの両方で、「ドメイン」フィールドにローカルサーバーの URL が指定されていることを確認します。
1. 「**[!UICONTROL 保存]**」をタップします。すべてのサービスが再開されるまで待ちます。

## Day CQ 電子メールサービスの設定 {#cqmail}

リファレンスサイトの実装では、ユーザーがフォームに入力して送信した場合に電子メールをサンプルユーザーに送信する必要があります。Day CQ 電子メールサービスを設定して SMTP サービスの詳細を指定することにより、顧客に対して電子メールを自動的に送信することができます。詳しくは、「[電子メール通知の設定](/help/sites-administering/notification.md)」を参照してください。

パブリッシュインスタンスで以下の手順を実行して、電子メールサービスを設定します。

1. OSGi設定(https://&lt;*hostname>*:*port>*/system/console/configMgr)に移動します。
1. 「**[!UICONTROL Day CQ Mail Service]**」を探してタップし、設定用に開きます。
1. SMTP サーバーのホスト名とポートの値を入力します。
1. 「**[!UICONTROL 保存]**」をタップします。

>[!NOTE]
>
>社内の SMTP サービスを使用することも、Gmail などのパブリックサービスを使用することもできます。SMTP サービスの設定方法については、SMTP サービスのマニュアルを参照してください。

## デフォルトの XSS 設定の上書き {#xss}

We.Finance リファレンスサイトの電子メールテンプレートには、電子メール内で使用するカスタマイズされた各種リンクが用意されています。これらのリンクには、`${placeholder}`というプレースホルダーがあります。 プレースホルダーは、電子メールの送信前に実際の値に置き換えられます。AEM のデフォルトの XSS 保護設定では、HTML コンテンツ内の URL に波括弧（**{ }**）を使用できません。ただし、パブリッシュインスタンスで以下の手順を実行することにより、デフォルトの設定を上書きすることができます。

1. `/libs/cq/xssprotection/config.xml` を `/apps/cq/xssprotection/config.xml` にコピーします。
1. 次を開きます： `/apps/cq/xssprotection/config.xml`.
1. `common-regexps`セクションで、`onsiteURL`エントリを次のように変更し、ファイルを保存します。

   `<regexp name="onsiteURL" value="([\p{L}\p{N}\\\.\#@\$\{\}%\+&;\-_~,\?=/!\*\(\)]*|\#(\w)+)"/>`

>[!NOTE]
>
>中括弧(**{ }**)は、HTMLコンテンツのURLに使用できる文字として含まれます。

SMTP サーバーを設定したら、Sarah Rose のペルソナを使ってフォームに入力し、下書きとして保存します。下書きとして保存する場合、電子メールを使用してその下書きを受信するオプションがあります。「**電子メールを送信**」ボタンをタップして、アプリケーションのドラフトのリンクが記載された電子メールを受信すれば、電子メールが正しく設定されています。Sarah の資格情報を使用してログインし、下書きを参照できることを確認してください。

## AEM DS の設定 {#aemds}

リファレンスサイトの使用例では、電子メール通信用のパブリッシュインスタンスにAEM DSサービスの設定が必要です。 パブリッシュインスタンスでAEM DSサービスを設定する詳細な手順については、「[AEM DSの設定](/help/forms/using/configuring-the-processing-server-url-.md)」を参照してください。

AEM Formsリファレンスサイトの場合、AEM DS Settings Serviceで、処理サーバーのURLではなく、パブリッシュサーバーのURLを指定します。

>[!CAUTION]
>
>AEM Forms OSGi用に設定する場合は、処理サーバーのURLに`/lc`を入れないでください。

## リファレンスサイトパッケージのデプロイメント {#refsite}

ソフトウェアディストリビューションを使用して、以下のリファレンスサイトパッケージをインストールします。

* [AEM-FORMS-6.4-FSI-REF-SITE](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq640/fd/AEM-FORMS-6.4-FSI-REF-SITE)
* [AEM-FORMS-6.4-GOV-REF-SITE](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq640/fd/AEM-FORMS-6.4-GOV-REF-SITE)

パッケージの使用方法について詳しくは、[パッケージの使用方法](/help/sites-administering/package-manager.md)を参照してください。

パッケージをインストールして、オーサーインスタンスとパブリッシュインスタンスを開始したら、ブラウザーで以下の URL にアクセスします。

* `https://[server]:[port]/wegov`
* `https://[server]:[port]/wefinance`

インストールが正常に完了すると、We.Gov と We.Finance のリファレンスサイトのランディングページにアクセスできるようになります。

## （オプション）サンプルデータをMicrosoft Dynamicsに読み込む {#optional-import-sample-data-into-microsoft-dynamics}

住宅ローン申し込みと自動保険申し込みリファレンスサイトは、Microsoft Dynamicsのレコードを使用するように構成されています。 リファレンスサイトパッケージでは、Microsoft Dynamicsに読み込んでリファレンスサイトを実行できるカスタムエンティティとサンプルレコードがインストールされます。 サンプルデータを移行して設定するには、次の手順を実行します。

自動保険申し込みのカスタムエンティティをインポートする手順は、次のとおりです。

1. AEMオーサーインスタンスの`https://[server]:[port]/content/aemforms-refsite-collaterals/we-finance/auto-insurance/ms-dynamics/WeFinanceAutoInsurance_1_0.zip`から&#x200B;**WeFinanceAutoInsurance_1_0.zip**&#x200B;ソリューションパッケージをダウンロードします。
1. Microsoft Dynamicsインスタンスで、**[!UICONTROL 設定]**&#x200B;メニューの&#x200B;**[!UICONTROL ソリューション]**&#x200B;に移動し、**[!UICONTROL 読み込み]**&#x200B;をクリックします。 パッケージを選択してインポートします。

自動保険申し込みのカスタムエンティティをインポートする手順は、次のとおりです。

1. https://[author]:[port]/content/aemforms-refsite-collaterals/we-finance/home-mortgage/ms-dynamics/AEMFormsFSIRefsite_1_0.zipから&#x200B;**AEMFormsFSIRefsite_1_0.zip**&#x200B;パッケージをダウンロードします。 パッケージを選択してインポートします。

1. Microsoft Dynamicsインスタンスで、**[!UICONTROL 設定]**&#x200B;メニューの&#x200B;**[!UICONTROL ソリューション]**&#x200B;に移動し、**[!UICONTROL 読み込み]**&#x200B;をクリックします。 パッケージを選択してインポートします。

顧客および保険契約レコードをインポートする手順は、次のとおりです。

1. AEMオーサーインスタンスの次の場所から、 **We.Finance Customers.csv 、 We.Finance Auto Insurance Renewals.csv** 、および&#x200B;**住宅ローン**&#x200B;のデータファイルをダウンロードします。

   * `https://[server]:[port/content/aemforms-refsite-collaterals/we-finance/auto-insurance/ms-dynamics/We.Finance Customers.csv`
   * `https://[server]:[port/content/aemforms-refsite-collaterals/we-finance/auto-insurance/ms-dynamics/We.Finance Auto Insurance Renewals.csv`
   * `https://[server]:[port]/content/aemforms-refsite-collaterals/we-finance/home-mortgage/ms-dynamics/Sarah%20Rose%20Contact.csv`

1. Microsoft Dynamicsインスタンスで、次の操作を行います。

   * **[!UICONTROL Sales/We.Financeのお客様]**&#x200B;に移動し、**[!UICONTROL 「]**&#x200B;をインポート」をクリックします。
   * **[!UICONTROL Sales/We.Finance Auto Insurance]**&#x200B;に移動し、「**[!UICONTROL Import]**」をクリックします。
   * **[!UICONTROL Sales/We.Finance Home Mortgage]**&#x200B;に移動し、**[!UICONTROL 「Import]**」をクリックします。

## OAuth クラウドサービスを Microsoft Dynamics 用に設定する {#configure-oauth-cloud-service-for-microsoft-dynamics}

AEM FormsでOAuthクラウドサービスを設定して、AEM FormsとMicrosoft Dynamics間の通信を有効にします。 次の手順を実行して、AEMオーサーインスタンスとパブリッシュCloud ServiceでOAuthインスタンスを設定します。

1. AEMオーサーインスタンスで、**[!UICONTROL ツール/Cloud Services/データソース/グローバル]**&#x200B;に移動します。 **[!UICONTROL Refsite Dynamics Integration]**&#x200B;アイコンをタップし、**[!UICONTROL 「プロパティ」]**&#x200B;をタップします。
1. Microsoft Azure Active Directory のアカウントに移動します。登録済みアプリケーションの「**[!UICONTROL 応答 URL]**」設定に、コピーしたクラウドサービス設定の URL を追加します。設定を保存します。
1. 「認証設定」タブで、Microsoft Dynamicsインスタンスの「**[!UICONTROL サービスルート]**」、「**[!UICONTROL クライアントID]**」、「**[!UICONTROL クライアントの秘密鍵]**」、「**[!UICONTROL リソースURL]**」を指定します。 Microsoft Dynamicsのログインページにリダイレクトする「**[!UICONTROL OAuth]**&#x200B;に接続」をクリックします。
1. ログイン情報を入力します。ログインすると、AEM Forms Cloud Service設定ページにリダイレクトされます。 「**[!UICONTROL 保存して閉じる]**」をクリックします。クラウドサービスの設定が保存されます。
1. **[!UICONTROL Forms/データ統合/We.Finance]**&#x200B;に移動します。 [自動保険(Dynamics)]を選択し、[編集]をクリックします。 Microsoft Dynamicsエンティティは、「データソース」タブに表示されます。 すべてのエンティティがMicrosoft Dynamicsから取得され、「データソース」タブに表示されるまで待ちます。
1. **[!UICONTROL AutoInsuranceRenewalエンティティ]**&#x200B;を選択し、「**[!UICONTROL モデルオブジェクトをテスト]**」をクリックします。 入力リクエストセクションで、顧客IDの値を「900001」と指定し、「**[!UICONTROL テスト]**」をクリックします。 「出力」セクションには、顧客ID 900001のMicrosoft Dynamicsから取得されたレコードが表示されます。
1. 入力リクエストセクションで、顧客IDの値を「900001」と指定し、「**[!UICONTROL テスト]**」をクリックします。 「出力」セクションには、顧客ID 900001のMicrosoft Dynamicsから取得されたレコードが表示されます。
1. パブリッシュインスタンスで手順1 ～ 6を繰り返します。

## Adobe Sign スケジューラーの設定 {#scheduler}

オーサーインスタンスとパブリッシュインスタンスの両方で以下の手順を実行します。

1. `https://[server]:[host]/system/console/configMgr`のAEM Web設定コンソールに移動します。
1. **[!UICONTROL Adobe Sign Configuration Service]**&#x200B;を探してタップし、設定用に開きます。
1. **[!UICONTROL ステータス更新スケジューラーの式]**&#x200B;を&#x200B;**0 0/2 &amp;ast；として設定します。&amp;ast;&amp;ast;?**.

   >[!NOTE]
   >
   >上記のようにスケジューラーを設定すると、Adobe Sign サービスのステータスが 2 分間隔で確認されます。

1. 「**[!UICONTROL 保存]**」をタップします。

## リファレンスサイトの Adobe Sign クラウドサービスの設定 {#sign-service}

オーサーインスタンスとパブリッシュインスタンスの両方で以下の手順を実行します。

1. **[!UICONTROL ツール/Cloud Services/Adobe Sign/グローバル]**&#x200B;に移動します。 「**[!UICONTROL AEM Formsリファレンスサイトの署名]**」を選択し、「**[!UICONTROL プロパティ]**」をタップします。

   >[!CAUTION]
   >
   >https://[host]:[ssl_port]/mnt/overlay/adobesign/cloudservices/adobesign/properties.html URLがAdobe Sign APIアプリケーションのOAuth設定のリダイレクトURLリストに追加されていることを確認します。

1. クライアント ID と、Adobe Sign アプリケーション OAuth 設定の秘密鍵を指定します。
1. （オプション）「**[!UICONTROL 添付ファイルにもAdobe Signを有効にする]**」オプションを選択し、「**[!UICONTROL Adobe Signに接続]**」をタップします。 この操作により、アダプティブフォームの添付ファイルが、署名用に送信された対応する Adobe Sign ドキュメントに添付されます。
1. 「**[!UICONTROL Adobe Signに接続]**」をタップし、Adobe Signの資格情報を使用してログインします。

## フォーム共通設定サービスの構成 {#anonymous}

匿名ユーザーによるアクセスを許可するには、パブリッシュインスタンス上で以下の手順を実行します。

1. `https://[server]:[port]/system/console/configMgr`のAEM Web設定コンソールに移動します。
1. **[!UICONTROL Forms Common Configuration Service]**&#x200B;を探してタップし、設定用に開きます。
1. **[!UICONTROL すべてのユーザー]**&#x200B;に対して&#x200B;**[!UICONTROL 許可]**&#x200B;フィールドを設定します。
1. 「**[!UICONTROL 保存]**」をタップします。

## フォームデータモデルに対する REST サービスの修正 {#fdm}

オーサーインスタンスとパブリッシュインスタンスの両方で以下の手順を実行します。

1. CRXDE(`https://[server]:[port]/crx/de/index.jsp`)に移動します。
1. **/conf/global/settings/cloudconfigs/fdm/roi-rest/jcr:content/swaggerFile**&#x200B;に移動し、swaggerファイルを開きます。
1. 環境に応じてホストとポートの設定を更新します。
1. 設定を保存します。
1. （**オーサーインスタンスのみ**）**[!UICONTROL ツール]**/**[!UICONTROL Cloud Services]**/**[!UICONTROL データソース]**/**[!UICONTROL グローバル]**&#x200B;に移動します。 **[!UICONTROL roi-rest]**&#x200B;を選択し、**[!UICONTROL プロパティ]**&#x200B;をタップします。 「**[!UICONTROL 認証設定]**」をタップし、「**[!UICONTROL 認証の種類]**」を「**[!UICONTROL 基本認証]**」に設定します。 サービスにアクセスするユーザー名とパスワードとして`admin`/ `admin`を指定します。 「**[!UICONTROL 保存して閉じる]**」をタップします。

## Marketing Cloudとの統合 {#integrate-with-marketing-cloud}

AEM FormsをAdobe AnalyticsおよびAdobe Targetと統合できます。 Adobe Analyticsは、アダプティブフォームのレポートを生成し、パフォーマンスを分析するのに役立ちますが、Adobe Targetは、パーソナライズされたエクスペリエンスを提供し、アダプティブフォームのA/Bテストを実行するのに役立ちます。

AEM FormsでAdobe AnalyticsとAdobe Targetを設定するには、次の手順を実行します。

### Adobe Analytics の設定 {#configure-adobe-analytics}

AEM Forms を Adobe Analytics に統合することで、フォームやドキュメントに顧客がどう対応するか監視および分析できます。問題のある領域を特定して修正し、コンバージョン率を上げるのに役立ちます。

この機能をリファレンスサイトで使用するには、「[分析とレポートの設定](/help/forms/using/configure-analytics-forms-documents.md)」の手順に従って、Analytics アカウントを設定します。

レポートを生成するために、シードデータはリファレンスサイトにバンドルされます。 シードデータを使用する前に、次の操作を行います。

1. We.FinanceとWe.Govの分析設定がAEMクラウドサービスで使用可能であることを確認します。 クラウドサービスは、次のいずれかの方法で検索できます。

   * **[!UICONTROL ツール/Cloud Services/従来のCloud Services]**&#x200B;に移動するか、https://&lt;host>:&lt;port>/libs/cq/core/content/tools/cloudservices.htmlを参照します。
   * **[!UICONTROL Cloud Services]**&#x200B;ページの&#x200B;**[!UICONTROL Adobe Analytics]**&#x200B;セクションで、`Show Configurations`をクリックします。 We.FinanceおよびWe.Govの設定を使用できます。 クリックして設定を開きます。設定ページで「**[!UICONTROL 編集]**」をクリックします。有効な会社名、ユーザー名、共有暗号鍵（パスワード）およびデータセンターを入力し、「**[!UICONTROL Analyticsに接続]**」をクリックします。 接続に成功したダイアログが表示されたら、設定ダイアログで「**[!UICONTROL OK]**」をクリックします。 [Analyticsとレポートの設定](/help/forms/using/configure-analytics-forms-documents.md)の説明に従って、Analytics設定の下でフレームワークを設定します。

1. https://&lt;*host*:&lt;*port*/system/console/configMgrに移動し、次の操作を行います。

   * **[!UICONTROL Webコンソール設定]**&#x200B;ページで、**[!UICONTROL AEM Forms Analytics設定]**&#x200B;を探してクリックします。
   * AEM Forms Analytics設定ダイアログの「**[!UICONTROL SiteCatalystフレームワーク]**」フィールドで、we-finance(we-finance)またはwe-gov(we-gov)を選択します。
   * 「**[!UICONTROL 保存]**」をクリックして、ページを更新します。

1. https://&lt;host>:&lt;port>/aem/formsのForms Managerに移動し、次の操作を行います。

   * We.FinanceフォルダーまたはWe.Govフォルダーを開き、レポートを表示するフォームを選択します。
   * アクションツールバーの「 Analyticsを有効にする」をクリックします。 フォームの分析を有効にしたら、「Analytics レポート」をクリックします。空白のレポートが生成されたことを確認できます。空のレポートが生成されたら、デモ用に分析レポートを生成するために、リファレンスサイトパッケージに付属のシードデータを提供する必要があります。

   リファレンスサイトは、クレジットカード、住宅ローン、チャイルドサポートの使用例に関するシードデータを含む分析レポートを提供します。 シードデータの設定については、[We.Financeリファレンスサイトのチュートリアル](/help/forms/using/finance-reference-site-walkthrough.md)および[We.Govリファレンスサイトのチュートリアル](/help/forms/using/gov-reference-site-walkthrough.md)を参照してください。

### Target の設定 {#configure-target}

リファレンスサイトでは、アダプティブドキュメントにターゲットを設定し、パーソナライズしたコンテンツを含めるための AEM Forms と Adobe Target の統合を紹介しています。さらに、アダプティブフォームの A/B テストを作成することもできます。

リファレンスサイトで統合を利用するには、AEM で次のように Target を設定します。

1. サーバーでA/Bテストを有効にするには、jvm引数`-Dabtesting.enabled=true`でオーサークイックスタートを起動します。

   **注意**:AEMインスタンスがJBoss（自動インストールからサービスとして開始）上で動作している場合は、ファイルの次のエントリにパラメー `-Dabtesting.enabled=true` ターを追加 `jboss\bin\standalone.conf.bat` します。

   `set "JAVA_OPTS=%JAVA_OPTS% -Dadobeidp.serverName=server1 -Dfile.encoding=utf8 -Djava.net.preferIPv4Stack=true -Dabtesting.enabled=true"`

1. https://&lt;*hostname*:&lt;*port*>/libs/cq/core/content/tools/cloudservices.htmlにアクセスします。

1. 「**[!UICONTROL Adobe Target]**」セクションで、「**[!UICONTROL 設定を表示]**」をクリックします。 We.Finance Target設定を使用できます。 クリックして設定を開きます。設定ページで「**[!UICONTROL 編集]**」をクリックします。設定の&#x200B;**[!UICONTROL コンポーネントを編集]**&#x200B;ダイアログが開きます。

1. Target アカウントに関連付けるクライアントコード、電子メール、パスワードを指定します。APIタイプとして&#x200B;**[!UICONTROL REST]**&#x200B;を選択します。
1. 「**[!UICONTROL Adobe Target に接続]**」をクリックします。Targetアカウントが正常に設定されたら、「**[!UICONTROL OK]**」をクリックします。 パッケージ化された設定にTargetフレームワークが含まれていることを確認できます。

1. https://&lt;*hostname*>:&lt;*port*/system/console/configMgrに移動します。

1. 「**[!UICONTROL AEM Forms Target の設定]**」をクリックします。
1. Targetフレームワークを選択します。
1. 「**[!UICONTROL Target URLs]**」フィールドに、AEM Forms への URL を指定します。例：https://&lt;*hostname*>:&lt;*port*>.

1. 「**[!UICONTROL 保存]**」をクリックします。

クレジットカード申し込みと住宅ローン申し込みの使用例では、デモ用にA/Bテストを実行し、レポートを表示する方法を示しています。 チュートリアルについては、[We.Financeリファレンスサイトのチュートリアル](/help/forms/using/finance-reference-site-walkthrough.md)を参照してください。

## 次の手順 {#next-step}

これで、リファレンスサイトを利用するための設定がすべて完了しました。リファレンスサイトのワークフローと手順についての詳細は以下を参照してください。

* [We.Finance リファレンスサイトのチュートリアル](/help/forms/using/finance-reference-site-walkthrough.md)
* [We.Gov リファレンスサイトのチュートリアル](/help/forms/using/gov-reference-site-walkthrough.md)

* [従業員セルフサービスリファレンスサイトのチュートリアル](/help/forms/using/employee-self-service-reference-site.md)
