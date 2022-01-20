---
title: 一括アセット移行用の機能パック18912のインストール
seo-title: Installing Feature Pack 18912 for bulk asset migration
description: 機能パック18912では、FTP を使用してアセットを一括取り込むことも、AEMでDynamic Media ClassicからDynamic Mediaにアセットを移行することもできます。 このオプションの機能パックは、アドビサポートから入手できます。
seo-description: Feature pack 18912 lets you either bulk ingest assets by way of FTP, or migrate assets from Dynamic Media Classic to Dynamic Media in AEM. This optional feature pack is available from Adobe support.
uuid: 316d77e3-3d61-4cf0-8955-726ee54e268c
contentOwner: rbrough
products: SG_EXPERIENCEMANAGER/6.4/ASSETS
topic-tags: dynamic-media
content-type: reference
discoiquuid: 6198e613-a867-49a8-b9a5-a05e7889821c
exl-id: f9bb59f6-39a5-4804-8abe-12783d4162c9
feature: Configuration
role: Admin,User
source-git-commit: 63a4304a1a10f868261eadce74a81148026390b6
workflow-type: tm+mt
source-wordcount: '388'
ht-degree: 20%

---

# 一括アセット移行用の機能パック18912をインストールしています {#installing-feature-pack}

機能パック18912のインストールは次のとおりです。 _オプション_.

機能パック18912では、FTP を使用してアセットをDynamic Media - AEMの Scene7 モードに直接一括取り込むか、Dynamic Media ClassicからAEMのDynamic Media - Scene7モードにアセットを移行することができます。 機能パックは、次の場所から入手できます。 [Adobe Professional Services](https://www.adobe.com/jp/experience-cloud/consulting-services.html).

>[!NOTE]
>
>機能パックを使用してDynamic Media ClassicからDynamic Media - AEMの Scene7 モードにアセットを一括移行することも、Dynamic Media Classicの FTP 機能を使用してアセットを一括移行することもできますが、Adobeでは *not* 複雑なので、この方法をお勧めします。
>
>そのため、このような移行機能パックは次のようになります。 *のみ* を通じた移行プロジェクトの一環としてサポートされる [Adobe Professional Services](https://www.adobe.com/experience-cloud/consulting-services.html).

この機能パックをインストールする前に、まずサービスユーザを作成し、その情報をAdobeに提供する必要があります。

関連トピック [Dynamic Media - Scene7モードの設定](https://helpx.adobe.com/jp/experience-manager/6-4/assets/using/config-dms7.html).

**一括アセット移行用の機能パック18912をインストールするには**,

1. AEMインスタンスで、に移動します。 **[!UICONTROL [ ツール ] > [ セキュリティ ] > [ ユーザ ] > [ ユーザの作成 ]]**. このサービスユーザーは、 `/content/dam`.
1. 「**[!UICONTROL ID]**」および「**[!UICONTROL パスワード]**」フィールドで、ユーザー名およびパスワードを入力します（例：`FTP User`）。この名前は、アセットを作成したユーザーとしてタイムラインに表示されます。アセットが FTP からアップロードされる場合、アセットは、FTP サーバーにアップロードされて AEM にプッシュされる際に作成されたと見なされます。
1. 連絡先 [AdobeのExperience Managerカスタマーサポート](https://helpx.adobe.com/jp/contact/enterprise-support.ec.html) 機能パック18912へのアクセス権をリクエストしてダウンロードします。 サポートに連絡する際には、次の情報が必要になる場合があります。

   * オーサーインスタンスのサーバー IP アドレス。ポート番号（デフォルトでは、ポート番号は 4502）を含みます。
   * 前の手順で作成したAEMサービスのユーザー名とパスワード。

1. AdobeのAEMカスタマーサポートでは、FTP 資格情報と機能パック18912へのアクセス権が提供されます。

1. 機能パック18912を受け取ったら、インストールします。

   詳しくは、 [パッケージの操作方法](/help/sites-administering/package-manager.md) AEMでのソフトウェア配布およびパッケージの使用に関する詳細
