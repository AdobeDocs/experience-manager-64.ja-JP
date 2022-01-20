---
title: Adobe Campaign コンポーネント
seo-title: Adobe Campaign Components
description: Adobe Campaign と統合しているときは、ニュースレター用とフォーム用のコンポーネントを使用できます。
seo-description: When you integrate with Adobe Campaign, you have components available for when working with newsletters and with forms
uuid: d1fb8649-8aae-49a5-8663-1b7cb74ee0e7
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.4/SITES
content-type: reference
topic-tags: personalization
discoiquuid: f328cd1e-30a3-42d2-88b7-64455ee9eb1f
exl-id: 02641496-188b-465c-9256-b2e377eb685c
source-git-commit: bd94d3949f0117aa3e1c9f0e84f7293a5d6b03b4
workflow-type: tm+mt
source-wordcount: '2765'
ht-degree: 73%

---

# Adobe Campaign コンポーネント{#adobe-campaign-components}

Adobe Campaign と統合しているときは、ニュースレター用とフォーム用のコンポーネントを使用できます。このドキュメントでは、両方のコンポーネントについて説明します。

## Adobe Campaign ニュースレターコンポーネント {#adobe-campaign-newsletter-components}

すべての Adobe Campaign コンポーネントは、[電子メールテンプレートのベストプラクティス](/help/sites-administering/best-practices-for-email-templates.md)で概説されているベストプラクティスに従います。また、Adobe マークアップ言語 [HTL](https://helpx.adobe.com/jp/experience-manager/htl/using/overview.html) をベースとしています。

Adobe Campaign と連携するように設定されているニュースレターまたは電子メールを開くと、「**Adobe Campaign ニュースレター**」セクションに以下のコンポーネントが表示されます。

* 見出し（Campaign）
* 画像（Campaign）
* リンク（Campaign）
* Dynamic Media画像テンプレート (Campaign)
* ターゲット参照（Campaign）
* テキストと画像（Campaign）
* テキストおよびパーソナライゼーション（Campaign）

これらのコンポーネントについては、以降のセクションで説明します。

コンポーネントは次のように表示されます。

![chlimage_1-105](assets/chlimage_1-105.png)

### 見出し（Campaign） {#heading-campaign}

見出しコンポーネントは、次のいずれかを表示します。

* 「**タイトル**」フィールドが空のときは、現在のページ名を表示します。
* 「**タイトル**」フィールドにテキストを指定したときは、そのテキストを表示します。

**見出し（Campaign）**&#x200B;コンポーネントを直接編集します。ページタイトルを使用する場合は空のままにします。

![chlimage_1-106](assets/chlimage_1-106.png)

次の項目を設定できます。

* **タイトル**
ページタイトル以外の名前を使用する場合は、ここに入力します。

* **見出しレベル（1、2、3、4）** HTML の見出しサイズ 1～4 に基づいた見出しレベル。

見出し（Campaign）コンポーネントの表示例を以下に示します。

![chlimage_1-107](assets/chlimage_1-107.png)

### 画像（Campaign） {#image-campaign}

画像（Campaign）コンポーネントは、指定されたパラメーターに従って、画像とそれに付随するテキストを表示します。

画像をアップロードした後に、編集および操作できます（切り抜き、回転、リンク／タイトル／テキストの追加など）。

画像は、[アセットブラウザー](/help/sites-authoring/author-environment-tools.md#assets-browser)から直接コンポーネントまたはコンポーネントの[設定ダイアログ](/help/sites-authoring/editing-content.md#edit-configure-copy-cut-delete-paste)にドラッグアンドドロップできます。設定ダイアログから画像をアップロードすることもできます。このダイアログでは、画像の定義および操作もすべて制御します。

![chlimage_1-108](assets/chlimage_1-108.png)

>[!NOTE]
>
>情報を **代替テキスト** 」フィールドに値が入力されていない場合、画像を保存できません。

画像のアップロード後（以前ではなく）、 [インプレース編集](/help/sites-authoring/editing-content.md#edit-configure-copy-cut-delete-paste) 必要に応じて画像を切り抜き/回転するには：

![](do-not-localize/chlimage_1-10.png)

>[!NOTE]
>
>インプレースエディターでは、編集時に、画像の元のサイズと縦横比を使用します。高さと幅のプロパティも指定できます。プロパティで定義したサイズや縦横比の制限は、編集の変更内容を保存するときに適用されます。
>
>インスタンスによっては、[ページのデザイン](/help/sites-developing/designer.md)によって最小、最大の制限が課される場合もあります。これらは、プロジェクト実装時に開発されます。

フルスクリーン編集モードで使用できる追加オプションがいくつか用意されています（マップ、ズームなど）。

![](do-not-localize/chlimage_1-11.png)

画像を読み込む際は、次の設定が可能です。

* **Map**

   画像をマッピングするには、「マップ」を選択します。 画像マップの作成方法（長方形、多角形など）を指定し、領域が指す位置を指定します。

* **切り抜き**

   「切り抜き」を選択して、画像を切り抜きます。 マウスを使用して画像を切り抜きます。

* **回転**

   画像を回転するには、「回転」を選択します。 画像が目的の向きになるまで繰り返し使用します。

* **消去**

   現在の画像を削除します。

* ズームバー（クラシックのみ）

   画像のズームインおよびズームアウトを行うには、画像の下（「OK」および「キャンセル」ボタンの上）のスライドバーを使用します。

* **タイトル**

   画像のタイトル。

* **代替テキスト**

   アクセシブルなコンテンツを作成する際に使用する代替テキスト。

* **リンク先**

   Web サイト内のアセットや他のページへのリンクを作成します。

* **説明**

   画像の説明。

* **サイズ**

   画像の高さと幅を設定します。

>[!NOTE]
>
>「**詳細**」タブの「**代替テキスト**」フィールドに情報を入力する必要があります。入力しない場合は画像を保存できず、次のエラーメッセージが表示されます。
>
>`Validation failed. Verify the values of the marked fields.`

画像（Campaign）コンポーネントの表示例を以下に示します。

![chlimage_1-109](assets/chlimage_1-109.png)

### リンク（Campaign） {#link-campaign}

リンク（Campaign）コンポーネントを使用して、ニュースレターにリンクを追加できます。

以下の項目を「**表示**」、「**URL 情報**」または「**詳細**」タブで設定できます。

* **リンクのキャプション**

   リンクのキャプション。 ユーザーに表示されるテキストです。

* **リンクツールヒント**

   リンクの使用方法に関する追加情報を追加しました。

* **LinkType**

   ドロップダウンリストで、 **カスタム URL** および **アダプティブドキュメント**. このフィールドは必須です。「カスタム URL」を選択した場合は、リンクの URL を指定できます。「アダプティブドキュメント」を選択した場合は、ドキュメントのパスを指定できます。

* **追加の URL パラメータ**

   その他の URL パラメーターを追加します。 「項目を追加」をクリックして、複数の項目を追加します。

>[!NOTE]
>
>情報を **リンクタイプ** フィールド **URL 情報** 」タブに移動しないと、コンポーネントを保存できず、次のエラーメッセージが表示されます。
>
>`Validation failed. Verify the values of the marked fields.`

リンク（Campaign）コンポーネントの表示例を以下に示します。

![chlimage_1-110](assets/chlimage_1-110.png)

### Scene7 画像テンプレート（Campaign） {#scene-image-template-campaign}

[Scene7画像テンプレート](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/template-basics/quick-start-template-basics.html#template-basics) はレイヤー化された画像ファイルで、コンテンツとプロパティをパラメータ化して可変性を持たせることができます。 この **画像テンプレート** コンポーネントを使用すると、ニュースレター内でDynamic Media Classic( 旧称Scene7) テンプレートを使用して、テンプレートパラメーターの値を変更できます。 また、パラメーター内でAdobe Campaignメタデータ変数を使用して、各ユーザーがパーソナライズされた方法で画像を体験できるようにすることができます。

![chlimage_1-111](assets/chlimage_1-111.png)

コンポーネントを設定するには、「**編集**」をクリックします。この節で説明する設定を構成できます。 このDynamic Media Classic( 旧称Scene7) の画像テンプレートについて詳しくは、 [Scene7画像テンプレートコンポーネント](/help/assets/scene7.md#image-template).

さらに、パラメーターパネルには、Dynamic Media Classic( 旧称Scene7) のテンプレートに対して定義されたすべてのテンプレートパラメーターが表示されます。 これらのパラメーターそれぞれに対して、値を変化させたり、変数を挿入したり、デフォルト値にリセットしたりできます。

![chlimage_1-112](assets/chlimage_1-112.png)

### ターゲット参照（Campaign） {#targeted-reference-campaign}

ターゲット参照（Campaign）コンポーネントを使用して、ターゲット段落への参照を作成できます。

このコンポーネント内で、ターゲット段落に移動して選択します。

フォルダーアイコンをクリックして、参照する段落に移動します。終了したら、チェックマークをクリックします。

### テキストと画像（Campaign） {#text-image-campaign}

テキストと画像（Campaign）コンポーネントでは、テキストブロックと画像を追加します。

クリックしてこのコンポーネントを設定する際には、「テキスト」または「画像」を選択します。

![chlimage_1-113](assets/chlimage_1-113.png)

「**テキスト**」を選択すると、インラインエディターが表示されます。

![](do-not-localize/chlimage_1-12.png)

「**画像**」を選択すると、画像用のインプレースエディターが表示されます。

![](do-not-localize/chlimage_1-13.png)

画像の使用について詳しくは、[画像（Campaign）コンポーネント](#image-campaign)を参照してください。テキストの使用について詳しくは、[テキストおよびパーソナライゼーション（Campaign）コンポーネント](#text-personalization-campaign)を参照してください。

テキストおよびパーソナライゼーション（Campaign）コンポーネントや画像（Campaign）コンポーネントと同様に、次の項目を設定できます。

* **テキスト**

   テキストを入力します。ツールバーを使用して書式設定の変更、リストの作成およびリンクの追加を行います。

* **画像**

   コンテンツファインダーから画像をドラッグするか、クリックして画像を参照します。必要に応じてトリミングや回転を行います。

* **画像のプロパティ** (**詳細画像プロパティ**)

   以下を指定できます。

   * **タイトル**

      ブロックのタイトル。マウスを置くと表示されます。

   * **代替テキスト**

      画像を表示できない場合に表示する代替テキスト。

   * **リンク先**

      Web サイト内のアセットや他のページへのリンクを作成します。

   * **説明**

      画像の説明。

   * **サイズ**

      画像の高さと幅を設定します。

>[!NOTE]
>
>「**詳細**」タブの「**代替テキスト**」フィールドは必須です。入力しない場合、コンポーネントを保存できず、次のエラーメッセージが表示されます。
>
>`Validation failed. Verify the values of the marked fields.`

テキストと画像（Campaign）コンポーネントの表示例を以下に示します。

![chlimage_1-114](assets/chlimage_1-114.png)

### テキストおよびパーソナライゼーション（Campaign） {#text-personalization-campaign}

テキストおよびパーソナライゼーション (Campaign) コンポーネントを使用すると、WYSIWYG エディターを使用してテキストブロックを入力できます。この機能は、 [リッチテキストエディター](/help/sites-authoring/rich-text-editor.md). さらに、このコンポーネントでは、Adobe Campaign のコンテキストフィールドとパーソナライゼーションブロックを使用できます。[パーソナライゼーションの挿入](/help/sites-authoring/campaign.md#inserting-personalization)も参照してください。

フォントの文字、配置、リンク、リスト、インデントなど、多様なアイコンでテキストの書式を設定できます。機能は、基本的に [両方の UI](/help/sites-authoring/editing-content.md)のルックアンドフィールは異なりますが、

![chlimage_1-115](assets/chlimage_1-115.png)

インプレースエディターで、テキストを追加し、ジャスティフィケーションを変更し、リンクを追加または削除し、コンテキストフィールドまたはパーソナライゼーションブロックを追加し、全画面モードに入ることができます。テキストまたはパーソナライゼーションの追加が完了したら、チェックマークを選択して変更を保存します（または「x」をクリックしてキャンセルします）。詳しくは、 [インプレース編集](/help/sites-authoring/editing-content.md#edit-configure-copy-cut-delete-paste) を参照してください。

>[!NOTE]
>
>* 使用できるパーソナライゼーションフィールドは、ニュースレターがリンクされている Adobe Campaign テンプレートによって異なります。
>* ContextHub からペルソナを選択すると、選択したプロファイルのデータでパーソナライゼーションフィールが自動的に置き換えられます。

>
>[パーソナライゼーションの挿入](/help/sites-authoring/campaign.md#inserting-personalization)を参照してください。

![chlimage_1-116](assets/chlimage_1-116.png)

>[!NOTE]
>
>**nms:seedMember** スキーマまたはその拡張で定義されているフィールドのみが考慮されます。**nms:seedMember** にリンクしているテーブルの属性は使用できません。

## Adobe Campaign フォームコンポーネント {#adobe-campaign-form-components}

Adobe Campaign コンポーネントを使用して、ニュースレターの購読や購読解除、ユーザープロファイルの更新といった手続きで記入するフォームを作成できます。詳細については、[Adobe Campaign フォームの作成](/help/sites-authoring/adobe-campaign-forms.md)を参照してください。

各コンポーネントフィールドを Adobe Campaign データベースフィールドにリンクできます。[コンポーネントとデータタイプ](#components-and-data-type)セクションで説明しているように、利用可能なフィールドは、格納するデータのタイプによって異なります。受信者スキーマを Adobe Campaign で拡張した場合は、データタイプが一致するコンポーネントで新しいフィールドが利用可能になります。

Adobe Campaignと統合するように設定されたフォームを開くと、次のコンポーネントが **Adobe Campaign** セクション：

* チェックボックス（Campaign）
* 日付フィールド（Campaign）と日付フィールド／HTML5（Campaign）
* 暗号化されたプライマリキー（Campaign）
* エラー表示（Campaign）
* 非表示の調整キー（Campaign）
* 数値フィールド（Campaign）
* オプションフィールド（Campaign）
* 購読チェックリスト（Campaign）
* テキストフィールド（Campaign）

コンポーネントは次のように表示されます。

![chlimage_1-117](assets/chlimage_1-117.png)

このセクションでは、各コンポーネントについて詳しく説明します。

### コンポーネントとデータタイプ {#components-and-data-type}

以下の表に、Adobe Campaign プロファイルデータの表示および変更に利用できるコンポーネントを示します。各コンポーネントを Adobe Campaign プロファイルフィールドにマップすることで、フィールドの値をフォームに表示したり、フォームが送信されたときにフィールドを更新したりできます。各種コンポーネントは、適切なデータタイプのフィールドにのみマップできます。

<table> 
 <tbody> 
  <tr> 
   <td><p><strong>コンポーネント</strong></p> </td> 
   <td><p><strong>Adobe Campaign フィールドのデータタイプ</strong></p> </td> 
   <td><p><strong>フィールドの例</strong></p> </td> 
  </tr> 
  <tr> 
   <td><p>チェックボックス (Campaign)</p> </td> 
   <td><p>ブール値</p> </td> 
   <td><p>今後は連絡しない（どのチャネルからも）</p> </td> 
  </tr> 
  <tr> 
   <td><p>日付フィールド (Campaign)</p> <p>日付フィールド / HTML 5 (Campaign)</p> </td> 
   <td><p>date</p> </td> 
   <td><p>誕生日</p> </td> 
  </tr> 
  <tr> 
   <td><p>数値フィールド (Campaign)</p> </td> 
   <td><p>数値（byte、short、long、double）</p> </td> 
   <td><p>年齢</p> </td> 
  </tr> 
  <tr> 
   <td><p>オプションフィールド (Campaign)</p> </td> 
   <td><p>値が関連付けられた byte</p> </td> 
   <td><p>性別</p> </td> 
  </tr> 
  <tr> 
   <td><p>テキストフィールド (Campaign)</p> </td> 
   <td><p>文字列</p> </td> 
   <td><p>電子メール</p> </td> 
  </tr> 
 </tbody> 
</table>

### 大部分のコンポーネントに共通の設定 {#settings-common-to-most-components}

Adobe Campaign コンポーネントには、ほとんどのコンポーネント（暗号化されたプライマリキーコンポーネントと非表示の調整キーコンポーネントを除く）に共通の設定があります。

大部分のコンポーネントでは、次の項目を設定できます。

#### タイトルとテキスト {#title-and-text}

![chlimage_1-118](assets/chlimage_1-118.png)

* **タイトル**

   要素名以外の名前を使用する場合は、ここに入力します。

* **タイトルを非表示にする**

   タイトルを表示しない場合は、このチェックボックスを選択します。

* **説明**

   フィールドに説明を追加して、ユーザーに詳細情報を提供します。

* **値の表示のみ**

   値が存在する場合にのみ値を表示

#### Adobe Campaign {#adobe-campaign}

次の項目を設定できます。

* **マッピング**

   必要に応じて、Adobe Campaignのパーソナライゼーションフィールドを選択します。

* **調整キー**

   このフィールドが紐付けキーの一部である場合は、このチェックボックスを選択します。

![chlimage_1-119](assets/chlimage_1-119.png)

#### 制約 {#constraints}

* **必須**

   このコンポーネントを必須にするには、このチェックボックスを選択します。つまり、ユーザーは値を入力する必要があります。

* **必須メッセージ**

   オプションで、フィールドが必須であることを示すメッセージを追加します。

![chlimage_1-120](assets/chlimage_1-120.png)

#### スタイル設定 {#styling}

* **CSS**&#x200B;このコンポーネントに使用する CSS クラスを入力します。

![chlimage_1-121](assets/chlimage_1-121.png)

### チェックボックス（Campaign） {#checkbox-campaign}

チェックボックス（Campaign）コンポーネントを使用すると、boolean データタイプの Adobe Campaign プロファイルフィールドをユーザーに変更させることができます。例えば、チェックボックス（Campaign）コンポーネントを使用して、受信者に連絡を希望するかどうかを選択させるオプションを作成できます。

チェックボックス（Campaign）コンポーネントでは、[大部分の Adobe Campaign コンポーネントに共通の設定](#settings-common-to-most-components)を使用できます。

チェックボックス（Campaign）コンポーネントの表示例を以下に示します。

![chlimage_1-122](assets/chlimage_1-122.png)

### 日付フィールド（Campaign）と日付フィールド／HTML 5（Campaign） {#date-field-campaign-and-date-field-html-campaign}

日付フィールドを使用して、受信者に日付を指定させることができます。例えば、受信者に誕生日を指定させることができます。日付の形式は、Adobe Campaign インスタンスで使用されている形式と一致します。

[大部分の Adobe Campaign コンポーネントに共通の設定](#settings-common-to-most-components)に加え、次の項目を設定できます。

* **制約 — 制約** ドロップダウン

   次を選択できます。 **なし** または **日付** — 日付の制約を追加するか、制約を追加しません。 日付を選択した場合、回答ユーザーは「 」フィールドに日付形式で入力する必要があります。

* **制約メッセージ**

   また、制約メッセージを追加して、回答を適切に書式設定する方法をユーザーに知らせることもできます。
* **スタイル設定 — 幅**
フィールドの幅を調整するには、 
**+** および **-** アイコンをクリックするか、数値を入力します。

幅が調整された日付フィールド（Campaign）コンポーネントの表示例を以下に示します。

![chlimage_1-123](assets/chlimage_1-123.png)

### 暗号化されたプライマリキー（Campaign） {#encrypted-primary-key-campaign}

このコンポーネントは、Adobe Campaign プロファイルの識別子（それぞれ Adobe Campaign Standard では&#x200B;**メインリソース識別子**、Adobe Campaign 6.1 では&#x200B;**暗号化されたプライマリキー**）を含む URL パラメーター名を定義します。

Adobe Campaign プロファイルデータを表示および変更する各フォームには、暗号化されたプライマリキーコンポーネントを含める&#x200B;**必要があります**。

暗号化されたプライマリキー（Campaign）コンポーネントでは、次の項目を設定できます。

* **タイトルとテキスト — 要素名**

   デフォルトでは、encryptedPK に設定されます。 フォーム上の別のエレメント名と競合する場合にのみ、エレメント名を変更する必要があります。2 つのフォームフィールドが同じエレメント名を持つことはできません。
* **Adobe Campaign - URL パラメーター** EPK 用の URL パラメーターを追加します。例えば、 
**epk**.

暗号化されたプライマリキー（Campaign）コンポーネントの表示例を以下に示します。

![chlimage_1-124](assets/chlimage_1-124.png)

### エラー表示（Campaign） {#error-display-campaign}

このコンポーネントを使用して、バックエンドのエラーを表示できます。このコンポーネントを適切に機能させるには、フォームのエラー処理を「転送」に設定する必要があります。

エラー表示（Campaign）コンポーネントの表示例を以下に示します。

![chlimage_1-125](assets/chlimage_1-125.png)

### 非表示の調整キー（Campaign） {#hidden-reconciliation-key-campaign}

非表示の紐付けキー (Campaign) コンポーネントを使用すると、非表示のフィールドを紐付けキーの一部としてフォームに追加できます。

非表示の調整キー（Campaign）コンポーネントでは、次の項目を設定できます。

* **タイトルとテキスト — 要素名**

   デフォルトは reconcilKey です。 フォーム上の別のエレメント名と競合する場合にのみ、エレメント名を変更する必要があります。2 つのフォームフィールドが同じエレメント名を持つことはできません。
* **Adobe Campaign - マッピング** Adobe Campaign パーソナライゼーションフィールドにマップします。

非表示の調整キー（Campaign）コンポーネントの表示例を以下に示します。

![chlimage_1-126](assets/chlimage_1-126.png)

### 数値フィールド（Campaign） {#numeric-field-campaign}

数値フィールドを使用して、受信者に年齢などの数字を入力させることができます。

[大部分の Adobe Campaign コンポーネントに共通の設定](#settings-common-to-most-components)に加え、次の項目を設定できます。

* **制約 — 制約** ドロップダウン

   次を選択できます。 **なし** または **数値**  — 数値の制約を追加するか、制約を追加しません。 数値を選択した場合、回答ユーザーは数値を入力する必要があります。

* **制約メッセージ**

   また、制約メッセージを追加して、回答を適切に書式設定する方法をユーザーに知らせることもできます。
* **スタイル設定 — 幅**
フィールドの幅を調整するには、 
**+** および **-** アイコンをクリックするか、数値を入力します。

幅が設定された数値フィールド（Campaign）コンポーネントの表示例を以下に示します。

![chlimage_1-127](assets/chlimage_1-127.png)

### オプションフィールド（Campaign） {#option-field-campaign}

このドロップダウンリストを使用して、受信者の性別やステータスなどのオプションを選択できます。

オプションフィールド（Campaign）コンポーネントでは、[大部分の Adobe Campaign コンポーネントに共通の設定](#settings-common-to-most-components)を使用できます。ドロップダウンリストを設定するには、Adobe Campaign のシンボルをクリックまたはタップし、Adobe Campaign パーソナライゼーションフィールドの適切なフィールドに移動して、そのフィールドを選択します。

![chlimage_1-128](assets/chlimage_1-128.png)

オプションフィールド（Campaign）コンポーネントの表示例を以下に示します。

![chlimage_1-129](assets/chlimage_1-129.png)

### 購読チェックリスト（Campaign） {#subscriptions-checklist-campaign}

**購読チェックリスト（Campaign）**&#x200B;コンポーネントを使用して、Adobe Campaign プロファイルに関連付けられた購読を変更できます。

このコンポーネントをフォームに追加すると、利用可能なすべての購読がチェックボックスとして表示されるので、ユーザーに目的の購読を選択させることができます。ユーザーがフォームを送信すると、このコンポーネントは、フォームアクションタイプ (**Adobe Campaign:サービスを購読** または **Adobe Campaign:サービスを購読解除**) をクリックします。

>[!NOTE]
>
>このコンポーネントは、ユーザーがどのサービスを購読または購読解除しているかを確認しません。

購読チェックリスト（Campaign）コンポーネントでは、[大部分の Adobe Campaign コンポーネントに共通の設定](#settings-common-to-most-components)を使用できます（このコンポーネントに利用できる Adobe Campaign 設定はありません）。

購読チェックリスト（Campaign）コンポーネントの表示例を以下に示します。

![chlimage_1-130](assets/chlimage_1-130.png)

### テキストフィールド（Campaign） {#text-field-campaign}

テキストフィールド（Campaign）コンポーネントを使用すると、名、姓、住所、電子メールアドレスなど、文字列タイプのデータを入力できます。

[大部分の Adobe Campaign コンポーネントに共通の設定](#settings-common-to-most-components)に加え、次の項目を設定できます。

* **制約 — 制約** ドロップダウン

   次を選択できます。 **なし、メール、** または **名前（ウムラウトなし）** — 電子メールアドレス、名前、または制約なしの制約を追加します。 「電子メール」を選択した場合は、このフィールドに電子メールアドレスを入力する必要があります。名前を選択した場合は、名前にする必要があります（ウムラウトは使用できません）。

* **制約メッセージ**

   また、制約メッセージを追加して、回答を適切に書式設定する方法をユーザーに知らせることもできます。

* **スタイル設定 — 幅**

   フィールドの幅を調整するには、 **+** および **-** アイコンをクリックするか、数値を入力します。

テキストフィールド（Campaign）コンポーネントの表示例を以下に示します。

![chlimage_1-131](assets/chlimage_1-131.png)
