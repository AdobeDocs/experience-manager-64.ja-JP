---
title: CDN にキャッシュされたコンテンツの無効化
seo-title: CDN にキャッシュされたコンテンツの無効化
description: コンテンツ配信ネットワーク（CDN）にキャッシュされたコンテンツを無効にすることで、Dynamic Media で配信されるアセットをすばやく更新できます。キャッシュが期限切れになるのを待つ必要はありません。
seo-description: コンテンツ配信ネットワーク（CDN）にキャッシュされたコンテンツを無効にすることで、Dynamic Media で配信されるアセットをすばやく更新できます。キャッシュが期限切れになるのを待つ必要はありません。
uuid: 0fd88e31-9745-4c98-a245-9f5d0766cad4
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.4/ASSETS
topic-tags: dynamic-media
content-type: reference
discoiquuid: e6c9b50b-c27c-48bf-b3c0-9994e7bf6d7e
translation-type: tm+mt
source-git-commit: e2bb2f17035e16864b1dc54f5768a99429a3dd9f

---


# CDN にキャッシュされたコンテンツの無効化 {#invalidating-your-cdn-cached-content}

CDN を使用して Dynamic Media アセットをキャッシュすることで、高速配信が可能になります。ただし、アセットを更新する場合は、その変更をすぐに有効にする必要がある場合があります。 コンテンツ配信ネットワーク（CDN）にキャッシュされたコンテンツを無効にすることで、Dynamic Media で配信されるアセットをすばやく更新できます。キャッシュが期限切れになるのを待つ必要はありません。

ダイナミックメ [ディアクラシック(Scene7)のキャッシュの概要も参照してください](https://helpx.adobe.com/experience-manager/scene7/kb/base/caching-questions/scene7-caching-overview.html)。

**CDN にキャッシュされたコンテンツを無効化するには、次の手順を実行します。**

1. 次のページから、Dynamic Media Classic（Scene7）アカウントにログオンします。

   [https://www.adobe.com/marketing-cloud/experience-manager/scene7-login.html](https://www.adobe.com/marketing-cloud/experience-manager/scene7-login.html)

   資格情報とログオンは、プロビジョニング時にアドビから付与されたものです。この情報をお持ちでない場合は、テクニカルサポートにお問い合わせください。

1. **[!UICONTROL 設定／アプリケーション設定／一般設定]**&#x200B;をクリックします。
1. On the Application General Settings page, under the Servers group heading, locate the **[!UICONTROL CDN Invalidation Template]** text box.

1. CDN（コンテンツ配信ネットワーク）のキャッシュの無効化に使用するテンプレートを指定します。

   For example, suppose you enter an image URL (including image presets or modifiers) referencing `<ID>`, instead of a specific image ID as in the following example:

   `https://server.com/is/image/Company/<ID>?$product$`

   If the Template just contains `<ID>`, then Dynamic Media fills in `https://<server>/is/image` where `<server>` is the Publish Server Name that is defined in General Settings and &lt;ID> is the asset(s) selected to be invalidated.

1. ページの右下隅にある「**[!UICONTROL 閉じる]**」をクリックします。
1. Dynamic Media Classic（Scene7）の UI で、1 つ以上のアセットを選択し、**[!UICONTROL ファイル／CDN を無効にする]**&#x200B;をクリックします。作成したテンプレートから生成された 1 つ以上の URL と、選択したアセット（またはアセット群）からなるリストが表示されます。このリストに使用されているのは、アプリケーションの全般設定の「公開先サーバー名」にリストされているサーバー URL です。

   例えば、前の手順で設定した CDN 無効化テンプレートを使用して、`Backpack_B` という名前の画像アセットを 1 つだけ選択したとします。**[!UICONTROL ファイル／CDN を無効にする]**&#x200B;をクリックすると、CDN 無効化のユーザーインターフェイスには、次のように生成された URL が表示されます。

   `https://server.com/is/image/Company/Backpack_B?$product$`

1. URL リストボックスで「**[!UICONTROL 続行]**」をクリックして、特定の URL ごとのキャッシュを消去します。URL リストボックスでは、URL を入力または貼り付けることによって、URL を編集したり、追加したりできます。事前に CDN 無効化テンプレートを設定する必要はありません。

   「**[!UICONTROL 続行]**」をクリックすると、キャッシュの消去にかかる時間の概算を示すインジケーターが表示されます。

   複数のアセットを選択して&#x200B;**[!UICONTROL ファイル／CDN を無効にする]**&#x200B;をクリックした場合、保存された&#x200B;**[!UICONTROL テンプレートの URL]** の各アセットが参照されます。したがって、各 URL の画像プリセット（製品の詳細、検索結果など）を参照する **[!UICONTROL CDN 無効化テンプレート]**&#x200B;を定義し、その画像プリセットを Web サイトで参照できます。これにより、キャッシュの無効化の対象として 1 つ以上の画像を選択したときに、それらの URL が自動的にインターフェイスに入力されます。

   >[!NOTE]
   >
   >アセットを選択して&#x200B;**[!UICONTROL ファイル／CDN を無効にする]**&#x200B;をクリックすると、Dynamic Media が CDN 無効化テンプレートを使用して、コンテンツ配信ネットワーク（CDN）内の無効化する URL 群を自動的に作成します。「**[!UICONTROL CDN 無効化テンプレート]**」テキストボックスに何も入力していないと、空白の URL リストが返されます。CDN におけるキャッシュは、アセットベースではありません。URL ベースです。したがって、Web サイト上での完全な URL を認識しておく必要があります。URL を特定した後は、手順の早い段階で、それらの URL を「**[!UICONTROL CDN 無効化テンプレート]**」テキストボックスに追加できます。これにより、アセットを選択し、ワンステップで URL を無効化することができます。
   >
   >Another option is to add complete URLs to the **[!UICONTROL Invalidate CDN]** list. この方法に従う場合は、**[!UICONTROL ファイル／CDN を無効にする]**&#x200B;オプションに進む前に Dynamic Media Classic でアセットを選択する必要はありません。

