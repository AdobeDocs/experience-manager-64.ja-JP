---
title: Geometrixxサイトの削除
seo-title: Removing the Geometrixx Sites
description: サンプルGeometrixxコンテンツの削除方法を説明します。
seo-description: Learn how to remove the sample Geometrixx content.
uuid: 07d20837-3375-4e64-bb07-3e4d10452335
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.4/SITES
content-type: reference
discoiquuid: 56761a36-ce21-46e1-856f-75a7e94acae9
exl-id: 495031fb-b559-4071-abc4-93d238ce136d
source-git-commit: c5b816d74c6f02f85476d16868844f39b4c47996
workflow-type: tm+mt
source-wordcount: '168'
ht-degree: 11%

---

# Geometrixxサイトの削除{#removing-the-geometrixx-sites}

>[!CAUTION]
>
>AEM 6.4 の拡張サポートは終了し、このドキュメントは更新されなくなりました。 詳細は、 [技術サポート期間](https://helpx.adobe.com/jp/support/programs/eol-matrix.html). サポートされているバージョンを見つける [ここ](https://experienceleague.adobe.com/docs/?lang=ja).

AEMには、一連のサンプルGeometrixxWeb サイトが付属しています。 このサンプルコンテンツは、 **パッケージマネージャー**.

geometrixx 関連の個々のパッケージは次のとおりです。

* `cq-geometrixx-outdoors-ugc-pkg-*<version>*.zip`
* `cq-geometrixx-pkg-*<version>*.zip`
* `cq-content-mac-*<version>*.zip`
* `cq-geometrixx-login-pkg-*<version>*.zip`
* `cq-geometrixx-users-pkg-*<version>*.zip`
* `cq-geometrixx-workflow-pkg-*<version>*.zip`
* `cq-geometrixx-outdoors-pkg-*<version>*.zip`
* `cq-geometrixx-commons-pkg-*<version>*.zip`
* `cq-geometrixx-media-pkg-*<version>*.zip`

個々のパッケージを削除するには、シンプルクリック **アンインストール** その荷物に

また、スーパーパッケージもあります。

* `cq-geometrixx-all-pkg-5.6.12.zip`

このパッケージには、上記の個々のパッケージがすべて含まれています。 geometrixx 関連のすべてのコンテンツを一度に削除するには、 **アンインストール** をこのパッケージに追加します。 スーパーパッケージはアンインストール済みの状態になり、個々のパッケージはすべてパッケージマネージャービューから消えます。

これで、デモンストレーションサイトが含まれない「空の」AEM インスタンスが作成されます。

>[!NOTE]
>
>アップグレード時に、geometrixx サイトが自動的に再インストールされます。 これらのサンプルが不要な場合は、アップグレード後に geometrixx Web サイトを削除する必要が生じる場合があります。
