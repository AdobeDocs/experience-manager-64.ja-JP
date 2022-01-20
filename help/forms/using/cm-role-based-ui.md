---
title: Correspondence Management でロールベースのユーザーインターフェイスを公開しない
seo-title: DO NOT PUBLISH Role based user interface in Correspondence Management
description: Correspondence Management でロールベースのユーザーインターフェイスを公開しない
seo-description: DO NOT PUBLISH Role based user interface in Correspondence Management
page-status-flag: de-activated
uuid: 60808852-f63f-4c0a-badb-b0af93c995a8
contentOwner: gtalwar
products: SG_EXPERIENCEMANAGER/6.3/FORMS
discoiquuid: 342f111e-f15a-4f9a-8993-f90760363c02
source-git-commit: e077347bc202b6a411006032c68aa4a3152be7c5
workflow-type: tm+mt
source-wordcount: '485'
ht-degree: 26%

---


# Correspondence Management でロールベースのユーザーインターフェイスを公開しない {#do-not-publish-role-based-user-interface-in-correspondence-management}

AEMでは、管理者は、様々なユーザーグループに対して役割ベースのアクセス権を提供し、様々なリソースに対して様々なアクションを実行できます。 例えば、データディクショナリの作成や編集の機能は、特定のユーザーグループのユーザーのみが利用でき、他のユーザーはデータディクショナリの表示とユーザーのみが利用できます。

AEMインターフェイスには、ユーザーのアクセスレベルに基づいて、アセットタイプの作成や編集などのオプションが表示されます。 例えば、ユーザーがデータディクショナリを作成する権限を持っていない場合、データディクショナリを作成するオプションは UI に表示されません。

CRX では、ユーザーアカウントとグループアカウントの両方にアクセス権を設定できますが、この記事では、役割またはユーザーグループベースのアクセス権について説明します。

グループ、権限、アクセス制御リスト、およびユーザーとグループの管理について詳しくは、 [ユーザー管理とセキュリティ](/help/sites-administering/security.md).

## 権限の管理 {#managing-permissions}

1. 権限を管理するユーザーが、関連するユーザーグループに追加されていることを確認します。

   例えば、ユーザー John Doe がグループに追加されたとします。 `agents` および `cm-creditcard`. 詳細については、「ユーザーまたはグループをグループに追加する」を参照してください。 詳しくは、 [ユーザーとユーザーグループの管理](/help/communities/users.md).

   ![]()

1. 目的の権限を許可するために適したフォルダーを作成します。

   例えば、企業が住宅ローン、クレジットカード、保険部門を持っている場合、次の名前のフォルダを作成できます。 `HomeMortgage`, `CreditCard,`および `Insurance` 関連するアセットを保持し、部門に関連するアセットのエージェントにのみ選択的にアクセスできるようにする。

1. AEM WCM セキュリティにアクセスするには、次のいずれかの操作をおこないます。

   1. ようこそ画面または AEM の様々な場所で、セキュリティアイコンをクリックします。

   1. に直接移動します。 `https://[server]:[port]/useradmin`.必ずAEMに管理者としてログインしてください。

      ![]()
   システム内の現在のユーザーとグループがすべて左側のツリーに表示されます。表示する列を選択したり、列の内容を並べ替えたりできます。また、列ヘッダーを新しい位置にドラッグして列の表示順序を変更することもできます。

   タブを使用すると、様々な設定にアクセスできます。

1. 左側のツリーリストで、関連するグループの名前をダブルタップし、「権限」タブを選択します。

   グループの名前を検索するには、指定されたスペースにグループの名前を入力します。

1. 「権限」タブで、権限を追加するパスに移動します。 Correspondence Management フォルダーは、 `content/apps/cm/` フォルダー。

   対象のパスに対する権限を追加するメンバーの「メンバー」列のチェックボックスをオンにします。権限を削除するメンバーのチェックボックスはオフにしてください。変更を行ったセルには赤い三角形が表示されます。

   ![useradmin-creditcard](assets/useradmin-creditcard.png)

   >[!NOTE]
   >
   >フォルダーで指定された権限は、そのサブフォルダーで指定された権限に優先します。

1. 「保存」をタップします。
1. ステップテキスト
1. ステップテキスト
1. ステップテキスト

