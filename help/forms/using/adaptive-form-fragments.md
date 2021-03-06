---
title: アダプティブフォームフラグメント
seo-title: Adaptive form fragments
description: アダプティブフォームでは、任意のアダプティブフォームで使用することができる、パネルやフィールドのグループなどのフォームセグメントを作成することができます。また、既存のパネルをフラグメントとして保存することもできます。
seo-description: Adaptive forms provides a mechanism to create a form segment, such as a panel or a group of fields, as use it in any adaptive form. You can also save an existing panel as fragment.
uuid: 1629dd9e-b04e-4baa-ae87-c18d4550ac0f
products: SG_EXPERIENCEMANAGER/6.4/FORMS
topic-tags: author
discoiquuid: 4df5ee77-5a77-4efd-b7e1-c78e650673a9
feature: Adaptive Forms
exl-id: f63478c5-1798-428e-a662-f3db692b27fc
source-git-commit: bd94d3949f0117aa3e1c9f0e84f7293a5d6b03b4
workflow-type: tm+mt
source-wordcount: '2056'
ht-degree: 98%

---

# アダプティブフォームフラグメント {#adaptive-form-fragments}

すべてのフォームは特定の目的用に設計されますが、ほとんどのフォームには、いくつかの共通するセグメントがあります（例：名前と住所、家族の詳細、収入の詳細などの個人情報などを入力するためのセグメント）。フォームの開発者は、新しいフォームを作成するたびに、こうした共通セグメントを作成する必要があります。

アダプティブフォームには、パネルやフィールドグループなどのフォームセグメントを 1 回だけ作成するための便利な機能が用意されています。作成したフォームセグメントは、アダプティブフォームで再利用することができます。この再利用可能なスタンドアロンのセグメントは、アダプティブフォームフラグメントといいます。

## フラグメントの作成 {#create-a-fragment}

アダプティブフォームフラグメントは、最初から作成することも、パネルを既存のアダプティブフォーム内にフラグメントとして保存することもできます。

### フラグメントを最初から作成 {#create-fragment-from-scratch}

1. AEM Forms オーサーインスタンス（https://[*hostname*]:[*port*]/aem/forms.html）にログインします。
1. **[!UICONTROL 作成／アダプティブフォームフラグメント]**&#x200B;をクリックします。
1. フラグメントのタイトル、名前、説明、タグを指定します。

   >[!NOTE]
   >
   >フラグメントには一意の名前を指定します。同じ名前を持つ別のフラグメントが既に存在する場合、フラグメントの作成は失敗します。

1. 「**[!UICONTROL フォームモデル]**」タブをクリックして開き、「**[!UICONTROL 次から選択]**」ドロップダウンメニューから、フラグメントに対して次のいずれかのモデルを選択します。

   * **[!UICONTROL なし]**：フォームモデルを使用しないで最初からフラグメントを作成するときに指定します。
   * **[!UICONTROL フォームテンプレート]**：AEM Forms にアップロードされた XDP テンプレートを使用してフラグメントを作成するときに指定します。フラグメントのフォームモデルとして適当な XDP テンプレートを選択してください。

   ![フォームテンプレートをモデルとして使用したアダプティブフォームの作成](assets/form-template-model.png)

   選択したフォームテンプレート内でフラグメントとしてマークされたサブフォームも表示されます。ドロップダウンリストから、アダプティブフォームフラグメントのサブフォームを選択できます。

   ![指定したフォームテンプレートからサブフォームを選択する](assets/fragment-subform.png)

   さらに、ドロップダウンボックスでサブフォームのための SOM 式を指定することで、フォームテンプレート内でフラグメントとしてマークされていないサブフォームを使用したアダプティブフォームフラグメントを作成することもできます。

   * **[!UICONTROL XML スキーマ]**：AEM Forms にアップロードされた XML スキーマを使用して、フラグメントを作成するときに指定します。フラグメントのフォームモデルとして使用可能な XML スキーマからアップロードまたは選択できます。

   ![モデルとして XML スキーマに基づいてアダプティブフォームフラグメントを作成](assets/xml-schema-model.png)

   ドロップダウンボックスから選択されたスキーマにある complexType を選択することで、アダプティブフォームフラグメントを作成することもできます。

   ![指定した XML スキーマモデルから複合タイプを選択する](assets/complex-type.png)

1. 「**[!UICONTROL 作成]**」をクリックし、次に「**[!UICONTROL 開く]**」をクリックして、編集モードでデフォルトテンプレートを使ってフラグメントを開きます。

編集モードでは、AEM サイドキックから任意のアダプティブフォームコンポーネントをフラグメントにドラッグアンドドロップできます。アダプティブフォームコンポーネントについて詳しくは、「[アダプティブフォームの作成について](/help/forms/using/introduction-forms-authoring.md)」を参照してください。

さらに、フラグメントのフォームモデルとして、XML スキーマまたは XDP フォームテンプレートを選択していた場合は、フォームモデル階層を示す新しいタブがコンテンツファインダーに表示されます。これにより、フォームモデルエレメントをフラグメントにドラッグアンドドロップできます。追加されたフォームモデルエレメントはフォームコンポーネントに変換されますが、関連の XDP または XSD からの元のプロパティは保持されます。

### パネルをフラグメントとして保存 {#save-panel-as-a-fragment}

1. アダプティブフォームフラグメントとして保存するパネルが含まれているアダプティブフォームを開きます。
1. パネルツールバーで、「**[!UICONTROL フラグメントとして保存]**」をクリックします。フラグメントとして保存ダイアログが開きます。

   >[!NOTE]
   >
   >フラグメントとして保存しているパネルに子パネルが含まれている場合、生成されるフラグメントにはこれらの子パネルが含まれます。

1. フラグメント作成ダイアログで、次の情報を指定します。

   * **[!UICONTROL 名前]**：フラグメントの名前。デフォルト値はパネルのエレメント名です。このフィールドは必須です。

      >[!NOTE]
      >
      >フラグメントには一意の名前を指定します。同じ名前を持つ別のフラグメントが既に存在する場合、フラグメントの作成は失敗します。

   * **[!UICONTROL タイトル]**：フラグメントのタイトル。デフォルト値はパネルのタイトルです。
   * **[!UICONTROL 説明]**：フラグメントの説明。
   * **[!UICONTROL タグ]**：フラグメントのタグメタデータ。
   * **[!UICONTROL ターゲットパス]**：フラグメントが保存されるリポジトリーパス。パスを指定しない場合、フラグメントと同じ名前を持つノードが、アダプティブフォームを含むノードの横に作成されます。フラグメントはこのノードに保存されます。
   * **[!UICONTROL フォームモデル]**：アダプティブフォームのフォームモデルに応じて、このフィールドには「**[!UICONTROL XML スキーマ]**」、「**[!UICONTROL フォームテンプレート]**」、または「**[!UICONTROL なし]**」が表示されます。このフィールドは編集できません。
   * **[!UICONTROL フラグメントモデルルート]**：XSD ベースのアダプティブフォームにのみ表示されます。フラグメントモデルのルートを指定します。ドロップダウンリストから **/** または XSD 複合タイプを選択できます。フラグメントを別のアダプティブフォームで再利用できるのは、複合タイプをフラグメントモデルルートとして選択した場合のみです。

      **/** をフラグメントモデルルートとして選択した場合、ルートからの完全な XSD ツリーは、「アダプティブフォームデータモデル」タブに表示されます。複合タイプのフラグメントモデルルートの場合、選択した複合タイプの子孫のみが、「アダプティブフォームデータモデル」タブに表示されます。

   * **[!UICONTROL XSD 参照]**：XSD ベースのアダプティブフォームにのみ表示されます。XML スキーマの場所を表示します。
   * **[!UICONTROL XDP 参照]**：XSD ベースのアダプティブフォームにのみ表示されます。XDP フォームテンプレートの場所を表示します。

   ![save-fragment](assets/save-fragment.png)
   **図：** *フラグメントとして保存ダイアログ*

1. 「**[!UICONTROL OK]**」をクリックします。

   パネルがリポジトリー内の指定した場所またはデフォルトの場所に保存されます。アダプティブフォームでは、パネルがフラグメントのスナップショットによって置き換えられます。以下に示すように、「一般情報」パネルとその子パネル、個人情報、アドレスは、フラグメントとして保存されます。

   フラグメントを編集するには、パネルツールバーで「**[!UICONTROL アセットを編集]**」をクリックします。フラグメントが新しいタブまたはウィンドウ上に編集モードで開きます。

   ![フラグメントの編集](assets/edit-fragment.png)

## フラグメントの操作 {#working-with-fragments}

### フラグメントの外観の設定 {#configure-fragment-appearance}

アダプティブフォームに挿入したフラグメントはすべてプレースホルダーの画像として表示されます。プレースホルダーには、フラグメント内の子パネルのタイトルが最大 10 個まで表示されます。AEM Forms を設定することにより、プレースホルダーの画像の代わりにすべてのフラグメントを表示することができます。

次の手順を実行して、フォームのフラグメントをすべて表示します。

1. AEM Web コンソールの設定ページ（https:[*host*]:[*port*]/system/console/configMgr）に移動します。
1. **[!UICONTROL アダプティブフォームとインタラクティブ通信の web チャネル設定]**&#x200B;を検索およびクリックして、編集モードで開きます。
1. 「**[!UICONTROL フラグメントの代わりにプレースホルダーを有効にする]**」チェックボックスを無効にして、プレースホルダーの画像の代わりにすべてのフラグメントを表示します。

### アダプティブフォームへのフラグメントの挿入 {#insert-a-fragment-in-an-adaptive-form}

作成したアダプティブフォームフラグメントは、AEM コンテンツファインダーの「アダプティブフォームフラグメント」タブに表示されます。アダプティブフォームフラグメントをアダプティブフォーム内に挿入するには、次の手順を実行します。

1. アダプティブフォームフラグメントを挿入するアダプティブフォームを編集モードで開きます。
1. サイドバーの「**[!UICONTROL Assets]** ![assets-browser](assets/assets-browser.png)」をクリックします。アセットブラウザーで、ドロップダウンリストから「**[!UICONTROL アダプティブフォームフラグメント]**」を選択します。

   すべてのアダプティブフォームフラグメントを表示することも、あるいはフォームモデル（フォームテンプレート、XML スキーマ、またはベーシック）に基づいてフィルタリングすることもできます。

1. アダプティブフォームフラグメントをアダプティブフォームにドラッグアンドドロップします。

   >[!NOTE]
   >
   >アダプティブフォーム内で、アダプティブフォームフラグメントをオーサリング用として使用することはできません。また、JSON ベースのアダプティブフォームで XSD ベースのフラグメントを使用することも、XSD ベースのアダプティブフォームで JSON ベースのフラグメントを使用することもできません。

アダプティブフォームフラグメントは、アダプティブフォーム内の参照により挿入され、スタンドアロンのアダプティブフォームフラグメントと同期されます。このことは、アダプティブフォームフラグメントが更新されるとその変更がフラグメントが使用されているすべてのアダプティブフォーム内に反映されることを意味します。

### フラグメントのアダプティブフォーム内への埋め込み {#embed-a-fragment-in-adaptive-form}

アダプティブフォーム内にアダプティブフォームフラグメントを埋め込むには、 **[!UICONTROL 埋め込みアセット： *fragmentName *]**ボタンを使用して、追加されたフラグメントのパネルツールバーを表示できます（次の例を参照）。

![フォームフラグメントのアダプティブフォーム内への埋め込み](assets/embed-fragment.png)

>[!NOTE]
>
>埋め込まれたフラグメントは、スタンドアロンのフラグメントとリンクされなくなりました。埋め込まれたフラグメント内のコンポーネントは、アダプティブフォーム内から編集できます。

### フラグメント内でのフラグメントの使用 {#using-fragments-within-fragments}

入れ子のアダプティブフォームフラグメントを作成できます。このことはフラグメント内に別のフラグメントをドラッグアンドドロップし、入れ子のフラグメント構造を構築できることを意味します。

### フラグメントの変更 {#change-fragments}

アダプティブフォームフラグメントパネルのコンポーネントの編集ダイアログ内で&#x200B;**[!UICONTROL フラグメントアセットを選択]**&#x200B;プロパティを使用することで、アダプティブフォームフラグメントを別のフラグメントで置き換えたり変更したりできます。

## データ連結のためのフラグメントの自動マッピング {#auto-mapping-of-fragments-for-data-binding}

FXA フォームテンプレートまたは XSD 複合タイプを使用してアダプティブフォームフラグメントを作成しフラグメントをアダプティブフォームにドラッグアンドドロップすると、XFA フラグメントまたは XSD 複合タイプは、フラグメントモデルルートが XFA フラグメントまたは XSD 複合タイプにマッピングされている対応アダプティブフォームフラグメントによって自動的に置換されます。

コンポーネントの編集ダイアログから、フラグメントアセットとその連結を変更できます。

>[!NOTE]
>
>また、AEM コンテンツファインダーのアダプティブフォームフラグメントライブラリからバインドされたアダプティブフォームフラグメントをドラッグアンドドロップし、アダプティブフォームフラグメントパネルのコンポーネントの編集ダイアログから正しいバインド参照を与えることもできます。

## フラグメントの管理 {#manage-fragments}

AEM Forms UI を使用して、アダプティブフォームフラグメントに対して複数の操作を実行できます。

1. `https://[hostname]:[port]/aem/forms.html` にアクセスします。

1. AEM Forms UI ツールバーで「**[!UICONTROL 選択]**」をクリックし、アダプティブフォームフラグメントを選択します。ツールバーには、選択されているアダプティブフォームフラグメントに対して実行できる次の操作が表示されます。

<table> 
 <tbody> 
  <tr> 
   <td><p><strong>操作</strong></p> </td> 
   <td><p><strong>説明</strong></p> </td> 
  </tr> 
  <tr> 
   <td><p>次を開きます：</p> </td> 
   <td><p>選択されているアダプティブフォームフラグメントを編集モードで開きます。<br /><br /> </p> </td> 
  </tr> 
  <tr> 
   <td><p>プロパティを表示</p> </td> 
   <td><p>プロパティパネルを開きます。プロパティパネルから、プロパティを表示し編集したり、プレビューを生成したり、選択したフラグメントのサムネイル画像をアップロードしたりできます。詳しくは、「<a href="/help/forms/using/manage-form-metadata.md" target="_blank">メタデータの管理</a>」を参照してください。<br /> <br /> </p> </td> 
  </tr> 
  <tr> 
   <td><p>コピー</p> </td> 
   <td><p>選択されているフラグメントをコピーします。貼り付けボタンがツールバーに表示されます。<br /> <br /> </p> </td> 
  </tr> 
  <tr> 
   <td><p>ダウンロード</p> </td> 
   <td><p>選択されているフラグメントをダウンロードします。<br /> <br /> </p> </td> 
  </tr> 
  <tr> 
   <td><p>プレビュー</p> </td> 
   <td><p>フラグメントを HTML でプレビューするか、あるいは XML ファイルからのデータをフラグメントとマージしてカスタムプレビューを生成するかのオプションが与えられます。詳しくは、「<a href="/help/forms/using/previewing-forms.md" target="_blank">フォームのプレビュー</a>」を参照してください。<br /><br /> </p> </td> 
  </tr> 
  <tr> 
   <td><p>レビューの開始／レビューの管理</p> </td> 
   <td><p>選択されているフラグメントのレビューを開始したり管理したりできます。詳しくは、「<a href="/help/forms/using/create-reviews-forms.md" target="_blank">レビューの作成と管理</a>」を参照してください。<br /> <br /> </p> </td> 
  </tr> 
  <tr> 
   <td><p>辞書の作成</p> </td> 
   <td><p>選択されているフラグメントをローカライズするための辞書を生成します。詳しくは、「<a href="/help/forms/using/lazy-loading-adaptive-forms.md" target="_blank">アダプティブフォームのローカライズ</a>」を参照してください。<br /> <br /> </p> </td> 
  </tr> 
  <tr> 
   <td><p>公開／非公開</p> </td> 
   <td><p>選択されているフラグメントを公開／非公開します。<br /> <br /> </p> </td> 
  </tr> 
  <tr> 
   <td><p>削除</p> </td> 
   <td><p>選択されているフラグメントを削除します。<br /> <br /> </p> </td> 
  </tr> 
 </tbody> 
</table>

## フラグメントを含むアダプティブフォームのローカライズ {#localizing-adaptive-form-containing-fragments}

アダプティブフォームフラグメントを含むアダプティブフォームをローカライズするには、フラグメントとフォームを別々にローカライズする必要があります。考え方としては、フラグメントを一度ローカライズし、それを複数のアダプティブフォーム内で再利用します。

>[!NOTE]
>
>フラグメント内のローカリゼーションキーは、アダプティブフォームの XLIFF ファイル内には表示されません。

## フラグメントで作業するときの考慮事項 {#key-points-to-remember-when-working-with-fragments}

* フラグメント名が一意であることを確認します。同じ名前の既存のフラグメントが存在する場合、フラグメントの作成は失敗します。
* XDP ベースのアダプティブフォームでは、別の XDP フラグメントを含むフラグメントとしてパネルを保存すると、生成されるフラグメントは子 XDP フラグメントに自動的にバインドされます。XSD ベースのアダプティブフォームでは、生成されるフラグメントはスキーマルートにバインドされます。
* アダプティブフォームフラグメントを作成すると、フラグメントノードが作成されます。これは CRXDE Lite における、アダプティブフォームの guideContainer ノードに類似したものです。
* 異なるフォームデータモデルを使用するアダプティブフォーム内のフラグメントは、サポートされていません。例えば、XSD ベースのアダプティブフォームでは、XDP ベースのフラグメントはサポートされていません（その逆についても同様です）。
* アダプティブフォームフラグメントは、AEM コンテンツファインダー内の「アダプティブフォームフラグメント」タブを通して使用するようになっています。
* スタンドアロンのアダプティブフォームフラグメント内の式、スクリプト、またはスタイルは、アダプティブフォームの参照によって挿入されたときや、埋め込まれたときにも保持されます。
* アダプティブフォームフラグメントを編集することはできません。これはアダプティブフォーム内から参照によって挿入されたものです。編集するには、スタンドアロンのアダプティブフォームフラグメントを編集するか、アダプティブフォームにフラグメントを埋め込みます。
* アダプティブフォームを発行する場合は、参照によってアダプティブフォームに挿入されたスタンドアロンのアダプティブフォームフラグメントを発行する必要があります。
* 更新されたアダプティブフォームフラグメントを再発行すると、フラグメントが使用されているアダプティブフォームの発行済みインスタンスに変更が反映されます。
* 検証コンポーネントが含まれているアダプティブフォームの場合、匿名ユーザーはサポートされません。また、アダプティブフォームフラグメントで検証コンポーネントを使用することはお勧めしません。
* （**Mac のみ**）フォームフラグメント機能がすべてのシナリオで正しく動作するようにするには、/private/etc/hosts ファイルに次のエントリを追加します。

   `127.0.0.1 <Host machine>`

   **ホストマシン**：AEM Forms がデプロイされている Apple Mac マシン。

## リファレンスフラグメント {#reference-fragments}

フォームを作成するために使用できるリファレンスアダプティブフォームフラグメントが提供されています。詳しくは、[リファレンスフラグメント](/help/forms/using/reference-adaptive-form-fragments.md)を参照してください。
