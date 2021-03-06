---
title: ページ編集のための取り消しの設定
seo-title: Configuring Undo for Page Editing
description: AEM でのページ編集のための取り消しサポートの設定方法について説明します。
seo-description: Learn how to configure Undo support for page editing in AEM.
uuid: e5a49587-a2a6-41d5-b449-f7a8f7e4cee6
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.4/SITES
topic-tags: operations
content-type: reference
discoiquuid: 3cc7efc5-bcb2-41c9-b78b-308f6b7a298e
exl-id: badb7082-3ebf-4bb3-9157-48b8e7ea8ff9
source-git-commit: bd94d3949f0117aa3e1c9f0e84f7293a5d6b03b4
workflow-type: tm+mt
source-wordcount: '702'
ht-degree: 67%

---

# ページ編集のための取り消しの設定{#configuring-undo-for-page-editing}

[OSGi サービス](/help/sites-deploying/configuring-osgi.md) **Day CQ WCM Undo Configuration**（`com.day.cq.wcm.undo.UndoConfigService`）では、ページ編集のための取り消しおよびやり直しのコマンドの動作を制御するプロパティを確認できます。

## デフォルトの設定 {#default-configuration}

標準インストールでは、デフォルト設定は `sling:OsgiConfig`ノード：

`/libs/wcm/core/config.author/com.day.cq.wcm.undo.UndoConfig`

このノードには、`cq.wcm.undo.whitelist` プロパティと `cq.wcm.undo.blacklist` プロパティが含まれ、その他のプロパティではデフォルトが取得されます。

>[!CAUTION]
>
>`/libs` パス内の設定は&#x200B;***一切***&#x200B;変更しないでください。
>
>`/libs` コンテンツは、インスタンスを次回アップグレードするとき（場合によってはホットフィックスまたは機能パックを適用したとき）に上書きされるからです。

## 取り消しとやり直しの設定 {#configuring-undo-and-redo}

独自のインスタンスに合わせて、これらの OSGi サービスのプロパティを設定できます。

>[!NOTE]
>
>AEM を操作しているときは、このようなサービスの設定を管理する方法がいくつかあります。詳細および推奨事項については、[OSGi の設定](/help/sites-deploying/configuring-osgi.md)を参照してください。

以下に、Web コンソールに表示されるプロパティと、対応する OSGi パラメーターの名前、説明およびデフォルト値（該当する場合）を示します。

* **Enable（有効）**
( 
`cq.wcm.undo.enabled`）

   * **説明**：ページの作成者が変更内容を取り消しおよびやり直しできるかどうかを決定します。
   * **デフォルト**: `Selected`
   * **型**：`Boolean`

* **パス**
( 
`cq.wcm.undo.path`）

   * **説明**：取り消しのバイナリデータを保持するリポジトリのパス。作成者が画像などのバイナリデータを変更すると、元のバージョンのデータがここに保持されます。バイナリデータの変更を元に戻すと、このバイナリの取り消しデータがページに復元されます。
   * **デフォルト**: `/var/undo`
   * **型**：`String`

   >[!NOTE]
   >
   >デフォルトでは、管理者のみが `/var/undo` ノード。 作成者によるバイナリコンテンツの取り消しおよびやり直しが可能になるのは、バイナリ取り消しデータへのアクセスを許可された後のみです。

* **Min.validity**
( 
`cq.wcm.undo.validity`）

   * **説明**:バイナリの取り消しデータが保存される最小時間（時間単位）です。 この期間を過ぎると、ディスク容量を節約するために、バイナリデータは削除可能になります。
   * **デフォルト**: `10`
   * **型**：`Integer`

* **手順**
( 
`cq.wcm.undo.steps`）

   * **説明**:取り消し履歴に保存されるページアクションの最大数。
   * **デフォルト**: `20`
   * **型**：`Integer`

* **永続性**
( 
`cq.wcm.undo.persistence`）

   * **説明**:取り消し履歴を保持するクラス。 2 つの永続クラスが用意されています。

      * `CQ.undo.persistence.WindowNamePersistence`：window.name プロパティを使用して履歴を保持します。
      * `CQ.undo.persistence.CookiePersistance`:cookie を使用して履歴を保持します。
   * **デフォルト**: `CQ.undo.persistence.WindowNamePersistence`
   * **型**：`String`


* **永続モード**
( 
`cq.wcm.undo.persistence.mode`）

   * **説明**:取り消し履歴を保持するタイミングを決定します。 ページが編集されるごとに取り消し履歴を保持するには、このオプションをオンにします。ページの再読み込みがおこなわれるとき（ユーザーが別のページに移動するときなど）のみに保持する場合は、このオプションをオフにします。

        取り消し履歴の保持には、Web ブラウザーのリソースを使用します。ページの編集に対してユーザーのブラウザーの反応が遅い場合は、ページの再読み込み時に取り消し履歴を保持するようにしてください。

   * **デフォルト**: `Selected`
   * **型**：`Boolean`

* **マーカーモード**
( 
`cq.wcm.undo.markermode`）

   * **説明**:取り消しまたはやり直しが発生したときに影響を受ける段落を示すために使用する視覚的なキューを指定します。 有効な値は次のとおりです。

      * flash：段落の選択インジケーターが一時的にフラッシュします。
      * select：段落が選択されています。
   * **デフォルト**: `flash`
   * **型**：`String`


* **優れたコンポーネント**
( 
`cq.wcm.undo.whitelist`）

   * **説明**：取り消しコマンドややり直しコマンドの影響を及ぼしたいコンポーネントのリスト。取り消しややり直しにより正しく機能するコンポーネントパスをこのリストに追加します。アスタリスク (&amp;ast;) を追加して、コンポーネントのグループを指定します。

      * 次の値は、基盤テキストコンポーネントを指定します。

         `foundation/components/text`

      * 次の値は、すべての基盤コンポーネントを指定します。

         `foundation/components/*`
   * このリストにないコンポーネントに対して取り消しまたはやり直しが実行されると、コマンドが信頼できない可能性があることを示すメッセージが表示されます。

   * **デフォルト**:プロパティには、AEMが提供する多くのコンポーネントが設定されます。
   * **型**：`String[]`


* **無効なコンポーネント**
( 
`cq.wcm.undo.blacklist`）

   * **説明**:取り消しコマンドの影響を受けないコンポーネントやコンポーネントの操作のリスト。 取り消しコマンドで正しく動作しないコンポーネントやコンポーネントの操作を追加します。

      * 取り消し履歴にあるコンポーネントの操作がまったく必要ない場合はコンポーネントのパスを追加します。例：`collab/forum/components/post`
      * 特定の操作を取り消し履歴から除外する場合（他の操作が正しく機能する場合）に、コロン (:) と操作をパスに追加します。 `collab/forum/components/post:insertParagraph.`

   >[!NOTE]
   >
   >リストに掲載されている操作でも、取り消し履歴には追加されます。取り消し履歴の **Bad Component** 操作の前に存在する操作は取り消すことができません。

   * 代表的な操作名は次のとおりです。

      * `insertParagraph`：コンポーネントがページに追加されます。
      * `removeParagraph`:コンポーネントが削除されます。
      * `moveParagraph`：段落が別の場所に移動されます。
      * `updateParagraph`：段落のプロパティが変更されます。
   * **デフォルト**：このプロパティには、複数のコンポーネントの操作が指定されます。
   * **型**：`String[]`
