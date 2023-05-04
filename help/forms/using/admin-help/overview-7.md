---
title: Forms 設定の基本事項
seo-title: Basics of configuring forms
description: インタラクティブなデータキャプチャアプリケーションを作成するのに役立つ様々なフォームサービスについて説明します。
seo-description: Learn about the various forms services that help you create interactive data capture applications.
uuid: f495c170-2d17-45b0-b09d-22cce101131e
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_forms
products: SG_EXPERIENCEMANAGER/6.4/FORMS
discoiquuid: e87c7379-28ed-4fda-aef1-970d2b54f30d
exl-id: 616cd550-c3bd-4daf-887d-0470f1b08389
source-git-commit: c5b816d74c6f02f85476d16868844f39b4c47996
workflow-type: tm+mt
source-wordcount: '237'
ht-degree: 9%

---

# Forms 設定の基本事項 {#basics-of-configuring-forms}

>[!CAUTION]
>
>AEM 6.4 の拡張サポートは終了し、このドキュメントは更新されなくなりました。 詳細は、 [技術サポート期間](https://helpx.adobe.com/jp/support/programs/eol-matrix.html). サポートされているバージョンを見つける [ここ](https://experienceleague.adobe.com/docs/?lang=ja).

Formsサービスを使用すると、通常 Designer で作成されるフォームを検証、処理、変換および配信する、インタラクティブなデータキャプチャクライアントアプリケーションを作成できます。 フォーム作成者は、Formsサービスが様々な形式でレンダリングする単一のフォームデザインを作成します。

* Adobe ReaderまたはブラウザーでのPDFとして
* XHTML 1.0 に準拠したレンダリングを含む、様々なブラウザー環境でのHTMLとして
* をフォームガイドとして使用します。これは、AdobeFlash Playerをサポートする様々なブラウザ環境で使用されます。

Formsサービスについて詳しくは、 [サービスリファレンス](https://www.adobe.com/go/learn_aemforms_services_63).

管理コンソールのFormsページを使用して、Formsサービスの動作を設定できます。 これらの設定は、サービスのすべての呼び出しに適用されます。 AEM forms SDK を通じて送信されるパラメーターは、管理コンソールで設定された設定より優先されます。ただし、影響を受けるのは特定の呼び出しのみです。

管理コンソールでForms設定を変更したら、「保存」をクリックします。 変更を有効にするために、サーバーを再起動する必要はありません。 ただし、キャッシュモードの設定を行う場合は、Formsサービスの停止と再起動が必要になる場合があります。 ( [サービスの開始と停止](/help/forms/using/admin-help/starting-stopping-services.md#starting-and-stopping-services).)
