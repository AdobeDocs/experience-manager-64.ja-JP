---
title: ページへの Dynamic Media アセットの追加
seo-title: Adding Dynamic Media assets to pages
description: Web サイトで使用するアセットに Dynamic Media 機能を追加するには、ページに直接Dynamic Mediaまたはインタラクティブメディアコンポーネントを追加します。
seo-description: To add the dynamic media functionality to assets you use on your websites, you can add the Dynamic Media or Interactive Media component directly on the page.
uuid: 650d0867-a079-4936-a466-55b7a30803a2
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.4/ASSETS
topic-tags: authoring
content-type: reference
discoiquuid: 331f4980-5193-4546-a22e-f27e38bb8250
exl-id: b498d54e-ff34-49a1-bfad-c6efbb6f75f4
source-git-commit: c5b816d74c6f02f85476d16868844f39b4c47996
workflow-type: tm+mt
source-wordcount: '1721'
ht-degree: 51%

---

# ページへの Dynamic Media アセットの追加{#adding-dynamic-media-assets-to-pages}

>[!CAUTION]
>
>AEM 6.4 の拡張サポートは終了し、このドキュメントは更新されなくなりました。 詳細は、 [技術サポート期間](https://helpx.adobe.com/jp/support/programs/eol-matrix.html). サポートされているバージョンを見つける [ここ](https://experienceleague.adobe.com/docs/?lang=ja).

Web サイトで使用するアセットにダイナミックメディア機能を追加するには、**[!UICONTROL ダイナミックメディア]**&#x200B;または&#x200B;**[!UICONTROL インタラクティブメディア]**&#x200B;のコンポーネントをページに直接追加します。これを行うには、次のように入力します。 [!UICONTROL デザイン] モードに切り替えて、dynamic media コンポーネントを有効にします。 次に、これらのコンポーネントをページに追加し、そのコンポーネントにアセットを追加できます。ダイナミックメディアおよびインタラクティブメディアコンポーネントはスマートです。追加する画像またはビデオの種類が判別され、それに応じて使用可能なオプションが変わります。

AEMを WCM として使用している場合は、Dynamic Media アセットを直接ページに追加します。

>[!NOTE]
>
>画像マップは追加設定なしでカルーセルバナーで使用できます。

## ページへの Dynamic Media コンポーネントの追加 {#adding-a-dynamic-media-component-to-a-page}

[!UICONTROL ダイナミックメディア]または[!UICONTROL インタラクティブメディア]のコンポーネントをページに追加することは、任意のページにコンポーネントを追加するのと同じです。[!UICONTROL ダイナミックメディア]と[!UICONTROL インタラクティブメディア]のコンポーネントの詳細については、次のセクションで説明します。

ダイナミックメディアのコンポーネントやビューアをページに追加する場合：

1. AEM で、Dynamic Media コンポーネントを追加するページを開きます。
1. 使用できるDynamic Mediaコンポーネントがない場合は、 [!UICONTROL サイドキック] 入る **[!UICONTROL デザイン]** モード、クリック **[!UICONTROL 編集]** parsys と選択します。 **[!UICONTROL Dynamic Media]** を使用して、Dynamic Mediaコンポーネントを使用可能にします。

   >[!NOTE]
   >
   >詳しくは、[デザインモードでのコンポーネントの設定](/help/sites-authoring/default-components-designmode.md)を参照してください。

1. [!UICONTROL サイドキック]の鉛筆アイコンをクリックして、**[!UICONTROL 編集]**&#x200B;モードに戻ります。
1. サイドキックの&#x200B;**[!UICONTROL その他]**&#x200B;グループからページの目的の場所に、**[!UICONTROL ダイナミックメディア]**&#x200B;または&#x200B;**[!UICONTROL インタラクティブメディア]**&#x200B;のコンポーネントをドラッグします。
1. クリック **[!UICONTROL 編集]** をクリックして、コンポーネントを開きます。
1. [コンポーネントの編集](#dynamic-media-component) 必要に応じて、をクリックします。 **[!UICONTROL OK]** 変更を保存します。

## ダイナミックメディアコンポーネント {#dynamic-media-components}

[!UICONTROL ダイナミックメディア]および[!UICONTROL インタラクティブメディア]は、**[!UICONTROL ダイナミックメディア]** の[!UICONTROL サイドキック]で使用できます。**[!UICONTROL インタラクティブメディア]**&#x200B;コンポーネントは、すべてのインタラクティブアセット（インタラクティブビデオ、インタラクティブ画像、カルーセルセットなど）に使用します。その他すべての Dynamic Media コンポーネントの場合は、 **[!UICONTROL Dynamic Media]** コンポーネント。

![chlimage_1-71](assets/chlimage_1-71.png)

>[!NOTE]
>
>これらのコンポーネントはデフォルトでは使用できないので、使用する前にデザインモードで選択する必要があります。 [デザインモードで使用可能になった後](/help/sites-authoring/default-components-designmode.md)を使用すると、他のAEMコンポーネントと同様に、コンポーネントをページに追加できます。

### ダイナミックメディアコンポーネント {#dynamic-media-component}

ダイナミックメディアコンポーネントはスマートであり、追加しているアセットが画像であるかビデオであるかに応じて、様々なオプションを使用できます。このコンポーネントは、画像プリセット、画像ベースのビューア（画像セット、スピンセット、混在メディアセットなど）およびビデオをサポートしています。また、ビューアはレスポンシブです。つまり、画面のサイズは画面のサイズに基づいて自動的に変更されます。 ビューアはすべて HTML5 ベースのビューアです。

>[!NOTE]
>
>[!UICONTROL ダイナミックメディア]コンポーネントを追加したときに、「**[!UICONTROL ダイナミックメディア設定]**」が空であるかアセットを適切に追加できない場合は、次の点を確認してください。
>
>* お持ちの [有効なDynamic Media](/help/assets/config-dynamic.md). Dynamic Media はデフォルトでは無効になっています。
>* 画像が PTIFF（Pyramid TIFF）ファイルであること。Dynamic Media を有効にする前に読み込まれた画像には、PTIFF（Pyramid TIFF）ファイルはありません。
>


#### 画像を操作する場合 {#when-working-with-images}

[!UICONTROL ダイナミックメディア]コンポーネントを使用すると、画像セット、スピンセット、混在メディアセットなどの動的イメージを追加できます。ズームイン、ズームアウト、スピンセット内での画像の回転（該当する場合）または別のタイプのセットからの画像の選択を行うことができます。

また、ビューアプリセット、画像プリセット、画像形式をコンポーネント内で直接設定することもできます。画像をレスポンシブにするには、ブレークポイントを設定するか、レスポンシブな画像プリセットを適用します。

![chlimage_1-72](assets/chlimage_1-72.png)

コンポーネントで「**[!UICONTROL 設定]**」をクリックし、「**[!UICONTROL ダイナミックメディア設定]**」タブをクリックすると、次のダイナミックメディア設定を編集することができます。

![chlimage_1-73](assets/chlimage_1-73.png)

>[!NOTE]
>
>デフォルトでは、ダイナミックメディアの画像コンポーネントはアダプティブです。画像コンポーネントを固定サイズにする場合は、そのコンポーネントで、「**[!UICONTROL 詳細]**」タブの「**[!UICONTROL 幅]**」と「**[!UICONTROL 高さ]**」のプロパティを使用してサイズを設定します。

**[!UICONTROL ビューアプリセット]**  — ドロップダウンメニューから既存のビューアプリセットを選択します。 探しているビューアプリセットが表示されない場合は、表示できるように設定する必要があります。詳しくは、[ビューアプリセットの管理](/help/assets/managing-viewer-presets.md)を参照してください。画像プリセットを使用している場合はビューアプリセットを選択できません。また、その逆の場合も選択できません。

これは、画像セット、スピンセットまたは混在メディアセットを表示している場合に使用できる唯一のオプションです。 表示されるビューアプリセットもスマートで、関連するビューアプリセットのみが表示されます。

**[!UICONTROL 画像プリセット]**  — ドロップダウンメニューから既存の画像プリセットを選択します。 探している画像プリセットが表示されない場合は、表示できるように設定する必要があります。[画像プリセットの管理](/help/assets/managing-image-presets.md)を参照してください。画像プリセットを使用している場合はビューアプリセットを選択できません。また、その逆の場合も選択できません。

このオプションは、画像セット、スピンセットまたは混在メディアセットを表示している場合には使用できません。

**[!UICONTROL 画像の修飾子]**  — 追加の画像コマンドを指定することで、画像の効果を変更できます。 詳しくは、 [画像プリセットの管理](/help/assets/managing-viewer-presets.md) そして [コマンドリファレンス](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/http-protocol-reference/command-reference/c-command-reference.html?lang=ja).

このオプションは、画像セット、スピンセットまたは混在メディアセットを表示している場合には使用できません。

**[!UICONTROL ブレークポイント]**  — レスポンシブサイトでこのアセットを使用する場合は、ページのブレークポイントを追加する必要があります。 画像のブレークポイントは、コンマ (,) で区切る必要があります。 このオプションを使用できるのは、画像プリセットで高さまたは幅が定義されていないときです。

このオプションは、画像セット、スピンセットまたは混在メディアセットを表示している場合には使用できません。

コンポーネントで「**[!UICONTROL 編集]**」をクリックして、次の[!UICONTROL 詳細設定]を編集できます。

**[!UICONTROL タイトル]**  — 画像のタイトルを変更します。

**[!UICONTROL 代替テキスト]**  — グラフィックの表示をオフにしているユーザー向けのタイトルを画像に追加します。

このオプションは、画像セット、スピンセットまたは混在メディアセットを表示している場合には使用できません。

**[!UICONTROL URL、で開く]**  — からアセットを設定して、リンクを開くことができます。 「**[!UICONTROL URL]**」と「**[!UICONTROL 次のウィンドウで開く]**」で、同じウィンドウで開くか新しいウィンドウで開くかを指定します。

このオプションは、画像セット、スピンセットまたは混在メディアセットを表示している場合には使用できません。

**[!UICONTROL 幅と高さ]**  — 画像を固定サイズで表示する場合は、値をピクセル単位で入力します。 これらの値を空にすると、アダプティブなアセットになります。

#### ビデオを操作する場合 {#when-working-with-video}

以下を使用： [!UICONTROL Dynamic Media] ダイナミックビデオを web ページに追加するコンポーネントです。コンポーネントの編集時に、ページ上でビデオを再生するための事前定義済みのビデオビューアプリセットを使用するように選択できます。

![chlimage_1-74](assets/chlimage_1-74.png)

コンポーネントで「**[!UICONTROL 編集]**」をクリックして、次の [!UICONTROL Dynamic Media 設定]を編集できます。

>[!NOTE]
>
>デフォルトでは、Dynamic Media ビデオコンポーネントはアダプティブです。ビデオコンポーネントを固定サイズにする場合は、そのコンポーネントで、「**[!UICONTROL 詳細]**」タブの「**[!UICONTROL 幅]**」と「**[!UICONTROL 高さ]**」を使用してサイズを設定します。

**[!UICONTROL ビューアプリセット]**  — ドロップダウンメニューから既存のビデオビューアプリセットを選択します。 探しているビューアプリセットが表示されない場合は、表示できるように設定する必要があります。詳しくは、[ビューアプリセットの管理](/help/assets/managing-viewer-presets.md)を参照してください。

コンポーネントで「**[!UICONTROL 編集]**」をクリックして、次の[!UICONTROL 詳細]設定を編集できます。

**[!UICONTROL タイトル]**  — ビデオのタイトルを変更します。

**[!UICONTROL 幅と高さ]**  — ビデオを固定サイズで表示する場合は、値をピクセル単位で入力します。 これらの値を空にすると、アダプティブなビデオになります。

#### セキュアなビデオの配信方法 {#how-to-delivery-secure-video}

AEM 6.2 で、 [FP-13480](https://experience.adobe.com/#/downloads/content/software-distribution/jp/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq620/featurepack/cq-6.2.0-featurepack-13480)を使用すると、ビデオを安全な SSL 接続 (HTTPS) と安全でない接続 (HTTP) のどちらで配信するかを制御できます。 デフォルトでは、ビデオ配信プロトコルは、埋め込み Web ページのプロトコルから自動的に継承されます。 Web ページが HTTPS で読み込まれる場合、ビデオも HTTPS で配信されます。 逆に、Web ページが HTTP 上にある場合、ビデオは HTTP 経由で配信されます。 ほとんどの場合、このデフォルトの動作に問題はなく、設定を変更する必要はありません。 ただし、このデフォルトの動作は、 `VideoPlayer.ssl=on` を埋め込みコードスニペット内の URL パスの末尾または他のビューア設定パラメーターのリストに追加して、ビデオのセキュア配信を強制します。

セキュアなビデオ配信、および URL パスの `VideoPlayer.ssl` 設定属性の使用について詳しくは、『ビューアリファレンスガイド』の「[ビデオのセキュア配信](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-aem-assets-dmc/video/c-html5-video-viewer-20-securevideodelivery.html?lang=ja)」を参照してください。ビデオビューアのほか、混在メディアビューアおよびインタラクティブビデオビューアでも、セキュアなビデオ配信を使用できます。

### インタラクティブメディアコンポーネント {#interactive-media-component}

インタラクティブメディアコンポーネントは、そのようなホットスポットや画像マップに対してインタラクティブ機能を持つアセット用です。 インタラクティブ画像、インタラクティブビデオ、カルーセルバナーがある場合は、 **[!UICONTROL インタラクティブメディア]** コンポーネント。

[!UICONTROL インタラクティブメディア]コンポーネントはスマートであり、追加しているアセットが画像であるかビデオであるかに応じて、さまざまなオプションを使用できます。また、ビューアはレスポンシブです。つまり、画面のサイズは画面のサイズに基づいて自動的に変更されます。 ビューアはすべて HTML5 ベースのビューアです。

![chlimage_1-75](assets/chlimage_1-75.png)

コンポーネントの「**[!UICONTROL 編集]**」をクリックして、次の&#x200B;**[!UICONTROL 一般]**&#x200B;設定を編集できます。

**[!UICONTROL ビューアプリセット]**  — ドロップダウンメニューから既存のビューアプリセットを選択します。 探しているビューアプリセットが表示されない場合は、表示できるように設定する必要があります。ビューアプリセットを使用するには、あらかじめ公開する必要があります。詳しくは、ビューアプリセットの管理を参照してください。

**[!UICONTROL タイトル]**  — ビデオのタイトルを変更します。

**[!UICONTROL 幅と高さ]**  — ビデオを固定サイズで表示する場合は、値をピクセル単位で入力します。 これらの値を空にすると、アダプティブな画像になります。

コンポーネントの「**[!UICONTROL 編集]**」をクリックして、次の&#x200B;**[!UICONTROL 買い物かごに追加]**&#x200B;設定を編集できます。

**[!UICONTROL 製品アセットを表示]**  — デフォルトでは、この値が選択されています。 製品アセットには、コマースモジュールで定義された製品の画像が表示されます。 製品アセットを表示しない場合は、チェックマークをオフにします。

**[!UICONTROL 製品価格を表示]**  — デフォルトでは、この値が選択されています。 製品価格は、コマースモジュールで定義された品目の価格を示します。 製品価格を表示しない場合は、チェックマークをオフにします。

**[!UICONTROL 製品フォームを表示]**  — デフォルトでは、この値は選択されていません。 製品フォームには、サイズや色など、製品のバリエーションが含まれます。 製品バリアントを表示しない場合は、チェックマークをオフにします。
