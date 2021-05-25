---
title: アダプティブフォームでの SOM 式の使用
seo-title: アダプティブフォームでの SOM 式の使用
description: アダプティブフォームのパネルで SOM 式を抽出する方法を学びます。
seo-description: アダプティブフォームのパネルで SOM 式を抽出する方法を学びます。
uuid: 4bc80e2a-3563-48a3-996d-021b701bc2ee
products: SG_EXPERIENCEMANAGER/6.4/FORMS
topic-tags: develop
discoiquuid: 7dff7ef2-80d1-434a-b9b0-ac6654736602
feature: アダプティブフォーム
exl-id: e4680ede-6a02-4b8b-8a6f-9599a05da8e7
source-git-commit: bd94d3949f0117aa3e1c9f0e84f7293a5d6b03b4
workflow-type: tm+mt
source-wordcount: '348'
ht-degree: 89%

---

# アダプティブフォームでの SOM 式の使用 {#using-som-expressions-in-adaptive-forms}

アダプティブフォームは AEM ページとしてモデル化され、AEM リポジトリで JCR コンテンツ構造で表示されます。コンテンツ構造のキー要素は guideContainer ノードです。guideContainer の下にある rootPanel にはネストされたパネルやフィールドが含まれる場合があります。

Scripting Object Model（SOM）を使用し、特定の Document Object Model（DOM）内の値、プロパティ、メソッドを参照できます。DOM はメモリのオブジェクトとプロパティをツリー階層で編成します。SOM 式はフィールド／描画の要素とパネルを参照します。

次の画像は、コンポーネントをフォームに追加する際にアダプティブフォームが変換するノード構造を示しています。 例えば、パネルをルートパネルに追加し、実行時に DOM に変換されるパネルにラジオボタンを追加できます。アダプティブフォームのラジオボタンフィールドのSOM式は`guide[0].guide1[0].guideRootPanel[0].panel1[0].radiobutton[0]`に指定されています。

![DOM ツリー](assets/hierarchy-1.png)

アダプティブフォーム内のすべての要素の SOM 式には、`guide[0].guide1[0]` ] というプレフィックスが付けられます。ノード構造階層のコンポーネントの場所は SOM 式の派生に使用されます。

![2 つのラジオボタンを持つ DOM ツリー](assets/hierarchy_radio_button.png)

アダプティブフォームでラジオボタンの位置を変更すると、SOM 式が変更されます。オーサリングモードでは、「SOM 式を表示」オプションを使用して AEM Forms 内のフィールドや要素の SOM 式を表示できます。このオプションはフィールドや要素を右クリックするとパネル上に表示されます。

![アダプティブフォームでの SOM 式の抽出](assets/som-expressions.png)

パネル内では、この機能にパネルツールバーからアクセスできます。この機能はアダプティブフォーム作成者のスクリプティングを促進します。 

![パネルツールバーを使用した SOM 式の抽出](assets/som-expression.png)

[GuideBridge](https://helpx.adobe.com/aem-forms/6/javascript-api/GuideBridge.md) に一覧表示されている API の一部は、要素の SOM 式を使用します。例えば、アダプティブフォーム内の特定のフィールドにフォーカスを移動するには、対応する SOM 式を `getFocus` の `guideBridge` API に渡します。 
