---
title: 一括アセット移行用の機能パック18912のインストール
seo-title: 一括アセット移行用の機能パック18912のインストール
description: 機能パック18912では、FTPを使用してアセットを一括で取り込むか、AEMのDynamic Media ClassicからDynamic Mediaにアセットを移行できます。 このオプションの機能パックは、アドビサポートから入手できます。
seo-description: 機能パック18912では、FTPを使用してアセットを一括で取り込むか、AEMのDynamic Media ClassicからDynamic Mediaにアセットを移行できます。 このオプションの機能パックは、アドビサポートから入手できます。
uuid: 316d77e3-3d61-4cf0-8955-726ee54e268c
contentOwner: rbrough
products: SG_EXPERIENCEMANAGER/6.4/ASSETS
topic-tags: dynamic-media
content-type: reference
discoiquuid: 6198e613-a867-49a8-b9a5-a05e7889821c
exl-id: f9bb59f6-39a5-4804-8abe-12783d4162c9
feature: 設定
role: Admin,User
source-git-commit: 5d96c09ef764b02e08dcdf480da1ee18f4d9a30c
workflow-type: tm+mt
source-wordcount: '429'
ht-degree: 20%

---

# 一括アセット移行用の機能パック18912をインストールしています {#installing-feature-pack}

機能パック18912のインストールは&#x200B;_オプション_&#x200B;です。

機能パック18912では、AEM上のDynamic Media - Scene7モードにFTPを使用して直接アセットを一括で取り込むか、Dynamic Media ClassicからAEM上のDynamic Media - Scene7モードにアセットを移行できます。 この機能パックは、[Adobe Professional Services](https://www.adobe.com/jp/experience-cloud/consulting-services.html)から入手できます。

>[!NOTE]
>
>機能パックを使用して、Dynamic Media ClassicからDynamic Media - AEMのScene7モードにアセットを一括移行することも、Dynamic Media ClassicのFTP機能を使用してアセットを一括移行することもできますが、複雑さのため、Adobeではこの方法を推奨しません。**
>
>そのため、このような移行機能パックは、[Adobe Professional Services](https://www.adobe.com/experience-cloud/consulting-services.html)を介した移行プロジェクトの一部として&#x200B;*のみ*&#x200B;サポートされています。

この機能パックをインストールする前に、まずサービスユーザーを作成し、その情報をAdobeに提供する必要があります。

[Dynamic Media - Scene7モード](https://helpx.adobe.com/jp/experience-manager/6-4/assets/using/config-dms7.html)の設定も参照してください。

**一括アセット移行用の機能パック18912をインストールするには**:

1. AEMインスタンスで、**[!UICONTROL ツール/セキュリティ/ユーザー/ユーザーを作成]**&#x200B;に移動します。 このサービスユーザーは、`/content/dam`に対する読み取り/書き込み権限を持っている必要があります。
1. 「**[!UICONTROL ID]**」および「**[!UICONTROL パスワード]**」フィールドで、ユーザー名およびパスワードを入力します（例：`FTP User`）。この名前は、アセットを作成したユーザーとしてタイムラインに表示されます。アセットが FTP からアップロードされる場合、アセットは、FTP サーバーにアップロードされて AEM にプッシュされる際に作成されたと見なされます。
1. [Experience Manager](https://helpx.adobe.com/jp/contact/enterprise-support.ec.html)のAdobeエンタープライズサポートに連絡して、ダウンロード用の機能パック18912へのアクセスをリクエストします。 サポートに連絡する際には、次の情報が必要になる場合があります。

   * オーサーインスタンスのサーバーIPアドレス（ポート番号を含む）（デフォルトでは、ポート番号は4502）。
   * 前の手順で作成したAEMサービスのユーザー名とパスワード。

1. Adobeエンタープライズサポート(AEM)では、FTP資格情報と機能パック18912へのアクセスが提供されます。

1. 機能パック18912を受け取ったら、インストールします。

   AEMでのソフトウェア配布とパッケージの使用について詳しくは、[パッケージ](/help/sites-administering/package-manager.md)の使用方法を参照してください。
