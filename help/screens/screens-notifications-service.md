---
title: AEM Screens 通知サービス
seo-title: AEM Screens 通知サービス
description: デバイスのアクティビティを監視する方法の詳細について説明します。
seo-description: デバイスのアクティビティを監視する方法の詳細について説明します。
uuid: 9843219d-ed39-4e4f-bef4-e500528ff9f1
contentOwner: jsyal
content-type: reference
products: SG_EXPERIENCEMANAGER/6.4/SCREENS
topic-tags: authoring
discoiquuid: 8879e510-4f0e-46da-87d2-77c5aaacb26e
translation-type: tm+mt
source-git-commit: cdec5b3c57ce1c80c0ed6b5cb7650b52cf9bc340

---


# AEM Screens 通知サービス {#aem-screens-notifications-service}

<!--removed from metadata: admitteddomains: @adobe.com;@caesars.com-->

***AEM Screens 通知サービス***&#x200B;では、デバイスのアクティビティを監視できる機能について説明します。

ここでは、以下のトピックについて説明します。

* **概要**
* **電子メールの設定**
* **電子メール通知**
* **使用例**

>[!CAUTION]
>
>この AEM Screens 機能は、AEM 6.3.2 機能パック 3 または AEM 6.4.1 Screens 機能パック 1 がインストールされている場合にのみ使用できます。
>
>この機能パックにアクセスするには、アドビサポートに連絡してアクセス権をリクエストする必要があります。アクセス権が付与されると、パッケージ共有から機能パックをダウンロードできるようになります。

## 概要 {#overview}

***AEM Screens 通知サービス***&#x200B;を使用すると、設定可能な期間 AEM Screens Player が ping を送信しなかった場合、それを知らせる電子メールを管理者が受信できます。

このサービスは OSGi Web コンソールで設定できます。

## 電子メールの設定 {#configuring-email-settings}

電子メール通知を設定するには、以下の手順に従います。

1. **Adobe Experience Manager Web コンソール設定**&#x200B;が開きます。
1. **Screens Device Email Monitoring Service** を開きます。

   ![screen_shot_2018-04-26at44602pm](assets/screen_shot_2018-04-26at44602pm.png)

1. 以下のフィールドを定義して、電子メールの設定を指定します。

   **デバイスパス**：監視する Screens プロジェクトへのパスを入力します。パスは通常、`/home/users/screens/<Name of your project>` です。

   例えば、プロジェクトが **We.Retail** の場合、プロジェクトのパスは ***/home/users/screens/we-retail*** になります。

   >[!NOTE]
   >
   >デバイスユーザーがアクセスするプロジェクトパスを指定します。

   **スケジュールの頻度**：このモニターが電子メールを送信する時刻（例：午後 5 時または 17 時）または頻度（時間単位、例：1）を指定します。

   **ping タイムアウト**：デバイスが到達不能と見なされるまでの経過時間を分単位で指定します。

   **SMTP サーバー**：電子メールの送信に使用する SMTP サーバーを指定します。

   **SMTP ポート**：SMTP ポートを入力します。

   **TLS を使用**：TLS（Transport Layer Security）を使用すると、SMTP サーバーとの安全な通信をおこなえます。

   会社のメールサーバーとの安全な接続には、TLS を使用することをお勧めします。適切な値については、メール管理者に確認してください。

   **ユーザー名**：電子メールを送信する際のユーザー名を指定します。

   **パスワード**：電子メールを送信する際のパスワードを指定します。

   **受信者**：受信者の電子メールアドレスを指定します。

   >[!NOTE]
   >
   >入力できる電子メールアドレスは 1 つだけです。一括電子メールを送信するには、該当するユーザーのグループつまり配布リストを作成します。

1. 「**保存**」をクリックして、AEM Screens デバイスの電子メールを使用した監視アクティビティを設定します。

## 電子メール通知 {#email-notification}

電子メール通知の設定をおこなうと、無操作状態が報告された実際のデバイスへのリンクを記載した電子メール通知が届きます。

このリンクにアクセスすると、デバイスのダッシュボードに直接移動します。

指定した ping タイムアウトの時間内に ping を送信せず、電子メールの生成時にもまだ ping を送信していないデバイスが 1 つ以上ある場合にのみ、電子メールが送信されます。

### 使用例 {#example-use-cases}

次の例では、Screens Device Email Monitoring Service のプロパティを設定するシナリオを参考までにいくつか示します。

**シナリオ 1**：

スケジュールの頻度を午前 1 時、ping タイムアウトを 60 分に設定した場合、Screens デバイスが午前 12 時から午後 1 時まで ping を送信しなければ、デバイスが無操作状態であることを確認する電子メール通知が届きます。

**シナリオ 2**：

スケジュールの頻度を 1 時間、ping タイムアウトを 60 分に設定した場合、Screens デバイスが任意の 1 時間に ping を送信しなければ、デバイスが無操作状態であることを確認する電子メール通知が届きます。
