---
title: コンテンツサービス
seo-title: Content Services
description: コンテンツサービス
seo-description: null
uuid: 7bd09c91-3931-400b-bdfc-b064b9ca9668
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.4/MOBILE
discoiquuid: 6a7e5472-cb57-4c78-b183-7c6dcac11a4e
exl-id: e900d93e-f7cd-4a0d-a866-7fc6c7882797
source-git-commit: c5b816d74c6f02f85476d16868844f39b4c47996
workflow-type: tm+mt
source-wordcount: '337'
ht-degree: 9%

---

# コンテンツサービス{#content-services}

>[!CAUTION]
>
>AEM 6.4 の拡張サポートは終了し、このドキュメントは更新されなくなりました。 詳細は、 [技術サポート期間](https://helpx.adobe.com/jp/support/programs/eol-matrix.html). サポートされているバージョンを見つける [ここ](https://experienceleague.adobe.com/docs/?lang=ja).

>[!NOTE]
>
>Adobeは、単一ページアプリケーションのフレームワークベースのクライアントサイドレンダリング（React など）を必要とするプロジェクトでは、SPA Editor を使用することをお勧めします。 [詳細情報](/help/sites-developing/spa-overview.md)を参照してください。

>[!CAUTION]
>
>コンテンツサービス機能は、プレビュー目的でのみドキュメントに記載されています。
>
>6.3 GA Service Pack 1 のリリースに伴って変更される場合があります。

AEM Mobile Content Services は、AEMで管理されるコンテンツをリクエストするための軽量な機能です。 これにより、AEMコンテンツリポジトリ (JCR) および Web フレームワーク (Sling) に関する深い知識を持つことなく、すべてのアプリ開発者がコンテンツを取得するパフォーマンスの高い方法を提供します。 これにより、リクエストアプリケーションをコンテンツリポジトリから切り離すことができます。

Content Services では、開発者がAEMで管理されるコンテンツに、そのコンテンツのリポジトリ構造を知らずにアクセスできる新しいAEM構造が導入されています。

これらの構成は、AEMが管理するコンテンツとコンテンツを使用するモバイルアプリの間に抽象レイヤーを提供することで、柔軟性を維持し、将来の拡張を可能にするために必要です。 これにより、AEM Content Services は、ネイティブアプリケーションのコンテンツ要件とAEMコンテンツリポジトリとの間の抽象レイヤーとして機能します。

コンテンツサービスは、コンテンツをアセット、パッケージHTML(HTML/CSS/JS) またはチャネルに依存しないコンテンツとして配信できます。

>[!CAUTION]
>
>**前提条件:**
>
>Content Services を使用する前に、Content Services フラグを有効にする必要があります。 アプリでモデルの作成と管理を有効にするには、設定ブラウザーでデータモデルを有効にする必要があります。
>
>詳しくは、 **[コンテンツサービスの管理](/help/mobile/developing-content-services.md)** 」を参照してください。
>
>詳しくは、[設定ブラウザーのドキュメント](/help/sites-administering/configurations.md)を参照してください。

![chlimage_1-143](assets/chlimage_1-143.png)

Content Services フラグを設定し、設定ブラウザーでデータモデルを有効にしたら、以下のリソースを参照して、AEM Mobile Content Services の基本を学び、モデル管理、エンティティ管理、AEM Mobile Content Services のコンテンツ配信/レンダリングなどのコンテンツサービスの概念を理解します。

* リポジトリ内のモデル
* レンダリングと配信
