---
title: トラブルシューティングプロセスのレポート
seo-title: Troubleshooting Process Reporting
description: JEE プロセスレポート上の AEM Forms における問題のトラブルシューティング
seo-description: Troubleshoot issues in AEM Forms on JEE Process Reporting
page-status-flag: de-activated
uuid: 1c1cc27c-fbed-4366-bffe-e1581d269a93
content-type: reference
products: SG_EXPERIENCEMANAGER/6.4/FORMS
discoiquuid: 0a818d19-8804-4c69-b721-31c347c593c0
exl-id: 57ddfead-22bb-4a99-925e-11d71fc61669
source-git-commit: c5b816d74c6f02f85476d16868844f39b4c47996
workflow-type: tm+mt
source-wordcount: '140'
ht-degree: 80%

---

# トラブルシューティングプロセスのレポート {#troubleshooting-process-reporting}

>[!CAUTION]
>
>AEM 6.4 の拡張サポートは終了し、このドキュメントは更新されなくなりました。 詳細は、 [技術サポート期間](https://helpx.adobe.com/jp/support/programs/eol-matrix.html). サポートされているバージョンを見つける [ここ](https://experienceleague.adobe.com/docs/?lang=ja).

## Microsoft Windows 7 上の Internet Explorer 9 でフィルターを作成する際に発生する問題 {#issues-faced-in-creating-filters-on-internet-explorer-on-microsoft-windows}

定義済みレポートのフィルターを作成すると、**Microsoft Windows 7** 環境の **Internet Explorer 9** 上で、次の問題が断続的に発生します。

* 「値」フィールドのドロップダウンリストに、値の代わりに一意の識別子が表示されます。
* 「値」フィールドのカレンダーコントロールが、日本語の文字を表示します。
* 「条件」フィールドが表示されません。
* 「値」フィールドのカレンダーコントロールが表示されません。

### 解像度 {#resolution}

プロセスレポートにログインしているとき：

1. ブラウザーのキャッシュをクリアします。
1. ブラウザー画面を更新します。
