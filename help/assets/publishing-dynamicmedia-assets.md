---
title: Dynamic Media アセットの公開
description: Dynamic Media アセットの公開方法 これらのアセットの HTTP/2 配信を含む
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.4/ASSETS
topic-tags: dynamic-media
content-type: reference
exl-id: ebe30c07-1d76-4338-b301-49591f981688
feature: Asset Management
role: User
source-git-commit: c5b816d74c6f02f85476d16868844f39b4c47996
workflow-type: tm+mt
source-wordcount: '445'
ht-degree: 64%

---

# Dynamic Media アセットの公開 {#publishing-dynamic-media-assets}

>[!CAUTION]
>
>AEM 6.4 の拡張サポートは終了し、このドキュメントは更新されなくなりました。 詳細は、 [技術サポート期間](https://helpx.adobe.com/jp/support/programs/eol-matrix.html). サポートされているバージョンを見つける [ここ](https://experienceleague.adobe.com/docs/?lang=ja).

アセットを選択して「**[!UICONTROL 公開]**」をタップすることで、Dynamic Media アセットを公開できます。Dynamic Media アセットを公開した後は、URL または埋め込みによってそのアセットを Web ページに追加できるようになります。

また、ユーザーの介入なしに、アップロードしたアセットを即座に公開することもできます。詳しくは、 [Dynamic Media - Scene7モードの設定](config-dms7.md).

**[!UICONTROL カード表示]**&#x200B;では、小さい地球のアイコンがアセット名のすぐ下に表示され、アセットが公開されていることを示します。**[!UICONTROL リスト表示]**&#x200B;では、公開されたアセットと公開されていないアセットが「**[!UICONTROL 公開]**」列でわかります。

>[!NOTE]
>
>アセットが既に公開されていて、AEM を使用してアセットを別のフォルダーに移動し、その移動先から再公開した場合は、新しく再公開されたアセットに加えて、元の公開済みアセットの場所も使用できる状態のままです。ただし、元の公開済みアセットは AEM からは「消失」しているので、非公開にすることができません。そのため、ベストプラクティスとしては、アセットを別のフォルダーに移動する前に、アセットを非公開にしてください。

ビデオアセットをエンコードした直後に公開する場合は、エンコードが完全に終了していることを確認してください。ビデオのエンコードがまだ完了していない場合は、ビデオ処理ワークフローが実行中であることが通知されます。ビデオのエンコードが完了すると、ビデオレンディションをプレビューできるようになります。その時点で、エラーが発生することなく、安全にビデオを公開できます。

[Web アプリケーションへの URL のリンク](linking-urls-to-yourwebapplication.md)も参照してください。

関連トピック [Web ページへのビデオビューアの埋め込み。](embed-code.md)

>[!NOTE]
>
>* アセットの URL を使用するためには、そのアセットを公開する必要があります。アセットが公開されていない場合、URL をコピーして Web ブラウザーに貼り付けても機能しません。
>* ライブ配信をするには、画像プリセットおよびビューアプリセットをアクティベートして公開する必要があります。
>


セットまたはアセットの公開について詳しくは、 [アセットを公開します。](managing-assets-touch-ui.md)

## Dynamic Media アセットの HTTP/2 配信 {#http-delivery-of-dynamic-media-assets}

AEMは、HTTP/2 経由でのすべてのDynamic Mediaコンテンツ（画像とビデオ）の配信をサポートするようになりました。 つまり、画像やビデオの公開済み URL または埋め込みコードを、ホストされているアセットを受け入れる任意のアプリケーションと統合できるようになります。 その公開済みアセットは、HTTP/2 プロトコルを使用して配信されます。 この配信方法を使用すると、ブラウザーとサーバーの通信方法が改善され、すべてのDynamic Mediaアセットの応答時間と読み込み時間が向上します。

詳しくは、[コンテンツの HTTP/2 配信に関する FAQ](/help/sites-administering/scene7-http2faq.md) を参照してください。
