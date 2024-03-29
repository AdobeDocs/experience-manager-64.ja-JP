---
title: ページプロパティの編集
seo-title: Editing Page Properties
description: ページのプロパティは、ページの特性に応じて異なる場合があります。 例えば、一部のページがライブコピーに接続されている場合と、接続されていない場合があり、ライブコピー情報は必要に応じて使用できます。
seo-description: Properties of a page can vary depending on the nature of the page. For example some pages might be connected to a live copy while others are not and the live copy information will be available as appropriate.
uuid: 63d37d1b-52da-489d-b02b-e8b3d17571d1
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.4/SITES
topic-tags: page-authoring
content-type: reference
discoiquuid: 23768c73-ac64-4727-8313-160c8c131b05
exl-id: 6969dc5e-f7fa-495e-8ddf-8123ca2bc9a6
source-git-commit: c5b816d74c6f02f85476d16868844f39b4c47996
workflow-type: tm+mt
source-wordcount: '799'
ht-degree: 26%

---

# ページプロパティの編集 {#editing-page-properties}

>[!CAUTION]
>
>AEM 6.4 の拡張サポートは終了し、このドキュメントは更新されなくなりました。 詳細は、 [技術サポート期間](https://helpx.adobe.com/jp/support/programs/eol-matrix.html). サポートされているバージョンを見つける [ここ](https://experienceleague.adobe.com/docs/?lang=ja).

ページに必要なプロパティを定義できます。これらは、ページの特性に応じて異なる場合があります。 例えば、一部のページがライブコピーに接続されている場合と、接続されていない場合があり、ライブコピー情報は必要に応じて使用できます。

## ページプロパティ {#page-properties}

プロパティは、次の複数のタブに分散しています。

### 基本 {#basic}

* **タイトル**

   ページのタイトルは様々な場所に表示されます。 例えば、 **Web サイト** タブリストと **サイト** カード/リスト表示。

   このフィールドは必須です。

* **タグ**

   ここでは、選択ボックスのリストを更新して、ページのタグの追加や削除をおこなうことができます。

   * タグを選択すると、選択ボックスの下に表示されます。 x を使用して、このリストからタグを削除できます。
   * 空の選択ボックスに名前を入力して、新しいタグを入力できます。

      Enter キーを押すと、新しいタグが実際に作成されます。 新しいタグがボックスに表示され、右側に小さな星が付き、新しいタグであることを示します。

   * ドロップダウン機能を使用して、既存のタグから選択できます。
   * 選択ボックスのタグエントリにマウスを合わせると、x が表示されます。これを使用して、このページのそのタグを削除できます。

* **ナビゲーション内で非表示にする**

   ページナビゲーションでページを表示するか非表示にするかを示す切り替えスイッチ。

* **ページタイトル**

   ページで使用するタイトル。

* **ナビゲーションタイトル**

   ナビゲーション内で使用するタイトルを別途指定できます（より簡潔にする場合など）。 空の場合、 **タイトル** が使用されます。

* **サブタイトル**

   ページで使用するサブタイトル。

* **説明**

   ページの説明、目的、または追加するその他の詳細。

* **オンタイム**

   公開されたページがアクティベートされる日時。 公開されると、このページは指定された時間まで休止状態に保たれます。

   即座に公開するページ（通常のシナリオ）の場合、これらのフィールドは空のままにします。

* **オフタイム**

   公開されたページのアクティベートを解除する時間。

   即座に公開するページでは、これらのフィールドを空のままにします。

* **バニティ URL**

   このページのバニティー URL を入力できます。 これにより、より短く、より表現力のある URL を指定できます。

   例えば、バニティ URL を web サイト h`ttp://example.com,` のパス /`v1.0/startpage` で特定されるページへの w`elcome` に設定した場合、h`ttp://example.com/welcome` は h`ttp://example.com/content/v1.0/startpage` のバニティ URL になります。

   >[!CAUTION]
   >
   >バニティ URL:
   >
   >* は一意である必要があるので、別のページで値がまだ使用されていないように注意する必要があります。
   >* 正規表現パターンはサポートしていません。


* **バニティー URL をリダイレクト**

   ページでバニティー URL を使用するかどうかを示します。

### 詳細 {#advanced}

* **言語**

   ページの言語。

* **リダイレクト**

   このページが自動的にリダイレクトするページを指定します。

* **デザイン**

   次を指定： [デザイン](/help/sites-developing/designer.md) をこのページに使用します。

* **エイリアス**

   このページで使用するエイリアスを指定します。

* **閉じられたユーザーグループを有効にする**

   の使用を有効（または無効）にします [閉じられたユーザーグループ](/help/sites-administering/cug.md) (CUG)。

* **ログインページ**

   ログインに使用するページ。

* **許可されたグループ**

   CUG へのログイン資格のあるグループ。

* **領域**

   CUG の領域名。

* **設定を書き出し**

   書き出し設定を指定します。

### サムネール {#thumbnail}

* **ページサムネール**

   ページサムネール画像が表示されます。以下の操作を実行できます。

   * **プレビューを生成**

      サムネールとして使用するページのプレビューを生成します。

   * **画像をアップロード**

      サムネールとして使用する画像をアップロードします。

### Cloud Services {#cloud-services}

* **Cloud Services**

   次のプロパティを定義： [クラウドサービス](/help/sites-developing/extending-cloud-config.md).

### パーソナライズ機能 {#personalization}

* **パーソナライズ機能**

   [ブランドを選択してターゲット設定の範囲を指定](/help/sites-classic-ui-authoring/classic-personalization-campaigns.md)します。

### 権限 {#permissions}

* **権限** （タッチ操作向け UI）

   [有効な権限を表示し、新しい権限を追加](/help/sites-administering/user-group-ac-admin.md)します。

### ブループリント {#blueprint}

* **ブループリント**

   内のブループリントページのプロパティを定義する [マルチサイト管理](/help/sites-administering/msm.md). 変更がライブコピーに反映される状況を制御します。

### ライブコピー {#live-copy}

* **ライブコピー**

   内でのライブコピーページのプロパティを定義します。 [マルチサイト管理](/help/sites-administering/msm.md). 変更をブループリントから反映する状況を制御します。

### サイト構造 {#site-structure}

* **サインアップページ**、**オフラインページ**&#x200B;など、サイト全体にわたる機能を提供するページへのリンクを指定します。

## ページプロパティの編集  {#editing-page-properties-2}

### 特定のページのページプロパティの編集 {#editing-page-properties-for-a-specific-page}

ページプロパティは、ページの様々なプロパティ（タイトルなど）を定義し、Web サイトに表示される際に使用します。

1. 編集するページを開きます。

1. サイドキックで「**ページ**」タブを開き、「**ページプロパティ**」を選択します。

   複数のタブを含むダイアログが開きます。

1. 必要な変更を加えたら、「**OK**」をクリックして保存します。
