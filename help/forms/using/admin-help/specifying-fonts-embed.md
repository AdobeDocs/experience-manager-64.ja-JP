---
title: 埋め込むフォントの指定
seo-title: Specifying fonts to embed
description: 埋め込むフォントの指定方法について説明します。
seo-description: Learn how to specify fonts to embed.
uuid: 97de6f98-ed3b-4a93-854a-193a967b4672
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_forms
products: SG_EXPERIENCEMANAGER/6.4/FORMS
discoiquuid: 4c83694c-b00f-40be-9ac4-f5785cd60741
exl-id: 0bde7192-9d21-40b4-9164-314c9a30153b
source-git-commit: bd94d3949f0117aa3e1c9f0e84f7293a5d6b03b4
workflow-type: tm+mt
source-wordcount: '250'
ht-degree: 79%

---

# 埋め込むフォントの指定 {#specifying-fonts-to-embed}

Forms サービスで生成されるフォームに常に埋め込むフォント、または埋め込まないフォントを指定できます。フォントを埋め込むと、フォームのファイルサイズが大きくなります。ユーザーのシステムに通常存在しない珍しいフォントを埋め込みます。通常インストールされているような一般的なフォントは埋め込まないでください。

>[!NOTE]
>
>Forms のカスタム XCI ファイルを指定している場合、これらの設定より、XCI ファイルのフォントの埋め込みオプションが優先されます（[Forms の場所の設定](/help/forms/using/admin-help/configuring-locations-forms.md#configuring-locations-for-forms)を参照）。

1. 管理コンソールで、 **[!UICONTROL サービス/Forms]**.
1. の下 **[!UICONTROL フォント埋め込み設定]**、 **[!UICONTROL 常にフォントを埋め込む]** ボックスに、フォームに埋め込むフォントの名前をコンマで区切って入力します。 指定するフォントは、生成されたフォームで使用されている場合にのみそのフォームに埋め込まれます。サービスに渡される XCI ファイルでフォントの埋め込みオプションが有効になっていると、この設定は無視されます。この場合は、PDF で使用されるすべてのフォントが常に埋め込まれるためです。
1. 内 **[!UICONTROL フォントを埋め込まない]** 」ボックスに、フォームに埋め込まないフォントの名前をコンマで区切って入力します。 指定するフォントは、生成された PDF で使用されていてもその PDF に埋め込まれません。サービスに渡される XCI ファイルでフォントの埋め込みオプションが無効になっていると、この設定は無視されます。この場合は、PDF で使用されるフォントが一切埋め込まれないためです。
1. 「**[!UICONTROL 保存]**」をクリックします。
