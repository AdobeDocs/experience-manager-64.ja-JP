---
title: ページへのダイナミックメディアアセットの追加
seo-title: ページへの Dynamic Media アセットの追加
description: AEM 内のページに Dynamic Media コンポーネントを追加する方法
seo-description: AEM 内のページに Dynamic Media コンポーネントを追加する方法
uuid: 77abcb87-2df7-449b-be52-540d749890b6
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.4/ASSETS
topic-tags: dynamic-media
content-type: reference
discoiquuid: d1f45751-1761-4d6b-b17d-110b2f1117ea
translation-type: tm+mt
source-git-commit: b698a1348df3ec2ab455c236422784d10cbcf7c2
workflow-type: tm+mt
source-wordcount: '2829'
ht-degree: 61%

---


# ページへの Dynamic Media アセットの追加 {#adding-dynamic-media-assets-to-pages}

To add the dynamic media functionality to assets you use on your websites, you can add the **Dynamic Media** or **Interactive Media** component directly on the page. そのためには、レイアウトモードに切り替えて、ダイナミックメディアコンポーネントを有効にします。次に、これらのコンポーネントをページに追加し、そのコンポーネントにアセットを追加できます。ダイナミックメディアコンポーネントおよびインタラクティブメディアコンポーネントはスマートであり、追加しているアセットが画像であるかビデオであるかを自動的に把握します。それに従って、使用可能なオプションが変わります。

You add dynamic media assets directly to the page if you are using AEM as your WCM. If you are using a third-party for your WCM, either [link](linking-urls-to-yourwebapplication.md) or [embed](embed-code.md) your assets. For a responsive third-party web site, see [delivering optimized images to a responsive site](responsive-site.md).

>[!NOTE]
>
>AEM のページに追加する前にアセットを公開する必要があります。[Dynamic Media アセットの公開](publishing-dynamicmedia-assets.md)を参照してください。

## ページへの Dynamic Media コンポーネントの追加 {#adding-a-dynamic-media-component-to-a-page}

ダイナミックメディアコンポーネントをページに追加するのは、コンポーネントをページに追加するのと同じです。 ダイナミックメディアコンポーネントについては、以下の節で詳しく説明します。

>[!NOTE]
>
>読み取り専用権限を持つユーザーがWebページにアクセスするダイナミックメディアコンポーネントがある場合、ページが壊れ、コンポーネントが正しくレンダリングされません。 これは、コンポーネントのプロパティが適切で、参照されているアセットや設定にアクセスできることを確認するためにページが再構築されるためです。 次に、ページが再びレンダリングされ、コンポーネントが壊れます。ユーザーの読み取り専用アクセス権が原因で、ページ上の各コンポーネントコードを再レンダリングできません。
>  
>この問題を回避するには、AEM Sitesのユーザーに、アセットへのアクセスに必要な権限があることを確認してください。

1. AEM で、Dynamic Media コンポーネントを追加するページを開きます。
1. ページの左側にあるパネル（サイドパネルの表示を切り替える必要がある場合があります）で、 **[!UICONTROL コンポーネント]** アイコンをクリックします。
1. 「 **[!UICONTROL コンポーネント]** 」見出しのドロップダウンリストで、「 **[!UICONTROL ダイナミックメディア]**」を選択します。 Dynamic Media コンポーネントのリストがない場合は、使用する Dynamic Media コンポーネントを有効にしなければならない可能性があります。詳しくは、[Dynamic Media コンポーネントの有効化](#enabling-dynamic-media-components)を参照してください。

   ![chlimage_1-537](assets/chlimage_1-537.png)

1. 使用するダイナミックメディアコンポーネントをページの目的の位置にドラッグします。
1. コンポーネントの上に直接マウスポインターを置きます。コンポーネントが青色のボックスで囲まれた時点で 1 回タップすると、コンポーネントのツールバーが表示されます。****&#x200B;設定（レンチ） アイコンをタップします。
1. [必要に応じてコンポーネントを編集し](#dynamic-media-components) 、チェックマークをクリックして変更を保存します。

### Dynamic Media コンポーネントの有効化 {#enabling-dynamic-media-components}

ページに追加できる Dynamic Media コンポーネントがない場合は、使用するコンポーネントをまず有効にしなければならない可能性があります。

1. AEM で、Dynamic Media コンポーネントを追加するページを開きます。
1. ページ上部付近のツールバーの左側にあるページ情報アイコンをタップした後、ドロップダウンリストから「**[!UICONTROL テンプレートを編集]**」をタップします。

   ![edit-template](/help/assets/assets-dm/edit-template.png)

1. ページ上部付近のツールバーの右側で、ドロップダウンリストから「**[!UICONTROL 構造]**」をタップします。

   ![ポリシー](/help/assets/assets-dm/structure-mode.png)

1. ページ下部付近の「**[!UICONTROL レイアウトコンテナ]**」をタップしてツールバーを開き、ポリシーアイコンをタップします。
1. **[!UICONTROL レイアウトコンテナ]**&#x200B;ページの「**[!UICONTROL プロパティ]**」見出しの下で、「**[!UICONTROL 許可されたコンポーネント]**」タブが選択されていることを確認します。

   ![許可されたコンポーネント](/help/assets/assets-dm/allowed-components.png)

1. **[!UICONTROL Dynamic Media]** が表示されるまでスクロールします。
1. **[!UICONTROL Dynamic Media]** の左側にある「>」アイコンをタップしてリストを展開し、有効にする Dynamic Media コンポーネントを選択します。

   ![Dynamic Media コンポーネントリスト](/help/assets/assets-dm/dm-components-select.png)

1. **[!UICONTROL レイアウトコンテナ]**&#x200B;ページの右上隅付近にある「完了」（チェックマーク）アイコンをタップします。

1. ページ上部付近のツールバーの右側で、ドロップダウンリストから「**[!UICONTROL 初期コンテンツ]**」をタップした後、通常どおりに[ページに Dynamic Media コンポーネントを追加](#adding-a-dynamic-media-component-to-a-page)します。

## Localizing Dynamic Media components {#localizing-dynamic-media-components}

Dynamic Media コンポーネントのローカライズの方法は 2 つあります。

* Sites の Web ページ内で、**[!UICONTROL プロパティ]**&#x200B;を開き、「**[!UICONTROL 詳細]**」タブを選択します。ローカライズに使用したい言語を選択します。

   ![chlimage_1-538](assets/chlimage_1-538.png)

* サイトセレクターからページあるいはページグループを選択します。「**[!UICONTROL プロパティ]**」をタップし、「**[!UICONTROL 詳細]**」タブを選択します。ローカライズに使用したい言語を選択します。

   >[!NOTE]
   >
   >現在&#x200B;**[!UICONTROL 言語]**&#x200B;メニューに表示される言語すべてにトークンが割り当てられているわけではないことに注意してください。

## Dynamic Media components {#dynamic-media-components}

Dynamic Media and Interactive Media are available under the [!UICONTROL Dynamic Media] tab in [!UICONTROL Components]. [!UICONTROL インタラクティブメディア]コンポーネントは、すべてのインタラクティブアセット（インタラクティブビデオ、インタラクティブ画像、カルーセルセットなど）に使用します。その他すべてのダイナミックメディアコンポーネントでは、ダイナミックメディアコンポーネントを使用します。

>[!NOTE]
>
>これらのコンポーネントはデフォルトでは使用できないので、使用前にテンプレートエディターで使用可能にする必要があります。[テンプレートエディターでコンポートを使用可能にした後は、他の AEM コンポーネントと同様にページに追加することができます。](/help/sites-authoring/templates.md#editing-templates-template-authors)

![chlimage_1-539](assets/chlimage_1-539.png)

### Dynamic Media コンポーネント {#dynamic-media-component}

ダイナミックメディアコンポーネントはスマートです。画像を追加するかビデオを追加するかに応じて、様々なオプションがあります。 このコンポーネントは画像プリセット、画像ベースのビューア（画像セット、スピンセット、混在メディアセットなど）およびビデオをサポートします。また、ビューアはレスポンシブです。 つまり、画面のサイズは、画面のサイズに基づいて自動的に変更されます。 すべてのビューアは HTML5 ビューアです。

>[!NOTE]
>
>読み取り専用権限を持つユーザーがWebページにアクセスするダイナミックメディアコンポーネント、インタラクティブメディアコンポーネント、またはその両方がある場合、ページの切れ目とコンポーネントは正しくレンダリングされません。 これは、コンポーネントのプロパティが適切で、参照されているアセットや設定にアクセスできることを確認するためにページが再構築されるためです。 次に、ページが再びレンダリングされ、コンポーネントが壊れます。ユーザーの読み取り専用アクセス権が原因で、ページ上の各コンポーネントコードを再レンダリングできません。
>  
>この問題を回避するには、AEM Sitesのユーザーに、アセットへのアクセスに必要な権限があることを確認してください。

>[!NOTE]
>
>Dynamic Media コンポーネントを追加したときに、「**[!UICONTROL Dynamic Media 設定]**」が空であるかアセットを適切に追加できない場合は、次の点を確認してください。
>
>* [Dynamic Media を有効にしている](config-dynamic.md)こと。Dynamic Media はデフォルトで無効になっています。
>* 画像が PTIFF（Pyramid TIFF）ファイルであること。Dynamic Media を有効にする前に読み込まれた画像には、pyramid tiff ファイルはありません。

>



#### 画像を操作する場合 {#when-working-with-images}

Dynamic Media コンポーネントでは、画像セット、スピンセット、混在メディアセットなどの動的イメージを追加できます。ズームイン、ズームアウト、スピンセット内での画像の回転（該当する場合）または別のタイプのセットからの画像の選択をおこなうことができます。

また、ビューアプリセット、画像プリセットまたは画像形式をコンポーネント内で直接設定することもできます。画像をレスポンシブにするために、ブレークポイントの設定かレスポンシブ画像プリセットの適用のいずれかを実行できます。

You must edit the following Dynamic Media Settings by clicking the **[!UICONTROL Edit]** icon in the component and then **[!UICONTROL Dynamic Media Settings]**.

![dm-settings-image-preset](assets/dm-settings-image-preset.png)

>[!NOTE]
>
>デフォルトでは、Dynamic Media 画像コンポーネントはアダプティブです。If you want to make it a fixed size, set it in the component in the **[!UICONTROL Advanced]** tab with the **[!UICONTROL Width]** and **[!UICONTROL Height]** settings.

* **[!UICONTROL ビューアプリセット]**&#x200B;ドロップダウンメニューから既存のビューアプリセットを選択します。 探しているビューアプリセットが表示されない場合は、表示できるように設定する必要があります。詳しくは、ビューアプリセットの管理を参照してください。画像プリセットを使用している場合は、ビューアプリセットを選択できません。逆の場合も同様です。これは、画像セット、スピンセットまたは混在メディアセットを表示している場合に唯一使用できるオプションです。表示されるビューアプリセットもスマートであり、関連するビューアプリセットのみが表示されます。

* **[!UICONTROL ビューア修飾子]**&#x200B;ビューア修飾子は、name=valueの形式で&amp;区切り文字を付けたもので、ビューアを変更できます。詳しくは、ビューアリファレンスガイドを参照してください。 ビューアの修飾子の例としては、posterimage=img.jpg&amp;caption=text.vtt,1があります。この場合、ビデオサムネールに別の画像が設定され、クローズドキャプション/サブタイトルファイルがビデオに関連付けられます。

* **[!UICONTROL 画像プリセット]**&#x200B;ドロップダウンメニューから既存の画像プリセットを選択します。 探している画像プリセットが表示されない場合は、表示できるように設定する必要があります。「画像プリセットの管理」を参照してください。画像プリセットを使用している場合は、ビューアプリセットを選択できません。逆の場合も同様です。このオプションは、画像セット、スピンセットまたは混在メディアセットを表示している場合には使用できません。

* **[!UICONTROL 画像修飾子]**：追加の画像コマンドを入力して、画像効果を適用できます。 これらは画像プリセットと画像をサーブするコマンドリファレンスに記述されています。このオプションは、画像セット、スピンセットまたは混在メディアセットを表示している場合には使用できません。

* **[!UICONTROL ブレークポイント]**&#x200B;レスポンシブサイトでこのアセットを使用する場合は、画像のブレークポイントを追加する必要があります。 画像のブレークポイントをコンマ（,）で区切って指定する必要があります。このオプションを使用できるのは、画像プリセットで高さまたは幅が定義されていないときです。このオプションは、画像セット、スピンセットまたは混在メディアセットを表示している場合には使用できません。コンポーネントの「**[!UICONTROL 編集]**」をクリックして、次の詳細設定を編集できます。

* **[!UICONTROL タイトル]**&#x200B;画像のタイトルを変更します。

* **[!UICONTROL Altグラフィックをオフにしてい追加るユーザーに対して、画像のタイトルをテキストで表示します。]**
このオプションは、画像セット、スピンセットまたは混在メディアセットを表示している場合には使用できません。

* **[!UICONTROL URL、開く場所]**&#x200B;アセットを設定して、リンクを開くことができます。 「URL」と「次のウィンドウで開く」で、同じウィンドウで開くか新しいウィンドウで開くかを指定します。このオプションは、画像セット、スピンセットまたは混在メディアセットを表示している場合には使用できません。

* **[!UICONTROL [幅]** ]と[ **[!UICONTROL 高さ]**]画像を固定サイズにする場合は、値をピクセル単位で入力します。 これらの値を空にすると、アダプティブなアセットになります。

#### ビデオを操作する場合 {#when-working-with-video}

Dynamic Media コンポーネントを使用して、ダイナミックビデオを Web ページに追加します。コンポーネントの編集時に、ページ上でビデオを再生するための事前定義済みのビデオビューアプリセットを使用するように選択できます。

![chlimage_1-540](assets/chlimage_1-540.png)

You must edit the following Dynamic Media Settings by clicking **[!UICONTROL Edit]** in the component.

>[!NOTE]
>
>デフォルトでは、Dynamic Media ビデオコンポーネントはアダプティブです。ビデオコンポーネントを固定サイズにする場合は、そのコンポーネントで、「**[!UICONTROL 詳細]**」タブの「**[!UICONTROL 幅]**」と「[!UICONTROL 高さ]」を使用してサイズを設定します。

* **[!UICONTROL ビューアプリセット]**&#x200B;ドロップダウンメニューから既存のビデオビューアプリセットを選択します。 探しているビューアプリセットが表示されない場合は、表示できるように設定する必要があります。詳しくは、ビューアプリセットの管理を参照してください。

* **[!UICONTROL ビューア修飾子]**&#x200B;ビューア修飾子は、name=valueのペアと&amp;区切り文字の形式をとり、Adobeビューアリファレンスガイドで概要を説明しているようにビューアを変更できます。 Posterimage=img.jpg&amp;caption=text.vtt,1 はビューア修飾子の一例です。

   例えば、ビューア修飾子を使用して、次の操作を行うことができます。

   * Associate a caption file with a video [caption.](https://docs.adobe.com/content/help/ja-JP/dynamic-media-developer-resources/library/viewers-aem-assets-dmc/video/command-reference-url-video/r-html5-video-viewer-url-caption.translate.html)
   * Associate a navigation file with a video [navigation.](https://docs.adobe.com/content/help/ja-JP/dynamic-media-developer-resources/library/viewers-aem-assets-dmc/video/command-reference-url-video/r-html5-video-viewer-url-navigation.translate.html)

You can edit the following [!UICONTROL Advanced Settings] by clicking **[!UICONTROL Edit]** in the component.

* **[!UICONTROL タイトル]**&#x200B;ビデオのタイトルを変更します。

* **[!UICONTROL 幅]** と **[!UICONTROL 高さ]**&#x200B;ビデオを固定サイズにする場合は、値をピクセル単位で入力します。 これらの値を空にすると、アダプティブな画像になります。

#### スマート切り抜きを操作する場合 {#when-working-with-smart-crop}

Dynamic Media コンポーネントを使用して、スマート切り抜き画像アセットを Web ページに追加します。コンポーネントの編集時に、ページ上でビデオを再生するための事前定義済みのビデオビューアプリセットを使用するように選択できます。

[イメージプロファイル](image-profiles.md)も参照してください。

![dm-settings-smart-crop](assets/dm-settings-smart-crop.png)

You can edit the following [!UICONTROL Dynamic Media Settings] by clicking **[!UICONTROL Edit]** in the component.

>[!NOTE]
>
>デフォルトでは、Dynamic Media 画像コンポーネントはアダプティブです。画像コンポーネントを固定サイズにする場合は、そのコンポーネントで、「[!UICONTROL 詳細]」タブの「**[!UICONTROL 幅]**」と「**[!UICONTROL 高さ]**」を使用してサイズを設定します。

* **[!UICONTROL 画像修飾子]**：追加の画像コマンドを入力して、画像効果を適用できます。 これらは画像プリセットと画像をサーブするコマンドリファレンスに記述されています。このオプションは、画像セット、スピンセットまたは混在メディアセットを表示している場合には使用できません。

You can edit the following **[!UICONTROL Advanced]** settings by clicking **[!UICONTROL Edit]** in the component.

* **[!UICONTROL タイトル]**&#x200B;スマート切り抜き画像のタイトルを変更します。

* **[!UICONTROL Altグラフィックをオフにしてい追加るユーザーに対して、スマート切り抜き画像のタイトルをテキストで表示します。]**
このオプションは、画像セット、スピンセットまたは混在メディアセットを表示している場合には使用できません。

* **[!UICONTROL URL、開く場所]**&#x200B;アセットを設定して、リンクを開くことができます。 「URL」と「次のウィンドウで開く」で、同じウィンドウで開くか新しいウィンドウで開くかを指定します。このオプションは、画像セット、スピンセットまたは混在メディアセットを表示している場合には使用できません。

* **[!UICONTROL [高さ]** ]と[ **[!UICONTROL 幅]**]スマート切り抜き画像を固定サイズにする場合は、ピクセル単位で値を入力します。 これらの値を空にすると、アダプティブな画像になります。

### Interactive Media component {#interactive-media-component}

インタラクティブメディアコンポーネントは、インタラクティビティ（ホットスポットまたは画像マップ）を含むアセット用です。インタラクティブ画像、インタラクティブビデオまたはカルーセルバナーがある場合は、インタラクティブメディアコンポーネントを使用します。

インタラクティブメディアコンポーネントはスマートです。画像を追加するかビデオを追加するかに応じて、様々なオプションを使用できます。 さらに、レスポンシブビューアであるので、ビューアのサイズは画面サイズに合わせて自動的に変化します。すべてのビューアは HTML5 ビューアです。

>[!NOTE]
>
>読み取り専用権限を持つユーザーがWebページにアクセスするダイナミックメディアコンポーネント、インタラクティブメディアコンポーネント、またはその両方がある場合、ページの切れ目とコンポーネントは正しくレンダリングされません。 これは、コンポーネントのプロパティが適切で、参照されているアセットや設定にアクセスできることを確認するためにページが再構築されるためです。 次に、ページが再びレンダリングされ、コンポーネントが壊れます。ユーザーの読み取り専用アクセス権が原因で、ページ上の各コンポーネントコードを再レンダリングできません。
> 
>この問題を回避するには、AEM Sitesのユーザーに、アセットへのアクセスに必要な権限があることを確認してください。

![chlimage_1-541](assets/chlimage_1-541.png)

コンポーネントの「**[!UICONTROL 編集]**」をクリックして、次の&#x200B;**[!UICONTROL 一般]**&#x200B;設定を編集できます。

* **[!UICONTROL ビューアプリセット]**&#x200B;ドロップダウンメニューから既存のビューアプリセットを選択します。 探しているビューアプリセットが表示されない場合は、表示できるように設定する必要があります。ビューアプリセットを使用するには、あらかじめ公開する必要があります。詳しくは、ビューアプリセットの管理を参照してください。

* **[!UICONTROL タイトル]**&#x200B;ビデオのタイトルを変更します。

* **[!UICONTROL 幅]** と **[!UICONTROL 高さ]**&#x200B;ビデオを固定サイズにする場合は、値をピクセル単位で入力します。 これらの値を空にすると、アダプティブな画像になります。

コンポーネントの「**[!UICONTROL 編集]**」をクリックして、次の&#x200B;**[!UICONTROL 買い物かごに追加]**&#x200B;設定を編集できます。

* **[!UICONTROL Show Product Asset]**&#x200B;デフォルトでは、この値が選択されています。 製品アセットには、コマースモジュールで定義された製品の画像が表示されます。製品アセットを表示しない場合はチェックマークをオフにします。

* **[!UICONTROL 製品価格]**&#x200B;を表示デフォルトでは、この値が選択されています。 製品価格には、コマースモジュールで定義されたアイテムの価格が表示されます。製品価格を表示しない場合はチェックマークをオフにします。

* **[!UICONTROL 製品フォームを表示]**&#x200B;デフォルトでは、この値は選択されていません。 製品フォームには、サイズや色など製品のバリエーションが含まれます。製品のバリエーションを表示しない場合はチェックマークをオフにします。

### Panoramic Media component {#panoramic-media-component}

パノラマメディアコンポーネントは、球パノラマ画像のアセット用です。このような画像では、室内、物件、場所、風景などをあらゆる角度から見ることができます。画像が球パノラマとして適格となるには、以下の一方または両方の条件を満たしている必要があります。

* 縦横比が 2:1 である必要があります。
* キーワード「equirectangular」または（「spherical」+「panorama」）または（「spherical」+「panoramic」）でタグ付けされている必要があります。[タグの使用](/help/sites-authoring/tags.md)を参照してください。

縦横比とキーワードの両方の条件が、アセットの詳細ページと「パノラマメディア」WCM コンポーネントのパノラマアセットに適用されます。

![panoramic-media-viewer-preset](assets/panoramic-media-viewer-preset.png)

コンポーネントの「**[!UICONTROL 設定]**」をタップして、次の設定を編集できます。

* **[!UICONTROL ビューアプリセット]**「ビューアプリセット」ドロップダウンメニューから既存のビューアを選択します。

探しているビューアプリセットが表示されない場合は、そのビューアプリセットが公開されていることを確認してください。ビューアプリセットを使用するには、公開する必要があります。詳しくは、[ビューアプリセットの管理](managing-viewer-presets.md)を参照してください。

### HTTP/2 を使用した Dynamic Media アセットの配信 {#using-http-to-delivery-dynamic-media-assets}

HTTP/2 は、ブラウザーとサーバーの交信を強化する、新しく更新された Web プロトコルです。このプロトコルを使用すれば、情報の伝送を高速化し、必要な処理能力を抑えることができます。HTTP/2 上で Dynamic Media アセットの配信が可能になり、応答時間と読み込み時間が短縮されました。

Dynamic Media アカウントでの HTTP/2 の使用方法について詳しくは、[コンテンツの HTTP/2 配信](http2.md)を参照してください。

>[!MORELIKETHIS]
>
>* [AEM Dynamic Media でのカラーマネジメントについて](https://helpx.adobe.com/experience-manager/kt/assets/using/dynamic-media-color-management-technical-video-setup.html)
>* [AEM Dynamic Media でのカスタムビデオサムネールの使用](https://helpx.adobe.com/experience-manager/kt/assets/using/dynamic-media-video-thumbnails-feature-video-use.html)
>* [AEM Dynamic Media でのアセットビューアについて](https://helpx.adobe.com/experience-manager/kt/assets/using/dynamic-media-viewer-feature-video-understand.html)
>* [AEM Dynamic Media でのインタラクティブビデオの使用](https://helpx.adobe.com/experience-manager/kt/assets/using/dynamic-media-interactive-video-feature-video-use.html)
>* [AEM Dynamic Media でのビデオプレーヤーの使用](https://helpx.adobe.com/experience-manager/kt/assets/using/dynamic-media-video-player-feature-video-use.html)
>* [AEM Dynamic Media での画像シャープニングの使用](https://helpx.adobe.com/experience-manager/6-4/assets/using/best-practices-for-optimizing-the-quality-of-your-images.html)

