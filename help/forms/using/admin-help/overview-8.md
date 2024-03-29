---
title: Output サービスの概要
seo-title: Overview of output service
description: Output では、XML フォームデータを Designer で作成されたフォームデザインと結合して、様々な形式のドキュメント出力ストリームを作成できます。
seo-description: Output lets you merge XML form data with a form design created in Designer to create a document output stream in various formats.
uuid: 7890b0a6-bae5-4ad5-ae41-503b988ba3da
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_output
products: SG_EXPERIENCEMANAGER/6.4/FORMS
discoiquuid: 5a96f5ea-6fe3-44b1-b314-14097b9e9c01
exl-id: 00ca8bdf-77be-4f4c-a3d3-d61d13eeba7e
source-git-commit: c5b816d74c6f02f85476d16868844f39b4c47996
workflow-type: tm+mt
source-wordcount: '301'
ht-degree: 10%

---

# Output サービスの概要 {#overview-of-output-service}

>[!CAUTION]
>
>AEM 6.4 の拡張サポートは終了し、このドキュメントは更新されなくなりました。 詳細は、 [技術サポート期間](https://helpx.adobe.com/jp/support/programs/eol-matrix.html). サポートされているバージョンを見つける [ここ](https://experienceleague.adobe.com/docs/?lang=ja).

Output では、XML フォームデータを Designer で作成されたフォームデザインと結合して、様々な形式のドキュメント出力ストリームを作成できます。 出力ストリームは、ネットワークプリンタ、ローカルプリンタ、またはディスクファイルに送信できます

管理コンソールの Output ページを使用して、Output サービスを管理できます。 設定した設定は、実行時に、対応する設定がAEM forms API で指定されていない場合に使用されます。 AEM forms SDK での設定は、管理コンソールでの設定よりも優先されます。

Output サービスについて詳しくは、 [サービスリファレンス](https://www.adobe.com/go/learn_aemforms_services_61).

管理コンソールの Output ページでは、次の複数のタスクを実行できます。

* 国際化の文字セットを指定します。 ( [文字セットの変更](/help/forms/using/admin-help/change-character-set.md#change-the-character-set).)
* URL、URI、XCI、ファイルの場所の絶対パスと相対パスを指定します。 ( [Output のファイルの場所を指定](/help/forms/using/admin-help/specify-file-locations-output.md#specify-file-locations-for-output).)
* キャッシュサイズとポリシーを設定します。 ( [キャッシュモードの指定](/help/forms/using/admin-help/configuring-caching-output.md#specifying-the-cache-mode) および [キャッシュ設定の指定](/help/forms/using/admin-help/configuring-caching-output.md#configuring-cache-settings).)
* フォントをアプリケーションサーバーで使用できるようにします。 ( [フォントを使用可能にする](/help/forms/using/admin-help/make-fonts-available.md#make-fonts-available).)
* 埋め込むフォントの指定.( [埋め込むフォントの指定](/help/forms/using/admin-help/specify-fonts-embed.md#specify-fonts-to-embed).)
* XCI 設定オプションの指定.( [XCI 設定オプションの指定](/help/forms/using/admin-help/specify-xci-configuration-options.md#specify-xci-configuration-options).)
* セキュリティ設定の指定.( [セキュリティ設定の指定](/help/forms/using/admin-help/specify-security-settings.md#specify-security-settings).)

設定を変更した後、「保存」をクリックして、設定を「出力」に適用します。 変更を有効にするためにサーバーを再起動する必要はありませんが、キャッシュ設定を構成する際に Output サービスの再起動が必要になる場合があります。
