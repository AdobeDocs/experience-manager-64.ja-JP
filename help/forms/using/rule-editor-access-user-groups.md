---
title: 選択したユーザーグループにルールエディターへのアクセスを許可する
seo-title: 選択したユーザーグループにルールエディターへのアクセスを許可する
description: 選択したユーザーグループにルールエディターへの制限付きアクセスを許可します。
seo-description: 選択したユーザーグループにルールエディターへの制限付きアクセスを許可します。
uuid: 3d982858-b2b5-4370-a9d7-5a95842a7897
content-type: reference
topic-tags: adaptive_forms, develop
products: SG_EXPERIENCEMANAGER/6.4/FORMS
discoiquuid: 6bd58e37-085e-4057-8200-1404d54f41cc
translation-type: tm+mt
source-git-commit: 5734bcd7231f7ba8779acd8e0325b875e252e104
workflow-type: tm+mt
source-wordcount: '334'
ht-degree: 57%

---


# 選択したユーザーグループにルールエディターへのアクセスを許可する {#grant-rule-editor-access-to-select-user-groups}

## 概要 {#overview}

アダプティブフォームで作業を行うユーザーのタイプやスキルは、それぞれ異なっています。正しい知識を使用してスクリプトや複雑なルールを操作できる上級ユーザーもいれば、アダプティブフォームのレイアウトや基本的なプロパティ以外の操作はできない初心者レベルのユーザーもいます。

AEM Forms では、各ユーザーの役割や職務に応じて、ルールエディターへのアクセスを制限することができます。アダプティブForms構成サービスの設定で、ルールエディターの表示とアクセスを可能にする[ユーザーグループ](/help/sites-administering/security.md)を指定できます。

## ルールエディターにアクセスできるユーザーグループの指定 {#specify-user-groups-that-can-access-rule-editor}

1. 管理者として AEM Forms にログインします。
1. オーサーインスタンスで、![adobeexperiencemanager](assets/adobeexperiencemanager.png)Adobe Experience Manager/ツール![ハンマー](assets/hammer.png)/操作/Webコンソールをクリックします。 をクリックします。新しいウィンドウが Web コンソールに表示されます。

   ![1](assets/1.png)

1. Webコンソールウィンドウで、「**[!UICONTROL アダプティブフォームとインタラクティブコミュニケーションWebチャネルの設定]**」を探してクリックします。 **[!UICONTROL Adaptive Form and Interactive Communication Webチャネル]** 設定ダイアログが表示されます。値を変更せずに、「**[!UICONTROL 保存]**」をクリックします。

   これにより、CRX リポジトリに /apps/system/config/com.adobe.aemds.guide.service.impl.AdaptiveFormConfigurationServiceImpl.config ファイルが作成されます。

1. 管理者として CRXDE にログインします。編集のため、/apps/system/config/com.adobe.aemds.guide.service.impl.AdaptiveFormConfigurationServiceImpl.config ファイルを開きます。
1. 次のプロパティを使用して、ルールエディターにアクセスできるグループの名前を指定し（例：RuleEditorsUserGroup）、「**すべて保存**」をクリックします。

   `af.ruleeditor.custom.groups=["RuleEditorsUserGroup"]`

   複数のグループに対するアクセスを有効にするには、カンマ区切り値のリストを指定します。

   `af.ruleeditor.custom.groups=["RuleEditorsUserGroup", "PermittedUserGroup"]`

   ![create-user](assets/create-user.png)

   現在は、指定したユーザーグループ（ここでは「RuleEditorsUserGroup」）に属していないユーザーがフィールドをタップした場合、コンポーネントツールバーでルールの編集アイコン(![edit-rules1](assets/edit-rules1.png))は使用できません。

   ![componentstoolbarwither](assets/componentstoolbarwithre.png)

   ルールエディターのアクセス権を持つユーザーに表示されるコンポーネントツールバー

   ![componentstoolbarwithouter](assets/componentstoolbarwithoutre.png)

   ルールエディターのアクセス権を持たないユーザーに表示されるコンポーネントツールバー

   ユーザーをグループに追加する手順については、[ユーザー管理とセキュリティ](/help/sites-administering/security.md)を参照してください。

