---
title: メール通知の設定
seo-title: Configuring Email Notification
description: AEMで電子メール通知を設定する方法を説明します。
seo-description: Learn how to configure Email Notification in AEM.
uuid: 6cbdc312-860b-4a69-8bbe-2feb32204a27
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.4/SITES
topic-tags: operations
content-type: reference
discoiquuid: 6466d7b8-e308-43c5-acdc-dec15f796f64
exl-id: ea12035c-09b6-4197-ab23-c27fe71e7432
source-git-commit: c5b816d74c6f02f85476d16868844f39b4c47996
workflow-type: tm+mt
source-wordcount: '1170'
ht-degree: 68%

---

# メール通知の設定{#configuring-email-notification}

>[!CAUTION]
>
>AEM 6.4 の拡張サポートは終了し、このドキュメントは更新されなくなりました。 詳細は、 [技術サポート期間](https://helpx.adobe.com/jp/support/programs/eol-matrix.html). サポートされているバージョンを見つける [ここ](https://experienceleague.adobe.com/docs/?lang=ja).

AEMは、次のユーザーに電子メール通知を送信します。

* 変更やレプリケーションなど、ページイベントを購読したことがある。[通知インボックス](/help/sites-classic-ui-authoring/author-env-inbox.md#subscribing-to-notifications)では、このようなイベントを購読する方法について説明します。

* フォーラムイベントを購読したことがある
* ワークフローで手順を実行する必要があります。 この [参加者ステップ](/help/sites-developing/workflows-step-ref.md#participant-step) ここでは、ワークフローでの e メール通知のトリガー方法について説明します。

前提条件：

* ユーザーのプロファイルで有効な E メールアドレスを定義する必要があります。
* **Day CQ Mail Service** が適切に設定されている必要があります。

ユーザーへの通知は、各自がプロファイルで定義している言語のメールで送信されます。言語ごとに、独自のカスタマイズ可能なテンプレートがあります。新しい言語用には新しいメールテンプレートを追加できます。

>[!NOTE]
>
>AEM を操作しているときは、このようなサービスの設定を管理する方法がいくつかあります。詳細および推奨事項については、[OSGi の設定](/help/sites-deploying/configuring-osgi.md)を参照してください。

## メールサービスの設定 {#configuring-the-mail-service}

AEMで E メールを送信するには、 **Day CQ Mail Service** を適切に設定する必要があります。 設定は Web コンソールで確認できます。 AEM を操作しているときは、このようなサービスの設定を管理する方法がいくつかあります。詳細および推奨事項については、[OSGi の設定](/help/sites-deploying/configuring-osgi.md)を参照してください。

以下の制約が適用されます。

* **SMTP サーバーポート**&#x200B;は 25 以上にする必要があります。

* **SMTP サーバーホスト名**&#x200B;は空白にできません。
* **「送信元」アドレス**&#x200B;は空白にしてはなりません。

**Day CQ Mail Service** の問題をデバッグしやすくするために、サービスのログを監視できます。

`com.day.cq.mailer.DefaultMailService`

設定は、Web コンソールに次のように表示されます。

![chlimage_1-276](assets/chlimage_1-276.png)

## メール通知チャネルの設定 {#configuring-the-email-notification-channel}

ページまたはフォーラムのイベント通知を購読するとき、送信元のメールアドレスは、デフォルトで `no-reply@acme.com` に設定されます。この値は、Web コンソールで **Notification Email Channel** サービスを設定することで変更できます。

送信元のメールアドレスを設定するには、`sling:OsgiConfig` ノードをリポジトリに追加します。以下の手順で、CRXDE Lite を使用してノードを直接追加します。

1. CRXDE Lite で、`config` という名前のノードを、アプリケーションフォルダーの下に追加します。
1. config フォルダーに、以下の名前のノードを追加します。

   `com.day.cq.wcm.notification.email.impl.EmailChannel`リソースのタイプは次のとおりとします。`sling:OsgiConfig`

1.  `String` プロパティを `email.from` という名前のノードに追加します。値には、使用するメールアドレスを指定します。

1. 「**すべて保存**」をクリックします。

次の手順を実行して、コンテンツパッケージのソースフォルダー内でノードを定義します。

1.  `jcr_root/apps/*app_name*/config folder` に、`com.day.cq.wcm.notification.email.impl.EmailChannel.xml` という名前のファイルを作成します。

1. このノードを表現する次の XML を追加します。

   `<?xml version="1.0" encoding="UTF-8"?> <jcr:root xmlns:sling="https://sling.apache.org/jcr/sling/1.0" xmlns:jcr="https://www.jcp.org/jcr/1.0" jcr:primaryType="sling:OsgiConfig" email.from="name@server.com"/>`
1. `email.from` 属性の値（`name@server.com`）を、実際のメールアドレスに置き換えます。

1.  ファイルを保存します。

## ワークフロー電子メール通知サービスの設定 {#configuring-the-workflow-email-notification-service}

ワークフローの電子メール通知を受け取ると、送信元電子メールアドレスとホスト URL プレフィックスの両方がデフォルト値に設定されます。 これらの値は、 **Day CQ Workflow Email Notification Service** をクリックします。 その場合は、リポジトリ内の変更を保持することをお勧めします。

デフォルトの設定は、Web コンソールで次のように表示されます。

![chlimage_1-277](assets/chlimage_1-277.png)

### ページ通知用のメールテンプレート {#email-templates-for-page-notification}

ページ通知用の電子メールテンプレートは、以下にあります。

`/libs/settings/notification-templates/com.day.cq.wcm.core.page`

デフォルトの英語のテンプレート（`en.txt`）は次のように定義されています。

```xml
subject=[CQ Page Event Notification]: Page Event

header=-------------------------------------------------------------------------------------\n \
Time: ${time}\n \
User: ${userFullName} (${userId})\n \
-------------------------------------------------------------------------------------\n\n

message=The following pages were affected by the event: \n \
 \n \
${modifications} \n \
 \n\n
footer=\n \
-------------------------------------------------------------------------------------\n \
This is an automatically generated message. Please do not reply.
```

#### ページ通知用のメールテンプレートのカスタマイズ {#customizing-email-templates-for-page-notification}

ページ通知用の英語のメールテンプレートをカスタマイズするには：

1. CRXDE で、次のファイルを開きます。

   `/libs/settings/notification-templates/com.day.cq.wcm.core.page/en.txt`

1. 必要に応じてファイルを変更します。
1. 変更内容を保存します。

テンプレートは、次のフォーマットにする必要があります。

```
 subject=<text_1>
 header=<text_2>
 message=<text_3>
 footer=<text_4>
```

ここで、 &lt;text_x> は、静的テキストと動的文字列変数を組み合わせることができます。 次の変数は、ページ通知用の電子メールテンプレート内で使用できます。

* `${time}`、イベントの日時。

* `${userFullName}`、イベントを実行したユーザーのフルネーム。

* `${userId}`、イベントを実行したユーザーの ID。
* `${modifications}`、ページイベントのタイプとページパスを次の形式で表します。

   &lt;page event type> => &lt;page path>

   次に例を示します。

   PageModified => /content/geometrixx/ja/products

### フォーラム通知用のメールテンプレート {#email-templates-for-forum-notification}

フォーラム通知用の電子メールテンプレートは、次の場所にあります。

`/etc/notification/email/default/com.day.cq.collab.forum`

デフォルトの英語のテンプレート（`en.txt`）は次のように定義されています。

```xml
subject=[CQ Forum Notification]

header=-------------------------------------------------------------------------------------\n \
Time: Time: ${time}\n \
Forum Page Path: ${forum.path}\n \
-------------------------------------------------------------------------------------\n\n

message=Page: ${host.prefix}${forum.path}.html\n

footer=\n \
-------------------------------------------------------------------------------------\n \
This is an automatically generated message. Please do not reply.
```

#### フォーラム通知用のメールテンプレートのカスタマイズ {#customizing-email-templates-for-forum-notification}

フォーラム通知用の英語のメールテンプレートをカスタマイズするには：

1. CRXDE で、次のファイルを開きます。

   `/etc/notification/email/default/com.day.cq.collab.forum/en.txt`

1. 必要に応じてファイルを変更します。
1. 変更内容を保存します。

テンプレートは、次のフォーマットにする必要があります。

```
 subject=<text_1>
 header=<text_2>
 message=<text_3>
 footer=<text_4>
```

`<text_x>` には、静的なテキストと動的な文字列変数を混在させることができます。

フォーラム通知用のメールテンプレート内では次の変数を使用できます。

* `${time}`、イベントの日時。

* `${forum.path}`、フォーラムページのパス。

### ワークフロー通知用のメールテンプレート {#email-templates-for-workflow-notification}

ワークフロー通知用の電子メールテンプレート（英語）は、次の場所にあります。

`/libs/settings/workflow/notification/email/default/en.txt`

これは次のように定義されます。

```xml
subject=Workflow notification: ${event.EventType}

header=-------------------------------------------------------------------------------------\n \
Time: ${event.TimeStamp}\n \
Step: ${item.node.title}\n \
User: ${participant.name} (${participant.id})\n \
Workflow: ${model.title}\n \
-------------------------------------------------------------------------------------\n\n

message=Content: ${host.prefix}${payload.path.open}\n

footer=\n \
-------------------------------------------------------------------------------------\n \
View the overview in your ${host.prefix}/aem/inbox\n \
-------------------------------------------------------------------------------------\n \
This is an automatically generated message. Please do not reply.
```

#### ワークフロー通知用の電子メールテンプレートのカスタマイズ {#customizing-email-templates-for-workflow-notification}

ワークフローイベント通知用の英語のメールテンプレートをカスタマイズするには：

1. CRXDE で、次のファイルを開きます。

   `/libs/settings/workflow/notification/email/default/en.txt`

1. 必要に応じてファイルを変更します。
1. 変更内容を保存します。

テンプレートは、次のフォーマットにする必要があります。

```
subject=<text_1>
 header=<text_2>
 message=<text_3>
 footer=<text_4>
```

>[!NOTE]
>
>`<text_x>` には、静的なテキストと動的な文字列変数を混在させることができます。`<text_x>` 項目の各行の末尾には、最後のインスタンスを除き、バックスラッシュ（`\`）を付加する必要があります。バックスラッシュがないと、`<text_x>` 文字列変数の終了と見なされます。
>
>テンプレート形式について詳しくは、[Properties.load() メソッドの javadocs](https://docs.oracle.com/javase/8/docs/api/java/util/Properties.html#load-java.io.InputStream-) を参照してください。

メソッド `${payload.path.open}` を使用すると、作業項目のペイロードのパスが表示されます。例えば、Sites のページの場合、`payload.path.open` は `/bin/wcmcommand?cmd=open&path=…` と同じようなものです。これにサーバー名が抜けているのは、テンプレートによってプレフィックスとして `${host.prefix}` が付加されるためです。

メールテンプレート内では以下の変数を使用できます。

* `${event.EventType}`、イベントのタイプ。
* `${event.TimeStamp}`、イベントの日時。
* `${event.User}`、イベントをトリガーしたユーザー。
* `${initiator.home}`、イニシエーターノードのパス。

* `${initiator.name}`、イニシエーター名。

* `${initiator.email}`、イニシエーターのメールアドレス。
* `${item.id}`、作業項目の ID。
* `${item.node.id}`、この作業項目に関連付けられているワークフローモデル内のノードの ID。
* `${item.node.title}`、作業項目のタイトル
* `${participant.email}`、参加者のメールアドレス
* `${participant.name}`、参加者の名前。
* `${participant.familyName}`、参加者の姓
* `${participant.id}`、参加者の ID
* `${participant.language}`、参加者の言語
* `${instance.id}`、ワークフローの ID
* `${instance.state}`、ワークフローの状態
* `${model.title}`、ワークフローモデルのタイトル
* `${model.id}`、ワークフローモデルの ID

* `${model.version}`、ワークフローモデルのバージョン
* `${payload.data}`、ペイロード

* `${payload.type}`、ペイロードのタイプ
* `${payload.path}`、ペイロードのパス
* `${host.prefix}`、ホストのプレフィックス（例：http://localhost:4502）

### 新しい言語用の電子メールテンプレートの追加 {#adding-an-email-template-for-a-new-language}

新しい言語用のテンプレートを追加するには：

1. CRXDE で、ファイル `<language-code>.txt` を以下に追加します。

   * `/libs/settings/notification-templates/com.day.cq.wcm.core.page`：ページ通知用
   * `/etc/notification/email/default/com.day.cq.collab.forum`：フォーラム通知用
   * `/libs/settings/workflow/notification/email/default`：ワークフロー通知用

1. 言語に合わせてファイルを調整します。
1. 変更内容を保存します。

>[!NOTE]
>
>メールテンプレートのファイル名として使用される `<language-code>` は、AEM で認識できる小文字 2 文字の言語コードにする必要があります。言語コードについては、AEM は ISO-639-1 に依存しています。

## AEM Assets電子メール通知の設定 {#assetsconfig}

AEM Assetsのコレクションが共有または非共有の場合、ユーザーはAEMから電子メール通知を受け取ることができます。 電子メール通知を設定するには、次の手順に従います。

1. 電子メールサービスを設定します ( 前述の [メールサービスの設定](/help/sites-administering/notification.md#configuring-the-mail-service).
1. AEM に管理者としてログインします。**ツール**／**操作**／**Web コンソール**&#x200B;をクリックして、Web コンソール設定を開きます。
1. 編集 **Day CQ DAM Resource Collection Servlet**. 選択 **メールを送信**. 「**保存**」をクリックします。
