---
title: 複数のアセットとコレクションのメタデータを一括編集
description: 多数のアセットとコレクションのメタデータを同時に編集し、一般的なメタデータの変更をすばやく反映する方法について説明します。
contentOwner: AG
translation-type: tm+mt
source-git-commit: 97bb17ce719f82449e28f9b32eb651b632b0f8b5
workflow-type: tm+mt
source-wordcount: '524'
ht-degree: 77%

---


# Manage multiple assets and collections {#managing-multiple-assets-and-collections}

複数のアセットおよびコレクションのメタデータを同時に編集して、共通のメタデータの変更をすばやくプロパゲートする方法を学習します。

Adobe Enterprise Manager（AEM）Assets を使用すると、複数のアセットのメタデータを同時に編集できるので、アセットに対して共通のメタデータの変更をすばやく一括でプロパゲートできます。複数のコレクションのメタデータを同時に編集することもできます。

プロパティページを使用して、複数のアセットまたはコレクションのメタデータを変更できます。

* メタデータプロパティを共通の値に変更する
* タグを追加または変更する

メタデータのプロパティページをカスタマイズ（メタデータのプロパティの追加、編集、削除など）するには、スキーマエディターを使用します。

>[!NOTE]
>
>一括編集メソッドは、フォルダーまたはコレクションで使用可能なアセットに対して機能します。複数のフォルダーで使用できるアセットや共通の条件に一致するアセットについては、アセット検索結果からメタデータを一括して更新できます。

## Edit metadata properties of multiple assets {#editing-metadata-properties-of-multiple-assets}

1. Assets ユーザーインターフェイスで、編集するアセットの場所に移動します。
1. 共通のプロパティを編集するアセットを選択します。
1. ツールバーで「]**プロパティ**[!UICONTROL 」アイコンをタップまたはクリックして、選択したアセットのプロパティページを開きます。

   >[!NOTE]
   >
   >複数のアセットを選択すると、それらのアセットに対して最も下位の共通親フォームが選択されます。つまり、プロパティページには、すべての個々のアセットのプロパティページに共通のメタデータフィールドのみが表示されます。

1. 様々なタブで選択したアセットのメタデータプロパティを変更します。
1. 特定のアセットのメタデータエディターを表示するには、リストの残りのアセットの選択を解除します。メタデータエディターのフィールドには、その特定のアセットのメタデータが入力されています。

   >[!NOTE]
   >
   >* プロパティページで、アセットのリストからアセットの選択を解除することでそのアセットを削除できます。アセットリストは、デフォルトではすべてのアセットが選択されています。リストから削除するアセットのメタデータは更新されていません。
   >* アセットリストの上部で、「**タイトル**」の横にあるチェックボックスをオンにして、アセットの選択とリストの消去を切り替えます。


1. アセットに別のメタデータスキーマを選択するには、ツールバーの「]**設定**[!UICONTROL 」アイコンをタップまたはクリックし、目的のスキーマを選択します。
1. 変更内容を保存します。
1. 複数の値が含まれるフィールドで、既存のメタデータに新しいメタデータを追加するには、「**[!UICONTROL 追加モード]**」を選択します。このオプションを選択しないと、フィールド内の既存のメタデータが新しいメタデータに置換されます。「**[!UICONTROL 送信]**」をタップまたはクリックします。

   >[!CAUTION]
   >
   >1 つの値のみを指定できるフィールドの場合、「**[!UICONTROL 追加モード]**」を選択しても、フィールド内の既存の値に新しいメタデータが追加されません。

## 一括メタデータ更新の上限を設定する {#configure-limit-for-bulk-metadata-update}

DOS などの状況を防ぐため、AEM では Sling 要求でサポートされるパラメーターの数を制限しています。一度に多くのアセットのメタデータを更新すると、上限に到達する可能性があり、それ以上のアセットでメタデータが更新されなくなります。AEM はログに次の警告を生成します。

`org.apache.sling.engine.impl.parameters.Util Too many name/value pairs, stopped processing after 10000 entries`

To change the limit, access **[!UICONTROL Tools > Operations > Web Console]** and change the value of [!UICONTROL Maximum POST Parameters] in [!UICONTROL Apache Sling Request Parameter Handling] OSGi configuration.

>[!MORELIKETHIS]
>
>* [複数のコレクションのメタデータを一括で編集](managing-collections-touch-ui.md#editing-collection-metadata-in-bulk)