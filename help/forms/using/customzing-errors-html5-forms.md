---
title: HTML5 フォームのエラーメッセージのカスタマイズ
seo-title: Customizing error messages for HTML5 forms
description: 位置や外観を変更する方法など、HTML5 フォームのエラーメッセージの表示をカスタマイズする方法について説明します。
seo-description: Learn how to customize the display of error messages for HTML5 forms including how to change their position and appearance.
uuid: 6f48b64e-858f-4323-ad50-88e25f3c2e3d
products: SG_EXPERIENCEMANAGER/6.4/FORMS
topic-tags: customization
discoiquuid: 44e49789-9075-41b3-bce8-03e8efce2d5a
feature: Mobile Forms
exl-id: e8a53976-e9bd-459d-92f5-88527c72428b
source-git-commit: bd94d3949f0117aa3e1c9f0e84f7293a5d6b03b4
workflow-type: tm+mt
source-wordcount: '515'
ht-degree: 60%

---

# HTML5 フォームのエラーメッセージのカスタマイズ {#customizing-error-messages-for-html-forms}

デフォルトの HTML5 フォームでは、エラーメッセージと警告の位置と外観（フォントや色）は固定されており、エラーは選択したフィールドに 1 つだけ表示されます。

この記事では、HTML5 フォームのエラーメッセージをカスタマイズし、

* エラーメッセージの外観と位置を変更する手順を説明します。エラーの表示位置は、フィールドの上側、下側、または右側から選べます。
* 複数のフィールドのエラーメッセージを任意の時点で表示できます。
* フィールドが選択されているかどうかに関わらずエラーを表示できます。

## エラーメッセージのカスタマイズ {#customizing-error-messages-nbsp}

エラーメッセージをカスタマイズする前に、添付のパッケージ（CustomErrorManager-1.0-SNAPSHOT.zip）をダウンロードして解凍します。

パッケージを展開したら、 CustomErrorManager-1.0-SNAPSHOT フォルダを開きます。 jcr_root および META-INF フォルダーが含まれます。 これらのフォルダーには、エラーメッセージのカスタマイズに必要な CSS ファイルと.JS ファイルが含まれています。

[ファイルを入手](assets/customerrormanager-1.0-snapshot.zip)

### エラーメッセージの位置のカスタマイズ  {#customizing-the-position-of-error-messages-nbsp}

エラーメッセージの位置をカスタマイズするには、 &lt;div> タグを付け、各エラーおよび警告フィールドに対して、 &lt;div> タグを左右に追加し、 &lt;div> タグを使用します。 詳細な手順については、以下に示す手順を参照してください。

1. `CustomErrorManager-1.0-SNAPSHOT` フォルダーに移動し、`etc\clientlibs\mf-custom-error-manager\CustomErrorManager\javascript` フォルダーを開きます。
1. `customErrorManager.js` ファイルを編集用として開きます。ファイル内の `markError` 関数は、次のパラメーターを受け付けます。

   |  |  |
   |---|---|
   | jqWidget | jqWidget はウィジェットのハンドルです。 |
   | msg | エラーメッセージを格納します |
   | type | エラーか警告かを示します |

1. 標準実装では、フィールドの右側にエラーメッセージが表示されます。 エラーメッセージを上側に表示するには、次のコードを使用します。

   ```
   markError: function (jqWidget, msg, type) {
               var element = jqWidget.element,                                //Gives the div containing widget
                   pos = $(element).offset(),                          //Calculates the position of the div in the view port
                                                                   msgHeight = xfalib.view.util.TextMetrics.measureExtent(msg).height + 5;  //Calculating the height of the Error Message
                   styles = {};
                   styles.left = pos.left + "px";         // Assign the desired left position using pos.left. Here it is calculated for exact left of the field 
                   styles.top = pos.top - msgHeight + "px";  // Assign the desired top position using pos.top. Here it is calculated for top of the field 
               if (type != "warning") {
                   if(!jqWidget.errorDiv){
                                                                                   //Adding the warning div if it is not present already
                       jqWidget.errorDiv=$("<div id='customError'></div>").appendTo('body');
                   }
                   jqWidget.$css(jqWidget.errorDiv.get(0), styles); // Applying the styles to the warning div
                   jqWidget.errorDiv.text(msg).show();                     //Showing the warning message
               } else {
                   if(!jqWidget.errorDiv){
                                                                                   //Adding the error div if it is not present already
                       jqWidget.errorDiv=$("<div id='customWarning'></div>").appendTo('body');
                   }
                   jqWidget.$css(jqWidget.errorDiv.get(0), styles); // Applying the styles to the error div
                   jqWidget.errorDiv.text(msg).show();                     //Showing the warning message
               }
   
           },
   ```

1. ファイルを保存して閉じます。
1. `CustomErrorManager-1.0-SNAPSHOT` フォルダーに移動し、jcr_root フォルダーと META-INF フォルダーのアーカイブを作成します。アーカイブの名前を CustomErrorManager-1.0-SNAPSHOT.zip に変更します。
1. パッケージマネージャーを使用し、パッケージをアップロードしてインストールします。

## 複数のフィールドのエラーメッセージを表示  {#display-error-messages-for-multiple-fields-nbsp}

添付されたパッケージを使用して、すべてのフィールドのエラーメッセージを同時に表示します。 エラーメッセージを単独で表示するには、デフォルトのプロファイルを使用します。

### エラーメッセージの外観のカスタマイズ。  {#customizing-the-appearance-of-error-messages-nbsp}

1. etc\clientlibs\mf-custom-error-manager\CustomErrorManager\css フォルダーに移動します。

1. sample.css ファイルを開いて編集します。css ファイルには 2 つの ID( #customError, #customWarning ) が含まれています。 これらの ID を使用して、色、フォントサイズなど、様々なプロパティを変更できます。

   次のコードを使用して、エラー／警告メッセージのフォントサイズと色を変更します。

   ```
   #customError {
   color: #0000FF; // it changes the color of Error Message
   display:none;
   position:absolute;
   opacity:0.85;
   font-size: 24px;  // it changes the font size of Error Message
   z-index:5;
   }
   
   #customWarning {
   color: #00FF00;  // it changes the color of Warning Message
   display:none;
   position:absolute;
   opacity:0.85;
   font-size: 18px;   // it changes the font size of Warning Message
   z-index:5;
   }
   
   Save the changes.
   ```

1. ファイルを保存して閉じます。
1. CustomErrorManager-1.0-SNAPSHOT フォルダーに移動し、jcr_root および META-INF フォルダーのアーカイブを作成します。 アーカイブの名前を CustomErrorManager-1.0-SNAPSHOT.zip に変更します。
1. パッケージマネージャーを使用し、パッケージをアップロードしてインストールします。

## 新しいプロファイルでフォームをレンダリングします。  {#render-the-form-with-the-new-profile-nbsp}

初期設定では、HTML5 フォームは次のデフォルトのプロファイルを使用しています。https://&lt;server>/content/xfaforms/profiles/default.html?contentRoot=&lt;XDP の場所>&amp;template=&lt;XDP の名前>

カスタムのエラーメッセージでフォームを表示するには、次のエラープロファイルでフォームをレンダリングします。https://&lt;server>/content/xfaforms/profiles/error.html?contentRoot=&lt;XDP の場所>&amp;template=&lt;XDP の名前>

>[!NOTE]
>
>エラープロファイルは、添付されているパッケージによりインストールされます。
