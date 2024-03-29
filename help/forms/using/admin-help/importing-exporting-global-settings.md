---
title: グローバル設定の読み込みと書き出し
seo-title: Importing and exporting global settings
description: Workspace の検索テンプレート定義およびグローバル設定の読み込みと書き出しが可能です。
seo-description: You can import and export search template definitions and global settings for Workspace.
uuid: 8f1f210d-e850-4b2c-bb5a-942fa8299791
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_workspace
products: SG_EXPERIENCEMANAGER/6.4/FORMS
discoiquuid: 72fe5749-2fa2-442f-b679-7889faeafcac
exl-id: 9eabafbe-2193-4799-9bdd-c2be42ead0b9
source-git-commit: c5b816d74c6f02f85476d16868844f39b4c47996
workflow-type: tm+mt
source-wordcount: '1229'
ht-degree: 37%

---

# グローバル設定の読み込みと書き出し {#importing-and-exporting-global-settings}

>[!CAUTION]
>
>AEM 6.4 の拡張サポートは終了し、このドキュメントは更新されなくなりました。 詳細は、 [技術サポート期間](https://helpx.adobe.com/jp/support/programs/eol-matrix.html). サポートされているバージョンを見つける [ここ](https://experienceleague.adobe.com/docs/?lang=ja).

Workspace の検索テンプレート定義およびグローバル設定の読み込みと書き出しが可能です。

>[!NOTE]
>
>AEM Forms のリリースでは Flex Workspace は廃止されています。

例えば、ある環境から検索テンプレート定義とグローバル設定を書き出し、別の環境に読み込むことで、開発環境から実稼動環境に移行できます。

グローバル設定ファイルを書き出した後、XML またはテキストエディタで設定を変更できます。 ただし、編集が必要な設定は、JChannelConnectionProperties、formViewOnly、specialRoutes の各設定のみです。 詳しくは、 [Workspace のグローバル設定](importing-exporting-global-settings.md#workspace-global-settings).

>[!NOTE]
>
>グローバル設定ファイルのイベントプロパティを変更する場合は、サーバーを再起動する必要があります。

## 検索テンプレート定義のインポート {#import-a-search-template-definition}

1. 管理コンソールで、サービス/Workspace/グローバル管理をクリックします。
1. 「検索テンプレート定義をインポート」ボックスで、「ファイルを選択」をクリックし、検索テンプレートを選択します。 読み込むことができるのは、Workspace のインスタンスから最初に書き出された検索テンプレート定義のみです。
1. 「読み込み」をクリックします。

## 検索テンプレート定義のエクスポート {#export-a-search-template-definition}

1. [ グローバル管理 ] ページの [ 検索テンプレート定義を書き出し ] で、[ すべてリスト ] をクリックします。
1. 検索テンプレートのリストで、書き出すテンプレートを選択します。

   >[!NOTE]
   >
   >複数のテンプレートを選択できますが、選択した最後のテンプレートのみが書き出されます。

1. 「書き出し」をクリックし、ファイルをコンピューターに保存します。

## グローバル設定を読み込む {#import-global-settings}

1. グローバル管理ページの「グローバル設定を読み込む」で、「ファイルを選択」をクリックし、グローバル設定ファイルを選択します。 グローバル設定ファイルは XML 形式である必要があります。
1. 「読み込み」をクリックします。

## グローバル設定を書き出し {#export-global-settings}

1. [ グローバル管理 ] ページの [ グローバル設定の書き出し ] で、[ 書き出し ] をクリックします。
1. ファイルをコンピューターに保存します。

## Workspace のグローバル設定 {#workspace-global-settings}

グローバル設定ファイルは変更できます。ただし、編集が必要な設定は、JChannelConnectionProperties、formViewOnly、specialRoutes の各設定のみです。

>[!NOTE]
>
>AEM Forms のリリースでは Flex Workspace は廃止されています。

Workspace グローバル設定ファイルには、次の設定が含まれています。

### specialRoutes 設定 {#specialroutes-settings}

この *specialRoutes* 設定は、Workspace で特別なルートのプロパティ、承認および拒否を指定します。 状況によっては、Workspace のタスクカードにこれらのルートのボタンが表示され、ユーザーはフォームを開かずにルートを選択できます。 グローバル設定ファイルの specialRoutes 設定を変更して、承認および拒否のためのカスタマイズ名を追加したり、追加のルートを作成したりできます。

**client_specialRoutes_routes_approve_style：**Workspace テーマにあるスタイルの名前。これによって、承認ボタンアイコンを識別します。このスタイルには、有効アイコンと無効アイコンの値を含める必要があります。 カスタムボタンのスタイルを定義するには、次のテンプレートを使用する必要があります。
` .buttonApprove {  icon: Embed('images/LC_DirectApprove_Sm_N.png');  disabledIcon: Embed('images/LC_DirectApprove_Sm_D.png');  paddingLeft: 5;  }` Workspace の CSS ファイルは、workspace-theme.swf ファイルに埋め込まれます。このファイルは、adobe-workspace-client.ear / adobe-workspace-client.war ファイルにあります。 Workspace の外観を変更するには、workspace-theme.swf ファイルを再コンパイルする必要があります。

**client_specialRoutes_routes_deny_names：** Workbench ユーザーが「拒否」と解釈するために使用できる様々な文字列です。 これらの文字列では、大文字と小文字が区別されます。例えば、デフォルト値は「deny」です。Workbench ユーザーのプロセスで「Deny」という単語が使用された場合、この単語は認識されません。ルートボタンをカスタマイズしたり、ルートボタンにスタイルを適用したりするには、「Deny」という単語をこの設定に追加する必要があります。

**client_specialRoutes_routes_deny_style：**ワークスペーステーマファイルにあるスタイルの名前。これによって、「拒否ボタン」アイコンを識別します。このスタイルには、有効アイコンと無効アイコンの値を含める必要があります。 カスタムボタンのスタイルを定義するには、次のテンプレートを使用する必要があります。
`  .buttonDeny {   icon: Embed('images/LC_DirectDeny_Sm_N.png');   disabledIcon: Embed('images/LC_DirectDeny_Sm_D.png');   paddingLeft: 0;   }` **client_specialRoutes_routes_approve_names:** Workbench ユーザーが「承認」と解釈するために使用できる様々な文字列。 これらの文字列では、大文字と小文字が区別されます。例えば、デフォルト値は、「approve」です。Workbench ユーザーのプロセスで「Approve」という単語が使用された場合、この単語は認識されません。ルートボタンをカスタマイズしたり、ルートボタンにスタイルを適用したりするには、「Approve」という単語をこの設定に追加する必要があります。

**client_specialRoutes_names：**&#x200B;カスタマイズされた文字列値をリソースファイルから検索するために使用されるキー。この設定の各エントリには、名前とスタイルの値を含める必要があります。

### グループ設定 {#jgroup-settings}

これらの設定は、AdobeLiveCycleES 2.5 以前からアップグレードした場合にのみ表示されます。

**server_remoteevents_ClientTimeoutMiliseconds：** JGroup がイベントメッセージを待機する最大時間。 この設定は変更しないでください。

**server_remoteevents_ServerTimeoutMiliseconds：**&#x200B;サーバーでの JGroup メッセージ受信のタイムアウト。 このオプションで、サーバーからクライアントにメッセージを送信する際の遅延を設定します。

**server_remoteevents_JChannelConnectionProperties：**（サービスイベントが RemoteEvent サービスによって処理される）サーバーと Workspace のすべてのインスタンスとの通信に使用される JGroup の接続プロパティです。

マルチキャスト IP アドレス (mcast_addr)、マルチキャスト IP ポート (mcast_port)、およびマルチキャストパケットの TTL(ip_ttl) に対して、UDP 値を変更する必要が生じる場合があります。 デフォルトでは、マルチキャスト IP アドレスとポートの値はランダムに生成され、通常は値を変更する必要はありません。 ただし、会社にマルチキャスト IP アドレスの特定のマルチキャスト範囲に関するネットワークポリシーがある場合は、値の変更が必要になる場合があります。

>[!NOTE]
>
>TTL は、クラスタ内のサーバー間のネットワークスイッチ数より大きく設定する必要があります。ただし、値が大きすぎる場合は、マルチキャストパケットがサブネットに送信され、サブネットが破棄される可能性があります。

この設定の残りのプロパティは変更しないでください。

**server_remoteevents_JGroupName：**&#x200B;リモートイベント通信に使用される JGroup の名前。この値は、クラスター内の競合を避けるために、ランダムに生成されます。 この値は変更しないでください。

### formView 設定 {#formview-settings}

**client_formView_openFormInFullScreen：** Workspace のすべてのフォームをフルスクリーンモードで表示するには、このオプションを true に設定します。このオプションのデフォルトは false に設定されており、フォームはフルスクリーンモードで表示されません。User サービスには、タスクに関連付けられたドキュメントをフルスクリーンモードで開くためのオプションが含まれています。 これにより、プロセスごとに表示を制御できます。

**client_routes_formViewOnly：** True に設定すると、ルートは Workspace でカード表示にもリスト表示にも表示されません。デフォルト値は False で、ルートはカード表示およびリスト表示に表示されます。

### その他の設定 {#other-settings}

**client_mimeTypes_openOutsideBrowser：** Workspace ブラウザーインスタンスとは別に開くドキュメントの MIME タイプです。組織のプロセスで追加の MIME タイプが必要な場合は、ここで指定します。 デフォルト値は次のとおりです。

* `application/msword`
* `application/msexcel`
* `application/ms-powerpoint`

**client_customUI_caching：**&#x200B;カスタムタスクのユーザーインターフェイスをキャッシュします。

**server_debugLevel：**&#x200B;この設定は変更しないでください。

**client_pollingInterval：**&#x200B;新しいタスクおよび変更されたタスクを検出するために Flex Workspace（JEE 上の AEM Forms では廃止されています）で使用されるポーリング間隔（秒）を設定します。デフォルト値は 3 秒です。これは、AEM Forms Workspace では機能しません。

**client_systemContext_name:** AEM Forms Workspace でタスクの添付ファイルに対して（「添付ファイル」タブの）「追加者」フィールドに表示するカスタム名（例：市民）を指定します。

カスタム名を定義するには：

`<client_systemContext_name>[custom name to display]</client_systemContext_name>`

>[!NOTE]
>
>Demo アプリケーションの場合、デフォルトの表示名はです。 **市民**. 作成するカスタムアプリケーションの場合、デフォルトの表示名はです。 **システムコンテキストアカウント**.
