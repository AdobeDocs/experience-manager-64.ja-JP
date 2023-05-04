---
title: ログファイル
seo-title: Log files
description: 実行時や起動時のエラーなどのイベントは、アプリケーションサーバーのログファイルに記録され、そのログファイルは任意のテキストエディターで開くことができます。
seo-description: Events such as run-time or startup errors are recorded to the application server log files, which can be  opened using any text editor.
uuid: 6ed9fdcd-ff02-4b35-893f-09261a6a557a
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_aem_forms
products: SG_EXPERIENCEMANAGER/6.4/FORMS
discoiquuid: cf140483-470f-4bff-8870-304207508aab
exl-id: acce13aa-864c-4999-be5c-6d49b99d5459
source-git-commit: c5b816d74c6f02f85476d16868844f39b4c47996
workflow-type: tm+mt
source-wordcount: '177'
ht-degree: 27%

---

# ログファイル {#log-files}

>[!CAUTION]
>
>AEM 6.4 の拡張サポートは終了し、このドキュメントは更新されなくなりました。 詳細は、 [技術サポート期間](https://helpx.adobe.com/jp/support/programs/eol-matrix.html). サポートされているバージョンを見つける [ここ](https://experienceleague.adobe.com/docs/?lang=ja).

実行時や起動時のエラーなどのイベントは、アプリケーションサーバーのログファイルに記録されます。 アプリケーションサーバーへのデプロイ中に問題が発生した場合は、ログファイルを使用して問題を見つけることができます。 ログファイルは、任意のテキストエディターを使用して開くことができます。

（JBoss）次のログファイルが `*[appserver root]*/server/*[server]*/log` ディレクトリにあります。

* boot.log
* server.log.*[yyyy-mm-dd]*
* server.log

(WebLogic) ドメインログファイルは、 *[appserverdomain]* ディレクトリとサーバ・ログ・ファイルは、*[appserverdomain]/servers/[appserver name]/logs *directory:

* access.log
* *[appserver name]*.log
* *[appserver name]*.out.*[増分数]*

(WebSphere) 次のログファイルが *[appserver root]*/profiles/default/logs/*[appserver name]* ディレクトリ：

* SystemErr.log
* SystemOut.log
* StartServer.log
