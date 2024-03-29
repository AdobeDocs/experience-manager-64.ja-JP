---
title: コミュニティの開発
seo-title: Developing Communities
description: フォーラムやユーザーグループなどのコミュニティ機能を作成し、カスタマイズする
seo-description: Create and customize community features such as forums, user groups, and more
uuid: 51dc54da-9090-4d36-adf9-72d5479062a5
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.4/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: fbfe8097-3c3f-4a05-97ad-1ce526362a26
exl-id: b051b279-b0d9-41a3-b5d8-4b9bad448c0f
source-git-commit: c5b816d74c6f02f85476d16868844f39b4c47996
workflow-type: tm+mt
source-wordcount: '428'
ht-degree: 20%

---

# コミュニティの開発 {#developing-communities}

>[!CAUTION]
>
>AEM 6.4 の拡張サポートは終了し、このドキュメントは更新されなくなりました。 詳細は、 [技術サポート期間](https://helpx.adobe.com/jp/support/programs/eol-matrix.html). サポートされているバージョンを見つける [ここ](https://experienceleague.adobe.com/docs/?lang=ja).

## 概要 {#overview}

AEM Communitiesは、フォーラム、ユーザーグループ、ブログ、Q&amp;A、カレンダー、コメント、レビュー、投票、評価、割り当てなどのコミュニティ機能の作成とカスタマイズを簡単にします。 これらの機能を使用すると、パブリッシュ環境にユーザー生成コンテンツ (UGC) が入力されます。

の基盤 [コミュニティサイト](overview.md#communitiessites) が [ソーシャルコンポーネントフレームワーク](scf.md) (SCF)。 コミュニティサイトの作成は、 [コミュニティサイトテンプレート](sites-console.md) それは [コミュニティ機能](functions.md).

概要と入門チュートリアルについては、次を参照してください。

* [AEM Communities の概要](overview.md)
* [AEM Communities 使用の手引き](getting-started.md)
* [イネーブルメントのための AEM Communities 使用の手引き](getting-started-enablement.md)

>[!NOTE]
>
>を常に最新の状態に保つことを強くお勧めします。 [最新リリース](deploy-communities.md#latest-releases).

## 推奨されるデプロイメント {#recommended-deployments}

* [コミュニティコンテンツストレージ](working-with-srp.md):UGC 共通ストアで使用可能な SRP の選択肢について説明します。
* [コミュニティ用の推奨トポロジ](topologies.md):使用例と SRP の選択に基づくトポロジについて説明します。

## ソーシャルコンポーネントフレームワーク {#social-component-framework}

* [ソーシャルコンポーネントフレームワーク](scf.md):フレームワークと API の概要
* [SCF Handlebars ヘルパー](handlebars-helpers.md):既定のヘルパーとカスタムヘルパーの書き込み方法
* [クライアント側のカスタマイズ](client-customize.md):ブラウザーで実行するコードのカスタマイズ
* [サーバー側のカスタマイズ](server-customize.md):サーバー上で実行するコードのカスタマイズ
* [ストレージリソースプロバイダー (SRP)](srp.md):コミュニティコンテンツストレージの概要
* [コーディングのガイドライン](code-guide.md):ガイドライン、ヒント、テクニック
* [コミュニティコンポーネントガイド](components-guide.md):インタラクティブ開発ツール

## コンポーネントおよび機能の基本事項 {#component-function-and-feature-essentials}

AEM Communitiesのコンポーネント、機能および機能は、 [コミュニティサイト](sites-console.md).

* [コンポーネントおよび機能の基本事項](essentials.md)
* [コミュニティコンポーネントの clientlib](clientlibs.md)
* [コミュニティ機能](functions.md)
* [コミュニティグループテンプレート](tools-groups.md)
* [コミュニティサイトテンプレート](sites.md)

## コミュニティメンバー {#community-members}

* [ユーザーとユーザーグループの管理](users.md)
* [Facebook と Twitter を使用したソーシャルログイン](social-login.md)

## コミュニティグループ {#community-groups}

[コミュニティグループ](overview.md#communitygroups) は、コミュニティメンバーがコミュニティサイト内でサブコミュニティを作成できるようにする概念です。 コミュニティグループの作成は、パブリッシュ環境またはオーサー環境でおこなうことができます。

* [コミュニティグループの基本事項](essentials-groups.md)
* [グループ機能](functions.md#groups-function)
* [コミュニティグループテンプレート](tools-groups.md)
* [ユーザーとユーザーグループの管理](users.md)
* [作成者向けコミュニティグループ](creating-groups.md)

## データの管理 {#managing-data}

* [SRP と UGC の基本事項](srp-and-ugc.md) - SRP API ユーティリティメソッドと例
* [タグの基本事項](tag.md)  — コミュニティメンバーが UGC やカタログ化されたイネーブルメントリソースにタグ付けする機能

## チュートリアル {#tutorials}

* [クライアント側チュートリアル](tutorials.md#client-side-customization)
* [サーバー側チュートリアル](tutorials.md#server-side-customization)
* [ハウツーインストラクション](tutorials.md#how-to-instructions)

## トラブルシューティング {#troubleshooting}

* [トラブルシューティング](troubleshooting.md)
* [既知の問題](/help/release-notes/known-issues.md)

## 関連するコミュニティドキュメント {#related-communities-documentation}

* 訪問 [コミュニティのデプロイ](deploy-communities.md) を参照してください。

* 訪問 [コミュニティサイトの管理](administer-landing.md) コミュニティサイトの作成、コミュニティサイトテンプレートの設定、コミュニティコンテンツのモデレート、メンバーの管理、メッセージングの設定について説明します。

* 訪問 [コミュニティコンポーネントのオーサリング](author-communities.md) コミュニティコンポーネントを使用して作成および設定する方法を学ぶには、以下を参照してください。
