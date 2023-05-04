---
title: 外観の変更（HBS）
seo-title: Alter the Appearance
description: HBS スクリプトの変更
seo-description: Modify the HBS scripts
uuid: 6e1030af-f170-4a60-9d3f-439afd05de57
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.4/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 70be208d-185b-4b27-8e01-74e62f656344
exl-id: 358b70b8-8122-4eda-baa7-d9a58d6901f9
source-git-commit: c5b816d74c6f02f85476d16868844f39b4c47996
workflow-type: tm+mt
source-wordcount: '304'
ht-degree: 6%

---

# 外観の変更（HBS） {#alter-the-appearance-hbs}

>[!CAUTION]
>
>AEM 6.4 の拡張サポートは終了し、このドキュメントは更新されなくなりました。 詳細は、 [技術サポート期間](https://helpx.adobe.com/jp/support/programs/eol-matrix.html). サポートされているバージョンを見つける [ここ](https://experienceleague.adobe.com/docs/?lang=ja).

アプリケーションディレクトリ (/apps) 内のカスタムコメントシステムのコンポーネントが配置され、resourceSuperType がデフォルトのコメントシステムとカスタムのモデル/ビューを参照するので、実装を変更できます。

シンプルなデモの場合、ビジュアル機能（コメントを投稿するサインインユーザーに表示されるアバター）は削除されます。

>[!NOTE]
>
>この拡張機能を利用するには、影響を受ける Web サイト内のコメントシステムのインスタンス (/content) で、その resourceType をカスタムコメントシステムに設定する必要があります。

## HBS スクリプトの変更 {#modify-the-hbs-scripts}

使用 [CRXDE Lite](../../help/sites-developing/developing-with-crxde-lite.md):

* 開く [/apps/custom/components/comments/comment/comment.hbs](http://localhost:4502/crx/de/index.jsp#/apps/custom/components/comments/comment/comment.hbs)

   * コメント投稿のアバターを含むタグをコメントアウトします（21 行目前後）。

      ```
      <!--
       <<img class="scf-comment-avatar {{#if topLevel}}withTopLevel{{/if}}" src="{{author.avatarUrl}}"></img>
       -->
      ```

* 開く [/apps/custom/components/comments/comments.hbs](http://localhost:4502/crx/de/index.jsp#/apps/custom/components/comments/comments.hbs)

   * 次のコメントエントリのアバターを含むタグをコメントアウトします（44 行目前後）。

      ```
      <!--
       <img class="scf-composer-avatar" src="{{loggedInUser.avatarUrl}}"></img>
       -->
      ```

* 選択 **すべて保存**

## カスタムアプリをレプリケート {#replicate-custom-app}

アプリケーションを変更した後、カスタムコンポーネントを再レプリケートする必要があります。

その方法の 1 つは、

* メインメニューから

   * 選択 **[!UICONTROL [ ツール ] > [ 操作 ] > [ レプリケーション ]]**
   * `Activate Tree` を選択します。
   * 設定 `Start Path`:から `/apps/custom`
   * オフ `Only Modified`
   * 選択 `Activate` ボタン

## 公開済みサンプルページで変更済みコメントを表示 {#view-modified-comment-on-published-sample-page}

[エクスペリエンスの継続](extend-sample-page.md#publish-sample-page) パブリッシュインスタンスでは、同じユーザーとしてサインインしたままで、パブリッシュ環境でページを更新して、アバターを削除するための変更を表示できます。

![chlimage_1-81](assets/chlimage_1-81.png)

## サンプルコメント拡張パッケージ {#sample-comment-extension-package}

このチュートリアルで作成したカスタムコメントアプリケーションのパッケージが添付されています。

[ファイルを入手](assets/sample-comment-extension-6-1-fp3.zip)
