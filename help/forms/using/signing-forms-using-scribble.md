---
title: 手書き署名を使用したフォームへの電子署名の適用
seo-title: Apply electronic signatures to a form using scribble signatures
description: 手書きでのフォームへの署名
seo-description: Signing forms using scribble
uuid: e807d0de-6d5f-458e-be3e-273ed7a521c0
products: SG_EXPERIENCEMANAGER/6.4/FORMS
topic-tags: author
discoiquuid: 6a806727-28c5-430e-9a83-b43e0e9d9e1c
feature: Adaptive Forms
exl-id: a870c4b7-4040-4bd8-b477-286ebe6a4b01
source-git-commit: f8b19b6723d333e76fed111b9fde376b3bb13a1d
workflow-type: tm+mt
source-wordcount: '498'
ht-degree: 90%

---

# 手書き署名を使用したフォームへの電子署名の適用 {#apply-electronic-signatures-to-a-form-using-scribble-signatures}

**手書き署名**&#x200B;コンポーネントや&#x200B;**署名ステップ**&#x200B;コンポーネントを使用すると、アダプティブフォームに手書きで署名することができます。署名ステップコンポーネントでは、アダプティブフォームの PDF バージョンが表示されます。署名ステップコンポーネントを使用するには、レコードのドキュメントオプションが有効になっているか、フォームテンプレートに基づくアダプティブフォームが必要です。

両方のコンポーネントでは、フォームに署名するために、以下のようなウィンドウが表示されます。また、位置情報アイコン ![aem_6_3_geolocation](assets/aem_6_3_geolocation.png) をクリックすることで、署名に位置情報を追加することもできます。

![手書き署名ダイアログ](assets/scribble-signature.png)

## アダプティブフォームでの手書き署名使用の設定 {#configure-an-adaptive-form-to-use-scribble-signature}

1. レコードのドキュメントオプションが有効になっているか、フォームテンプレートに基づくアダプティブフォームを作成します。詳しい手順については、「[アダプティブフォームの作成](/help/forms/using/creating-adaptive-form.md)」を参照してください。
1. **手書き署名**&#x200B;コンポーネントを、コンポーネントブラウザーからアダプティブフォームにドラッグ＆ドロップします。
1. **設定**（![設定](assets/configure.png)）アイコンをタップします。この操作により、手書き署名コンポーネントのプロパティを表示するプロパティブラウザーが開きます。手書き署名コンポーネントのプロパティを設定します。
1. 署名ステップコンポーネントを、コンポーネントブラウザーからアダプティブフォームにドラッグ＆ドロップします。

   >[!NOTE]
   >
   >署名ステップコンポーネントは、フォームの幅いっぱいに表示されます。そのため、署名ステップコンポーネントが含まれているセクションに他のコンポーネントを配置しないようにすることをお勧めします。

1. コンテンツブラウザーで「**フォームコンテナ**」をタップし、**設定**&#x200B;アイコン（![設定](assets/configure.png)）をタップします。この操作により、アダプティブフォームのコンテナプロパティを表示するプロパティブラウザーが開きます。に移動します。 **アダプティブフォームコンテナ** > **電子署名** を選択し、選択を解除します。 **Acrobat Signを有効にする** オプション。 完了（![aem_6_3_forms_save](assets/aem_6_3_forms_save.png)）アイコンをタップして、変更を保存します。

   >[!NOTE]
   >
   >署名ステップコンポーネントをアダプティブフォームに追加すると、「 Acrobat Signを有効にする」オプションが自動的に選択されます。

1. **設定**（![設定](assets/configure.png)）アイコンをタップします。この操作により、署名ステップのプロパティを表示するプロパティブラウザーが開きます。以下のプロパティを設定します。

   * **要素名**：コンポーネントの名前を指定します。
   * **タイトル：**&#x200B;コンポーネントの一意のタイトルを指定します。
   * **テンプレートメッセージ：**&#x200B;署名 PDF の読み込み中に表示するメッセージを指定します。Acrobat Signサービスでは、署名PDFの準備と読み込みに時間がかかります。
   * **署名サービス：**「**手書き署名**」オプションを選択します。
   * **CSS クラス**：クライアントライブラリの CSS クラスを指定します（存在する場合）。CSS クラスの代わりに[テーマ](/help/forms/using/themes.md)や[インラインスタイル](/help/forms/using/inline-style-adaptive-forms.md)を使用することをお勧めします。

   完了（![aem_6_3_forms_save](assets/aem_6_3_forms_save.png)）アイコンをタップして、変更を保存します。署名が正常に設定されます。

   これで、フォームを記入する際に、PDF バージョンのアダプティブフォームが表示され、PDF ドキュメントの署名オプションが提供されます。詳しくは、「[手書き署名を使用したアダプティブフォームの署名](/help/forms/using/signing-forms-using-scribble.md#p-sign-an-adaptive-form-using-scribble-signature-p)」を参照してください。

## 手書き署名を使用したアダプティブフォームの署名 {#sign-an-adaptive-form-using-scribble-signature}

1. フォームへの記入を完了して署名ステップページに到達すると、署名画面が表示されます。

   ![EchoSign ページの署名画面](assets/esignscribblesign.jpg)

1. 「**[!UICONTROL 署名]**」をクリックします。手書き署名ダイアログが表示されます。フォームに署名し、完了（![aem_6_3_forms_save](assets/aem_6_3_forms_save.png)）アイコンをクリックして、変更内容を保存します。

   ![手書き署名ダイアログ](assets/scribblewidget.jpg)

1. 「完了」をクリックして署名プロセスを完了します。

   ![署名プロセスの完了](assets/scribblecomplete.jpg)

署名がフォームに追加され、フォームコントロールが次のパネルに移動します。
