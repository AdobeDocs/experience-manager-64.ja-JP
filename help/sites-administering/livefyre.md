---
title: Livefyre との統合
seo-title: Integrating with Livefyre
description: Livefyre の業界最高レベルのキュレーション機能を AEM 6.4 と統合する方法を説明します。これにより、ソーシャルネットワークからの有用なユーザー生成コンテンツ（UGC）をサイトに数分で公開できます。
seo-description: Learn how to integrate and use Livefyre with AEM 6.4.
uuid: c355705d-6e0f-4a33-aa1f-d2d1c818aac0
contentOwner: ind14750
content-type: reference
topic-tags: integration
products: SG_EXPERIENCEMANAGER/6.4/SITES
discoiquuid: bb3fcb53-b8c3-4b1d-9125-4715f34ceb0b
exl-id: 39ecacda-2941-4b57-a001-e7ad1349723c
source-git-commit: bd94d3949f0117aa3e1c9f0e84f7293a5d6b03b4
workflow-type: tm+mt
source-wordcount: '1656'
ht-degree: 67%

---

# Livefyre との統合{#integrating-with-livefyre}

Livefyre の業界最高レベルのキュレーション機能を AEM 6.4 と統合する方法を説明します。これにより、ソーシャルネットワークからの有用なユーザー生成コンテンツ（UGC）をサイトに数分で公開できます。

## はじめに {#getting-started}

### AEM 用 Livefyre パッケージのインストール {#install-livefyre-package-for-aem}

AEM 6.4 には、Livefyre 機能パッケージ 1.2.6 がプリインストールされています。このパッケージには Livefyre の AEM Sites との統合のみが含まれているので、更新パッケージをインストールする前に、まずアンインストールする必要があります。最新のパッケージでは、Sites、Assets および Commerce を含む、Livefyre と AEM の完全な統合を利用できます。

>[!NOTE]
>
>AEM-LF パッケージの一部の機能は、ソーシャルコンポーネントフレームワーク（SCF）に依存しています。Livefyre 機能パックをコミュニティ以外のサイトの一部として使用している場合は、Web サイトのオーサー clientlibs に依存関係として *cq.social.scf* を宣言する必要があります。コミュニティ Web サイトの一部として LF 機能パックを使用している場合、この依存関係はすでに宣言されているはずです。

1. AEMホームページで、 **ツール** アイコンをクリックします。
1. に移動します。 **導入/パッケージ**.
1. パッケージマネージャーで、プリインストールされた Livefyre 機能パッケージが表示されるまでスクロールし、パッケージのタイトルをクリックします。 **cq-social-livefyre-pkg-1.2.6.zip** をクリックしてオプションを展開します。
1. クリック **その他 > アンインストール**.

   ![livefyre-aem-uninstall-64](assets/livefyre-aem-uninstall-64.png)

1. Livefyre パッケージのダウンロード元 [ソフトウェア配布](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html).

1. パッケージマネージャーで、ダウンロードしたパッケージをインストールします。 AEMでのソフトウェア配布およびパッケージの使用手順については、 [パッケージの操作方法](/help/sites-administering/package-manager.md).

   ![livefyre-aem4-6-4](assets/livefyre-aem4-6-4.png)

   Livefyre-AEM パッケージがインストールされます。統合機能を使い始める前に、Livefyre を使用するように AEM を設定する必要があります。

   機能パックの詳細およびリリースノートについては、 [機能パック](https://helpx.adobe.com/jp/experience-manager/6-3/release-notes/feature-packs-release-notes.html).

### Livefyre を使用するようにAEMを設定します。設定フォルダーの作成 {#configure-aem-to-use-livefyre-create-a-configuration-folder}

1. AEMホームページで、 **ツール** アイコンをクリックし、 **一般/設定ブラウザー**.
   * 詳しくは、[](/help/sites-administering/configurations.md)設定ブラウザーのドキュメントを参照してください。
1. 「**作成**」をクリックして、設定を作成ダイアログを開きます。
1. 設定に名前を付けて、 **クラウド設定** チェックボックス。

   これにより、の下にフォルダーが作成されます。 **ツール/デプロイメント/ Livefyre 設定** 指定された名前で置き換えます。

   ![livefyre-aem-create-config-folder](assets/livefyre-aem-create-config-folder.png)

### Livefyre を使用するための AEM の設定：Livefyre 設定 の作成 {#configure-aem-to-use-livefyre-create-a-livefyre-configuration}

組織の Livefyre ライセンス資格情報を使用するように AEM を設定して、Livefyre と AEM の間で通信できるようにします。

1. AEMホームページで、 **ツール** アイコンをクリックし、 **デプロイメント/Livefyre 設定**.
1. 新しい Livefyre 設定を作成する設定フォルダーを選択して、「**作成**」をクリックします。

   ![create-livefyre-configuration1](assets/create-livefyre-configuration1.png)

   >[!NOTE]
   >
   >Livefyre 設定を追加する前に、フォルダーのプロパティでクラウド設定を有効にしておく必要があります。 設定フォルダーが作成され、設定ブラウザーで管理されます。
   >
   >設定の名前は作成できません。フォルダーのパスによって参照されます。設定はフォルダーごとに 1 つのみです。
   >
   >詳しくは、[](/help/sites-administering/configurations.md)設定ブラウザーのドキュメントを参照してください。

1. 新しく作成した Livefyre 設定カードを選択して、「**プロパティ**」をクリックします。

   ![create-livefyre-configuration2](assets/create-livefyre-configuration2.png)

1. 組織の Livefyre 資格情報を入力し、「 **OK**.

   ![configure-aem2](assets/configure-aem2.png)

   この情報にアクセスするには、Livefyre Studio を開き、に移動します。 **設定/統合設定/資格情報**.

   Livefyre を使用するように AEM インスタンスが設定され、統合機能を使用できます。

### シングルサインオン統合のカスタマイズ {#customize-single-sign-on-integration}

AEM 用 Livefyre パッケージには、AEM Communities プロファイルと Livefyre の SSO サービス間の標準の統合が含まれています。

ユーザーは、AEM サイトにログインすることで、Livefyre ソーシャルコンポーネントにもログインします。ログアウトしたユーザーが、写真のアップロードなど、認証が必要な Livefyre コンポーネント機能を使用しようとすると、Livefyre コンポーネントがユーザー認証を開始します。

デフォルトの認証統合は、すべてのサイトに対して完璧なわけではありません。サイトテンプレートの認証フローに完全に合致させるために、ニーズに合わせてデフォルトの Livefyre Authentication Delegate を上書きすることができます。次の手順を実行します。

1. CRXDE Liteを使用して、コピー */libs/social/integrations/livefyre/components/authorizablecomponent/authclientlib* から */apps/social/integrations/livefyre/components/authorizablecomponent/authclientlib*.
1. 編集して保存 */apps/social/integrations/livefyre/components/authorizablecomponent/authclientlib/auth.js* を使用して、必要に応じて Livefyre Auth Delegate を実装します。

   Auth Delegate のカスタマイズの詳細については、 [ID 統合](https://answers.livefyre.com/developers/identity-integration/).

   AEM Clientlibs について詳しくは、 [クライアント側ライブラリの使用](https://helpx.adobe.com/jp/experience-manager/6-3/sites/developing/using/clientlibs.html).

## AEM Sites での Livefyre の使用 {#use-livefyre-with-aem-sites}

### Livefyre コンポーネントのページへの追加 {#add-livefyre-components-to-a-page}

Livefyre コンポーネントを Sites 内のページに追加する前に、Livefyre クラウド設定を親ページから継承するか、設定をページに直接追加することで、ページ用の Livefyre を有効にする必要があります。サイトのクラウドサービスの追加方法について、実装を参照します。

ページ用に Livefyre が有効になったら、Livefyre コンポーネントを許可するようにコンテナを設定する必要があります。詳しくは、 [デザインモードでのコンポーネントの設定](https://helpx.adobe.com/jp/experience-manager/6-3/sites/authoring/using/default-components-designmode.html) 様々なコンポーネントを有効にする方法を参照してください。

>[!NOTE]
>
>Customize Single Sign-on Integration で認証が設定されるまで、認証が必要なアプリは機能しません。

1. 次の **コンポーネント** デザインモードのサイドパネルで、「 **Livefyre** メニューから選択して、リストを使用可能な Livefyre コンポーネントに制限します。

   ![livefyre-add](assets/livefyre-add.png)

1. Livefyre コンポーネントを選択して、ページ上の位置にドラッグします。
1. 新しい Livefyre アプリを作成するか、既存のアプリを埋め込むかを選択します。

   既存のアプリを埋め込む場合、アプリを選択するように促されます。新しいアプリを作成する場合、アプリは、コンテンツが表示される前に設定しておく必要があります。アプリは、Livefyre サイト、およびページ用に Livefyre クラウド設定を有効にした際に選択したネットワークに作成されます。

   コンポーネントの挿入について詳しくは、 [ページのコンテンツの編集](https://helpx.adobe.com/jp/experience-manager/6-3/sites/authoring/using/editing-content.html).

### AEM ページ用の Livefyre コンポーネントの編集 {#edit-a-livefyre-component-for-an-aem-page}

Livefyre コンポーネントは、Livefyre Studio でのみ設定および編集できます。AEM で次の手順を実行します。

1. 設定する Livefyre コンポーネントをクリックします。
1. 次をクリック： **設定** アイコン（レンチ）を使用して、設定ダイアログを開きます。
1. クリック **このコンポーネントを編集するには、Livefyre Studio に移動します。**.
1. Livefyre Studio でアプリを編集します。

## AEM Assets での Livefyre の使用 {#use-livefyre-with-aem-assets}

### 権限のリクエストと AEM Assets への UGC の読み込み {#request-rights-and-import-ugc-into-aem-assets}

UGC Importer を使用して、Twitter および Instagram ユーザー生成コンテンツ（UGC）を Livefyre Studio から AEM Assets に読み込むことができます。読み込むコンテンツを選択したら、読み込みを完了する前に、コンテンツに対する権限をリクエストする必要があります。

>[!NOTE]
>
>Assets を使用して UGC を読み込む前に、Livefyre Studio でソーシャルアカウントと権限リクエストアカウントを設定する必要があります。詳しくは、 [設定：権限リクエスト](https://docs.adobe.com/content/help/en/livefyre/using/rights-requests/c-how-requesting-rights-works.html) を参照してください。

UGC を AEM Assets に読み込むには：

1. AEMホームページで、に移動します。 **アセット/ファイル**.
1. クリック **作成**&#x200B;を選択し、「 **UGC を読み込みます。**

   ![livefyre-aem-import-ugc](assets/livefyre-aem-import-ugc.png)

1. 次の方法でコンテンツを見つけます。

   * Livefyre からコンテンツを見つけるには、「UGC ライブラリ」タブをクリックします。フィルターおよび検索を使用して UGC ライブラリからコンテンツを見つけます。
   * Twitter および Instagram からコンテンツを見つけるには、「Twitter」または「Instagram」タブをクリックします。検索またはフィルターを使用してコンテンツを見つけます。

1. 読み込むアセットを選択します。選択したアセットは自動的にカウントされ、「 **選択済み** タブをクリックします。
1. **オプション**:次をクリック： **選択済み** 「 」タブに移動し、読み込む UGC コンテンツを確認します。
1. 「**次へ**」をクリックします。

   ![livefyre-aem-import-ugc2](assets/livefyre-aem-import-ugc2.png)

1. 権限リクエストについて、各アセットに対して次のいずれかのオプションを選択します。

   Instagram の場合：

   * **手動で権限をリクエスト** をクリックして、コピー&amp;ペーストできるメッセージを取得し、Instagramを使用してコンテンツ所有者に手動で送信します。
   * **コンテンツ権限の手動属性設定** をクリックして、個々のアセットの権限を上書きします。

   >[!NOTE]
   >
   >ビジネス以外のユーザーアカウントからのコンテンツの集計に影響する更新により、お客様に代わってコメントを投稿したり、作成者からの返信を自動的に確認したりできなくなりました。 [詳しくはここをクリック](https://developers.facebook.com/blog/post/2018/04/04/facebook-api-platform-product-changes/).

   ![livefyre-aem-import-ugc3-6-4](assets/livefyre-aem-import-ugc3-6-4.png)

   Twitter の場合

   * **作成者へメッセージ**：コンテンツ所有者に、アセットに対する権限をリクエストするメッセージを送信します。
   * **コンテンツ権限の手動属性設定** をクリックして、個々のアセットの権限を上書きします。


1. 「**読み込み**」をクリックします。

   Twitter の権限リクエストを送信する場合、コンテンツ所有者には、自身のアカウント上に権限リクエストメッセージが表示されます。

   ![livefyre-aem-rights-request-twitter](assets/livefyre-aem-rights-request-twitter.png)

   >[!NOTE]
   >
   >Twitter には、同じアカウントから来る同じリクエストに対して制限があります。2 つ以上のアセットを読み込む場合、メッセージを個別に変更して、フラグが設定されるのを避けます。

1. クリック **完了** をクリックして、権限リクエストワークフローを完了します。

    Livefyre Studio で、アセットに対する保留中の権限リクエストのステータスを確認できます。コンテンツが権限リクエストを保留している場合、権限が付与されるまで、AEM Assets でアセットが表示されません。権限リクエストが許可されると、AEM Assets にアセットが自動的に表示されます。

   Instagram の場合は、コンテンツ所有者の応答を追跡し、コンテンツへの権限が与えられている場合は手動で権限を付与する必要があります。

## AEM Commerce での Livefyre の使用 {#use-livefyre-with-aem-commerce}

### AEM Commerce を使用した製品カタログの Livefyre への読み込み {#import-product-catalogs-into-livefyre-with-aem-commerce}

AEM Commerce ユーザーは、既存の製品カタログを Livefyre にシームレスに統合して、Livefyre のビジュアライゼーションアプリのユーザーエンゲージメントを推進できます。

製品カタログを読み込んだら、製品がリアルタイムに Livefyre インスタンスに表示されます。AEM Commerce 製品カタログの項目を編集または削除する場合、変更は Livefrye で自動的に更新されます。

1. AEMインスタンスにAEM用の最新の Livefyre パッケージがインストールされていることを確認します。
1. AEMホームページで、に移動します。 **AEM Commerce**.
1. 新しいコレクションを作成するか、既存のコレクションを使用します。
1. コレクションの上にマウスポインターを置いて、「 **コレクションのプロパティ** （鉛筆アイコン）を使用します。
1. チェック **Livefyre に同期**.
1. 入力 **Livefyre ページのプレフィックス** このコレクションをAEMの特定のページにリンクする場合。

   ページのプレフィックスは、環境のルートパスを定義します（そこから製品ページの検索が開始されます）。Livefyre で、関連付けられた対応する製品を含む最初のページが選択されます。別の製品のための別のページを取得するには、複数のコレクションが必要です。

## Livefyre アプリの AEM サポート一覧 {#aem-support-matrix-for-livefyre-apps}

| Livefyre アプリ | AEM 6.1 | AEM 6.2 | AEM 6.3 | AEM 6.4 |
|---|---|---|---|---|
| カルーセル | X | X | X | X |
| チャット | X | X | X | X |
| コメント | X | X | X | X |
| フィルムストリップ |  | X | X | X |
| LiveBlog | X | X | X | X |
| Map | X | X | X | X |
| Media Wall | X | X | X | X |
| モザイク | X | X | X | X |
| 投票 |  | X | X | X |
| レビュー |  | X | X | X |
| シングルカード | X | X | X | X |
| Storify 2 |  | X | X | X |
| トレンド分析 |  | X | X | X |
| アップロードボタン |  | X | X | X |
