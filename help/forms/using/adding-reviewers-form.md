---
title: 送信レビュー担当者のフォームへの関連付け
seo-title: Associating submission reviewers with a form
description: AEM Formsで送信レビュー担当者をフォームに関連付ける方法を説明します。 関連付けられたレビュー担当者は、送信されたフォームをフォームポータル経由でレビューします。
seo-description: Learn how to associate submission reviewers with a form in AEM Forms. Associated reviewers review a form submitted via forms portal.
uuid: 66834c2b-ae70-4a6e-ae8e-07d0e38de06b
products: SG_EXPERIENCEMANAGER/6.4/FORMS
topic-tags: author
discoiquuid: 7c39383b-b430-40a1-9bcb-f5aaccb616ad
feature: Adaptive Forms
exl-id: b45d844e-acf9-4da2-b54e-08c67aa183a3
source-git-commit: c5b816d74c6f02f85476d16868844f39b4c47996
workflow-type: tm+mt
source-wordcount: '529'
ht-degree: 73%

---

# 送信レビュー担当者とフォームの関連付け  {#associating-submission-reviewers-with-a-form}

>[!CAUTION]
>
>AEM 6.4 の拡張サポートは終了し、このドキュメントは更新されなくなりました。 詳細は、 [技術サポート期間](https://helpx.adobe.com/jp/support/programs/eol-matrix.html). サポートされているバージョンを見つける [ここ](https://experienceleague.adobe.com/docs/?lang=ja).

フォーム作成時に、フォームポータル経由で送信されたフォームのレビューおよびフィードバックを行うユーザーを指定できます。組織はフィードバックを収集し、送信済みフォームに対して再作業を行うことができます。

AEM Forms では、レビュー担当者グループをフォームに関連付けることができます。フォームのレビューグループに追加されたユーザーは、フォームの送信を確認し、フィードバックを提供します。

フォームに割り当てられたレビュー担当者グループは指定されたフォームのみをレビューできます。

## 前提条件 {#prerequisite}

### メタデータスキーマエディターを使用してアダプティブフォームの送信レビュー担当者グループプロパティを有効にする {#enabling-submission-reviewer-groups-property-for-adaptive-forms-using-metadata-schema-editor}

レビュー担当者グループをフォームに関連付けるには、アダプティブフォームのメタデータスキーマを編集します。 デフォルトでは、送信されたフォームにレビュー担当者グループを追加できません。

メタデータスキーマを編集するには、以下の手順に従います。

1. オーサーモードで、Experience Manager の **[!UICONTROL ツール／アセット／メタデータスキーマ]** をクリックします。
1. スキーマFormsページで、に移動します。 **[!UICONTROL Forms / Forms AEMで作成]**.

   ページの URL は次のようになります。

   ```
   https://<hostname>:<port>/mnt/overlay/dam/gui/content/metadataschemaeditor/
    schemalist.html/dam/content/schemaeditors/forms/forms/
    aem-authored
   ```

1. 「**[!UICONTROL アダプティブフォーム]**」を選択し、「**[!UICONTROL 編集]**」をクリックします。
1. 「フォームの編集」ページで、「**[!UICONTROL 詳細]**」をクリックします。
1. 「詳細」タブで、ビルドフォームで使用可能な「**[!UICONTROL 1 行テキスト]**」コンポーネントをドラッグ＆ドロップします。
1. 追加されたテキストコンポーネントを選択し、その設定を確認します。

   「設定」の下の「プロパティにマップ」フィールドに `./jcr:content/metadata/form-submission-reviewer-group` と入力します。

   アダプティブフォームの詳細属性の送信レビュー担当者グループフィールドが、フィールドラベルで指定した名前で有効化されます。

## 送信レビュー担当者のフォームへの関連付け {#associating-submission-reviewers-with-a-form-1}

送信レビュー担当者をアダプティブフォームに関連付けるには、レビュー担当者グループを作成し、そのグループにユーザーを追加します。 フォームの詳細属性内のフォーム送信レビュー担当者のフィールドに、作成したレビュー担当者グループを追加します。\
ユーザーグループを使用することで、アダプティブフォームごとに異なる送信レビュー担当者のグループを関連付けることができます。この機能によって、権限のないユーザーによる送信レビューを避けることができます。

以下の手順を行う前に、「[必要条件](/help/forms/using/adding-reviewers-form.md#prerequisite)」を参照してください。

グループを作成し、メンバーを追加するには、**[!UICONTROL ツール／操作／セキュリティ／グループ]**&#x200B;に移動します。\
詳しくは、「[ユーザー管理およびサービス](/help/sites-administering/security.md)」を参照してください。\
作成したグループが、あらかじめ用意されているユーザーグループ **forms-submission-reviewers** のメンバーとして追加されていることを確認してください。このユーザーグループは、AEM Forms に付属しており、ユーザーは送信レビュー担当者として確実に追加されます。

ユーザーグループをアダプティブフォームに関連付けるには、次の手順を実行します。

1. 作成者モードで、**[!UICONTROL フォーム／フォームとドキュメント]**&#x200B;に移動します。
1. 以下を使用： **[!UICONTROL 選択]** アダプティブフォームを選択するオプションを選択し、 **[!UICONTROL プロパティを表示]**.
1. フォームのプロパティウィンドウで「**[!UICONTROL 編集]**」をクリックし、「**[!UICONTROL 詳細]**」をクリックします。
1. 送信レビュー担当者グループのフィールドにグループを入力し、「**[!UICONTROL 完了]**」をクリックします。

   送信レビュー担当者グループのフィールドには、アダプティブフォームのメタデータスキーマの編集で指定した名前が表示されます。

>[!NOTE]
>
>AEM Formsのリモート実装でユーザーとフォームを確実に使用できるように、ユーザーとフォームを複製します。
>
>リモートで、すべてのユーザーがレビュー担当のメンバーとして複製されていることを確認してください。
