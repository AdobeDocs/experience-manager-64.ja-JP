---
title: AEM Forms Workspace のアーキテクチャ
seo-title: AEM Forms Workspace Architecture
description: LiveCycleAEM Forms Workspace の概念情報とアーキテクチャの概要です。
seo-description: Conceptual information and overview of the architecture of LiveCycle AEM Forms workspace.
uuid: e1a48452-ed44-4ea7-ba38-d961c8faafa5
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.4/FORMS
topic-tags: forms-workspace
discoiquuid: c3a312fb-f684-477d-916d-2d3c99aa7607
exl-id: 30bde8d6-7959-4e4b-a6f4-faf52444e67a
source-git-commit: bd94d3949f0117aa3e1c9f0e84f7293a5d6b03b4
workflow-type: tm+mt
source-wordcount: '219'
ht-degree: 31%

---

# AEM Forms Workspace のアーキテクチャ {#aem-forms-workspace-architecture}

AEM Forms workspace は、CRX™でホストされる Web アプリケーションです。 ワークスペースをブラウザーで開くと、CRX リソースにアクセスし、アプリケーションがブラウザーでHTMLページとしてレンダリングされます。

アプリケーションは、REST エンドポイント上のAEM Formsサーバーにアクセスし、次の操作を実行します。

* ユーザータスク、プロセスの開始点、プロセス履歴、およびユーザー情報を取得します
* タスクに対するアクションの実行
* データベースのクエリタスク
* ユーザーの環境設定の更新など

AEM Formsサーバーは、JDBC を介してAEM Formsデータベースにアクセスします。 データベースには、タスク、プロセス、そのインスタンス、ユーザー、および関連情報が保持されます。

AEM Forms Workspace は、モジュール形式の JavaScript™ コンポーネントで組み立てられており、これらのコンポーネントは他の Web アプリケーションで個々にカスタマイズしたり再利用することができます。コンポーネントは、Web アプリケーションに構造を提供する JavaScript ライブラリである BackBone に基づいています。 コンポーネントと BackBone の相互作用を説明する詳細な記事は次のとおりです。 [ここ](/help/forms/using/backbone-interaction.md). CRX フォルダー構造内のコンポーネントの構成については、 [この](/help/forms/using/folder-structure.md) 記事。

AEM Forms Workspace 用に配信されたパッケージ：

* `adobe-lc-workspace-pkg-<version>.zip`：これは CRX パッケージです。すなわち、Package Manager を使用して CRX 内にデプロイできます。
* `adobe-lc-workspace-<version>-src.zip`：デプロイパッケージ（Ship、Debug、および Dev パッケージ）を作成するための AEM Forms Workspace とスクリプトの完全なコードを含むアーカイブです。
