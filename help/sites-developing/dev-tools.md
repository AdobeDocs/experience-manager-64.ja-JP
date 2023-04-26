---
title: 開発ツール
seo-title: Development Tools
description: JCR、Apache Sling、AEMの各アプリケーションを開発するために、多数のツールセットを使用できます
seo-description: To develop your JCR, Apache Sling or AEM applications, a number of tool sets are available
uuid: 1bee3a52-5d76-4b0c-a222-a02e12ff3a43
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.4/SITES
topic-tags: development-tools
content-type: reference
discoiquuid: 76c570e5-46ed-46be-9864-4fe4a83f0caf
exl-id: 3c18feab-97a6-49f2-96be-7e7458199f5d
source-git-commit: bd94d3949f0117aa3e1c9f0e84f7293a5d6b03b4
workflow-type: tm+mt
source-wordcount: '392'
ht-degree: 74%

---

# 開発ツール{#development-tools}

JCR、Apache Sling、AEMの各アプリケーションを開発するには、次のツールセットを使用できます。

* [CRXDE Lite](/help/sites-developing/developing-with-crxde-lite.md) と WebDAV で構成されたツールセット。CRXDE Lite は CRX／AEM に搭載されており、これを使用してブラウザー内で標準的な開発作業を実行できます。CRXDE Lite を使用すると、ファイル（.jsp、.java など）、フォルダー、テンプレート、コンポーネント、ダイアログ、ノード、プロパティおよびバンドルを作成、編集することができ、さらに SVN によるロギングや統合が可能です。

   CRX/AEMサーバーに直接アクセスできない場合、標準のコンポーネントと Java バンドルを拡張または変更してアプリケーションを開発する場合、または専用のデバッガー、コード補完および構文ハイライトが必要ない場合に、CRXDE Liteをお勧めします。

* 統合開発環境（例：[Eclipse](/help/sites-developing/howto-projects-eclipse.md) または [IntelliJ](/help/sites-developing/ht-intellij.md)）、ビルドツール（例：[Apache Maven](/help/sites-developing/ht-projects-maven.md)）、リポジトリをファイルシステムにマッピングするために開発された FileVault、バージョン管理システム（例：Subversion）、バグ追跡システム（例：JIRA）、依存関係中央管理システム（例：Apache Archiva）およびビルド自動化システム（例：Apache Continuum）から構成されたツールセット。

   このセットアップで、アプリケーション（コンテンツ、コード、設定）をあらゆる開発環境とプロセスに完全に統合できます。リポジトリのファイルシステムは FileVault によって様々な要素間のリンクで表わされ、前述のすべての開発ツールでファイルを操作できます。

## 統合開発環境の拡張 {#extensions-for-integrated-development-environments}

Adobeは、次の拡張機能をリリースしました。

* [AEM Eclipse 拡張](/help/sites-developing/aem-eclipse.md)
* [AEM Brackets Extension](/help/sites-developing/aem-brackets.md)
* [AEM IntelliJ 拡張](https://github.com/headwirecom/aem-ide-tooling-4-intellij/blob/master/documenation/AEM%20Tooling%20Plugin%20for%20IntelliJ%20IDEA.pdf)（Headwire）

### その他のツール {#other-tools}

AEMには、開発を容易にする他のツールが付属しています。

* [ダイアログエディター](/help/sites-developing/dialog-editor.md)
* [トランスレーターを使用した辞書の管理](/help/sites-developing/i18n-translator.md)
* [Maven を使用したパッケージの管理](/help/sites-developing/vlt-mavenplugin.md)
* [Eclipse を使用して AEM プロジェクトを開発する方法](/help/sites-developing/howto-projects-eclipse.md)
* [Apache Maven を使用して AEM プロジェクトをビルドする方法](/help/sites-developing/ht-projects-maven.md)
* [IntelliJ IDEA を使用して AEM プロジェクトを開発する方法](/help/sites-developing/ht-intellij.md)
* [VLT ツールを使用する方法](/help/sites-developing/ht-vlttool.md)
* [プロキシサーバーツールを使用する方法](/help/sites-developing/ht-proxy-server.md)
* [AEM Modernization Tools](/help/sites-developing/modernization-tools.md)
* [AEM Repo ツール](/help/sites-developing/aem-repo-tool.md)

以下は、新しいプロジェクトの作成に役立つツールです。

* [AEM プロジェクトアーキタイプ](https://github.com/Adobe-Marketing-Cloud/aem-project-archetype)
* [AEM Lazybones テンプレート](https://github.com/Adobe-Consulting-Services/lazybones-aem-templates)

>[!NOTE]
>
>新しい AEM プロジェクトを開始する際には、次のチュートリアルが参考になる場合があります。\
>[AEM Sites の概要（第 1 章）- プロジェクトの設定](https://helpx.adobe.com/experience-manager/kt/sites/using/getting-started-wknd-tutorial-develop/part1.html)
