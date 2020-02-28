---
title: Correspondence Managementでロールベースのユーザーインターフェイスを公開しない
seo-title: Correspondence Managementでロールベースのユーザーインターフェイスを公開しない
description: 'null'
seo-description: 'null'
page-status-flag: de-activated
uuid: 60808852-f63f-4c0a-badb-b0af93c995a8
contentOwner: gtalwar
products: SG_EXPERIENCEMANAGER/6.3/FORMS
discoiquuid: 342f111e-f15a-4f9a-8993-f90760363c02
translation-type: tm+mt
source-git-commit: cdec5b3c57ce1c80c0ed6b5cb7650b52cf9bc340

---


# Correspondence Managementでロールベースのユーザーインターフェイスを公開しない {#do-not-publish-role-based-user-interface-in-correspondence-management}

AEMでは、管理者は、様々なリソースに対して様々なアクションを実行する様々なユーザーグループに対して、ロールベースのアクセスを提供できます。 例えば、データディクショナリの作成または編集の機能は特定のユーザーグループのユーザーのみが使用でき、他のユーザーはデータディクショナリの表示とユーザーのみが使用できます。

AEMインターフェイスには、ユーザーのアクセスレベルに基づいて、アセットタイプの作成や編集などのオプションが表示されます。 例えば、ユーザーにデータディクショナリの作成権限がない場合、データディクショナリの作成オプションはUIに表示されません。

CRXでは、ユーザーアカウントとグループアカウントの両方に対してアクセス権を設定できますが、この記事はロールまたはユーザーグループベースのアクセス権に関するものです。

グループ、権限、アクセス制御リスト、およびユーザーとグループの管理の詳細については、「ユーザー管理とセキュリ [ティ」を参照してください](/help/sites-administering/security.md)。

## 権限の管理 {#managing-permissions}

1. 権限を管理するユーザーが、関連するユーザーグループに追加されていることを確認します。

   例えば、ユーザーJohn Doeがグループおよびに追加され `agents` ます `cm-creditcard`。 詳しくは、「グループへのユーザーまたはグループの追加」を参照してください。 For more information, see [Managing Users and User Groups](/help/communities/users.md).

   ![]()

1. 目的の権限を許可するのに適したフォルダーを作成します。

   例えば、企業に住宅ローン、クレジットカード、保険部門がある場合は、名前を付けたフォルダを作成し、関連する資産を保持し、部門に関連する資産の代理店に対してのみアクセスを選択できます。 `HomeMortgage``CreditCard,``Insurance`

1. AEM WCM セキュリティにアクセスするには、次のいずれかの操作をおこないます。

   1. ようこそ画面または AEM の様々な場所で、セキュリティアイコンをクリックします。

   1. Navigate directly to `https://[server]:[port]/useradmin`. Be sure you log into AEM as an administrator.

      ![]()
   システム内の現在のユーザーとグループがすべて左側のツリーに表示されます。表示する列を選択したり、列の内容を並べ替えたりできます。また、列ヘッダーを新しい位置にドラッグして列の表示順序を変更することもできます。

   タブを使用すると、様々な設定にアクセスできます。

1. 左のツリーリストで、関連するグループの名前をダブルタップし、「権限」タブを選択します。

   グループの名前を検索するには、用意されているスペースにグループの名前を入力します。

1. 「権限」タブで、権限を追加するパスに移動します。 Correspondence Managementフォルダーはフォルダーの下にあ `content/apps/cm/` ります。

   対象のパスに対する権限を追加するメンバーの「メンバー」列のチェックボックスをオンにします。権限を削除するメンバーのチェックボックスはオフにしてください。変更を行ったセルには赤い三角形が表示されます。

   ![useradmin-creditcard](assets/useradmin-creditcard.png)

   >[!NOTE]
   >
   >フォルダーで指定された権限は、そのサブフォルダーで指定された権限より優先されます。

1. 「保存」をタップします。
1. ステップテキスト
1. ステップテキスト
1. ステップテキスト

