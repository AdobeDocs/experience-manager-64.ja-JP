---
title: 埋め込むフォントの指定
seo-title: Specifying fonts to embed
description: 埋め込むフォントを指定する方法を説明します。
seo-description: Learn how to specify fonts to embed.
uuid: 97de6f98-ed3b-4a93-854a-193a967b4672
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_forms
products: SG_EXPERIENCEMANAGER/6.4/FORMS
discoiquuid: 4c83694c-b00f-40be-9ac4-f5785cd60741
exl-id: 0bde7192-9d21-40b4-9164-314c9a30153b
source-git-commit: c5b816d74c6f02f85476d16868844f39b4c47996
workflow-type: tm+mt
source-wordcount: '286'
ht-degree: 24%

---

# 埋め込むフォントの指定 {#specifying-fonts-to-embed}

>[!CAUTION]
>
>AEM 6.4 の拡張サポートは終了し、このドキュメントは更新されなくなりました。 詳細は、 [技術サポート期間](https://helpx.adobe.com/jp/support/programs/eol-matrix.html). サポートされているバージョンを見つける [ここ](https://experienceleague.adobe.com/docs/?lang=ja).

Formsサービスで生成されるフォームに常に埋め込むフォントと埋め込まないフォントを指定できます。 フォントを埋め込むと、フォームのファイルサイズが大きくなります。 ユーザーがごく一般的でないフォントをシステムに埋め込みます。 一般的にインストールされている一般的なフォントは埋め込まないでください。

>[!NOTE]
>
>Formsのカスタム XCI ファイルを指定した場合、XCI ファイルのフォントの埋め込みオプションがこれらの設定よりも優先されます。 ( [Formsの場所の設定](/help/forms/using/admin-help/configuring-locations-forms.md#configuring-locations-for-forms).)

1. 管理コンソールで、**[!UICONTROL サービス／Forms]** をクリックします。
1. 「**[!UICONTROL フォントの埋め込み設定]**」の「**[!UICONTROL 常に埋め込むフォント]**」ボックスに、フォームに埋め込むフォントの名前をコンマで区切って入力します。指定したフォントは、生成後のフォームに埋め込まれます（フォーム内で使用されている場合）。 サービスに渡される XCI ファイルでフォントの埋め込みオプションがオンになっている場合、このPDFは無視されます。この場合、フォントで使用されるすべてのフォントが常に埋め込まれるからです。
1. 「**[!UICONTROL 常に埋め込まないフォント]**」ボックスで、フォームに埋め込まないフォントの名前をコンマで区切って入力します。指定したフォントは、生成されたPDFで使用されている場合でも、PDFに埋め込まれません。 サービスに渡される XCI ファイルでフォントの埋め込みオプションがオフになっている場合、このPDFは無視されます。この場合、フォントで使用されるフォントは埋め込まれないからです。
1. 「**[!UICONTROL 保存]**」をクリックします。
