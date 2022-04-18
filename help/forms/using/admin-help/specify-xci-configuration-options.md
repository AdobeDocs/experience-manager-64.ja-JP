---
title: XCI 設定オプションの指定
seo-title: Specify XCI configuration options
description: XCI 設定オプションの指定方法について説明します。
seo-description: Learn how to specify XCI configuration options.
uuid: cf9e544d-63cd-4fad-8f89-bdb46eeef409
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_output
products: SG_EXPERIENCEMANAGER/6.4/FORMS
discoiquuid: f38ebd69-8d1c-49b6-824f-4bf0ec8a8953
exl-id: 5156bb1c-8ad6-498c-aaf7-6474ffa8c83c
source-git-commit: bd94d3949f0117aa3e1c9f0e84f7293a5d6b03b4
workflow-type: tm+mt
source-wordcount: '129'
ht-degree: 100%

---

# XCI 設定オプションの指定 {#specify-xci-configuration-options}

Output では、レンダリングに使用するカスタム XCI ファイルを指定できます（[Output のファイルの場所の指定](/help/forms/using/admin-help/specify-file-locations-output.md#specify-file-locations-for-output)を参照）。デフォルトでは、Output が、以下をはじめとする XCI ファイルで指定されている一部のオプションより優先されます。

* `config/present/xdp/packets`
* `config/present/pdf/creator`
* `config/present/pdf/producer`
* `config/present/pdf/compression/compressObjectStream`

前述のオプションの上書きをキャンセルするオプションを選択できます。この場合、Output では、カスタム XCI ファイルで指定されている値が使用されます。

1. 管理コンソールで、サービス／Output をクリックします。
1. 「システムデフォルトの XCI オプションを使用」チェックボックスをオンまたはオフにします。このオプションを選択すると、Output では、パケット、作成者、プロデューサーおよび compressObjectStream の設定にデフォルト値が使用されます。このオプションを選択しない場合、Output では、カスタム XCI ファイルで指定された値が使用されます。
1. 「保存」をクリックしてください。
