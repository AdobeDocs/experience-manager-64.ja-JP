---
title: 埋め込むフォントの指定
seo-title: Specify fonts to embed
description: 埋め込むフォントを指定する方法を説明します。
seo-description: Learn how to specify fonts to embed.
uuid: 02da5c00-0467-4633-a076-c36725cbfbad
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_output
products: SG_EXPERIENCEMANAGER/6.4/FORMS
discoiquuid: 180f0448-d507-4b6d-bb8a-d12a434e1250
exl-id: e24f4123-bed3-4096-b3fb-22deb1c1e9b9
source-git-commit: c5b816d74c6f02f85476d16868844f39b4c47996
workflow-type: tm+mt
source-wordcount: '287'
ht-degree: 24%

---

# 埋め込むフォントの指定{#specify-fonts-to-embed}

>[!CAUTION]
>
>AEM 6.4 の拡張サポートは終了し、このドキュメントは更新されなくなりました。 詳細は、 [技術サポート期間](https://helpx.adobe.com/jp/support/programs/eol-matrix.html). サポートされているバージョンを見つける [ここ](https://experienceleague.adobe.com/docs/?lang=ja).

Output で使用されるフォームに常に埋め込むフォントと埋め込まないフォントを指定できます。 フォントを埋め込むと、フォームのファイルサイズが大きくなります。 ユーザーがシステムに持っていない可能性の高い珍しいフォントを埋め込み、インストールする一般的なフォントを埋め込みません。

>[!NOTE]
>
>Output のカスタム XCI ファイルを指定した場合、XCI ファイルのフォントの埋め込みオプションがこれらの設定よりも優先されます。 ( [Output のファイルの場所を指定](/help/forms/using/admin-help/specify-file-locations-output.md#specify-file-locations-for-output).)

1. 管理コンソールで、サービス／Output をクリックします。
1. 「フォントの埋め込み設定」の「常に埋め込むフォント」ボックスに、フォームに埋め込むフォントの名前をコンマで区切って入力します。指定したフォントは、生成後のフォームに埋め込まれます（フォーム内で使用されている場合）。 サービスに渡される XCI ファイルで、埋め込みフォントオプションがオンになっている場合、この設定は無視されます。 その場合、PDFで使用されるすべてのフォントが常に埋め込まれます。
1. 「常に埋め込まないフォント」ボックスで、フォームに埋め込まないフォントの名前をコンマで区切って入力します。指定したフォントは、生成されたPDFで使用されている場合でも、PDFに埋め込まれません。 サービスに渡される XCI ファイルで、埋め込みフォントオプションがオフになっている場合、この設定は無視されます。 その場合、埋め込まれるフォントはPDFにはありません。
1. 「保存」をクリックします。
