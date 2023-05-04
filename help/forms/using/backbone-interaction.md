---
title: Backbone インタラクション
seo-title: Backbone interaction
description: AEM Forms Workspace での Backbone JavaScript モデルの使用に関する概念情報です。
seo-description: Conceptual information about use of Backbone JavaScript models in AEM Forms workspace.
uuid: c70da848-e514-42bc-a59b-44a7c00aa529
content-type: reference
products: SG_EXPERIENCEMANAGER/6.4/FORMS
topic-tags: forms-workspace
discoiquuid: d363eec3-172b-413e-9743-ed51804ea1e9
exl-id: f726cb73-732c-4893-bdb5-10ddcf4a340a
source-git-commit: c5b816d74c6f02f85476d16868844f39b4c47996
workflow-type: tm+mt
source-wordcount: '470'
ht-degree: 34%

---

# Backbone インタラクション {#backbone-interaction}

>[!CAUTION]
>
>AEM 6.4 の拡張サポートは終了し、このドキュメントは更新されなくなりました。 詳細は、 [技術サポート期間](https://helpx.adobe.com/jp/support/programs/eol-matrix.html). サポートされているバージョンを見つける [ここ](https://experienceleague.adobe.com/docs/?lang=ja).

Backbone は、Web アプリケーションで MVC アーキテクチャを作成およびフォローするのに役立つライブラリです。 Backbone の基本的な考え方は、インターフェイスをモデルに基づいた論理ビューに編成することです。モデルが変更された場合に、ページを再描画する必要なく、それぞれを個別に更新できます。 Backbone について詳しくは、[https://backbonejs.org](https://backbonejs.org/) を参照してください。

いくつかの主要な概念を次に示します。

**Backbone モデル**：データと、このデータに関連付けられたほとんどのロジックが含まれています。

**Backbone ビュー**：対応するモデルの状態を表示するために使用します。Backbone ビューは実際にはコントローラと同じように動作します。ユーザーがクリックするなどのユーザーインターフェイスイベントやモデルイベント（データが変更されたなど）をリッスンし、ユーザーインターフェイスを適宜変更します。

**HTML テンプレート**：モデルによって生成されたプレースホルダーがある、ラッパーテンプレート。

**AEM Forms ワークスペース**：複数の個別コンポーネントが含まれます。各コンポーネント：

* 単一の論理ユーザーインターフェイス要素を表します。
* 類似したコンポーネントのコレクションにすることができます。
* Backbone モデル、Backbone ビュー、およびHTMLテンプレートで構成されます。
* サービスへの参照が含まれます。
* 必要なユーティリティへの参照を含みます。

コンポーネントを初期化すると、次のオブジェクトが作成されます。

* コンポーネントの Backbone モデルの新しいインスタンスが作成されます。 モデルにサービスが挿入されます。
* Backbone ビューの新しいインスタンスが作成されます。
* 対応するモデル、HTMLテンプレート、ユーティリティのインスタンスがビューに挿入されます。

Backbone ビューには、対応するハンドラとのユーザーインターフェイスインタラクションによって発生する可能性のある様々なイベントをマッピングするイベントマップがあります。 このマッピングは、コンポーネントが初期化されると開始されます。

ビューが初期化されると、ビューは対応するモデルを呼び出して、サーバからデータを取得します。 ビューによって要求されたすべてのデータが使用可能になると、ビューはデータを HTML テンプレートによって指定された形式にレンダリングします。複数のビューで、通信用に同じモデルを共有することが可能です。

![](do-not-localize/aem_forms_workflow.png)

例：

1. ユーザーがタスクリスト内のタスクテンプレートをクリックします。
1. タスクビューは、クリックをリッスンし、タスクモデルでレンダリング関数を呼び出します。
1. その後タスクモデルは、AEM Forms サーバーとのすべての通信で共通のポイントであるサービスを呼び出します。
1. サービスクラスは、レンダリングメソッドの AEM Forms REST エンドポイントを Ajax 経由で呼び出します。
1. この Ajax 呼び出しの成功コールバックは、タスクモデルで定義されます。
1. タスクモデルは、レンダリング呼び出しが完了した通知として Backbone イベントを発生させます。
1. 別のビューであるタスクの詳細ビューは、タスクモデルからこのイベントをリッスンします。
1. 次に、タスクの詳細ビューは、タスクの詳細テンプレートを変更し、レンダリングされたタスク（フォーム、詳細、添付ファイル、メモなど）をユーザーに表示します。
