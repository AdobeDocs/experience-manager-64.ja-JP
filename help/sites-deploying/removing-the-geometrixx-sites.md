---
title: Geometrixx サイトの削除
seo-title: Removing the Geometrixx Sites
description: サンプルの Geometrixx コンテンツの削除方法について説明します。
seo-description: Learn how to remove the sample Geometrixx content.
uuid: 07d20837-3375-4e64-bb07-3e4d10452335
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.4/SITES
content-type: reference
discoiquuid: 56761a36-ce21-46e1-856f-75a7e94acae9
exl-id: 495031fb-b559-4071-abc4-93d238ce136d
source-git-commit: bd94d3949f0117aa3e1c9f0e84f7293a5d6b03b4
workflow-type: tm+mt
source-wordcount: '132'
ht-degree: 100%

---

# Geometrixx サイトの削除{#removing-the-geometrixx-sites}

AEM には一連の Geometrixx サンプル Web サイトが付属しています。このサンプルコンテンツを&#x200B;**パッケージマネージャー**&#x200B;経由で削除できます。

geometrixx 関連の個別のパッケージは次のとおりです。

* `cq-geometrixx-outdoors-ugc-pkg-*<version>*.zip`
* `cq-geometrixx-pkg-*<version>*.zip`
* `cq-content-mac-*<version>*.zip`
* `cq-geometrixx-login-pkg-*<version>*.zip`
* `cq-geometrixx-users-pkg-*<version>*.zip`
* `cq-geometrixx-workflow-pkg-*<version>*.zip`
* `cq-geometrixx-outdoors-pkg-*<version>*.zip`
* `cq-geometrixx-commons-pkg-*<version>*.zip`
* `cq-geometrixx-media-pkg-*<version>*.zip`

個別のパッケージを削除するには、そのパッケージで「**アンインストール**」をクリックします。

また、以下のスーパーパッケージがあります。

* `cq-geometrixx-all-pkg-5.6.12.zip`

このパッケージには、上記の個々のパッケージがすべて含まれています。すべての geometrixx 関連のコンテンツを一度に削除するには、このパッケージの「**アンインストール**」をクリックします。スーパーパッケージが未インストールの状態になり、個々のパッケージはすべて、パッケージマネージャーに表示されなくなります。

これで、デモンストレーションサイトが含まれない「空の」AEM インスタンスが作成されます。

>[!NOTE]
>
>アップグレードの際には、geometrixx サイトが自動的に再作成されます。これらのサンプルが不要な場合は、アップグレード後に geometrixx Web サイトを削除する必要があります。
