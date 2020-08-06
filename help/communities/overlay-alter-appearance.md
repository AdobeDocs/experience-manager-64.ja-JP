---
title: 外観の変更
seo-title: 外観の変更
description: スクリプトの変更
seo-description: スクリプトの変更
uuid: 6930381b-74c1-4e63-9621-621dbedbc25e
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.4/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: da3891d3-fa07-4c88-b4ac-077926b3a674
translation-type: tm+mt
source-git-commit: 1ae2d7f99286e0b958d343778159e2d35095510e
workflow-type: tm+mt
source-wordcount: '219'
ht-degree: 50%

---


# 外観の変更 {#alter-the-appearance}

## スクリプトの変更 {#modify-the-script}

comment.hbsスクリプトは、各コメントの全体的なHTMLを作成します。

投稿された各コメントの横のアバターを表示しないようにするには：

1. コピー `comment.hbs`元 `libs`: `apps`
   1.  `/libs/social/commons/components/hbs/comments/comment/comment.hbs`
   1. Select **[!UICONTROL Copy]**
   1.  `/apps/social/commons/components/hbs/comments/comment`
   1. Select **[!UICONTROL Paste]**
1. Open the overlaid `comment.hbs`
   * ノードを重複クリック `comment.hbs`する `/apps/social/commons/components/hbs/comments/comment folder`
1. 次の行を探し、削除するかコメントアウトします。

   ```xml
   <aside class="scf-comment-author">
           <img class="scf-comment-avatar {{#if topLevel}}withTopLevel{{/if}}" src="{{author.avatarUrl}}"></img>
   ```

行を削除するか、「&lt;!--」と「-->」で囲んでコメントアウトします。また、アバターの位置を視覚的に示すインジケーターとして「xxx」という文字が追加されています。

```xml
<!-- do not display avatar with comment
    <aside class="scf-comment-author">
        <img class="scf-comment-avatar {{#if topLevel}}withTopLevel{{/if}}" src="{{author.avatarUrl}}"></img>
```

## オーバーレイのレプリケート {#replicate-the-overlay}

レプリケーションツールを使用して、オーバーレイされたコメントコンポーネントをパブリッシュインスタンスにプッシュします。

>[!NOTE]
>
>より強固なレプリケーション形式は、パッケージマネージャーでパッケージを作成し、それを[アクティベート](../../help/sites-administering/package-manager.md#replicating-packages)することです。パッケージは、書き出しおよびアーカイブできます。

From the global navigation, select **[!UICONTROL Tools > Deployment > Replication]** and then **[!UICONTROL Activate Tree]**.

For the Start Path enter `/apps/social/commons` and select **[!UICONTROL Activate]**.

![chlimage_1-42](assets/chlimage_1-42.png)

## 結果の表示 {#view-results}

パブリッシュインスタンスに管理者としてログインする(例：http://localhost:4503/crx/de as admin/admin)と、オーバーレイされたコンポーネントが存在することを確認できます。

ログアウトして `aaron.mcdonald@mailinator.com/password` として再ログインし、ページを更新した場合は、投稿されたコメントはアバターと一緒には表示されなくなっており、代わりに単純な「xxx」が表示されることがわかります。

![chlimage_1-43](assets/chlimage_1-43.png)

