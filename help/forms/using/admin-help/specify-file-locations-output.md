---
title: Output のファイルの場所の指定
seo-title: Specify file locations for Output
description: Output のファイルの場所を指定する方法を説明します。
seo-description: Learn how to specify file locations for Output.
uuid: 3287274f-85b5-4811-8abb-d347a9b80947
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_output
products: SG_EXPERIENCEMANAGER/6.4/FORMS
discoiquuid: 460bbb31-8187-469c-8102-b310093b6c03
exl-id: 5b8f04dd-6781-4126-8bb2-5d8b7a2f19c8
source-git-commit: bd94d3949f0117aa3e1c9f0e84f7293a5d6b03b4
workflow-type: tm+mt
source-wordcount: '314'
ht-degree: 61%

---

# Output のファイルの場所の指定 {#specify-file-locations-for-output}

Output で必要な特定の種類のファイルを検索する場所を指定できます。

1. 管理コンソールで、サービス／Output をクリックします。
1. 「場所」で、適切なオプションを指定します。
1. 「保存」をクリックします。

## 場所の設定 {#locations-settings}

**コンテンツルート URI：**&#x200B;フォームの取得元であるリポジトリの URI または絶対位置。この値と、API 経由で指定された sForm パラメーターを連結して、フォームの取得元である絶対パスが作られます。この値は、HTTP を使用してアクセス可能なディレクトリまたは Web の場所を参照できます。

デフォルト値は空の文字列です。

**XCI 設定ファイル：** Output サービスがレンダリングで使用する XCI 設定ファイルの相対位置または絶対位置です。相対パスの場合は、AEM Forms のデプロイ可能な EAR ファイル内に XCI ファイルが保存されていることが前提となります。

デフォルト値は `com/adobe/formServer/PA/pa_output.xci` です。

**キャッシュの場所：** Output ディスクキャッシュの場所を指定します。この設定を変更すると、現在の場所の既存のキャッシュ情報がすべてリセットされ、新しいキャッシュが新しい場所に作成されます。 次のいずれかのオプションを選択します。

**デフォルトの場所：** これはデフォルトの選択です。このオプションを選択すると、次のように使用しているアプリケーションサーバーによって決まる場所にキャッシュが作成されます。

* **JBoss:** `[JBoss Home]\server\[install type]\svcdata\Output\Cache`
* **WebLogic:** `[WebLogic Home]\user_projects\domains\[aem-forms domain Name]\adobe\[forms server name]\Output\Cache`
* **WebSphere:** `[IBM Home]\WebSphere\AppServer\installedApps\adobe\server1\Output\Cache`

**LC の一時ディレクトリ：**&#x200B;キャッシュは、AEM Forms の一時ディレクトリのサブディレクトリ（管理コンソールの、設定／コアシステム設定／設定／一時ディレクトリの場所で指定）に作成されます。サブディレクトリの名前は `adobeoutput_[servername]` です。

>[!NOTE]
>
>一時クリーニングユーティリティを使用している場合、これらのディレクトリを削除しても機能に影響はありませんが、新しいキャッシュが作成されるまで、短時間のパフォーマンスに大きな影響が及ぶ可能性があります。 この問題を回避するには、AEM forms の一時ディレクトリをクリアする際に、これらのディレクトリを削除しないでください。
