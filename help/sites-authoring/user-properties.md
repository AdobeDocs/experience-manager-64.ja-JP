---
title: 'アカウント環境の設定 '
seo-title: Configuring your account environment
description: AEM では、アカウントおよびオーサー環境の特定項目を設定できます
seo-description: AEM provides you with the capability to configure your account and certain aspects of the author environment
uuid: 01e76771-9ac8-4919-9e50-0a63826177d1
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.4/SITES
topic-tags: introduction
content-type: reference
discoiquuid: 6afbc889-c613-40e6-8a25-1570dff32d60
exl-id: f620e85e-8c77-41a3-a238-9b93c819909d
source-git-commit: bd94d3949f0117aa3e1c9f0e84f7293a5d6b03b4
workflow-type: tm+mt
source-wordcount: '481'
ht-degree: 96%

---

# アカウント環境の設定 {#configuring-your-account-environment}

AEM では、アカウントおよびオーサー環境の特定項目を設定できます。

の使用 [ユーザー](/help/sites-authoring/user-properties.md#user-settings) オプション [ヘッダー](/help/sites-authoring/basic-handling.md#the-header) そして関連する [環境設定](#my-preferences) ダイアログで、ユーザオプションを変更できます。

## ユーザー設定 {#user-settings}

**ユーザー**&#x200B;設定ダイアログでは、次の機能にアクセスできます。

* 次のユーザーとして操作

   * [次のユーザーとして動作](/help/sites-administering/security.md#impersonating-another-user)機能では、ユーザーは別のユーザーに成り代わって作業をおこなうことができます。

* プロファイル

   * [ユーザー設定](/help/sites-administering/security.md)への便利なリンクを提供します。

* [環境設定](/help/sites-authoring/user-properties.md#my-preferences)

   * ユーザー独自の様々な環境設定を指定します。

![screen_shot_2018-03-20at103808](assets/screen_shot_2018-03-20at103808.png)

## 環境設定 {#my-preferences}

**環境設定**&#x200B;ダイアログには、ヘッダーの「[ユーザー](/help/sites-authoring/user-properties.md#user-settings)」オプションを使用してアクセスできます。

各ユーザーは、自分の特定のプロパティを設定できます。

![screen_shot_2018-03-20at102118](assets/screen_shot_2018-03-20at102118.png)

* **言語**

   オーサリング環境の UI で使用する言語を定義します。使用できるリストから必要な言語を選択します。

   この設定は、クラシック UI でも使用されます。

* **ウィンドウ管理**

   ウィンドウの動作や開くウィンドウを定義します。次のいずれかを選択します。

   * **複数ウィンドウ**（デフォルト）

      * 新しいウィンドウでページが開きます。
   * **単一ウィンドウ**

      * 現在のウィンドウでページが開きます。


* **アセットのデスクトップアクションを表示**

   このオプションを使用するには、AEM デスクトップアプリケーションが必要です。

* **注釈カラー**

   注釈を作成する際のデフォルトのカラーを定義します。

   * カラーブロックをクリックすると、色を選択するためのスウォッチセレクターが表示されます。
   * または、フィールドに目的のカラーの 16 進コードを入力します。

* **相対的な日付の表示**

   読みやすくするために、AEM では、過去 7 日以内の日付を相対日付（例： 3 日前）で表示し、それ以前の日付を正確な日付（例：2017 年 3 月 20 日）で表示します。

   このオプションは、システムの日付の表示方法を定義します。以下のオプションが利用できます。

   * **常に正確な日付を表示**：常に正確な日付が表示されます（相対日付は表示されません）。
   * **1 日**：1 日以内の日付に相対日付が表示され、それ以外は正確な日付が表示されます。
   * **7 日（デフォルト）**：7 日以内の日付に相対日付が表示され、それ以外は正確な日付が表示されます。
   * **1 ヶ月**：1 ヶ月以内の日付に相対日付が表示され、それ以外は正確な日付が表示されます。
   * **1 年**：1 年以内の日付に相対日付が表示され、それ以外は正確な日付が表示されます。
   * **常に相対日付を表示**：正確な日付は表示されず、相対日付のみが表示されます。

* **ショートカットを有効にする**

   AEM には、オーサリングの効率性を高める多くのキーボードショートカットがあります。

   * [ページ編集時のキーボードショートカット](/help/sites-authoring/page-authoring-keyboard-shortcuts.md)
   * [コンソールのキーボードショートカット](/help/sites-authoring/keyboard-shortcuts.md)

   このオプションは、キーボードショートカットを有効にします。デフォルトでは有効になっていますが、例えばユーザーに特定のアクセシビリティ要件がある場合に、無効にできます。

* **従来のオーサリング機能を使用**

   このオプションは、[クラシック UI](/help/sites-classic-ui-authoring/home.md) ベースのページオーサリングを有効にします。デフォルトでは、標準 UI が使用されます。

* **アセットのホームページを有効にする**

   このオプションは、システム管理者がアセットホームページの使用を組織全体で有効にしている場合にのみ使用できます。
