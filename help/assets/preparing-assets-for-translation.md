---
title: 翻訳用アセットの準備
description: 言語ルートフォルダーを作成し、多言語アセットを翻訳するための準備をします。
contentOwner: AG
translation-type: tm+mt
source-git-commit: 0d70a672a2944e2c03b54beb3b5f734136792ab1

---


# 翻訳用アセットの準備 {#preparing-assets-for-translation}

多言語アセットとは、複数の言語のバイナリ、メタデータ、タグを含むアセットです。通常、アセットのバイナリ、メタデータ、タグに使用される言語は 1 つですが、多言語プロジェクト用に他の言語へと翻訳されます。

Adobe Experience Manager（AEM）Assets では、多言語アセットはフォルダーに含まれ、各フォルダーに異なる言語のアセットが格納されます。

各言語のフォルダーは言語コピーと呼ばれます。言語コピーのルートフォルダー（言語ルート）が、言語コピー内のコンテンツの言語を識別します。For example, */content/dam/it* is the Italian language root for the Italian language copy. Language copies must use a [correctly-configured language root](preparing-assets-for-translation.md#creating-a-language-root) so that the correct language is targeted when translations of source assets are performed.

最初にアセットを追加した言語コピーが言語マスターです。言語マスターは、他の言語に翻訳されるソースです。

サンプルフォルダー階層にはいくつかの言語ルートが含まれています。

```java
/content
    /- dam
             |- en
             |- fr
             |- de
             |- es
             |- it
             |- ja
             |- zh
```

翻訳するアセットを準備するには、次の手順を実行します。

1. 言語マスターの言語ルートを作成します。For example, the language root of the English language copy in the sample folder hierarchy is `/content/dam/en`. Ensure that the language root is correctly configured according to the information in [Creating a Language Root](preparing-assets-for-translation.md#creating-a-language-root).

1. 言語マスターにアセットを追加します。
1. 言語コピーが必要な各ターゲット言語の言語ルートを作成します。

## 言語ルートの作成 {#creating-a-language-root}

言語ルートを作成するには、フォルダーを作成し、「名前」プロパティの値として ISO 言語コードを使用します。言語ルートを作成したら、言語ルート内の任意のレベルに言語コピーを作成できます。

For example, the root page of the Italian language copy of the sample hierarchy has `it` as the Name property. The Name property is used as the name of the asset node in the repository, and therefore determines the path of the assets. (`https://[AEM_server]:[port]/assets.html/content/dam/it/*`)

1. Assets コンソールで「**[!UICONTROL 作成]**」をクリックし、メニューから「**[!UICONTROL フォルダー]**」を選択します。

   ![chlimage_1-120](assets/chlimage_1-120.png)

1. In the Name field type the country code in the format of `<language-code>`.

   ![chlimage_1-121](assets/chlimage_1-121.png)

1. 「**[!UICONTROL 作成]**」をクリックまたはタップします。Assets コンソール内に言語ルートが作成されます。

## 言語ルートの表示 {#viewing-language-roots}

タッチ対応 UI には参照パネルがあります。このパネルには、AEM Assets 内で作成された言語ルートのリストが表示されます。

1. Assets コンソールで、言語コピーを作成する言語マスターを選択します。
1. グローバルナビゲーションアイコンをクリックまたはタップして、「**[!UICONTROL 参照]**」を選択して参照パネルを開きます。

   ![chlimage_1-122](assets/chlimage_1-122.png)

1. 参照パネルで、「**[!UICONTROL 言語コピー]**」をクリックまたはタップします。アセットの言語コピーが言語コピーパネルに表示されます。

   ![chlimage_1-123](assets/chlimage_1-123.png)

