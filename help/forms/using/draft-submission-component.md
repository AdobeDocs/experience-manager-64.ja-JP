---
title: ドラフトと送信コンポーネント
seo-title: ドラフトと送信コンポーネント
description: ドラフトと送信コンポーネントは、ドラフト状態のフォームと、既に送信済みのフォームを一覧表示します。コンポーネントの外観およびスタイルをカスタマイズできます。
seo-description: ドラフトと送信コンポーネントは、ドラフト状態のフォームと、既に送信済みのフォームを一覧表示します。コンポーネントの外観およびスタイルをカスタマイズできます。
uuid: 351d6df5-0dc3-4f7a-8bdf-0f1c8dd80f34
content-type: reference
products: SG_EXPERIENCEMANAGER/6.4/FORMS
topic-tags: publish
discoiquuid: 219dd379-5bc9-40b0-bdc2-2fb347da29d8
translation-type: tm+mt
source-git-commit: 2abf448e0231eb6fcd9295f498a24e81e1ead11a
workflow-type: tm+mt
source-wordcount: '791'
ht-degree: 60%

---


# ドラフトと送信コンポーネント {#drafts-and-submissions-component}

ドラフトと送信コンポーネントは、ドラフト状態のすべてのフォームと、既に送信済みのフォームを一覧表示します。コンポーネントには、ドラフトのフォームと送信済みのフォームで別々のセクション（タブ）があります。ユーザーに表示されるのは、ユーザーのドラフトフォームと送信済みのフォームのみです。

## コンポーネントの設定 {#configuring-the-component}

ドラフトと送信コンポーネントには、「ドラフト」および「送信」の 2 つのタブがあります。

To enable submission of an adaptive form to appear in the submissions tab, set the **Submit action** to **[Forms Portal Submit Action](/help/forms/using/configuring-submit-actions.md).**または、「Formsポータル送信」オプションを有効にします。 ユーザーがフォームを送信するたびに、フォームが「送信」タブに追加されます。

ドラフト機能は初期設定で有効になっています。ユーザーがアダプティブフォームで「**保存**」をクリックすると、フォームが「ドラフト」タブに追加されます。

次の手順に従って、ドラフトと送信コンポーネントを追加して設定します。

1. コンポーネントブラウザー内の Document Services カテゴリー下にある&#x200B;**ドラフトと送信**&#x200B;コンポーネントをページにドラッグアンドドロップします。
1. Tap the component and then tap ![settings_icon](assets/settings_icon.png) to open the Edit dialog for the component.

   ![ドラフトと送信コンポーネント](assets/drafts-submissions-edit.png)

1. 編集ダイアログで以下の内容を指定し、「**完了**」をタップして設定を保存します。

<table>
 <tbody>
  <tr>
   <th>タブ</th>
   <th>設定</th>
   <th>説明</th>
  </tr>
  <tr>
   <td>一般</td>
   <td>合計結果数</td>
   <td>表示する結果の最大数を指定します。結果数が合計結果数の制限を超えると、「<strong>さらに表示</strong>」というリンクがコンポーネントの下部に表示されます。Clicking <strong>More </strong>shows all the forms. </td>
  </tr>
  <tr>
   <td> </td>
   <td>スタイルタイプ</td>
   <td>コンポーネントのスタイルを指定します。You can specify <strong>No Style</strong>, <strong>Default Style</strong>, or <strong>Custom Style</strong> for listing the forms. 「カスタムスタイル」オプションの場合、「<strong>カスタムスタイルパス</strong>」フィールドでカスタム CSS ファイルのパスを指定できます<strong>。</strong></td>
  </tr>
  <tr>
   <td> </td>
   <td>カスタムスタイルパス</td>
   <td>If you choose <strong>Custom Style</strong> option in the <strong>Style Type</strong> field, use the <strong>Custom Style Path</strong> field to specify the path of custom CSS file. </td>
  </tr>
  <tr>
   <td> </td>
   <td>表示オプション</td>
   <td><p>表示するタブを指定します。「ドラフトフォーム」、「送信済みのフォーム」または「両方」のうちどれを表示するかを選択できます。 </p> <p><strong>注意</strong>：<em><strong>「表示」オプション</strong>で、「<strong>両方</strong>」以外のオプションを選択する場合、「<strong>デフォルトタブ</strong>」フィールドのオプションは使用されません。</em></p> </td>
  </tr>
  <tr>
   <td> </td>
   <td>デフォルトタブ</td>
   <td>フォームポータルページを読み込むときに表示するタブを指定します。<strong>「ドラフトフォーム」タブ</strong>または<strong>「送信済みのフォーム」タブ</strong>のいずれかを選択します。</td>
  </tr>
  <tr>
   <td>ドラフトフォームタブ設定</td>
   <td>カスタムタイトル</td>
   <td>「<strong>ドラフトフォーム</strong>」タブのタイトルを指定します。デフォルト値は<strong>Draft Forms</strong>です。</td>
  </tr>
  <tr>
   <td> </td>
   <td>テンプレートのレイアウト</td>
   <td><p>ドラフトフォームリストに使用するレイアウトを指定します。</p> <p><strong>注意：</strong>デフォルト（非推奨）オプションは使用しないようにしてください。<br /> </p> </td>
  </tr>
  <tr>
   <td>送信済みのフォームタブの設定</td>
   <td>カスタムタイトル </td>
   <td>「<strong>送信済みのフォーム</strong>」タブのタイトルを指定します。デフォルト値は<strong>Submitted Forms</strong>です。</td>
  </tr>
  <tr>
   <td> </td>
   <td>テンプレートのレイアウト</td>
   <td>Specifies the layout to use for Submitted Forms<strong> </strong>list. </td>
  </tr>
 </tbody>
</table>

## ストレージのカスタマイズ {#customizing-the-storage}

「フォームポータル」送信アクションを使用したり、アダプティブフォームでフォームポータルにデータを保存するオプションを有効にしたりすると、フォームデータは AEM リポジトリに保存されます。実稼働環境では、ドラフトまたは送信されたフォームデータを AEM リポジトリに保存しないことをお勧めします。ドラフトと送信済みのフォームデータを保存するには、ドラフトと送信コンポーネントをエンタープライズデータベースなどの安全なストレージと統合する必要があります。

Formsポータルでは、ローカルのAEMリポジトリ、リモートのAEMリポジトリ、またはデータベースにデータを保存できます。 AEM Formsでは、ドラフトと送信のユーザーデータの保存の実装をカスタマイズできます。 デフォルトのメソッドを上書きして、ドラフトと送信データを任意のストレージに保存する方法を指定できます。 例えば、組織に現在実装されているデータストアにデータを保存することができます。

Formsポータルは、ローカルおよびリモートのAEM Forms発行インスタンスのcrx-repositoryにデータを保存するための、初期設定済みのサービス(API)を提供します。 「ドラフトと送信のストレージサービスの [設定](/help/forms/using/configuring-draft-submission-storage.md) 」の記事で説明されているデフォルトの実装を、デフォルトの機能を置き換えるカスタム実装に置き換えることができます。 保護された場所にコンテンツを保存するためにカスタム実装で必要な方法について詳しくは、「ドラフトと送信データサービスの [カスタマイズ](/help/forms/using/custom-draft-submission-data-services.md) 」および「ドラフトと送信コンポーネントの [カスタムストレージ」を参照してください。](/help/forms/using/adding-custom-storage-provider-forms.md)

AEM Formsのドキュメントには、ドラフトと送信コンポーネントとデータベースの統合の [サンプルが含まれています](https://helpx.adobe.com/in/experience-manager/6-4/forms/using/integrate-draft-submission-database.html)。 サンプルの実装を使用して、独自のカスタム実装を開発できます。

## 関連記事

* [フォームポータルコンポーネントの有効化](/help/forms/using/enabling-forms-portal-components.md)
* [フォームポータルページの作成](/help/forms/using/creating-form-portal-page.md)
* [API を使用した Web ページ上のフォームの一覧表示](/help/forms/using/listing-forms-webpage-using-apis.md)
* [ドラフトと送信コンポーネントの使用](/help/forms/using/draft-submission-component.md)
* [ドラフトと送信済みフォームのストレージのカスタマイズ](/help/forms/using/draft-submission-component.md)
* [ドラフトと送信コンポーネントとデータベースの統合のサンプル](/help/forms/using/integrate-draft-submission-database.md)
* [フォームポータルコンポーネントのテンプレートをカスタマイズする](/help/forms/using/customizing-templates-forms-portal-components.md)
* [ポータル上のフォーム発行の概要](/help/forms/using/introduction-publishing-forms.md)
