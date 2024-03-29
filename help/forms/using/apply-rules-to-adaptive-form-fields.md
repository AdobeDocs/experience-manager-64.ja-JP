---
title: 「公開しないチュートリアル：アダプティブフォームフィールドにルールを適用する»
seo-title: Apply rules to adaptive form fields
description: このチュートリアルでは、ルールを作成して、インタラクティブ機能、ビジネスロジックおよびスマート検証機能をアダプティブフォームに追加する方法について説明します。
seo-description: Create rules to add interactivity, business logic, and smart validations to an adaptive form.
page-status-flag: de-activated
uuid: 60f142aa-81ca-4333-8614-85a01e23e917
products: SG_EXPERIENCEMANAGER/6.3/FORMS
discoiquuid: 982eddba-2350-40e7-8a42-db02d28cf133
feature: Adaptive Forms
exl-id: bb65b6d7-5bbf-4cc5-a468-9ea8465f7a07
source-git-commit: c5b816d74c6f02f85476d16868844f39b4c47996
workflow-type: tm+mt
source-wordcount: '1168'
ht-degree: 52%

---

# チュートリアル：アダプティブフォームフィールドへのルールの適用 {#tutorial-apply-rules-to-adaptive-form-fields}

>[!CAUTION]
>
>AEM 6.4 の拡張サポートは終了し、このドキュメントは更新されなくなりました。 詳細は、 [技術サポート期間](https://helpx.adobe.com/jp/support/programs/eol-matrix.html). サポートされているバージョンを見つける [ここ](https://experienceleague.adobe.com/docs/?lang=ja).

![06-apply-rules-to-adaptive-form_main](assets/06-apply-rules-to-adaptive-form_main.png)

このチュートリアルは、 [最初のアダプティブフォームを作成する](/help/forms/using/create-your-first-adaptive-form.md) 系列。 Adobeは、チュートリアルの使用例を理解し、実行し、実際に使用するために、一連の作業を時系列に従うことをお勧めします。

## このチュートリアルについて {#about-the-tutorial}

ルールを使用して、アダプティブフォームにインタラクティビティ、ビジネスロジック、スマート検証を追加できます。 アダプティブフォームには、ルールエディターが組み込まれています。 ルールエディターには、ガイド付きツアーと同様のドラッグ&amp;ドロップ機能が用意されています。 ドラッグ&amp;ドロップによる方法は、ルールを作成する最も速く最も簡単な方法です。 また、ルールエディターには、コーディングスキルのテストやルールの次のレベルへの移行に関心のあるユーザー向けのコードウィンドウも用意されています。

ルールエディターについて詳しくは、 [アダプティブFormsルールエディター](/help/forms/using/rule-editor.md).

このチュートリアルを終了すると、ルールを作成して以下の操作を実行できるようになります。

* フォームデータモデルサービスを呼び出してデータベースからデータを取得する
* フォームデータモデルサービスを呼び出してデータベースにデータを追加する
* 検証チェック処理を実行して、エラーメッセージを表示する

このチュートリアルの各セクションの最後にあるインタラクティブな GIF 画像で、作成するフォームの機能をその場で確認することができます。

## 手順 1:データベースから顧客レコードを取得する {#retrieve-customer-record}

フォームデータモデルを作成するには、次の手順に従います。 [フォームデータモデルを作成](/help/forms/using/create-form-data-model.md) 記事。 これで、ルールエディターを使用してForms Data Model サービスを呼び出し、情報を取得してデータベースに追加できます。

すべての顧客に一意の顧客 ID 番号が割り当てられ、データベース内の関連する顧客データを識別するのに役立ちます。 以下の手順では、顧客 ID を使用してデータベースから情報を取得します。

1. アダプティブフォームを編集用に開きます。

   [http://localhost:4502/editor.html/content/forms/af/change-billing-shipping-address.html](http://localhost:4502/editor.html/content/forms/af/change-billing-shipping-address.html)

1. 「**[!UICONTROL 顧客 ID]**」フィールドをタップし、「**[!UICONTROL ルールを編集]**」アイコンをタップします。ルールエディターウィンドウが表示されます。
1. 次をタップします。 **[!UICONTROL +作成]** アイコンをクリックして、ルールを追加します。 Visual Editor が開きます。

   ビジュアルエディターでは、「**[!UICONTROL 条件]**」ステートメントがデフォルトで選択されています。また、ルールエディターの起動元となったフォームオブジェクト（この場合は「**[!UICONTROL 顧客 ID]**」）が、「**[!UICONTROL 条件]**」ステートメントで指定されています。

1. 「**[!UICONTROL 状態の選択]**」ドロップダウンをタップして「**[!UICONTROL 変更済み]**」を選択します。

   ![whencustomeridischanged](assets/whencustomeridischanged.png)

1. 内 **[!UICONTROL THEN]** 文、選択 **[!UICONTROL サービスを起動]** から **[!UICONTROL アクションを選択]** 」ドロップダウンリストから選択できます。
1. を選択します。 **[!UICONTROL 配送先住所の取得]** サービス **[!UICONTROL 選択]** 」ドロップダウンリストから選択できます。
1. 「フォームオブジェクト」タブの「**[!UICONTROL 顧客 ID]**」フィールドをドラッグし、「**[!UICONTROL 入力]**」ボックスの「**[!UICONTROL オブジェクトをドロップまたは次から選択]**」フィールドにドロップします。

   ![dropobjectstoinputfield-retrievedata](assets/dropobjectstoinputfield-retrievedata.png)

1. 「フォームオブジェクト」タブの各フィールド（**[!UICONTROL 顧客 ID、名前、発送先住所、都道府県、郵便番号]**）をドラッグし、「**[!UICONTROL 出力]**」ボックスの「**[!UICONTROL オブジェクトをドロップまたは次から選択]**」フィールドにドロップします。

   ![dropobjectstooutputfield-retrievedata](assets/dropobjectstooutputfield-retrievedata.png)

   「**[!UICONTROL 完了]**」をクリックして、ルールを保存します。ルールエディターウィンドウで「**[!UICONTROL 閉じる]**」をタップします。

1. アダプティブフォームのプレビューを表示します。ID を **[!UICONTROL 顧客 ID]** フィールドに入力します。 これで、フォームは、データベースから顧客の詳細を取得できるようになります。

   ![retrieve-information](assets/retrieve-information.gif)

## 手順 2:更新した顧客アドレスをデータベースに追加 {#updated-customer-address}

顧客の詳細がデータベースから取得されたら、配送先住所、都道府県、郵便番号を更新できます。 以下の手順では、フォームデータモデルサービスを呼び出して、顧客情報をデータベースに更新します。

1. 「**[!UICONTROL 送信]**」フィールドを選択して「**[!UICONTROL ルールを編集]**」アイコンをタップします。ルールエディターウィンドウが表示されます。
1. **[!UICONTROL 送信]** - クリックルールを選択して「**[!UICONTROL 編集]**」アイコンをタップします。送信ルールを編集するためのオプションが表示されます。

   ![submit-rule](assets/submit-rule.png)

   「条件」オプションの「**[!UICONTROL 送信]**」オプションと「**[!UICONTROL クリックされた]**」オプションが既に選択されています。

   ![submit-is-clicked](assets/submit-is-clicked.png)

1. 内 **[!UICONTROL THEN]** オプションを選択し、 **[!UICONTROL +ステートメントを追加]** オプション。 選択 **[!UICONTROL サービスを起動]** から **[!UICONTROL アクションを選択]** 」ドロップダウンリストから選択できます。
1. を選択します。 **[!UICONTROL 配送先住所の更新]** サービス **[!UICONTROL 選択]** 」ドロップダウンリストから選択できます。

   ![update-shipping-address](assets/update-shipping-address.png)

1. ![dropobjectstoinputfield-updatedata](assets/dropobjectstoinputfield-updatedata.png)

   「フォームオブジェクト」タブの各フィールド（**[!UICONTROL 発送先住所、都道府県、郵便番号]**）をドラッグして、「**[!UICONTROL 入力]**」ボックスの「**[!UICONTROL オブジェクトをドロップまたは次から選択]**」フィールドの対応する [テーブル名].[プロパティ]（例：customerdetails.shippingAddress）にドロップします。先頭にテーブル名（このユースケースでは customerdetails）が付いたすべてのフィールドは、更新サービスの入力データとして機能します。 これらのフィールドで指定された値は、すべてデータソース内で更新されます。

   >[!NOTE]
   >
   >「**[!UICONTROL 名前]**」フィールドと「**[!UICONTROL 顧客 ID]**」フィールドは、対応する [テーブル名].[プロパティ] 形式のフィールド（例：customerdetails.name）にドラッグ＆ドロップしないでください。顧客名と顧客 ID が誤って変更されるのを避けるためです。

1. 「フォームオブジェクト」タブの「**[!UICONTROL 顧客 ID]**」フィールドをドラッグし、「**[!UICONTROL 入力]**」ボックスの「ID」フィールドにドロップします。先頭にテーブル名（このユースケースでは customerdetails）が付いていないフィールドは、更新サービスの検索パラメーターとして機能します。 このユースケースでは、「**[!UICONTROL ID]**」フィールドにより、顧客詳細テーブルのレコードを一意に特定することができます。
1. 「**[!UICONTROL 完了]**」をクリックして、ルールを保存します。ルールエディターウィンドウで「**[!UICONTROL 閉じる]**」をタップします。
1. アダプティブフォームのプレビューを表示します。顧客の詳細を取得し、配送先住所を更新して、フォームを送信します。 同じ顧客の詳細を再度取得すると、更新された配送先住所が表示されます。

## 手順 3:（ボーナスセクション）コードエディターを使用して、検証を実行し、エラーメッセージを表示します。 {#step-bonus-section-use-the-code-editor-to-run-validations-and-display-error-messages}

フォームの検証を実行して、フォームに入力されたデータが正しいことと、データが正しくない場合はエラーメッセージが表示されることを確認する必要があります。 例えば、存在しない顧客 ID をフォームに入力すると、エラーメッセージが表示されます。

アダプティブフォームには、電子メールフィールドや数値フィールドなど、検証機能が組み込まれたコンポーネントがいくつか用意されています。これらは一般的な使用例で使用できます。 高度なユースケース（データベースからレコードが 1 件も返されなかった場合にエラーメッセージを表示するなど）の場合は、ルールエディターを使用します。

次の手順では、データベース内に存在しない顧客 ID がフォームに入力された場合にエラーメッセージを表示するためのルールを作成する方法を示します。このルールによってフォーカスが「顧客 ID」フィールドに移動し、このフィールドがリセットされます。このルールでは、データモデルサービスの [dataIntegrationUtils API](/help/forms/using/invoke-form-data-model-services.md) を使用して、フォームに入力された顧客 ID がデータベース内に存在するかどうかが確認されます。

1. 「**[!UICONTROL 顧客 ID]**」フィールドをタップし、`Edit Rules` アイコンをタップします。ルールエディターウィンドウが表示されます。
1. 次をタップします。 **[!UICONTROL +作成]** アイコンをクリックして、ルールを追加します。 Visual Editor が開きます。

   ビジュアルエディターでは、「**[!UICONTROL 条件]**」ステートメントがデフォルトで選択されています。また、ルールエディターの起動元となったフォームオブジェクト（この場合は「**[!UICONTROL 顧客 ID]**」）が、「**[!UICONTROL 条件]**」ステートメントで指定されています。

1. 「**[!UICONTROL 状態の選択]**」ドロップダウンをタップして「**[!UICONTROL 変更済み]**」を選択します。

   ![whencustomeridischanged](assets/whencustomeridischanged.png)

   内 **[!UICONTROL THEN]** 文、選択 **[!UICONTROL サービスを起動]** から **[!UICONTROL アクションを選択]** 」ドロップダウンリストから選択できます。

1. 切り替え元 **[!UICONTROL Visual Editor]** から **[!UICONTROL コードエディター]**. スイッチコントロールは、ウィンドウの右側にあります。 コードエディターが開き、次のようなコードが表示されます。

   ![code-editor](assets/code-editor.png)

1. 「入力変数」セクションのコードを以下のように置換します。

   ```
   var inputs = {
       "id" : this
   };
   ```

1. guidelib.dataIntegrationUtils.executeOperation (operationInfo, inputs, outputs) セクションを次のコードに置き換えます。

   ```
   guidelib.dataIntegrationUtils.executeOperation(operationInfo, inputs, outputs, function (result) {
     if (result) {
         result = JSON.parse(result);
       customer_Name.value = result.name;
       customer_Shipping_Address = result.shippingAddress;
     } else {
       if(window.confirm("Invalid Customer ID. Provide a valid customer ID")) {
             customer_Name.value = " ";
            guideBridge.setFocus(customer_ID);
       }
     }
   });
   ```

1. アダプティブフォームのプレビューを表示します。間違った顧客 ID を入力してください。 エラーメッセージが表示されます。

   ![display-validation-error](assets/display-validation-error.gif)
