---
title: 一括アセット移行用の機能パック18912のインストール
seo-title: 一括アセット移行用の機能パック18912のインストール
description: 機能パック18912では、FTPを使用してアセットを一括インジェストするか、AEMでDynamic Media Classicからダイナミックメディアにアセットを移行することができます。 このオプションの機能パックは、アドビサポートから入手できます。
seo-description: 機能パック18912では、FTPを使用してアセットを一括インジェストするか、AEMでDynamic Media Classicからダイナミックメディアにアセットを移行することができます。 このオプションの機能パックは、アドビサポートから入手できます。
uuid: 316d77e3-3d61-4cf0-8955-726ee54e268c
contentOwner: rbrough
products: SG_EXPERIENCEMANAGER/6.4/ASSETS
topic-tags: dynamic-media
content-type: reference
discoiquuid: 6198e613-a867-49a8-b9a5-a05e7889821c
translation-type: tm+mt
source-git-commit: e2bb2f17035e16864b1dc54f5768a99429a3dd9f

---


# Installing feature pack 18912 for bulk asset migration {#installing-feature-pack}

The installation of feature pack 18912 is _optional_.

機能パック18912では、FTP経由でアセットを直接ダイナミックメディア — AEMのScene7モードにバルクインジェストしたり、AEMでアセットをダイナミックメディアクラシックからダイナミックメディア — Scene7モードに移行したりできます。 この機能パックは、 [Adobe Professional Servicesから入手できます](https://www.adobe.com/experience-cloud/consulting-services.html)。

>[!NOTE]
>
>機能パックを使用して、AEMのDynamic Media ClassicからDynamic Media - Scene7モードにアセットを一括移行したり、Dynamic Media ClassicのFTP機能を使用してアセットを一括移行したりすることは可能ですが、複雑さのため ** 、この方法は推奨されません。
>
>そのため、このような移行機能パックは *、* Adobe Professional Servicesを使用した移行プロジェクトの一部としてのみサポートされます [](https://www.adobe.com/experience-cloud/consulting-services.html)。

この機能パックをインストールする前に、まずサービスユーザーを作成し、その情報をアドビに提供する必要があります。

See also [Configuring Dynamic Media - Scene7 mode](https://helpx.adobe.com/experience-manager/6-4/assets/using/config-dms7.html).

**一括アセット移行用の機能パック18912をインストールするには**、

1. In your AEM instance, navigate to **[!UICONTROL Tools > Security > Users > Create User]**. This service user must have read/write permissions to `/content/dam`.
1. 「**[!UICONTROL ID]**」および「**[!UICONTROL パスワード]**」フィールドで、ユーザー名およびパスワードを入力します（例：`FTP User`）。この名前は、アセットを作成したユーザーとしてタイムラインに表示されます。アセットが FTP からアップロードされる場合、アセットは、FTP サーバーにアップロードされて AEM にプッシュされる際に作成されたと見なされます。
1. Experience Managerのアドビエ [ンタープライズサポートに問い合わせて](https://helpx.adobe.com/contact/enterprise-support.ec.html) 、機能パック18912のダウンロードをリクエストします。 サポートに問い合わせる際には、次の情報が必要になる場合があります。

   * 作成者インスタンスのサーバーIPアドレス。ポート番号を含みます（デフォルトでは、ポート番号は4502）。
   * 前の手順のAEMサービスのユーザー名とパスワード。

1. AEMのアドビエンタープライズサポートでは、FTP証明書と機能パック18912へのアクセスを提供します。

1. 機能パック18912を受け取ったら、インストールします。

   See [How to work with packages](/help/sites-administering/package-manager.md) for more information on using Package Share and packages in AEM.

