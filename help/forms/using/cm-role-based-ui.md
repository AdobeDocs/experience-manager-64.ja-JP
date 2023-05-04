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
source-git-commit: c5b816d74c6f02f85476d16868844f39b4c47996
workflow-type: tm+mt
source-wordcount: '521'
ht-degree: 9%

---


# Correspondence Management でロールベースのユーザーインターフェイスを公開しない {#do-not-publish-role-based-user-interface-in-correspondence-management}

>[!CAUTION]
>
>AEM 6.4 の拡張サポートは終了し、このドキュメントは更新されなくなりました。 詳細は、 [技術サポート期間](https://helpx.adobe.com/jp/support/programs/eol-matrix.html). サポートされているバージョンを見つける [ここ](https://experienceleague.adobe.com/docs/?lang=ja).

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

1. AEM WCM セキュリティにアクセスするには、次のいずれかの操作を行います。

   1. ようこそ画面または AEM の様々な場所で、セキュリティアイコンをクリックします。

   1. `https://[server]:[port]/useradmin` に直接アクセスします。管理者として AEM にログインしてください。

      ![]()
   左側のツリーには、現在システムに存在するすべてのユーザーとグループが一覧表示されます。 列ヘッダーを新しい位置にドラッグすると、表示する列を選択したり、列の内容を並べ替えたり、列の表示順序を変更したりできます。

   タブを使用すると、様々な設定にアクセスできます。

1. 左側のツリーリストで、関連するグループの名前をダブルタップし、「権限」タブを選択します。

   グループの名前を検索するには、指定されたスペースにグループの名前を入力します。

1. 「権限」タブで、権限を追加するパスに移動します。 Correspondence Management フォルダーは、 `content/apps/cm/` フォルダー。

   そのパスに対する権限を持つメンバーの [ メンバー ] 列のチェックボックスをオンにします。 権限を削除するメンバーのチェックボックスをオフにします。 変更を加えたセルに赤い三角形が表示されます。

   ![useradmin-creditcard](assets/useradmin-creditcard.png)

   >[!NOTE]
   >
   >フォルダーで指定された権限は、そのサブフォルダーで指定された権限に優先します。

1. 「保存」をタップします。
1. ステップテキスト
1. ステップテキスト
1. ステップテキスト

