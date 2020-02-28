---
title: アセットのリンク共有
description: AEM Assets内のアセット、フォルダー、コレクションを外部関係者へのURLとして共有する方法。
contentOwner: AG
translation-type: tm+mt
source-git-commit: 0d70a672a2944e2c03b54beb3b5f734136792ab1

---


# アセットのリンク共有 {#asset-link-sharing}

Adobe Experience Manager（AEM）Assets では、アセット、フォルダーおよびコレクションを URL として、組織内や外部（パートナー、ベンダーを含む）のメンバーと共有できます。リンクを使用したアセットの共有は、AEM Assetsに最初にログインしなくても、外部のユーザーがリソースを利用できるようにする便利な方法です。

>[!NOTE]
>
>リンクとして共有するフォルダーとアセットに対するACLの編集権限が必要です。

## アセットの共有 {#share-assets}

ユーザーと共有するアセットの URL を生成するには、リンク共有ダイアログを使用します。Users with administrator privileges or with read permissions at `/var/dam/share` location are able to view the links shared with them.

>[!NOTE]
>
>Before you share a link with users, ensure that [!UICONTROL Day CQ Mail Service] is configured. [Day CQ Mail Service を設定](link-sharing.md#configure-day-cq-mail-service)せずにリンクの共有を試行すると、エラーが発生します。

1. Assets のユーザーインターフェイスで、リンクとして共有するアセットを選択します。
1. From the toolbar, click/tap the **[!UICONTROL Share Link]** ![assets share icon](assets/assets_share.png).

   An asset link is auto-created in the **[!UICONTROL Share Link]** field. このリンクをコピーしてユーザーと共有します。リンクのデフォルトの有効期間は 1 日です。

   ![「リンクを共有」と表示されたダイアログ](assets/chlimage_1-542.png)

   または、この手順の 3～7 に進んで電子メールの受信者を追加し、リンクの有効期限を設定して、ダイアログから送信することもできます。

   >[!NOTE]
   >
   >AEM作成者から外部エンティティへのリンクを共有するには、GETリクエストのリンク共有に使用される次のURLのみを公開します。 他のURLをブロックして、AEMのデプロイメントがセキュリティで保護されていることを確認します。
   >
   >* &lt;AEM Server>/linkshare.html
   * &lt;AEM Server>/linksharepreview.html
   * &lt;AEM Server>/linkexpired.html


   >[!NOTE]
   共有アセットが別の場所に移動されると、そのリンクは機能しなくなります。リンクを再作成し、ユーザーと再共有します。

1. Web コンソールで、**[!UICONTROL Day CQ Link Externalizer]** 設定を開き、「**[!UICONTROL ドメイン]**」フィールドで次のプロパティの値をそれぞれ変更します。

   * local
   * author
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

   ![共有リンクの有効期限の設定](assets/chlimage_1-544.png)

1. ユーザーが元の画像をレンディションと共にダウンロードすることを許可するには、「**[!UICONTROL 元のファイルのダウンロードを許可]**」を選択します。

   >[!NOTE]
   デフォルトでは、ユーザーはリンクとして共有されているアセットのレンディションのみをダウンロードできます。

1. 「**[!UICONTROL 共有]**」をクリックします。リンクが電子メールによってユーザーと共有されることを確認するメッセージが表示されます。
1. 共有アセットを表示するには、ユーザーに送信された電子メールのリンクをクリックまたはタップします。共有アセットが [!UICONTROL Adobe Marketing Cloud] ページに表示されます。

   ![共有アセットはAdobe Marketing cloudで使用できます](assets/chlimage_1-545.png)

   リスト表示に切り替えるには、ツールバーのレイアウトアイコンをクリックまたはタップします。

1. アセットのプレビューを生成するには、共有アセットをクリックまたはタップします。Click/tap **[!UICONTROL Back]** on the toolbar to close the preview and return to the [!UICONTROL Marketing Cloud] page. フォルダーを共有している場合は、「**[!UICONTROL 親フォルダー]**」をクリックまたはタップして親フォルダーに戻ります。

   ![chlimage_1-546](assets/chlimage_1-546.png)

   >[!NOTE]
   AEM は、これらの MIME タイプ（JPG、PNG、GIF、BMP、INDD、PDF、および PPT）のアセットのプレビューの生成をサポートしています。他の MIME タイプのアセットのみをダウンロードできます。

1. To download the shared asset, click/tap the **[!UICONTROL Select]** icon from the toolbar, click/tap the asset, and then click/tap **[!UICONTROL Download]** from the toolbar.

   ![共有アセットをダウンロードするツールバーオプション](assets/chlimage_1-547.png)

1. リンクとして共有したアセットを表示するには、Assets の UI に移動し、**[!UICONTROL グローバルナビゲーション]**&#x200B;アイコンをクリックまたはタップします。Choose **[!UICONTROL Navigation]** from the list to display the Navigation pane.
1. ナビゲーションウィンドウで、「**[!UICONTROL 共有リンク]**」を選択して共有アセットのリストを表示します。
1. To unshare an asset, select it and tap/click **[!UICONTROL Unshare]** from the toolbar. アセットを共有しないことを確認するメッセージが表示されます。また、このアセットの項目がリストから削除されます。

## Day CQ Mail Service の設定 {#configure-day-cq-mail-service}

1. AEM のロゴをクリックまたはタップし、**[!UICONTROL ツール／操作／Web コンソール]**&#x200B;に移動します。
1. サービスのリストから、**[!UICONTROL Day CQ Mail Service]** を探します。
1. サービスの横の&#x200B;**[!UICONTROL 編集]**&#x200B;アイコンをクリックして、**[!UICONTROL Day CQ Mail Service]** のパラメーターを次のように設定します。

   * SMTP server host name：電子メールサーバーのホスト名
   * SMTP server port：電子メールサーバーのポート
   * SMTP user：メールサーバーのユーザー名
   * SMTP password：電子メールサーバーのパスワード
   ![chlimage_1-548](assets/chlimage_1-548.png)

1. 「**[!UICONTROL 保存]**」をクリックまたはタップします。

## 最大データサイズの設定 {#configure-maximum-data-size}

リンク共有機能を使用して共有されているリンクからアセットをダウンロードすると、AEM は、リポジトリのアセットの階層全体を圧縮して、ZIP ファイルとしてアセットを返します。ただし、ZIP ファイルとして圧縮できるデータ量に制限がないと、膨大なデータが圧縮の対象となり、JVM のメモリ不足エラーの原因となります。To secure the system from a potential denial of service attack due to this situation, configure the maximum size using the **[!UICONTROL Max Content Size (uncompressed)]** parameter for **[!UICONTROL Day CQ DAM Adhoc Asset Share Proxy Servlet]** in Configuration Manager. アセットの未圧縮時のサイズが設定値を超えていると、アセットのダウンロード要求は拒否されます。デフォルト値は 100 MB です。

1. AEM のロゴをクリックまたはタップし、**[!UICONTROL ツール／操作／Web コンソール]**&#x200B;に移動します。
1. From the web console, locate the **[!UICONTROL Day CQ DAM Adhoc Asset Share Proxy Servlet]** configuration.
1. 「**[!UICONTROL Day CQ DAM Adhoc Asset Share Proxy Servlet]**」設定を編集モードで開き、「**[!UICONTROL 最大コンテンツサイズ（非圧縮）]**」パラメーターの値を変更します。

   ![chlimage_1-549](assets/chlimage_1-549.png)

1. 変更内容を保存します。

## ベストプラクティスとトラブルシューティング {#best-practices-and-troubleshooting}

* 名前に空白を含むアセットフォルダーまたはコレクションは共有されない場合があります。
* ユーザーが共有アセットをダウンロードできない場合は、AEM 管理者に[ダウンロード制限](#configure-maximum-data-size)を確認してください。
* 共有アセットへのリンクを含むメールを送信できない場合、または他のユーザーがお客様からのメールを受信できない場合、AEM 管理者に[メールサービス](#configure-day-cq-mail-service)が構成されているかどうかを確認してください。
* リンク共有機能を使用してアセットを共有できない場合は、適切な権限を持っていることを確認してください。[アセットの共有](#share-assets)を参照してください。
