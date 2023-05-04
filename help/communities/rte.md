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
source-git-commit: c5b816d74c6f02f85476d16868844f39b4c47996
workflow-type: tm+mt
source-wordcount: '266'
ht-degree: 9%

---

# リッチテキストエディターの基本事項 {#rich-text-editor-essentials}

>[!CAUTION]
>
>AEM 6.4 の拡張サポートは終了し、このドキュメントは更新されなくなりました。 詳細は、 [技術サポート期間](https://helpx.adobe.com/jp/support/programs/eol-matrix.html). サポートされているバージョンを見つける [ここ](https://experienceleague.adobe.com/docs/?lang=ja).

## 概要 {#overview}

リッチテキストエディター (RTE) を使用すると、マークアップを含むテキストを入力できます。

コミュニティコンポーネントの場合は、 [オーサー環境のリッチテキストエディター](../../help/sites-authoring/rich-text-editor.md)パブリッシュ環境で入力されたテキストに影響します。

![chlimage_1-410](assets/chlimage_1-410.png)

## リッチテキストエディターの有効化 {#enabling-rich-text-editor}

ユーザー生成コンテンツ (UGC) を許可するコミュニティコンポーネントを有効にして、RTE を許可できます。 コンポーネントがページに追加されたか、ページ内に含まれたかに応じて [関数](functions.md)の場合、RTE はデフォルトで有効になっている場合と無効になっている場合があります。

有効になっていない場合は、 [オーサー編集モード](sites-console.md#authoring-site-content)をクリックし、編集するコンポーネントを選択して、 `Rich Text Editor` チェックボックス。

RTE は、次のコミュニティコンポーネントで使用できます。

* [ブログ](blog-feature.md)
* [Calendar](calendar.md)
* [コメント](comments.md)
* [Filelibrary](file-library.md)
* [フォーラム](forum.md)
* [メッセージ](configure-messaging.md)
* [Q&amp;A](working-with-qna.md)
* [レビュー](reviews.md)

## カスタマイズ {#customization}

実装が [CKEditor](https://www.ckeditor.com/).

コミュニティコンポーネントの現在の設定は、 `cq.social.  scf   clientlib`( リポジトリ内の場所：

`/libs/clientlibs/social/commons/scf/ckrte.js`

cq.social.scf clientlib は変更しないでください。将来のアップグレードで編集が上書きされる可能性があるからです。

### カスタマイズの例：インラインリンク {#example-customization-inline-links}

セキュリティ上の問題により、ハイパーリンクオプションは、デフォルトでメンバーに表示されるリッチテキストアイコンのセットに含まれません。 UGC で href が許可されている場合、悪戯の能力は大きくなります。

ツールバーにハイパーリンクオプションを追加するには、次の手順を実行します。

* 「 `links`&quot;
   * `{ name: 'links', items: [ 'Link','Unlink','Anchor' ] }`
* 選択 **[!UICONTROL すべて保存]**

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
