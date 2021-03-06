---
title: リッチテキストエディターの基本事項
seo-title: Rich Text Editor Essentials
description: リッチテキストエディター機能の概要
seo-description: Rich text Editor feature overview
uuid: f96015cc-114b-431a-a5ba-dc195c2a0b83
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.4/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 0225a543-0fad-488b-8b0b-8b3512d44fbe
exl-id: d236a8d3-20ad-4568-a7c2-87d146aa0532
source-git-commit: bd94d3949f0117aa3e1c9f0e84f7293a5d6b03b4
workflow-type: tm+mt
source-wordcount: '230'
ht-degree: 73%

---

# リッチテキストエディターの基本事項 {#rich-text-editor-essentials}

## 概要 {#overview}

リッチテキストエディター（RTE）では、マークアップを使用してテキストを入力できます。

コミュニティコンポーネントの場合、[オーサー環境のリッチテキストエディター](../../help/sites-authoring/rich-text-editor.md)に似ていますが、パブリッシュ環境で入力されたテキストに影響します。

![chlimage_1-410](assets/chlimage_1-410.png)

## リッチテキストエディターの有効化 {#enabling-rich-text-editor}

ユーザー生成コンテンツ（UGC）を許可するコミュニティコンポーネントを有効にすることによって、RTE を許可することができます。コンポーネントがページに追加されたか、ページ内に含まれたかに応じて [関数](functions.md)の場合、RTE はデフォルトで有効になっている場合と無効になっている場合があります。

有効になっていない場合は、 [オーサー編集モード](sites-console.md#authoring-site-content)をクリックし、編集するコンポーネントを選択して、 `Rich Text Editor` チェックボックス。

RTE は、次のコミュニティコンポーネントに使用できます。

* [ブログ](blog-feature.md)
* [Calendar](calendar.md)
* [コメント](comments.md)
* [Filelibrary](file-library.md)
* [フォーラム](forum.md)
* [メッセージ](configure-messaging.md)
* [Q&amp;A](working-with-qna.md)
* [レビュー](reviews.md)

## カスタマイズ {#customization}

リッチテキストエディターのカスタマイズは、[CKEditor](https://www.ckeditor.com/) に基づいて実装した場合に可能になります。

コミュニティコンポーネントの現在の設定は、次のリポジトリにある `cq.social.  scf   clientlib` に含まれています。

`/libs/clientlibs/social/commons/scf/ckrte.js`

今後のアップグレードにより編集内容が上書きされる可能性があるので、cq.social.scf clientlib を変更しないことをお勧めします。

### カスタマイズの例：インラインリンク {#example-customization-inline-links}

セキュリティ上の懸念事項により、デフォルトでメンバーに表示されるリッチテキストアイコンのセットにハイパーリンクオプションは含まれません。UGC で href が許可されている場合、悪戯の能力は大きくなります。

ツールバーにハイパーリンクオプションを追加するには：

* 「 `links`&quot;
   * `{ name: 'links', items: [ 'Link','Unlink','Anchor' ] }`
* 「**[!UICONTROL すべて保存]**」を選択します。

#### /libs/clientlibs/social/commons/scf/ckrte.js {#libs-clientlibs-social-commons-scf-ckrte-js}

```
CKRte.prototype.config = {
    toolbar: [
        { name: "basicstyles",
           items: ["Bold", "Italic", "Underline", "NumberedList", "BulletedList", "Outdent", "Indent", "JustifyLeft", "JustifyCenter", "JustifyRight", "JustifyBlock", "TextColor"]
        },
        { name: 'links', 
           items: [ 'Link','Unlink','Anchor' ] 
        }
    ],
    autoParagraph: false,
    autoUpdateElement: false,
    removePlugins: "elementspath",
    resize_enabled: false
};
```
