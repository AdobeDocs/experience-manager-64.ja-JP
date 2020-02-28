---
title: フォームへの送信レビュー担当者の関連付け
seo-title: フォームへの送信レビュー担当者の関連付け
description: AEM Forms のフォームへ送信レビュー担当者を関連付ける方法を説明します。関連付けられたレビュー担当者は、送信されたフォームをフォームポータル経由でレビューします。
seo-description: AEM Forms のフォームへ送信レビュー担当者を関連付ける方法を説明します。関連付けられたレビュー担当者は、送信されたフォームをフォームポータル経由でレビューします。
uuid: 66834c2b-ae70-4a6e-ae8e-07d0e38de06b
products: SG_EXPERIENCEMANAGER/6.4/FORMS
topic-tags: author
discoiquuid: 7c39383b-b430-40a1-9bcb-f5aaccb616ad
translation-type: tm+mt
source-git-commit: e2bb2f17035e16864b1dc54f5768a99429a3dd9f

---


# フォームへの送信レビュー担当者の関連付け  {#associating-submission-reviewers-with-a-form}

フォーム作成時に、フォームポータル経由で送信されたフォームのレビューおよびフィードバックを行うユーザーを指定することができます。組織はフィードバックを収集し、送信済みフォームに対して再作業を行うことができます。

AEM Forms では、レビュー担当者グループをフォームへ関連付けることができます。フォームのレビューグループに追加されたユーザーは、このフォームの送信を確認し、フィードバックを提供します。

フォームに割り当てられたレビュー担当者グループは指定されたフォームのみをレビューできます。

## 前提条件 {#prerequisite}

### メタデータスキーマエディターを使用してアダプティブフォームで送信レビュー担当者グループのプロパティを有効化 {#enabling-submission-reviewer-groups-property-for-adaptive-forms-using-metadata-schema-editor}

レビュー担当者グループをフォームに関連付けるには、アダプティブフォームのメタデータスキーマを編集します。デフォルトでは、送信されたフォームにレビュー担当者グループを追加することはできません。

メタデータスキーマを編集するには、次の手順に従います。

1. 作成者モードを使用して、Experience Manager の「**[!UICONTROL ツール／アセット／メタデータスキーマ]**」をクリックします。
1. In the Schema Forms page, navigate to **[!UICONTROL Forms > Forms Authored in AEM]**.

   ページのURLは次のとおりです。

   ```
   https://<hostname>:<port>/mnt/overlay/dam/gui/content/metadataschemaeditor/
    schemalist.html/dam/content/schemaeditors/forms/forms/
    aem-authored
   ```

1. Select **[!UICONTROL Adaptive Form]** and click **[!UICONTROL Edit]**.
1. 「フォームの編集」ページで、「**[!UICONTROL 詳細]**」をクリックします。
1. In the Advanced tab, drag-and-drop the **[!UICONTROL Single Line Text]** component available under Build Form.
1. 追加されたテキストコンポーネントを選択し、その設定を確認します。

   「設定」で、「プロパティ `./jcr:content/metadata/form-submission-reviewer-group` にマップ」フィールドにと入力します。

   アダプティブフォームの詳細属性の送信レビュー担当者グループフィールドが、フィールドラベルで指定した名前で有効化されます。

## フォームへの送信レビュー担当者の関連付け {#associating-submission-reviewers-with-a-form-1}

アダプティブフォームに送信レビュー担当者を関連付けるには、レビュー担当者グループを作成し、そこにユーザーを追加します。フォームの詳細属性内のフォーム送信レビュー担当者のフィールドに、作成したレビュー担当者グループを追加します。\
ユーザーグループを使用することで、アダプティブフォームごとに異なる送信レビュー担当者のグループを関連付けることができます。この機能は、権限のないユーザーによる送信レビューを防止します。

以下の手順を行う前に、「[必要条件](/help/forms/using/adding-reviewers-form.md#prerequisite)」を参照してください。

To create a group and add members to it, navigate to **[!UICONTROL Tools > Operations > Security > Groups]**.\
For more information, see [User Administration and Services](/help/sites-administering/security.md).\
Ensure that you add the group you create as a member of the out-of-the-box user group: **forms-submission-reviewers**. このユーザーグループはAEM Formsに付属し、送信レビュー担当者として追加されます。

アダプティブフォームにユーザーグループを関連付けるには、次の手順に従います。

1. 作成者モードで、「**[!UICONTROL フォーム／フォームとドキュメント]**」に移動します。
1. Use the **[!UICONTROL Select]** option to select an adaptive form, and click **[!UICONTROL View Properties]**.
1. In the Properties window of the form, click **[!UICONTROL Edit]**, and then click **[!UICONTROL ADVANCED]**.
1. Enter the group in the submission reviewer group field, and click **[!UICONTROL Done]**.

   送信レビュー担当者グループのフィールドには、アダプティブフォームのメタデータスキーマの編集で指定した名前が表示されます。

>[!NOTE]
>
>リモートでの AEM Forms の導入においてユーザーとフォームの可用性を確認するには、ユーザーとフォームを複製してください。
>
>リモートで、すべてのユーザーがレビュー担当のメンバーとして複製されていることを確認してください。

