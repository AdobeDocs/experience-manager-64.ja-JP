---
title: オーサリング時の AEM のトラブルシューティング
seo-title: Troubleshooting AEM when Authoring
description: 以下のセクションでは、AEM の使用時に発生する可能性のあるいくつかの問題を取り上げます。それらのトラブルシューティング方法に関する推奨事項についても説明します。
seo-description: The following section covers some issues that you might encounter when using AEM, together with suggestions on how to troubleshoot them.
uuid: eb95e5ba-1eed-4ffb-80c1-9b8468820c22
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.4/SITES
topic-tags: page-authoring
content-type: reference
discoiquuid: 9b492b17-9029-46ae-9dc0-bb21e6b484df
exl-id: 09409631-c579-4b1f-9193-1348896f6a09
source-git-commit: c5b816d74c6f02f85476d16868844f39b4c47996
workflow-type: tm+mt
source-wordcount: '466'
ht-degree: 55%

---

# オーサリング時の AEM のトラブルシューティング {#troubleshooting-aem-when-authoring}

>[!CAUTION]
>
>AEM 6.4 の拡張サポートは終了し、このドキュメントは更新されなくなりました。 詳細は、 [技術サポート期間](https://helpx.adobe.com/jp/support/programs/eol-matrix.html). サポートされているバージョンを見つける [ここ](https://experienceleague.adobe.com/docs/?lang=ja).

ここでは、AEM の使用時に発生する可能性のあるいくつかの問題を取り上げます。また、それらのトラブルシューティング方法に関する推奨事項についても説明します。

>[!NOTE]
>
>問題が発生した場合は、リストを確認することも重要です [既知の問題](/help/release-notes/known-issues.md) インスタンス（リリースおよびサービスパック）の

>[!NOTE]
>
>管理者権限を持ち、AEMの問題をトラブルシューティングするユーザーは、 [トラブルシューティングAEM （管理者向け）](/help/sites-administering/troubleshoot.md). 十分な権限がない場合は、AEMのトラブルシューティングに関して、システム管理者に問い合わせてください。

## 公開されたサイト上に古いバージョンのページがまだある {#old-page-version-still-on-published-site}

* **問題**：

   * ページに変更を加えてそのページを公開サイトにレプリケートしましたが、公開サイトでは古いバージョンのページが依然として表示されます&#x200B;*。*

* **理由**:

   * これには複数の原因が考えられます。ほとんどの場合、キャッシュ（ローカルブラウザーまたは Dispatcher）が原因ですが、レプリケーションキューに問題が発生する場合があります。

* **ソリューション**:

   * ここには、様々な可能性があります。
   * ページが正しくレプリケートされていることを確認します。 ページのステータスと、必要に応じてレプリケーションキューの状態を確認します。
   * ローカルブラウザーのキャッシュをクリアして、ページに再度アクセスします。
   * ページ URL の末尾に `?` を追加します。以下に例を示します。

      `http://localhost:4502/sites.html/content?`

       これによって、ページが AEM から直接リクエストされ、Dispatcher がスキップされます。更新されたページを受け取った場合、Dispatcher のキャッシュをクリアする必要があることを表しています。

   * システム管理者に問い合わせて、レプリケーションキューに問題があることを伝えます。

## サイドキックが表示されません {#sidekick-not-visible}

* **問題**：

   * オーサー環境でコンテンツページを編集する際に、サイドキックが表示されない。

* **理由**:

   * まれに、サイドキックのヘッダーが現在のウィンドウの範囲外に配置されている可能性があります。 これは、再び再配置できないことを意味します。

* **ソリューション**：

   * 現在のセッションからログアウトし、再度ログインします。 サイドキックはデフォルトの位置に戻ります。

## 検索と置換 — すべてのインスタンスが置き換えられていません {#find-replace-not-all-instances-are-replaced}

* **問題:**

   * 「**検索と置換**」オプションを使用するとき、`find` 検索語句の一部のインスタンスがページ上で置換されないことがあります。

* **理由**:

   * **検索と置換**&#x200B;の機能は、コンテンツの保存のされ方と、コンテンツを検索できるかどうかに依存しています。例えば、ブログテキストは `jcr:text` プロパティに格納されますが、このプロパティは検索対象として設定されません。検索と置換のサーブレットのデフォルトスコープには、次のプロパティが含まれています。

      * `jcr:title`
      * `jcr:description`
      * `jcr:text`
      * `text`

* **ソリューション**：

   * これらの定義は、例えば次の場所にある **web コンソール**&#x200B;を使用して、**Day CQ WCM 検索置換サーブレット** を設定することで変更できます。

      `http://localhost:4502/system/console/configMgr`
