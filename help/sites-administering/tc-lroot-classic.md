---
title: クラシック UI による言語ルートの作成
seo-title: Creating a Language Root Using the Classic UI
description: クラシック UI を使用して言語ルートを作成する方法を説明します。
seo-description: Learn how to create a language root using the Classic UI.
uuid: d44a51a0-1507-4838-851c-cacff48ad825
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.4/SITES
topic-tags: site-features
content-type: reference
discoiquuid: 237b8cc6-158e-4c51-970d-4c9cc74f6496
feature: Language Copy
exl-id: 316903a8-22cf-45e6-a9f3-ac1d75beddec
source-git-commit: c5b816d74c6f02f85476d16868844f39b4c47996
workflow-type: tm+mt
source-wordcount: '352'
ht-degree: 24%

---

# クラシック UI による言語ルートの作成{#creating-a-language-root-using-the-classic-ui}

>[!CAUTION]
>
>AEM 6.4 の拡張サポートは終了し、このドキュメントは更新されなくなりました。 詳細は、 [技術サポート期間](https://helpx.adobe.com/jp/support/programs/eol-matrix.html). サポートされているバージョンを見つける [ここ](https://experienceleague.adobe.com/docs/?lang=ja).

次の手順では、クラシック UI を使用してサイトの言語ルートを作成します。 詳しくは、 [言語ルートの作成](/help/sites-administering/tc-prep.md#creating-a-language-root).

1. Web サイトコンソールの Web サイトツリーで、サイトのルートページを選択します。 ([http://localhost:4502/siteadmin#](http://localhost:4502/siteadmin#))
1. サイトの言語バージョンを表す新しい子ページを追加します。

   1. 新規/新しいページをクリックします。
   1. ダイアログで、「タイトル」と「名前」を指定します。名前の形式は `<language-code>` または `<language-code>_<country-code>` です。例えば、en、en_US、en_us、en_GB、en_gb のようにします。

      * サポートされている言語コードは、ISO-639-1 で定義されている小文字の 2 文字コードです。
      * サポートされる国コードは、ISO 3166 で定義されている小文字または大文字 2 文字のコードです。
   1. テンプレートを選択し、「作成」をクリックします。

   ![newpagefr](assets/newpagefr.png)

1. Web サイトコンソールの Web サイトツリーで、サイトのルートページを選択します。
1. ツールメニューで、「言語コピー」を選択します。

   ![toollanguagecopy](assets/toolslanguagecopy.png)

   言語コピーダイアログには、使用可能な言語バージョンと Web ページの一覧が表示されます。 言語列の x は、その言語でページが利用できることを意味します。

   ![languagecopydialog](assets/languagecopydialog.png)

1. 既存のページまたはページツリーを言語バージョンにコピーするには、言語列でそのページのセルを選択します。 矢印をクリックし、作成するコピーのタイプを選択します。

   次の例では、equipment/sunglass/irian ページがフランス語版にコピーされています。

   ![languagecopydilogdropdown](assets/languagecopydilogdropdown.png)

   | 言語コピーのタイプ | 説明 |
   |---|---|
   | auto | 親ページの動作を使用します |
   | 無視 | このページとその子のコピーを作成しません |
   | `<language>+` （例：フランス語+） | ページとそのすべての子を対象の言語からコピーします。 |
   | `<language>` （例：フランス語） | その言語からページのみをコピーします |

1. 「OK」をクリックして、ダイアログを閉じます。
1. 次のダイアログで、「はい」をクリックしてコピーを確定します。
