---
title: ページでのリンクコンポーネントの埋め込み
seo-title: Embedding link component in a page
description: 'リンクコンポーネントを使用して、任意のページからアダプティブドキュメントまたはアダプティブフォームにリンクできます。  '
seo-description: You can use the link component to link an adaptive document or an adaptive form from any page.
uuid: fde56b5f-634c-406f-a026-875f972f7c8f
content-type: reference
products: SG_EXPERIENCEMANAGER/6.4/FORMS
topic-tags: publish
discoiquuid: a4a36e73-3f7a-4173-8807-931f26daa35a
exl-id: eb816a35-0773-4eda-95b2-1d351c71be8b
source-git-commit: bd94d3949f0117aa3e1c9f0e84f7293a5d6b03b4
workflow-type: tm+mt
source-wordcount: '408'
ht-degree: 92%

---

# ページでのリンクコンポーネントの埋め込み{#embedding-link-component-in-a-page}

## 前提条件 {#prerequisites}

リンクコンポーネントは、Document Services カテゴリのメンバーです。Document Services カテゴリが AEM コンポーネントブラウザーに表示されていることを確認してください。カテゴリがリスト表示されていない場合は、[フォームポータルコンポーネントの有効化](/help/forms/using/enabling-forms-portal-components.md)にリストされている手順に従ってください。

## リンクコンポーネント {#link-component}

フォームポータルの作成者は、リンクコンポーネントを使用してページの任意の場所からアダプティブフォームへのリンクを作成できます。リンクコンポーネントは、コンポーネントブラウザーの Document Services セクションで利用できます。

次の手順を実行して、ページにリンクコンポーネントを追加します。

1. **リンク**&#x200B;コンポーネントをページにドラッグします。コンポーネントを選択し、 ![cmppr](assets/cmppr.png). リンクコンポーネントを編集ダイアログが開きます。

   ![edit-link-component](assets/edit-link-component.png)

1. 「**表示**」タブで次の情報を指定します。

   * **リンクのキャプション**：リンクテキストまたはリンクのキャプション。
   * **リンクツールチップ**：リンクのツールヒント
   * **レイアウトテンプレート**：リンクコンポーネントのレイアウト用テンプレート

1. 「**アセット情報**」タブを開き、アセットのタイプを指定します。アセットは、 **フォーム**. 選択するアセットのタイプによって、次のオプションが表示されます。

   * **アセットパス**：アセットが保存されるリポジトリパス。
   * **レンダリングタイプ**：レンダリング形式--PDF、HTML または自動。自動レンダリングタイプでは、ユーザーの環境が検出され、それに応じて HTML 形式または PDF 形式でフォームがレンダリングされます。例えば、フォームがモバイルデバイスからアクセスされる場合、自動レンダリングタイプでは HTML 形式でフォームがレンダリングされます。
   * **送信 URL:**  フォームデータが送信されるサーブレットの URL。
   * **HTML プロファイル：** HTML 形式でのフォームのレンダリングのためのプロファイル。
   * **PDF プロファイル**：PDF 文書形式でのフォームのレンダリングのためのプロファイル。

1. 「**詳細**」タブを開きます。その他のパラメーターは、キーと値のペアの形式で指定できます。リンクをクリックすると、これらのその他のパラメーターはフォームと共に渡されます。

   タップ **完了** 設定を保存します。

## リンクコンポーネントを使用するためのベストプラクティス {#best-practices-for-using-link-component-br}

* フォームパスに指定したパスが、レンダリング形式として許可された PDF を含む文書を指す場合は、レンダリングタイプとして PDF を選択したことを確認してください。
* フォームの送信 URL は複数の場所で指定でき、その優先順位は以下の通りです。

   1. 優先順位が最も高いのは、フォーム（送信ボタン）に埋め込まれている送信 URL です。
   1. 優先順位が中程度なのは、Forms Manager で説明している送信 URL です。
   1. 一番優先順位が引くのが、フォームポータルで説明している送信URLです。
