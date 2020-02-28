---
title: Windows 10 プレーヤーの実装
seo-title: Windows 10 プレーヤーの実装
description: 'このページでは、AEM Screens Windows 10 プレーヤーの設定について説明します。 '
seo-description: 'このページでは、AEM Screens Windows 10 プレーヤーの設定について説明します。 '
uuid: cdd7e9f1-f836-4d52-8026-80537a6623ca
contentOwner: jsyal
products: SG_EXPERIENCEMANAGER/6.4/SCREENS
topic-tags: administering
content-type: reference
discoiquuid: 9b66225a-a893-491b-b47c-ae7b3048ed80
translation-type: tm+mt
source-git-commit: c8694726dc29b391a157db3ef230f21517c957bd

---


# Windows 10 プレーヤーの実装{#implementing-windows-player}

ここでは、AEM Screens Windows 10 プレーヤーの設定について説明します。使用可能な設定ファイルやオプションと、開発およびテストに使用する設定に関する推奨事項について説明します。

## Windows プレーヤーのインストール {#installing-windows-player}

AEM Screens 用の Windows プレーヤーを実装するには、同プレーヤーをインストールしてください。

[**AEM 6.4 Player のダウンロード&#x200B;**](https://download.macromedia.com/screens/)ページにアクセスします。

### アドホック方式 {#ad-hoc-method}

最新のWindows Player(*.exe*)をインストールするアドホック方法については、 [**AEM 6.4 Playerのダウンロードページを参照してください&#x200B;**](https://download.macromedia.com/screens/)。

アプリケーションをダウンロードしたら、以下の手順に従ってプレーヤーのアドホックインストールを完了します。

1. 左上隅を長押しして、管理パネルを開きます。
1. 左のアクションメニューから「**設定**」に移動し、接続する AEM インスタンスの場所（アドレス）を入力して、「**保存**」をクリックします。

1. Click on the **Registration** link from the left action menu to complete the device registation process.

### 1 つの設定を使用した複数の Windows 10 プレーヤーの登録 {#registering-multiple-windows-players-with-one-configuration}

Windows プレーヤーをインストールしたら、1 つの設定で複数のプレーヤーを登録できます。

>[!NOTE]
>
>**Windows プレーヤーの一括登録**
>
>Windows プレーヤーを実装する場合、すべてのプレーヤーを個別に手動で設定する必要はありません。テスト済みで導入の準備ができた設定 JSON ファイルを更新することで、すべてのプレーヤーを設定できます。
>
>設定では、すべてのプレーヤーが設定ファイルで指定された同じサーバーに接続されていることが確認されます。プレーヤーの登録は個別に手動でおこなう必要があります。

Windows 10 プレーヤーを設定するには、次の手順を実行します。

1. Windows プレーヤーをインストールします。
1. 設定ファイルは ***%appdata%\com.adobe.aem.screens.player\config.json*** の下にあります。
1. 後述の情報を使用して設定 JSON を更新し、同じフォルダーをプレーヤーが存在するすべてのシステムにコピーします。

### ポリシー属性    {#policy-attributes}

次の表に、参照用のポリシー JSON の例と共にポリシー属性を示します。

| **ポリシー名** | **目的** |
|---|---|
| server | Adobe Experience Manager（AEM） サーバーの URL。 |
| resolution | デバイスの解像度。 |
| rebootSchedule | プレーヤーを再起動するスケジュール。 |
| enableAdminUI | サイト上でデバイスを設定するための Admin UI を有効にします。完全に設定されて実稼動になったら、false に設定します。 |
| enableOSD | デバイスのチャネルを切り替えるための、ユーザー用のチャネルスイッチャー UI を有効にします。完全に設定されて実稼動になったら、false に設定することを検討します。 |
| enableActivityUI | 有効にすると、ダウンロードや同期などのアクティビティの進行状況を表示します。トラブルシューティング用に有効にし、完全に設定されて実稼動になったら無効にします。 |

#### ポリシー JSON ファイルの例 {#example-policy-json-file}

```
{
    "server": "http://localhost:4502",
    "resolution": "auto",
    "rebootSchedule": "at 4:00 am",
    "enableAdminUI": false,
    "enableOSD": false,
    "enableActivityUI": false
}
```

