---
title: JavaScript ファイルの縮小
seo-title: Minification of the JavaScript files
description: AEM Forms Workspace をカスタマイズした後で JS ファイルを Web 用に最適化するための縮小コードを生成する手順。
seo-description: Instructions to generate minified code after AEM Forms workspace customizations to optimize the JS files for the web.
uuid: ad91e380-a988-4740-9534-e09657e0322a
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.4/FORMS
topic-tags: forms-workspace
discoiquuid: c88a3013-5da2-4b09-9f29-ac1fb00822ec
exl-id: 8394151e-e9cf-4f68-97a3-ba1d1dd6a2d2
source-git-commit: bd94d3949f0117aa3e1c9f0e84f7293a5d6b03b4
workflow-type: tm+mt
source-wordcount: '183'
ht-degree: 83%

---

# JavaScript ファイルの縮小 {#minification-of-the-javascript-files}

縮小では、ソースコードから余白、復帰改行、コメントなどの冗長文字を削除します。これにより、コードのサイズが削減されてパフォーマンスが向上します。縮小は機能に影響しませんが、コードの可読性を削減します。

セマンティックの変更のための縮小コードを生成するには、次の手順に従います。

1. コピー `client-html/src/main/webapp/js` ファイルシステムの src-package から

   >[!NOTE]
   >
   >パッケージに関する詳細については、「[AEM Forms Workspace のカスタマイズの概要](/help/forms/using/introduction-customizing-html-workspace.md)」を参照してください。

1. でパスを更新 `main.js` 追加/更新されたモデル/ビューの場合は、client-html/src/main/webapp/js の下に配置されます。

   たとえば、新しい Sharequeue モデル、mySharequeue を追加する場合は、

   ```
   sharequeuemodel : pathprefix + 'runtime/models/sharequeue',
   
   To
   
   sharequeuemodel : pathprefix + 'runtime/myModels/mySharequeue',
   ```

1. 更新 `registry-config.xml, located at client-html/src/main/webapp/js/resource_generator,` エイリアスの変更や追加が `main.js`.

   たとえば、新しい Sharequeue モデル、mySharequeue を追加する場合は、

   ```xml
   <sharequeue
               name="sharequeue"
               path="runtime/models/sharequeue.js"
               service="service"/>
   
   To
   
   <sharequeue
               name="sharequeue"
               path="runtime/myModels/mySharequeue.js"
               service="service"/>
   ```

1. client-html/src/main/webapp/js/minifier で、コマンド：

   ```shell
   mvn clean install
   ```

   これにより、client-html/src/main/webapp/js の下に縮小された main.js と registry.js と共に縮小されたファイルのフォルダーが生成されます。

>[!NOTE]
>
>縮小は 64 ビット VM でのみ機能します。

>[!NOTE]
>
>縮小した場合は、アップグレードに影響が出ます。
