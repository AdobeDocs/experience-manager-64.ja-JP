---
title: ファイルライブラリ機能
seo-title: ファイルライブラリ機能
description: ファイルライブラリ機能により、サインインしたサイト訪問者がファイルをアップロード、管理、ダウンロードできるようになります
seo-description: ファイルライブラリ機能により、サインインしたサイト訪問者がファイルをアップロード、管理、ダウンロードできるようになります
uuid: 7da94703-8334-4c02-ba2a-55b5cde22e6c
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.4/COMMUNITIES
topic-tags: authoring
content-type: reference
discoiquuid: cdcae09f-c3cb-471e-863f-b33130e9df0f
translation-type: tm+mt
source-git-commit: 3d2b91565e14e85e9e701663c8d0ded03e5b430c
workflow-type: tm+mt
source-wordcount: '676'
ht-degree: 82%

---


# ファイルライブラリ機能 {#file-library-feature}

## 概要 {#introduction}

ファイルライブラリ機能は、サインインしているサイト訪問者（コミュニティメンバー）がコミュニティサイト内でファイルをアップロード、管理およびダウンロードする場所を提供します。

ドキュメントのこのセクションでは、以下の内容について説明します。

* AEMサイトへのファイルライブラリ機能の追加
* Configuration settings for the `File Library` component

## ファイルライブラリをページに追加 {#adding-a-file-library-to-a-page}

To add a `File Library` component to a page in author mode, locate the component

* `Communities / File Library`

コンポーネントを探し、ページ上の位置にドラッグします。

For necessary information, visit [Communities Components Basics](basics.md).

[必要なクライアント側ライブラリが含まれる場合](essentials-file-library.md#essentials-for-client-side) 、次のようにコンポー `File Library` ネントが表示されます。

![chlimage_1-430](assets/chlimage_1-430.png)

## ファイルライブラリの設定 {#configuring-file-library}

Select the placed `File Library` component to access and select the `Configure` icon which opens the edit dialog.

![chlimage_1-431](assets/chlimage_1-431.png) ![chlimage_1-432](assets/chlimage_1-432.png)

### 「コメント」タブ{#comments-tab}

「**[!UICONTROL コメント]**」タブでは、アップロードしたファイルに対するコメントを表示するかどうかと、その方法を指定します。

* **[!UICONTROL ファイルへのコメントを許可]**&#x200B;オンにすると、アップロードしたファイルに対するコメントを許可します。初期設定はオフです。

* **[!UICONTROL 1 ページのコメント数]** 1 ページに表示されるコメント数と返信数を制限します。初期設定は です。 
**10**.

* **[!UICONTROL 最大ファイルサイズ]**&#x200B;この値によって、アップロードするファイルサイズが制限されます。デフォルトの制限は104857600(10 Mb)です。

* **[!UICONTROL メッセージの最大長]**&#x200B;テキストボックスに入力できる最大文字数です。初期設定は 4096 文字です。

* **[!UICONTROL 許可されるファイルタイプ]**&#x200B;ドット付きのファイル拡張子をコンマ区切りで指定します（例：.jpg, .jpeg, .png, .doc, .docx, .pdf）。ファイルの種類を指定すると、指定されていないファイルは許可されません。 初期設定は、すべてのファイルタイプを許可するように指定されません。

* **[!UICONTROL リッチテキストエディター]**&#x200B;オンにすると、マークアップを使用してコメントを入力できます。初期設定はオフです。

* **[!UICONTROL コメントを削除]**&#x200B;オンにすると、ユーザーは自分のコメントを削除できます。初期設定はオンです。

* **[!UICONTROL タグ付けを許可]**&#x200B;オンにすると、ファイルにタグを付加する機能が有効になります。初期設定はオフです。

* **[!UICONTROL 許可された名前空間]**「タグ付けを許可」がオンの場合、使用可能なタグは選択した名前空間に限定されます。名前空間が選択されていない場合、すべての名前空間が許可されます。初期設定はすべての名前空間です。

* **[!UICONTROL 推奨の制限]**「タグ付けを許可」がオンの場合に、表示する推奨タグの数の上限を設定します。-1 に設定した場合、制限はありません。初期設定は -1 です。

* **[!UICONTROL 投票を許可]**&#x200B;オンにすると、ファイルに投票する機能が有効になります。初期設定はオフです。

* **[!UICONTROL フォローを許可]**&#x200B;オンにすると、ブログ記事にフォロー機能が追加され、新しい投稿があった場合にメンバーに[通知](notifications.md)できるようになります。初期設定はオフです。

* **[!UICONTROL スレッド化された返信を許可]**&#x200B;オンにすると、投稿されたコメントに返信できるようになります。初期設定はオフです。

### 「ユーザーモデレート」タブ {#user-moderation-tab}

「**[!UICONTROL ユーザーモデレート]**」タブでは、コメントが許可されている場合に、コメントのモデレートを設定します。

* **[!UICONTROL モデレート前]**&#x200B;オンにすると、コメントを公開サイトに表示する前に承認が必要になります。初期設定はオフです。

* **[!UICONTROL コメントを削除]**&#x200B;オンにすると、コメントを投稿した訪問者がそのコメントを削除できます。初期設定はオンです。

* **[!UICONTROL コメントを拒否]**&#x200B;オンにすると、信頼されているメンバーモデレーターがコメントを拒否できます。初期設定はオフです。

* **[!UICONTROL コメントを閉じる／再度開く]**&#x200B;オンにすると、信頼されているメンバーモデレーターがコメントを閉じたり、再度開いたりすることができます。初期設定はオフです。

* **[!UICONTROL コメントにフラグを設定]**&#x200B;オンにすると、訪問者はコメントに「不適切」のフラグを設定できます。初期設定はオフです。

* **[!UICONTROL フラグ設定理由リスト]**&#x200B;オンにすると、訪問者はコメントに「不適切」のフラグを設定した理由をドロップダウンリストから選択できます。初期設定はオフです。

* **[!UICONTROL カスタムフラグ設定理由]**&#x200B;オンにすると、訪問者はコメントに「不適切」のフラグを設定した独自の理由を入力できます。初期設定はオフです。

* **[!UICONTROL モデレートのしきい値]**&#x200B;訪問者がコメントに何回フラグを設定したらモデレーターに通知するかを指定します。初期設定は1回(
**1**).

* **[!UICONTROL フラグ付けの制限]**&#x200B;コメントに何回フラグが設定されたら、公開表示から非公開にするかを指定します。この数値は、 
**モデレートのしきい値**. 初期設定は 5 です。

## 追加情報 {#additional-information}

More information may be found on the [File Library Essentials](essentials-file-library.md) page for developers.

投稿されたトピックとコメントのモデレートについては、[ユーザー生成コンテンツのモデレート](moderate-ugc.md)を参照してください。

投稿されたトピックとコメントのタグ付けについては、[ユーザー生成コンテンツのタグ付け](tag-ugc.md)を参照してください。
