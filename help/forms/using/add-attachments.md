---
title: 添付ファイルの追加
seo-title: Adding attachments
description: 写真や手書きメモを注釈としてAEM Formsアプリのタスクに追加する
seo-description: Add photographs and scribble notes as annotations to your task in the AEM Forms app
uuid: cf8b54a8-e5bc-49df-90f8-c6a37533c347
content-type: reference
products: SG_EXPERIENCEMANAGER/6.4/FORMS
topic-tags: forms-app
discoiquuid: 184b5c7f-a704-4b8c-b1ec-f4d6616a1afc
exl-id: ad1cc63a-cf99-456b-8b83-0605fb3ac6ec
source-git-commit: c5b816d74c6f02f85476d16868844f39b4c47996
workflow-type: tm+mt
source-wordcount: '597'
ht-degree: 55%

---

# 添付ファイルの追加 {#adding-attachments}

>[!CAUTION]
>
>AEM 6.4 の拡張サポートは終了し、このドキュメントは更新されなくなりました。 詳細は、 [技術サポート期間](https://helpx.adobe.com/jp/support/programs/eol-matrix.html). サポートされているバージョンを見つける [ここ](https://experienceleague.adobe.com/docs/?lang=ja).

## AEM Forms Workflow（JEE 上の AEM Forms）と同期されたフォーム内で、添付ファイルを追加する {#adding-annotations}

AEM Formsアプリを使用すると、AEM Forms JEE サーバーと同期されたフォームに、画像、手書きメモ、テキストメモを添付できます。 フォームがAEM Forms Workflow サーバーから読み込まれると、添付ファイルがフォームに追加されます。 添付ボタン ![attachments-app](assets/attachments-app.png) をタップすると、フォームに添付されたファイルを一括表示することができます。赤色の通知は、フォームの添付ファイルの数を表示します。フォームに添付ファイルが存在しない場合、赤の通知ボタンは表示されません。フォームに添付ファイルが存在しない場合に添付ファイルボタン ![attch](assets/attch.png) をタップすると、写真や手書きメモを添付できるオプションが表示されます。

以下のオプションがあります。

* **[!UICONTROL ギャラリー]**：デバイス上に保存された画像を追加することができます。

* **[!UICONTROL カメラ]**：写真を撮ってフォームに追加できます。

* **[!UICONTROL メモ]**：手書きメモやテキストメモを追加できます。手書きメモを追加するには![手書き](assets/scribble.png)を、テキストメモを追加するには![キーボード](assets/keyboard.png)を使用します。

>[!NOTE]
>
>単一ユーザーによって追加された添付ファイルは、他の AEM Forms アプリケーションのユーザーにも表示されます。他のユーザーは、ユーザーが追加した添付ファイルを削除することはできません。

### 添付ファイル画面 {#the-attachments-screen}

すべての添付ファイルを一括表示するには、![attachments-app](assets/attachments-app.png) をタップします。ここでは、添付ファイルの追加、名前変更、削除が可能です。

![すべての添付ファイルを集めた状態](assets/attachments-screen.png)

別の画像、手書きメモまたはテキストを添付する場合は、添付ファイル画面の「**+**」ボタンを使用することができます。

### 写真の追加 {#adding-a-photograph}

モバイルデバイスのカメラを使用したり、デバイスに保存した画像を使用して、フォームに画像を添付したりできます。

1. ウィンドウ下部にある添付ファイルボタン ![attch](assets/attch.png) をクリックします。
1. 表示されるポップアップの中から、「**[!UICONTROL ギャラリー]**」または「**[!UICONTROL カメラ]**」をタップします。
1. 選択したオプションに基づいて、次の操作を実行します。

   1. 次を選択した場合、 **[!UICONTROL カメラ]**.

      写真を撮りなさい。 次に&#x200B;**[!UICONTROL 使用]** ![use-pic](assets/use-pic.png)ボタンをタップします。

      あるいは、**[!UICONTROL 撮り直し]** ![retake](assets/retake.png) ボタンをタップして写真を撮り直します。

   1. 次を選択した場合、 **[!UICONTROL ギャラリー]**.

      デバイスの画像ブラウザーがポップアップ表示されます。 デバイスの画像ブラウザーから、添付する画像をタップします。

### メモを追加する {#adding-a-note}

「**メモ**」オプションでは、フォームに手書きメモやテキストメモの添付ファイルを追加することができます。

1. ウィンドウ下部にある添付ファイルボタン ![attch](assets/attch.png) をクリックします。
1. タップ **[!UICONTROL メモ]** が表示されるポップアップに表示されます。
1. 起動した Notes ユーザーインターフェイスで、フリーハンドの手書きメモをキャプチャします。

   ![手書きメモインターフェイス](assets/scribble-ui.png)
   **図：** *手書き*

   手書きメモインターフェイスでは、次のオプションを使用できます。

   * **[!UICONTROL クリア]**:画面をクリアします。
   * **[!UICONTROL 完了]**:現在の手書きメモを添付します。
   * **[!UICONTROL キャンセル]**:現在の手書きメモを破棄し、手書きメモユーザーインターフェイスを終了します。
   * ![キーボード](assets/keyboard.png)：手書きメモをクリアし、テキストメモを追加します。

   ![AEM Forms アプリの手書きメモ画面に表示されたキーボード](assets/keyboard-inapp.png)

## AEM Forms Workflow を使用せずにAEM Formsサーバーと同期されたフォームの添付ファイル (OSGi 上のAEM Forms) {#attachments-in-forms-synced-with-the-aem-forms-servers-without-aem-forms-workflow-aem-forms-on-osgi}

AEM Forms OSGi サーバーと同期されたモバイルフォームの添付ファイルは、AEM Forms JEE サーバーと同様に機能します。

フォームレベルの添付ファイルは、AEM Forms OSGi サーバーからアプリ内で読み込まれたアダプティブフォームではサポートされていません。 画像やテキストメモを添付するには、フォームの作成時にフィールドレベルの添付ファイルを有効にします。 ファイル添付コンポーネントを、コンポーネントブラウザーからフィールドにドラッグ&amp;ドロップします。

アダプティブフォームでは、添付されたファイルをレコードのドキュメント（DoR）に表示することができます。[非 XFA アダプティブフォームにおける、レコードのドキュメントの生成](/help/forms/using/generate-document-of-record-for-non-xfa-based-adaptive-forms.md)を参照してください。
