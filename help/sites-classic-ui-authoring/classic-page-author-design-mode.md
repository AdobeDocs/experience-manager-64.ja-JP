---
title: デザインモードでのコンポーネントの設定
seo-title: Configuring Components in Design Mode
description: AEMインスタンスを標準でインストールすると、サイドキックで直ちに様々なコンポーネントを使用できます。 これらに加えて、他の様々なコンポーネントも使用できます。デザインモードを使用して、このようなコンポーネントを有効または無効にすることができます。
seo-description: When AEM instance is installed out-of-the-box, a selection of components are immediately available in the sidekick. In addition to these, various other components are also available. You can use Design mode to Enable/disable such components.
page-status-flag: de-activated
uuid: 57249965-3a30-49ce-9fb0-864c5daaa262
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.4/SITES
topic-tags: page-authoring
content-type: reference
discoiquuid: 93f98f7b-7ab8-4d9c-b179-dc99b80ffc91
exl-id: af6c383b-f8fd-442c-8fc5-3cdd40657c6a
source-git-commit: c5b816d74c6f02f85476d16868844f39b4c47996
workflow-type: tm+mt
source-wordcount: '536'
ht-degree: 39%

---

# デザインモードでのコンポーネントの設定 {#configuring-components-in-design-mode}

>[!CAUTION]
>
>AEM 6.4 の拡張サポートは終了し、このドキュメントは更新されなくなりました。 詳細は、 [技術サポート期間](https://helpx.adobe.com/jp/support/programs/eol-matrix.html). サポートされているバージョンを見つける [ここ](https://experienceleague.adobe.com/docs/?lang=ja).

AEMインスタンスを標準でインストールすると、サイドキックで直ちに様々なコンポーネントを使用できます。

これらに加えて、その他の様々なコンポーネントも使用できます。このような[コンポーネントを有効または無効にする](#enabledisablecomponentsusingdesignmode)には、デザインモードを使用します。コンポーネントを有効にしてページに配置したら、デザインモードを使用して属性パラメーターを編集することで[コンポーネントデザインの様々な要素を設定](#configuringcomponentsusingdesignmode)できます。

>[!NOTE]
>
>これらのコンポーネントを編集する際は慎重に行ってください。デザインの設定は、通常、web サイト全体のデザインで重要な部分なので、適切な権限（および十分な経験）のあるユーザー（通常は、管理者または開発者）のみが変更を行う必要があります。詳しくは、[コンポーネントの開発](/help/sites-developing/components.md)を参照してください。

具体的には、ページの段落システムで許可された構成要素を追加したり、削除したりすることです。段落システム（`parsys`）は、他のすべての段落コンポーネントを含む複合コンポーネントです。段落システムを使用すると、作成者は異なるタイプのコンポーネントを、他のすべての段落コンポーネントを含むページに追加できます。 各段落タイプは、コンポーネントとして表されます。

例えば、製品ページのコンテンツには、次の情報を含む段落システムを含めることができます。

* 製品の画像（画像または textimage 段落の形式）
* 製品の説明（テキスト段落）
* 技術データを含むテーブル（表の段落として）
* フォームユーザーが入力する（フォームの開始、フォームの要素、フォームの終了段落として）

>[!NOTE]
>
>[ について詳しくは、](/help/sites-developing/components.md#paragraphsystem)コンポーネントの開発[および](/help/sites-developing/dev-guidelines-bestpractices.md#guidelines-for-using-templates-and-components)テンプレートとコンポーネントの使用に関するガイドライン`parsys`を参照してください。

## コンポーネントを有効/無効にする {#enable-disable-components}

デザインモードでは、サイドキックは最小化され、オーサリング用にアクセス可能なコンポーネントを設定できます。

1. デザインモードに入るには、編集するページを開き、サイドキックアイコンを使用します。

   ![](do-not-localize/chlimage_1.png)

1. 段落システムの「**編集**」（**段落のデザイン**）をクリックします。

   ![screen_shot_2012-02-08at102726am](assets/screen_shot_2012-02-08at102726am.png)

1. ダイアログが開き、サイドキックに表示されるコンポーネントグループと、それらが含む個々のコンポーネントが一覧表示されます。

   必要に応じて、サイドキックで使用可能なコンポーネントを追加または削除します。

   ![screen_shot_2012-02-08at103407am](assets/screen_shot_2012-02-08at103407am.png)

1. デザインモードでは、サイドキックは最小化されます。 矢印をクリックすると、サイドキックを最大化して編集モードに戻ることができます。

   ![](do-not-localize/sidekick-collapsed.png)

## コンポーネントのデザインの設定 {#configuring-the-design-of-a-component}

デザインモードでは、個々のコンポーネントの属性を設定することもできます。 各コンポーネントには独自のパラメーターがあります。次に例を示します。 **画像** コンポーネント：

1. デザインモードに入るには、編集するページを開き、サイドキックアイコンを使用します。

   ![](do-not-localize/chlimage_1-1.png)

1. コンポーネントのデザインを設定できます。

   たとえば、画像コンポーネントの「**編集**」（**画像のデザイン**）をクリックすると、そのコンポーネント特有のパラメーターを設定できます。

   ![chlimage_1-12](assets/chlimage_1-12.png)

1. 「**OK**」をクリックして、変更を保存します。

1. デザインモードでは、サイドキックは最小化されます。 矢印をクリックすると、サイドキックを最大化して編集モードに戻ることができます。

   ![](do-not-localize/sidekick-collapsed-1.png)
