---
title: アプリを管理タイル
seo-title: Manage App Tile
description: このページでは、アプリケーションの詳細を変更する機能を提供する、アプリダッシュボードのアプリを管理タイルについて説明します。
seo-description: Follow this page to learn about the Manage App Tile on the app dashboard that provides the ability to modify details about the Application.
uuid: bde75ecd-8694-427c-9b16-2c4ab2fd4d8b
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.4/MOBILE
topic-tags: authoring-adobe-phonegap-enterprise
discoiquuid: a87834c9-247c-49fa-9978-a969230db91c
exl-id: 732ef9c7-b556-497d-a157-c1b2945eb4e1
source-git-commit: c5b816d74c6f02f85476d16868844f39b4c47996
workflow-type: tm+mt
source-wordcount: '1299'
ht-degree: 4%

---

# アプリを管理タイル{#manage-app-tile}

>[!CAUTION]
>
>AEM 6.4 の拡張サポートは終了し、このドキュメントは更新されなくなりました。 詳細は、 [技術サポート期間](https://helpx.adobe.com/jp/support/programs/eol-matrix.html). サポートされているバージョンを見つける [ここ](https://experienceleague.adobe.com/docs/?lang=ja).

>[!NOTE]
>
>Adobeは、単一ページアプリケーションのフレームワークベースのクライアントサイドレンダリング（React など）を必要とするプロジェクトでは、SPA Editor を使用することをお勧めします。 [詳細情報](/help/sites-developing/spa-overview.md)を参照してください。

この **アプリを管理** アプリダッシュボード上のタイルを使用すると、アプリケーションの詳細を変更できます。 詳細ページを開くには、アプリを管理タイルの詳細リンクをクリックします。 アプリを管理ページから、PhoneGap アプリケーション設定 (config.xml) 設定を編集し、様々なアプリケーションストアに送信するためのアプリケーションを準備できます。

![chlimage_1-116](assets/chlimage_1-116.png)

## アプリを管理タイルについて {#understanding-the-manage-app-tile}

内の各タイルにドリルインできます。 **アプリを管理** タイルを表示または編集するには、「。..」をクリックします。 をクリックします。

### 「基本」タブ {#the-basic-tab}

次の項目を編集： **名前**, **作成者**, **短い説明**、および **説明** 」をクリックします。

![chlimage_1-117](assets/chlimage_1-117.png)

### 「詳細」タブ {#the-advanced-tab}

各モバイルアプリケーションプラットフォームは、各アプリストアを特別にターゲティングして、どのデータが収集されるかを記述します。

表示されるプラットフォームは、PhoneGap config.xml コンテンツによって決まります。

```xml
<widget>  
<gap:platform name="ios"/>  
<gap:platform name="android"/>  
</widget>
```

例えば、Apple App StoreやGoogle Play Store などの各ベンダーのアプリケーションストアでは、顧客にアプリの詳細を表示するために、モバイルアプリケーションのスクリーンショットが 1 つ以上必要です。 これらのスクリーンショットは、ディメンションとコンテンツに関して厳密な要件を持つ場合があります（基本的には、アプリケーションを真に表す必要があります）。 AEM Apps では、サポート対象のプラットフォームに関するこれらのスクリーンショットの選択と管理、および各ベンダーのアプリケーションストアで必要なポートのサイズの表示をサポートしています。

>[!NOTE]
>
>AEM Verify アプリを使用すると、AEMのアプリの詳細にスクリーンショットを直接送信できます。
>
>詳しくは、 [AEM Verify のモバイルクイックスタート](/help/mobile/phonegap-mobile-quickstart.md) を参照してください。

![chlimage_1-118](assets/chlimage_1-118.png)

### メタデータ {#metadata}

>[!NOTE]
>
>以前、 **アプリを管理** タイル：詳しくは、 [アプリのメタデータの編集](/help/mobile/phonegap-editmetadata.md) をクリックして、メタデータを表示および編集します。

#### 共通メタデータ {#common-metadata}

各アプリケーションには、アプリケーションの様々な側面を設定する際に役立つメタデータを関連付ける必要があります。 アプリを管理ページは、メタデータの収集に関連する 2 つの異なる領域に分かれています。 プラットフォーム固有のメタデータと共通のメタデータ。

すべてのプラットフォームに共通の設定とメタデータがあります。

このセクションでは、コンテンツ更新サーバーの URL、モバイルアプリケーションのランディングページ、コンパイル用の PhoneGap バージョン、アプリケーションのバージョン、名前、説明などを定義します。

**アプリのバージョン** は、アプリケーションの動作中のバージョンです。 一般的なベストプラクティスは、3 桁の表記を使用し、最初のリリースの前に 1.0.0 未満で開始することです。

**PhoneGap バージョン** は、PhoneGap でアプリケーションをコンパイルするバージョンです。 最新で最大の機能とバグ修正を確実に入手するために、現在のバージョンに対応することをお勧めします。

**コンテンツ更新サーバー URL** は、アプリケーションがコンテンツ同期の更新を呼び出す際に使用する URL です。 Dispatcher URL に設定するか、Dispatcher を使用していない場合は、アプリケーションに対して ContentSync の更新を提供するために使用されるパブリッシュインスタンスの 1 つに設定する必要があります。

![chlimage_1-119](assets/chlimage_1-119.png)

>[!NOTE]
>
>フィールドにデータが入力されている場合を除き、このセクションは空に表示される場合があります。
>
>詳細ビューの上部に、「アプリケーションのバージョン」、「 PhoneGap のバージョン」、「 URL を更新」が表示されます。これらの値は、それぞれ「共通メタデータ」セクション内で設定できます。 ただし、アプリ ID は編集できません。

#### プラットフォームメタデータ {#platform-metadata}

PhoneGap config.xml で定義されているすべてのプラットフォームには、カスタムプラットフォームプロパティを含めることができます。 AEM開発者は、これらのプロパティを取り込むために、コンテンツ構造に寄稿する必要があります。 iOSでは、プラットフォーム固有のプロパティの例が提供されています。

設定済みのすべてのプラットフォームのメタデータが、アプリを管理タイルの「詳細」タブに同時に表示されるようになりました。

>[!NOTE]
>
>プラットフォームメタデータセクションは、CLI または Remote PhoneGap ビルド中は PhoneGap では使用されませんが、AEMは、ターゲットベンダーのアプリケーションストアに送信する際に後で使用できるように、プラットフォームのメタデータを取得しようとします。

AEMで認識されないプラットフォームの場合でも、AEM開発者は、UI を拡張して、後でアプリケーションの送信プロセス中に書き出して使用できる、このメタデータを取り込むことができます。

#### iOS メタデータ {#ios-metadata}

Apple AppStore では、配布用にアプリケーションを送信するために追加のメタデータが必要です。 iOSのメタデータセクションは、Appleの iTMSTransporter ツールで、関連するApple開発者のアカウントにメタデータを公開するために使用できる、必要な情報の収集を試みます。

Apple固有のメタデータを取得するには、まず、にアプリケーションを作成する必要があります [https://itunesconnect.apple.com](https://itunesconnect.apple.com/). Apple iTMSTransporter ツールを使用してメタデータを検証し、itunesconnect.apple.com にアップロードする場合は、アプリケーションを作成すると、AppleはiOSのメタデータセクションで必要なメタデータを生成します。 収集するメタデータを取得するだけの場合は、iOS固有のメタデータを入力する必要はありません。 iOSと共通のメタデータを結合するメタデータを書き出し、すべてのスクリーンショットを zip ファイルに収集して、いつでもダウンロードできます。

ダウンロードした zip ファイルには、metadata.xml を調べることができる itmsp ファイルが含まれています。 itmsp ファイルには、書き出されたメタデータ（metadata.xml ファイル内）と、関連するすべてのスクリーンショットが含まれます。

書き出し機能は、スクリーンショットとメタデータを収集する便利な方法を提供します。この方法を使用して、ベンダー固有のアプリケーションストアに入力するために、アプリケーションパブリッシャーに渡すことができます。

![chlimage_1-120](assets/chlimage_1-120.png)

#### Android メタデータ {#android-metadata}

Android プラットフォームを選択する場合、この時点では設定できるカスタムメタデータはありません。 ダウンロードボタンをクリックすると、すべてのメタデータと関連するスクリーンショットを含むプロパティファイルを使用して zip ファイルが生成されます。

書き出し機能は、スクリーンショットとメタデータを収集する便利な方法を提供します。この方法を使用して、ベンダー固有のアプリケーションストアに入力するために、アプリケーションパブリッシャーに渡すことができます。

![chlimage_1-121](assets/chlimage_1-121.png)

### コンテンツ更新サーバーの URL {#content-update-server-url}

AEM Apps の主な機能の 1 つは、モバイルアプリケーションが ContentSync を通じて新しいコンテンツをリクエストする機能です。コンテンツは、HTML リソース、ページ、ビデオ、画像、テキストなどです。 コンテンツ作成者がコンテンツを更新して公開すると、サーバーがそのコンテンツの更新をモバイルアプリケーションがダウンロードできるようになります。

Content Update Server URL プロパティは、パブリッシュインスタンスを指す必要がある URL です。直接、または Dispatcher または CDN を通じて。 URL の形式は次のとおりです。

`https://[hostname]:[port]`

>[!NOTE]
>
>オーサーサーバーインスタンスが複数のパブリッシュサーバーインスタンス (AEMの共通アーキテクチャ ) にレプリケートされている場合、更新はオーサーインスタンス上で構築され、すべてのパブリッシュインスタンスにレプリケートされるので、各パブリッシュサーバーには同じ更新内容が含まれます。 基本的に、ロードバランシングとフェイルオーバーは完全にサポートされます。

### 「プラグイン」タブ {#the-plugins-tab}

この **プラグイン** 「 」タブには、アプリに関連付けられているプラグインが表示されます。 この情報は、ビルド中に適切なプラグインを取得するために使用されます。

![chlimage_1-122](assets/chlimage_1-122.png)

### 「スクリーンショット」タブ {#the-screenshots-tab}

この **スクリーンショット** 「 」タブには、様々なプラットフォームでサポートされているスクリーンショット解像度が表示されます。

![chlimage_1-123](assets/chlimage_1-123.png)

>[!NOTE]
>
>スクリーンショットを追加および削除するには、 [アプリのメタデータの編集](/help/mobile/phonegap-editmetadata.md).

### 「認証」タブ {#the-authentication-tab}

この **認証** 「 」タブでは、アプリケーションに関連付ける OAuth クライアントを選択でき、開発者がAdobe Experience Managerの OAuth 認証を利用できるようになります。

![chlimage_1-124](assets/chlimage_1-124.png)

### 次の手順 {#the-next-steps}

アプリケーションダッシュボードの「アプリの管理」タイルについて学習したら、他のオーサリングの役割に関する次のリソースを参照します。

* [アプリのメタデータの編集](/help/mobile/phonegap-editmetadata.md)
* [アプリの定義](/help/mobile/phonegap-app-definitions.md)
* [アプリを作成ウィザードを使用した新しいアプリの作成](/help/mobile/phonegap-create-new-app.md)
* [既存のハイブリッドアプリの読み込み](/help/mobile/phonegap-adding-content-to-imported-app.md)
* [コンテンツサービス](/help/mobile/develop-content-as-a-service.md)

### その他のリソース {#additional-resources}

管理者および開発者の役割と責務について詳しくは、以下のリソースを参照してください。

* [AEMを使用したAdobe PhoneGap Enterprise 向け開発](/help/mobile/developing-in-phonegap.md)
* [AEM を使用した Adobe PhoneGap Enterprise のコンテンツの管理](/help/mobile/administer-phonegap.md)
