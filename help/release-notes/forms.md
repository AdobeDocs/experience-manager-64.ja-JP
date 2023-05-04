---
title: AEM Forms
seo-title: AEM Forms
description: リリースノート (Adobe Experience Manager 6.3 Forms固有 )
seo-description: Release notes specific to Adobe Experience Manager 6.3 Forms.
uuid: 317770c9-bb59-4bdf-8a14-be265e8f5f81
contentOwner: khsingh
products: SG_EXPERIENCEMANAGER/6.4
topic-tags: release-notes
content-type: reference
discoiquuid: 3f592c5a-4e59-436e-b67b-3ed575c6afc3
exl-id: 94989316-02df-4cfa-bb2e-c0d357dff728
source-git-commit: c5b816d74c6f02f85476d16868844f39b4c47996
workflow-type: tm+mt
source-wordcount: '399'
ht-degree: 3%

---

# AEM Forms {#aem-forms}

>[!CAUTION]
>
>AEM 6.4 の拡張サポートは終了し、このドキュメントは更新されなくなりました。 詳細は、 [技術サポート期間](https://helpx.adobe.com/jp/support/programs/eol-matrix.html). サポートされているバージョンを見つける [ここ](https://experienceleague.adobe.com/docs/?lang=ja).

この節では、AEM 6.4 Formsリリースの主な機能について説明します。 すべての新機能の詳細については、 [AEM 6.4 Formsの新機能および機能強化の概要](/help/forms/using/whats-new.md).

## マルチチャネルインタラクティブ通信 {#multi-channel-interactive-communications}

* 印刷チャネルと Web チャネル用の統合されたマルチチャネルオーサリングインターフェイス
* ビジネスユーザーにとって使いやすい WYSIWYG とドラッグ&amp;ドロップベースのオーサリング
* 統合アセットリポジトリ、標準コンポーネント、データモデル
* 印刷チャネルと Web チャネルの両方に共通のドキュメントフラグメントを使用して作業を軽減
* 印刷チャネルから Web チャネルコンテンツを自動生成する機能
* 一貫したスタイルとブランディングを提供するテーマのサポート
* 印刷チャネルと Web チャネルの両方をサポートする拡張エージェントインターフェイス
* 通信でより豊富なデータ視覚化を提供するグラフ
* フォームデータモデルを介した通信におけるバックエンドデータの統合に対する、そのまま使用できるサポート
* ドキュメントフラグメントでフォームデータモデル要素を使用する機能
* レターおよびデータ辞書を使用した顧客のアップグレードをサポートする互換性パッケージ

## データ統合の強化 {#data-integration-enhancements}

* データソースを使用せずにフォームデータモデルを作成する機能
* フォームやインタラクティブ通信の作成者にデータソースへの依存を避けるために、データソースをフォームデータモデルに遅延バインディングする
* 既存のフォームデータモデルでエンティティとプロパティを作成し、後でデータソースにバインドする機能
* フォームデータモデルエンティティのデータに対するルールを使用し、フォームと通信で使用する計算済みプロパティ
* 開発時にフォームとドキュメントのプレビューに役立つサンプルデータを生成またはフォームデータモデルに関連付ける機能
* フォームデータモデルのデータソース定義を更新して、バックエンドのデータソースの変更を反映する
* データソース設定にタッチ操作対応 UI インターフェイスを利用する

## ワークフローの最新化とモバイルワーカーのサポート {#workflow-modernization-and-mobile-worker-support}

* ワークフローモデルを設計するためのタッチインターフェイス
* ワークフローステップを通じてフォームデータモデルの操作を呼び出す機能
* E メールを簡単に送信するための E メールワークフローステップ
* AEM Formsアプリでのフォームデータモデルを使用したアダプティブフォームのサポート
* 遅延読み込みされたフラグメントを含むアダプティブフォームをAEM Formsアプリで使用する

## 遅延読み込みフラグメントのサポートの強化 {#enhanced-support-of-lazy-loading-fragments}

* 遅延読み込みされたフォームフラグメントで、添付ファイルと利用条件のコンポーネントを使用できます
* 繰り返し可能パネル内での遅延読み込みアダプティブフォームフラグメントのサポート

## LiveCycleからExperience Manager Forms 6.4 へのシングルホップアップグレード {#single-hop-upgrade-from-livecycle-to-experience-manager-forms}

* LiveCycleES4 からAEM 6.4 Forms JEE への直接アップグレード
