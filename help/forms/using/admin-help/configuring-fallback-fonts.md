---
title: 代替フォントの設定
seo-title: Configuring fallback fonts
description: 代替フォントの設定方法について説明します。
seo-description: Learn how to configure fallback fonts.
uuid: 2745541c-8c6d-4bb4-aa14-ec19afd6bc35
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/working_with_pdf_generator
products: SG_EXPERIENCEMANAGER/6.4/FORMS
discoiquuid: d997a268-a40a-462d-badd-94f0731f7ba4
feature: PDF Generator
exl-id: 6942b6fc-8d04-429f-8433-1ab74c68fcc1
source-git-commit: bd94d3949f0117aa3e1c9f0e84f7293a5d6b03b4
workflow-type: tm+mt
source-wordcount: '254'
ht-degree: 69%

---

# 代替フォントの設定 {#configuring-fallback-fonts}

デフォルトのフォントがサーバーでは使用できない場合に、FontManagerResources.properties ファイルを手動で設定して、デフォルトの AEM forms のフォントを代替フォントにマップすることができます。このプロパティファイルは、adobe-fontmanager.jar ファイルにあります。

>[!NOTE]
>
>代替フォントの設定は Assembler サービスにも適用されます。

1. adobe-livecycle-*[appserver]*.ear ファイル ( *[aem-forms ルート]*/configurationManager/export ディレクトリを作成し、バックアップコピーを作成して、元のディレクトリのパッケージ化を解除します。
1. adobe-fontmanager.jar ファイルを検索し、展開します。
1. FontManagerResources.properties ファイルを検索し、テキストエディターで開きます。
1. 必要に応じて汎用フォントと代替フォントの場所と名前を変更し、ファイルを保存します。

   FontManagerResources.properties ファイルのフォントエントリは、 *[aem-forms ルート]*/fonts ディレクトリに保存します。 デフォルトの AEM forms フォントではないフォントを指定する場合は、このディレクトリ構造内（既存のディレクトリ内または新しく作成したディレクトリ内）にそれらのフォントをインストールする必要があります。

   >[!NOTE]
   >
   >指定したフォントまたはデフォルトのフォントに特定の Unicode 文字が含まれない場合や使用できない場合、その文字は次の優先度に従って代替フォントから取得されます。

   * ロケール固有のフォント
   * ロケールが設定されていない場合は ROOT フォント
   * 代替テーブルで設定された順序で検索される汎用フォント

1. adobe-fontmanager.jar ファイルを再パッケージ化します。
1. adobe-livecycle-*[appserver]*.ear ファイルを編集し、手動で、または Configuration Manager を実行して再デプロイします。

>[!NOTE]
>
>Configuration Manager を使用して adobe-livecycle-[appserver].ear ファイルを編集すると、変更内容がAEM forms のデフォルト値で上書きされるので、.ear ファイルを編集します。
