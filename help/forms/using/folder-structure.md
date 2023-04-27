---
title: フォルダー構造について
seo-title: Understanding the folder structure
description: カスタマイズするAEM Forms Workspace ソースコードのフォルダー構造を理解する方法です。
seo-description: How to understand the folder structure of AEM Forms workspace source code to customize.
uuid: ee844f89-887e-4f07-9db3-389859baa374
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.4/FORMS
topic-tags: forms-workspace
discoiquuid: 7427858d-8eec-423d-a0a9-444140420620
exl-id: 192c436d-a507-4883-bd68-a6863a6664e0
source-git-commit: bd94d3949f0117aa3e1c9f0e84f7293a5d6b03b4
workflow-type: tm+mt
source-wordcount: '145'
ht-degree: 53%

---

# フォルダー構造について {#understanding-the-folder-structure}

AEM Forms Workspace コンポーネントは、Backbone を使用した MVC アーキテクチャ上で設計されています。 各コンポーネントには、次の用のファイルがあります。

* ビジネスロジックを含むモデル。
* インターフェイスコントロールを含むHTMLファイルです。
* テンプレートに対するコントローラクラスとして機能する表示。

すべてのコンポーネントのアセットは、以下に説明するフォルダー構造に配置されます。 アセットにアクセスするには、CRXDE Lite にログインし、`/libs/ws/js/runtime/` を参照します。

**models**：バックボーンモデルが含まれます。

**views**：バックボーンビューが含まれます。

**templates**：コンポーネント用の HTML テンプレートのみが含まれます。

**routes**：ユニバーサルルートが含まれます。routes 内部の Templates フォルダーには、HTML コードとコンポーネントへの参照が含まれます。

**services**：REST エンドポイント上の Adobe Experience Manager サーバーの API を呼び出すためのサービスインターフェイスが含まれます。

**util**：複数のコンポーネントによって使用可能な一般ユーティリティが含まれます。
