---
title: JavaScript ファイルの縮小
seo-title: Minification of the JavaScript files
description: AEM Forms Workspace のカスタマイズ後に縮小コードを生成して Web 用の JS ファイルを最適化するための手順です。
seo-description: Instructions to generate minified code after AEM Forms workspace customizations to optimize the JS files for the web.
uuid: ad91e380-a988-4740-9534-e09657e0322a
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.4/FORMS
topic-tags: forms-workspace
discoiquuid: c88a3013-5da2-4b09-9f29-ac1fb00822ec
exl-id: 8394151e-e9cf-4f68-97a3-ba1d1dd6a2d2
source-git-commit: c5b816d74c6f02f85476d16868844f39b4c47996
workflow-type: tm+mt
source-wordcount: '219'
ht-degree: 37%

---

# JavaScript ファイルの縮小 {#minification-of-the-javascript-files}

>[!CAUTION]
>
>AEM 6.4 の拡張サポートは終了し、このドキュメントは更新されなくなりました。 詳細は、 [技術サポート期間](https://helpx.adobe.com/jp/support/programs/eol-matrix.html). サポートされているバージョンを見つける [ここ](https://experienceleague.adobe.com/docs/?lang=ja).

縮小により、ソースコードから、空白、新しい行、コメントなどの冗長な文字が削除されます。 これにより、コードのサイズが小さくなるので、パフォーマンスが向上します。 縮小化は機能に影響を与えませんが、コードの読みやすさが低下します。

セマンティックの変更用に縮小コードを生成するには、次の手順に従います。

1. src-package の `client-html/src/main/webapp/js` を filesystem にコピーします。

   >[!NOTE]
   >
   >パッケージに関する詳細については、「[AEM Forms Workspace のカスタマイズの概要](/help/forms/using/introduction-customizing-html-workspace.md)」を参照してください。

1. モデルやビューの追加または更新の場合は、client-html/src/main/webapp/js の下にある `main.js` のパスを更新します。

   たとえば、新しい Sharequeue モデル、mySharequeue を追加する場合は、

   ```
   sharequeuemodel : pathprefix + 'runtime/models/sharequeue',
   
   To
   
   sharequeuemodel : pathprefix + 'runtime/myModels/mySharequeue',
   ```

1. エイリアスの変更や追加が `main.js` にある場合は、`registry-config.xml, located at client-html/src/main/webapp/js/resource_generator,` をアップデートします。

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

1. client-html/src/main/webapp/js/minifier で、次のコマンドを実行します。

   ```shell
   mvn clean install
   ```

   client-html/src/main/webapp/js の下に、main.js と registry.js の縮小化されたフォルダー minified-files が生成されます。

>[!NOTE]
>
>縮小は 64 ビット JVM でのみ機能します。

>[!NOTE]
>
>縮小した場合は、アップグレードに影響が出ます。
