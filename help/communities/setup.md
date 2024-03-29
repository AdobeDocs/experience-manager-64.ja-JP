---
title: 初期セットアップ
seo-title: Initial Setup
description: コミュニティの設定
seo-description: Setting up Communities
uuid: c53d280c-c5ae-47cf-8038-f0dea68e15ff
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.4/COMMUNITIES
topic-tags: introduction
content-type: reference
discoiquuid: 0d462ad1-5619-4bb6-9609-bc8987c40a0c
exl-id: 27e92acb-16bd-4519-a7fc-ea1655c56be8
source-git-commit: c5b816d74c6f02f85476d16868844f39b4c47996
workflow-type: tm+mt
source-wordcount: '734'
ht-degree: 4%

---

# 初期セットアップ {#initial-setup}

>[!CAUTION]
>
>AEM 6.4 の拡張サポートは終了し、このドキュメントは更新されなくなりました。 詳細は、 [技術サポート期間](https://helpx.adobe.com/jp/support/programs/eol-matrix.html). サポートされているバージョンを見つける [ここ](https://experienceleague.adobe.com/docs/?lang=ja).

## オーサーインスタンスとパブリッシュインスタンスを開始 {#start-author-and-publish-instances}

開発およびデモの目的では、1 つのオーサーインスタンスと 1 つのパブリッシュインスタンスを実行する必要があります。

これをおこなうには、基本的なAEM [はじめに](../../help/sites-deploying/deploy.md#getting-started) 指示 (

* でのオーサー環境 [localhost:4502](http://localhost:4502/)
* でのパブリッシュ環境 [localhost:4503](http://localhost:4503/)

AEM Communities、

* オーサー環境は

   * サイト、テンプレート、コンポーネントの開発
   * 管理タスクと設定タスク

* パブリッシュ環境は、

   * コンテンツの投稿とモデレートを行うコミュニティエクスペリエンス
   * コミュニティグループ、メンバーおよびメンバーグループの作成

>[!NOTE]
>
>AEMに詳しくない場合は、 [基本操作](../../help/sites-authoring/basic-handling.md) および [ページのオーサリングのクイックガイド](../../help/sites-authoring/qg-page-authoring.md).

## 最新の Communities リリースをインストール {#install-latest-communities-release}

このチュートリアルでは、 [エンゲージメントコミュニティサイト](overview.md#engagement-community) とは、AEM Communities 6.2 機能パックバージョン 1.10 に基づいています。

最新の機能パックがインストールされていることを確認するには、次のページにアクセスします。

* [最新リリース](deploy-communities.md#latest-releases)

を作成するチュートリアルの場合、 [実施可能コミュニティサイト](overview.md#enablement-community)，訪問 [AEM Communities使用の手引き](getting-started-enablement.md).

## Analytics の設定 {#configure-analytics}

条件 [Adobe Analyticsはコミュニティサイト用に設定されています](analytics.md)では、コミュニティメンバーのエクスペリエンスを向上させ、サイトの管理者にフィードバックを提供する、コミュニティアクティビティに関する情報を利用できます。

Adobe Analyticsとの統合はオプションです。

## 電子メールで通知を設定する {#configure-email-for-notifications}

通知機能。デフォルトでは、 `Communities Sites` コンソール。通知用の e メールチャネルを提供します。

必要なのは、電子メールがサイトに対して適切に設定されるためです。

詳しくは、 [電子メールの設定](email.md).

## トンネルサービスの有効化 {#enable-the-tunnel-service}

オーサー環境でコミュニティサイトを作成する場合、トンネルサービスを使用して、パブリッシュ環境に登録されている信頼済みコミュニティメンバーに役割を割り当てることができます。 また、トンネルサービスでは、 [メンバーコンソールとグループコンソール](members.md) （オーサー環境で）

この規則は、パブリッシュ環境で作成されたメンバーとメンバーグループに対して次のように適用されます。 *not* は、オーサー環境で再作成されます。 詳しくは、 [ユーザーとユーザーグループの管理](users.md).

でトンネルサービスを有効にする簡単な手順 **作成者** インスタンスについては、 [トンネルサービス](deploy-communities.md#tunnel-service-on-author).

## コミュニティ管理者の役割 {#community-administrator-role}

コミュニティ管理者グループのメンバーは、コミュニティサイトの作成、サイトの管理、メンバーの管理（コミュニティからのメンバーの禁止が可能）、コンテンツのモデレートをおこなうことができます。

### ユーザーを作成 {#create-user}

でのユーザーの作成 *作成者*&#x200B;コミュニティ管理者の役割が割り当てられているユーザー：

* オーサーインスタンス上

   * 例： [http://localhost:4502/](http://localhost:4503/)

* 管理者権限でログイン

   * 例えば、ユーザー名「admin」/パスワード「admin」です。

* メインコンソールから、に移動します。 **[!UICONTROL ツール/運営/セキュリティ/ユーザー]**
* 次の **[!UICONTROL 編集]** メニュー、選択 **[!UICONTROL ユーザーを追加]**

* 内 `Create New User` ダイアログ入力

   * **[!UICONTROL ID&amp;ast;]**:シリウス
   * **[!UICONTROL 電子メールアドレス]**:sirius.nilson@mailinator.com
   * **[!UICONTROL パスワード (&amp;A);]**:パスワード
   * **[!UICONTROL パスワードの確認 (&amp;A);]**:パスワード
   * **[!UICONTROL 名]**:シリウス
   * **[!UICONTROL 姓 (&amp;A);]**:ニルソン

### コミュニティ管理者グループに Sirius を割り当て {#assign-sirius-to-community-administrators-group}

下にスクロールして `Add User to Groups`:

* 「C」と入力して検索

   * `Community Administrators` を選択します。
   * `Community Enablement Managers` を選択します。

* 「**[!UICONTROL 保存]**」を選択します

![chlimage_1-301](assets/chlimage_1-301.png)

## ソーシャルログインの有効化 {#enable-social-login}

facebookとTwitterを使用したソーシャルログインのデモバージョンを使用する前に、次の手順を実行する必要があります。

1. 修正パックまたは [最新の機能パック](deploy-communities.md#latestfeaturepack) (2017 年 3 月のFacebook API の変更に対応 )
1. [OAuth プロバイダーを有効にする](social-login.md#adobe-granite-oauth-authentication-handler) パブリッシュ環境で

実稼動サーバーの場合、ソーシャルログインの提供に必要なクラウドサービスを作成する必要があります。

詳しくは、 [facebookとTwitterを使用したソーシャルログイン](social-login.md).

## チュートリアルタグを作成 {#create-tutorial-tags}

のタグ名前空間を使用して、エンゲージメントチュートリアルとイネーブルメントチュートリアルに使用するタグを作成します。 `Tutorial`.

以下を使用： [タグ付けコンソール](../../help/sites-administering/tags.md#tagging-console) 次のタグを作成するには：

* `Tutorial: Sports / Baseball`
* `Tutorial: Sports / Gymnastics`
* `Tutorial: Sports / Skiing`
* `Tutorial: Arts / Visual`
* `Tutorial: Arts / Auditory`
* `Tutorial: Arts / History`

![chlimage_1-302](assets/chlimage_1-302.png)

その後、

1. [タグ権限の設定](../../help/sites-administering/tags.md#setting-tag-permissions)
1. [タグを公開](../../help/sites-administering/tags.md#publishing-tags)

AEM CommunitiesはじめにのTutorials用に作成されたタグのサンプルパッケージ

[ファイルを入手](assets/tutorial_tags-v63.zip)

## UGC 共通ストア用の MongoDB {#mongodb-for-ugc-common-store}

を設定することをお勧めしますが、オプションです。 [MSRP](msrp.md) (MongoDB) [共通店](working-with-srp.md) を使用すると、パブリッシュ環境またはオーサー環境からすべての UGC を柔軟にモデレートできます。

手順については、 [デモ用に MongoDB を設定する方法](demo-mongo.md).

デフォルトでは、オーサーインスタンスとパブリッシュAEMインスタンスをインストールすると、ユーザー生成コンテンツ (UGC) がに保存されます [JCR Tar ストレージ](../../help/sites-deploying/platform.md) （を使用してアクセス） [JSRP](jsrp.md). JSRP は共通のストアではありません。つまり、UGC は、UGC が入力されたインスタンス上でのみ表示されます。 通常、UGC はパブリッシュインスタンスで入力され、オーサー環境では表示されないので、モデレートタスクはすべてパブリッシュインスタンスを使用する必要があります。
