---
title: AEM Communities リリースノート
seo-title: AEM Communities
description: Adobe Experience Manager 6.4 Communities 固有のリリースノート。
seo-description: Adobe Experience Manager 6.4 Communities 固有のリリースノート。
uuid: 2de9f511-2a61-4003-9b2c-d6728bc9d57a
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.4
topic-tags: release-notes
content-type: reference
discoiquuid: 55a0b70e-5212-408b-8560-6e758bd8bb10
translation-type: tm+mt
source-git-commit: 242f60c70c7cc00871d2ff9f42d2ade4125eaa31

---


# AEM Communities リリースノート {#aem-communities-release-notes}

この節では、AEM Communities の 6.3 リリース以降の改善点について説明します。To learn about the new features in greater detail, see [What&#39;s New in AEM 6.4 Communities](/help/communities/whats-new-aem-communities.md).

最新リリースを入手するには、このドキュメントの [Communities のデプロイ](/help/communities/deploy-communities.md#latest-releases)の節を参照してください。

## 主な改善点 {#main-improvements}

コミュニティサイト：

* コミュニティ管理者は、次のことができます。

   * コミュニティサイトを完全に削除
   * コンテキスト対応のコミュニティサイト設定フォルダーを選択

コミュニティグループ：

* コミュニティ管理者は、次のことができます。

   * コミュニティグループを完全に削除
   * 複数の言語でのコミュニティグループの作成
   * コミュニティグループ内に実施可能カタログおよび割り当てを追加

* イネーブルメントマネージャーは以下をおこなえるようになりました。

   * コミュニティグループ内にリソースと学習パスを作成して割り当て

ファイルライブラリ：

* コミュニティメンバーはファイルライブラリへのいくつかの機能強化（ソート順序、タグ付けなど）を利用できるようになりました。

通知:

* モデレートプロセスを経た投稿が承認されたときに、コミュニティメンバーが通知を受け取るようになりました。

モデレート：

* 自動スパム検出フィルター
* コミュニティモデレーターが使用できるモデレートフィルターが追加されました（回答済み／未回答の質問など）。
* コミュニティモデレーターはモデレートを定義済みのフィルター（承認保留中のすべての投稿など）にブックマークまたはリンクできます。

AEM 6.4 における基盤の変更と完全に互換性があります。

Note: all these features are also available for AEM 6.3. Please check the AEM Communities release notes for [6.3](https://helpx.adobe.com/experience-manager/6-3/release-notes.html).

## 既知の問題 {#known-issues}

* **モデレート**：一括モデレート UI から 1 回の削除操作で親投稿を削除できない（CQ-4236797）
* **コンソール** - 「ユーザー名またはパスワードを忘れた場合」リンクが、対応するパスワード取得フォームではなく「ログインページ」にリダイレクトされる(CQ-4237682)

## 高度な機能 {#select-features}

エキスパートスコアリング（*Adobe Sensei を利用*）を使用すると、ゲーミフィケーションを有効にすることができます。これは、コミュニティでの有益な行動を奨励し、それに報いる効果的な手段です。また、レコメンデーションやマーケティングの目的で、エキスパートを識別するためにも使用できます。

## デモ {#demonstrations}

これらの機能はすべて、GitHub.com で公開されている [AEM のデモマシン](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki)を使用して AEM Communities のデモシナリオで試すことができます。また、新しい We.Retail のリファレンス実装内でも試すことができます。
