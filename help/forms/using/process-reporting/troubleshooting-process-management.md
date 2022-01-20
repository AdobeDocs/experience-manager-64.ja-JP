---
title: トラブルシューティングプロセスのレポート
seo-title: Troubleshooting Process Reporting
description: JEE 上のAEM Forms Process Reporting の問題のトラブルシューティング
seo-description: Troubleshoot issues in AEM Forms on JEE Process Reporting
page-status-flag: de-activated
uuid: 1c1cc27c-fbed-4366-bffe-e1581d269a93
content-type: reference
products: SG_EXPERIENCEMANAGER/6.4/FORMS
discoiquuid: 0a818d19-8804-4c69-b721-31c347c593c0
exl-id: 57ddfead-22bb-4a99-925e-11d71fc61669
source-git-commit: bd94d3949f0117aa3e1c9f0e84f7293a5d6b03b4
workflow-type: tm+mt
source-wordcount: '104'
ht-degree: 4%

---

# トラブルシューティングプロセスのレポート {#troubleshooting-process-reporting}

## Microsoft Windows 7 上の Internet Explorer 9 でフィルターを作成する際に発生する問題 {#issues-faced-in-creating-filters-on-internet-explorer-on-microsoft-windows}

定義済みレポートのフィルターを作成する場合、 **Internet Explorer 9** 対象 **Microsoft Windows 7** 環境：

* 「値」フィールドのドロップダウンリストには、値の代わりに一意の ID が表示されます。
* 「値」フィールドのカレンダーコントロールには、日本語の文字が表示されます。
* 「条件」フィールドは表示されません。
* 「値」フィールドのカレンダーコントロールは表示されません。

### 解像度 {#resolution}

Process Reporting にログインした状態で、次の操作を実行します。

1. ブラウザーのキャッシュをクリアします。
1. ブラウザー画面を更新します。
