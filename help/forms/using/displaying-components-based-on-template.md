---
title: 使用するテンプレートに基づいたコンポーネントの表示
seo-title: 使用するテンプレートに基づいたコンポーネントの表示
description: フォームの作成時に、選択したテンプレートに基づいて、サイドバーのコンポーネントを有効にする方法について説明します。
seo-description: フォームの作成時に、選択したテンプレートに基づいて、サイドバーのコンポーネントを有効にする方法について説明します。
uuid: 4e87f400-fb45-413d-9be8-72edbe99f210
contentOwner: sashanka
products: SG_EXPERIENCEMANAGER/6.4/FORMS
topic-tags: customization
content-type: reference
discoiquuid: 940e45b4-dbf1-4207-bd4a-cf677d645fb4
translation-type: tm+mt
source-git-commit: 74d51d46d61b005930f382a33278ae0bea6435e2
workflow-type: tm+mt
source-wordcount: '378'
ht-degree: 65%

---


# 使用するテンプレートに基づいたコンポーネントの表示 {#displaying-components-based-on-the-template-used}

フォーム作成者は、[テンプレート](/help/forms/using/template-editor.md)を使用してアダプティブフォームを作成する際、テンプレートポリシーに基づいて、特定のコンポーネントを表示して使用できます。テンプレートコンテンツポリシーを指定することにより、フォームの作成中にフォーム作成者に表示されるコンポーネントのグループを選択できます。

## テンプレートのコンテンツポリシーの変更 {#changing-the-content-policy-of-a-template}

When you create a template, it is created under `/conf` in the content repository. Based on the folders you have created in the `/conf` directory, path to your template is: `/conf/<your-folder>/settings/wcm/templates/<your-template>`.

次の手順を実行して、テンプレートのコンテンツポリシーに基づいてサイドバーにコンポーネントを表示します。

1. CRXDE Lite を開きます。

   URL: `https://<server>:<port>/crx/de/index.jsp`

1. CRXDE で、テンプレートを作成したフォルダーに移動します。

   例：`/conf/<your-folder>/`

1. In CRXDE, navigate to: `/conf/<your-folder>/settings/wcm/policies/fd/af/layouts/gridFluidLayout/`

   コンポーネントのグループを選択するためには、新しいコンテンツポリシーが必要です。新しいポリシーを作成するには、デフォルトのポリシーをコピーして貼り付け、名前を変更します。

   デフォルトコンテンツポリシーのパス： `/conf/<your-folder>/settings/wcm/policies/fd/af/layouts/gridFluidLayout/default`

   `gridFluidLayout` フォルダーで、デフォルトのポリシーをコピーして貼り付け、名前を変更します。例： `myPolicy`

   ![デフォルトのポリシーをコピー](assets/crx-default1.png)

1. Select the new policy you create, and select the **components** property in the right-side panel with type `string[]`.

   components プロパティを選択して開くと、components を編集ダイアログが表示されます。components を編集ダイアログでは、「**+**」および「**-**」ボタンを使用して、コンポーネントグループを追加または削除できます。作成者が使用するコンポーネントを含むコンポーネントグループを追加できます。

   ![ポリシーのコンポーネントを追加または削除](assets/add-components-list1.png)

   After you add a component group, click **OK** to update the list, and then click **Save All** above CRXDE address bar and refresh.

1. テンプレートで、コンテンツポリシーをデフォルトから、作成した新しいポリシーに変更します。( `myPolicy` in this example.)

   ポリシーを変更するには、CRXDEでに移動し `/conf/<your-folder>/settings/wcm/templates/<your-template>/policies/jcr:content/guideContainer/rootPanel/items`ます。

   In the `cq:policy` property, change `default` to the new policy name ( `myPolicy`).

   ![更新されたテンプレートコンテンツポリシー](assets/updated-policy.png)

   テンプレートを使用して作成したフォームを使用すると、追加したコンポーネントがサイドバーに表示されます。

