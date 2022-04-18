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
source-git-commit: bd94d3949f0117aa3e1c9f0e84f7293a5d6b03b4
workflow-type: tm+mt
source-wordcount: '141'
ht-degree: 65%

---

# ログファイル {#log-files}

実行時や起動時のエラーなどのイベントは、アプリケーションサーバーのログファイルに記録されます。アプリケーションサーバーへのデプロイ中に問題が発生した場合には、ログファイルを参照して問題を見つけることができます。ログファイルは、テキストエディターを使用して開くことができます。

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
