---
title: アダプティブフォームのキャッシュの設定
seo-title: Configure adaptive forms cache
description: アダプティブフォームのキャッシュは、アダプティブフォームとアダプティブドキュメント用に特別に設計されています。 クライアント上でのアダプティブフォームまたはドキュメントのレンダリングに要する時間を短縮する目的で、アダプティブフォームおよびアダプティブドキュメントをキャッシュします。
seo-description: The adaptive forms cache is designed specifically for adaptive forms and documents. It caches adaptive forms and adaptive documents with the objective of reducing the time required to render an adaptive form or document on the client.
uuid: 3bd4e405-1eab-4e02-95cd-eb6ac25d18e3
content-type: reference
products: SG_EXPERIENCEMANAGER/6.4/FORMS
topic-tags: Configuration
discoiquuid: dd18f7b5-882d-4e81-ab3d-85f1e5d74992
role: Admin
exl-id: 6a610e9d-beec-486d-b1d2-78b5fec44c52
source-git-commit: c5b816d74c6f02f85476d16868844f39b4c47996
workflow-type: tm+mt
source-wordcount: '306'
ht-degree: 54%

---

# アダプティブフォームのキャッシュの設定 {#configure-adaptive-forms-cache}

>[!CAUTION]
>
>AEM 6.4 の拡張サポートは終了し、このドキュメントは更新されなくなりました。 詳細は、 [技術サポート期間](https://helpx.adobe.com/jp/support/programs/eol-matrix.html). サポートされているバージョンを見つける [ここ](https://experienceleague.adobe.com/docs/?lang=ja).

キャッシュは、データへのアクセスにかかる時間を短縮し、遅延を削減して I／O 速度を改善するメカニズムです。アダプティブフォームのキャッシュには、アダプティブフォームのHTMLコンテンツと JSON 構造のみが保存されます。事前入力されたデータは保存されません。 これにより、クライアント上でアダプティブフォームやドキュメントをレンダリングするのに必要な時間を短縮できます。 アダプティブフォーム専用に設計され、アダプティブドキュメントもサポートします。

>[!NOTE]
>
>アダプティブフォームのキャッシュを使用する場合は、AEM Dispatcher を使用してアダプティブフォームまたはアダプティブドキュメントのクライアントライブラリ（CSS および JavaScript）をキャッシュします。

>[!NOTE]
>
>カスタムコンポーネントの開発時には、開発に使用されるサーバー上でアダプティブフォームのキャッシュを無効にしておく必要があります。

## キャッシュの設定 {#configure-the-cache}

次の手順を実行してアダプティブフォームのキャッシュを設定します。

1. `https://[server]:[port]/system/console/configMgr` の AEM Web コンソール設定マネージャーに移動します。
1. 「**アダプティブフォームおよびインタラクティブ通信 Web チャネルの設定**」をクリックして、設定値を編集します。
1. 設定値を編集ダイアログで、AEM Forms サーバーのインスタンスでキャッシュできるフォームまたはドキュメントの最大数を「**アダプティブフォームの数**」フィールドに指定します。デフォルト値は 100 です。

   >[!NOTE]
   >
   >キャッシュを無効にするには、「アダプティブフォームの数」フィールドの値を **0** に設定します。キャッシュ設定を無効にしたり変更したりすると、キャッシュがリセットされ、すべてのフォームとドキュメントがキャッシュから削除されます。

   ![アダプティブフォームの HTML キャッシュの設定ダイアログ](assets/cache-configuration-edit.png)

1. 「**保存**」をクリックして、設定を保存します。
