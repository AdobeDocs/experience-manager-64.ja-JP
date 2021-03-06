---
title: フォームポータルコンポーネントの有効化
seo-title: Enabling forms portal components
description: デフォルトでは、フォームポータルコンポーネントは無効になっています。フォームポータルコンポーネントを有効にするには、Document Services と Document Services Predicates グループを有効にします。
seo-description: Out of the box, Forms Portal components are disabled. Enable Document Services and Document Services Predicates groups to enable Forms Portal components.
uuid: 92d25da6-f1df-4ac0-bf84-2edf9e2722b3
content-type: reference
products: SG_EXPERIENCEMANAGER/6.4/FORMS
topic-tags: publish
discoiquuid: 4d318908-c724-4582-a82b-6e9b1c55705b
feature: Forms Portal
exl-id: 01c5eb6b-b097-4354-84b2-8bee7b7626f2
source-git-commit: 251000ec9a67e5175c708d558c3c71a2061a1c9e
workflow-type: tm+mt
source-wordcount: '320'
ht-degree: 100%

---

# フォームポータルコンポーネントの有効化 {#enabling-forms-portal-components}

デフォルトでは、フォームポータルコンポーネントは使用できません。AEM サイドキックで使用可能なコンポーネントのリストにコンポーネントを表示するには、次の手順を実行します。

1. Web サイトのオーサーインスタンスにログインし、AEM Sites ページを開きます。

1. 静的テンプレートを使用するページでは、次の手順を実行します。

   1. ページのヘッダーで、![canvas-drop-down](assets/canvas-drop-down.png)>**Design** をタップすると、デザインモードでページが表示されます。
   1. 任意の（青色の境界線の付いている）コンポーネントをタップしてから「![フィールドレベル](assets/field-level.png)」をタップし、現在のコンポーネントが含まれている段落システムを選択します。
   1. 段落システムで「![settings_icon](assets/settings_icon.png)」をタップして段落システムの編集ダイアログを開きます。
   1. **[!UICONTROL 許可されたコンポーネント]**&#x200B;のリストから、**[!UICONTROL Document Services]** コンポーネントと **[!UICONTROL Document Services Predicates]** コンポーネントのチェックボックスをオンにします。「**[!UICONTROL OK]**」をタップします。

1. 動的テンプレートを使用するページでは、次の手順を実行します。

   1. ページのヘッダーで、「![プロパティ](assets/properties.png)>**テンプレートの編集**」の順にタップしてページのテンプレートを開きます。
   1. 「**レイアウトコンテナ**」と「![FeedManagement](assets/FeedManagement.png)」をタップします。「**許可されたコンポーネント**」タブで「**Document Services」オプションと「Document Service Predicates**」オプションを有効にして「![aem_6_3_forms_save](assets/aem_6_3_forms_save.png)」をタップします。

>[!NOTE]
>
>また、コンポーネントを選択して、これらのカテゴリから特定のコンポーネントを有効にすることもできます。コンポーネントとその使用方法について詳しくは、「[フォームポータルページの作成](/help/forms/using/creating-form-portal-page.md)」と「[ページでのリンクコンポーネントの埋め込み](/help/forms/using/embedding-link-component-page.md)」を参照してください。

これで、コンポーネントブラウザーで Document Services コンポーネントカテゴリと Document Services Predicates コンポーネントカテゴリを使用できるようになります。コンポーネントは、同じテンプレートを使用するすべてのページで有効になります。

## 関連記事

* [フォームポータルコンポーネントの有効化](/help/forms/using/enabling-forms-portal-components.md)
* [フォームポータルページの作成](/help/forms/using/creating-form-portal-page.md)
* [API を使用した Web ページ上のフォームの一覧表示](/help/forms/using/listing-forms-webpage-using-apis.md)
* [ドラフトと送信コンポーネントの使用](/help/forms/using/draft-submission-component.md)
* [ドラフトと送信済みフォームのストレージのカスタマイズ](/help/forms/using/draft-submission-component.md)
* [ドラフトと送信コンポーネントとデータベースの統合のサンプル](/help/forms/using/integrate-draft-submission-database.md)
* [フォームポータルコンポーネントのテンプレートをカスタマイズする](/help/forms/using/customizing-templates-forms-portal-components.md)
* [ポータル上のフォーム発行の概要](/help/forms/using/introduction-publishing-forms.md)
