---
title: 選択したユーザーグループにルールエディターへのアクセスを許可する
seo-title: Grant rule editor access to select user groups
description: 選択したユーザーグループに対して、ルールエディターへのアクセス制限を付与します。
seo-description: Grant restricted access to rule editor to select user groups.
uuid: 3d982858-b2b5-4370-a9d7-5a95842a7897
content-type: reference
topic-tags: adaptive_forms, develop
products: SG_EXPERIENCEMANAGER/6.4/FORMS
discoiquuid: 6bd58e37-085e-4057-8200-1404d54f41cc
feature: Adaptive Forms
exl-id: 5e2960f2-b172-48a7-bba3-4561a5f9c7bc
source-git-commit: c5b816d74c6f02f85476d16868844f39b4c47996
workflow-type: tm+mt
source-wordcount: '352'
ht-degree: 70%

---

# 選択したユーザーグループにルールエディターへのアクセスを許可する {#grant-rule-editor-access-to-select-user-groups}

>[!CAUTION]
>
>AEM 6.4 の拡張サポートは終了し、このドキュメントは更新されなくなりました。 詳細は、 [技術サポート期間](https://helpx.adobe.com/jp/support/programs/eol-matrix.html). サポートされているバージョンを見つける [ここ](https://experienceleague.adobe.com/docs/?lang=ja).

## 概要 {#overview}

アダプティブFormsでは、様々なスキルを持つ様々なタイプのユーザーが作業をおこなうことができます。 正しい知識を使用してスクリプトや複雑なルールを操作できる上級ユーザーもいれば、アダプティブフォームのレイアウトや基本的なプロパティ以外の操作はできない初心者レベルのユーザーもいます。

AEM Forms では、各ユーザーの役割や職務に応じて、ルールエディターへのアクセスを制限することができます。アダプティブフォームの設定サービスを使用して、ルールエディターを表示してアクセスできる[ユーザーグループ](/help/sites-administering/security.md)を指定することができます。

## ルールエディターにアクセスできるユーザーグループの指定 {#specify-user-groups-that-can-access-rule-editor}

1. 管理者として AEM Forms にログインします。
1. オーサーインスタンスで、![adobeexperiencemanager](assets/adobeexperiencemanager.png)Adobe Experience Manager／ツール![ハンマー](assets/hammer.png)／操作／Web コンソール をクリックしてください。新しいウィンドウに web コンソールが表示されます。

   ![1](assets/1.png)

1. Web コンソールウィンドウで、**[!UICONTROL アダプティブフォームとインタラクティブ通信の web チャネル設定]**&#x200B;を探してクリックします。**[!UICONTROL アダプティブフォームおよびインタラクティブ通信 web チャネルの設定]**&#x200B;ダイアログが表示されます。値を変更せずに、「**[!UICONTROL 保存]**」をクリックします。

   CRX-repository に/apps/system/config/com.adobe.aemds.guide.service.impl.AdaptiveFormConfigurationServiceImpl.config ファイルが作成されます。

1. 管理者として CRXDE にログインします。/apps/system/config/com.adobe.aemds.guide.service.impl.AdaptiveFormConfigurationServiceImpl.config ファイルを開いて編集します。
1. 次のプロパティを使用して、ルールエディターにアクセスできるグループの名前（例えば RuleEditorsUserGroup）を指定し、「**すべて保存**」をクリックします。

   `af.ruleeditor.custom.groups=["RuleEditorsUserGroup"]`

   複数のグループにアクセスを有効にするには、コンマ区切りの値のリストを指定します。

   `af.ruleeditor.custom.groups=["RuleEditorsUserGroup", "PermittedUserGroup"]`

   ![create-user](assets/create-user.png)

   これで、指定したユーザーグループ（ここでは RuleEditorsUserGroup）に属していないユーザーがフィールドをタップしたときに、ルールを編集アイコン ( ![edit-rules1](assets/edit-rules1.png)) は、コンポーネントツールバーでは使用できません。

   ![componentstoolbarwither](assets/componentstoolbarwithre.png)

   ルールエディターへのアクセス権を持つユーザーに表示されるコンポーネントツールバー

   ![componentstoolbarwithouter](assets/componentstoolbarwithoutre.png)

   ルールエディターへのアクセス権を持たないユーザーに表示されるコンポーネントツールバー

   ユーザーをグループに追加する方法については、[ユーザーの管理とセキュリティ](/help/sites-administering/security.md)を参照してください。
