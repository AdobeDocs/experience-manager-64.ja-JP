---
title: AEM 6.4 における Assets リポジトリの再構築
seo-title: Assets Repository Restructuring in AEM 6.4
description: AEM 6.4 for Assets の新しいリポジトリ構造に移行するために必要な変更を加える方法について説明します。
seo-description: Learn how to make the necessary changes in order to migrate to the new repository structure in AEM 6.4 for Assets.
uuid: 0e3d8163-6274-4d1b-91c7-32ca927fb83c
products: SG_EXPERIENCEMANAGER/6.4/SITES
content-type: reference
topic-tags: repo_restructuring
discoiquuid: 212930fc-3430-4a0a-842c-2fb613ef981f
feature: Upgrading
exl-id: 3d5bbf95-bd1e-453b-b487-517a56fe727f
source-git-commit: cda63b9ece88d8172fa4d9817e315c9cff88c224
workflow-type: tm+mt
source-wordcount: '1113'
ht-degree: 49%

---

# AEM 6.4 における Assets リポジトリの再構築{#assets-repository-restructuring-in-aem}

親の説明に従って [AEM 6.4 におけるリポジトリの再構築](/help/sites-deploying/repository-restructuring.md) このページでは、AEM 6.4 にアップグレードするお客様は、このページを使用して、AEM Assetsソリューションに影響を与えるリポジトリの変更に関連する作業量を評価する必要があります。 一部の変更は AEM 6.4 アップグレードプロセス中に作業が必要ですが、それ以外は 6.5 アップグレードまで延期できます。

**6.4 へのアップグレード時におこなう変更**

* [その他](https://experienceleague.adobe.com/docs/experience-manager-64/deploying/restructuring/assets-repository-restructuring-in-aem-6-4.html#misc)

**6.5 へのアップグレードまでにおこなう変更**

* [アセット／収集イベント電子メール通知テンプレート](https://experienceleague.adobe.com/docs/experience-manager-64/deploying/restructuring/assets-repository-restructuring-in-aem-6-4.html#asset-collection-event-e-mail-notification-template)
* [従来のアセット共有デザイン](https://experienceleague.adobe.com/docs/experience-manager-64/deploying/restructuring/assets-repository-restructuring-in-aem-6-4.html#classic-asset-share-designs)
* [アセットダウンロード電子メール通知テンプレート](https://experienceleague.adobe.com/docs/experience-manager-64/deploying/restructuring/assets-repository-restructuring-in-aem-6-4.html#download-asset-e-mail-notification-template)
* [サンプル DRM ライセンス](https://experienceleague.adobe.com/docs/experience-manager-64/deploying/restructuring/assets-repository-restructuring-in-aem-6-4.html#example-drm-licenses)

* [リンク共有電子メール通知テンプレート](https://experienceleague.adobe.com/docs/experience-manager-64/deploying/restructuring/assets-repository-restructuring-in-aem-6-4.html#link-share-e-mail-notification-template)
* [InDesign ワークフロースクリプト](https://experienceleague.adobe.com/docs/experience-manager-64/deploying/restructuring/assets-repository-restructuring-in-aem-6-4.html#indesign-workflow-scripts)
* [ビデオトランスコーディング設定](https://experienceleague.adobe.com/docs/experience-manager-64/deploying/restructuring/assets-repository-restructuring-in-aem-6-4.html#video-transcoding-configurations)
* [その他](https://experienceleague.adobe.com/docs/experience-manager-64/deploying/restructuring/assets-repository-restructuring-in-aem-6-4.html#misc2)

## 6.4 へのアップグレード時におこなう変更 {#with-upgrade}

### その他 {#misc}

<table> 
 <tbody> 
  <tr> 
   <td><strong>以前の場所</strong></td> 
   <td>/etc/dam/jobs</td> 
  </tr> 
  <tr> 
   <td><strong>新しい場所</strong></td> 
   <td>/var/dam/jobs</td> 
  </tr> 
  <tr> 
   <td><strong>再構築の手引き</strong></td> 
   <td><p>カスタムコードがこの場所に依存している（コードがこのパスに明示的に依存している）場合は、アップグレード前に、新しい場所を使用するようにコードを更新する必要があります。JCR 内の特定パスへの依存を減らすために Java API が利用可能な場合は、Java API を使用することをお勧めします。</p> <p>クライアントがダウンロードする zip ファイルを一時的に保存するための場所。クライアントがアセットのダウンロードを要求するので、更新する必要はありません。新しい場所にファイルが生成されます。</p> </td> 
  </tr> 
  <tr> 
   <td><strong>備考</strong></td> 
   <td>該当なし</td> 
  </tr> 
 </tbody> 
</table>

## 6.5 へのアップグレードまでにおこなう変更 {#prior-to-upgrade}

### アセット／収集イベント電子メール通知テンプレート {#asset-collection-event-e-mail-notification-template}

<table> 
 <tbody> 
  <tr> 
   <td><strong>以前の場所</strong></td> 
   <td><code>/etc/notification/email/default</code></td> 
  </tr> 
  <tr> 
   <td><strong>新しい場所</strong></td> 
   <td><p><code>/libs/settings/dam/notification</code></p> <p><code>/apps/settings/dam/notification</code></p> </td> 
  </tr> 
  <tr> 
   <td><strong>再構築の手引き</strong></td> 
   <td><p>電子メールテンプレートが顧客によって変更されている場合は、新しいリポジトリ構造に合わせるために次の操作を実行します。</p> 
    <ol> 
     <li>この <code>/libs/settings/dam/notification</code> 電子メールテンプレートは次の場所からコピーする必要があります： <strong><code>/etc/notification/email/default</code></strong> から <strong><code>/apps/settings/notification/email/default</code></strong> 
      <ol> 
       <li>宛先が<strong> <code>/apps</code></strong> この変更は、SCM に保持する必要があります。</li> 
      </ol> </li> 
     <li>フォルダーを削除します。 <strong><code>/etc/dam/notification/email/default</code></strong> 電子メールテンプレートが移動された後。<br /> 
      <ol> 
       <li>電子メールテンプレートが更新されなかった場合は、<strong> <code>/etc/notification/email/default</code></strong>に設定した場合、元の電子メールテンプレートがの下に存在するので、フォルダーを削除できます。 <strong><code>/libs/settings/notification/email/default</code></strong> AEM 6.4 のインストールの一環として。</li> 
      </ol> </li> 
    </ol> </td> 
  </tr> 
  <tr> 
   <td><strong>備考</strong></td> 
   <td>該当なし<br /> </td> 
  </tr> 
 </tbody> 
</table>

### 従来のアセット共有デザイン {#classic-asset-share-designs}

<table> 
 <tbody> 
  <tr> 
   <td><strong>以前の場所</strong></td> 
   <td><code>/etc/designs/assetshare</code></td> 
  </tr> 
  <tr> 
   <td><strong>新しい場所</strong></td> 
   <td><p><code>/libs/settings/wcm/designs/assetshare</code></p> <p><code>/apps/settings/wcm/designs/assetshare</code></p> </td> 
  </tr> 
  <tr> 
   <td><strong>再構築の手引き</strong></td> 
   <td><p>SCM で管理されており、実行時にデザインダイアログから書き込まれていないデザインについては、次の操作を実行して最新のモデルに合わせます。</p> 
    <ol> 
     <li>以前の場所からのデザインを以下の新しい場所にコピーします。 <code>/apps</code>.</li> 
     <li><a href="/help/sites-developing/clientlibs.md#creating-client-library-folders" target="_blank"> を使用して、デザイン内の CSS、JavaScript、静的リソースを</a>クライアントライブラリ<code>allowProxy = true</code>に変換します。</li> 
     <li><code>cq:designPath</code>AEM／DAM 管理／アセット共有ページ／ページのプロパティ／詳細タブ／デザインフィールド<strong>を使用して、</strong> プロパティで以前の場所への参照を更新します。</li> 
     <li>以前の場所を参照しているすべてのページを更新して、新しいクライアントライブラリカテゴリを使用するようにします。それには、ページの実装コードを更新する必要があります。</li> 
     <li>Dispatcher のルールを更新し、 <code>/etc.clientlibs/</code> プロキシサーブレット。</li> 
    </ol> <p>SCM で管理されず、デザインダイアログで実行時に変更されたデザインの場合は、オーサリング可能なデザインをから移動しないでください。 <code>/etc</code>.</p> </td> 
  </tr> 
  <tr> 
   <td><strong>備考</strong></td> 
   <td>該当なし<br /> </td> 
  </tr> 
 </tbody> 
</table>

### アセットダウンロード電子メール通知テンプレート {#download-asset-e-mail-notification-template}

<table> 
 <tbody> 
  <tr> 
   <td><strong>以前の場所</strong></td> 
   <td><code>/etc/dam/workflow/notification/email/downloadasset</code></td> 
  </tr> 
  <tr> 
   <td><strong>新しい場所</strong></td> 
   <td><p><code>/libs/settings/dam/workflownotification/email/downloadasset</code></p> <p><code>/apps/settings/dam/workflownotification/email/downloadasset</code></p> </td> 
  </tr> 
  <tr> 
   <td><strong>再構築の手引き</strong></td> 
   <td><p>電子メールテンプレート（<strong>downloadasset</strong> または <strong>transientworkflowcompleted</strong>）が変更されている場合は、以下の手順に従って新しい構造に合わせます。</p> 
    <ol> 
     <li>更新された電子メールテンプレートのコピー元 <strong><code>/etc/dam/workflow/notification/email/downloadasset</code></strong> から <strong><code>/apps/settings/dam/workflow/notification/email/downloadasset</code></strong> 
      <ol> 
       <li>宛先が<strong> <code>/apps</code></strong> この変更は、SCM に保持する必要があります。</li> 
      </ol> </li> 
     <li>フォルダーを削除します。 <code>/etc/dam/workflow/notification/email/downloadasset </code>電子メールテンプレートが移動された後。<br /> 
      <ol> 
       <li>電子メールテンプレートが更新されなかった場合は、<strong> <code>/etc</code></strong>に設定した場合、元の電子メールテンプレートがの下に存在するので、フォルダーを削除できます。 <strong><code>/libs/settings/dam/workflownotification/email/downloadasset</code></strong> AEM 6.4 のインストールの一環として。</li> 
      </ol> </li> 
    </ol> </td> 
  </tr> 
  <tr> 
   <td><strong>備考</strong></td> 
   <td>While <code>/conf/global/settings/dam/workflownotification/email/downloadasset</code> は、参照に対して技術的にサポートされます ( 通常の Sling CAConfig 参照で/apps より前、ただし <code>/etc</code>) テンプレートを <code>/conf/global/settings/dam/workflownotification/email/downloadasset</code>. ただし、電子メールテンプレートを容易に編集できる実行時 UI がないので、これはお勧めできません。</td> 
  </tr> 
 </tbody> 
</table>

### サンプル DRM ライセンス {#example-drm-licenses}

| **以前の場所** | `/etc/dam/drm/licenses/` |
|---|---|
| **新しい場所** | `/libs/settings/dam/drm` |
| **再構築の手引き** | 該当なし |
| **備考** | 該当なし |

### リンク共有電子メール通知テンプレート {#link-share-e-mail-notification-template}

<table> 
 <tbody> 
  <tr> 
   <td><strong>以前の場所</strong></td> 
   <td><code>/etc/dam/adhocassetshare</code></td> 
  </tr> 
  <tr> 
   <td><strong>新しい場所</strong></td> 
   <td><p><code>/libs/settings/dam/adhocassetshare</code></p> <p><code>/apps/settings/dam/adhocassetshare</code></p> </td> 
  </tr> 
  <tr> 
   <td><strong>再構築の手引き</strong></td> 
   <td><p>電子メールテンプレートが顧客によって変更されている場合は、新しいリポジトリ構造に合わせるために以下を実行します。</p> 
    <ol> 
     <li>更新された電子メールテンプレートのコピー元 <strong><code>/etc/dam/adhocassetshare</code></strong> から <strong><code>/apps/settings/dam/adhocassetshare</code></strong> 
      <ol> 
       <li>宛先が<strong> <code>/apps</code></strong> この変更は、SCM に保持する必要があります。</li> 
      </ol> </li> 
     <li>フォルダーを削除します。 <strong><code>/etc/dam/adhocassetshare</code></strong> 電子メールテンプレートが移動された後。<br /> 
      <ol> 
       <li>電子メールテンプレートが更新されなかった場合は、<strong> <code>/etc</code></strong>に設定した場合、元の電子メールテンプレートがの下に存在するので、フォルダーを削除できます。 <strong><code>/libs/settings/dam/adhocassetshare</code></strong> AEM 6.4 のインストールの一環として。</li> 
      </ol> </li> 
    </ol> </td> 
  </tr> 
  <tr> 
   <td><strong>備考</strong></td> 
   <td>While <code>/conf/global/settings/dam/adhocassetshare</code> は、参照に対して技術的にサポートされます ( 参照は、 <code>/apps</code> 通常の Sling CAConfig 参照経由、ただし <code>/etc</code>) の代わりに、 <code>/conf/global/settings/dam/adhocassetshare</code>. ただし、電子メールテンプレートを容易に編集できる実行時 UI がないので、これはお勧めできません。</td> 
  </tr> 
 </tbody> 
</table>

### InDesign ワークフロースクリプト {#indesign-workflow-scripts}

<table> 
 <tbody> 
  <tr> 
   <td><strong>以前の場所</strong></td> 
   <td><code>/etc/dam/indesign/scripts</code></td> 
  </tr> 
  <tr> 
   <td><strong>新しい場所</strong></td> 
   <td><p><code>/libs/settings/dam/indesign</code></p> <p><code>/apps/settings/dam/indesign</code></p> </td> 
  </tr> 
  <tr> 
   <td><strong>再構築の手引き</strong></td> 
   <td><p>新しいリポジトリ構造に合わせるには：</p> 
    <ol> 
     <li>次の場所からすべてのカスタムスクリプトまたは変更済みスクリプトをコピーする <strong><code>/etc/dam/indesign/scripts</code></strong> から <strong><code>/apps/settings/dam/indesign/scripts</code></strong><br /> 
      <ol> 
       <li>AEMが提供する未変更のスクリプトはで使用できるので、新しいスクリプトまたは変更されたスクリプトのみをコピーできます。 <strong><code>/libs/settings</code></strong> AEM 6.4 の場合</li> 
      </ol> </li> 
     <li>メディア抽出プロセスワークフローステップを使用するすべてのワークフローモデルを見つけて、以下をおこないます。 
      <ol> 
       <li>ワークフローステップの各インスタンスで、設定内のパスを更新し、<strong> <code>/apps/settings/dam/indesign/scripts</code></strong> または <strong><code>/libs/settings/dam/indesign/scripts</code></strong> 必要に応じて。</li> 
      </ol> </li> 
     <li>削除<strong> <code>/etc/dam/indesign/scripts</code></strong> 完全に。</li> 
    </ol> </td> 
  </tr> 
  <tr> 
   <td><strong>備考</strong></td> 
   <td>カスタマイズしたスクリプトは、以下の場所に保存することをお勧めします。 <code>/apps</code>に設定されます。これは、コードが保存される場所だからです。</td> 
  </tr> 
 </tbody> 
</table>

### ビデオトランスコーディング設定 {#video-transcoding-configurations}

<table> 
 <tbody> 
  <tr> 
   <td><strong>以前の場所</strong></td> 
   <td><code>/etc/dam/video</code></td> 
  </tr> 
  <tr> 
   <td><strong>新しい場所</strong></td> 
   <td><p><code>/libs/settings/dam/video</code></p> <p><code>/apps/settings/dam/video</code></p> </td> 
  </tr> 
  <tr> 
   <td><strong>再構築の手引き</strong></td> 
   <td><p>プロジェクトレベルのカスタマイズは、同等の下に切り取って貼り付ける必要があります <code>/apps</code> または <code>/conf</code> 該当するパス。</p> <p>AEM 6.4 のリポジトリ構造に合わせるには：</p> 
    <ol> 
     <li>変更されたビデオ設定を次の場所からコピーします。 <code>/etc/dam/video</code> から <code>/apps/settings/dam/video</code></li> 
     <li>削除 <code>/etc/dam/video</code></li> 
    </ol> </td> 
  </tr> 
  <tr> 
   <td><strong>備考</strong></td> 
   <td>該当なし</td> 
  </tr> 
 </tbody> 
</table>

### ビューアプリセット設定 {#viewer-preset-configurations}

<table> 
 <tbody> 
  <tr> 
   <td><strong>以前の場所</strong></td> 
   <td><code>/etc/dam/presets/viewer</code></td> 
  </tr> 
  <tr> 
   <td><strong>新しい場所</strong></td> 
   <td><p><code>/libs/settings/dam/dm/presets/viewer</code></p> <p><code>/conf/global/settings/dam/dm/presets/viewer</code></p> </td> 
  </tr> 
  <tr> 
   <td><strong>再構築の手引き</strong></td> 
   <td><p>既製のビューアプリセットの場合は、新しい場所でのみ使用できます。</p> <p>カスタムビューアプリセットの場合：</p> 
    <ul> 
     <li>ノードを移動するには、移行スクリプトを実行する必要があります。 <code>/etc</code> から <code>/conf</code>. スクリプトは、 <em>https://serveraddress:serverport/libs/settings/dam/dm/presets.migratedmcontent.json</em></li> 
     <li>または、設定を編集できます。編集した設定は新しい場所に自動保存されます。</li> 
    </ul> <p>を指すように copyURL/埋め込みコードを調整する必要はありません。 <code>/conf</code>. に対する既存のリクエスト <code>/etc</code> が次の場所から正しいコンテンツに再ルーティングされます： <code>/conf</code>.</p> </td> 
  </tr> 
  <tr> 
   <td><strong>備考</strong></td> 
   <td>該当なし</td> 
  </tr> 
 </tbody> 
</table>

### その他 {#misc2}

<table> 
 <tbody> 
  <tr> 
   <td><strong>以前の場所</strong></td> 
   <td><p><code>/etc/clientlibs/foundation/asseteditor</code></p> <p><code>/etc/clientlibs/foundation/assetshare</code></p> <p><code>/etc/clientlibs/foundation/assetinsights</code></p> </td> 
  </tr> 
  <tr> 
   <td><strong>新しい場所</strong></td> 
   <td><code>/libs/dam/clientlibs</code></td> 
  </tr> 
  <tr> 
   <td><strong>再構築の手引き</strong></td> 
   <td><p>以下の新しいリソースを指すように参照を調整します。 <code>/libs</code> の使用 <code>/etc.clientlibs/</code> プロキシのプレフィックスを許可します。</p> <p>最後に、移行した clientlibs のフォルダーを <code>/etc/clientlibs/foundation/</code></p> </td> 
  </tr> 
  <tr> 
   <td><strong>備考</strong></td> 
   <td>該当なし<br /> </td> 
  </tr> 
 </tbody> 
</table>
