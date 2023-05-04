---
title: XFA または PDF フォームテンプレートのダウンロード
seo-title: Download an XFA or a PDF form template
description: リポジトリからローカルシステムにフォームを書き出し、ダウンロードしたフォームを新しいリポジトリに移行することができます。
seo-description: You can export forms from the repository to the local system and migrate the downloaded forms to new repository.
uuid: 5f7fbd14-cb9d-4749-8708-7efe49df89d7
content-type: reference
products: SG_EXPERIENCEMANAGER/6.4/FORMS
topic-tags: forms-manager
discoiquuid: 6699e0e7-fd42-41ae-86a2-3b940d905111
role: Admin
exl-id: 68d881c6-7507-4018-b40e-205604221d0c
source-git-commit: c5b816d74c6f02f85476d16868844f39b4c47996
workflow-type: tm+mt
source-wordcount: '349'
ht-degree: 38%

---

# XFA または PDF フォームテンプレートのダウンロード {#download-an-xfa-or-a-pdf-form-template}

>[!CAUTION]
>
>AEM 6.4 の拡張サポートは終了し、このドキュメントは更新されなくなりました。 詳細は、 [技術サポート期間](https://helpx.adobe.com/jp/support/programs/eol-matrix.html). サポートされているバージョンを見つける [ここ](https://experienceleague.adobe.com/docs/?lang=ja).

ダウンロード操作を実行すると、名前が示すように、リポジトリからローカルシステムにフォームを書き出すことができます。 アップロード操作と組み合わせて、この操作を使用すると、あるリポジトリから別のリポジトリにフォームを移行する際に役立ちます。

AEM Formsでは、次のアセットタイプでダウンロード操作がサポートされています。

* フォームテンプレート (XFA Forms)
* PDF forms
* ドキュメント ( フラットPDFファイル )

AEM Formsでは、これらのフォームタイプを個別にダウンロードすることも、サポートされている 1 つ以上のフォームを含むフォルダーでダウンロードすることもできます。

これらのアセットの他に、`Resource` タイプのアセットもフォルダー内に存在すればダウンロードすることができます。この機能は、XFA フォームで参照されているリソースを、フォームとともにダウンロードできるようにするためのものです。

## 1 つまたは複数のフォームのダウンロード {#download-one-or-more-forms}

1. `https://<server>:<port>/aem/forms.html` で、AEM Forms のユーザーインターフェイスにログインします。

1. ダウンロードしたいアセットの場所に移動します。

1. アセットを選択します。ツールバーの「**[!UICONTROL ダウンロード]** ![aem6forms_download](assets/aem6forms_download.png)」アイコンをクリックします。

   >[!NOTE]
   >
   >ダウンロードするフォームは 1 つだけ選択できます。 複数のフォームをダウンロードする場合は、フォルダーとしてダウンロードする必要があります。

1. 表示されるダイアログボックスで、「**[!UICONTROL ダウンロード]**」をクリックします。

   AEM Formsは、選択したファイルまたはフォルダーを含む ZIP ファイルを生成します。

   フォルダーをダウンロードする場合は、フォルダー内のサポートされているアセットが既存の階層にダウンロードされます。

   ZIP ファイルは、ご利用のシステムの `Downloads` フォルダーに保存されます。

## アップロード操作に関する考慮事項 {#related-considerations-for-the-upload-operation}

* ZIP ファイルは、同じリポジトリ内の別の場所、または別のリポジトリにアップロードできます
* フォルダー内のアセットの階層は、アップロード操作時に保持されます
* ダウンロードされたアセットに対してダウンロード前に行われたメタデータの変更は、アップロード時に反映されます。
