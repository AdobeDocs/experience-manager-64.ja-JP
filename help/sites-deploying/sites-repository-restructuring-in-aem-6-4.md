---
title: AEM 6.4 における Sites リポジトリの再構築
seo-title: Sites Repository Restructuring in AEM 6.4
description: AEM 6.4 での Sites の新しいリポジトリ構造に移行するために、必要な変更を加える方法について説明します。
seo-description: Learn how to make the necessary changes in order to migrate to the new repository structure in AEM 6.4 for Sites.
uuid: 6dc5f8bd-1680-40af-9b8f-26c1f4bc3304
products: SG_EXPERIENCEMANAGER/6.4/SITES
content-type: reference
topic-tags: repo_restructuring
discoiquuid: 3eccb2d5-c325-43a6-9c03-5f93f7e30712
feature: Upgrading
exl-id: d0cdb15d-196a-44e3-bd98-91588b6979ab
source-git-commit: bd94d3949f0117aa3e1c9f0e84f7293a5d6b03b4
workflow-type: tm+mt
source-wordcount: '1572'
ht-degree: 72%

---

# AEM 6.4 における Sites リポジトリの再構築{#sites-repository-restructuring-in-aem}

親の説明に従って [AEM 6.4 におけるリポジトリの再構築](/help/sites-deploying/repository-restructuring.md) このページでは、AEM 6.4 にアップグレードするお客様は、このページを使用して、AEM Sitesソリューションに影響を与えるリポジトリの変更に関連する作業量を評価する必要があります。 一部の変更は AEM 6.4 アップグレードプロセス中に作業が必要ですが、それ以外は 6.5 アップグレードまで延期できます。

**6.4 へのアップグレード時におこなう変更**

* [ContextHub セグメント](/help/sites-deploying/sites-repository-restructuring-in-aem-6-4.md#contexthub-segments)

**6.5 へのアップグレードまでにおこなう変更**

* [Adobe Analytics クライアントライブラリ](/help/sites-deploying/sites-repository-restructuring-in-aem-6-4.md#adobe-analytics-client-libraries)
* [クラシックな Microsoft Word から Web ページへのデザイン](/help/sites-deploying/sites-repository-restructuring-in-aem-6-4.md#classic-microsoft-word-to-web-page-designs)
* [モバイルデバイスエミュレーター設定](/help/sites-deploying/sites-repository-restructuring-in-aem-6-4.md#mobile-device-emulator-configurations)
* [Multi-site Manager のブループリント設定](/help/sites-deploying/sites-repository-restructuring-in-aem-6-4.md#multi-site-manager-blueprint-configurations)
* [Multi-site Manager のロールアウト設定](/help/sites-deploying/sites-repository-restructuring-in-aem-6-4.md#multi-site-manager-rollout-configurations)
* [ページイベント通知電子メールテンプレート](/help/sites-deploying/sites-repository-restructuring-in-aem-6-4.md#page-event-notification-e-mail-template)
* [ページ基礎モード](/help/sites-deploying/sites-repository-restructuring-in-aem-6-4.md#page-scaffolding)
* [レスポンシブグリッド LESS](/help/sites-deploying/sites-repository-restructuring-in-aem-6-4.md#responsive-grid-less)
* [静的テンプレートデザイン](/help/sites-deploying/sites-repository-restructuring-in-aem-6-4.md#static-template-designs)
* [Adobe Search and Promote 統合クライアントライブラリ](/help/sites-deploying/sites-repository-restructuring-in-aem-6-4.md#adobe-search-and-promote-integration-client-libraries)
* [Adobe Target 統合クライアントライブラリ](/help/sites-deploying/sites-repository-restructuring-in-aem-6-4.md#adobe-target-integration-client-libraries)
* [WCM Foundation クライアントライブラリ](/help/sites-deploying/sites-repository-restructuring-in-aem-6-4.md#wcm-foundation-client-libraries)

## 6.4 へのアップグレード時におこなう変更 {#with-upgrade}

### ContextHub セグメント {#contexthub-segments}

<table> 
 <tbody>
  <tr>
   <td><strong>以前の場所</strong></td> 
   <td><code>/etc/segmentation/contexthub</code></td> 
  </tr>
  <tr>
   <td><strong>新しい場所</strong></td> 
   <td><p><code>/apps/settings/wcm/segments</code> </p> <p><code>/conf/settings/settings/wcm/segments</code> </p> <p><code>/conf/&lt;tenant&gt;/settings/wcm/segments</code></p> </td> 
  </tr>
  <tr>
   <td><strong>再構築の手引き</strong></td> 
   <td><p>新規または変更された ContextHub セグメントが AEM で編集されるのではなく、ソース管理で編集されることを意図している場合は、それらを新しい場所に移行する必要があります。</p> 
    <ol> 
     <li>新規または変更された ContextHub セグメントを以前の場所から適切な新しい場所 (/<code>apps</code>, <code>/conf/global</code> または <code>/conf/&lt;tenant&gt;</code>)</li> 
     <li>以前の場所の ContextHub セグメントへの参照を、移行された新しい場所の ContextHub セグメントに更新します (<code>/apps</code>, <code>/conf/global</code>, <code>/conf/&lt;tenant&gt;</code>) をクリックします。</li> 
    </ol> <p>次の QueryBuilder クエリは、以前の場所内の ContextHub セグメントへのすべての参照を探します。<br /> <br /> <code class="code">path=/content
       property=cq:segments
       property.operation=like
       property.value=/etc/segmentation/contexthub/%</code><br /> <br /> これは、 <a href="/help/sites-developing/querybuilder-api.md" target="_blank">AEM QueryBuilder Debugger UI</a>. これはトラバースクエリなので、実稼動環境に対して実行しないでください。また、必要に応じてトラバーサル制限を調整してください。</p> </td> 
  </tr>
  <tr>
   <td><strong>備考</strong></td> 
   <td><p>以前の場所に保存されている ContextHub セグメントは、<strong>AEM／パーソナライゼーション／オーディエンス</strong>に読み取り専用として表示されます。</p> <p>AEMで ContextHub セグメントを編集可能にするには、新しい場所 (<code>/conf/global</code> または <code>/conf/&lt;tenant&gt;</code>) をクリックします。 AEMで作成された新しい ContentHub セグメントは、新しい場所 (<code>/conf/global</code> または <code>/conf/&lt;tenant&gt;</code>) をクリックします。</p> <p>AEM Sitesのページプロパティでは、以前の場所 (<code>/etc</code>) または単一の新しい場所 (<code>/apps</code>, <code>/conf/global</code> または <code>/conf/&lt;tenant&gt;</code>) が選択されている場合は、それに応じて ContextHub セグメントを移行する必要があります。</p> <p>AEM 参照サイトからの未使用の ContextHub セグメントは削除でき、新しい場所に移行されません。</p> 
    <ul> 
     <li>/etc/segmentation/geometrixx/</li> 
     <li>/etc/segmentation/geometrixx-outdoors</li> 
    </ul> <p>注：ClientContext が使用中の場合は、ContextHub に変換することをお勧めします。</p> </td> 
  </tr>
 </tbody>
</table>

## 6.5 へのアップグレードまでにおこなう変更 {#prior-to-upgrade}

### Adobe Analytics クライアントライブラリ {#adobe-analytics-client-libraries}

<table> 
 <tbody>
  <tr>
   <td><strong>以前の場所</strong></td> 
   <td><p><code>/etc/clientlibs/foundation/sitecatalyst</code></p> </td> 
  </tr>
  <tr>
   <td><strong>新しい場所</strong></td> 
   <td><code>/libs/cq/analytics/clientlibs/analytics</code></td> 
  </tr>
  <tr>
   <td><strong>再構築の手引き</strong></td> 
   <td><p>これらのクライアントライブラリをカスタムで使用する場合は、パスではなくカテゴリでクライアントライブラリを参照する必要があります。</p> 
    <ol> 
     <li>以前の場所のパスによるクライアントライブラリへの参照はすべて <a href="/help/sites-developing/clientlibs.md#referencing-client-side-libraries" target="_blank">AEM のクライアントライブラリ参照フレームワーク</a>を使用するように更新する必要があります。</li> 
     <li>AEM のクライアントライブラリ参照フレームワークを使用できない場合、クライアントライブラリの絶対パスは AEM のクライアントライブラリプロキシサーブレットを介して参照できます。
      <ul> 
       <li><code>/etc.clientlibs/cq/analytics/clientlibs/sitecatalyst/appmeasurement.js</code></li> 
       <li><code>/etc.clientlibs/cq/analytics/clientlibs/sitecatalyst/plugins.js</code></li> 
       <li><code>/etc.clientlibs/cq/analytics/clientlibs/sitecatalyst/sitecatalyst.js</code></li> 
       <li><code>/etc.clientlibs/cq/analytics/clientlibs/sitecatalyst/tracking.js</code></li> 
       <li><code>/etc.clientlibs/cq/analytics/clientlibs/sitecatalyst/util.js</code></li> 
      </ul> </li> 
    </ol> </td> 
  </tr>
  <tr>
   <td><strong>備考</strong></td> 
   <td><p>これらのクライアントライブラリの編集はサポートされていませんでした。</p> <p>クライアントライブラリのカテゴリを入手するには、CRXDELite で各 <code>cq:ClientLIbraryFolder</code> ノードを検索し、カテゴリプロパティを調べます.</p> 
    <ul> 
     <li><code>/libs/cq/analytics/clientlibs/sitecatalyst/appmeasurement</code></li> 
     <li><code>/libs/cq/analytics/clientlibs/sitecatalyst/plugins</code></li> 
     <li><code>/libs/cq/analytics/clientlibs/sitecatalyst/sitecatalyst</code></li> 
     <li><code>/libs/cq/analytics/clientlibs/sitecatalyst/tracking</code></li> 
     <li><code>/libs/cq/analytics/clientlibs/sitecatalyst/util</code></li> 
    </ul> </td> 
  </tr>
 </tbody>
</table>

### クラシックな Microsoft Word から Web ページへのデザイン {#classic-microsoft-word-to-web-page-designs}

<table> 
 <tbody>
  <tr>
   <td><strong>以前の場所</strong></td> 
   <td><code>/etc/designs/wordDesign</code></td> 
  </tr>
  <tr>
   <td><strong>新しい場所</strong></td> 
   <td><p><code>/libs/settings/wcm/designs/wordDesign</code></p> <p><code>/apps/settings/wcm/designs/wordDesign</code></p> </td> 
  </tr>
  <tr>
   <td><strong>再構築の手引き</strong></td> 
   <td><p>SCM で管理されており、実行時にデザインダイアログから書き込まれていないデザインの場合：</p> 
    <ol> 
     <li>以前の場所から新しい場所 (<code>/apps</code>) をクリックします。</li> 
     <li><a href="/help/sites-developing/clientlibs.md#creating-client-library-folders" target="_blank"> を使用して、デザイン内の CSS、JavaScript、静的リソースを</a>クライアントライブラリ<code>allowProxy = true</code>に変換します。</li> 
     <li>cq:designPath プロパティの以前の場所への参照を更新します。</li> 
     <li>以前の場所を参照しているページを更新して、新規のクライアントライブラリカテゴリを使用します（これにはページ実装コードの更新が必要です）。</li> 
     <li>AEM Dispatcher のルールを更新して、 <code>/etc.clientlibs/</code> プロキシサーブレット。</li> 
    </ol> <p>SCM で管理されておらず、実行時にデザインダイアログで変更されたデザインの場合：</p> 
    <ul> 
     <li>次の場所からオーサー可能なデザインを移動しない <code>/etc</code>.</li> 
    </ul> </td> 
  </tr>
  <tr>
   <td><strong>備考</strong></td> 
   <td>該当なし<br /> </td> 
  </tr>
 </tbody>
</table>

### モバイルデバイスエミュレーター設定 {#mobile-device-emulator-configurations}

<table> 
 <tbody>
  <tr>
   <td><strong>以前の場所</strong></td> 
   <td><p><code>/etc/mobile</code></p> </td> 
  </tr>
  <tr>
   <td><strong>新しい場所</strong></td> 
   <td><p><code>/libs/settings/mobile</code></p> <p><code>/apps/settings/mobile</code></p> <p><code>/conf/global/settings/mobile</code></p> <p><code>/conf/&lt;tenant&gt;/settings/mobile</code></p> </td> 
  </tr>
  <tr>
   <td><strong>再構築の手引き</strong></td> 
   <td>新しいモバイルデバイスエミュレーター設定は、新しい場所に移行する必要があります。
    <ol> 
     <li>新しいモバイルデバイスエミュレーター設定を以前の場所から新しい場所 (<code>/apps</code>, <code>/conf/global</code>, <code>/conf/&lt;tenant&gt;</code>) をクリックします。</li> 
     <li>これらのモバイルデバイスエミュレーター設定に依存するAEM Sitesページの場合、ページの <span class="code">
       <code>
        jcr
       </code>
       <code>
        :content
       </code></span> ノード： <br /> <span class="code">[cq:Page]/jcr:content@cq:
       <code>
        deviceGroups
       </code> = String[ mobile/groups/responsive ]</span></li> 
     <li>これらのモバイルデバイスエミュレーター設定に依存する編集可能なテンプレートに対して、編集可能なテンプレートを更新し、 <span class="code">
       <code>
        cq
       </code>:
       <code>
        deviceGroups
       </code></span> を「新しい場所」に追加します。</li> 
    </ol> </td> 
  </tr>
  <tr>
   <td><strong>備考</strong></td> 
   <td><p>モバイルデバイスエミュレータ設定の解決は、次の順序でおこなわれます。</p> 
    <ol> 
     <li><code>/conf/&lt;tenant&gt;/settings/mobile</code></li> 
     <li><code>/conf/global/settings/mobile</code></li> 
     <li><code>/apps/settings/mobile</code></li> 
     <li><code>/libs/settings/mobile</code></li> 
     <li><code>/etc/mobile</code></li> 
    </ol> </td> 
  </tr>
 </tbody>
</table>

### Multi-site Manager のブループリント設定 {#multi-site-manager-blueprint-configurations}

<table> 
 <tbody>
  <tr>
   <td><strong>以前の場所</strong></td> 
   <td><code>/etc/blueprints</code></td> 
  </tr>
  <tr>
   <td><strong>新しい場所</strong></td> 
   <td><p><code>/apps/msm</code> （顧客のブループリント設定）</p> <p><code>/libs/msm</code> （Screens、Commerce の標準ブループリント設定）</p> </td> 
  </tr>
  <tr>
   <td><strong>再構築の手引き</strong></td> 
   <td><p>新規または変更された Multi-site Manager ブループリント設定は、新しい場所 (<code>/apps</code>) をクリックします。</p> 
    <ol> 
     <li>新規または変更された Multi-site Manager ブループリント設定を以前の場所から新しい場所 (<code>/apps</code>) をクリックします。</li> 
     <li>移行した Multi-site Manager のブループリント設定を以前の場所から削除します。</li> 
    </ol> </td> 
  </tr>
  <tr>
   <td><strong>備考</strong></td> 
   <td><p>Multi-site Manager で提供されるすべてのAEMのブループリント設定は、 <code>/libs</code>.</p> <p>コンテンツは Multi-site Manager のブループリント設定を参照していないため、調整するコンテンツ参照はありません。</p> </td> 
  </tr>
 </tbody>
</table>

### Multi-site Manager のロールアウト設定 {#multi-site-manager-rollout-configurations}

<table> 
 <tbody>
  <tr>
   <td><strong>以前の場所</strong></td> 
   <td><p><code>/etc/msm/rolloutConfigs</code></p> </td> 
  </tr>
  <tr>
   <td><strong>新しい場所</strong></td> 
   <td><p><code>/libs/msm/wcm/rolloutconfigs</code></p> <p><code>/apps/msm/wcm/rolloutconfigs</code></p> </td> 
  </tr>
  <tr>
   <td><strong>再構築の手引き</strong></td> 
   <td><p>新規または変更された Multi-Site Manager のロールアウト設定は、新しい場所に移行する必要があります。</p> 
    <ol> 
     <li>新規または変更された Multi-site Manager のロールアウト設定を以前の場所から新しい場所 (<code>/apps</code>) をクリックします。</li> 
     <li>AEMページ上の参照を、以前の場所の Multi-site Manager ロールアウト設定に更新し、新しい場所 (<code>/libs</code> または <code>/apps</code>) をクリックします。</li> 
    </ol> <p>移行した Multi-site Manager のロールアウト設定を以前の場所から削除します。</p> </td> 
  </tr>
  <tr>
   <td><strong>備考</strong></td> 
   <td>移行した Multi-site Manager のロールアウト設定を以前の場所から削除しないと、ロールアウトオプションが AEM 作成者に重複して表示されます。</td> 
  </tr>
 </tbody>
</table>

### ページイベント通知電子メールテンプレート {#page-event-notification-e-mail-template}

<table> 
 <tbody>
  <tr>
   <td><strong>以前の場所</strong></td> 
   <td><p><code>/etc/notification/email/default/com.day.cq.wcm.core.page</code></p> </td> 
  </tr>
  <tr>
   <td><strong>新しい場所</strong></td> 
   <td><p><code>/libs/settings/notification-templates/com.day.cq.wcm.core.page</code></p> <p><code>/apps/settings/notification-templates/com.day.cq.wcm.core.page</code></p> </td> 
  </tr>
  <tr>
   <td><strong>再構築の手引き</strong></td> 
   <td><p>サポートされている唯一の新規ページイベント通知電子メールテンプレートは、新しいロケールをサポートするものです。</p> <p>ページイベント電子メールテンプレートの解決は、次の順序でおこなわれます。</p> 
    <ol> 
     <li><code>/etc/notification/email/default/com.day.cq.wcm.core.page</code></li> 
     <li><code>/apps/settings/notification-templates/com.day.cq.wcm.core.page</code></li> 
     <li><code>/libs/settings/notification-templates/com.day.cq.wcm.core.page</code></li> 
    </ol> </td> 
  </tr>
  <tr>
   <td><strong>備考</strong></td> 
   <td><p>新規または変更されたページイベント通知電子メールテンプレートは、以下の新しい場所に移行する必要があります。 <code>/apps</code>:</p> 
    <ol> 
     <li>新規または変更されたページイベント通知電子メールテンプレートを以前の場所から新しい場所 (<code>/apps</code>) をクリックします。</li> 
     <li>移行したページイベント通知電子メールテンプレートを以前の場所からすべて削除します。</li> 
    </ol> </td> 
  </tr>
 </tbody>
</table>

### ページ基礎モード {#page-scaffolding}

<table> 
 <tbody>
  <tr>
   <td><strong>以前の場所</strong></td> 
   <td><code>/etc/scaffolding</code></td> 
  </tr>
  <tr>
   <td><strong>新しい場所</strong></td> 
   <td><p><span class="code">/libs/settings/
      <code>
       wcm
      </code>/template-types/scaffolding/scaffolding</span></p> <p><span class="code">/apps/settings/
      <code>
       wcm
      </code>/template-types/scaffolding/scaffolding</span></p> </td> 
  </tr>
  <tr>
   <td><strong>再構築の手引き</strong></td> 
   <td>以前の場所の下に作成された基礎モードは、従来の基礎モードフレームワークを使用するため、新しい場所に移行できません。新しい場所に合わせるには、サポートされている基礎モードフレームワークを使用して、従来の基礎モードを再開発する必要があります。</td> 
  </tr>
  <tr>
   <td><strong>備考</strong></td> 
   <td>該当なし<br /> </td> 
  </tr>
 </tbody>
</table>

### レスポンシブグリッド LESS {#responsive-grid-less}

<table> 
 <tbody>
  <tr>
   <td><strong>以前の場所</strong></td> 
   <td><code>/etc/clientlibs/wcm/foundation/grid/grid_base.less</code></td> 
  </tr>
  <tr>
   <td><strong>新しい場所</strong></td> 
   <td><code>/libs/wcm/foundation/clientlibs/grid/grid_base.less</code></td> 
  </tr>
  <tr>
   <td><strong>再構築の手引き</strong></td> 
   <td><p>カスタム LESS ファイル内の以前の場所への参照はすべて、新しい場所からインポートするように更新する必要があります。</p> 
    <ul> 
     <li>以前の場所で grid_base.less を参照している参照カスタム LESS ファイルを、新しい場所を参照するように更新します。</li> 
    </ul> </td> 
  </tr>
  <tr>
   <td><strong>備考</strong></td> 
   <td>存在しない <code>grid_base.less</code> ファイルを参照すると、ページのレイアウトモードとテンプレートエディターが機能せず、ページレイアウトが中断されます。</td> 
  </tr>
 </tbody>
</table>

### 静的テンプレートデザイン {#static-template-designs}

<table> 
 <tbody>
  <tr>
   <td><strong>以前の場所</strong></td> 
   <td><code>/etc/designs/&lt;custom-site&gt;</code></td> 
  </tr>
  <tr>
   <td><strong>新しい場所</strong></td> 
   <td><code>/apps/settings/wcm/designs/&lt;custom-site&gt;</code></td> 
  </tr>
  <tr>
   <td><strong>再構築の手引き</strong></td> 
   <td><p>SCM で管理されており、実行時にデザインダイアログから書き込まれていないデザインの場合：</p> 
    <ol> 
     <li>以前の場所から新しい場所 (<code>/apps</code>) をクリックします。</li> 
     <li><a href="/help/sites-developing/clientlibs.md#creating-client-library-folders" target="_blank"> を使用して、デザイン内の CSS、JavaScript、静的リソースを</a>クライアントライブラリ<code>allowProxy = true</code>に変換します。</li> 
     <li><code>cq:designPath</code>AEM／Sites／カスタムサイトページ／ページのプロパティ／詳細タブ／デザインフィールド<strong>で </strong> プロパティの以前の場所への参照を更新します。</li> 
     <li>以前の場所を参照しているページを更新して、新規のクライアントライブラリカテゴリを使用します（これにはページ実装コードの更新が必要です）。</li> 
     <li>AEM Dispatcher のルールを更新して、 <code>/etc.clientlibs/</code> プロキシサーブレット。</li> 
    </ol> <p>SCM で管理されておらず、実行時にデザインダイアログで変更されたデザインの場合：</p> 
    <ul> 
     <li>次の場所からオーサー可能なデザインを移動しない <code>/etc</code>.</li> 
    </ul> </td> 
  </tr>
  <tr>
   <td><strong>備考</strong></td> 
   <td>推奨されるアプローチは、デザインの代わりに構造コンテンツとポリシーを使用する編集可能なテンプレートを使用して AEM Sites とページを構築することです。</td> 
  </tr>
 </tbody>
</table>

### Adobe Search and Promote 統合クライアントライブラリ {#adobe-search-and-promote-integration-client-libraries}

<table> 
 <tbody>
  <tr>
   <td><strong>以前の場所</strong></td> 
   <td><p><code>/etc/clientlibs/foundation/searchpromote</code></p> </td> 
  </tr>
  <tr>
   <td><strong>新しい場所</strong></td> 
   <td><code>/libs/cq/searchpromote/clientlibs/searchpromote</code></td> 
  </tr>
  <tr>
   <td><strong>再構築の手引き</strong></td> 
   <td><p>これらのクライアントライブラリをカスタムで使用する場合は、パスではなくカテゴリでクライアントライブラリを参照する必要があります。</p> 
    <ol> 
     <li>以前の場所のパスによるクライアントライブラリへの参照はすべて <a href="/help/sites-developing/clientlibs.md#referencing-client-side-libraries" target="_blank">AEM のクライアントライブラリ参照フレームワーク</a>を使用するように更新する必要があります。</li> 
     <li>AEM のクライアントライブラリ参照フレームワークを使用できない場合、クライアントライブラリの絶対パスは AEM のクライアントライブラリプロキシサーブレットを介して参照できます:</li> 
    </ol> 
    <ul> 
     <li><code>/etc.clientlibs/cq/searchpromote/clientlibs/searchpromotei.js</code></li> 
    </ul> </td> 
  </tr>
  <tr>
   <td><strong>備考</strong></td> 
   <td><p>これらのクライアントライブラリの編集はサポートされていませんでした。</p> <p>クライアントライブラリのカテゴリを入手するには、CRXDELite で各 cq:ClientLIbraryFolder ノードを検索し、カテゴリプロパティを調べます:</p> 
    <ul> 
     <li><code>/libs/cq/searchpromote/clientlibs/searchpromote</code></li> 
    </ul> </td> 
  </tr>
 </tbody>
</table>

### Adobe Target 統合クライアントライブラリ {#adobe-target-integration-client-libraries}

<table> 
 <tbody>
  <tr>
   <td><strong>以前の場所</strong></td> 
   <td><p><code>/etc/clientlibs/foundation/target</code></p> </td> 
  </tr>
  <tr>
   <td><strong>新しい場所</strong></td> 
   <td><code>/libs/cq/testandtarget/clientlibs/testandtarget</code></td> 
  </tr>
  <tr>
   <td><strong>再構築の手引き</strong></td> 
   <td><p>これらのクライアントライブラリをカスタムで使用する場合は、パスではなくカテゴリでクライアントライブラリを参照する必要があります。</p> 
    <ol> 
     <li>以前の場所のパスによるクライアントライブラリへの参照はすべて <a href="/help/sites-developing/clientlibs.md#referencing-client-side-libraries" target="_blank">AEM のクライアントライブラリ参照フレームワーク</a>を使用するように更新する必要があります。</li> 
     <li>AEM のクライアントライブラリ参照フレームワークを使用できない場合、クライアントライブラリの絶対パスは AEM のクライアントライブラリプロキシサーブレットを介して参照できます:</li> 
    </ol> 
    <ul> 
     <li><code>/etc.clientlibs/cq/testandtarget/clientlibs/testandtarget/testandtarget.js</code></li> 
     <li><code>/etc.clientlibs/cq/testandtarget/clientlibs/testandtarget/atjs.js</code></li> 
     <li><code>/etc.clientlibs/cq/testandtarget/clientlibs/testandtarget/atjs-integration.js</code></li> 
     <li><code>/etc.clientlibs/cq/testandtarget/clientlibs/testandtarget/init.js</code></li> 
     <li><code>/etc.clientlibs/cq/testandtarget/clientlibs/testandtarget/mbox.js</code></li> 
     <li><code>/etc.clientlibs/cq/testandtarget/clientlibs/testandtarget/parameters.js</code></li> 
     <li><code>/etc.clientlibs/cq/testandtarget/clientlibs/testandtarget/util.js</code></li> 
    </ul> </td> 
  </tr>
  <tr>
   <td><strong>備考</strong></td> 
   <td><p>これらのクライアントライブラリの編集はサポートされていませんでした。</p> <p>クライアントライブラリのカテゴリを入手するには、CRXDELite で各 cq:ClientLIbraryFolder ノードを検索し、カテゴリプロパティを調べます:</p> 
    <ul> 
     <li><code>/libs/cq/testandtarget/clientlibs/testandtarget/testandtarget</code></li> 
     <li><code>/libs/cq/testandtarget/clientlibs/testandtarget/atjs</code></li> 
     <li><code>/libs/cq/testandtarget/clientlibs/testandtarget/atjs-integration</code></li> 
     <li><code>/libs/cq/testandtarget/clientlibs/testandtarget/init</code></li> 
     <li><code>/libs/cq/testandtarget/clientlibs/testandtarget/mbox</code></li> 
     <li><code>/libs/cq/testandtarget/clientlibs/testandtarget/parameters</code></li> 
     <li><code>/libs/cq/testandtarget/clientlibs/testandtarget/util</code></li> 
    </ul> </td> 
  </tr>
 </tbody>
</table>

### WCM Foundation クライアントライブラリ {#wcm-foundation-client-libraries}

<table> 
 <tbody>
  <tr>
   <td><strong>以前の場所</strong></td> 
   <td><p><code>/etc/clientlibs/wcm/foundation</code></p> </td> 
  </tr>
  <tr>
   <td><strong>新しい場所</strong></td> 
   <td><code>/libs/wcm/foundation/clientlibs</code></td> 
  </tr>
  <tr>
   <td><strong>再構築の手引き</strong></td> 
   <td><p>これらのクライアントライブラリをカスタムで使用する場合は、パスではなくカテゴリでクライアントライブラリを参照する必要があります。</p> 
    <ol> 
     <li>以前の場所のパスによるクライアントライブラリへの参照はすべて <a href="/help/sites-developing/clientlibs.md#referencing-client-side-libraries" target="_blank">AEM のクライアントライブラリ参照フレームワーク</a>を使用するように更新する必要があります。</li> 
     <li>AEM のクライアントライブラリ参照フレームワークを使用できない場合、クライアントライブラリの絶対パスは AEM のクライアントライブラリプロキシサーブレットを介して参照できます。</li> 
    </ol> 
    <ul> 
     <li><code>/etc.clientlibs/wcm/foundation/clientlibs/accessibility.css</code></li> 
     <li><code>/etc.clientlibs/wcm/foundation/clientlibs/main.css</code></li> 
     <li><code>/etc.clientlibs/wcm/foundation/clientlibs/main.js</code></li> 
    </ul> </td> 
  </tr>
  <tr>
   <td><strong>備考</strong></td> 
   <td><p>これらのクライアントライブラリの編集はサポートされていませんでした。</p> <p>クライアントライブラリのカテゴリを入手するには、CRXDELite で各 <code>cq:ClientLIbraryFolder</code> ノードを検索し、カテゴリプロパティを調べます:</p> 
    <ul> 
     <li><code>/libs/wcm/foundation/clientlibs/accessibility</code></li> 
     <li><code>/libs/wcm/foundation/clientlibs/main</code></li> 
    </ul> </td> 
  </tr>
 </tbody>
</table>
