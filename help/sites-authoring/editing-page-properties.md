---
title: ページプロパティの編集
seo-title: Editing Page Properties
description: ページに必要なプロパティを定義する
seo-description: Define the required properties for a page
uuid: c0386cd6-ca01-4741-b8c8-36edb66e50ef
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.4/SITES
topic-tags: page-authoring
content-type: reference
discoiquuid: 8e85ea7f-80ea-43b6-a67c-366852ef86ce
exl-id: b0e579a4-f5bd-4a55-a003-0496224bc940
source-git-commit: c5b816d74c6f02f85476d16868844f39b4c47996
workflow-type: tm+mt
source-wordcount: '1825'
ht-degree: 51%

---

# ページプロパティの編集 {#editing-page-properties}

>[!CAUTION]
>
>AEM 6.4 の拡張サポートは終了し、このドキュメントは更新されなくなりました。 詳細は、 [技術サポート期間](https://helpx.adobe.com/jp/support/programs/eol-matrix.html). サポートされているバージョンを見つける [ここ](https://experienceleague.adobe.com/docs/?lang=ja).

ページに必要なプロパティを定義できます。これらは、ページの特性に応じて異なる場合があります。 例えば、一部のページがライブコピーに接続されている場合と、接続されていない場合があり、ライブコピー情報は必要に応じて使用できます。

## ページプロパティ {#page-properties}

プロパティは次のタブに分散しています。

### 基本 {#basic}

* **タイトル**

   ページのタイトルは様々な場所に表示されます。 例えば、 **Web サイト** タブリストと **サイト** カード/リスト表示。

   このフィールドは必須です。

* **タグ**

   ここでは、選択ボックスのリストを更新して、ページのタグの追加や削除をおこなうことができます。

   * タグを選択すると、選択ボックスの下に表示されます。 x を使用して、このリストからタグを削除できます。
   * 空の選択ボックスに名前を入力して、新しいタグを入力できます。

      * Enter キーを押すと、新しいタグが作成されます。
      * 新しいタグが右側に小さな星付きで表示され、新しいタグであることを示します。
   * ドロップダウン機能を使用して、既存のタグから選択できます。
   * 選択ボックスのタグエントリにマウスを移動すると、x が表示されます。この x は、このページのそのタグを削除するのに使用できます。

   タグについて詳しくは、 [タグの使用](/help/sites-authoring/tags.md).

* **ナビゲーション内で非表示にする**

   使用されるサイトでページがページのナビゲーションに表示されるかどうかを示します。

* **ブランディング**

   各ページタイトルにブランド見出しを追加して、ページ間で一貫したブランドアイデンティティを適用します。この機能では、[コアコンポーネント](https://experienceleague.adobe.com/docs/?lang=jaexperience-manager-core-components/using/introduction.html)のリリース 2.14.0 以降に含まれているページコンポーネントを使用する必要があります。

   * **オーバーライド** - このページにブランド見出しを定義する場合にオンにします。
      * 子ページにも&#x200B;**オーバーライド**&#x200B;値が設定されている場合を除き、値はすべての子ページに継承されます。
   * **値をオーバーライド** - ページタイトルに追加するブランド見出しのテキストです。
      * この値は、「Cycling Tuscany | Always ready for the WKND」のように、ページタイトルの末尾にパイプ文字に続けて追加されます。

* **ページタイトル**

   ページで使用するタイトル。 通常、タイトルコンポーネントで使用されます。 空の場合、 **タイトル** が使用されます。

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

   これらのフィールドを空のままにしておくと、すぐに操作できます。

* **バニティ URL**

   このページのバニティー URL を入力できます。バニティー URL を入力すると、短い URL や表現上の URL を指定できます。

   例えば、バニティ URL を web サイト h`ttp://example.com,` のパス /`v1.0/startpage` で特定されるページへの w`elcome` に設定した場合、h`ttp://example.com/welcome` は h`ttp://example.com/content/v1.0/startpage` のバニティ URL になります。

   >[!CAUTION]
   >
   >バニティ URL:
   >
   >* 他のページで値がまだ使用されていないように、一意である必要があります。
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

   * 例えば、ページ `private` に `/content/wknd/us/en/magazine/members-only` というエイリアスを定義した場合、このページには `/content/wknd/us/en/magazine/private` を介してもアクセスできます。。
   * エイリアスを作成すると、ページノードに `sling:alias` プロパティが設定されます。これは、リポジトリパスではなく、リソースにのみ影響を与えます。
   * エディターでエイリアスによってアクセスされたページは公開できません。エディターの[「公開」オプション](/help/sites-authoring/publishing-pages.md)は、実際のパスを介してアクセスしたページでのみ使用できます。
   * 詳しくは、 [「SEO と URL 管理のベストプラクティス」のページ名のローカライズ](/help/managing/seo-and-url-management.md#localized-page-names)

* **許可されたテンプレート**

   [使用可能なテンプレートのリストを定義します](/help/sites-authoring/templates.md#enabling-and-allowing-a-template-template-author) このサブブランチ内に

* **認証要件**

   ページにアクセスするための認証の使用を有効（または無効）にします。

   認証が必要な場合は、指定されたログオンページと共にここで設定できます。 ページにアクセスできるユーザーグループは、「**[権限](/help/sites-authoring/editing-page-properties.md#permissions)**」タブで定義します。

   >[!CAUTION]
   >
   >「**[権限](/help/sites-authoring/editing-page-properties.md#permissions)**」タブでは、`granite:AuthenticationRequired` mixin が存在することにより、CUG 設定を編集できます。cq:cugEnabled プロパティの存在に基づいて、非推奨の CUG 設定を使用してページ権限が設定されている場合、次の場所に警告メッセージが表示されます。 **認証要件** また、オプションは編集できず、 [権限](/help/sites-authoring/editing-page-properties.md#permissions) 編集可能です。
   >
   >
   >そのような場合は、CUG 権限を[クラシック UI](/help/sites-classic-ui-authoring/classic-page-author-edit-page-properties.md) で編集する必要があります。

* **ログインページ**

   ログインに使用するページ。

* **設定を書き出し**

   書き出し設定を指定します。

### サムネール {#thumbnail}

1. **ページサムネール**

   ページサムネール画像が表示されます。以下の操作を実行できます。

   * **プレビューを生成**

      サムネールとして使用するページのプレビューを生成します。

   * **画像をアップロード**

      サムネールとして使用する画像をアップロードします。

### ソーシャルメディア {#social-media}

* **ソーシャルメディア共有**

   ページで使用可能な共有オプションを定義します。 使用可能なオプションを [コアコンポーネントの共有](https://helpx.adobe.com/jp/experience-manager/core-components/using/sharing.html).

   * **facebookのユーザー共有を有効にする**
   * **pinterestのユーザー共有を有効にする**
   * **優先 XF バリエーション**&#x200B;ページのメタデータの生成に使用されるエクスペリエンスフラグメントのバリエーションを定義します

### Cloud Services {#cloud-services}

* **Cloud Services**

   次のプロパティを定義： [クラウドサービス](/help/sites-developing/extending-cloud-config.md).

### パーソナライズ機能 {#personalization}

* **パーソナライズ機能**

   [ブランドを選択してターゲット設定の範囲を指定](/help/sites-authoring/personalization.md)します。

### 権限 {#permissions}

* **権限**

   このタブでは、次の操作を実行できます。

   * [権限を追加](/help/sites-administering/user-group-ac-admin.md)
   * [閉じられたユーザーグループを編集](/help/sites-administering/cug.md#applying-your-closed-user-group-to-content-pages)
   * [有効な権限](/help/sites-administering/user-group-ac-admin.md)を表示

   >[!CAUTION]
   >
   >「**権限**」タブでは、`granite:AuthenticationRequired` mixin が存在することにより、CUG 設定を編集できます。`cq:cugEnabled` プロパティが存在することにより、廃止された CUG 設定を使用してページの権限が設定された場合、警告メッセージが表示され、CUG 権限は編集できず、「[詳細](/help/sites-authoring/editing-page-properties.md#advanced)」タブの認証要件も編集できません。
   >
   >
   >そのような場合は、CUG 権限を[クラシック UI](/help/sites-classic-ui-authoring/classic-page-author-edit-page-properties.md) で編集する必要があります。

   >[!NOTE]
   >
   >「権限」タブでは、空の CUG グループを作成できません。これは、すべてのユーザーに対するアクセスを拒否する簡単な方法として役立ちます。 これをおこなうには、CRX Explorer を使用する必要があります。 詳しくは、[ユーザー、グループおよびアクセス権限の管理](/help/sites-administering/user-group-ac-admin.md)のドキュメントを参照してください。

### ブループリント {#blueprint}

* **ブループリント**

   内のブループリントページのプロパティを定義する [マルチサイト管理](/help/sites-administering/msm.md). 変更がライブコピーに反映される状況を制御します。

### ライブコピー {#live-copy}

* **ライブコピー**

   内でのライブコピーページのプロパティを定義します。 [マルチサイト管理](/help/sites-administering/msm.md). 変更をブループリントから反映する状況を制御します。

### サイト構造 {#site-structure}

* **サインアップページ**、**オフラインページ**&#x200B;など、サイト全体にわたる機能を提供するページへのリンクを指定します。

## ページプロパティの編集  {#editing-page-properties-2}

次のように、ページプロパティを定義できます。

* **サイト**&#x200B;コンソールから：

   * [新しいページを作成](/help/sites-authoring/managing-pages.md#creating-a-new-page)します（プロパティのサブセット）
   * 「**プロパティ**」をクリックまたはタップします

      * 単一ページの場合
      * 複数のページの場合（プロパティのサブセットのみが一括編集に使用できます）

* ページエディターから、次の操作を行います。

   * 「**ページ情報**」（その後、「**プロパティを開く**」）を使用します

### サイトコンソールから - 単一のページ {#from-the-sites-console-single-page}

「**プロパティ**」をクリックまたはタップして、ページのプロパティを定義します。

1. **サイト**&#x200B;コンソールを使用して、プロパティを表示および編集するページの場所に移動します。

1. 次のいずれかを使用して、目的のページで「**プロパティ**」オプションを選択します。

   * [クイックアクション](/help/sites-authoring/basic-handling.md#quick-actions)
   * [選択モード](/help/sites-authoring/basic-handling.md#viewing-and-selecting-resources)

   ページのプロパティが該当するタブに表示されます。

1. 必要に応じてプロパティを表示または編集します。

1. その後、「**保存**」を使用して更新内容を保存し、「**閉じる**」を使用してコンソールに戻ります。

### ページの編集中 {#when-editing-a-page}

ページの編集中は、**ページ情報**&#x200B;を使用してページプロパティを定義できます。

1. プロパティを編集するページを開きます。

1. **ページ情報**&#x200B;アイコンを選択して選択メニューを開きます。

   ![screen_shot_2018-03-22at095740](assets/screen_shot_2018-03-22at095740.png)

1. 「**プロパティを開く**」を選択すると、プロパティを編集するためのダイアログが開きます。プロパティは適切なタブに分類されています。ツールバーの右側にある次のボタンも使用できます。

   * **キャンセル**
   * **保存して閉じる**

1. 「**保存して閉じる**」ボタンを使用して、変更を保存します。

### サイトコンソールから - 複数のページ {#from-the-sites-console-multiple-pages}

**Sites** コンソールから、複数のページを選択し、「**プロパティを表示**」を使用してページのプロパティを表示および編集することができます。これは、ページプロパティの一括編集と呼ばれます。

>[!NOTE]
>
>また、アセットではプロパティの一括編集も可能です。 これは非常に似ていますが、いくつかの点で異なります。 詳しくは、 [複数のアセットのプロパティの編集](/help/assets/managing-multiple-assets.md) 」を参照してください。
>
>また、 [バルクエディター](/help/sites-administering/bulk-editor.md):GQL(Google Query Language) を使用して複数のページからコンテンツを検索し、元のページに対する変更を保存する前に Bulk Editor で直接コンテンツを編集できます。

次のような様々な方法で、一括編集用に複数のページを選択できます。

* を参照して **サイト** コンソール
* 使用後 **検索** 一連のページを見つけるには

![screen_shot_2018-03-22at100039](assets/screen_shot_2018-03-22at100039.png)

ページを選択して **プロパティ** 」オプションを選択すると、一括プロパティが表示されます。

![screen_shot_2018-03-22at100114](assets/screen_shot_2018-03-22at100114.png)

次の条件を満たすページの一括編集のみ可能です。

* 同じリソースタイプを共有
* ライブコピーに含まれていません

   * いずれかのページがライブコピー中である場合、プロパティを開くときにメッセージが表示されます。

一括編集を開始すると、次の操作を行うことができます。

* **表示**

   複数のページのページプロパティを表示すると、次の内容が表示されます。

   * 影響を受けたページのリスト

      * 必要に応じて選択/選択解除できます
   * タブ

      * 単一ページのプロパティを表示する場合と同様に、プロパティはタブの下に並べられます。
   * プロパティのサブセット

      * 選択したすべてのページで使用できるプロパティ（および一括編集で使用できると明示的に定義されたプロパティ）が表示されます。
      * 選択するページを 1 つに減らすと、すべてのプロパティが表示されます。
   * 共通の値を持つ共通のプロパティ

      * 表示モードで表示されるのは、共通の値を持つプロパティのみです。
      * フィールドが複数値（タグなど）の場合は、すべての値が共通の場合に限り、値が表示されます&#x200B;*。*&#x200B;一部の値のみが共通の場合は、それらの値は編集時にのみ表示されます。

   一般的な値を含むプロパティがない場合は、メッセージが表示されます。

* **編集**

   複数ページのページプロパティを編集する場合：

   * 利用可能なフィールドの値を更新できます。

      * 新しい値は、「**完了**」を選択したときに、選択したすべてのページに適用されます。
      * フィールドが複数値（タグなど）の場合は、新しい値を追加するか、共通の値を削除できます。
   * 共通のフィールドに、ページによって異なる値が設定されている場合、それらのフィールドは特別な値（「`<Mixed Entries>`」というテキストなど）で示されます。そのようなフィールドを編集する際は、データが失われないように、慎重に行う必要があります。


>[!NOTE]
>
>ページコンポーネントを設定して、一括編集が可能なフィールドを指定できます。詳しくは、 [ページプロパティの一括編集用のページの設定](/help/sites-developing/bulk-editing.md).
