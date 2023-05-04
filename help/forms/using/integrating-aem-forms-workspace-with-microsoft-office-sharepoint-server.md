---
title: AEM Forms Workspace に Microsoft Office SharePoint Server を統合する
seo-title: Integrating AEM forms workspace with Microsoft Office SharePoint Server
description: AEM forms workspace をMicrosoft Office SharePoint Server と統合できます。
seo-description: You can integrate AEM forms workspace with Microsoft Office SharePoint Server.
uuid: d43396d4-117f-47ea-91e4-10ee96107bc8
content-type: reference
products: SG_EXPERIENCEMANAGER/6.4/FORMS
topic-tags: Configuration
discoiquuid: 1bada670-3e0e-40f4-b9be-8b090df910be
exl-id: 43149456-8ff8-4ce1-9c51-1d950f60ff5d
source-git-commit: c5b816d74c6f02f85476d16868844f39b4c47996
workflow-type: tm+mt
source-wordcount: '591'
ht-degree: 17%

---

# AEM Forms Workspace に Microsoft Office SharePoint Server を統合する {#integrating-aem-forms-workspace-with-microsoft-office-sharepoint-server}

>[!CAUTION]
>
>AEM 6.4 の拡張サポートは終了し、このドキュメントは更新されなくなりました。 詳細は、 [技術サポート期間](https://helpx.adobe.com/jp/support/programs/eol-matrix.html). サポートされているバージョンを見つける [ここ](https://experienceleague.adobe.com/docs/?lang=ja).

**- 要件**

**必要な知識**
AEM Forms Workspace を SharePoint Server に追加するに当たり、SharePoint Server への適切なアクセス権を持っている必要があります。また、Workspace にアクセスするための URL を把握している必要もあります。以下の手順では、SharePoint Server に関する知識があることを前提としています。 SharePoint Server の Web パーツの詳細については、「 Windows SharePoint Services の Web パーツ」を参照してください。

**ユーザレベル**
初心者

Microsoft Office SharePoint Server( 例：Microsoft Office SharePoint Server 2007) でAEM Forms Workspace を Web パーツとして使用できます。 ユーザーは、Web ブラウザーを使用してSharePoint Server に接続し、統合されたエクスペリエンスを提供することで、AEM Forms Workspace にアクセスできます。 この記事では、AEM Forms Workspace をMicrosoft Office SharePoint Server で Web パーツとして表示する基本的な手順を説明します。 この記事で説明する手順を実行すると、SharePointサーバーに接続しているユーザーが同じポートからAEM Forms Workspace にアクセスできるように、統合されたエクスペリエンスを提供できます。

>[!NOTE]
>
>この記事に記載されている手順は、特定のMicrosoft SharePoint Server 2007 です。 また、他のサポート対象バージョンの Microsoft SharePoint も、HTML Workspace と統合することができます。

## AEM Forms Workspace とMicrosoft Office SharePoint Server 2007 の統合 {#integrate-aem-forms-workspace-with-microsoft-office-sharepoint-server}

AEM Forms Workspace を Web パーツに統合するには、次の手順を実行します。

1. Web ブラウザーで、 https://*などのSharePointサイトに移動します。[myMOSServer]:*44299/default.aspx *[myMOSServer]* は、SharePoint サーバーの名前または IP アドレスです。

   >[!NOTE]
   >
   >44299は、SharePointサーバーのデフォルトのポート番号です。 ポート番号は、SharePoint Server のインストールに応じて異なります。

1. Web ページの右上で、 **サイトの操作** を選択し、 **ページを編集**.
1. 「**Web パーツの追加**」ボタンをクリックします。
1. [Web パーツの追加 — Web ページの追加 ] ダイアログボックスの [ その他 ] で、を選択します。 **ページビューア Web パーツ** 次に、 **追加**.
1. [ ページビューアの Web パーツ ] ボックスで、 **編集** を選択し、 **共有 Web パーツの修正**.

   >[!NOTE]
   >
   >[ ページビューアの Web パーツ ] ボックスが **Web パーツの追加** 次の図（図 1）に示すように、手順 3 でクリックしたボタン。

   ![Microsoft Office SharePoint Server の「ページビューアの web パーツ」ボックス。](assets/page-viewer-web-part-box-in-microsoft-office-sharepoint-server.png)

   **図：** *Microsoft Office SharePointサーバーの [ ページビューアの Web パーツ ] ボックス*

1. ページビューアページで、次のタスクを実行します。

   1. 「リンク」ボックスに、AEM Forms Workspace の URL( 例：https://*) を入力します。[AEM_forms_Server]:*8080/lc/ws *[AEM_forms_Server]* は、AEM forms サーバーの IP または名前を表します。
   1. クリック **外観** 高さ、幅およびタイトルを変更して、Workspace ユーザーインターフェイス全体を表示できるようにします。 例えば、高さと幅をそれぞれ 6 インチと 11 インチに設定できます。
   1. クリック **リンクをテスト**. 新しい Web ブラウザーウィンドウが開き、そのウィンドウに Workspace が表示されます。
   1. （オプション）「 **レイアウト** Web パーツの Workspace のレイアウトを変更します。
   1. （オプション）「 **詳細** また、説明や、Web パーツで Workspace を最小化または閉じることができるかどうかなど、他の設定も変更します。

      「**適用**」をクリックします。

1. クリック **編集モードを終了** Workspace にアクセスできることを確認します。

上記の手順を完了すると、SharePointサイトは次の図のようになります（図 2）。

![Microsoft Office SharePoint Server を統合した AEM Forms Workspace](assets/aem-forms-workspace.jpg)

**図：** *Microsoft Office SharePoint Server と統合されたAEM Forms Workspace*
