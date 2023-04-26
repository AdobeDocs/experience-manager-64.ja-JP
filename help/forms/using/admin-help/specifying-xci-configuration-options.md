---
title: XCI 設定オプションの指定
seo-title: Specifying XCI configuration options
description: XCI 設定オプションを指定する方法について説明します。
seo-description: Learn how to specify XCI configuration options.
uuid: 5d3c10c1-4a93-4336-b311-20faaf835b9f
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_forms
products: SG_EXPERIENCEMANAGER/6.4/FORMS
discoiquuid: 162c9fda-f4d4-4ad5-a9ab-7554828e821c
exl-id: 7a13b13f-3eee-4fc0-8957-bd42f43119e9
source-git-commit: bd94d3949f0117aa3e1c9f0e84f7293a5d6b03b4
workflow-type: tm+mt
source-wordcount: '130'
ht-degree: 12%

---

# XCI 設定オプションの指定 {#specifying-xci-configuration-options}

Formsでは、レンダリングに使用するカスタム XCI ファイルを指定できます。 ( [Formsの場所の設定](/help/forms/using/admin-help/configuring-locations-forms.md#configuring-locations-for-forms).) デフォルトでは、Formsは、次のオプションなど、XCI ファイルで指定された一部のオプションを上書きします。

* `config/present/xdp/packets`
* `config/present/pdf/creator`
* `config/present/pdf/producer`
* `config/present/pdf/compression/compressObjectStream`

上記のオプションの上書きをキャンセルするオプションを選択できます。この場合、Formsはカスタム XCI ファイルで指定された値を使用します。

1. 管理コンソールで、サービス／Forms をクリックします。
1. 「 Use System Default XCI Options 」チェックボックスをオンまたはオフにします。 このオプションを選択すると、Formsはパケット、作成者、プロデューサー、compressObjectStream の設定にデフォルト値を使用します。 このオプションの選択を解除すると、Formsはカスタム XCI ファイルで指定された値を使用します。
1. 「保存」をクリックします。
