---
title: アダプティブフォームのセットを使用したアダプティブフォームの作成
seo-title: Create an adaptive form using a set of adaptive forms
description: AEM Formsでは、アダプティブフォームを統合して 1 つの大きなアダプティブフォームを作成し、その機能を理解します。
seo-description: With AEM Forms, bring adaptive forms together to author a single large adaptive form, and understand its features.
uuid: 1423038b-8261-455b-b4ff-7be7222448c9
products: SG_EXPERIENCEMANAGER/6.4/FORMS
topic-tags: develop
discoiquuid: 75ee94f7-e939-409b-b8cb-8fdc3f79bb63
feature: Adaptive Forms
exl-id: 969b0c11-adc7-476e-8c82-d444fccba984
source-git-commit: bd94d3949f0117aa3e1c9f0e84f7293a5d6b03b4
workflow-type: tm+mt
source-wordcount: '569'
ht-degree: 50%

---

# アダプティブフォームのセットを使用したアダプティブフォームの作成 {#create-an-adaptive-form-using-a-set-of-adaptive-forms}

## 概要 {#overview}

銀行口座の開設の申し込みなどのワークフローでは、ユーザーは複数のフォームに記入します。 フォームのセットに入力するよう依頼する代わりに、フォームを積み重ねて大きなフォーム（親フォーム）を作成できます。 大きい方のフォームにアダプティブフォームを追加すると、パネル（子フォーム）として追加されます。 子フォームのセットを追加して、親フォームを作成します。 ユーザーの入力に基づいて、パネルの表示と非表示を切り替えることができます。 親フォームのボタン（送信やリセットなど）は、子フォームのボタンを上書きします。 親フォームにアダプティブフォームを追加するには、アダプティブフォームを（アダプティブフォームフラグメントと同様に）アセットブラウザーからドラッグ&amp;ドロップします。

使用できる機能は、次のとおりです。

* 独立オーサリング
* 適切なフォームの表示/非表示
* 遅延読み込み

独立オーサリングや遅延読み込みなどの機能を使用すると、個々のコンポーネントを使用して親フォームを作成する場合のパフォーマンスが向上します。

>[!NOTE]
>
>XFA ベースのアダプティブフォーム/フラグメントは、子フォームや親フォームとして使用することはできません。

## 舞台裏 {#behind-the-scenes}

親フォームに XSD ベースのアダプティブフォームとフラグメントを追加することができます。 親フォームの構造は [任意のアダプティブフォーム](/help/forms/using/prepopulate-adaptive-form-fields.md). アダプティブフォームを子フォームとして追加すると、親フォームのパネルとして追加されます。バインドされた子フォームのデータは、親フォームの XML スキーマの `afBoundData` セクションの `data` ルートに保存されます。

例えば、顧客が申込フォームに入力するとします。 フォームの最初の 2 つのフィールドは、名前と ID です。 XML は次のようになります。

```xml
<afData>
    <afUnboundData>
        <data />
    </afUnboundData>
    <afBoundData>
        <data xmlns:xfa="https://www.xfa.org/schema/xfa-data/1.0/">
            <applicantName>Sarah Rose</applicantName>
            <applicantId>1234</applicantId>
        </data>
    </afBoundData>
</afData>
```

顧客がオフィスの住所を入力できるフォームをアプリに追加します。 子フォームのスキーマのルートは `officeAddress` です。`bindref`、`/application/officeAddress` または `/officeAddress` を適用します。`bindref` がない場合、子フォームが `officeAddress` サブツリーとして追加されます。以下のフォームの XML を参照してください。

```xml
<afData>
    <afUnboundData>
        <data />
    </afUnboundData>
    <afBoundData>
        <data xmlns:xfa="https://www.xfa.org/schema/xfa-data/1.0/">
            <applicantName>Sarah Rose</applicantName>
            <applicantId>1234</applicantId>
            <officeAddress>
                <addressLine>1, Geometrixx City</addressLine>
                <zip>11111</zip>
            </officeAddress>
        </data>
    </afBoundData>
</afData>
```

顧客が住所を入力できる別のフォームを挿入する場合は、`bindref` `/application/houseAddress or /houseAddress.`を適用すると、XML は次のようになります。

```xml
<afData>
    <afUnboundData>
        <data />
    </afUnboundData>
    <afBoundData>
        <data xmlns:xfa="https://www.xfa.org/schema/xfa-data/1.0/">
            <applicantName>Sarah Rose</applicantName>
            <applicantId>1234</applicantId>
            <officeAddress>
                <addressLine>1, Geometrixx City</addressLine>
                <zip>11111</zip>
            </officeAddress>
            <houseAddress>
                <addressLine>2, Geometrixx City</addressLine>
                <zip>11111</zip>
            </houseAddress>
        </data>
    </afBoundData>
</afData>
```

スキーマのルートと同じサブルート名にするには、（この例では`Address` ）、インデックス付きの bindref を使用します。

例えば、bindref `/application/address[1]` または `/address[1]` および `/application/address[2]` または `/address[2]` を適用します。このフォームの XML は、以下のようになります。

```xml
<afData>
    <afUnboundData>
        <data />
    </afUnboundData>
    <afBoundData>
        <data xmlns:xfa="https://www.xfa.org/schema/xfa-data/1.0/">
            <applicantName>Sarah Rose</applicantName>
            <applicantId>1234</applicantId>
            <address>
                <addressLine>1, Geometrixx City</addressLine>
                <zip>11111</zip>
            </address>
            <address>
                <addressLine>2, Geometrixx City</addressLine>
                <zip>11111</zip>
            </address>
        </data>
    </afBoundData>
</afData>
```

`bindRef` プロパティを使用して、フォームまたはフラグメントのデフォルトサブツリーを変更することができます。`bindRef` プロパティにより、XML スキーマのツリー構造における位置を示すパスを指定できます。

バインドされていない子フォームのデータは、親フォームの XML スキーマの `afUnboundData` セクションの `data` ルートに保存されます。

アダプティブフォームを子フォームとして、複数回追加できます。`bindRef` が正しく修正されて、アダプティブフォームの各使用済みインスタンスが、データルート上で異なるサブルートを指定するようにします。

>[!NOTE]
>
>異なるフォームやフラグメントが同じサブルートにマッピングされている場合、データは上書きされます。

## アセットブラウザーを使用した子フォームとしてのアダプティブフォームの追加 {#adding-an-adaptive-form-as-a-child-form-using-asset-browser}

アセットブラウザーを使用してアダプティブフォームを子フォームとして追加するには、次の手順を実行します。

1. 親フォームを編集モードで開きます。
1. サイドバーで、**アセット**／![アセットブラウザー](assets/assets-browser.png)をクリックします。アセットの下で、**アダプティブフォーム** をドロップダウンリストから選択します。
   [ ![アセットの下でアダプティブフォームを選択する](assets/asset.png)](assets/asset-1.png)

1. 子フォームとして追加するアダプティブフォームをドラッグ＆ドロップします。
   [ ![サイトにアダプティブフォームをドラッグ＆ドロップします。](assets/drag-drop.png)](assets/drag-drop-1.png)ドロップしたアダプティブフォームは、子フォームとして追加されます。
