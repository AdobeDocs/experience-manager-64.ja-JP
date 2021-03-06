---
title: イネーブルメントリソースのコンソール
seo-title: Enablement Resources Console
description: リソースコンソールは、イネーブルメントマネージャーが、イネーブルメントコミュニティサイトのリソースの作成、管理、メンバーへの割り当てをおこなう場所です
seo-description: The Resources console is where Enablement Managers create, manage, and assign resources to members of an enablement community site
uuid: 52445b39-c339-4b39-8004-eb36de99bced
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.4/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: 1ef15e76-fe7c-4ced-a20d-c0a9385e3ee4
role: Admin
exl-id: 67d80ec9-64c9-43a5-8cb1-9da819471797
source-git-commit: 3c050c33a384d586d74bd641f7622989dc1d6b22
workflow-type: tm+mt
source-wordcount: '2957'
ht-degree: 50%

---

# イネーブルメントリソースのコンソール {#enablement-resources-console}

AEM Communities のリソースコンソールは、[イネーブルメントマネージャー](users.md)が、イネーブルメントコミュニティサイトのリソースの作成、管理、メンバーへの割り当てをおこなう場所です。

## 要件 {#requirements}

コミュニティサイトにイネーブルメントリソースを追加する前に、以下のものを含め、AEM インスタンスを適切に設定しておく必要があります。

* SCORM
* FFmpeg

詳しくは、 [有効化の設定](enablement.md).

>[!CAUTION]
>
>コミュニティサイトの作成後に SCORM をインストールした場合は、SCORM をインストールする前に存在していたイネーブルメントリソースを作成し直す必要があります。

>[!NOTE]
>
>のリリースに伴い [AEM 6.3](deploy-communities.md#latestfeaturepack) および同等のコミュニティの機能パック [AEM 6.2 FP3](deploy-communities.md#latestfeaturepack) および [AEM 6.1 FP7](https://docs.adobe.com/content/docs/en/aem/6-1/deploy/communities.html#Latest機能パック ) を使用する場合、イネーブルメント機能に [MySQL データベース](mysql.md).

## 用語 {#terminology}

### リソース {#resource}

リソースは[イネーブルメントコミュニティ](overview.md#enablement-community)に欠かせないものです。メンバーに割り当てられた資料で、メンバーのスキルを向上させることができます。

リソースの特性：

* タイプ
   * 画像 (JPG、PNG、GIF、BMP)
   * ビデオ (MP4)
   * Flash(SWF)
   * Document (PDF)
   * クイズ (SCORM)
* 1 つ以上の学習パスから参照できます

### 学習パス {#learning-path}

学習パスは、メンバーへの割り当てを容易にするために、複数のイネーブルメントリソースを論理的にグループ化したものです。

### メンバーグループ {#members-group}

コミュニティサイトの作成時にサイトの URL に指定した名前が、様々な役割にふさわしい権限を持つ[サイト固有のユーザーグループ](users.md)を作成する際に使用されます。これらの自動的に作成されたグループの前には、「 `Community *<site-name>*`.

そのようなユーザーグループの 1 つが、 `Community *<site-name>* Members` グループ：パブリッシュ環境の登録ユーザーをコミュニティメンバーとして識別します。 チュートリアルを参照 [AEM Communities使用の手引き](getting-started-enablement.md) 例：

の場合 [コミュニティ](overview.md#egagementcommunity)を使用する場合、サイト訪問者が自己登録またはソーシャルログインを使用できるようにすると、その時点で訪問者がメンバーグループに自動的に追加されます。

[イネーブルメントコミュニティ](overview.md#enablement-community)の場合は、サイトを非公開にすることを推奨します。非公開のサイトでは、管理者がユーザーをメンバーグループに追加する必要があります。

## コミュニティサイトのイネーブルメントリソースへのアクセス {#accessing-a-community-site-s-enablement-resources}

### コミュニティリソースへの移動 {#navigate-to-communities-resources}

オーサー環境でリソースコンソールに移動するには、

* グローバルナビゲーションから： **[!UICONTROL ナビゲーション/コミュニティ/リソース]**

![chlimage_1-163](assets/chlimage_1-163.png)

### コミュニティサイトの選択 {#select-a-community-site}

コミュニティリソースコンソールには、すべてのコミュニティサイトが表示されます。

リソースコンソールで特定のコミュニティサイトを選択すると、そのサイトに対してイネーブルメントリソースが作成されます。

特定のコミュニティサイトを選択した後は、既存のイネーブルメントリソースや学習パスにアクセスして管理や変更をおこなったり、新しいイネーブルメントリソースや学習パスを作成したりできます。

![chlimage_1-164](assets/chlimage_1-164.png)

#### 検索 {#search-features}

![chlimage_1-165](assets/chlimage_1-165.png)

イネーブルメントリソースまたは学習パスを検索するには、サイドパネル切り替えアイコンを選択します。選択すると、コンソールの左側に検索パネルが開き、検索語句を入力できるテキストボックスが表示されます。

![chlimage_1-166](assets/chlimage_1-166.png)

#### 選択モード {#selection-mode}

複数のイネーブルメントリソースを選択するには、まず 1 つ目のカードにカーソルを合わせてチェックマークアイコンをクリックし、選択状態にします。選択した他のカードを選択すると、選択グループに追加されます。 2 回目を選択すると、カードの選択が解除されます。

![chlimage_1-167](assets/chlimage_1-167.png)

## リソースの作成 {#create-a-resource}

![chlimage_1-168](assets/chlimage_1-168.png)

コミュニティサイトに新しいイネーブルメントリソースを追加するには、

* を選択します。 `Create` アイコン
* 表示されるサブメニューから、「 」を選択します。 `Resource`

すると、以下の設定をおこなう段階的なプロセスが開始します。

* リソースの説明（名前、カード画像、テキスト）
* リソースコンテンツの選択
* リソースのカバー画像の選択
* リソースの連絡先の識別
* メンバーへのリソースの割り当て

リソースがコース（学習パス）に含まれている場合は、メンバーを学習パスに割り当てる必要があります。割り当ては、イネーブルメントリソースの作成後に追加できます。

### 1 基本情報 {#basic-info}

![chlimage_1-169](assets/chlimage_1-169.png)

* **[!UICONTROL 画像を追加]**

   (*オプション*) メンバーの割り当てページおよびリソースコンソールのイネーブルメントリソースのカードに表示する画像です。 画像は、サーバーのローカルファイルシステムから選択されます。 画像が指定されていない場合、アップロードされたリソースのサムネールが生成されます。

   ***注意***：推奨される画像サイズは 480 x 480 ピクセルではありません。カードが様々なブラウザーサイズにレスポンシブデザインになるので、表示サイズは 220 x 165 ピクセルから 400 x 165 ピクセルまで様々です。

* **[!UICONTROL サイト名]**

   (*読み取り専用*) リソースを追加するコミュニティサイト。

* **[!UICONTROL リソース名&amp;ast;]**

   (*必須*) リソースの表示名。 有効なノード名が表示名から作成されます。

* **[!UICONTROL タグ]**

   (*オプション*) イネーブルメントリソースを 1 つ以上のカタログに関連付ける 1 つ以上のタグを選択できます。 [実施可能リソースのタグ付け](tag-resources.md)を参照してください。

* **[!UICONTROL カタログに表示]**

   オフにすると、イネーブルメントリソースはどのカタログにも表示されません。 オンにすると、イネーブルメントリソースがすべてのカタログに表示されます。ただし、[事前にフィルタリングされている](catalog-developer-essentials.md#pre-filters)場合と、メンバーが UI からフィルタリングした場合は除きます。初期設定はオフです。

* **[!UICONTROL 説明]**

   (*オプション*) イネーブルメントリソースに対して表示する説明。

* **[!UICONTROL 小さなアセット]**

   (*オプション*) AEM Assetsから選択しました。 カタログ内など、パブリッシュ環境でリソースを表すサムネイル画像です。

* **[!UICONTROL 大きなアセット]**

   (*オプション*) AEM Assetsから選択しました。 リソースのメインページなど、パブリッシュ環境でリソースを表す大きな画像です。

* **[!UICONTROL コンテンツフラグメントアセット]**

   (*オプション*) AEM Assetsから選択しました。 パブリッシュ環境で参照できるコンテンツフラグメント。ただし、初期設定では使用されません。

* 「**[!UICONTROL 次へ]**」を選択します。

### 2 コンテンツの追加 {#add-content}

![chlimage_1-170](assets/chlimage_1-170.png)

複数のイネーブルメントリソースを選択できるように見えますが、選択できるのは 1 つだけです。

を選択します。 `'+' icon`の右上隅にあるをクリックし、ソースを識別してリソースを選択するプロセスを開始します。

![chlimage_1-171](assets/chlimage_1-171.png)

* **[!UICONTROL ローカルファイルからアップロード]**&#x200B;ローカルファイルシステムからアップロードする場合は、ネイティブのファイルブラウザーを使用し、ファイルを選択してアップロードします。サポートされるファイルタイプは、SCORM.zip(HTML5 またはSWF)、MP4 ビデオ、SWF、PDF、画像の各タイプ (JPG、PNG、GIF、BMP) です。 ファイル名がアセットの名前になり、アセットライブラリに追加されます。

* **[!UICONTROL アセットライブラリを参照]**&#x200B;アセットライブラリから選択します。選択できるのは、コミュニティサイト内で表示されるものに限られます。

* **[!UICONTROL 外部 URL を追加]**

   学習コンテンツへのリンクを入力します。

   表示されたダイアログに以下を入力します。

   * **[!UICONTROL タイトル]**

      イネーブルメントリソースのアセットの名前です。

   * **[!UICONTROL URL]**

      アセットの URL。

* **[!UICONTROL Adobe Connect URL を追加]**

   Adobe Connectセッションへのリンクを入力します。

   表示されたダイアログに以下を入力します。

   * **[!UICONTROL タイトル]**

      イネーブルメントリソースのアセットの名前です。

   * **[!UICONTROL URL]**

      Adobe Connect セッションの URL です。

* **[!UICONTROL 外部リソースを定義]**

   資材を表示する場所を入力します。 成功ステータスとスコアの値は手動で入力します ( [レポート](reports.md)) をクリックします。 アップロードしたカバー画像を使用して、追加情報を提供できます。

   表示されたダイアログに以下を入力します。

   * **[!UICONTROL タイトル]**

      イネーブルメントリソースのアセットの名前です。

   * **[!UICONTROL 場所]**

      教室などの物理的なサイトの場所。

#### 追加されたビデオリソースの例 {#example-of-an-added-video-resource}

![chlimage_1-172](assets/chlimage_1-172.png)

* **[!UICONTROL リソースのカバー画像]**

   カバー画像は、イネーブルメントリソースが最初に表示されたときに表示される画像です。 例えば、ビデオリソースがまだ再生されていない場合に、カバー画像が表示されます。 カスタム画像がアップロードされない場合は、デフォルト画像が表示されます。 ビデオリソースの場合、次の操作が可能です。 [サムネールを生成](enablement.md#ffmpeg)ただし、ビデオが URL として参照されている場合はアップロード時にのみ有効です。 場所のリソースの場合、画像を使用して追加情報を提供できます。

   カバー画像の推奨サイズは 640 x 360 px です。

* 「**[!UICONTROL 次へ]**」を選択します。

### 3 設定 {#settings}

![chlimage_1-173](assets/chlimage_1-173.png)

>[!NOTE]
>
>学習パスで参照されるイネーブルメントリソースに学習者を直接登録することはできません。学習者は学習パスにのみ登録する必要があります。
>
>メンバーがリソースとそのリソースを参照する学習パスの両方に登録されている場合、そのメンバーの割り当てには、単体のリソースと学習パス内のリソースの両方が表示されます。

* **[!UICONTROL ソーシャルの設定]**

   これらの設定は、イネーブルメントリソースに関する入力を学習者に提供できるかどうかを制御します。 この [モデレート設定](sites-console.md#moderation) は親コミュニティサイトのものです。

   * **[!UICONTROL コメントを許可]**

      オンにすると、メンバーはリソースに対するコメントを許可されます。 初期設定はオンです。

   * **[!UICONTROL 評価を許可]**

      オンにすると、メンバーはリソースの評価を許可されます。 初期設定はオンです。

   * **[!UICONTROL 匿名アクセスを許可]**

      オンにすると、コミュニティサイトで匿名アクセスも許可されている場合に、匿名のサイト訪問者がカタログ内のリソースを表示できるようになります。 初期設定はオフです。

* **[!UICONTROL 期限]**

   *（オプション）* 割り当てを完了する日付を選択できます。

* **[!UICONTROL リソース作成者]**
   *（オプション）* イネーブルメントリソースの作成者。 プルダウンメニューを使用して、[メンバーグループ](#members-group)のメンバーの中から選択します。

* **[!UICONTROL リソース連絡先&amp;ast;]**
   *（必須）* メンバーがイネーブルメントリソースに関して連絡できる担当者。 プルダウンメニューを使用して、[メンバーグループ](#members-group)のメンバーの中から選択します。

* **[!UICONTROL リソースエキスパート]**
   *（オプション）* イネーブルメントリソースに関する専門知識を持つメンバーが連絡できる人物。 プルダウンメニューを使用して[メンバーグループ](#members-group)のメンバーの中から選択します。

### 4 割り当て {#assignments}

![chlimage_1-174](assets/chlimage_1-174.png)

* **[!UICONTROL 担当者を追加]**
プルダウンメニューを使用して、次の中から選択します。 [メンバー](#members-group)  — 学習者として登録されるユーザーおよびユーザーグループ（太字で表示）。 メンバーがコミュニティサイトにサインインすると、登録されているイネーブルメントリソース（および学習パス）がコミュニティサイトに表示されます [割り当て](functions.md#assignments-function) ページ。

* 「**[!UICONTROL 作成]**」を選択します。

![chlimage_1-175](assets/chlimage_1-175.png)

イネーブルメントリソースが正常に作成されると、リソースコンソールに戻ります。新しく作成されたリソースが選択状態になっています。このコンソールから、次の操作を実行できます。 [リソースの管理](#managing-a-resource).

## 学習パスの作成 {#create-a-learning-path}

![chlimage_1-176](assets/chlimage_1-176.png)

新しい学習パスをコミュニティサイトに追加するには、

* を選択します。 `Create` アイコン
* 表示されるサブメニューから、「 」を選択します。 `Learning Path`

すると、以下の設定をおこなう段階的なプロセスが開始します。

* 学習パスの識別
* 学習者に学習パスを表すカード画像の提供
* 学習パスに含めるイネーブルメントリソースを参照する
* 必要に応じて、リソースを並べ替えます。
* 前提条件の学習パスを任意で指定
* 学習パスの連絡先の識別
* メンバーの登録

学習パスに含まれるイネーブルメントリソースについては、リソースごとではなく、学習パスの単位で割り当てをおこなう必要があります。

### 基本情報 {#basic-info-1}

![chlimage_1-177](assets/chlimage_1-177.png)

* **[!UICONTROL 画像を追加]**

   (*オプション*) メンバーの割り当てページおよびリソースコンソールの学習パスのカードに表示する画像です。 画像は、サーバーのローカルファイルシステムから選択されます。 画像が指定されていない場合、アップロードされたリソースのサムネールが生成されます。

   ***注意***：推奨される画像サイズが 480 x 480 ピクセルではなくなりました。カードが様々なブラウザーサイズにレスポンシブデザインになるので、表示サイズは 220 x 165 ピクセルから 400 x 165 ピクセルまで様々です。

* **[!UICONTROL サイト名]**

   (*読み取り専用*) リソースを追加するコミュニティサイト。

* **[!UICONTROL 学習パス名]**

   (*必須*) 学習パスの表示名。 有効なノード名が表示名から作成されます。

* **[!UICONTROL タグ]**

   (*オプション*) 学習パスを 1 つ以上のカタログに関連付ける 1 つ以上のタグを選択できます。 [実施可能リソースのタグ付け](tag-resources.md)を参照してください。

* **[!UICONTROL カタログに表示]**

   オフにすると、学習パスはどのカタログにも表示されません。 オンにすると、学習パスがすべてのカタログに表示されます。ただし、[事前にフィルタリングされている](catalog-developer-essentials.md#pre-filters)場合と、メンバーが UI からフィルタリングした場合は除きます。カタログに学習パスを表示すると、含まれるすべてのリソースに対して間接的に読み取りアクセス権が付与されます。 初期設定はオフです。

* **[!UICONTROL 説明]**

   (*オプション*) イネーブルメントリソースに対して表示する説明。

* **[!UICONTROL 小さなアセット]**

   (*オプション*) AEM Assetsから選択しました。 カタログ内など、パブリッシュ環境でリソースを表すサムネイル画像です。

* **[!UICONTROL 大きなアセット]**

   (*オプション*) AEM Assetsから選択しました。 リソースのメインページなど、パブリッシュ環境でリソースを表す大きな画像です。

* **[!UICONTROL コンテンツフラグメントアセット]**

   (*オプション*) AEM Assetsから選択しました。 パブリッシュ環境で参照できるコンテンツフラグメント。ただし、初期設定では使用されません。

* 「**[!UICONTROL 次へ]**」を選択します。

### 前提条件を追加 {#add-prerequisites}

![chlimage_1-178](assets/chlimage_1-178.png)

* **[!UICONTROL 前提条件の学習パス]**
(
*オプション*) 公開された他の学習パスを選択した場合、学習者がこの学習パスを選択する前に、パスを入力する必要があります。

* 「**[!UICONTROL 次へ]**」を選択します。

### リソースを追加 {#add-resources}

![chlimage_1-179](assets/chlimage_1-179.png)

* **[!UICONTROL 学習パスの順序を適用]**

   (*オプション*) をオンに設定すると、イネーブルメントリソースが追加される順序は、学習パスを進めるために学習者が必要とする順序になります。 初期設定はオフです。

* **[!UICONTROL リソース]**

   現在のコミュニティサイト用に作成された公開済みのイネーブルメントリソースの中から 1 つ以上のリソースを選択します。

>[!NOTE]
>
>学習パスと同じレベルのリソースのみを選択できます。例えば、グループ内に作成された学習パスには、グループレベルのリソースのみを使用できます。コミュニティサイト内に作成された学習パスには、そのサイト内のリソースを追加できます。

* 「**[!UICONTROL 次へ]**」を選択します。

### 設定 {#settings-1}

![chlimage_1-180](assets/chlimage_1-180.png)

* **[!UICONTROL 登録を追加]**

   プルダウンメニューを使用して、コミュニティサイトのメンバーであるメンバーおよびメンバーグループ（太字で表示）から選択します。 [メンバーグループ](#members-group). 最初に学習パスを作成する際に、割り当てを追加する必要はありません。 学習パスのプロパティを変更して、後で学習者を追加できます。

* **[!UICONTROL 学習パスの連絡先&amp;ast;]**

   *（必須）* メンバーが学習パスに関して連絡できる人物。 プルダウンメニューを使用して、コミュニティサイトの[メンバーグループ](#members-group)のメンバーの中から選択します。

* 「**[!UICONTROL 作成]**」を選択します。

>[!NOTE]
>
>学習パスにより参照されているイネーブルメントリソースに、同じ割り当て先（学習者）を登録する必要はありません（該当する場合）。
>
>メンバーがイネーブルメントリソースとそのリソースを参照する学習パスの両方に登録されている場合、そのメンバーの割り当てには、単体のリソースと学習パス内のリソースの両方が表示されます。

## リソースの管理 {#managing-a-resource}

単体のイネーブルメントリソースを管理するには、

* リソースコンソールから
* リソースを含むコミュニティサイトを選択します
* リソースを選択

選択したイネーブルメントリソースに対し、以下を実行できます。

* プロパティの表示（デフォルト）
* プロパティの編集
* 削除
* 公開
* 非公開

新しいバージョンのイネーブルメントリソースをアップロードする際は、新しいリソースを作成したうえで、古いバージョンのリソースからメンバーを登録解除して新しいバージョンのリソースに登録することを推奨します。

### リソースの編集 {#edit-resource}

![chlimage_1-181](assets/chlimage_1-181.png)

鉛筆アイコンを選択すると、イネーブルメントリソースを作成したときと同じ手順が表示されるので、ここで設定を変更できます。

「設定」の手順の割り当て先だけを変更する場合は、変更して保存すると、変更が公開されます。その他の変更が行われた場合は、保存後にリソースを明示的に公開する必要があります。

### リソースの削除 {#delete-resource}

![chlimage_1-182](assets/chlimage_1-182.png)

ごみ箱アイコンを選択すると、イネーブルメントリソースは次のようになります。 `Delete`d 確認後。

### 公開 {#publish}

![chlimage_1-183](assets/chlimage_1-183.png)

学習者が割り当てられたイネーブルメントリソースを確認できるようにするには、以下の手順でリソースを公開する必要があります。

* 次の場所にある世界のアイコンを選択します。 `Publish`
* ポップアップ表示されるダイアログで、「 」を選択します。 **[!UICONTROL 公開]** 再度
* 選択 **[!UICONTROL 閉じる]**

ダイアログに「アクションは待機中です」と表示されても、通常はすぐに公開されます。

### 非公開 {#unpublish}

![chlimage_1-184](assets/chlimage_1-184.png)

パブリッシュ環境のメンバーが削除せずに一時的にイネーブルメントリソースにアクセスできなくするには、ワールドアイコンを使用して `Unpublish`リソース。

### レポート {#report}

![chlimage_1-185](assets/chlimage_1-185.png)

「レポート」アイコンを選択すると、学習者がパブリッシュ環境で割り当てられたイネーブルメントリソースに接したときに生成されるレポートにアクセスできます。レポートは、リソースのタイプに応じて異なります。

すべての学習パスに対して、リソースまたは学習者 ( `User Report`) をクリックします。

![chlimage_1-186](assets/chlimage_1-186.png)

このレポートは、現在のイネーブルメントリソースまたは学習パスに関するものです。表示されるレポートの深さは、レポートの種類に応じて異なります [Adobe Analytics](analytics.md) はコミュニティサイトに対してライセンスを取得し、有効にしています。 この [タイムライン](#timeline), [閲覧者のアクション](#viewer-engagement)、および [デバイス別のエンゲージメント](#engagement-by-device) レポートは、 [ポーリング間隔](analytics.md#report-importer).

どのイネーブルメントリソースでも、Adobe Analytics が有効かどうかに関係なく、[担当者ステータス](#assignee-status)および[評価](#ratings)に関するレポートと、[レポートサマリ](#report-summary)テーブルを利用できます。

![chlimage_1-187](assets/chlimage_1-187.png)

#### タイムライン {#timeline}

Analytics のタイムラインレポートには、このイネーブルメントリソースで以下のイベントが発生した時刻が表示されます。

* **表示**

   ビューとは、学習者がリソースの詳細ページを訪問したときのことです

* **再生**

   再生とは、学習者がリソースとやり取りするとき ( ビデオの再生やPDFの開始など )

* **Ratings**

   評価とは、学習者がリソースに星評価を割り当てたときです

* **コメント**

   コメントとは、alNearner がコメントを追加したときです

縦軸はイベント数です。

横軸はカレンダー時間です。

[Adobe Analytics が必要](sites-console.md#analytics)です。

#### ビューアエンゲージメント {#viewer-engagement}

Analytics のビューアエンゲージメントレポート（ビデオリソース用）には、リソースを表示した学習者の数が表示されます。また、学習者が最後まで再生しなかった場合は、再生をやめた時点が表示されます。

縦軸はこのリソースを表示した学習者の数です。

横軸はこのリソースの期間です。

[Marketing Cloud 組織 ID が必要](sites-console.md#enablement)です。

#### デバイス別のアクション {#engagement-by-device}

Analytics のデバイス別のアクションレポート（ビデオリソース用）には、デスクトップとモバイルから再生された閲覧数の割合が表示されます。

[Marketing Cloud 組織 ID が必要](sites-console.md#enablement)です。

#### 担当者ステータス {#assignee-status}

担当者ステータスレポートには、以下の分類に該当する学習者の数が表示されます。

* **未開始**
* **処理中**
* **完了**

#### 評価 {#ratings}

評価レポートには、イネーブルメントリソースを評価した学習者の数が表示されます。それぞれの星評価の数に加え、評価の合計数と平均評価の概要が表示されます。

#### レポートサマリ {#report-summary}

イネーブルメントリソースの場合、レポートサマリには以下の内容が表示されます。

* リソースを操作した各学習者
   * ステータス
   * リソースが割り当てられたかどうか
      * カタログでリソースを見つけるのとは対照的に
   * 投稿されたコメント数
   * 与えられた評価（存在する場合）

学習パスのリソースレポートの場合、レポートサマリには以下の内容が表示されます。

* 学習パスに含まれる各リソース
   * 公開ステータス
   * ビュー数
   * 再生数
   * 平均評価
   * 形式
   * サイズ
   * コミュニティサイト名

学習パスのユーザーレポートの場合、レポートサマリには以下の内容が表示されます。

* 学習パスに割り当てられている各学習者
   * 完了したリソースの数
   * ステータス

列を選択すると、テーブルの表示を調整できます。 `Show / hide columns` セレクター。

#### CSV 形式でのレポートのダウンロード {#download-report-as-csv}

コンソール上部のボタンを使用して、「レポートの概要」テーブルを CSV 形式でダウンロードできます。

* イネーブルメントリソースの場合： `Download Resource Report as CSV` ボタン
* 学習パスの場合： `Download Learning Path Report as CSV` ボタン

一部の列だけを表示するよう選択している場合でも、「レポートの概要」テーブルのすべての列がダウンロードされます。
