---
title: AEM 6.4 でのDynamic Mediaリポジトリの再構築
seo-title: Dynamic Media repository restructuring in AEM 6.4
description: AEM 6.4 での Dynamic Media の新しいリポジトリ構造に移行するために、必要な変更を加える方法について説明します。
seo-description: Learn how to make the necessary changes in order to migrate to the new repository structure in AEM 6.4 for Dynamic Media.
uuid: e26d61a4-47b6-493a-9ba2-4c58b200ddd9
products: SG_EXPERIENCEMANAGER/6.4/SITES
content-type: reference
topic-tags: repo_restructuring
discoiquuid: 61cd5751-0dc8-48e0-873e-3a64899489bb
feature: Upgrading
exl-id: 1323ee60-c80c-4eed-b3e5-aa0f0c07e6ee
source-git-commit: bd94d3949f0117aa3e1c9f0e84f7293a5d6b03b4
workflow-type: tm+mt
source-wordcount: '413'
ht-degree: 68%

---

# AEM 6.4 でのDynamic Mediaリポジトリの再構築{#dynamic-media-repository-restructuring-in-aem}

親の説明に従って [AEM 6.4 におけるリポジトリの再構築](/help/sites-deploying/repository-restructuring.md) このページでは、AEM 6.4 にアップグレードするお客様は、このページを使用して、Dynamic Mediaソリューションに影響を与えるリポジトリの変更に関連する作業量を評価する必要があります。 一部の変更は AEM 6.4 アップグレードプロセス中に作業が必要ですが、それ以外は 6.5 アップグレードまで延期できます。

**6.5 へのアップグレードまでにおこなう変更**

* [カスタム適応ビデオエンコーディング設定](/help/sites-deploying/dynamicmedia-repository-restructuring-in-aem-6-4.md#custom-adaptive-video-encoding-configurations)
* [Dynamic Media（DMS7）クラウド設定](/help/sites-deploying/dynamicmedia-repository-restructuring-in-aem-6-4.md#dynamic-media-dms-cloud-configuration)
* [Dynamic Media（DM ハイブリッド）クラウドサービスの設定](/help/sites-deploying/dynamicmedia-repository-restructuring-in-aem-6-4.md#cloudserviceconfiguration)
* [Dynamic Media - YouTube クラウドサービスの設定](/help/sites-deploying/dynamicmedia-repository-restructuring-in-aem-6-4.md#youtubecloudserviceconfiguration)
* [その他](/help/sites-deploying/dynamicmedia-repository-restructuring-in-aem-6-4.md#misc)

## 6.5 へのアップグレードまでにおこなう変更 {#prior-to-upgrade}

### カスタムアダプティブビデオエンコーディング設定  {#custom-adaptive-video-encoding-configurations}

<table> 
 <tbody>
  <tr>
   <td><strong>以前の場所</strong></td> 
   <td><code>/etc/dam/video/dynamicmedia</code></td> 
  </tr>
  <tr>
   <td><strong>新しい場所</strong></td> 
   <td><code>/conf/global/settings/dam/dm/presets/video/jcr:content</code></td> 
  </tr>
  <tr>
   <td><strong>再構築の手引き</strong></td> 
   <td><p>次の移行スクリプトを使用して、新しい場所に移行できます：</p> <p><em>https://serveraddress:serverport/libs/settings/dam/dm/presets.migratedmcontent.json</em></p> <p>または、AEM UI で設定を編集すると、変更内容が新しい場所に保存されます。</p> </td> 
  </tr>
  <tr>
   <td><strong>備考</strong></td> 
   <td>該当なし<br /> </td> 
  </tr>
 </tbody>
</table>

### Dynamic Media (DMS7) クラウド設定 {#dynamic-media-dms-cloud-configuration}

<table> 
 <tbody>
  <tr>
   <td><strong>以前の場所</strong></td> 
   <td><code>/etc/cloudservices/dmscene7</code></td> 
  </tr>
  <tr>
   <td><strong>新しい場所</strong></td> 
   <td><code>/conf/global/settings/cloudservices/dmscene7</code></td> 
  </tr>
  <tr>
   <td><strong>再構築の手引き</strong></td> 
   <td><p>ユーザーはこの場所で移行スクリプトを実行できます。<br /> </p> 
    <ul> 
     <li><em>https://serveraddress:serverport/libs/settings/dam/dm/presets.migratedmcontent.json</em></li> 
     <li>Dynamic Media OSGi バンドルを再起動します。</li> 
    </ul> </td> 
  </tr>
  <tr>
   <td><strong>備考</strong></td> 
   <td>該当なし</td> 
  </tr>
 </tbody>
</table>

### Dynamic Media(DM Hybrid)Cloud Service設定 {#cloudserviceconfiguration}

<table> 
 <tbody>
  <tr>
   <td><strong>以前の場所</strong></td> 
   <td><code>/etc/cloudservices/dynamicmediaservices</code></td> 
  </tr>
  <tr>
   <td><strong>新しい場所</strong></td> 
   <td><code>/conf/global/settings/dam/dm/cloudservices/dynamicmediaservices</code></td> 
  </tr>
  <tr>
   <td><strong>再構築の手引き</strong></td> 
   <td><p>最新のモデルに合わせるには、以下の移行スクリプトを実行できます:</p> <p><em>https://serveraddress:serverport/libs/settings/dam/dm/presets.migratedmcontent.jso</em></p> </td> 
  </tr>
  <tr>
   <td><strong>備考</strong></td> 
   <td>該当なし<br /> </td> 
  </tr>
 </tbody>
</table>

### Dynamic Media - YouTubeCloud Service設定  {#youtubecloudserviceconfiguration}

<table> 
 <tbody>
  <tr>
   <td><strong>以前の場所</strong></td> 
   <td><code>/etc/cloudservices/youtube</code></td> 
  </tr>
  <tr>
   <td><strong>新しい場所</strong></td> 
   <td><code>/libs/settings/dam/dm/youtube</code></td> 
  </tr>
  <tr>
   <td><strong>再構築の手引き</strong></td> 
   <td><p>1. YouTube からすべての動画を非公開にする<br /> 2.新しい TouchUI を使用したYouTube設定の作成 ( <code>/conf</code>) 古い場所からすべてのチャネルをコピーするを含む<br /> 3. すべての動画を YouTube に公開しなおします。</p> <p>このワークフローにより、新しいYouTube URL が生成されます。 新規のタッチ UI YouTube 設定を作成する前に非公開にしないと、再作成されたチャンネルは機会があれば再度公開されるため、プロパティの下に複数の YouTube URL が表示されます。つまり、プロパティの下に不要なURLが表示されていることになります。</p> </td> 
  </tr>
  <tr>
   <td><strong>備考</strong></td> 
   <td>該当なし<br /> </td> 
  </tr>
 </tbody>
</table>

### その他 {#misc}

<table> 
 <tbody>
  <tr>
   <td><strong>以前の場所</strong></td> 
   <td><code>/etc/dam/imageserver/macros</code></td> 
  </tr>
  <tr>
   <td><strong>新しい場所</strong></td> 
   <td><code>/conf/global/settings/dam/dm/presets/macro</code></td> 
  </tr>
  <tr>
   <td><strong>再構築の手引き</strong></td> 
   <td><p>ユーザーは以下の移行スクリプトを実行できます。</p> <p><em>https://serveraddress:serverport/libs/settings/dam/dm/presets.migratedmcontent.json</em></p> <p>または、AEM UI で設定を編集すると、変更内容が新しい場所に保存されます。</p> </td> 
  </tr>
  <tr>
   <td><strong>備考</strong></td> 
   <td>該当なし</td> 
  </tr>
 </tbody>
</table>

<table> 
 <tbody>
  <tr>
   <td><strong>以前の場所</strong></td> 
   <td><code>/etc/dam/presets/analytics</code></td> 
  </tr>
  <tr>
   <td><strong>新しい場所</strong></td> 
   <td><code>/libs/settings/dam/dm/analytics</code></td> 
  </tr>
  <tr>
   <td><strong>再構築の手引き</strong></td> 
   <td><p>ユーザーは以下の移行スクリプトを実行できます。</p> <p><em>https://serveraddress:serverport/libs/settings/dam/dm/presets.migratedmcontent.json</em></p> </td> 
  </tr>
  <tr>
   <td><strong>備考</strong></td> 
   <td>該当なし</td> 
  </tr>
 </tbody>
</table>
