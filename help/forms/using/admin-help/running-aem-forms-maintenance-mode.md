---
title: メンテナンスモードでの AEM Forms の実行
seo-title: メンテナンスモードでの AEM Forms の実行
description: メンテナンスモードは、DSC のパッチ適用、AEM Forms のアップグレード、サービスパックの適用などのタスクを実行するときに役立ちます。メンテナンスモードでの AEM Forms の実行について詳しく学びます。
seo-description: メンテナンスモードは、DSC のパッチ適用、AEM Forms のアップグレード、サービスパックの適用などのタスクを実行するときに役立ちます。メンテナンスモードでの AEM Forms の実行について詳しく学びます。
uuid: 9aa3be20-f17e-4384-b4ce-daaee2898c96
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_aem_forms
products: SG_EXPERIENCEMANAGER/6.4/FORMS
discoiquuid: 94047c12-ba3d-457a-954f-e035c7cc3ecd
exl-id: 2f56bbc7-5e23-4c84-ac0a-03f0b01150b3
source-git-commit: bd94d3949f0117aa3e1c9f0e84f7293a5d6b03b4
workflow-type: tm+mt
source-wordcount: '309'
ht-degree: 95%

---

# メンテナンスモードでの AEM Forms の実行 {#running-aem-forms-in-maintenance-mode}

メンテナンスモードは、DSC のパッチ適用、AEM Forms のアップグレード、サービスパックの適用などのタスクを実行するときに役立ちます。

サーバーがメンテナンスモードのときはプロセスを一切開始しないでください。サーバーがメンテナンスモードのときにプロセスを開始すると、次の問題が発生します。

* プロセスの有効期間が長い場合、プロセスはジョブデータベースに追加されますが開始されません。メンテナンスモードを終了すると、メンテナンスモード中にサーバーが再起動した場合でも、キューにある長期間有効なジョブが AEM Forms で処理されます。
* プロセスの有効期間が短い場合はすぐに処理されます。

**AEM Forms をメンテナンスモードにする**

1. Web ブラウザーに次のように入力します。

   `https://`*[]*`:`*[]* `/dsc/servlet/DSCStartupServlet?maintenanceMode=pause&user=`*[hostnameportadministrator ]*`&password=`*[usernamepassword]*

   ブラウザーウィンドウに「一時停止中」のメッセージが表示されます。

   >[!NOTE]
   >
   >メンテナンスモードの間にサーバーをシャットダウンすると、再起動してもメンテナンスモードのままです。メンテナンスタスクを終了したら、メンテナンスモードをオフにする必要があります。

**AEM Forms がメンテナンスモードで実行中かどうかの確認**

1. Web ブラウザーに次のように入力します。

   `https://`*[hostname]:[]*`/dsc/servlet/DSCStartupServlet?maintenanceMode=isPaused&user=`*[portadministrator usernamepassword]* `&password=`*[]*

   ブラウザーウィンドウにステータスが表示されます。「true」のステータスはサーバーがメンテナンスモードで動作中であることを示し、「false」はサーバーがメンテナンスモードではないことを示します。

**メンテナンスモードのオフ**

1. Web ブラウザーに次のように入力します。

   `https://`*[hostname]:[]*`/dsc/servlet/DSCStartupServlet?maintenanceMode=resume&user=`*[portadministrator usernamepassword]* `&password=`*[]*

   ブラウザーウィンドウに「実行中」のメッセージが表示されます。
