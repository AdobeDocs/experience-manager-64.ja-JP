---
title: AEM 6.4 における Assets リポジトリの再構築
seo-title: Assets Repository Restructuring in AEM 6.4
description: AEM 6.4 での Assets の新しいリポジトリ構造に移行するために、必要な変更を加える方法について説明します。
seo-description: Learn how to make the necessary changes in order to migrate to the new repository structure in AEM 6.4 for Assets.
uuid: 0e3d8163-6274-4d1b-91c7-32ca927fb83c
products: SG_EXPERIENCEMANAGER/6.4/SITES
content-type: reference
topic-tags: repo_restructuring
discoiquuid: 212930fc-3430-4a0a-842c-2fb613ef981f
feature: Upgrading
exl-id: 3d5bbf95-bd1e-453b-b487-517a56fe727f
source-git-commit: c5b816d74c6f02f85476d16868844f39b4c47996
workflow-type: tm+mt
source-wordcount: '1149'
ht-degree: 76%

---

# AEM 6.4 における Assets リポジトリの再構築{#assets-repository-restructuring-in-aem}

>[!CAUTION]
>
>AEM 6.4 の拡張サポートは終了し、このドキュメントは更新されなくなりました。 詳細は、 [技術サポート期間](https://helpx.adobe.com/jp/support/programs/eol-matrix.html). サポートされているバージョンを見つける [ここ](https://experienceleague.adobe.com/docs/?lang=ja).

[AEM 6.4 におけるリポジトリの再構築](/help/sites-deploying/repository-restructuring.md)ページで説明しているように、AEM 6.4 にアップグレードする場合は、このページを参考に、AEM Assets ソリューションに影響を与えるリポジトリ変更に伴う作業量を評価する必要があります。一部の変更ではAEM 6.4 のアップグレードプロセス中に作業が必要ですが、6.5 のアップグレードまで延期することもできます。

**6.4 へのアップグレード時におこなう変更**

* [その他](https://experienceleague.adobe.com/docs/?lang=jaexperience-manager-64/deploying/restructuring/assets-repository-restructuring-in-aem-6-4.html#misc)

**6.5 へのアップグレード前**

* [アセット／コレクションイベントのメール通知テンプレート](https://experienceleague.adobe.com/docs/experience-manager-64/deploying/restructuring/assets-repository-restructuring-in-aem-6-4.html#asset-collection-event-e-mail-notification-template)
* [従来のアセット共有デザイン](https://experienceleague.adobe.com/docs/experience-manager-64/deploying/restructuring/assets-repository-restructuring-in-aem-6-4.html#classic-asset-share-designs)
* [アセットダウンロードのメール通知テンプレート](https://experienceleague.adobe.com/docs/experience-manager-64/deploying/restructuring/assets-repository-restructuring-in-aem-6-4.html#download-asset-e-mail-notification-template)
* [サンプル DRM ライセンス](https://experienceleague.adobe.com/docs/experience-manager-64/deploying/restructuring/assets-repository-restructuring-in-aem-6-4.html#example-drm-licenses)

* [リンク共有のメール通知テンプレート](https://experienceleague.adobe.com/docs/experience-manager-64/deploying/restructuring/assets-repository-restructuring-in-aem-6-4.html#link-share-e-mail-notification-template)
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
   <td><p>カスタムコードがこの場所 ( コードは明示的にこのパスに依存しています )。その場合、アップグレードの前に、新しい場所を使用するようにコードを更新する必要があります。Java API を使用して、JCR 内の特定のパスへの依存を減らすのが理想的です。</p> <p>クライアントがダウンロードする zip ファイルを保持する一時的な場所。 クライアントがアセットのダウンロードをリクエストするので、更新する必要はありません。 新しい場所にファイルが生成されます。</p> </td> 
  </tr> 
  <tr> 
   <td><strong>備考</strong></td> 
   <td>該当なし</td> 
  </tr> 
 </tbody> 
</table>

## 6.5 へのアップグレード前 {#prior-to-upgrade}

### アセット／コレクションイベントのメール通知テンプレート {#asset-collection-event-e-mail-notification-template}

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
   <td><p>メールテンプレートが顧客によって変更されている場合は、新しいリポジトリ構造に合わせるために以下の操作を実行します。</p> 
    <ol> 
     <li><code>/libs/settings/dam/notification</code> メールテンプレートを <strong><code>/etc/notification/email/default</code></strong> から <strong><code>/apps/settings/notification/email/default</code></strong> にコピーする必要があります。 
      <ol> 
       <li>コピー先が <strong> <code>/apps</code></strong> にあるので、この変更は SCM に保存されます。</li> 
      </ol> </li> 
     <li><strong><code>/etc/dam/notification/email/default</code></strong> フォルダー内のメールテンプレートを移動したら、このフォルダーを削除します。<br /> 
      <ol> 
       <li><strong> <code>/etc/notification/email/default</code></strong> 内のメールテンプレートが更新されていない場合は、このフォルダーを削除してかまいません。インストールされた AEM 6.4 の一部として元のメールテンプレートが <strong><code>/libs/settings/notification/email/default</code></strong> に存在するからです。</li> 
      </ol> </li> 
    </ol> </td> 
  </tr> 
  <tr> 
   <td><strong>メモ</strong></td> 
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
   <td><p>SCM で管理されており、実行時にデザインダイアログから書き込まれていないデザインについては、以下の操作を実行して最新のモデルに合わせます。</p> 
    <ol> 
     <li>デザインを以前の場所から <code>/apps</code> 内の新しい場所にコピーします。</li> 
     <li><code>allowProxy = true</code> を使用して、デザイン内の CSS、JavaScript、静的リソースを<a href="/help/sites-developing/clientlibs.md#creating-client-library-folders" target="_blank">クライアントライブラリ</a>に変換します。</li> 
     <li><strong>AEM／DAM 管理／アセット共有ページ／ページのプロパティ／詳細タブ／デザインフィールド</strong>を使用して、<code>cq:designPath</code> プロパティで以前の場所への参照を更新します。</li> 
     <li>以前の場所を参照しているページを更新して、新規のクライアントライブラリカテゴリを使用します。これにはページ実装コードの更新が必要です。</li> 
     <li>Dispatcher ルールを更新して、<code>/etc.clientlibs/</code> プロキシサーブレット経由でクライアントライブラリを提供できるようにします。</li> 
    </ol> <p>SCM で管理されておらず、実行時にデザインダイアログで変更されるデザインの場合は、オーサリング可能なデザインを <code>/etc</code> から移動しないでください。</p> </td> 
  </tr> 
  <tr> 
   <td><strong>備考</strong></td> 
   <td>該当なし<br /> </td> 
  </tr> 
 </tbody> 
</table>

### アセットダウンロードのメール通知テンプレート {#download-asset-e-mail-notification-template}

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
   <td><p>メールテンプレート（<strong>downloadasset</strong> または <strong>transientworkflowcompleted</strong>）が変更されている場合は、以下の手順に従って新しい構造に合わせます。</p> 
    <ol> 
     <li>更新されたメールテンプレートを <strong><code>/etc/dam/workflow/notification/email/downloadasset</code></strong> から <strong><code>/apps/settings/dam/workflow/notification/email/downloadasset</code></strong> にコピーします。 
      <ol> 
       <li>コピー先が <strong> <code>/apps</code></strong> にあるので、この変更は SCM に保存されます。</li> 
      </ol> </li> 
     <li><code>/etc/dam/workflow/notification/email/downloadasset </code> フォルダー内のメールテンプレートを移動したら、このフォルダーを削除します。<br /> 
      <ol> 
       <li><strong> <code>/etc</code></strong> 内のメールテンプレートが更新されていない場合は、このフォルダーを削除してかまいません。インストールされた AEM 6.4 の一部として元のメールテンプレートが <strong><code>/libs/settings/dam/workflownotification/email/downloadasset</code></strong> に存在するからです。</li> 
      </ol> </li> 
    </ol> </td> 
  </tr> 
  <tr> 
   <td><strong>備考</strong></td> 
   <td><code>/conf/global/settings/dam/workflownotification/email/downloadasset</code> がルックアップ対象として技術的にサポートされている間は（通常の Sling CAConfig ルックアップでは /apps より優先されますが、<code>/etc</code> の方が優先されます）、テンプレートを <code>/conf/global/settings/dam/workflownotification/email/downloadasset</code> に格納することもできます。ただし、電子メールテンプレートの編集を容易にするランタイム UI がないので、この方法はお勧めしません。</td> 
  </tr> 
 </tbody> 
</table>

### サンプル DRM ライセンス {#example-drm-licenses}

| **以前の場所** | `/etc/dam/drm/licenses/` |
|---|---|
| **新しい場所** | `/libs/settings/dam/drm` |
| **再構築の手引き** | 該当なし |
| **備考** | 該当なし |

### リンク共有のメール通知テンプレート {#link-share-e-mail-notification-template}

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
   <td><p>メールテンプレートが顧客によって変更されている場合は、新しいリポジトリ構造に合わせるために以下を実行します。</p> 
    <ol> 
     <li>更新されたメールテンプレートを <strong><code>/etc/dam/adhocassetshare</code></strong> から <strong><code>/apps/settings/dam/adhocassetshare</code></strong> にコピーします。 
      <ol> 
       <li>コピー先が <strong> <code>/apps</code></strong> にあるので、この変更は SCM に保存されます。</li> 
      </ol> </li> 
     <li><strong><code>/etc/dam/adhocassetshare</code></strong> フォルダー内のメールテンプレートを移動したら、このフォルダーを削除します。<br /> 
      <ol> 
       <li><strong> <code>/etc</code></strong> 内のメールテンプレートが更新されていない場合は、このフォルダーを削除してかまいません。インストールされた AEM 6.4 の一部として元のメールテンプレートが <strong><code>/libs/settings/dam/adhocassetshare</code></strong> に存在するからです。</li> 
      </ol> </li> 
    </ol> </td> 
  </tr> 
  <tr> 
   <td><strong>備考</strong></td> 
   <td><code>/conf/global/settings/dam/adhocassetshare</code> がルックアップ対象として技術的にサポートされている間は（通常の Sling CAConfig ルックアップでは <code>/apps</code> より優先されますが、<code>/etc</code> の方が優先されます）、テンプレートを <code>/conf/global/settings/dam/adhocassetshare</code> に格納することもできます。ただし、電子メールテンプレートの編集を容易にするランタイム UI がないので、この方法はお勧めしません</td> 
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
     <li>すべてのカスタムスクリプトまたは変更済みスクリプトを <strong><code>/etc/dam/indesign/scripts</code></strong> から <strong><code>/apps/settings/dam/indesign/scripts</code></strong><br /> にコピーします。 
      <ol> 
       <li>AEM に用意されている未変更のスクリプトは、AEM 6.4 では <strong><code>/libs/settings</code></strong> から利用できるので、新規または変更済みのスクリプトのみコピーします。</li> 
      </ol> </li> 
     <li>メディア抽出プロセスワークフローステップを使用するすべてのワークフローモデルを探し、以下の操作を実行します。 
      <ol> 
       <li>ワークフローステップのインスタンスごとに、config のパスを更新して、<strong> <code>/apps/settings/dam/indesign/scripts</code></strong> または <strong><code>/libs/settings/dam/indesign/scripts</code></strong>（該当する場合）内の適切なスクリプトを明示的に指すようにします。</li> 
      </ol> </li> 
     <li><strong> <code>/etc/dam/indesign/scripts</code></strong> を完全に削除します。</li> 
    </ol> </td> 
  </tr> 
  <tr> 
   <td><strong>備考</strong></td> 
   <td>カスタマイズしたスクリプトは、コードの格納先である <code>/apps</code> 内に格納することをお勧めします。</td> 
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
   <td><p>必要に応じて、プロジェクトレベルのカスタマイズを、対応する <code>/apps</code> または <code>/conf</code> パスに移動（切り取って貼り付け）する必要があります。</p> <p>AEM 6.4 のリポジトリ構造に合わせるには：</p> 
    <ol> 
     <li>変更されたビデオ設定を <code>/etc/dam/video</code> からコピーし、次の場所に貼り付けます： <code>/apps/settings/dam/video</code></li> 
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
   <td><p>標準提供のビューアプリセットの場合、新しい場所でのみ使用できます。</p> <p>カスタムビューアプリセットの場合：</p> 
    <ul> 
     <li>移行スクリプトを実行して、ノードを <code>/etc</code> から <code>/conf</code> に移動する必要があります。スクリプトの URL は <em>https://serveraddress:serverport/libs/settings/dam/dm/presets.migratedmcontent.json</em> です。</li> 
     <li>または、設定を編集できます。編集した設定は新しい場所に自動保存されます。</li> 
    </ul> <p>なお、<code>/conf</code> を指すようにコピー URL や埋め込みコードを調整する必要はありません。<code>/etc</code> への既存のリクエストは、<code>/conf</code> 内の適切なコンテンツに再ルーティングされます。</p> </td> 
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
   <td><p><code>/libs</code> 内の新しいリソースを指すようにすべての参照を調整します。それには、<code>/etc.clientlibs/</code> を使用してプロキシプレフィックスを許可します。</p> <p>最後に、移行した clientlibs のフォルダーを / / から削除して、クリーンアップをおこないます。 <code>/etc/clientlibs/foundation/</code></p> </td> 
  </tr> 
  <tr> 
   <td><strong>備考</strong></td> 
   <td>該当なし<br /> </td> 
  </tr> 
 </tbody> 
</table>
