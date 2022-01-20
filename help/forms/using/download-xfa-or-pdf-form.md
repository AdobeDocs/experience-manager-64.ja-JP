---
title: XFA または PDF フォームテンプレートのダウンロード
seo-title: Download an XFA or a PDF form template
description: リポジトリからローカルシステムへとフォームをエクスポートし、ダウンロードされたフォームを新しいリポジトリに移行することができます。
seo-description: You can export forms from the repository to the local system and migrate the downloaded forms to new repository.
uuid: 5f7fbd14-cb9d-4749-8708-7efe49df89d7
content-type: reference
products: SG_EXPERIENCEMANAGER/6.4/FORMS
topic-tags: forms-manager
discoiquuid: 6699e0e7-fd42-41ae-86a2-3b940d905111
role: Admin
exl-id: 68d881c6-7507-4018-b40e-205604221d0c
source-git-commit: 3c050c33a384d586d74bd641f7622989dc1d6b22
workflow-type: tm+mt
source-wordcount: '313'
ht-degree: 87%

---

# XFA または PDF フォームテンプレートのダウンロード {#download-an-xfa-or-a-pdf-form-template}

ダウンロード操作では、その名のとおり、リポジトリからローカルシステムへとフォームをエクスポートすることができます。アップロード操作と組み合わせることにより、リポジトリから別のリポジトリへとフォームを移行することができます。

AEM Forms では、ダウンロード操作は次のアセットタイプに対してサポートされています。

* フォームテンプレート（XFA フォーム）
* PDF のフォーム
* ドキュメント（非インタラクティブ PDF ファイル）

AEM Forms では、これらのフォームタイプを個別にダウンロードするか、サポートされているフォームを 1 つまたは複数含むフォルダでダウンロードすることができます。

これらのアセットの他に、 `Resource` アセットがフォルダー内に存在する場合は、そのアセットのタイプ。 この機能は、XFA フォームによって参照されているリソースを、フォームとともにダウンロードできるようにするためのものです。

## 1 つまたは複数のフォームのダウンロード {#download-one-or-more-forms}

1. `https://<server>:<port>/aem/forms.html` で、AEM Forms ユーザーインターフェイスにログインします。

1. ダウンロードしたいアセットの場所に移動します。

1. アセットを選択します。次をクリック： **[!UICONTROL ダウンロード]** ![aem6forms_download](assets/aem6forms_download.png) アイコンをクリックします。

   >[!NOTE]
   >
   >ダウンロードするフォームは 1 つだけ選択することができます。複数のフォームをダウンロードしたい場合は、フォルダーとしてダウンロードする必要があります。

1. 表示されるダイアログボックスで、**[!UICONTROL ダウンロード]**&#x200B;をクリックします。

   AEM Forms が、選択されたファイルまたはフォルダーを含む ZIP ファイルを生成します。

   フォルダーをダウンロードする場合、フォルダー内のサポートされているアセットが、既存の階層にダウンロードされます。

   ZIP ファイルは、 `Downloads` フォルダーを設定します。

## アップロード操作に関する考慮事項 {#related-considerations-for-the-upload-operation}

* ZIP ファイルは、同じリポジトリ内の別のロケーション、もしくは別のリポジトリにアップロードすることができます。
* フォルダー内のアセットの階層は、アップロード操作の間も保持されます。
* ダウンロードされたアセットに対してダウンロード前に行われたメタデータの変更は、アップロード時に反映されます。
