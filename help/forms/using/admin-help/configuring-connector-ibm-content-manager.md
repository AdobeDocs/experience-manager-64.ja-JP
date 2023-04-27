---
title: Connector for IBM Content Manager の設定
seo-title: Configuring Connector for IBM Content Manager
description: AEM forms とIBM Content Manager 間の通信を有効にするように、Connector for IBM Content Manager を設定します。
seo-description: Configure the Connector for IBM Content Manager to enable communication between AEM forms and IBM Content Manager.
uuid: 3d55169d-93e3-4d4e-b18b-2a3394e1de3b
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/connecting_to_a_content_management_system
products: SG_EXPERIENCEMANAGER/6.4/FORMS
discoiquuid: 3094b178-3b1a-46b3-8fbd-c20388afa3a7
exl-id: 8c65531e-f4f0-4cc4-b328-eaefb5662cf1
source-git-commit: bd94d3949f0117aa3e1c9f0e84f7293a5d6b03b4
workflow-type: tm+mt
source-wordcount: '277'
ht-degree: 7%

---

# Connector for IBM Content Manager の設定{#configuring-connector-for-ibm-content-manager}

Connector for IBM Content Manager は、AEM forms とIBM Content Manager 間の通信を可能にします。 その他の背景情報については、 [サービスリファレンス](https://www.adobe.com/go/learn_aemforms_services_63).

## IBM Content Manager 接続の設定 {#configure-the-ibm-content-manager-connection}

1. 管理コンソールで、サービス/IBM Content Manager 用コネクタをクリックします。
1. 「データストア名」ボックスに、接続先のIBM Content Manager データストアの名前を入力します。 データベースがローカルの場合は、データベースの名前を入力します。 データベースがリモートの場合は、そのエイリアス名を入力します。
1. 「 User Name 」ボックスに、IBM Content Manager データストアに接続するユーザーのユーザー ID を入力します。
1. 「パスワード」ボックスに、ユーザーのパスワードを入力します。
1. （オプション）「Alias Connection String」ボックスに、追加の接続引数を入力します。 ほとんどの場合、このボックスは空にする必要があります。 詳しくは、IBMのドキュメントを参照してください。
1. 「保存」をクリックします。

## サービス設定の検証 {#validation-of-service-settings}

誤った dataStore のエイリアス、ユーザー名またはパスワードを入力した場合は、IBM Content Manager サービス用の Content Repository Connector が現在実行中かどうかに応じて、次の結果が返されます。

* サービスが停止している場合は、サービス構成情報を保存したときに、エラーは表示されません。 ただし、次回サービスを開始する際には例外が発生し、サービスは開始されません。
* サービスが起動した場合、サービス構成情報を保存すると、サービスは資格情報の検証を直ちに試みます。 この場合、エラーが発生し、設定情報は保存されません。
