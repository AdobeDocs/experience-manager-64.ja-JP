---
title: アクセシブルなアダプティブフォームの作成
seo-title: Creating accessible adaptive forms
description: AEM Forms には、アクセシブルなアダプティブフォームを作成するためのツールが用意されており、アクセシビリティ標準への準拠を支援する機能が含まれています。
seo-description: AEM Forms provides you tools and to create accessible adaptive forms and helps comply with accessibility standards.
uuid: eceb3282-0b90-4e0a-8b89-137d27029747
products: SG_EXPERIENCEMANAGER/6.4/FORMS
topic-tags: author
discoiquuid: 96d9ad52-074b-4084-b818-abce79282776
feature: Adaptive Forms
exl-id: adad26fa-b27a-4bd7-806c-4ddfbaae7a37
source-git-commit: bd94d3949f0117aa3e1c9f0e84f7293a5d6b03b4
workflow-type: tm+mt
source-wordcount: '903'
ht-degree: 99%

---

# アクセシブルなアダプティブフォームの作成 {#creating-accessible-adaptive-forms}

## はじめに {#introduction}

アクセシブルなフォームとは、特別な支援を必要とするユーザーを含むすべてのユーザーが使用できるフォームを意味します。Adobe Experience Manager (AEM) は、障害を持つ様々なユーザーに対するアダプティブフォームの可用性を向上するためのさまざまな特長や機能を備えています。このソリューションは、フォーム作成者がアクセスしやすいアダプティブフォームを作成する上でも役立ちます。

アクセシビリティをアダプティブフォームに組み入れることは、可能な限り多くの人がコンテンツにアクセスできるようになるだけでなく、アクセシビリティ標準への準拠が法律で義務付けられている地域にドキュメントを供給するときの必要条件でもあります。AEM Forms は、フォーム開発者がアクセシビリティ標準に準拠できるよう考慮されています。

アダプティブフォームの作成時に、作成者は次の事項を考慮してアクセシブルなアダプティブフォームを作成する必要があります。

* フォームのコントロールに対する正しいラベルの提供
* 画像の代替テキストの提供
* 十分なカラーコントラストの提供
* フォームのコントロールがキーボードでアクセスできることの確認

## フォームのコントロールに対する正しいラベルの提供 {#provide-proper-labels-for-form-controls}

コンポーネントのラベルまたはタイトルにより、フォームコンポーネントの内容が分かります。例えば、「名」というテキストを付ければ、テキストフィールドに名前を入力するようにユーザーに指示することができます。スクリーンリーダーによってアクセシブルにするために、ラベルはフォームコンポーネントにプログラム的に関連付けられます。あるいは、フォームのコントロールは追加のアクセシブル情報で設定されます。

スクリーンリーダーによって認識されるラベルは、表示キャプションと必ずしも同じである必要はありません。場合によっては、コントロールの目的をさらに具体的に説明するものにすることもできます。フォームの各フィールドオブジェクトごとに、アクセシビリティオプションを使用して、スクリーンリーダーがその特定のフォームフィールドを識別するためのものを指定することができます。

アクセシビリティオプションを使用するには、次の手順に従います。

1. コンポーネントを選択して、![cmppr](assets/cmppr.png) をタップします。
1. サイドバーの&#x200B;**アクセシビリティ**&#x200B;をクリックして、必要なアクセシビリティオプションを選択します。

### フォームコンポーネントのアクセシビリティオプション {#accessibility-options-in-form-components}

![フォームコンポーネントのアクセシビリティオプション](assets/accessibility-options.png)

**カスタムテキスト**&#x200B;フォーム作成者は、アクセシビリティオプションカスタムテキストフィールドにコンテンツを入力します。スクリーンリーダーなどの支援機能は、このカスタムテキストを使用します。ほとんどの事例の場合、タイトル設定を使用することが最も適切です。カスタムのスクリーンリーダーテキストを作成するのは、タイトルや簡単な説明を使用できない場合のみにすることに留意してください。

**簡単な説明** ほとんどのコンポーネントでは、ユーザーがコンポーネントの上にポインターを置くと、実行時に簡単な説明が表示されます。このオプションは、ヘルプコンテンツオプションの簡単な説明フィールドで設定できます。

**タイトル** このオプションを使用すると、AEM Forms はフォームフィールドに関連付けられている表示ラベルをスクリーンリーダーのテキストとして使用できます。

**名前** バインディングタブの名前フィールドに値を指定できます。名前には空白を含めることはできません。

**なし** 「なし」を選択すると、フォームオブジェクトは発行されたフォームに名前が表示されなくなります。フォームのコントロールに対して「なし」を設定することは推奨しません。

>[!NOTE]
>
>ラジオボタンとチェックボックスには、アクセシビリティのために 2 つだけオプション（カスタムテキストとタイトル）を設定することができます。

>[!NOTE]
>
>FXA ベースのアダプティブフォームの場合、アクセシビリティオプションは、XDP に設定されているアクセシビリティオプションから継承されます。XDP のツールヒントは簡単な説明にマッピングされ、キャプションはタイトルにマッピングされます。その他のオプションはそのまま機能します。

## 画像の代替テキストの提供 {#provide-text-equivalents-for-images}

画像を使用すると、一部のユーザーに対して理解度を向上することに役立ちます。ただし、スクリーンリーダーを使用するユーザーに対しては、画像の使用はフォームのアクセシビリティを低下させます。画像を使用する場合は、すべての画像に対して代替テキストを提供してください。

このテキストは、フォーム内のオブジェクトとその目的を説明する内容である必要があります。スクリーンリーダーが画像を検出すると、この代替テキストを読み上げます。画像は常に代替テキストが指定される必要があります。

画像コンポーネントを選択し ![cmppr](assets/cmppr.png) をタップします。サイドバーのプロパティで、画像の代替テキストを指定します。

![画像の代替テキスト](assets/image-properties.png)

## 十分なカラーコントラストの提供 {#provide-sufficient-color-contrast}

アクセシビリティデザインでは、カラーの使用に対する特別なガイドラインを考慮する必要があります。フォーム作成者は、カラーを使用して様々なフォームのコンポーネントを強調表示することで、フォームの外観を改善できます。ただし、カラーの使い方が不適切だと、障害を持つ人たちがフォームを読むことを困難あるいは不可能にしてしまうことがあります。

視覚障害を持つユーザーは、デジタルコンテンツを読むときに、テキストと背景の間に高いコントラストを必要とします。十分なコントラストがないと、一部のユーザーがフォームを読むことが不可能ではないにしても困難になる場合があります。

デフォルトのフォントと背景（白の背景に黒のコンテンツ）を使用することが推奨されます。デフォルトカラーを変更する場合は、明るい背景に暗い前景またはその逆を選択してください。

アダプティブフォームのカラーコントラストとテーマを変更することについて詳しくは、[アダプティブフォームのカスタムテーマの作成](/help/forms/using/creating-custom-adaptive-form-themes.md)を参照してください。

## フォームのコントロールがキーボードでアクセスできることの確認 {#ensure-that-form-controls-are-keyboard-accessible}

アクセシブルフォームは、キーボードまたは相当の入力デバイスのみを使用してすべて記入できます。四肢や視覚に障害を持つユーザーはキーボードのみで入力を行わなければならない場合があります。また、マウスを使用できるユーザーでもキーボード入力を好むひとが多くいます。入力の方法を複数用意することで、アクセシブルなフォームが作成できるだけではなく、すべてのユーザーの要望に応えられるフォームが作成できます。

AEM Forms では次のキーボードショートカットが使用できます。

| 動作 | キーボードショートカット |
|---|---|
| 次のフォームへカーソルを移動させます。 | タブ |
| 前のフォームへカーソルを移動させます。 | Shift + Tab |
| 次のパネルに移動します。 | Alt + 右向き矢印 |
| 前のパネルに移動します。 | Alt + 左向き矢印 |
| フォーム内の記入済みデータをリセットします。 | Alt + R |
| フォームを送信します。 | Alt + S | configuring-watched-folder-endpoints.md |
