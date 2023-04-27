---
title: メンテナンスモードでの AEM Forms の実行
seo-title: Running AEM forms in maintenance mode
description: メンテナンスモードは、DSC のパッチ適用、AEM Forms のアップグレード、サービスパックの適用などのタスクを実行する場合に役立ちます。 メンテナンスモードでのAEM forms の実行に関する詳細
seo-description: Maintenance mode is useful when performing tasks such as patching a DSC, upgrading AEM forms, or applying a service pack. Learn more about running AEM forms in maintenance mode.
uuid: 9aa3be20-f17e-4384-b4ce-daaee2898c96
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_aem_forms
products: SG_EXPERIENCEMANAGER/6.4/FORMS
discoiquuid: 94047c12-ba3d-457a-954f-e035c7cc3ecd
exl-id: 2f56bbc7-5e23-4c84-ac0a-03f0b01150b3
source-git-commit: bd94d3949f0117aa3e1c9f0e84f7293a5d6b03b4
workflow-type: tm+mt
source-wordcount: '274'
ht-degree: 8%

---

# メンテナンスモードでの AEM Forms の実行 {#running-aem-forms-in-maintenance-mode}

メンテナンスモードは、DSC のパッチ適用、AEM Forms のアップグレード、サービスパックの適用などのタスクを実行する場合に役立ちます。

サーバーがメンテナンスモードの間は、プロセスを呼び出さないでください。 サーバーがメンテナンスモードの間にプロセスが呼び出された場合は、次のようになります。

* プロセスが長期間有効な場合、ジョブデータベースに追加されますが、開始されません。 メンテナンスモードを終了すると、メンテナンスモード中にサーバーを再起動した場合でも、AEM forms はキュー内の長期間有効なジョブを処理します。
* プロセスの有効期間が短い場合は、すぐに処理されます。

**AEM forms をメンテナンスモードにする**

1. Web ブラウザーに次のように入力します。

   `https://`*[hostname ]*`:`*[ポート]* `/dsc/servlet/DSCStartupServlet?maintenanceMode=pause&user=`*[管理者ユーザー名&#x200B;]*`&password=`*[パスワード]*

   ブラウザーウィンドウに「一時停止中」のメッセージが表示されます。

   >[!NOTE]
   >
   >メンテナンスモードの間にサーバーをシャットダウンした場合、サーバーを再起動してもメンテナンスモードのままです。 メンテナンスタスクが終了したら、メンテナンスモードをオフにする必要があります。

**AEM forms がメンテナンスモードで実行されているかどうかの確認**

1. Web ブラウザーに次のように入力します。

   `https://`*[hostname]:[ポート&#x200B;]*`/dsc/servlet/DSCStartupServlet?maintenanceMode=isPaused&user=`*[管理者ユーザー名]* `&password=`*[パスワード&#x200B;]*

   ブラウザーウィンドウにステータスが表示されます。 ステータスが「true」の場合は、サーバーがメンテナンスモードで実行されていることを示し、「false」の場合は、サーバーがメンテナンスモードではありません。

**メンテナンスモードをオフにする**

1. Web ブラウザーに次のように入力します。

   `https://`*[hostname]:[ポート&#x200B;]*`/dsc/servlet/DSCStartupServlet?maintenanceMode=resume&user=`*[管理者ユーザー名]* `&password=`*[パスワード&#x200B;]*

   ブラウザーウィンドウに「実行中」のメッセージが表示されます。
