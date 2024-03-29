---
title: AEM Repo ツール
seo-title: AEM Repo Tool
description: AEM Repo ツールは、FTP に相当するコマンドラインを使用してローカルファイルシステムと AEM サーバーの間で JCR コンテンツを転送するためのシンプルなソリューションです。AEM Repo ツールは、Jackrabbit FileVault ツールに似ていますが、より高速で依存関係が最小限であり、シンプルな bash スクリプトです。
seo-description: The AEM Repo Tool is a simple solution to transfer JCR content between your local filesystem and the AEM server via the command line comparable to FTP. The AEM Repo Tool is similar to the Jackrabbit FileVault tool, but is faster, has minimal dependencies, and is a simple bash script.
uuid: 6c4a3504-e8e8-46c0-83cb-c18d9791f93e
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.4/SITES
topic-tags: development-tools
content-type: reference
discoiquuid: 7de7b2f9-770e-4af3-8a31-c7b4de64fd43
exl-id: 8da27ef5-bb61-4246-8a13-96a60188ebbb
source-git-commit: c5b816d74c6f02f85476d16868844f39b4c47996
workflow-type: tm+mt
source-wordcount: '320'
ht-degree: 77%

---

# AEM Repo ツール{#aem-repo-tool}

>[!CAUTION]
>
>AEM 6.4 の拡張サポートは終了し、このドキュメントは更新されなくなりました。 詳細は、 [技術サポート期間](https://helpx.adobe.com/jp/support/programs/eol-matrix.html). サポートされているバージョンを見つける [ここ](https://experienceleague.adobe.com/docs/?lang=ja).

AEM Repo ツールは、FTP に相当するコマンドラインを使用してローカルファイルシステムと AEM サーバーの間で JCR コンテンツを転送するためのシンプルなソリューションです。AEM Repo ツールは、[Jackrabbit FileVault ツール](/help/sites-developing/ht-vlttool.md)に似ていますが、より高速で依存関係が最小限であり、シンプルな bash スクリプトです。

このツールは、開発者向けのファイルの転送を簡素化し、IntelliJ と Eclipse に統合して開発をより効率的にすることもできます。

## 概要 {#overview}

ファイルシステム上の `jcr_root` filevault 構造内の特定のパスの場合、AEM Repo ツールは、サブツリー全体に対する単一のフィルターを含むパッケージを作成し、それをサーバーにプッシュして（FTP の `put` と同じ）、サーバーから取得（`get`）または違いを比較（`status` および `diff`）します。

このツールは、複数のフィルターパスや FileVault の `filter.xml` をサポートしません。

>[!CAUTION]
>
>AEM Repo Tool は常に、指定されたファイルまたはディレクトリ全体を上書きします。

## ダウンロードとドキュメント {#download-and-documentation}

[AEM Repo ツールは、このリンクの GitHub で利用できます](https://github.com/Adobe-Marketing-Cloud/tools/tree/master/repo)。詳細なインストールおよび使用手順も用意されています。

AEM Repo ツールのソースをダウンロードする場合は、GitHub プロジェクト（次のリンク）を参照してください。

GitHub のコード

このページのコードは GitHub にあります

* [GitHub でツールのプロジェクトを開きます](https://github.com/Adobe-Marketing-Cloud/tools)
* プロジェクトを [ZIP ファイル](https://github.com/Adobe-Marketing-Cloud/tools/archive/master.zip)としてダウンロードします
