---
title: フォルダー構造について
seo-title: フォルダー構造について
description: AEM Forms Workspace ソースコードのフォルダー構造を理解してカスタマイズする方法。
seo-description: AEM Forms Workspace ソースコードのフォルダー構造を理解してカスタマイズする方法。
uuid: ee844f89-887e-4f07-9db3-389859baa374
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.4/FORMS
topic-tags: forms-workspace
discoiquuid: 7427858d-8eec-423d-a0a9-444140420620
exl-id: 192c436d-a507-4883-bd68-a6863a6664e0
source-git-commit: bd94d3949f0117aa3e1c9f0e84f7293a5d6b03b4
workflow-type: tm+mt
source-wordcount: '163'
ht-degree: 66%

---

# フォルダー構造について  {#understanding-the-folder-structure}

AEM Forms Workspace は Backbone を使用して MVC アーキテクチャ上で設計されています。各コンポーネントは次のものに対してファイルを持ちます。

* ビジネスロジックを含むモデル 。
* インターフェイスコントロールを含む HTML ファイルであるテンプレート。
* コントローラークラスとしてテンプレートに対して動作する表示。

すべてのコンポーネントのアセットは、以下に示すフォルダー構造内に配置されています。アセットにアクセスするには、CRXDE Liteにログインし、`/libs/ws/js/runtime/`を参照します。

**** modelsバックボーンモデルが含まれます。

**** viewsBackboneビューを含みます。

**** templatesコンポーネントのHTMLテンプレートのみが含まれます。

**** routesContains universal routes.routes 内部の Templates フォルダーには、HTML コードとコンポーネントへの参照が含まれます。

**** servicesRESTエンドポイントでAdobe Experience ManagerサーバーAPIを呼び出すためのサービスインターフェイスが含まれます。

**** utilContains複数のコンポーネントで使用できる汎用ユーティリティ。
