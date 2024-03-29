---
title: アダプティブフォームの再利用
seo-title: Reusing adaptive forms
description: 既存のアダプティブフォームを再利用して、新しいアダプティブフォームを作成することができます。
seo-description: You can reuse an existing adaptive form to create new adaptive forms.
uuid: f1d0fb70-e255-4dd9-8e6d-fd65eaf2e81a
products: SG_EXPERIENCEMANAGER/6.4/FORMS
topic-tags: author
discoiquuid: ef564750-f107-41cb-887e-fc6d22b7d32e
feature: Adaptive Forms
exl-id: 9393fe94-002a-497b-9579-d6ad3bb3973e
source-git-commit: c5b816d74c6f02f85476d16868844f39b4c47996
workflow-type: tm+mt
source-wordcount: '574'
ht-degree: 64%

---

# アダプティブフォームの再利用 {#reusing-adaptive-forms}

>[!CAUTION]
>
>AEM 6.4 の拡張サポートは終了し、このドキュメントは更新されなくなりました。 詳細は、 [技術サポート期間](https://helpx.adobe.com/jp/support/programs/eol-matrix.html). サポートされているバージョンを見つける [ここ](https://experienceleague.adobe.com/docs/?lang=ja).

## はじめに {#introduction}

既存のアダプティブフォームの一部のプロパティを使用して新しいアダプティブフォームを生成する場合は、単純にコピー&amp;ペースト機能を使用できます。 さらに、新しいアダプティブフォームを目的のフォルダーパスに貼り付けることができます。 すべてのメタデータプロパティが複製され、XFA ベースのアダプティブフォームの XFA と XSD ベースのアダプティブフォームの XSD もコピーされます。

>[!NOTE]
>
>ステータスとレビューの詳細はコピーされません。例えば、アダプティブフォームが発行された後でコピーした場合、貼り付けられたアダプティブフォームは非公開の状態になります。 同様に、コピーされたアセットがレビュー中の場合、貼り付けられたアセットは同じレビュー中とはなりません。

### アダプティブフォームのコピー {#copy-an-adaptive-form}

次のいずれかの方法を使用してアダプティブフォームをコピーします。

1. クイックアクションからコピー ![aem6forms_copy](assets/aem6forms_copy.png) アイコンをクリックします。

   >[!NOTE]
   >
   >クイックアクションは、マウスのカーソルを合わせたときにサムネール上に表示されるアクション項目です。

1. アダプティブフォームを選択します。 選択方法はビューによって異なります。

   カードビューの場合は、選択 ![aem6forms_check-circle](assets/aem6forms_check-circle.png) アイコンをクリックして選択モードに移行し、コピーするすべてのアダプティブフォームをクリックします。

   リスト表示の場合は、選択するすべてのアダプティブフォームのチェックボックスをオンにします。

   >[!NOTE]
   >
   >コピーと貼り付けの機能はアダプティブフォームのみをサポートしていますので、選択したアセットはすべてアダプティブフォームである必要があります。また、選択したすべてのアセットは同じフォルダー内のものである必要があります。

   アセットを選択したら、ツールバーにあるコピー ![aem6forms_copy](assets/aem6forms_copy.png) アイコンをクリックして、選択したアダプティブフォームをコピーします。

### アダプティブフォームの貼り付け {#paste-an-adaptive-form}

コピーアクションをクリックすると、選択モードが自動的に終了し、貼り付け ![aem6forms_paste](assets/aem6forms_paste.png) アイコンが表示されます。必要なフォルダーパスに移動して貼り付け ![aem6forms_paste](assets/aem6forms_paste.png) アイコンをクリックし、コピーしたアダプティブフォームを貼り付けます。

同じフォルダー内に貼り付ける場合、または貼り付け先のフォルダー内に同じノード名（CRX リポジトリへの保存に使用される名前）の別のファイルがある場合は、接尾辞に 1 が追加されます（例えば、myaf は myaf1 となり、同じ場所に myaf1 がある場合は myaf が myaf2 になります）。その他のプロパティは、元のアダプティブフォームと同じです。

貼り付け ![aem6forms_paste](assets/aem6forms_paste.png) アイコンをクリックすると、アイコンは再び非表示になります。一度に行える貼り付け操作は一回だけです。同じアセットのコピーを再び作成するには、再度アセットをコピーします。

### 新しいアダプティブフォームのコンテンツの変更 {#change-contents-of-new-adaptive-form}

貼り付けたアダプティブフォームのコンテンツは、次の方法で変更し、コピーしたフォームとは異なる内容にすることができます。

1. **メタデータプロパティの変更：**

   タイトルや説明など、アダプティブフォームのメタデータプロパティを変更できます。メタデータプロパティとその変更方法について詳しくは、 [フォームメタデータの管理](/help/forms/using/manage-form-metadata.md) を参照してください。

1. **XFA/XSD ベースのアダプティブフォームの XFA/XSD の変更：**

   アダプティブフォームで使用される XFA/XSD を変更できます。 これらのアダプティブフォームの変更方法については、 [フォームメタデータの管理](/help/forms/using/manage-form-metadata.md)

1. **再公開：**

   貼り付けられたアセットは、コピーされたアセットとは異なります。 エンドユーザーが使用できるように、新しいアセットとして公開することができます。アセットの公開方法については、 [フォームの発行と非公開](/help/forms/using/publishing-unpublishing-forms.md)
