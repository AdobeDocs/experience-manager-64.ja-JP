---
title: 一括アセット移行のための機能パック18912のインストール
seo-title: 一括アセット移行のための機能パック18912のインストール
description: 機能パック18912では、FTPを使用してアセットを一括インジェストするか、アセットをDynamic MediaクラシックからAEMのDynamic Mediaに移行できます。 このオプションの機能パックは、アドビサポートから入手できます。
seo-description: 機能パック18912では、FTPを使用してアセットを一括インジェストするか、アセットをDynamic MediaクラシックからAEMのDynamic Mediaに移行できます。 このオプションの機能パックは、アドビサポートから入手できます。
uuid: 316d77e3-3d61-4cf0-8955-726ee54e268c
contentOwner: rbrough
products: SG_EXPERIENCEMANAGER/6.4/ASSETS
topic-tags: dynamic-media
content-type: reference
discoiquuid: 6198e613-a867-49a8-b9a5-a05e7889821c
translation-type: tm+mt
source-git-commit: b1603091bb05493c9cfffa6067f414f73774edb2
workflow-type: tm+mt
source-wordcount: '428'
ht-degree: 20%

---


# Installing feature pack 18912 for bulk asset migration {#installing-feature-pack}

The installation of feature pack 18912 is _optional_.

機能パック18912では、FTP経由でアセットを直接Dynamic Media- AEMのScene7モードに一括インジェストするか、Dynamic MediaClassicからDynamic Media- AEMのScene7モードに移行できます。 この機能パックは、 [Adobe Professional Servicesから入手できます](https://www.adobe.com/jp/experience-cloud/consulting-services.html)。

>[!NOTE]
>
>機能パックを使用して、Dynamic MediaクラシックからDynamic Mediaにアセットを一括移行することもできますが、Dynamic MediaクラシックのFTP機能を使用した一括移行は可能です ** 。複雑さが原因で、この方法をお勧めしません。
>
>したがって、このような移行機能パックは、 *Adobe Professional Servicesを通じた移行プロジェクトの一部としての* みサポートされます [](https://www.adobe.com/jp/experience-cloud/consulting-services.html)。

この機能パックをインストールする前に、サービスユーザーを作成し、その情報をアドビに提供する必要があります。

See also [Configuring Dynamic Media - Scene7 mode](https://helpx.adobe.com/jp/experience-manager/6-4/assets/using/config-dms7.html).

**一括アセット移行用の機能パック18912をインストールするには**、

1. In your AEM instance, navigate to **[!UICONTROL Tools > Security > Users > Create User]**. This service user must have read/write permissions to `/content/dam`.
1. 「**[!UICONTROL ID]**」および「**[!UICONTROL パスワード]**」フィールドで、ユーザー名およびパスワードを入力します（例：`FTP User`）。この名前は、アセットを作成したユーザーとしてタイムラインに表示されます。アセットが FTP からアップロードされる場合、アセットは、FTP サーバーにアップロードされて AEM にプッシュされる際に作成されたと見なされます。
1. 機能パック18912のダウンロードをリクエストするには、 [Experience Manager](https://helpx.adobe.com/jp/contact/enterprise-support.ec.html) (Adobe Enterprise Support)にお問い合わせください。 サポートに問い合わせる際には、次の情報が必要になる場合があります。

   * 作成者インスタンスのサーバーIPアドレス。ポート番号（デフォルトでは、ポート番号は4502）を含みます。
   * 前の手順のAEMサービスユーザー名とパスワード。

1. AEMのアドビエンタープライズサポートでは、FTP資格情報と機能パック18912へのアクセス権を提供します。

1. 機能パック18912を受け取ったら、インストールします。

   See [How to work with packages](/help/sites-administering/package-manager.md) for more information on using Software Distribution and packages in AEM.
