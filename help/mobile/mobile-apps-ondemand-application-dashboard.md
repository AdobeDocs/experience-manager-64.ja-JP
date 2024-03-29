---
title: AEM Mobile アプリケーションのダッシュボード
seo-title: AEM Mobile Application Dashboard
description: アプリケーションおよびモバイルアプリコンテンツは、AEM Mobileのアプリケーションダッシュボードまたはコントロールセンターから管理できます。 このページでは、この機能について詳しく見ていきます。
seo-description: You can manage your application and mobile app content from AEM Mobile Application Dashboard or the Control Center. Follow this page to learn more.
uuid: 0d182989-eb83-4207-a8e0-050edbf98ff9
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.4/MOBILE
topic-tags: authoring-on-demand-services-app
discoiquuid: 42a38399-f5a7-4d2f-aa6a-d409a7ec60f7
exl-id: 538d6c02-acee-4774-ab3f-1cf152bb42da
source-git-commit: c5b816d74c6f02f85476d16868844f39b4c47996
workflow-type: tm+mt
source-wordcount: '633'
ht-degree: 8%

---

# AEM Mobile アプリケーションのダッシュボード {#aem-mobile-application-dashboard}

>[!CAUTION]
>
>AEM 6.4 の拡張サポートは終了し、このドキュメントは更新されなくなりました。 詳細は、 [技術サポート期間](https://helpx.adobe.com/jp/support/programs/eol-matrix.html). サポートされているバージョンを見つける [ここ](https://experienceleague.adobe.com/docs/?lang=ja).

>[!NOTE]
>
>Adobeは、単一ページアプリケーションのフレームワークベースのクライアントサイドレンダリング（React など）を必要とするプロジェクトでは、SPA Editor を使用することをお勧めします。 [詳細情報](/help/sites-developing/spa-overview.md)を参照してください。

アプリケーションおよびモバイルアプリコンテンツは、AEM Mobileのアプリケーションダッシュボードまたはコントロールセンターから管理できます。

コントロールセンターの各タイルにドリルダウンして、「。..」をクリックして詳細を表示または編集できます。 をクリックします。

![chlimage_1-54](assets/chlimage_1-54.png)

>[!NOTE]
>
>タイルのグラバーアイコン（左上の 9 つのドット）をクリックして、タイルの順序を並べ替えることができます。 注文の変更は、ユーザー固有のもので、ユーザーごとに異なります。

アプリコンテンツの管理には、開発者、コンテンツ作成者、管理者が共同で取り組む必要があります。 作成者は、アプリ開発者が生成したテンプレートやコンポーネントに基づいて、ページを操作します。

最後に、管理者は更新されたアプリコンテンツを戦略的に公開します。

## アプリを管理タイル {#the-manage-app-tile}

この **アプリを管理** タイルには、使用可能なアプリケーション情報が表示されます。

* タイトル
* 説明
* アイコン
* 最終変更
* 最終変更者

![chlimage_1-55](assets/chlimage_1-55.png)

## 接続を管理タイル {#the-manage-connection-tile}

この **接続を管理** タイルには、AEM Mobile On-demand Servicesの接続情報が表示されます。

* クラウド設定名
* プロジェクト名と ID
* 接続ステータス

>[!NOTE]
>
>右上の歯車をクリックして、Mobile On-Demand クラウド設定をセットアップします。
>
>詳しくは、 [Mobile On-Demand Services の設定](/help/mobile/mobile-on-demand-associating-an-on-demand-app-to-cloud-configuration.md) 」を参照してください。

![chlimage_1-56](assets/chlimage_1-56.png)

## エンティティの管理 {#managing-entities}

以下の 3 つのタイルは、アプリのコンテンツの状態の概要を示します。

* **バナー**
* **記事**
* **コレクション**

右下隅の省略記号 (...) をクリックすると、各タイルを展開して、より詳細なリストビューを表示できます。 これらのリスト表示を使用すると、削除、アップロード、プロパティの編集など、一般的な Mobile On Demand アクションにアクセスする代替の方法が提供されます。

### バナーを管理タイル {#the-manage-banners-tile}

この **バナーを管理** タイルを使用すると、バナーのコンテンツを管理できます。 バナーには次の情報が表示されます。

* image
* **タイトル**:バナーの名前
* **変更済み**:AEMでの最終変更日
* **アップロード済み**:AEMから最後にアップロードした日時
* **公開済み**:AEMでの最終公開リクエスト
* **ソース**:ソース (AEMローカルまたは Mobile On Demand からのリモート )

次の画像は、 **バナーを管理** AEM Mobile Application Dashboard のタイル：

![chlimage_1-57](assets/chlimage_1-57.png)

>[!NOTE]
>
>詳しくは、 **[バナーの管理](/help/mobile/mobile-on-demand-managing-banners.md)** バナーの作成、削除、更新に使用します。

### 記事を管理タイル {#the-manage-articles-tile}

この **記事を管理** タイルでは、記事のコンテンツを管理できます。 記事に関しては、次の情報が表示されます。

* image
* **タイトル**:記事の名前
* **変更済み**:AEMでの最終変更日
* **アップロード済み**:AEMから最後にアップロードした日時
* **公開済み**:AEMでの最終公開リクエスト
* **ソース**:ソース (AEMローカルまたは Mobile On-Demand からのリモート )

次の画像は、 **記事を管理** AEM Mobile Application Dashboard のタイル：

![chlimage_1-58](assets/chlimage_1-58.png)

>[!NOTE]
>
>詳しくは、 [**記事の管理**](/help/mobile/mobile-on-demand-managing-articles.md) 記事を作成、削除または更新する場合。

### コレクションを管理タイル {#the-manage-collections-tile}

この **コレクションを管理** タイルでは、コレクションのコンテンツを管理できます。 コレクションに関する次の情報が表示されます。

* image
* **タイトル**:コレクションの名前
* **変更済み**:AEMでの最終変更日
* **アップロード済み**:AEMから最後にアップロードした日時
* **公開済み**:AEMでの最終公開リクエスト
* **ソース**:ソース (AEMローカルまたは Mobile On-Demand からのリモート )

次の画像は、 **コレクションを管理** AEM Mobile Application Dashboard のタイル：

![chlimage_1-59](assets/chlimage_1-59.png)

>[!NOTE]
>
>詳しくは、 **[コレクションの管理](/help/mobile/mobile-on-demand-managing-collections.md)** コレクションを作成、削除または更新する場合。

### 次の手順 {#the-next-steps}

アプリケーションダッシュボードについて理解したら、次のリソースを参照してモバイルアプリを作成します。

* [アプリケーションの作成および設定アクション](/help/mobile/mobile-apps-ondemand-application-create-configure-action.md)
* [On-Demand アプリをクラウド設定に関連付け](/help/mobile/mobile-on-demand-associating-an-on-demand-app-to-cloud-configuration.md)
* [コンテンツ管理アクション](/help/mobile/mobile-apps-ondemand-manage-content-ondemand.md)

### その他のリソース {#additional-resources}

管理者および開発者の役割と責務について詳しくは、以下のリソースを参照してください。

* [AEM Mobile On-demand Services向けAEMコンテンツの開発](/help/mobile/aem-mobile-on-demand.md)
* [AEM Mobile On-demand Servicesを使用するコンテンツの管理](/help/mobile/aem-mobile.md)
