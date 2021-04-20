---
title: 一括アセット移行のための機能パック18912のインストール
seo-title: 一括アセット移行のための機能パック18912のインストール
description: 機能パック18912では、FTPを使用してアセットを一括インジェストするか、AEMのDynamic MediaクラシックからDynamic Mediaにアセットを移行できます。 このオプションの機能パックは、アドビサポートから入手できます。
seo-description: 機能パック18912では、FTPを使用してアセットを一括インジェストするか、AEMのDynamic MediaクラシックからDynamic Mediaにアセットを移行できます。 このオプションの機能パックは、アドビサポートから入手できます。
uuid: 316d77e3-3d61-4cf0-8955-726ee54e268c
contentOwner: rbrough
products: SG_EXPERIENCEMANAGER/6.4/ASSETS
topic-tags: dynamic-media
content-type: reference
discoiquuid: 6198e613-a867-49a8-b9a5-a05e7889821c
exl-id: f9bb59f6-39a5-4804-8abe-12783d4162c9
feature: Configuration
role: Administrator,Business Practitioner
translation-type: tm+mt
source-git-commit: 13eb1d64677f6940332a2eeb4d3aba2915ac7bba
workflow-type: tm+mt
source-wordcount: '429'
ht-degree: 20%

---

# 一括アセット移行用の機能パック18912をインストールしています{#installing-feature-pack}

機能パック18912のインストールは&#x200B;_オプション_&#x200B;です。

機能パック18912では、FTP経由でアセットを直接Dynamic Media- AEMのScene7モードにバルクインジェストしたり、AEMでDynamic MediaクラシックからDynamic Media-Scene7モードにアセットを移行したりできます。 この機能パックは[Adobe Professional Services](https://www.adobe.com/jp/experience-cloud/consulting-services.html)から入手できます。

>[!NOTE]
>
>機能パックを使用して、AEMのDynamic MediaクラシックからDynamic Media- Scene7モードにアセットを一括移行したり、Dynamic MediaクラシックのFTP機能を使用してアセットを一括移行することは可能ですが、Adobeは複雑さのため、この方法を推奨しません。**
>
>したがって、このような移行機能パックは、[Adobe Professional Services](https://www.adobe.com/experience-cloud/consulting-services.html)を介した移行プロジェクトの一部として&#x200B;*のみ*&#x200B;サポートされます。

この機能パックをインストールする前に、サービスユーザーを作成し、Adobeに提供する必要があります。

[Dynamic Mediaの設定 —Scene7モード](https://helpx.adobe.com/jp/experience-manager/6-4/assets/using/config-dms7.html)も参照してください。

**一括アセット移行用の機能パック18912をインストールするには**、

1. AEMインスタンスで、**[!UICONTROL ツール/セキュリティ/ユーザー/ユーザーを作成]**&#x200B;に移動します。 このサービスユーザーは、`/content/dam`に対する読み取り/書き込み権限が必要です。
1. 「**[!UICONTROL ID]**」および「**[!UICONTROL パスワード]**」フィールドで、ユーザー名およびパスワードを入力します（例：`FTP User`）。この名前は、アセットを作成したユーザーとしてタイムラインに表示されます。アセットが FTP からアップロードされる場合、アセットは、FTP サーバーにアップロードされて AEM にプッシュされる際に作成されたと見なされます。
1. Experience Manager](https://helpx.adobe.com/jp/contact/enterprise-support.ec.html)のAdobeエンタープライズサポートに問い合わせて、機能パック18912のダウンロードを依頼します。 [サポートに問い合わせる際には、次の情報が必要になる場合があります。

   * 作成者インスタンスのサーバーIPアドレス。ポート番号（デフォルトでは、ポート番号は4502）を含みます。
   * 前の手順のAEMサービスユーザー名とパスワード。

1. AEMAdobeエンタープライズサポートでは、FTP資格情報と機能パック18912へのアクセスが提供されます。

1. 機能パック18912を受け取ったら、インストールします。

   AEMでのソフトウェア配布とパッケージの使い方の詳細は、[パッケージの使い方](/help/sites-administering/package-manager.md)を参照してください。
