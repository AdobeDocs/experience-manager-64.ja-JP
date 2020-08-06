---
title: アセットのリンク共有
description: アセット、フォルダー、コレクションをAEM Assets内で外部の関係者へのURLとして共有する方法。
contentOwner: AG
translation-type: tm+mt
source-git-commit: 0d70a672a2944e2c03b54beb3b5f734136792ab1
workflow-type: tm+mt
source-wordcount: '1226'
ht-degree: 83%

---


# アセットのリンク共有 {#asset-link-sharing}

Adobe Experience Manager（AEM）Assets では、アセット、フォルダーおよびコレクションを URL として、組織内や外部（パートナー、ベンダーを含む）のメンバーと共有できます。リンクによるアセットの共有は、外部の関係者が AEM Assets にログインすることなくリソースを利用するための便利な方法です。

>[!NOTE]
>
>リンクとして共有するフォルダーとアセットに対するACLの編集権限が必要です。

## アセットの共有 {#share-assets}

ユーザーと共有するアセットの URL を生成するには、リンク共有ダイアログを使用します。`/var/dam/share` の場所への管理者特権または読み取り権限を持つユーザーが、共有されたリンクを表示することができます。

>[!NOTE]
>
>Before you share a link with users, ensure that [!UICONTROL Day CQ Mail Service] is configured. [Day CQ Mail Service を設定](link-sharing.md#configure-day-cq-mail-service)せずにリンクの共有を試行すると、エラーが発生します。

1. Assets のユーザーインターフェイスで、リンクとして共有するアセットを選択します。
1. From the toolbar, click/tap the **[!UICONTROL Share Link]** ![assets share icon](assets/assets_share.png).

   「**[!UICONTROL リンクを共有]**」フィールドにアセットリンクが自動的に作成されます。このリンクをコピーしてユーザーと共有します。リンクのデフォルトの有効期間は 1 日です。

   ![「リンクを共有」と表示されたダイアログ](assets/chlimage_1-542.png)

   または、この手順の 3～7 に進んで電子メールの受信者を追加し、リンクの有効期限を設定して、ダイアログから送信することもできます。

   >[!NOTE]
   >
   >AEM作成者から外部エンティティへのリンクを共有するには、GETリクエストのリンク共有に使用される次のURLのみを公開します。 AEMのデプロイメントが安全であることを確認するために、他のURLをブロックします。
   >
   >* &lt;AEM Server>/linkshare.html
   * &lt;AEM Server>/linksharepreview.html
   * &lt;AEM Server>/linkexpired.html


   >[!NOTE]
   共有アセットが別の場所に移動されると、そのリンクは機能しなくなります。リンクを再作成し、ユーザーと再共有します。

1. Web コンソールで、**[!UICONTROL Day CQ Link Externalizer]** 設定を開き、「**[!UICONTROL Domains]**」フィールドの次のプロパティの値をそれぞれ変更します。

   * local
   * 作成者
   * publish

   For the `local` and `author` properties, provide the URL for the local and author instance respectively. Both `local` and `author` properties have the same value if you run a single AEM author instance. For `publish`, provide the URL for the publish instance.

1. **[!UICONTROL リンク共有]**&#x200B;ダイアログの電子メールアドレスボックスに、リンクを共有するユーザーの電子メール ID を入力します。このリンクを複数のユーザーと共有することもできます。

   ユーザーが組織内のメンバーの場合は、入力領域の下のリストに表示される電子メール ID の候補から、ユーザーの電子メール ID を選択します。外部ユーザーの場合は、完全な電子メール ID を入力してリストから選択します。

   ユーザーへの電子メールの送信を有効にするには、[Day CQ Mail Service](link-sharing.md#configure-day-cq-mail-service) で SMTP サーバーの詳細を設定します。

   ![アセットへのリンクをリンク共有ダイアログから直接共有する](assets/chlimage_1-543.png)

   アセットへのリンクをリンク共有ダイアログから直接共有する

   >[!NOTE]
   組織内のメンバーではないユーザーの電子メール ID を入力した場合、ユーザーの電子メール ID に「外部ユーザー」というプレフィックスが付けられます。

1. 「**[!UICONTROL 件名]**」ボックスに、共有するアセットの件名を入力します。
1. 「**[!UICONTROL メッセージ]**」ボックスに、オプションでメッセージを入力します。
1. 「**[!UICONTROL 有効期限]**」フィールドに、日付選択を使用してリンクの有効期限の日付と時間を指定します。デフォルトでは、有効期限日はリンクを共有した日から 1 週間後に設定されます。

   ![共有リンクの有効期限の日時を設定する](assets/chlimage_1-544.png)

1. ユーザーが元の画像をレンディションと共にダウンロードすることを許可するには、「**[!UICONTROL 元のファイルのダウンロードを許可]**」を選択します。

   >[!NOTE]
   デフォルトでは、ユーザーはリンクとして共有されているアセットのレンディションのみをダウンロードできます。

1. 「**[!UICONTROL 共有]**」をクリックします。リンクが電子メールによってユーザーと共有されることを確認するメッセージが表示されます。
1. 共有アセットを表示するには、ユーザーに送信された電子メールのリンクをクリックまたはタップします。共有アセットが [!UICONTROL Adobe Marketing Cloud] ページに表示されます。

   ![共有アセットはAdobe Marketing Cloudで利用可能](assets/chlimage_1-545.png)

   リスト表示に切り替えるには、ツールバーのレイアウトアイコンをクリックまたはタップします。

1. アセットのプレビューを生成するには、共有アセットをクリックまたはタップします。Click/tap **[!UICONTROL Back]** on the toolbar to close the preview and return to the [!UICONTROL Marketing Cloud] page. フォルダーを共有している場合は、「**[!UICONTROL 親フォルダー]**」をクリックまたはタップして親フォルダーに戻ります。

   ![chlimage_1-546](assets/chlimage_1-546.png)

   >[!NOTE]
   AEM は、これらの MIME タイプ（JPG、PNG、GIF、BMP、INDD、PDF、および PPT）のアセットのプレビューの生成をサポートしています。他の MIME タイプのアセットのみをダウンロードできます。

1. To download the shared asset, click/tap the **[!UICONTROL Select]** icon from the toolbar, click/tap the asset, and then click/tap **[!UICONTROL Download]** from the toolbar.

   ![共有アセットをダウンロードするツールバーオプション](assets/chlimage_1-547.png)

1. リンクとして共有したアセットを表示するには、Assets の UI に移動し、**[!UICONTROL グローバルナビゲーション]**&#x200B;アイコンをクリックまたはタップします。リストから「**[!UICONTROL ナビゲーション]**」を選択して、ナビゲーションウィンドウを表示します。
1. ナビゲーションウィンドウで、「**[!UICONTROL 共有リンク]**」を選択して共有アセットのリストを表示します。
1. To unshare an asset, select it and tap/click **[!UICONTROL Unshare]** from the toolbar. アセットを共有しないことを確認するメッセージが表示されます。また、このアセットの項目がリストから削除されます。

## Day CQ Mail Service の設定 {#configure-day-cq-mail-service}

1. AEM のロゴをクリックまたはタップし、**[!UICONTROL ツール／運営／Web コンソール]**&#x200B;に移動します。
1. サービスのリストから、**[!UICONTROL Day CQ Mail Service]** を探します。
1. サービスの横の&#x200B;**[!UICONTROL 編集]**&#x200B;アイコンをクリックして、**[!UICONTROL Day CQ Mail Service]** のパラメーターを次のように設定します。

   * SMTP server host name：電子メールサーバーのホスト名
   * SMTP server port：電子メールサーバーのポート
   * SMTP user：メールサーバーのユーザー名
   * SMTP password：電子メールサーバーのパスワード

   ![chlimage_1-548](assets/chlimage_1-548.png)

1. 「**[!UICONTROL 保存]**」をクリックまたはタップします。

## 最大データサイズの設定 {#configure-maximum-data-size}

リンク共有機能を使用して共有されているリンクからアセットをダウンロードすると、AEM は、リポジトリのアセットの階層全体を圧縮して、ZIP ファイルとしてアセットを返します。ただし、ZIP ファイルとして圧縮できるデータ量に制限がないと、膨大なデータが圧縮の対象となり、JVM のメモリ不足エラーの原因となります。この状況による潜在的な DoS 攻撃からシステムを保護するには、Configuration Manager で Day CQ DAM Adhoc Asset Share Proxy Servlet の「**[!UICONTROL Max Content Size (uncompressed)]**」パラメーターを使用して、最大サイズを設定します。****&#x200B;アセットの未圧縮時のサイズが設定値を超えていると、アセットのダウンロード要求は拒否されます。デフォルト値は 100 MB です。

1. AEM のロゴをクリックまたはタップし、**[!UICONTROL ツール／運営／Web コンソール]**&#x200B;に移動します。
1. Web コンソールで、「**[!UICONTROL Day CQ DAM Adhoc Asset Share Proxy Servlet]**」設定を見つけます。
1. 「**[!UICONTROL Day CQ DAM Adhoc Asset Share Proxy Servlet]**」設定を編集モードで開き、「**[!UICONTROL Max Content Size (uncompressed)]**」パラメーターの値を変更します。

   ![chlimage_1-549](assets/chlimage_1-549.png)

1. 変更内容を保存します。

## ベストプラクティスとトラブルシューティング {#best-practices-and-troubleshooting}

* 名前に空白を含むアセットフォルダーまたはコレクションは共有されない場合があります。
* ユーザーが共有アセットをダウンロードできない場合は、AEM 管理者に[ダウンロード制限](#configure-maximum-data-size)を確認してください。
* 共有アセットへのリンクを含むメールを送信できない場合、または他のユーザーがお客様からのメールを受信できない場合、AEM 管理者に[メールサービス](#configure-day-cq-mail-service)が構成されているかどうかを確認してください。
* リンク共有機能を使用してアセットを共有できない場合は、適切な権限を持っていることを確認してください。[アセットの共有](#share-assets)を参照してください。
