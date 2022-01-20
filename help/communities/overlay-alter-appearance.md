---
title: 外観の変更
seo-title: Alter the Appearance
description: スクリプトの変更
seo-description: Modify the script
uuid: 6930381b-74c1-4e63-9621-621dbedbc25e
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.4/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: da3891d3-fa07-4c88-b4ac-077926b3a674
exl-id: 01a20578-56c3-41b3-8a0e-281104af2481
source-git-commit: bd94d3949f0117aa3e1c9f0e84f7293a5d6b03b4
workflow-type: tm+mt
source-wordcount: '213'
ht-degree: 48%

---

# 外観の変更 {#alter-the-appearance}

## スクリプトの変更 {#modify-the-script}

comment.hbs スクリプトは、各コメントの全体的なHTMLを作成します。

投稿された各コメントの横のアバターを表示しないようにするには：

1. コピー `comment.hbs`から `libs`から `apps`
   1.  `/libs/social/commons/components/hbs/comments/comment/comment.hbs`
   1. 選択 **[!UICONTROL コピー]**
   1.  `/apps/social/commons/components/hbs/comments/comment`
   1. 選択 **[!UICONTROL 貼り付け]**
1. オーバーレイを開く `comment.hbs`
   * ノードをダブルクリック  `comment.hbs`in `/apps/social/commons/components/hbs/comments/comment folder`
1. 次の行を探し、削除するかコメントアウトします。

   ```xml
   <aside class="scf-comment-author">
           <img class="scf-comment-avatar {{#if topLevel}}withTopLevel{{/if}}" src="{{author.avatarUrl}}"></img>
   ```

行を削除するか、「&lt;!--」と「-->」で囲んでコメントアウトします。また、アバターがあった場所を視覚的に示すインジケーターとして、文字「xxx」が追加されています。

```xml
<!-- do not display avatar with comment
    <aside class="scf-comment-author">
        <img class="scf-comment-avatar {{#if topLevel}}withTopLevel{{/if}}" src="{{author.avatarUrl}}"></img>
```

## オーバーレイのレプリケート {#replicate-the-overlay}

レプリケーションツールを使用して、オーバーレイされたコメントコンポーネントをパブリッシュインスタンスにプッシュします。

>[!NOTE]
>
>より強固なレプリケーション形式は、パッケージマネージャーでパッケージを作成し、それを[アクティベート](../../help/sites-administering/package-manager.md#replicating-packages)することです。パッケージはエクスポートおよびアーカイブできます。

グローバルナビゲーションから、 **[!UICONTROL ツール/導入/レプリケーション]** その後 **[!UICONTROL ツリーをアクティベート]**.

「開始パス」に、と入力します。 `/apps/social/commons` を選択し、 **[!UICONTROL 有効化]**.

![chlimage_1-42](assets/chlimage_1-42.png)

## 結果の表示 {#view-results}

パブリッシュインスタンスに管理者 ( http://localhost:4503/crx/deなど ) としてログインした場合は、オーバーレイされたコンポーネントが存在することを確認できます。

ログアウトして `aaron.mcdonald@mailinator.com/password` として再ログインし、ページを更新した場合は、投稿されたコメントはアバターと一緒には表示されなくなっており、代わりに単純な「xxx」が表示されることがわかります。

![chlimage_1-43](assets/chlimage_1-43.png)
