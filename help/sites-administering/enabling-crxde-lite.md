---
title: AEM での CRXDE Lite の有効化
seo-title: Enabling CRXDE Lite in AEM
description: AEMでCRXDE Liteを有効にする方法を説明します。
seo-description: Learn how to enable CRXDE Lite in AEM.
uuid: d7a3db67-6384-463b-9aa9-f08ecc6c99c6
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.4/SITES
topic-tags: Security
content-type: reference
discoiquuid: 72df3ece-badf-466b-8f9a-0ec985d87741
exl-id: 3d8dc987-2ff9-4f71-bc07-48018caa3af4
source-git-commit: bd94d3949f0117aa3e1c9f0e84f7293a5d6b03b4
workflow-type: tm+mt
source-wordcount: '212'
ht-degree: 75%

---

# AEM での CRXDE Lite の有効化 {#enabling-crxde-lite-in-aem}

AEMのインストールを可能な限り安全にするために、セキュリティチェックリストでは、 [WebDAV の無効化](/help/sites-administering/security-checklist.md#disable-webdav) 実稼動環境で使用できます。

ただし、CRXDE Lite が正しく機能するには `org.apache.sling.jcr.davex` バンドルに依存するので、WebDAV を無効にすると CRXDE Lite も無効になります。

これが発生すると、`https://serveraddress:4502/crx/de/index.jsp` にアクセスするときに空のルートノードが表示され、CRXDE Lite のリソースへのすべての HTTP リクエストが失敗します。

```xml
404 Resource at '/crx/server/crx.default/jcr:root/.1.json' not found: No resource found
```

この推奨事項は攻撃対象領域を可能な限り減らすことを目的としていますが、システム管理者はコンテンツの参照や実稼動インスタンスの問題をデバッグするために CRXDE Lite にアクセスする必要がある場合があります。

無効にした場合、CRXDE Lite をオンにするには次の手順を実行します。

1. OSGi コンポーネントコンソール（`http://localhost:4502/system/console/components`）に移動します。
1. 次のコンポーネントを検索します。

   * `org.apache.sling.jcr.davex.impl.servlets.SlingDavExServlet`

1. その設定オプションを確認するには、その横にあるレンチのアイコンをクリックします。

   ![chlimage_1-80](assets/chlimage_1-80.png)

1. 次の設定を作成します。

   * **ルートパス：** `/crx/server`
   * 「**絶対 URI を使用**」ボックスにチェックマークを入れます。

1. CRXDE Lite の使用が終わったら、再度 WebDAV を無効にしてください。

次のコマンドを実行して、cURL 経由でCRXDE Liteを有効にすることもできます。

```shell
curl -u admin:admin -F "jcr:primaryType=sling:OsgiConfig" -F "alias=/crx/server" -F "dav.create-absolute-uri=true" -F "dav.create-absolute-uri@TypeHint=Boolean" http://localhost:4502/apps/system/config/org.apache.sling.jcr.davex.impl.servlets.SlingDavExServlet
```

## その他のリソース {#other-resources}

AEM 6 のセキュリティ機能について詳しくは、次のページを参照してください。

* [AEM セキュリティチェックリスト](/help/sites-administering/security-checklist.md)
* [実稼動準備モードでの AEM の実行](/help/sites-administering/production-ready.md)
