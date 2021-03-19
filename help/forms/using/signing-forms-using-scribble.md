---
title: 手書き署名を使用したフォームへの電子署名の適用
seo-title: 手書き署名を使用したフォームへの電子署名の適用
description: 手書きでのフォームへの署名
seo-description: 手書きでのフォームへの署名
uuid: e807d0de-6d5f-458e-be3e-273ed7a521c0
products: SG_EXPERIENCEMANAGER/6.4/FORMS
topic-tags: author
discoiquuid: 6a806727-28c5-430e-9a83-b43e0e9d9e1c
feature: アダプティブフォーム
translation-type: tm+mt
source-git-commit: 75312539136bb53cf1db1de03fc0f9a1dca49791
workflow-type: tm+mt
source-wordcount: '513'
ht-degree: 71%

---


# 手書き署名を使用したフォームへの電子署名の適用 {#apply-electronic-signatures-to-a-form-using-scribble-signatures}

**手書き署名**&#x200B;コンポーネントや&#x200B;**署名ステップ**&#x200B;コンポーネントを使用すると、アダプティブフォームに手書きで署名することができます。署名ステップコンポーネントでは、アダプティブフォームのPDF バージョンが表示されます。「レコードのドキュメント」オプションを有効にするか、フォームテンプレートベースのアダプティブフォームで、署名手順コンポーネントを使用する必要があります。

両方のコンポーネントでは、フォームに署名するために、下記のようなウィンドウが表示されます。位置情報アイコン![aem_6_3_geolocation](assets/aem_6_3_geolocation.png)をクリックして、署名に位置情報を追加することもできます。

![手書き署名ダイアログ](assets/scribble-signature.png)

## アダプティブフォームでの手書き署名使用の設定 {#configure-an-adaptive-form-to-use-scribble-signature}

1. レコードのドキュメントオプションが有効になっている、またはフォームテンプレートベースのアダプティブフォームを作成します。詳細な手順については、「[アダプティブフォームの作成](/help/forms/using/creating-adaptive-form.md)」を参照してください。
1. コンポーネントブラウザーからアダプティブフォームに&#x200B;**手書き署名**&#x200B;コンポーネントをドラッグ&amp;ドロップします。
1. **設定** ![設定](assets/configure.png)アイコンをタップします。 この操作により、手書き署名コンポーネントのプロパティを表示するプロパティブラウザーが開きます。手書き署名コンポーネントのプロパティを設定します。
1. 「署名手順」コンポーネントをコンポーネントブラウザーからアダプティブフォームにドラッグ&amp;ドロップします。

   >[!NOTE]
   >
   >署名ステップコンポーネントは、フォームの幅いっぱいに表示されます。そのため、署名ステップコンポーネントが含まれているセクションに他のコンポーネントを配置しないようにすることをお勧めします。

1. コンテンツブラウザーで、**フォームコンテナ**&#x200B;をタップし、**設定** ![設定](assets/configure.png)アイコンをタップします。 この操作により、アダプティブフォームのコンテナプロパティを表示するプロパティブラウザーが開きます。**アダプティブフォームコンテナ**／**電子署名**&#x200B;に移動して、「**Adobe Sign を有効にする**」オプションを選択解除します。![aem_6_3_forms_save](assets/aem_6_3_forms_save.png)を完了アイコンをタップして、変更を保存します。

   >[!NOTE]
   >
   >署名ステップコンポーネントをアダプティブフォームに追加すると、「Adobe Sign を有効にする」オプションが自動的に選択されます。

1. **設定** ![設定](assets/configure.png)アイコンをタップします。 この操作により、署名ステップのプロパティを表示するプロパティブラウザーが開きます。以下のプロパティを設定します。

   * **要素名：**&#x200B;コンポーネントの名前を指定します。
   * **タイトル：**&#x200B;コンポーネントの一意のタイトルを指定します。
   * **テンプレートメッセージ：**&#x200B;署名 PDF の読み込み中に表示するメッセージを指定します。Adobe Sign サービスによる署名 PDF の準備と読み込みには、ある程度の時間がかかります。
   * **署名サービス：** 「**手書き署名**」オプションを選択します。
   * **CSS クラス**：クライアントライブラリの CSS クラスを指定します（存在する場合）。CSS クラスの代わりに[テーマ](/help/forms/using/themes.md)や[インラインスタイル](/help/forms/using/inline-style-adaptive-forms.md)を使用することをお勧めします。

   ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png)を完了アイコンをタップして、変更を保存します。 署名が正常に設定されました。

   これで、フォームを記入する際に、PDF バージョンのアダプティブフォームが表示され、PDF ドキュメントの署名オプションが提供されます。詳しくは、「[手書き署名を使用したアダプティブフォームへの署名](/help/forms/using/signing-forms-using-scribble.md#p-sign-an-adaptive-form-using-scribble-signature-p)」を参照してください。

## 手書き署名を使用したアダプティブフォームの署名 {#sign-an-adaptive-form-using-scribble-signature}

1. フォームへの記入を完了して署名ステップページに到達すると、署名画面が表示されます。

   ![EchoSign ページの署名画面](assets/esignscribblesign.jpg)

1. 「**[!UICONTROL 署名]**」をクリックします。手書き署名ダイアログが表示されます。フォームに署名し、完了![aem_6_3_forms_save](assets/aem_6_3_forms_save.png)アイコンをクリックして署名を保存します。

   ![手書き署名ダイアログ](assets/scribblewidget.jpg)

1. 「完了」をクリックして署名プロセスを完了します。

   ![署名プロセスの完了](assets/scribblecomplete.jpg)

署名がフォームに追加され、フォームコントロールが次のパネルに移動します。

