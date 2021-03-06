---
title: タイムラインのアクティビティストリーム
description: 'この記事では、アセットのアクティビティログをタイムラインに表示する方法について説明します。 '
contentOwner: AG
feature: Asset Management
role: User,Admin
exl-id: 52fa2d59-177f-49ca-a480-7213ce0ca7d7
source-git-commit: 1679bbab6390808a1988cb6fe9b7692c3db31ae4
workflow-type: tm+mt
source-wordcount: '211'
ht-degree: 85%

---

# タイムラインのアクティビティストリーム {#activity-stream-in-timeline}

この機能は、タイムラインにアセットのアクティビティログを表示します。[!DNL Adobe Experience Manager Assets] で以下のアセット関連操作を実行すると、アクティビティストリーム機能により、タイムラインが更新され、そのアクティビティが反映されます。

アクティビティストリームでログに記録される操作は次のとおりです。

* 作成
* 削除
* ダウンロード（レンディションを含む）
* 公開
* 非公開
* 承認
* 拒否
* 移動

タイムラインに表示されるアクティビティログは、ログファイルが格納されている CRX の `/var/audit/com.day.cq.dam/content/dam` から取得されます。

さらに、新しいアセットがアップロードされたり、既存のアセットが変更され、を通じてExperience Managerにチェックインされたりすると、タイムラインアクティビティがログに記録されます。 [Adobeアセットリンク](https://helpx.adobe.com/jp/enterprise/admin-guide.html/enterprise/using/manage-assets-using-adobe-asset-link.ug.html) または [[!DNL Experience Manager] デスクトップアプリ](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/introduction.html?lang=ja).

>[!NOTE]
>
>一時的なワークフローは、履歴情報が保存されないので、タイムラインに表示されません。

アクティビティストリームを表示するには、アセットに対して 1 つ以上の操作を実行して、アセットを選択してから、グローバルナビゲーションリストから&#x200B;**[!UICONTROL タイムライン]**&#x200B;を選択します。

![timeline-3](assets/timeline-3.png)

タイムラインに、アセットに対して実行した操作のアクティビティストリームが表示されます。

![activity_stream](assets/activity_stream.png)

>[!NOTE]
>
>**公開**&#x200B;タスクと&#x200B;**非公開**&#x200B;タスクのデフォルトのログ保管先は `/var/audit/com.day.cq.replication/content` です。**移動**&#x200B;タスクの場合は、デフォルトの保管先は `/var/audit/com.day.cq.wcm.core.page` になります。
