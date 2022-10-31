---
title: UI の選択
seo-title: Selecting your UI
description: AEM で使用するインターフェイスを設定します
seo-description: Configure which interface you will use to work in AEM
uuid: af956219-178e-477b-a0cd-dd2341ed2ff0
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.4/SITES
topic-tags: introduction
content-type: reference
discoiquuid: 9cadec1b-f435-4fd8-b4bc-1a23a0cf11f3
exl-id: 415efbe0-95f5-4c9e-ac33-c4a384a8271e
source-git-commit: bd94d3949f0117aa3e1c9f0e84f7293a5d6b03b4
workflow-type: tm+mt
source-wordcount: '907'
ht-degree: 84%

---

# UI の選択 {#selecting-your-ui}

## UI について

オーサー環境では、次の操作をおこなうことができます。

* [オーサリング](/help/sites-authoring/author.md)（[ページオーサリング](/help/sites-authoring/author-environment-tools.md)、[アセットの管理](/help/assets/home.md)、[コミュニティ](/help/communities/author-communities.md)を含む）

* web サイトでのコンテンツの生成および管理の際に必要になる[管理](/help/sites-administering/home.md)タスク

これらの操作のために次の 2 つのグラフィカルユーザーインターフェイスが提供されており、最近のすべてのブラウザーからアクセスできます。

1. タッチ操作対応 UI

   * これは、最新のデフォルトのAEM UI です。
   * 灰色を基調としており、クリーンでフラットなインターフェイスになっています。
   * タッチデバイスとデスクトップデバイスの両方で使用するように設計されており、ルックアンドフィールはすべてのデバイスで同じです。ただし、[リソースの表示および選択](/help/sites-authoring/basic-handling.md#viewing-and-selecting-resources)はわずかに異なります（タップとクリック）。

      * デスクトップ：

   ![screen_shot_2018-03-23at115248](assets/screen_shot_2018-03-23at115248.png)

   * タブレットデバイス（または幅 1024 ピクセル未満のデスクトップ）。

   ![screen_shot_2018-03-23at115505](assets/screen_shot_2018-03-23at115505.png)

1. クラシック UI

   * これはレガシー UI であり、AEM で長年にわたって使用されています。
   * 緑色を基調としています。
   * デスクトップデバイス向けに設計されています。
   * 以降のドキュメントでは、最新の UI について説明しています。クラシック UI でのオーサリングについて詳しくは、[クラシック UI でのオーサリングに関するドキュメント](/help/sites-classic-ui-authoring/classicui.md)を参照してください。

   ![chlimage_1-232](assets/chlimage_1-232.png)

## UI の切り替え

タッチ操作対応 UI が標準の UI になり、 [特徴パリティ](../release-notes/touch-ui-features-status.md) は、サイトの管理および編集にほぼ到達しているので、ユーザーが [クラシック UI](/help/sites-classic-ui-authoring/classicui.md). そのためのオプションがいくつか用意されています。

>[!NOTE]
>
>クラシック UI の機能の同一性の状況について詳しくは、[タッチ UI 機能の同一性](../release-notes/touch-ui-features-status.md)のドキュメントを参照してください。

様々な場所で、使用する UI を定義できます。

* [インスタンスのデフォルト UI の設定](#configuring-the-default-ui-for-your-instance)  — これにより、ユーザーのログイン時にデフォルトの UI が表示されるように設定されますが、ユーザーは、これを上書きして、自分のアカウントまたは現在のセッション用に別の UI を選択できます。

* [お使いのアカウント用のクラシック UI オーサリングの設定](/help/sites-authoring/select-ui.md#setting-classic-ui-authoring-for-your-account)  — これにより、ユーザーはこれを上書きして、自分のアカウントまたは現在のセッション用に別の UI を選択できますが、ページの編集時にデフォルトとして使用される UI が設定されます。

* [現在のセッションのクラシック UI への切り替え](#switching-to-classic-ui-for-the-current-session)  — 現在のセッションのクラシック UI に切り替わります。

* [ページのオーサリング時には、状況に応じて、UI が自動的に上書きされます](#ui-overrides-for-the-editor)。

>[!CAUTION]
>
>クラシック UI に切り替えるための様々なオプションは、そのまますぐに使用することはできません。使用しているインスタンス用に設定する必要があります。
>
>詳しくは、[クラシック UI へのアクセスの有効化](/help/sites-administering/enable-classic-ui.md)を参照してください。

>[!NOTE]
>
>以前のバージョンからアップグレードされたインスタンスでは、ページオーサリング用にクラシック UI が保持されます。
>
>アップグレード後、ページオーサリングが自動的にタッチ対応 UI に切り替わることはありませんが、**WCM オーサリング UI モードサービス**（`AuthoringUIMode` サービス）の [OSGi 設定](/help/sites-deploying/configuring-osgi.md)を使用すると、その切り替えを設定できます。[エディターの UI 上書き](#ui-overrides-for-the-editor)を参照してください。

## ユーザーのインスタンス用のデフォルト UI の設定 {#configuring-the-default-ui-for-your-instance}

システム管理者は、[ルートマッピング](/help/sites-deploying/osgi-configuration-settings.md)を使用して、起動時およびログイン時に表示される UI を設定できます。

この設定はユーザーデフォルトまたはセッション設定によって上書きできます。

## ユーザーのアカウント用のクラシック UI オーサリングの設定 {#setting-classic-ui-authoring-for-your-account}

各ユーザーは、[ユーザーの環境設定](/help/sites-authoring/user-properties.md)にアクセスして、ページオーサリング用に（デフォルト UI の代わりに）クラシック UI を使用するかどうかを定義できます。

この設定はセッション設定によって上書きできます。

## 現在のセッションでのクラシック UI への切り替え {#switching-to-classic-ui-for-the-current-session}

タッチ対応 UI を使用しているデスクトップユーザーは、必要に応じてクラシック UI（デスクトップ専用）に戻すことができます。現在のセッション用にクラシック UI に切り替えるには、複数の方法があります。

* **ナビゲーションリンク**

   >[!CAUTION]
   >
   >クラシック UI に切り替えるためのこのオプションは、そのまますぐに使用することはできません。使用しているインスタンス用に設定する必要があります。
   >
   >
   >詳しくは、[クラシック UI へのアクセスの有効化](/help/sites-administering/enable-classic-ui.md)を参照してください。

   この設定を有効にすると、該当するコンソールの上にマウスポインターを置くたびに、アイコン（モニターのシンボル）が表示され、これをタップ／クリックすると、適切な場所がクラシック UI で開きます。

   例えば、**Sites** から **siteadmin** へのリンクなどです。

   ![screen_shot_2018-03-23at111924](assets/screen_shot_2018-03-23at111924.png)

* **URL**

   クラシック UI には、`welcome.html` のようこそ画面の URL を使用してアクセスできます。例は次のとおりです。

   `http://localhost:4502/welcome.html`

   >[!NOTE]
   >
   >タッチ対応 UI には、`sites.html` 経由でアクセスできます。次に例を示します。
   >
   >
   >`http://localhost:4502/sites.html`

### ページ編集時のクラシック UI への切り替え {#switching-to-classic-ui-when-editing-a-page}

>[!CAUTION]
>
>クラシック UI に切り替えるためのこのオプションは、そのまますぐに使用することはできません。使用しているインスタンス用に設定する必要があります。
>
>詳しくは、[クラシック UI へのアクセスの有効化](/help/sites-administering/enable-classic-ui.md)を参照してください。

有効な場合は、**ページ情報**&#x200B;ダイアログで&#x200B;**クラシック UI を開く**&#x200B;が使用可能です。

![chlimage_1-49](assets/chlimage_1-49.png)

### エディターの UI 上書き {#ui-overrides-for-the-editor}

ページのオーサリング時には、ユーザーまたはシステム管理者が定義した設定がシステムによって上書きされることがあります。

* ページのオーサリング時には次のようになります。

   * URL で `cf#` を使用してページにアクセスする場合、クラシックエディターが強制的に使用されます。次に例を示します。

      `http://localhost:4502/cf#/content/geometrixx/en/products/triangle.html`

   * URL で `/editor.html` を使用しているか、タッチデバイスを使用している場合、タッチ対応エディターが強制的に使用されます。次に例を示します。

      `http://localhost:4502/editor.html/content/geometrixx/en/products/triangle.html`

* 強制は一時的なものであり、ブラウザーセッションでのみ有効です。

   * Cookie は、タッチ対応（`editor.html`）とクラシック（`cf#`）のどちらが使用されているかに応じて設定されます。

* `siteadmin` を使用してページを開くと、以下が存在するかがチェックされます。

   * Cookie
   * ユーザーの環境設定
   * どちらも存在しない場合は、**WCM オーサリング UI モードサービス**（`AuthoringUIMode` サービス）の [OSGi 設定](/help/sites-deploying/configuring-osgi.md)で指定された定義がデフォルトで使用されます。

>[!NOTE]
>
>[ユーザーが既にページオーサリング用の環境設定を定義している](#setting-classic-ui-authoring-for-your-account)場合は、OSGi プロパティの変更によってその設定が上書きされることはありません。

>[!CAUTION]
>
>既に説明したように、Cookie を使用しているので、次の操作はお勧めしません。
>
>* URL の手動編集 - 非標準の URL を使用すると予期しない状況となり、機能しなくなる可能性があります。
>* 両方のエディターを同時に開くこと - 例えば、別のウィンドウで開くなど。
>

