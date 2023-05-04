---
title: XCI 設定オプションの指定
seo-title: Specify XCI configuration options
description: XCI 設定オプションを指定する方法について説明します。
seo-description: Learn how to specify XCI configuration options.
uuid: cf9e544d-63cd-4fad-8f89-bdb46eeef409
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_output
products: SG_EXPERIENCEMANAGER/6.4/FORMS
discoiquuid: f38ebd69-8d1c-49b6-824f-4bf0ec8a8953
exl-id: 5156bb1c-8ad6-498c-aaf7-6474ffa8c83c
source-git-commit: c5b816d74c6f02f85476d16868844f39b4c47996
workflow-type: tm+mt
source-wordcount: '165'
ht-degree: 14%

---

# XCI 設定オプションの指定 {#specify-xci-configuration-options}

>[!CAUTION]
>
>AEM 6.4 の拡張サポートは終了し、このドキュメントは更新されなくなりました。 詳細は、 [技術サポート期間](https://helpx.adobe.com/jp/support/programs/eol-matrix.html). サポートされているバージョンを見つける [ここ](https://experienceleague.adobe.com/docs/?lang=ja).

Output では、レンダリングに使用するカスタム XCI ファイルを指定できます。 ( [Output のファイルの場所を指定](/help/forms/using/admin-help/specify-file-locations-output.md#specify-file-locations-for-output).) デフォルトでは、Output は、次のオプションなど、XCI ファイルで指定された一部のオプションよりも優先されます。

* `config/present/xdp/packets`
* `config/present/pdf/creator`
* `config/present/pdf/producer`
* `config/present/pdf/compression/compressObjectStream`

上記のオプションの上書きをキャンセルするオプションを選択できます。この場合、Output ではカスタム XCI ファイルで指定された値が使用されます。

1. 管理コンソールで、サービス／Output をクリックします。
1. 「 Use System Default XCI Options 」チェックボックスをオンまたはオフにします。 このオプションを選択すると、Output はパケット、クリエイター、プロデューサー、compressObjectStream の設定にデフォルト値を使用します。 このオプションの選択を解除すると、Output ではカスタム XCI ファイルで指定された値が使用されます。
1. 「保存」をクリックしてください。
