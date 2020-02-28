---
title: デバイスの登録
seo-title: デバイスの登録
description: ここでは、AEM Screens プロジェクトでのデバイス登録プロセスについて説明します。
seo-description: ここでは、AEM Screens プロジェクトでのデバイス登録プロセスについて説明します。
uuid: babf0de1-1f39-4e22-82aa-ce7fa7052659
contentOwner: jsyal
products: SG_EXPERIENCEMANAGER/6.4/SCREENS
content-type: reference
topic-tags: administering
discoiquuid: a1534cfd-66a1-4e28-8938-e09a24dec8ee
translation-type: tm+mt
source-git-commit: 3addef2141ebb831f8677d011d68faf88e648dc2

---


# デバイスの登録{#device-registration}

ここでは、AEM Screens プロジェクトでのデバイス登録プロセスについて説明します。

## デバイスの登録 {#registering-a-device}

デバイス登録プロセスには、次に示す 2 台のコンピューターを使用します。

* 実際に登録するデバイス（サイネージディスプレイなど）
* デバイスの登録に使用する AEM サーバー

>[!NOTE]
>
>最新の Windows プレーヤー（*.exe*）を [**AEM Screens Player Downloads **](https://download.macromedia.com/screens/)ページからダウンロードしたら、以下の手順に従ってプレーヤーのアドホックインストールを完了します。
>
>1. 左上隅を長押しして、管理パネルを開きます。
>1. 左のアクションメニューから「**設定**」に移動し、AEM インスタンスの場所のアドレスを「**サーバー**」に入力して、「**保存**」をクリックします。
   >
   >
1. 左のアクションメニューの「**登録**」リンクをクリックし、以下の手順でデバイス登録プロセスを完了します。
>



![screen_shot_2018-11-26at12118pm](assets/screen_shot_2018-11-26at12118pm.png)

1. デバイスで AEM Screens プレーヤーを起動します。登録用の UI が表示されます。

   ![screen_shot_2018-11-26at104230am](assets/screen_shot_2018-11-26at104230am.png)

1. AEM で、プロジェクトの&#x200B;**デバイス**&#x200B;フォルダーに移動します。

   >[!NOTE]
   >
   >AEM ダッシュボードで Screens の新しいプロジェクトを作成する方法について詳しくは、[Screens プロジェクトの作成と管理](/help/screens/creating-a-screens-project.md)を参照してください。

1. アクションバーの「**デバイスマネージャー**」ボタンをタップまたはクリックします。

   ![screen_shot_2018-11-26at104702am](assets/screen_shot_2018-11-26at104702am.png)

1. 右上にある「**デバイスの登録**」ボタンをタップまたはクリックします。

   ![screen_shot_2018-11-26at104815am](assets/screen_shot_2018-11-26at104815am.png)

1. 目的の（手順 1 と同じ）デバイスを選択し、「**デバイスを登録**」をタップまたはクリックします。

   ![screen_shot_2018-11-26at105112am](assets/screen_shot_2018-11-26at105112am.png)

1. AEM で、デバイスから登録コードが送信されるのを待機します。

   ![screen_shot_2018-11-26at105150am](assets/screen_shot_2018-11-26at105150am.png)

1. デバイスで、**登録コード**&#x200B;を確認します。

   ![screen_shot_2018-11-26at105227am](assets/screen_shot_2018-11-26at105227am.png)

1. 両方のコンピューターの&#x200B;**登録コード**&#x200B;が同じである場合は、AEM の「**検証**」ボタンをタップまたはクリックします（手順 6 を参照）。
1. デバイスの名前を設定し、「登録」をクリック選択します。

   ![screen_shot_2018-11-26at105357am](assets/screen_shot_2018-11-26at105357am.png)

1. 「完了」をタップまたはクリックして、登録プロセスを完了します。

   ![screen_shot_2018-11-26at105456am](assets/screen_shot_2018-11-26at105456am.png)

   >[!NOTE]
   >
   >「**戻る**」をタップまたはクリックすると、新しいデバイスを登録できます。
   >
   >「**ディスプレイを割り当て**」をタップまたはクリックすると、デバイスをディスプレイに直接追加できます。

   「**完了**」をタップまたはクリックする場合は、デバイスをディスプレイに割り当てる必要があります。

   ![screen_shot_2018-11-26at105740am](assets/screen_shot_2018-11-26at105740am.png)

   >[!NOTE]
   >
   >Screens プロジェクトのディスプレイの作成と管理について詳しくは、[ディスプレイの作成と管理](/help/screens/managing-displays.md)を参照してください。

### ディスプレイへのデバイスの割り当て {#assigning-device-to-a-display}

デバイスをディスプレイにまだ割り当てていない場合は、以下の手順に従って、デバイスを AEM Screens プロジェクト内のディスプレイに割り当てます。

1. デバイスを選択し、アクションバーの「**デバイスを割り当て**」をクリックします。

   ![screen_shot_2018-11-26at111026am](assets/screen_shot_2018-11-26at111026am.png)

1. 「**ディスプレイ / デバイス設定パス**」でディスプレイのパスを選択します。

   ![screen_shot_2018-11-26at111252am](assets/screen_shot_2018-11-26at111252am.png)

1. パスを選択したら、「**割り当て**」をクリックします。

   ![screen_shot_2018-11-26at111722am](assets/screen_shot_2018-11-26at111722am.png)

1. デバイスが正常に割り当てられたら、「**完了**」をクリックします（下図を参照）。

   ![screen_shot_2018-11-26at112041am](assets/screen_shot_2018-11-26at112041am.png)

   また、「**完了**」をクリックすると、ディスプレイダッシュボードが表示されます。

   ![screen_shot_2018-11-26at112154am](assets/screen_shot_2018-11-26at112154am.png)

## デバイスの登録の制限  {#limitations-on-device-registration}

システム全体のユーザーパスワードの制限により、デバイスの登録に失敗することがあります。デバイスの登録では、デバイスのユーザーを作成するためにランダム生成されたパスワードが使用されます。

このパスワードが *AuthorizableActionProvider* 設定により制限されている場合は、デバイスのユーザーの作成に失敗することがあります。

>[!NOTE]
>
>現在生成されるランダムパスワードは、33 ～ 122 の範囲の 36 文字の ASCII 文字で構成されています（ほとんどすべての特殊文字が含まれます）。

```java
25.09.2016 16:54:03.140 *ERROR* [59.100.121.82 [1474844043109] POST /content/screens/svc/registration HTTP/1.1] com.adobe.cq.screens.device.registration.impl.RegistrationServlet Error during device registration
javax.jcr.nodetype.ConstraintViolationException: Password violates password constraint (^(?=.*\d).{7,9}$).
        at org.apache.jackrabbit.oak.spi.security.user.action.PasswordValidationAction.validatePassword(PasswordValidationAction.java:105)
        at org.apache.jackrabbit.oak.spi.security.user.action.PasswordValidationAction.onPasswordChange(PasswordValidationAction.java:76)
        at org.apache.jackrabbit.oak.security.user.UserManagerImpl.onPasswordChange(UserManagerImpl.java:308)
```

### その他のリソース {#additional-resources}

AEM Screens Player について詳しくは、[AEM Screens Player](/help/screens/working-with-screens-player.md) を参照してください。
