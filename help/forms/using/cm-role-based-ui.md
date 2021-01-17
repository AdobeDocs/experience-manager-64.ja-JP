---
title: Correspondence Managementでロールベースのユーザーインターフェイスを発行しない
seo-title: Correspondence Managementでロールベースのユーザーインターフェイスを発行しない
description: Correspondence Managementでロールベースのユーザーインターフェイスを発行しない
seo-description: Correspondence Managementでロールベースのユーザーインターフェイスを発行しない
page-status-flag: de-activated
uuid: 60808852-f63f-4c0a-badb-b0af93c995a8
contentOwner: gtalwar
products: SG_EXPERIENCEMANAGER/6.3/FORMS
discoiquuid: 342f111e-f15a-4f9a-8993-f90760363c02
translation-type: tm+mt
source-git-commit: e077347bc202b6a411006032c68aa4a3152be7c5
workflow-type: tm+mt
source-wordcount: '505'
ht-degree: 25%

---


# Correspondence Managementのロールベースのユーザーインターフェイスを発行しない{#do-not-publish-role-based-user-interface-in-correspondence-management}

AEMでは、管理者は様々なユーザーグループに対して、様々なリソースに対して様々な操作を実行するロールベースのアクセスを提供できます。 例えば、データディクショナリの作成または編集機能は、特定のユーザーグループのユーザーのみが使用でき、他のユーザーはデータディクショナリの表示およびユーザーのみが使用できます。

AEMインターフェイスには、ユーザのアクセスレベルに基づいてアセットタイプの作成や編集などのオプションが表示されます。 例えば、ユーザーにデータディクショナリの作成権限がない場合、データディクショナリの作成オプションはUIに表示されません。

CRXでは、ユーザーアカウントとグループアカウントの両方にアクセス権を設定できますが、この記事はロールまたはユーザーグループベースのアクセス権に関するものです。

グループ、権限、アクセス制御リスト、およびユーザーとグループの管理について詳しくは、[ユーザー管理とセキュリティ](/help/sites-administering/security.md)を参照してください。

## 権限の管理 {#managing-permissions}

1. 権限を管理するユーザーが、関連するユーザーグループに追加されていることを確認します。

   例えば、ユーザーJohn Doeがグループ`agents`と`cm-creditcard`に追加されます。 詳しくは、「ユーザーまたはグループのグループへの追加」を参照してください。 詳細については、[ユーザーとユーザーグループの管理](/help/communities/users.md)を参照してください。

   ![]()

1. 目的の権限を許可するのに適したフォルダーを作成します。

   例えば、企業が住宅ローン、クレジットカード、保険部門を持つ場合、`HomeMortgage`、`CreditCard,`、`Insurance`という名前のフォルダーを作成して、関連資産を保持し、部門に関連する資産のエージェントに対してのみ選択的にアクセスできます。

1. AEM WCM セキュリティにアクセスするには、次のいずれかの操作をおこないます。

   1. ようこそ画面または AEM の様々な場所で、セキュリティアイコンをクリックします。

   1. `https://[server]:[port]/useradmin`に直接移動します。必ず、管理者としてAEMにログインしてください。

      ![]()
   システム内の現在のユーザーとグループがすべて左側のツリーに表示されます。表示する列を選択したり、列の内容を並べ替えたりできます。また、列ヘッダーを新しい位置にドラッグして列の表示順序を変更することもできます。

   タブを使用すると、様々な設定にアクセスできます。

1. 左のツリーリストで、重複を押しながら関連グループの名前をタップし、「権限」タブを選択します。

   グループの名前を検索するには、用意されているスペースにグループの名前を入力します。

1. 「権限」タブで、権限を追加する先のパスに移動します。 Correspondence Managementフォルダーは`content/apps/cm/`フォルダーの下にあります。

   対象のパスに対する権限を追加するメンバーの「メンバー」列のチェックボックスをオンにします。権限を削除するメンバーのチェックボックスはオフにしてください。変更を行ったセルには赤い三角形が表示されます。

   ![useradmin-creditcard](assets/useradmin-creditcard.png)

   >[!NOTE]
   >
   >フォルダーで指定された権限が、そのサブフォルダーで指定された権限よりも優先されます。

1. 「保存」をタップします。
1. ステップテキスト
1. ステップテキスト
1. ステップテキスト

