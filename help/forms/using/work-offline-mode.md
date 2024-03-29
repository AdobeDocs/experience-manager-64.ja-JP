---
title: オフラインモードの使用
seo-title: Working in the offline mode
description: モバイルデバイスをAEM Formsネットワークの範囲外で、または完全にオフラインモードで使用して、AEM Formsアプリで作業します。
seo-description: Take your mobile device offline outside your AEM Forms network range or in a completely offline mode and work on the AEM Forms app
uuid: b900a0f8-90ce-486a-bde6-6cdf11bd2801
content-type: reference
products: SG_EXPERIENCEMANAGER/6.4/FORMS
topic-tags: forms-app
discoiquuid: 9a3c6ab4-8bb9-40c7-8c56-59153b364887
exl-id: 14303b8f-40a7-4bc5-8282-7526e0319264
source-git-commit: c5b816d74c6f02f85476d16868844f39b4c47996
workflow-type: tm+mt
source-wordcount: '568'
ht-degree: 34%

---

# オフラインモードの使用 {#working-in-the-offline-mode}

>[!CAUTION]
>
>AEM 6.4 の拡張サポートは終了し、このドキュメントは更新されなくなりました。 詳細は、 [技術サポート期間](https://helpx.adobe.com/jp/support/programs/eol-matrix.html). サポートされているバージョンを見つける [ここ](https://experienceleague.adobe.com/docs/?lang=ja).

AEM Forms アプリケーションのオフラインモードを使用すると、アプリケーションがオフラインになってもシームレスに作業を続けることができます。ネットワーク接続を必要とせずにフォームを開いたり、更新したり、送信したりすることができます。

AEM Forms アプリケーションで作業を開始する際は、まずアプリケーションを AEM Forms サーバーと同期します。自分に割り当てられているすべてのフォームが、自分のアプリにダウンロードされます。 JEE 上のAEM Formsの場合、タスクは「タスク」タブで取得され、スタートポイント関連のフォームおよび他のフォームは「Forms」タブで取得されます。 OSGi 上のAEM Formsの場合、Formsのみが「Forms」タブに読み込まれます。

アプリケーションを同期する方法について詳しくは、 [アプリの同期](/help/forms/using/sync-app.md).

## Formsをオフラインで使用できるようにする {#making-forms-available-offline}

アプリケーションをAEM Formsサーバーと同期すると、フォームがモバイルデバイスにダウンロードされます。 ただし、デフォルトでは、フォームに関連付けられている添付ファイルはダウンロードされません。 これは、オンラインになっている場合、添付ファイルを表示できることを意味します。 ただし、添付ファイルをオフラインモードで表示できるようにするには、アプリのデフォルト設定を変更します。

関連する添付ファイルが各フォームと共に確実にダウンロードされるようにするには、「添付ファイルを取得」を「オン」に設定します。 詳しくは、 [一般設定の更新](/help/forms/using/update-general-settings.md).

モバイルデバイスでのデータのダウンロードは、デバイスのパフォーマンスに影響を与える可能性があるので、デフォルトでは、「添付ファイルの取得」設定は「オフ」に設定されています。 設定が「オン」に更新された後、サーバーからダウンロードされたタスクの添付ファイルがデバイスに取得されます。 オフラインモードでは、「**添付ファイルを取得する**」オプションを「有効」に設定することで、デバイスにダウンロードされるタスクすべてが作業可能になります。

## AEM Forms アプリケーションに対してオフラインサービスを設定する {#configuring-offline-service-for-aem-forms-app-br}

AEM Forms アプリケーションオフラインサービスでは、フォームで使用するリソースを認識します。AEM Forms アプリケーションは、フォームの依存関係に関する情報を取得する際に、このサービスに依存しています。オフライン機能を有効にするには、フォームの依存関係に関する情報が必要です。 AEM Forms App Offline Service は、フォームで使用されるリソースのパスまたは URL をキャッシュします。 キャッシュは、フォームに加えられた変更やオフラインサービスに設定された有効期間に基づいて更新されます。フォームで使用されるリソースのパスや URL をキャッシュに保存することで、サーバー側のパフォーマンスが向上します。

AEM Forms アプリケーションでサーバー側のオフラインコンポーネントの設定は、次のように行います。

1. オーサーインスタンスで、**Adobe Experience Manager**／**ツール**／**Forms**／**Forms アプリケーションオフラインサービスを設定**&#x200B;に移動します。

   URL：`https://<server>:<port>/<context-path>/libs/fd/workspace-offline/gui/content/config.html`

1. 「一般設定」では、次の操作を実行できます。

   * **キャッシュをクリア**:フォームの依存関係のサーバー側キャッシュをクリアします。
   * **設定のリセット**：AEM Forms アプリケーションのオフライン設定をリセットします。
   * **キャッシュの有効性**:サーバー側のオフラインキャッシュの有効期間を指定します。
   * **リソース監視パス**:オフラインサービスがリソースの変更を監視するパスを指定します。 指定したパスに変更が発生した場合は、依存するすべてのフォームのオフラインキャッシュが更新されます。 （例：`/etc/clientlibs/fd,/content/dam/images`）。

1. 内 **手動のリソースキャッシュ** 「 」タブで、「依存関係オフラインサービスが識別できないフォームの依存関係を指定します。 JavaScript 内で読み込んだ画像などのリソースを指定できます。 AEM Forms App は、オフラインモード用にこれらのリソースもダウンロードします。
