---
title: タグの管理
seo-title: Administering Tags
description: AEM でタグを管理する方法について説明します。
seo-description: Learn how to administer Tags in AEM.
uuid: 77e1280a-feea-4edd-94b6-4fb825566c42
contentOwner: Chiradeep Majumdar
products: SG_EXPERIENCEMANAGER/6.4/SITES
topic-tags: content
content-type: reference
discoiquuid: 69253ee9-8c28-436b-9331-6fb875f64cba
exl-id: 5c78edf8-148f-41a3-8b11-c1dada34090e
source-git-commit: 2208d23985ebd913b6aa9dee3bf16ce7529a8fa6
workflow-type: tm+mt
source-wordcount: '1755'
ht-degree: 49%

---

# タグの管理{#administering-tags}

タグは、Web サイト内のコンテンツをすばやく簡単に分類するために使用します。検索の結果としてコンテンツをよりすばやく見つけることのできるキーワードまたはラベル（メタデータ）と考えることができます。

Adobe Experience Manager（AEM）では、タグが以下のプロパティとなる場合があります。

* ページのコンテンツノード（[タグの使用](/help/sites-authoring/tags.md)を参照）。

* アセットのメタデータノード（[デジタルアセット用のメタデータの管理](/help/assets/metadata.md)を参照）。

ページやアセットに加え、AEM Communities の機能では次の場所でタグが使用されます。

* ユーザー生成コンテンツ（[UGC のタグ付け](/help/communities/tag-ugc.md)を参照）。

* イネーブルメントリソース（[イネーブルメントソースのタグ付け](/help/communities/functions.md#catalog-function)を参照）。

## タグの機能 {#tag-features}

AEM 内のタグには以下のような機能があります。

* タグは様々な名前空間にグループ分けできます。階層で分類を作成できます。この分類は、AEM 全体で使用されます。
* 新規に作成するタグの主な制限は、特定の名前空間内で一意でなければならないことです。
* タグのタイトルには、タグパスの区切り文字を含めないでください（含めても表示されません）。

   * コロン（:） - 名前空間タグを区切ります。
   * スラッシュ（/） - サブタグを区切ります。

* タグは、作成者およびサイト訪問者が適用できます。すべてのフォームのタグは、作成者に関係なく、ページへの割り当て時および検索時に選択できるようになっています。
* タグの作成と分類の変更は、「tag-administrators」グループのメンバーおよび変更権限を持つメンバーがおこなうことができます。 `/content/cq:tags`.

   * 子タグが含まれるタグはコンテナタグと呼ばれます
   * コンテナタグ以外のタグはリーフタグと呼ばれます
   * タグの名前空間はリーフタグかコンテナタグのいずれかです

* タグを[検索コンポーネント](https://helpx.adobe.com/experience-manager/core-components/using/quick-search.html)で使用すると、コンテンツを簡単に検索できます。
* タグは [Teaser コンポーネント](https://helpx.adobe.com/experience-manager/core-components/using/teaser.html)で使用され、ユーザーのタグクラウドを監視してターゲットのコンテンツを提供できます。
* タグ付けがコンテンツの重要な側面である場合は、次のことに注意します。

   * タグとタグを使用するページを必ずパッケージ化すること
   * [タグの権限](#setting-tag-permissions)に読み取りアクセスを有効にすること

## タグ付けコンソール {#tagging-console}

タグ付けコンソールは、タグと分類の作成および管理に使用します。1 つの目的は、基本的に同じものに関連する多数の類似タグを持つのを避けることです。例えば、page と pages、footwear と shoes などです。

タグは、複数の名前空間にグループ分けして、新規のタグを作成する前に既存のタグの使用状況を確認し、現在参照されているコンテンツからタグを切り離すことなく整理し直すことによって管理します。

タグ付けコンソールにアクセスするには：

* オーサー環境で
* 管理者権限でサインインします
* グローバルナビゲーションから、次の操作をおこないます

   * 選択 **`Tools`**
   * 選択 **`General`**
   * 選択 **`Tagging`**

![managing_tags_usingthetagasadministrationconsole](assets/managing_tags_usingthetagasministrationconsole.png)

### 名前空間の作成 {#creating-a-namespace}

新しい名前空間を作成するには、 **`Create Namespace`** アイコン

名前空間はそれ自体がタグです。サブタグが含まれている必要はありません。ただし、分類の作成を続けるには、 [サブタグの作成](#creating-tags)（リーフタグまたはコンテナタグのいずれか）

![chlimage_1-183](assets/chlimage_1-183.png) ![creating_tags_andnamespaces](assets/creating_tags_andnamespaces.png)

* **タイトル**
*（必須） *名前空間の表示タイトル。

* **名前**
*（オプション） *名前空間の名前。 指定しない場合、有効なノード名が「タイトル」から作成されます。[タグ ID](/help/sites-developing/framework.md#tagid) を参照してください。

* **説明**
*（オプション） *名前空間の説明。

必要な情報を入力したら

* 「**作成**」を選択します

### タグの操作 {#operations-on-tags}

名前空間または他のタグを選択すると、次の操作をおこなえるようになります。

* [プロパティを表示](#viewing-tag-properties)
* [参照](#showing-tag-references)
* [タグを作成](#creating-tags)
* [編集](#editing-tags)
* [移動](#moving-tags)
* [統合](#merging-tags)
* [公開](#publishing-tags)
* [非公開](#unpublishing-tags)
* [削除](#deleting-tags)

![chlimage_1-184](assets/chlimage_1-184.png)

ブラウザーウィンドウが全てのアイコンを表示するのに十分な広さでない場合、右端のアイコンは、 **`... More`** アイコン。選択すると、非表示の操作アイコンのドロップダウンリストが表示されます。

![chlimage_1-185](assets/chlimage_1-185.png)

### 名前空間タグの選択 {#selecting-a-namespace-tag}

最初に選択したときに、名前空間にタグが含まれていない場合は右にプロパティが表示され、含まれている場合は子タグが表示されます。選択した各タグには、そのタグに含まれるタグ、または子タグがない場合はそのプロパティが表示されます。

操作対象のタグを選択したり、複数選択をおこなう場合は、タイトルの横にあるアイコンを選択するだけです。タイトルを選択すると、プロパティのみが表示されるか、タグを開いてその内容を表示します。

![chlimage_1-186](assets/chlimage_1-186.png) ![chlimage_1-187](assets/chlimage_1-187.png)

### タグプロパティの表示 {#viewing-tag-properties}

![chlimage_1-188](assets/chlimage_1-188.png)

名前空間または他のタグが選択されたときに、 **`View Properties`** アイコンを使用すると、 `name`、最後の編集の時間、参照数。 公開された場合は、最後に公開された日時と公開者の ID が表示されます。 この情報は、タグ列の左側の列に表示されます。

![chlimage_1-189](assets/chlimage_1-189.png)

### タグ参照の表示 {#showing-tag-references}

![chlimage_1-190](assets/chlimage_1-190.png)

名前空間または他のタグが選択されたときに、**`References`**アイコンは、タグが適用されたコンテンツを識別します。

まず、適用されているタグの数が表示されます。

![chlimage_1-191](assets/chlimage_1-191.png)

数の右にある矢印を選択すると、参照名がリストされます。

参照の上にカーソルを重ねると、その参照へのパスがツールチップとして表示されます。

![chlimage_1-192](assets/chlimage_1-192.png)

### タグの作成 {#creating-tags}

![chlimage_1-193](assets/chlimage_1-193.png)

（タイトルの横にあるアイコンを選択して）名前空間または他のタグが選択されている場合、現在のタグに対して子タグを作成するには、 **`Create Tag`** アイコン

![chlimage_1-194](assets/chlimage_1-194.png)

* **タイトル**
*（必須） *タグの表示タイトル。

* **名前**
*（オプション） *タグの名前。 指定しない場合、有効なノード名が「タイトル」から作成されます。[タグ ID](/help/sites-developing/framework.md#tagid) を参照してください。

* **説明**
*（オプション） *タグの説明。

必要な情報を入力したら

* 「**作成**」を選択します

### タグの編集 {#editing-tags}

![chlimage_1-195](assets/chlimage_1-195.png)

名前空間または他のタグが選択されている場合、「タイトル」、「説明」の変更や、タイトルのローカライゼーションの指定は、「**」`Edit`**icon.

編集が完了したら、「**保存**」を選択します。

言語の翻訳の追加について詳しくは、 [異なる言語でのタグの管理](#managing-tags-in-different-languages).

![chlimage_1-196](assets/chlimage_1-196.png)

### タグの移動 {#moving-tags}

![chlimage_1-197](assets/chlimage_1-197.png)

名前空間または他のタグが選択されたときに、 **`Move`** アイコンを使用すると、タグ管理者および開発者は、タグを新しい場所に移動したり、タグの名前を変更したりして、分類をクリーンアップできます。 選択したタグがコンテナタグの場合、タグを移動すると、すべての子タグも移動されます。

>[!NOTE]
>
>作成者には、 [編集](#editing-tags) タグの `title`（タグの移動や名前の変更はしない）。

![chlimage_1-198](assets/chlimage_1-198.png)

* **パス**

   *（読み取り専用）* 選択したタグの現在のパス。

* **移動先** タグの移動先の新しいパスを参照します。

* **名前をに変更**
最初に現在の 
`name`」と入力します。 新しい `name`を入力できます。

* 「**保存**」を選択します

### タグの統合 {#merging-tags}

![chlimage_1-199](assets/chlimage_1-199.png)

タグの統合は、分類が重複する場合に使用できます。タグ A がタグ B に統合されると、タグ A が付けられたすべてのページにタグ B が付けられ、作成者はタグ A を使用できなくなります。

名前空間または他のタグが選択されたときに、**`Merge`**アイコンをクリックすると、パネルが開き、統合先のパスが選択されます。

![chlimage_1-200](assets/chlimage_1-200.png)

* **パス**

   *（読み取り専用）* 別のタグに結合するために選択したタグのパス。

* **統合対象**&#x200B;統合先のタグのパスを参照して選択します。

>[!NOTE]
>
>結合後、最初に選択した**パス**は（事実上）存在しなくなります。
>
>参照先のタグが移動または統合されても、タグは物理的には削除されないので、参照を維持することは可能です。

### タグの公開 {#publishing-tags}

![chlimage_1-201](assets/chlimage_1-201.png)

名前空間または他のタグが選択されたときに、**`Publish`**アイコン：パブリッシュ環境でタグをアクティベートします。 ページコンテンツと同様、コンテナタグかどうかに関係なく、選択したタグのみが公開されます。

分類（名前空間とサブタグ）を公開するベストプラクティスとして、名前空間の[パッケージ](/help/sites-administering/package-manager.md)を作成します（[分類のルートノード](/help/sites-developing/framework.md#taxonomy-root-node)を参照）。必ず [権限の適用](#setting-tag-permissions) を名前空間に追加してから、パッケージを作成します。

### タグを非公開にする {#unpublishing-tags}

![chlimage_1-202](assets/chlimage_1-202.png)

名前空間または他のタグが選択されたときに、**`Unpublish`**アイコンをクリックすると、オーサー環境でタグが非アクティブ化され、パブリッシュ環境から削除されます。 次に類似 `Delete`選択したタグがコンテナタグの場合、そのすべての子タグはオーサー環境で非アクティブ化され、パブリッシュ環境から削除されます。

### タグの削除 {#deleting-tags}

![chlimage_1-203](assets/chlimage_1-203.png)

名前空間または他のタグが選択されたときに、**`Delete`**icon は、オーサー環境からタグを完全に削除します。 タグが公開された場合は、パブリッシュ環境からも削除されます。 選択したタグがコンテナタグの場合、その子タグもすべて削除されます。

## タグの権限の設定 {#setting-tag-permissions}

タグ権限は、 [&#39;secure （デフォルト）&#39;](/help/sites-administering/production-ready.md);タグに対して明示的に読み取り権限を許可する必要があるパブリッシュ環境のベストプラクティスです。 基本的には、オーサー環境で権限が設定された後にタグ名前空間のパッケージを作成し、そのパッケージをすべてのパブリッシュインスタンスにインストールすることで実行します。

* オーサーインスタンスで

   * 管理者権限でサインインします
   * [セキュリティコンソール](/help/sites-administering/security.md#accessing-user-administration-with-the-security-console)にアクセスします

      * 例えば、http://localhost:4502/useradmin に移動します
   * 左側のウィンドウで、[読み取り権限](/help/sites-administering/security.md#permissions)を付与するグループ（またはユーザー）を選択します
   * 右側のウィンドウで、タグ名前空間への**パス**を見つけます。

      * 例： `/content/cq:tags/mycommunity`
   * を選択します。 `checkbox`内 **読み取り** 列
   * 「**Save**」を選択します。



![chlimage_1-204](assets/chlimage_1-204.png)

* すべてのパブリッシュインスタンスが同じ権限となるようにします

   * 1 つのアプローチは、オーサー環境で名前空間の[パッケージを作成](/help/sites-administering/package-manager.md#package-manager)することです

      * オン `Advanced` タブ、の `AC Handling` 選択 `Overwrite`
   * パッケージをレプリケートします

      * 選択 `Replicate` パッケージマネージャーから


## 他の言語でのタグの管理 {#managing-tags-in-different-languages}

この `title`タグのプロパティは、複数の言語に翻訳できます。 翻訳が完了したら、適切なタグ `title`は、ユーザーの言語またはページの言語に従って表示されます。

### 複数言語でのタグタイトルの定義 {#defining-tag-titles-in-multiple-languages}

以下では、 `title`タグの **動物** 英語からドイツ語、フランス語へ。

まず、 **フォトグラフィー** 名前空間と選択**`Edit`**icon ( [タグの編集](#editing-tags) を参照 )。

タグを編集パネルで、タグのタイトルを翻訳する言語を選択できます。

各言語を選択すると、テキスト入力ボックスが表示され、翻訳されたタイトルを入力できます。

すべての翻訳を入力したら、「**保存**」を選択して編集モードを終了します。

![chlimage_1-205](assets/chlimage_1-205.png)

一般的に、タグに選択した言語はページの言語から取得されます。[`tag` ウィジェットが他のケース（フォームやダイアログなど）で使用されている場合、タグの言語はコンテキストによって変わります。](/help/sites-developing/building.md#tagging-on-the-client-side)

タグ付けコンソールでは、ページの言語設定の代わりに、ユーザーの言語設定が使用されます。タグ付けコンソールで、ユーザープロパティで言語をフランス語に設定しているユーザーに対しては、「Animals」タグに対して「Animaux」が表示されます。

ダイアログに新しい言語を追加するには、 [タグを編集ダイアログへの新しい言語の追加](/help/sites-developing/building.md#adding-a-new-language-to-the-edit-tag-dialog).

>[!NOTE]
>
>標準ページコンポーネント内のタグクラウドとメタキーワードは、ローカライズされたタグを使用します `titles`ページ言語に基づく（可能な場合）

## リソース {#resources}

* [開発者向けタグ付け](/help/sites-developing/tags.md)

   タグ付けフレームワークに関する情報と、カスタムアプリケーションでタグを拡張および含める方法について説明します。

* [クラシック UI のタグ付けコンソール](/help/sites-administering/classic-console.md)
