---
title: 複数のアセットおよびコレクションのメタデータの一括編集
description: 多数のアセットやコレクションのメタデータを同時に編集して、共通のメタデータの変更をすばやく反映する方法を説明します。
contentOwner: AG
feature: Asset Management,Metadata,Collections
role: User
exl-id: 3541b50a-f226-4a6a-9c2a-03a5f47f1c23
source-git-commit: c5b816d74c6f02f85476d16868844f39b4c47996
workflow-type: tm+mt
source-wordcount: '469'
ht-degree: 56%

---

# 複数のアセットやコレクションの管理 {#managing-multiple-assets-and-collections}

>[!CAUTION]
>
>AEM 6.4 の拡張サポートは終了し、このドキュメントは更新されなくなりました。 詳細は、 [技術サポート期間](https://helpx.adobe.com/jp/support/programs/eol-matrix.html). サポートされているバージョンを見つける [ここ](https://experienceleague.adobe.com/docs/?lang=ja).

複数のアセットやコレクションのメタデータを同時に編集して、共通のメタデータの変更をすばやく反映する方法を説明します。

AdobeEnterprise Manager Assets では、複数のアセットのメタデータを同時に編集できるので、共通のメタデータの変更をアセットに一括ですばやく反映できます。 複数のコレクションのメタデータを一括して編集することもできます。

プロパティページを使用して、複数のアセットまたはコレクションに対してメタデータの変更を実行します。

* メタデータのプロパティを共通の値に変更
* タグを追加または変更

メタデータのプロパティページをカスタマイズ（メタデータのプロパティの追加、変更、削除など）するには、スキーマエディターを使用します。

>[!NOTE]
>
>一括編集メソッドは、フォルダーまたはコレクションで使用可能なアセットに対して機能します。フォルダー全体で使用可能なアセットや共通の条件に一致するアセットについては、アセット検索結果からメタデータを一括更新することができます。

## 複数アセットのメタデータプロパティの編集 {#editing-metadata-properties-of-multiple-assets}

1. Assets ユーザーインターフェイスで、編集するアセットの場所に移動します。
1. 共通のプロパティを編集するアセットを選択します。
1. ツールバーで「**[!UICONTROL プロパティ]**」をクリックして、選択したアセットのプロパティページを開きます。
1. 様々なタブで選択したアセットのメタデータプロパティを変更します。
1. 特定のアセットのメタデータを表示するには、リストの残りのアセットの選択をキャンセルします。[!UICONTROL プロパティ]ページでいくつかのアセットの選択をキャンセルした場合、それらのアセットのメタデータは更新されません。
1. アセットに別のメタデータスキーマを選択するには、ツールバーの「**[!UICONTROL 設定]**」をクリックし、スキーマを選択します。「**[!UICONTROL 保存して閉じる]**」をクリックします。
1. 複数の値が含まれるフィールドで、既存のメタデータに新しいメタデータを追加するには、「**[!UICONTROL 追加モード]**」を選択します。このオプションを選択しないと、フィールド内の既存のメタデータが新しいメタデータに置換されます。「**[!UICONTROL 送信]**」をクリックします。

![複数のアセットへのメタデータスキーマの一括適用](assets/metadata-schema-bulk-edit.gif)

>[!CAUTION]
>
>1 つの値のみを指定できるフィールドの場合、「**[!UICONTROL 追加モード]**」を選択しても、フィールド内の既存の値に新しいメタデータが追加されません。

## 一括メタデータ更新の上限を設定する {#configure-limit-for-bulk-metadata-update}

DOS のような状況を防ぐには、 [!DNL Experience Manager] は、Sling 要求でサポートされるパラメーターの数を制限します。 一度に多くのアセットのメタデータを更新すると、上限に到達する可能性があり、それ以上のアセットでメタデータが更新されなくなります。[!DNL Experience Manager] によって、ログに次の警告が生成されます。

`org.apache.sling.engine.impl.parameters.Util Too many name/value pairs, stopped processing after 10000 entries`

制限を変更するには、**[!UICONTROL ツール／操作／Web コンソール]**&#x200B;にアクセスし、[!UICONTROL Apache Sling Request Parameter Handling] OSGi 設定で [!UICONTROL Maximum POST Parameters] の値を変更します。

>[!MORELIKETHIS]
>
>* [複数コレクションのメタデータの一括編集](managing-collections-touch-ui.md#editing-collection-metadata-in-bulk)

