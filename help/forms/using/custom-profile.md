---
title: HTML5 フォームのカスタムプロファイルの作成
seo-title: Creating a custom profile for HTML5 forms
description: HTML5 フォームプロファイルは Apache Sling のリソースノードです。それは HTML5 forms Render サービスのカスタマイズされたバージョンを表します。
seo-description: A HTML5 forms profile is a resource node in Apache Sling. It represents a customized version of HTML5 forms Render service.
uuid: b9938280-a92c-4dde-b465-04372db3ca8d
content-type: reference
products: SG_EXPERIENCEMANAGER/6.4/FORMS
topic-tags: hTML5_forms
discoiquuid: 9cd22244-9aa6-4b5f-96cf-c9cb3d6f9c8a
feature: Mobile Forms
exl-id: 4630c43f-5b47-435c-8ce5-b4e0d986ec02
source-git-commit: bd94d3949f0117aa3e1c9f0e84f7293a5d6b03b4
workflow-type: tm+mt
source-wordcount: '661'
ht-degree: 59%

---

# HTML5 フォームのカスタムプロファイルの作成 {#creating-a-custom-profile-for-html-forms}

プロファイルは、 [Apache Sling](https://sling.apache.org/). これは、カスタムバージョンのHTML5 forms レンディションサービスを表します。 HTML5 forms レンディションサービスを使用して、HTML5 forms の外観、動作、操作をカスタマイズできます。 プロファイルノードが `/content` JCR リポジトリ内のフォルダー。 ノードは、 `/content` フォルダーまたはそのサブフォルダー `/content` フォルダー。

Profile ノードには **xfaforms/profile** のデフォルト値を持つ **sling:resourceSuperType**&#x200B;プロパティがあります。このノードのレンダリングスクリプトは、/libs/xfaforms/profile にあります。

Sling スクリプトは JSP スクリプトです。JSP スクリプトは要求されたフォームと必要な JS / CSS アーティファクトの HTML を組み立てるためのコンテナとして機能します。これらの Sling スクリプトは&#x200B;**プロファイルレンダラースクリプトとも呼ばれます。** プロファイルレンダラーはForms OSGi サービスを呼び出して、要求されたフォームをレンダリングします。

GETとPOSTのリクエストでは、プロファイルスクリプトは html.jsp と html.POST.jsp にあります。 これらのファイルをコピーして変更することで、上書きして独自のカスタマイズを追加できます。インプレースで変更を加えないでください。パッチの更新によって、そのような変更が上書きされます。

プロファイルにはさまざまなモジュールが含まれています。これらのモジュールは、formRuntime.jsp、config.jsp、toolbar.jsp、formBody.jsp、nav_footer.jsp、および footer.jsp です。

## formRuntime.jsp {#formruntime-jsp-br}

formRuntime.jsp モジュールには、クライアントライブラリの参照が含まれます。 これは、リクエストからロケール情報を抽出したし、ローカライズしたメッセージをリクエストに含めるなどのための方法も示します。独自のカスタム JavaScript ライブラリまたはスタイルを formRuntime.jsp に含めることができます。

## config.jsp {#config-jsp}

config.jsp モジュールには、ロギング、プロキシサービス、動作バージョンなど、さまあまな設定が含まれています。独自の設定およびウィジェットカスタマイズを config.jsp モジュールに追加することができます。また、config.jsp モジュールにカスタムウィジェット登録などの設定を追加することもできます。

## toolbar.jsp {#toolbar-jsp}

toolbar.jsp には、色付きのツールバーを作成するコードが含まれています。 ツールバーを削除するには、toolbar.jsp を HTML.jsp から削除します。

## formBody.jsp {#formbody-jsp}

formBody.jsp モジュールは、XFA フォームのHTML表現用です。

## nav_footer.jsp {#nav-footer-jsp}

最初に、HTML5 フォームはフォームの最初のページのみをレンダリングします。ユーザーがフォームをスクロールすると、フォームの残りの部分がロードされます。こうすることでロード体験が高速になります。nav_footer.jsp コンポーネントには、すべてのスタイルとスクロール時のページのロードを支援するために必要なエレメントが含まれます。 

## footer.jsp {#footer-jsp}

footer.jsp モジュールは空です。ユーザーの操作にのみ使用されるスクリプトを追加できます。

## カスタムプロファイルの作成 {#creating-custom-profiles}

カスタムプロファイルを作成するには、次の手順を実行します。

### プロファイルノードの作成 {#create-profile-node}

1. URL で CRX DE インターフェイスに移動します。 `https://[server]:[port]/crx/de` 管理者の資格情報を使用してインターフェイスにログインします。

1. 左のペインで */content/xfaforms/profiles* の場所に移動します。

1. default ノードをコピーし、*hrform* という名前で別のフォルダー (*/content/profiles*) にそのノードをペーストします。

1. 新しいノード、*hrform* を選択し、*hrform/demo* の値を持つ文字列プロパティ *sling:resourceType* を追加します。

1. ツールバーメニューで「すべて保存」をクリックして、変更を保存します。

### プロファイルレンダラースクリプトを作成する {#create-the-profile-renderer-script}

カスタムプロファイルの作成後、このプロファイルにレンダラーの情報を追加します。新しいプロファイルの要求を受け取る際に、CRX はレンダリングする JSP ページの /apps フォルダーの存在を確認します。JSP ページを /apps フォルダーで作成します。

1. 左側のウィンドウで、 `/apps` フォルダー。
1. を右クリックします。 `/apps` フォルダーを選択し、名前を持つフォルダーを作成します。 **hrform**.
1. 内部の **hrform** フォルダー作成フォルダー名： **デモ**.
1. 「**すべて保存**」ボタンをクリックします。
1. に移動します。 `/libs/xfaforms/profile/html.jsp` ノードをコピーします。 **html.jsp**.
1. 貼り付け **html.jsp** ノードを `/apps/hrform/demo` 同じ名前で上に作成されたフォルダ **html.jsp** をクリックし、 **保存**.
1. プロファイルスクリプトのその他のコンポーネントを持っている場合は、手順 1 から 6 に従って、/apps/hrform/demo フォルダーにそのコンポーネントをコピーします。

1. プロファイルが作成されたことを確認するには、URL を開きます。 `https://[server]:[port]/content/xfaforms/profiles/hrform.html`

フォームを検証するには、ローカルファイルシステムから AEM Forms に[フォームを読み込み](/help/forms/using/get-xdp-pdf-documents-aem.md)、AEM サーバーオーサーインスタンスで[フォームをプレビュー](/help/forms/using/previewing-forms.md)します。
