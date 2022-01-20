---
title: CDN にキャッシュされたコンテンツの無効化
seo-title: Invalidating your CDN cached content
description: コンテンツ配信ネットワーク（CDN）にキャッシュされたコンテンツを無効にすることで、Dynamic Media で配信されるアセットをすばやく更新できます。キャッシュが期限切れになるのを待つ必要はありません。
seo-description: Invalidating your CDN (Content Delivery Network) cached content lets you quickly update assets that are delivered by Dynamic Media, instead of waiting for the cache to expire.
uuid: 0fd88e31-9745-4c98-a245-9f5d0766cad4
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.4/ASSETS
topic-tags: dynamic-media
content-type: reference
discoiquuid: e6c9b50b-c27c-48bf-b3c0-9994e7bf6d7e
exl-id: 335c7a78-a00f-451b-8e53-225830d429c6
feature: Asset Management,CDN Cache
role: Admin,User,Developer
source-git-commit: 0120fe1303aa3b7f5aa7db39eaf40ff127f2e338
workflow-type: tm+mt
source-wordcount: '638'
ht-degree: 93%

---

# CDN にキャッシュされたコンテンツの無効化 {#invalidating-your-cdn-cached-content}

CDN を使用して Dynamic Media アセットをキャッシュすることで、高速配信が可能になります。ただし、あるアセットを更新する場合に、変更をすぐに適用したいことがあります。コンテンツ配信ネットワーク（CDN）にキャッシュされたコンテンツを無効にすることで、Dynamic Media で配信されるアセットをすばやく更新できます。キャッシュが期限切れになるのを待つ必要はありません。

[Dynamic Media Classic のキャッシュの概要](https://helpx.adobe.com/jp/experience-manager/scene7/kb/base/caching-questions/scene7-caching-overview.html)も参照してください。

**CDN にキャッシュされたコンテンツを無効化するには、次の手順を実行します。**

1. Dynamic Media Classicデスクトップアプリケーションにログインします。

   [Dynamic Media Classicデスクトップアプリケーション](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/intro/dynamic-media-classic-desktop-app.html#system-requirements-dmc-app)

   資格情報とログオンは、プロビジョニング時にアドビから付与されたものです。この情報をお持ちでない場合は、テクニカルサポートにお問い合わせください。

1. **[!UICONTROL 設定／アプリケーション設定／一般設定]**&#x200B;をクリックします。
1. アプリケーションの一般設定ページで、「サーバー」グループ見出しの下にある「**[!UICONTROL CDN 無効化テンプレート]**」テキストボックスを見つけます。

1. CDN（コンテンツ配信ネットワーク）のキャッシュの無効化に使用するテンプレートを指定します。

   例えば、次の例にあるように、特定の画像 ID ではなく、`<ID>` を参照する画像 URL（画像プリセットまたは画像の修飾子を含む）を入力するとします。

   `https://server.com/is/image/Company/<ID>?$product$`

   テンプレートに `<ID>` だけが含まれている場合は、Dynamic Media が `https://<server>/is/image` 部分を埋めます。ここで、`<server>` は、「一般設定」で定義されているパブリッシュサーバー名であり、&lt;ID> は、無効化の対象として選択されたアセット（またはアセット群）です。

1. ページの右下隅にある「**[!UICONTROL 閉じる]**」をクリックします。
1. Dynamic Media Classicデスクトップアプリケーションのユーザーインターフェイスで、1 つ以上のアセットを選択し、 **[!UICONTROL ファイル/CDN を無効にする]**. 作成したテンプレートから生成された 1 つ以上の URL と、選択したアセット（またはアセット群）からなるリストが表示されます。このリストに使用されているのは、アプリケーションの一般設定の「公開先サーバー名」にリストされているサーバー URL です。

   例えば、前の手順で設定した CDN 無効化テンプレートを使用して、`Backpack_B` という名前の画像アセットを 1 つだけ選択したとします。**[!UICONTROL ファイル／CDN を無効にする]**&#x200B;をクリックすると、CDN 無効化のユーザーインターフェイスには、次のように生成された URL が表示されます。

   `https://server.com/is/image/Company/Backpack_B?$product$`

1. URL リストボックスで「**[!UICONTROL 続行]**」をクリックして、特定の URL ごとのキャッシュを消去します。URL リストボックスでは、URL を入力または貼り付けることによって、URL を編集したり、追加したりできます。事前に CDN 無効化テンプレートを設定する必要はありません。

   「**[!UICONTROL 続行]**」をクリックすると、キャッシュの消去にかかる時間の概算を示すインジケーターが表示されます。

   複数のアセットを選択して&#x200B;**[!UICONTROL ファイル／CDN を無効にする]**&#x200B;をクリックした場合、保存された&#x200B;**[!UICONTROL テンプレートの URL]** の各アセットが参照されます。したがって、Web サイトで参照される各 URL の画像プリセット（製品の詳細、検索結果など）を参照する **[!UICONTROL CDN 無効化テンプレート]**&#x200B;を定義できます。これにより、キャッシュの無効化の対象として 1 つ以上の画像を選択したときに、それらの URL が自動的にインターフェイスに入力されます。

   >[!NOTE]
   >
   >アセットを選択して&#x200B;**[!UICONTROL ファイル／CDN を無効にする]**&#x200B;をクリックすると、Dynamic Media が CDN 無効化テンプレートを使用して、コンテンツ配信ネットワーク（CDN）内の無効化する URL 群を自動的に作成します。「**[!UICONTROL CDN 無効化テンプレート]**」テキストボックスに何も入力していないと、空白の URL リストが返されます。CDN におけるキャッシュは、アセットベースではありません。URL ベースです。したがって、Web サイト上での完全な URL を認識しておく必要があります。URL を特定した後は、上記の手順で、それらの URL を「**[!UICONTROL CDN 無効化テンプレート]**」テキストボックスに追加できます。これにより、アセットを選択し、ワンステップで URL を無効化することができます。
   >
   >もう 1 つのオプションとして、完全な URL を **[!UICONTROL CDN 無効化]**&#x200B;リストに追加する方法があります。この方法に従う場合は、**[!UICONTROL ファイル／CDN を無効にする]**&#x200B;オプションに進む前に Dynamic Media Classic でアセットを選択する必要はありません。
