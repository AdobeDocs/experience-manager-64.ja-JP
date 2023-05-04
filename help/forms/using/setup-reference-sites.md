---
title: AEM Formsリファレンスサイトのセットアップと設定
seo-title: Set up and configure AEM Forms reference sites
description: AEM Formsリファレンスサイトでは、AEM Formsを使用して組織にエンドツーエンドのワークフローを実装する方法を紹介しています。
seo-description: AEM Forms reference sites showcase how you can use AEM Forms to implement end-to-end workflow in an organization.
uuid: 087d58a1-d84e-49ac-a82d-4e7fc708f00f
content-type: reference
products: SG_EXPERIENCEMANAGER/6.4/FORMS
topic-tags: introduction
discoiquuid: 2feb4a9c-57ad-4c6b-a572-0047bc409bbb
exl-id: 9c5d956c-06bc-4428-afcd-02b4f81b802f
source-git-commit: c5b816d74c6f02f85476d16868844f39b4c47996
workflow-type: tm+mt
source-wordcount: '2947'
ht-degree: 5%

---

# AEM Formsリファレンスサイトのセットアップと設定 {#set-up-and-configure-aem-forms-reference-sites}

>[!CAUTION]
>
>AEM 6.4 の拡張サポートは終了し、このドキュメントは更新されなくなりました。 詳細は、 [技術サポート期間](https://helpx.adobe.com/jp/support/programs/eol-matrix.html). サポートされているバージョンを見つける [ここ](https://experienceleague.adobe.com/docs/?lang=ja).

AEM Formsはリファレンスサイトの実装を提供し、AEM Formsが金融サービス業界や政府機関が、複雑なトランザクションを、いつでも、任意のデバイス上で、簡単で魅力的なデジタルエクスペリエンスに変えるのにどのように役立つかを示しています。

We.Finance および We.Gov リファレンスサイトは、既存のお客様や潜在的なお客様との関わり合いを、ファーストタッチの時点から、パーソナライズされたコスト効率の高い方法で通信やトランザクションを管理する、実際の使用例を描きます。

リファレンスサイトでは、AEM Formsの次の主要機能を参照、紹介できます。

* 魅力的でレスポンシブなアダプティブフォームとインタラクティブ通信のオーサリングエクスペリエンスをシンプルにしました。
* インタラクティブ通信：デバイスの設定やレイアウトに適応する、インタラクティブでパーソナライズされたレスポンシブな顧客通信を作成します。
* 異なるデータソースに接続し、フォームデータモデルを使用してフォームデータを事前入力および送信するためのデータ統合。
* ビジネスプロセスとワークフローを自動化するFormsワークフロー。
* 高度なユーザーデータ管理および処理機能。
* Acrobat Signとの統合により、アダプティブフォームに安全に署名して送信することができます。
* ターゲットを絞ったレコメンデーションを提供し、フォームからの ROI を最大化する A/B テストを実行するAdobe Targetとの統合。
* Adobe Analyticsとの統合により、フォームやキャンペーンのパフォーマンスを測定し、十分な情報に基づいた意思決定をおこなうことができます。
* フォーム入力の操作性が向上しました。

リファレンスサイトには、独自のアセットを作成するためのテンプレートとして使用できる、再利用可能なアセットが用意されています。

* Acrobat Signとの統合により、アダプティブフォームに安全に署名して送信することができます。

* Acrobat Signとの統合により、アダプティブフォームに安全に署名して送信することができます。

## リファレンスサイトの前提条件と設定手順 {#prerequisites-and-steps-to-set-up-reference-sites}

リファレンスサイトを設定する前に、次の点を確認してください。

* **AEM essentials**

   AEM QuickStart、AEM Formsアドオンパッケージ、およびリファレンスサイトパッケージ。 詳しくは、 [AEM Formsリリース](https://helpx.adobe.com/jp/aem-forms/kb/aem-forms-releases.html) アドオンおよびリファレンスサイトのパッケージの詳細。

* **SMTP サービス**
任意の SMTP サービスを使用できます。

* **Acrobat Sign開発者アカウントとAcrobat Sign API アプリケーション**

   デジタル署名機能を使用するには、Acrobat Sign開発者アカウントが必要です。 詳しくは、 [Acrobat Sign](https://acrobat.adobe.com/jp/ja/why-adobe/developer-form.html).

* AEM Formsと統合するMicrosoft Dynamics 365 の実行中のインスタンス。 リファレンスサイトを実行するには、サンプルデータをMicrosoft Dynamics インスタンスに読み込んで、リファレンスサイトで使用されるインタラクティブ通信に事前に入力します。
* Formsアドオンパッケージを含むAEM 6.4 の実行インスタンス。 詳しくは、 [AEM Formsのインストールと設定](installing-configuring-aem-forms-osgi.md).

次の手順を推奨順に実行して、リファレンスサイトを設定します。

<table> 
 <tbody> 
  <tr> 
   <th><strong>手順</strong></th> 
   <th><strong> の設定</strong></th> 
   <th><strong>備考</strong></th> 
  </tr> 
  <tr> 
   <td><a href="#installaemforms">AEM Forms のインストールと設定</a></td> 
   <td>オーサーとパブリッシュ</td> 
   <td>AEM Formsオーサーインスタンスとパブリッシュインスタンスをインストールして設定します。</td> 
  </tr> 
  <tr> 
   <td><a href="#ssl">SSL の設定</a></td> 
   <td>オーサーとパブリッシュ<br /> </td> 
   <td>Acrobat Signとの安全な通信のために、HTTP over SSL を有効にします。</td> 
  </tr> 
  <tr> 
   <td><p><a href="#externalizer">Day CQ Link Externalizer の設定</a></p> </td> 
   <td>オーサーとパブリッシュ<br /> </td> 
   <td><p>リファレンスサイトの使用例では、様々なトランザクション用の E メールを配信します。 この設定は、E メールを使用したニュースレターの配信に必要です。 これにより、URL と画像がパブリッシュインスタンスを指すようになります。 </p> </td> 
  </tr> 
  <tr> 
   <td><a href="#cqmail">Day CQ メールサービスの設定</a></td> 
   <td>オーサーとパブリッシュ</td> 
   <td>電子メール通信に必要です。</td> 
  </tr> 
  <tr> 
   <td><a href="#xss">デフォルトの XSS 設定を上書き</a></td> 
   <td>パブリッシュ</td> 
   <td>xss セキュリティによってブロックされている$、{、} 文字を上書きするために使用されます。</td> 
  </tr> 
  <tr> 
   <td><a href="#aemds">AEM DS の設定</a></td> 
   <td>オーサー</td> 
   <td>パブリッシュインスタンスでのフォーム送信と、オーサーインスタンスでの処理ワークフローに対して、AEM DS を設定します。</td> 
  </tr> 
  <tr> 
   <td><a href="#refsite">リファレンスサイトパッケージのデプロイ</a></td> 
   <td>オーサー</td> 
   <td>AEM Formsオーサーインスタンスにリファレンスサイトパッケージをデプロイします。</td> 
  </tr> 
  <tr> 
   <td><a href="/help/forms/using/setup-reference-sites.md#optional-import-sample-data-into-microsoft-dynamics">サンプルデータをMicrosoft Dynamics に読み込む</a></td> 
   <td>オーサーとパブリッシュ</td> 
   <td>クレジットカード申し込み、住宅ローン申し込み、住宅保険申し込みのチュートリアル用のサンプルデータをインポートします</td> 
  </tr> 
  <tr> 
   <td><a href="/help/forms/using/setup-reference-sites.md#configure-oauth-cloud-service-for-microsoft-dynamics">Microsoft Dynamics の OAuth クラウドサービスを設定する</a></td> 
   <td>オーサーとパブリッシュ</td> 
   <td>AEM FormsとMicrosoft Dynamics 間の通信を有効にするように、AEM Formsで OAuth クラウドサービスを設定します。 </td> 
  </tr> 
  <tr> 
   <td><a href="#scheduler">Acrobat Sign Scheduler の設定</a></td> 
   <td>オーサーとパブリッシュ<br /> </td> 
   <td>スケジューラーの設定を変更し、2 分ごとにステータスを確認します。</td> 
  </tr> 
  <tr> 
   <td><a href="#sign-service">参照サイトの設定Acrobat SignCloud Service</a></td> 
   <td>オーサーとパブリッシュ<br /> </td> 
   <td>リファレンスサイトパッケージに付属し、有効な資格情報を使用して再設定が必要な設定。</td> 
  </tr> 
  <tr> 
   <td><a href="#anonymous">匿名ユーザー向けのForms Common Configuration Service の設定</a></td> 
   <td>パブリッシュ</td> 
   <td>この設定により、匿名ユーザーに対して送信、署名、レコードのドキュメントを生成できます。</td> 
  </tr> 
  <tr> 
   <td><a href="#fdm">フォームデータモデル用の Rest Service Swagger ファイルの変更</a></td> 
   <td>オーサーとパブリッシュ<br /> </td> 
   <td>環境のサービスを変更します。</td> 
  </tr> 
 </tbody> 
</table>

## AEM Forms のインストールと設定 {#install-and-configure-aem-forms}

AEM Formsのインストールとデプロイ ( [OSGi へのAEM Formsのインストールと設定](/help/forms/using/installing-configuring-aem-forms-osgi.md).

>[!NOTE]
>
>複数のパブリッシュインスタンスがある場合や、オーサーインスタンスとパブリッシュインスタンスが異なるマシンに存在する場合は、レプリケーションエージェントとリバースレプリケーションエージェントを設定します。

## SSL の設定 {#ssl}

Acrobat Signサーバーと通信するには、SSL 設定が必要です。 詳細な手順については、 [HTTP over SSL の有効化](/help/sites-administering/ssl-by-default.md).

>[!CAUTION]
>
>SSL の強制を設定しない `/etc/map` フォルダー。

## Day CQ Link Externalizer の設定 {#externalizer}

AEMで、 **Externalizer** は、事前に設定された DNS でパスの前にを付けることで、リソースパス（例えば、/path/to/my/page）を外部の絶対 URL および絶対 URL( 例えば、https://www.mycompany.com/path/to/my/page) にプログラムで変換できる OSGI サービスです。 詳しくは、 [URL の外部化](/help/sites-developing/externalizer.md).

>[!CAUTION]
>
>SSL に自己署名証明書を使用している場合は、HTTPS URL に外部化しないでください。
>
>また、ローカルサーバーには、ホスト名の代わりに localhost を使用します。

オーサーインスタンスとパブリッシュインスタンスの両方で、次の手順を実行します。

1. OSGi 設定 (https://&lt;) に移動します。*hostname>*:&lt;*ポート >*/system/console/configMgr.
1. 検索とタップ **[!UICONTROL Day CQ Link Externalizer]** 設定。

   Day CQ Link Externalizer ダイアログが開き、設定を編集できます。

1. Day CQ Link Externalizer ダイアログで、「ドメイン」フィールドの次の操作を実行します。

   * オーサーインスタンスで、外部システムからアクセスできるパブリッシュ URL を指定します。 例えば、ホスト名や発行用 Web サーバーなどです。
   * パブリッシュインスタンスで、オーサー URL とパブリッシュ URL の両方を指定します。

1. オーサーインスタンスとパブリッシュインスタンスの両方で、ローカルサーバーの URL が「ドメイン」フィールドに指定されていることを確認します。
1. 「**[!UICONTROL 保存]**」をタップします。すべてのサービスが再起動するまでしばらく待ちます。

## Day CQ メールサービスの設定 {#cqmail}

リファレンスサイトの実装では、サンプルユーザーがフォームに入力して送信する際に電子メールを送信する必要があります。 Day CQ Mail Service を設定すると、SMTP サービスの詳細を指定して、顧客に自動メールを送信できます。 詳しくは、 [電子メール通知の設定](/help/sites-administering/notification.md).

パブリッシュインスタンスでメールサービスを設定するには、次の手順を実行します。

1. OSGi 設定 (https://&lt;) に移動します。*hostname>*:&lt;*ポート >*/system/console/configMgr.
1. 検索とタップ **[!UICONTROL Day CQ Mail Service]** をクリックして、設定用に開きます。
1. SMTP サーバーのホスト名とポートの値を指定します。
1. 「**[!UICONTROL 保存]**」をタップします。

>[!NOTE]
>
>会社の SMTP サービスや Gmail などのパブリックサービスを使用できます。 SMTP サービスの設定については、 SMTP サービスのドキュメントを参照してください。

## デフォルトの XSS 設定を上書き {#xss}

We.Finance リファレンスサイトの電子メールテンプレートには、電子メール内にパーソナライズされたリンクが含まれています。 これらのリンクには、プレースホルダーが `${placeholder}`. これらのプレースホルダーは、電子メールを送信する前に実際の値に置き換えられます。 AEMのデフォルトの XSS 保護設定では中括弧 (**{ }**) をHTMLコンテンツ内の URL に追加します。 ただし、パブリッシュインスタンスで次の手順を実行することで、デフォルトの設定を上書きできます。

1. `/libs/cq/xssprotection/config.xml` を `/apps/cq/xssprotection/config.xml` にコピーします。
1. `/apps/cq/xssprotection/config.xml` を開きます。
1. 内 `common-regexps` セクションで、 `onsiteURL` 次のように入力し、ファイルを保存します。

   `<regexp name="onsiteURL" value="([\p{L}\p{N}\\\.\#@\$\{\}%\+&;\-_~,\?=/!\*\(\)]*|\#(\w)+)"/>`

>[!NOTE]
>
>中括弧 (**{ }**) は、受け入れ可能な文字としてHTMLコンテンツの URL に含まれます。

SMTP サーバーを設定したら、Sarah Rose のペルソナを使用してフォームに入力し、下書きとして保存します。 ドラフトとして保存すると、電子メールを使用してドラフトを受け取るオプションが表示されます。 次をタップしたとき： **メールの送信** ボタンをクリックすると、アプリケーションの下書きへのリンクが記載された電子メールが届き、電子メールの設定に成功します。 Sarah の資格情報を使用してログインし、下書きを表示していることを確認します。

## AEM DS の設定 {#aemds}

リファレンスサイトの使用例では、電子メール通信用のパブリッシュインスタンスにAEM DS サービスの設定が必要です。 パブリッシュインスタンスでAEM DS サービスを設定する詳細な手順については、 [AEM DS の設定](/help/forms/using/configuring-the-processing-server-url-.md).

AEM Formsリファレンスサイトの場合、AEM DS Settings Service で、処理サーバーの URL ではなく、パブリッシュサーバーの URL を指定します。

>[!CAUTION]
>
>入れない `/lc` (AEM Forms OSGi 用に設定する場合 )

## リファレンスサイトパッケージのデプロイ {#refsite}

ソフトウェア配布を使用して、次のリファレンスサイトパッケージをインストールします。

* [AEM-FORMS-6.4-FSI-REF-SITE](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq640/fd/AEM-FORMS-6.4-FSI-REF-SITE)
* [AEM-FORMS-6.4-GOV-REF-SITE](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq640/fd/AEM-FORMS-6.4-GOV-REF-SITE)

パッケージの使用方法について詳しくは、 [パッケージの操作方法](/help/sites-administering/package-manager.md).

パッケージをインストールし、オーサーインスタンスとパブリッシュインスタンスを起動したら、ブラウザーで次の URL にアクセスします。

* `https://[server]:[port]/wegov`
* `https://[server]:[port]/wefinance`

インストールに成功した場合は、We.Gov および We.Finance のリファレンスサイトのランディングページにアクセスできます。

## （オプション）サンプルデータをMicrosoft Dynamics にインポートする {#optional-import-sample-data-into-microsoft-dynamics}

住宅ローン申し込みと自動保険申し込みリファレンスサイトは、Microsoft Dynamics のレコードを使用するように設定されています。 リファレンスサイトパッケージでは、カスタムエンティティとサンプルレコードがインストールされ、Microsoft Dynamics に読み込んでリファレンスサイトを実行することができます。 サンプルデータを移行して設定するには、次の手順を実行します。

自動保険申込用のカスタムエンティティをインポートする手順は、次のとおりです。

1. をダウンロードします。 **WeFinanceAutoInsurance_1_0.zip** ソリューションパッケージ `https://[server]:[port]/content/aemforms-refsite-collaterals/we-finance/auto-insurance/ms-dynamics/WeFinanceAutoInsurance_1_0.zip` をAEMオーサーインスタンスで使用します。
1. Microsoft Dynamics インスタンスで、に移動します。 **[!UICONTROL ソリューション]** 内 **[!UICONTROL 設定]** メニューとクリック **[!UICONTROL インポート]**. パッケージを選択してインポートします。

自動保険申込用のカスタムエンティティをインポートする手順は、次のとおりです。

1. をダウンロードします。 **AEMFormsFSIRefsite_1_0.zip** https://からのパッケージ[作成者]:[ポート]/content/aemforms-refsite-collaterals/we-finance/home-mortgage/ms-dynamics/AEMFormsFSIRefsite_1_0.zip. パッケージを選択してインポートします。

1. Microsoft Dynamics インスタンスで、に移動します。 **[!UICONTROL ソリューション]** 内 **[!UICONTROL 設定]** メニューとクリック **[!UICONTROL インポート]**. パッケージを選択してインポートします。

顧客および保険証券レコードをインポートする手順は、次のとおりです。

1. をダウンロードします。 **We.Finance Customers.csv, We.Finance Auto Insurance Renewals.csv**、および **住宅ローン** AEMオーサーインスタンス上の次の場所にあるデータファイル：

   * `https://[server]:[port/content/aemforms-refsite-collaterals/we-finance/auto-insurance/ms-dynamics/We.Finance Customers.csv`
   * `https://[server]:[port/content/aemforms-refsite-collaterals/we-finance/auto-insurance/ms-dynamics/We.Finance Auto Insurance Renewals.csv`
   * `https://[server]:[port]/content/aemforms-refsite-collaterals/we-finance/home-mortgage/ms-dynamics/Sarah%20Rose%20Contact.csv`

1. Microsoft Dynamics インスタンスで、以下の操作を実行します。

   * に移動します。 **[!UICONTROL セールス/We.Finance のお客様]** をクリックし、 **[!UICONTROL インポート]**.
   * に移動します。 **[!UICONTROL 営業 > We.Finance 自動保険]** をクリックし、 **[!UICONTROL インポート]**.
   * に移動します。 **[!UICONTROL セールス > We.Finance 社の住宅ローン]**  をクリックし、 **[!UICONTROL インポート]**.

## Microsoft Dynamics の OAuth クラウドサービスを設定する {#configure-oauth-cloud-service-for-microsoft-dynamics}

AEM FormsとMicrosoft Dynamics 間の通信を有効にするように、AEM Formsで OAuth クラウドサービスを設定します。 AEMオーサーインスタンスとパブリッシュインスタンスで OAuthCloud Serviceを設定するには、次の手順を実行します。

1. AEMオーサーインスタンスで、に移動します。 **[!UICONTROL ツール/Cloud Services/データソース/グローバル]**. タップ **[!UICONTROL リファレンスサイトの Dynamics 統合]** アイコンとタップ **[!UICONTROL プロパティ]**.
1. Microsoft Azure Active Directory アカウントに移動します。 コピーしたクラウドサービス設定 URL を **[!UICONTROL 返信 URL]** の設定を登録します。 設定を保存します。
1. 「認証設定」タブで、次の情報を指定します。 **[!UICONTROL サービスルート]**, **[!UICONTROL クライアント ID]**, **[!UICONTROL クライアント秘密鍵]**、および **[!UICONTROL リソース URL]** (Microsoft Dynamics インスタンス用 ) クリック **[!UICONTROL OAuth に接続]** Microsoft Dynamics のログインページにリダイレクトされる
1. ログイン資格情報を入力します。 ログインすると、AEM Forms Cloud Service 設定ページにリダイレクトされます。 「**[!UICONTROL 保存して閉じる]**」をクリックします。クラウドサービスの設定が保存されます。
1. に移動します。 **[!UICONTROL Forms /データ統合/ We.Finance]**. [ 自動保険 (Dynamics)] を選択し、[ 編集 ] をクリックします。 Microsoft Dynamics エンティティは、「データソース」タブに表示されます。 すべてのエンティティがMicrosoft Dynamics から取得され、「データソース」タブに表示されるまで待ちます。
1. を選択します。 **[!UICONTROL AutoInsuranceRenewal エンティティ]** をクリックし、 **[!UICONTROL モデルオブジェクトのテスト]**. 入力リクエストセクションで、顧客 ID の値を「900001」と指定し、 **[!UICONTROL テスト]**. 「出力」セクションには、顧客 ID 900001のMicrosoft Dynamics から取得したレコードが表示されます。
1. 入力リクエストセクションで、顧客 ID の値を「900001」と指定し、 **[!UICONTROL テスト]**. 「出力」セクションには、顧客 ID 900001のMicrosoft Dynamics から取得したレコードが表示されます。
1. パブリッシュインスタンスで手順 1～6 を繰り返します。

## Acrobat Sign Scheduler の設定 {#scheduler}

オーサーインスタンスとパブリッシュインスタンスの両方で、以下の操作を実行します。

1. AEM Web Configuration コンソール ( ) に移動します。 `https://[server]:[host]/system/console/configMgr`.
1. 検索とタップ **[!UICONTROL Acrobat Sign Configuration Service]** をクリックして、設定用に開きます。
1. 設定 **[!UICONTROL ステータス更新スケジューラの式]** as **0 0/2 &amp;ast;&amp;ast;&amp;ast;?**.

   >[!NOTE]
   >
   >上記のスケジューラー設定は、2 分ごとにAcrobat Signサービスのステータスを確認します。

1. 「**[!UICONTROL 保存]**」をタップします。

## リファレンスサイトのAcrobat Sign Cloud Service の設定 {#sign-service}

オーサーインスタンスとパブリッシュインスタンスの両方で、以下の操作を実行します。

1. に移動します。 **[!UICONTROL ツール/Cloud Services/ Acrobat Sign /グローバル]**. 選択 **[!UICONTROL AEM Formsリファレンスサイトの署名]** とタップします。 **[!UICONTROL プロパティ]**.

   >[!CAUTION]
   >
   >https://[ホスト]:[ssl_port]/mnt/overlay/adobesign/cloudservices/adobesign/properties.html URL が、Acrobat Sign API アプリケーションの OAuth 設定のリダイレクト URL リストに追加されます。

1. クライアント ID とAcrobat Signアプリケーション OAuth 設定の秘密鍵を指定します。
1. （オプション） **[!UICONTROL 添付ファイルにAcrobat Signも有効にする]** オプションを選択し、をタップします。 **[!UICONTROL Acrobat Signに接続]**. アダプティブフォームに添付されたファイルが、署名用に送信された対応するAcrobat Signドキュメントに追加されます。
1. タップ **[!UICONTROL Acrobat Signに接続]** Acrobat Signの資格情報を使用してログインします。

## Forms Common Configuration Service の設定 {#anonymous}

匿名ユーザーに対するアクセスを許可するには、パブリッシュインスタンスで次の操作を実行します。

1. AEM Web Configuration コンソール ( ) に移動します。 `https://[server]:[port]/system/console/configMgr`.
1. 検索とタップ **[!UICONTROL Forms Common Configuration Service]** をクリックして、設定用に開きます。
1. の設定 **[!UICONTROL 許可]** ～のフィールド **[!UICONTROL すべてのユーザー]**.
1. 「**[!UICONTROL 保存]**」をタップします。

## フォームデータモデルの Rest サービスを変更 {#fdm}

オーサーインスタンスとパブリッシュインスタンスの両方で、以下の操作を実行します。

1. CRXDE( ) に移動します。 `https://[server]:[port]/crx/de/index.jsp`.
1. に移動します。 **/conf/global/settings/cloudconfigs/fdm/roi-rest/jcr:content/swaggerFile** swagger ファイルを開きます。
1. 環境に応じて、ホストとポートの設定を更新します。
1. 設定を保存します。
1. (**オーサーインスタンスのみ**) に移動します。 **[!UICONTROL ツール]** > **[!UICONTROL Cloud Services]** > **[!UICONTROL データソース]** > **[!UICONTROL global]**. 選択 **[!UICONTROL roi-rest]** とタップします。 **[!UICONTROL プロパティ]**. タップ **[!UICONTROL 認証設定]** および設定 **[!UICONTROL 認証タイプ]** から **[!UICONTROL 基本認証]**. 指定 `admin`/ `admin`サービスにアクセスするためのユーザー名/パスワード。 **[!UICONTROL 保存して閉じる]**&#x200B;をタップします。

## Marketing Cloudとの統合 {#integrate-with-marketing-cloud}

AEM FormsをAdobe AnalyticsおよびAdobe Targetと統合できます。 Adobe Analyticsはアダプティブフォームのレポートを生成し、パフォーマンスを分析するのに役立ちますが、Adobe Targetは、パーソナライズされたエクスペリエンスを提供し、アダプティブフォームの A/B テストを実行するのに役立ちます。

AEM FormsでAdobe AnalyticsとAdobe Targetを設定するには、以下の手順を実行します。

### Adobe Analytics の設定 {#configure-adobe-analytics}

AEM FormsとAdobe Analyticsの統合により、顧客がフォームやドキュメントとどのようにやり取りするかを監視および分析できます。 問題のある領域を特定して修正し、コンバージョン率を上げるための対策を行うのに役立ちます。

この機能をリファレンスサイトで使用するには、 [分析とレポートの設定](/help/forms/using/configure-analytics-forms-documents.md).

レポートを生成するために、シードデータはリファレンスサイトにバンドルされます。 シードデータを使用する前に、次の手順を実行します。

1. We.Finance と We.Gov の分析設定が AEM Cloud Services で使用可能であることを確認します。 クラウドサービスは、次のいずれかの方法で検索できます。

   * に移動します。 **[!UICONTROL ツール/Cloud Services/レガシーCloud Services]** またはhttps://を参照します。&lt;host>:&lt;port>/libs/cq/core/content/tools/cloudservices.html.
   * 内 **[!UICONTROL Cloud Services]** ページ、下 **[!UICONTROL Adobe Analytics]** セクションで、 `Show Configurations`. We.Finance と We.Gov の設定を確認できます。 「 」をクリックして、設定を開きます。 設定ページで、 **[!UICONTROL 編集]**. 有効な会社名、ユーザー名、共有暗号鍵（パスワード）およびデータセンターを入力し、 **[!UICONTROL Analytics に接続]**. 接続に成功したダイアログが表示されたら、「 **[!UICONTROL OK]** をクリックします。 Analytics 設定の下でフレームワークを設定します。詳しくは、 [Analytics とレポートの設定](/help/forms/using/configure-analytics-forms-documents.md).

1. https://&lt; に移動します。*ホスト*>:&lt;*ポート*>/system/console/configMgr を開き、以下の手順を実行します。

   * 内 **[!UICONTROL Web コンソール設定]** ページを検索してクリック **[!UICONTROL AEM Forms Analytics 設定]**.
   * 内 **[!UICONTROL SiteCatalyst]** 「 AEM Forms Analytics 設定」ダイアログの「 we-finance (we-finance) 」または「 we-gov (we-gov) 」を選択します。
   * クリック **[!UICONTROL 保存]** ページを更新します。

1. https://で Forms Manager に移動します。&lt;host>:&lt;port>/aem/forms を実行し、次の操作を行います。

   * We.Finance フォルダーまたは We.Gov フォルダーを開き、レポートを表示するフォームを選択します。
   * アクションツールバーの「 Analytics を有効にする」をクリックします。 フォームの分析を有効にしたら、「分析レポート」をクリックします。 空のレポートが生成されているのを確認できます。 空のレポートが生成されたら、デモ用の分析レポートを生成するために、リファレンスサイトパッケージに含まれているシードデータを指定する必要があります。

   リファレンスサイトは、クレジットカード、住宅ローン、チャイルドサポートの使用例に関するシードデータを使用して分析レポートを提供します。 シードデータの設定については、 [We.Finance リファレンスサイトのチュートリアル](/help/forms/using/finance-reference-site-walkthrough.md) および [We.Gov リファレンスサイトのチュートリアル](/help/forms/using/gov-reference-site-walkthrough.md).

### Target の設定 {#configure-target}

リファレンスサイトでは、アダプティブドキュメントにターゲットを絞り込んでパーソナライズしたコンテンツを含めることができる、AEM FormsとAdobe Targetの統合を紹介しています。 また、アダプティブフォームの A/B テストを作成することもできます。

リファレンスサイトで統合を体験するには、次の手順を実行してAEMで Target を設定します。

1. jvm 引数でオーサークイックスタートを開始します。 `-Dabtesting.enabled=true` ：サーバー上で A/B テストを有効にします。

   **注意**:AEMインスタンスが JBoss 上で動作していて、自動インストールからサービスとして開始される場合は、 `-Dabtesting.enabled=true` パラメーターを `jboss\bin\standalone.conf.bat` ファイル：

   `set "JAVA_OPTS=%JAVA_OPTS% -Dadobeidp.serverName=server1 -Dfile.encoding=utf8 -Djava.net.preferIPv4Stack=true -Dabtesting.enabled=true"`

1. https://&lt; にアクセス&#x200B;*hostname*>:&lt;*ポート*>/libs/cq/core/content/tools/cloudservices.html.

1. 内 **[!UICONTROL Adobe Target]** セクションで、 **[!UICONTROL 設定を表示]**. We.Finance Target の設定を確認できます。 「 」をクリックして、設定を開きます。 設定ページで、 **[!UICONTROL 編集]**. この **[!UICONTROL コンポーネントを編集]** ダイアログが開きます。

1. Target アカウントに関連付けるクライアントコード、電子メール、パスワードを指定します。 API タイプをとして選択します。 **[!UICONTROL REST]**.
1. クリック **[!UICONTROL Adobeターゲットに接続]**. Target アカウントが正常に設定されたら、「 **[!UICONTROL OK]**. パッケージ化された設定に Target フレームワークが含まれていることを確認できます。

1. https://&lt;*hostname*>:&lt;*port*>/system/console/configMgr にアクセスします。

1. クリック **[!UICONTROL AEM Forms Target 設定]**.
1. Target フレームワークを選択します。
1. 内 **[!UICONTROL ターゲット URL]** フィールドに、AEM Formsへの URL を指定します。 例：https://&lt;*hostname*>:&lt;*ポート*>.

1. 「**[!UICONTROL 保存]**」をクリックします。

クレジットカード申し込みと住宅ローン申し込みの使用例では、A/B テストを実行し、デモ用にレポートを表示する方法を示しています。 手順については、 [We.Finance リファレンスサイトのチュートリアル](/help/forms/using/finance-reference-site-walkthrough.md).

## 次の手順 {#next-step}

これで、 リファレンスサイトを利用するための設定がすべて完了しました。リファレンスサイトのワークフローと手順について詳しくは、次を参照してください。

* [We.Finance リファレンスサイトのチュートリアル](/help/forms/using/finance-reference-site-walkthrough.md)
* [We.Gov リファレンスサイトのチュートリアル](/help/forms/using/gov-reference-site-walkthrough.md)

* [従業員セルフサービスリファレンスサイトのチュートリアル](/help/forms/using/employee-self-service-reference-site.md)
