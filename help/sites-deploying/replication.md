---
title: レプリケーション
seo-title: Replication
description: AEMでレプリケーションエージェントを設定および監視する方法について説明します。
seo-description: Learn how to configure and monitor replication agents in AEM.
uuid: 0e4fa6be-2e94-42c7-9cc2-516495e48deb
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.4/SITES
content-type: reference
topic-tags: configuring
discoiquuid: 6fe1c5c5-deb7-4405-82e4-23e0f90e2bd8
feature: Configuring
exl-id: b4a56f59-dc5e-40c3-a024-ee9df10949d8
source-git-commit: c5b816d74c6f02f85476d16868844f39b4c47996
workflow-type: tm+mt
source-wordcount: '3613'
ht-degree: 40%

---

# レプリケーション{#replication}

>[!CAUTION]
>
>AEM 6.4 の拡張サポートは終了し、このドキュメントは更新されなくなりました。 詳細は、 [技術サポート期間](https://helpx.adobe.com/jp/support/programs/eol-matrix.html). サポートされているバージョンを見つける [ここ](https://experienceleague.adobe.com/docs/?lang=ja).

レプリケーションエージェントは、次の目的で使用されるメカニズムとしてAdobe Experience Manager(AEM) の中心となるものです。

* [公開（アクティベート）](/help/sites-authoring/publishing-pages.md#publishing-pages) オーサー環境からパブリッシュ環境にコンテンツを書き込むことができます。
* Dispatcher キャッシュからコンテンツを明示的にフラッシュします。
* パブリッシュ環境からオーサー環境（オーサー環境の制御下）にユーザー入力（フォーム入力など）を返します。

リクエストは [キュー](/help/sites-deploying/osgi-configuration-settings.md) を適切なエージェントに追加して処理します。

>[!NOTE]
>
>ユーザーデータ（ユーザー、ユーザーグループ、ユーザープロファイル）は、オーサーインスタンスとパブリッシュインスタンスの間でレプリケートされません。
>
>複数のパブリッシュインスタンスの場合、ユーザーデータは次の場合に Sling を配布 [ユーザーの同期](/help/sites-administering/sync.md) が有効になっている。

## オーサーからパブリッシュにレプリケート中 {#replicating-from-author-to-publish}

パブリッシュインスタンスまたは Dispatcher へのレプリケーションは、次の手順でおこなわれます。

* 作成者が、特定のコンテンツの公開（アクティベート）をリクエストするこれは、手動のリクエストまたは事前設定された自動トリガーで開始できます。
* リクエストは、適切なデフォルトレプリケーションエージェントに渡されます。1 つの環境に複数のデフォルトエージェントを設定でき、これらのアクションでは常に選択されます。
* レプリケーションエージェントは、コンテンツを「パッケージ化」し、レプリケーションキューに配置します。
* 「Web サイト」タブで、 [色付きステータスインジケーター](/help/sites-authoring/publishing-pages.md#determining-publication-status) は個々のページに対して設定されます。
* コンテンツはキューから取り除かれ、設定されたプロトコルを使用してパブリッシュ環境に転送されます。通常、これは HTTP です。
* パブリッシュ環境内のサーブレットが要求を受信し、受信したコンテンツを公開します。デフォルトのサーブレットは `http://localhost:4503/bin/receive` です。

* 複数のオーサー環境とパブリッシュ環境を設定できます。

![chlimage_1-144](assets/chlimage_1-144.png)

## パブリッシュからオーサーにレプリケート中 {#replicating-from-publish-to-author}

一部の機能では、ユーザーはパブリッシュインスタンスでデータを入力できます。

場合によっては、このデータをオーサー環境に返し、そこから他のパブリッシュ環境に再配布するために、リバースレプリケーションと呼ばれる一種のレプリケーションが必要になることがあります。 セキュリティ上の問題を考慮し、パブリッシュ環境からオーサー環境へのトラフィックは厳密に制御する必要があります。

リバースレプリケーションでは、オーサー環境を参照するパブリッシュ環境のエージェントを使用します。 このエージェントは、データをアウトボックスに配置します。 このアウトボックスは、オーサー環境のレプリケーションリスナーと一致します。 リスナーはアウトボックスをポーリングして入力されたデータを収集し、必要に応じて配布します。 これにより、オーサー環境がすべてのトラフィックを制御できます。

コミュニティ機能（フォーラム、ブログ、コメント、レビューなど）の場合、レプリケーションを使用してAEMインスタンス間で効率的に同期する際に、パブリッシュ環境に入力されるユーザー生成コンテンツ (UGC) の量が少なくなりません。

AEM [Communities](/help/communities/overview.md) では、UGC にレプリケーションを使用しません。その代わりに、Communities のデプロイメントでは UGC 用の共通ストアが必要になります（[コミュニティコンテンツのストレージ](/help/communities/working-with-srp.md)を参照）。

## レプリケーション（デフォルト） {#replication-out-of-the-box}

AEMの標準インストールに含まれるGeometrixxWeb サイトを使用して、レプリケーションを説明できます。

この例に従ってデフォルトのレプリケーションエージェントを使用するには、次の環境を使用して [AEM をインストール](/help/sites-deploying/deploy.md)する必要があります。

* オーサー環境（ポート `4502`）
* パブリッシュ環境（ポート `4503`）

>[!NOTE]
>
>デフォルトで有効 :
>
>* 作成者のエージェント：デフォルトエージェント (publish)
>
>デフォルトで有効に無効になっています (AEM 6.1 以降 )。
>
>* オーサー環境のエージェント：リバースレプリケーションエージェント（publish_reverse）
>* パブリッシュ環境のエージェント：リバースレプリケーション（outbox）
>
>エージェントまたはキューのステータスを確認するには、**ツール**&#x200B;コンソールを使用します。\
>[レプリケーションエージェントの監視](#monitoring-your-replication-agents)を参照してください。

### レプリケーション（オーサー環境からパブリッシュ環境へ） {#replication-author-to-publish}

1. オーサー環境でサポートページに移動します。

   `http://localhost:4502/content/geometrixx/en/support.html`

1. ページを編集して新しいテキストを追加します。
1. **ページをアクティベート** 変更を公開する場合。
1. パブリッシュ環境でサポートページを開きます。

   `http://localhost:4503/content/geometrixx/en/support.html`

1. 作成者に入力した変更を表示できます。

このレプリケーションは、次の方法でオーサー環境から実行されます。

* **デフォルトエージェント (publish)**
このエージェントは、デフォルトのパブリッシュインスタンスにコンテンツをレプリケートします。

   この詳細（設定とログ）は、オーサー環境のツールコンソールからアクセスできます。または

   `http://localhost:4502/etc/replication/agents.author/publish.html`。

### レプリケーションエージェント — 標準 {#replication-agents-out-of-the-box}

標準のAEMインストールでは、次のエージェントを使用できます。

* [デフォルトエージェント](#replication-author-to-publish)  — オーサーからパブリッシュへのレプリケーションに使用します。

* Dispatcher フラッシュ — Dispatcher キャッシュの管理に使用されます。詳しくは、 [オーサリング環境からの Dispatcher キャッシュの無効化](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/page-invalidate.html?lang=ja#invalidating-dispatcher-cache-from-the-authoring-environment) および [パブリッシュインスタンスからの Dispatcher キャッシュの無効化](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/page-invalidate.html?lang=ja#invalidating-dispatcher-cache-from-a-publishing-instance) を参照してください。

* [リバースレプリケーション](#replicating-from-publish-to-author)  — パブリッシュからオーサーへのレプリケーションに使用します。 リバースレプリケーションは、フォーラム、ブログ、コメントなどのコミュニティ機能には使用されません。アウトボックスが有効化されていないので、事実上、この機能は無効になっています。リバースレプリケーションを使用するには、カスタム設定が必要になります。

* 静的エージェント — 「ノードの静的表現をファイルシステムに保存するエージェント」です。 例えば、デフォルト設定では、コンテンツページと DAM アセットが `/tmp` に HTML または適切なアセット形式として格納されます。設定については、`Settings` タブと `Rules` タブを参照してください。これは、ページがアプリケーションサーバーから直接要求される場合に、コンテンツを確認できるようにするためのエージェントです。これは特殊なエージェントであり、（おそらく）ほとんどのインスタンスでは必要ありません。

## レプリケーションエージェント — 設定パラメーター {#replication-agents-configuration-parameters}

ツールコンソールからレプリケーションエージェントを設定する場合、ダイアログ内に次の 4 つのタブが表示されます。

### 設定 {#settings}

* **名前**

   レプリケーションエージェントの一意の名前。

* **説明**

   このレプリケーションエージェントが提供する目的の説明。

* **Enabled**

   レプリケーションエージェントが現在有効かどうかを示します。

   エージェントが **有効** キューは次のように表示されます。

   * **アクティブ**：項目が処理されています。
   * **待機中**：キューが空です。
   * **ブロック**：項目がキュー内にありますが、処理できません。例えば、受信側のキューが無効な場合などです。

* **シリアル化の種類**

   シリアル化の種類：

   * **デフォルト**:エージェントを自動的に選択する場合は、を設定します。
   * **Dispatcher フラッシュ**:エージェントを使用して Dispatcher キャッシュをフラッシュする場合に選択します。

* **再試行遅延**

   問題が発生した場合の、2 回の再試行の間の遅延（ミリ秒単位の待機時間）。

   デフォルト: `60000`

* **エージェントユーザー ID**

   環境に応じて、エージェントはこのユーザーアカウントを使用して次の操作を行います。

   * オーサー環境からコンテンツを収集し、パッケージ化します。
   * パブリッシュ環境でのコンテンツの作成と書き込み

   システムユーザーアカウント（sling で管理者ユーザーとして定義したアカウント。デフォルトでは、`admin` です）を使用するには、このフィールドを空白のままにします。

   >[!CAUTION]
   >
   >オーサー環境におけるエージェントの場合、このアカウントには、レプリケーションしたすべてのパスに対する読み取りアクセス権が必要です&#x200B;*。*

   >[!CAUTION]
   >
   >*パブリッシュ環境におけるエージェントの場合、このアカウントでコンテンツをレプリケーションするには、作成／書き込みアクセス権が必要です。*

   >[!NOTE]
   >
   >これは、レプリケーション用に特定のコンテンツを選択するメカニズムとして使用できます。

* **ログレベル**

   ログメッセージに使用する詳細レベルを指定します。

   * `Error`：エラーだけがログに記録されます。
   * `Info`：エラー、警告およびその他の情報メッセージがログに記録されます。
   * `Debug`：主にデバッグを目的として、高いレベルの詳細がメッセージで使用されます。

   デフォルト: `Info`

* **リバースレプリケーションに使用**

   このエージェントをリバースレプリケーションに使用するかどうかを示します。パブリッシュ環境からオーサー環境にユーザー入力を返します。

* **エイリアスの更新**

   このオプションを選択すると、Dispatcher に対するエイリアスまたはバニティーパスの無効化要求が有効になります。 [Dispatcher フラッシュエージェントの設定](/help/sites-deploying/replication.md#configuring-a-dispatcher-flush-agent) も参照してください。

### トランスポート {#transport}

* **URI**

   ターゲットの場所にある受信サーブレットを指定します。 特に、ここでターゲットインスタンスのホスト名（またはエイリアス）とコンテキストパスを指定できます。

   次に例を示します。

   * デフォルトエージェントによるレプリケーション先：`http://localhost:4503/bin/receive`
   * Dispatcher フラッシュエージェントによるレプリケーション先：`http://localhost:8000/dispatcher/invalidate.cache`

   ここで指定するプロトコル（HTTP または HTTPS）によってトランスポート方法が決まります。

   Dispatcher フラッシュエージェントの場合、「URI」プロパティは、パスに基づく virtualhost エントリを使用してファームを区別する場合にのみ使用されます。このフィールドを使用して、無効にするファームをターゲット設定してください。例えば、ファーム #1 の仮想ホストは `www.mysite.com/path1/*` で、ファーム #2 の仮想ホストは `www.mysite.com/path2/*` です。この場合、`/path1/invalidate.cache` の URL を使用して最初のファームをターゲット設定し、`/path2/invalidate.cache` を使用して 2 つ目のファームをターゲット設定できます。

* **ユーザー**

   ターゲットへのアクセスに使用するアカウントのユーザー名。

* **パスワード**

   ターゲットへのアクセスに使用するアカウントのパスワード。

* **NTLM ドメイン**

   NTML 認証用のドメイン。

* **NTLM ホスト**

   NTML 認証用のホスト。

* **緩和された SSL を有効にする**

   自己証明 SSL 証明書を受け入れる場合は、有効にします。

* **期限切れの証明書を許可する**

   有効期限切れの SSL 証明書を受け入れる場合に有効にします。

### プロキシ {#proxy}

次の設定は、プロキシが必要な場合にのみ必要です。

* **プロキシホスト**

   トランスポートに使用するプロキシのホスト名。

* **プロキシポート**

   プロキシのポート。

* **プロキシユーザー**

   使用するアカウントのユーザー名。

* **プロキシパスワード**

   使用するアカウントのパスワード。

* **プロキシ NTLM ドメイン**

   プロキシ NTLM ドメイン。

* **プロキシ NTLM ホスト**

   プロキシ NTLM ドメイン。

### 拡張 {#extended}

* **インターフェイス**

   ここで、バインド先のソケットインターフェイスを定義できます。

   接続の作成時に使用するローカルアドレスを設定します。 これを設定しない場合は、デフォルトのアドレスが使用されます。 これは、マルチホームシステムまたはクラスターシステムで使用するインターフェイスを指定する場合に便利です。

* **HTTP メソッド**

   使用する HTTP メソッド。

   Dispatcher フラッシュエージェントの場合、これはほとんど常にGETで、変更しないでください (POSTも可能な値です )。

* **HTTP ヘッダー**

   これらは Dispatcher フラッシュエージェントに使用され、フラッシュする必要のある要素を指定します。

   Dispatcher フラッシュエージェントの場合、次の 3 つの標準エントリを変更する必要はありません。

   * `CQ-Action:{action}`
   * `CQ-Handle:{path}`
   * `CQ-Path:{path}`

   必要に応じて、ハンドルまたはパスのフラッシュ時に使用するアクションを示すために使用します。 サブパラメーターは動的です。

   * `{action}` はレプリケーションアクションを示します
   * `{path}` はパスを示します

   これらは、リクエストに関連するパス/アクションで置き換えられるので、「ハードコード」する必要はありません。

   >[!NOTE]
   >
   >推奨されるデフォルトのコンテキスト以外のコンテキストにAEMをインストールした場合は、そのコンテキストを HTTP ヘッダーに登録する必要があります。 次に例を示します。
   >
   >`CQ-Handle:/<*yourContext*>{path}`

* **接続を閉じる**

   各要求の後で接続を閉じることを有効にします。

* **接続タイムアウト**

   接続を確立しようとした際に適用されるタイムアウト（ミリ秒）。

* **Socket Timeout**

   接続が確立された後にトラフィックを待機する際に適用されるタイムアウト（ミリ秒）。

* **プロトコルのバージョン**

   プロトコルのバージョンです。例えば、HTTP/ の場合は `1.0`1.0 です。

#### トリガー {#triggers}

次の設定は、自動レプリケーションのトリガーを定義するために使用します。

* **デフォルトを無視**

   オンにすると、エージェントはデフォルトのレプリケーションから除外されます。つまり、コンテンツ作成者がレプリケーションアクションを実行しても使用されません。

* **変更時**

   ここでは、ページが変更されたときに、このエージェントによるレプリケーションが自動的にトリガーされます。 これは主に Dispatcher フラッシュエージェントに使用されますが、リバースレプリケーションにも使用されます。

* **配布時**

   オンにすると、配布用にマークされたコンテンツが変更されたときに、エージェントが自動的に複製します。

* **オン/オフタイムに達しました**

   これにより、トリガーに対して定義されたオンタイムまたはオフタイムが発生した場合に、（ページを適切にアクティベートまたはアクティベート解除するために）自動レプリケーションが実行されます。 これは主に Dispatcher フラッシュエージェントで使用されます。

* **受信時**

   オンにすると、レプリケーションイベントを受け取るたびにエージェントがチェーンレプリケーションを行います。

* **ステータス更新がありません**

   オンにすると、エージェントはレプリケーションステータスの更新を強制しません。

* **バージョン管理がありません**

   オンにすると、エージェントはアクティベートされたページのバージョン管理を強制しません。

## レプリケーションエージェントの設定 {#configuring-your-replication-agents}

MSSL を使用してレプリケーションエージェントをパブリッシュインスタンスに接続する方法について詳しくは、 [相互 SSL を使用したレプリケーション](/help/sites-deploying/mssl-replication.md).

### オーサー環境からのレプリケーションエージェントの設定 {#configuring-your-replication-agents-from-the-author-environment}

オーサー環境の「ツール」タブで、オーサー環境 (**作成者のエージェント**) またはパブリッシュ環境 (**公開のエージェント**) をクリックします。 次の手順では、オーサー環境用のエージェントの設定を示しますが、両方に使用できます。

>[!NOTE]
>
>Dispatcher がオーサーインスタンスまたはパブリッシュインスタンスの HTTP 要求を処理する場合、レプリケーションエージェントからの HTTP 要求には PATH ヘッダーを含める必要があります。以下の手順に加えて、PATH ヘッダーをクライアントヘッダーの Dispatcher リストに追加する必要があります。( [/clientheaders （クライアントヘッダー）](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html?lang=ja-JP). [](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html?lang=ja-JP)

1. 次にアクセス： **ツール** 」タブをAEMでクリックします。
1. クリック **レプリケーション** （フォルダーを開くには左側のペイン）。
1. ダブルクリック **作成者のエージェント** （左または右のウィンドウ）。
1. 適切なエージェント名（リンク）をクリックして、そのエージェントの詳細情報を表示します。
1. クリック **編集** 設定ダイアログを開くには：

   ![chlimage_1-145](assets/chlimage_1-145.png)

1. デフォルトのインストールに適した値を指定する必要があります。値を変更したら、「**OK**」をクリックして値を保存します（個々のパラメーターについて詳しくは、[レプリケーションエージェント - 設定パラメーター](#replication-agents-configuration-parameters)を参照してください）。

>[!NOTE]
>
>AEM の標準インストールでは、`admin` をデフォルトのレプリケーションエージェント内のトランスポート資格情報のユーザーとして指定します。
>
>必要なパスをレプリケートする権限を持つサイト固有のレプリケーションユーザーアカウントに変更する必要があります。

### リバースレプリケーションの設定 {#configuring-reverse-replication}

リバースレプリケーションは、パブリッシュインスタンスで生成されたユーザーコンテンツをオーサーインスタンスに戻すために使用します。 これは、調査や登録フォームなどの機能で一般的に使用されます。

ほとんどのネットワークトポロジは、セキュリティ上の理由により、「非武装地帯（DMZ）」（インターネットなどの信頼できないネットワークに外部サービスを公開するサブネットワーク）からの接続を許可しません&#x200B;*。*

パブリッシュ環境は通常 DMZ にあるので、コンテンツをオーサー環境に戻すには、オーサーインスタンスから接続を開始する必要があります。 これは、次を使用しておこないます。

* コンテンツが配置されているパブリッシュ環境の&#x200B;*アウトボックス*
* オーサー環境のエージェント（パブリッシュ）。このエージェントは、アウトボックスを定期的にポーリングして新しいコンテンツを探します。

>[!NOTE]
>
>AEM [Communities](/help/communities/overview.md) では、パブリッシュインスタンス上のユーザー生成コンテンツにレプリケーションを使用しません。[コミュニティコンテンツのストレージ](/help/communities/working-with-srp.md)を参照してください。

そのためには、次のものが必要です。

**オーサー環境のリバースレプリケーションエージェント** これは、パブリッシュ環境のアウトボックスから情報を収集するアクティブなコンポーネントとして機能します。

リバースレプリケーションを使用する場合は、このエージェントをアクティベートします。

![chlimage_1-146](assets/chlimage_1-146.png)

**パブリッシュ環境（アウトボックス）のリバースレプリケーションエージェント** これは「アウトボックス」として機能する受動的な要素です。オーサー環境でエージェントが収集する場所から、ユーザー入力がここに配置されます。

![chlimage_1-9](assets/chlimage_1-9.jpeg)

### 複数のパブリッシュインスタンス用のレプリケーションの設定 {#configuring-replication-for-multiple-publish-instances}

>[!NOTE]
>
>コンテンツのみがレプリケートされます。ユーザーデータはレプリケートされません（ユーザー、ユーザーグループ、ユーザープロファイル）。
>
>複数のパブリッシュインスタンス間でユーザーデータを同期させるには、[ユーザーの同期](/help/sites-administering/sync.md)を有効化します。

インストール時に、localhost のポート 4503 で実行されているパブリッシュインスタンスに対するコンテンツのレプリケーション用のデフォルトエージェントが既に設定されています。

追加のパブリッシュインスタンス用にコンテンツのレプリケーションを設定するには、新しいレプリケーションエージェントを作成して設定する必要があります。

1. を開きます。 **ツール** 」タブをAEMでクリックします。
1. 選択 **レプリケーション**&#x200B;を、 **作成者のエージェント** をクリックします。
1. 選択 **新規…**.
1. を **タイトル** および **名前**&#x200B;を選択し、「 **レプリケーションエージェント**.
1. クリック **作成** 新しいエージェントを作成します。
1. 新しいエージェント項目をダブルクリックして、設定パネルを開きます。
1. クリック **編集** - **エージェント設定** ダイアログが開きます — **シリアル化の種類** は既にデフォルトとして定義されています。このままにしておく必要があります。

   * 内 **設定** タブ：

      * 有効化 **有効**.
      * を入力します。 **説明**.
      * 「**再試行遅延**」を `60000` に設定します。
      * **シリアル化のタイプ**&#x200B;は`Default`のままにします。
   * 「**トランスポート**」タブで、次のように設定します。

      * 新しいパブリッシュインスタンスに必要な URI を入力します。次に例を示します。 

         `http://localhost:4504/bin/receive`。

      * レプリケーションに使用するサイト固有のユーザーアカウントを入力します。
      * 必要に応じて、他のパラメーターを設定できます。


1. クリック **OK** 設定を保存します。

その後、オーサー環境でページを更新してから公開することで、操作をテストできます。

更新は、上記のように設定されたすべてのパブリッシュインスタンスに表示されます。

問題が発生した場合は、オーサーインスタンスでログを確認できます。必要な詳細レベルに応じて、前述の **エージェント設定** ダイアログを使用して、**ログレベル** を `Debug` に設定することもできます。

>[!NOTE]
>
>この設定を「[エージェントユーザー ID](#settings)」と一緒に使用すると、個々のパブリッシュ環境にレプリケーションする別のコンテンツを選択できます。それぞれのパブリッシュ環境に対して、次の手順を実行します。
>
>1. そのパブリッシュ環境にレプリケーションするレプリケーションエージェントを設定します。
>1. ユーザーアカウントを設定する特定のパブリッシュ環境にレプリケートされるコンテンツを読み取るのに必要なアクセス権を持つ。
>1. ユーザーアカウントを **エージェントユーザー ID** レプリケーションエージェント用。

>


### Dispatcher フラッシュエージェントの設定 {#configuring-a-dispatcher-flush-agent}

デフォルトのエージェントがインストールに含まれます。 ただし、設定は引き続き必要で、新しいエージェントを定義する場合も同様です。

1. を開きます。 **ツール** 」タブをAEMでクリックします。
1. クリック **導入**.
1. **レプリケーション**&#x200B;を選択した後、**パブリッシュ環境のエージェント**&#x200B;を選択してください。
1. をダブルクリックします。 **Dispatcher フラッシュ** 「 」項目をクリックして、概要を開きます。
1. クリック **編集** - **エージェント設定** ダイアログが開きます。

   * 内 **設定** タブ：

      * 有効化 **有効**.
      * を入力します。 **説明**.
      * **シリアル化のタイプ**&#x200B;を `Dispatcher Flush` のままにするか、またはエージェントを新規作成する場合に同様の設定を行います。
      * （オプション）**エイリアスの更新**&#x200B;を選択して、Dispatcher に対するエイリアスまたはバニティーパスの無効化要求を有効にします。
   * 「**トランスポート**」タブで、次のように設定します。

      * 新しいパブリッシュインスタンスに必要な URI を入力します。次に例を示します。 

         `http://localhost:80/dispatcher/invalidate.cache`。

      * レプリケーションに使用するサイト固有のユーザーアカウントを入力します。
      * 必要に応じて、他のパラメーターを設定できます。

   Dispatcher フラッシュエージェントの場合、「URI」プロパティは、パスに基づく virtualhost エントリを使用してファームを区別する場合にのみ使用されます。このフィールドを使用して、無効にするファームをターゲット設定してください。例えば、ファーム #1 の仮想ホストは `www.mysite.com/path1/*` で、ファーム #2 の仮想ホストは `www.mysite.com/path2/*` です。この場合、`/path1/invalidate.cache` の URL を使用して最初のファームをターゲット設定し、`/path2/invalidate.cache` を使用して 2 つ目のファームをターゲット設定できます。

   >[!NOTE]
   >
   >推奨されるデフォルトのコンテキスト以外のコンテキストに AEM をインストールした場合は、「[拡張](#extended)」タブで **HTTP ヘッダー**&#x200B;を設定する必要があります。

1. 「**OK**」をクリックして、変更を保存します。
1. に戻る **ツール** タブ、ここから、次の操作が可能です。 **有効化** の **Dispatcher フラッシュ** エージェント (**公開のエージェント**) をクリックします。

**Dispatcher フラッシュ**&#x200B;レプリケーションエージェントは、オーサーではアクティブではありません。同等の URI（例：`http://localhost:4503/etc/replication/agents.publish/flush.html`）を使用すると、パブリッシュ環境で同じページにアクセスできます。

### レプリケーションエージェントへのアクセスの制御 {#controlling-access-to-replication-agents}

`etc/replication` ノードに対するユーザーまたはグループのページの権限を使用して、レプリケーションエージェントの設定に使用するページへのアクセスを制御できます。

>[!NOTE]
>
>このような権限の設定は、例えば Web サイトコンソールやサイドキックのオプションからコンテンツをレプリケーションするユーザーには影響を及ぼしません。レプリケーションフレームワークでは、ページのレプリケーション時に、現在のユーザーの「ユーザーセッション」を使用してレプリケーションエージェントにアクセスしません。

### CRXDE Lite からのレプリケーションエージェントの設定 {#configuring-your-replication-agents-from-crxde-lite}

>[注意!]
>
>レプリケーションエージェントの作成は、`/etc/replication` リポジトリの場所でのみサポートされます。関連する ACL を正しく処理するには、これが必要です。ツリーの別の場所にレプリケーションエージェントを作成すると、不正アクセスにつながる可能性があります。

CRXDE Lite を使用して、レプリケーションエージェントの様々なパラメーターを設定できます。

`/etc/replication` に移動すると、次の 3 つのノードがあります。

* `agents.author`
* `agents.publish`
* `treeactivation`

2 つの `agents` は、適切な環境に関する設定情報を保持し、その環境が実行中の場合にのみアクティブになります。例えば、`agents.publish` は、パブリッシュ環境でのみ使用されます。次のスクリーンショットは、AEM WCM に含まれる、オーサー環境のパブリッシュエージェントを示しています。

![chlimage_1-147](assets/chlimage_1-147.png)

## レプリケーションエージェントの監視 {#monitoring-your-replication-agents}

レプリケーションエージェントを監視するには：

1. 次にアクセス： **ツール** 」タブをAEMでクリックします。
1. クリック **レプリケーション**.
1. 適切な環境のエージェントへのリンク（左または右のウィンドウ）をダブルクリックします。例： **作成者のエージェント**.

   表示されるウィンドウには、オーサー環境のすべてのレプリケーションエージェントの概要が表示されます。この概要には、ターゲットとステータスも含まれます。

1. 適切なエージェント名（リンク）をクリックすると、そのエージェントに関する詳細情報が表示されます。

   ![chlimage_1-10](assets/chlimage_1-10.jpeg)

   ここでは、以下のことができます。

   * エージェントが有効かどうかを確認します。
   * レプリケーションのターゲットを確認します。
   * レプリケーションキューが現在アクティブ（有効）かどうかを確認します。
   * キュー内に項目があるかどうかを確認します。
   * **更新** または **クリア** キュー・エントリの表示を更新するこれにより、キューに入って離れた項目を確認できます。
   * **ログを表示** をクリックして、レプリケーションエージェントによるアクションのログにアクセスします。
   * **接続をテスト** をターゲットインスタンスに追加します。
   * **再試行を強制** （必要に応じて、すべてのキュー項目）に対して実行します。

   >[!CAUTION]
   >
   >パブリッシュインスタンスのリバースレプリケーションアウトボックスには、「接続をテスト」リンクを使用しないでください。
   >
   >アウトボックスクエリ用にレプリケーションテストが実行されると、リバースレプリケーションのたびに、テストレプリケーションより古い項目がすべて再処理されます。
   >
   >そのような項目がキュー内に既に存在する場合は、次の XPath JCR クエリを使用して検索し、削除する必要があります。
   >
   >`/jcr:root/var/replication/outbox//*[@cq:repActionType='TEST']`

## バッチレプリケーション {#batch-replication}

バッチレプリケーションは、個々のページやアセットをレプリケートしませんが、時間やサイズに基づいて、2 つの最初のしきい値がトリガーされるのを待ちます。

次に、すべてのレプリケーション項目を 1 つのパッケージに圧縮し、単一のファイルとしてパブリッシャーにレプリケートします。

パブリッシャーは、すべての項目を展開し、保存して作成者に報告します。

### バッチレプリケーションの設定 {#configuring-batch-replication}

1. `http://serveraddress:serverport/siteadmin` に移動します。
1. 画面の上側にある&#x200B;**[!UICONTROL ツール]**&#x200B;アイコンを押します。
1. 左側のナビゲーションレールから、**[!UICONTROL レプリケーション - 作成者のエージェント]**&#x200B;に移動し、「**[!UICONTROL デフォルトエージェント]**」をダブルクリックします。
   * また、直接 `http://serveraddress:serverport/etc/replication/agents.author/publish.html` に移動して、デフォルトのパブリッシュレプリケーションエージェントに到達することもできます。
1. レプリケーションキューの上にある「**[!UICONTROL 編集]**」ボタンを押します。
1. 次のウィンドウで、「 **[!UICONTROL バッチ]**」タブに移動します。
   ![batchreplication](assets/batchreplication.png)
1. エージェントを設定します。

### パラメーター {#parameters}

* `[!UICONTROL Enable Batch Mode]` - バッチレプリケーションモードを有効または無効にします
* `[!UICONTROL Max Wait Time]` - バッチリクエストが開始されるまでの最大待機時間（秒単位）。デフォルト値は 2 秒です。
* `[!UICONTROL Trigger Size]` - このサイズの上限に達したときにバッチレプリケーションを開始します に到達した（MB 単位）。 デフォルトは 5MB です。

## その他のリソース {#additional-resources}

トラブルシューティングの詳細については、 [レプリケーションのトラブルシューティング](/help/sites-deploying/troubleshoot-rep.md) ページ。

詳しくは、Adobeにはレプリケーションに関する一連のナレッジベース記事があります。

[https://helpx.adobe.com/experience-manager/kb/ReplicationSiblingReordering.html](https://helpx.adobe.com/experience-manager/kb/ReplicationSiblingReordering.html)\
[https://helpx.adobe.com/experience-manager/kb/ReplicationFailureAfterNewIP.html](https://helpx.adobe.com/experience-manager/kb/ReplicationFailureAfterNewIP.html)\
[https://helpx.adobe.com/experience-manager/kb/LimitAccessToReplicationAgents.html](https://helpx.adobe.com/experience-manager/kb/LimitAccessToReplicationAgents.html)\
[https://helpx.adobe.com/experience-manager/kb/PagePermissionsNotReplicatedWithUser.html](https://helpx.adobe.com/experience-manager/kb/PagePermissionsNotReplicatedWithUser.html)\
[https://helpx.adobe.com/experience-manager/kb/HowToUseReverseReplication.html](https://helpx.adobe.com/experience-manager/kb/HowToUseReverseReplication.html)\
[https://helpx.adobe.com/experience-manager/kb/CQ5ReplicateToSpecificAgents.html](https://helpx.adobe.com/experience-manager/kb/CQ5ReplicateToSpecificAgents.html)\
[https://helpx.adobe.com/experience-manager/kb/ReplicationListener.html](https://helpx.adobe.com/experience-manager/kb/ReplicationListener.html)\
[https://helpx.adobe.com/experience-manager/kb/replication-stuck.html](https://helpx.adobe.com/experience-manager/kb/replication-stuck.html)\
[https://helpx.adobe.com/experience-manager/kb/replication-privileges-missing-after-upgrade-to-cq-5-5.html](https://helpx.adobe.com/experience-manager/kb/replication-privileges-missing-after-upgrade-to-cq-5-5.html)\
[https://helpx.adobe.com/experience-manager/kb/CQ53UnableToCreateJobQueueDueToMaxQueues.html](https://helpx.adobe.com/experience-manager/kb/CQ53UnableToCreateJobQueueDueToMaxQueues.html)\
[https://helpx.adobe.com/experience-manager/kb/ACLReplication.html](https://helpx.adobe.com/experience-manager/kb/ACLReplication.html)\
[https://helpx.adobe.com/experience-manager/kb/content-grow-due-reverse-replication.html](https://helpx.adobe.com/experience-manager/kb/content-grow-due-reverse-replication.html)\
[https://helpx.adobe.com/experience-manager/kb/ReplicationAgentUsingAnonUser.html](https://helpx.adobe.com/experience-manager/kb/ReplicationAgentUsingAnonUser.html)
