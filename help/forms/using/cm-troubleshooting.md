---
title: 「Correspondence Management：トラブルシューティング」
seo-title: Correspondence Management Troubleshooting
description: Correspondence Management のトラブルシューティング
seo-description: Correspondence Management Troubleshooting
uuid: 25828cdd-110e-4a84-8f31-d82cd610a54f
content-type: reference
products: SG_EXPERIENCEMANAGER/6.4/FORMS
topic-tags: correspondence-management
discoiquuid: cc473808-e71a-4834-bb30-91e6df783e60
feature: Correspondence Management
exl-id: 82a35d81-13d0-435f-875e-6fd0a6d574d5
source-git-commit: bd94d3949f0117aa3e1c9f0e84f7293a5d6b03b4
workflow-type: tm+mt
source-wordcount: '199'
ht-degree: 24%

---

# Correspondence Management：トラブルシューティング {#correspondence-management-troubleshooting}

## レターを保存する際のエラー {#errors-when-saving-a-letter}

### 問題 {#issue}

レターを保存する際に、次のエラーの 1 つが表示されます。

* テキストモジュールのデータ連結が存在しません
* 次に必要なプロパティ情報を指定してください

### 理由 {#reason}

これらのエラーは、次のいずれかが原因で発生する可能性があります。

* データディクショナリはレターにバインドされていますが、サーバーに存在しません。
* データディクショナリは文字にバインドされていますが、名前にアンダースコア (_) が含まれています。

### 対処方法 {#workaround}

レターで使用しているデータディクショナリがサーバー上に存在し、名前にアンダースコア (_) が含まれていないことを確認します。

## レターをプレビュー中にエラーが発生しました {#error-when-previewing-a-letter}

### 問題 {#issue-1}

レターのプレビュー中に、「レターの読み込み中にエラーが発生しました：レター内の非公開のテキストアセットが公開されている場合でも、「XML 入力からアセットを読み込めませんでした」と表示されます。

### 対処方法 {#workaround-1}

次の手順を使用して発行インスタンスのレターキャッシュをリセットし、レターの表示を再試行します。

1. **`https://[server]:[port]/[contextPath]/system/console/configMgr`** に移動して管理者としてログインします。
1. 「**Correspondence Management の設定**」を選択します。
1. 「**Correspondence Management の設定**」で、「**レターのキャッシュを有効にする**」を無効にして「**保存**」をクリックします。
1. 「**レターのキャッシュを有効にする**」を無効にし、「**保存**」をクリックします。
1. レターの表示をもう一度やり直します。
