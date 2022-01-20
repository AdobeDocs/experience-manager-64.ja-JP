---
title: 6.4 における AEM Communities のリポジトリ再構築
seo-title: Repository Restructuring for AEM Communities in 6.4
description: AEM 6.4 for Communities の新しいリポジトリ構造に移行するために必要な変更を加える方法について説明します。
seo-description: Learn how to make the necessary changes in order to migrate to the new repository structure in AEM 6.4 for Communities.
uuid: d161655f-4074-44a7-8d69-38e80934c58b
products: SG_EXPERIENCEMANAGER/6.4/SITES
content-type: reference
topic-tags: repo_restructuring
discoiquuid: 7383265b-0ed4-4ea7-b741-0a417d187bdd
feature: Upgrading
exl-id: f66e349f-09a1-47f1-88fc-61eb51f65664
source-git-commit: bd94d3949f0117aa3e1c9f0e84f7293a5d6b03b4
workflow-type: tm+mt
source-wordcount: '1008'
ht-degree: 60%

---

# 6.4 における AEM Communities のリポジトリ再構築{#repository-restructuring-for-aem-communities-in}

親の説明に従って [AEM 6.4 におけるリポジトリの再構築](/help/sites-deploying/repository-restructuring.md) このページでは、AEM 6.4 にアップグレードするお客様は、このページを使用して、AEM Communitiesソリューションに影響を与えるリポジトリの変更に関連する作業量を評価する必要があります。 一部の変更は AEM 6.4 アップグレードプロセス中に作業が必要ですが、それ以外は 6.5 アップグレードまで延期できます。

**6.4 へのアップグレード時におこなう変更**

* [電子メール通知テンプレート](/help/sites-deploying/communities-repository-restructuring-in-aem-6-4.md#e-mail-notification-templates)
* [サブスクリプション設定](/help/sites-deploying/communities-repository-restructuring-in-aem-6-4.md#subscription-configurations)

**6.5 へのアップグレードまでにおこなう変更**

* [バッジ設定](/help/sites-deploying/communities-repository-restructuring-in-aem-6-4.md#badging-configurations)
* [従来のコミュニティコンソールデザイン](/help/sites-deploying/communities-repository-restructuring-in-aem-6-4.md#classic-communities-console-designs)
* [Facebook ソーシャルログイン設定](/help/sites-deploying/communities-repository-restructuring-in-aem-6-4.md#facebook-social-login-configurations)
* [言語オプション設定](/help/sites-deploying/communities-repository-restructuring-in-aem-6-4.md#language-options-configurations)

* [Pinterest ソーシャルログイン設定](/help/sites-deploying/communities-repository-restructuring-in-aem-6-4.md#pinterest-social-login-configurations)
* [スコアリング設定](/help/sites-deploying/communities-repository-restructuring-in-aem-6-4.md#scoring-configurations)
* [Twitter ソーシャルログイン設定](/help/sites-deploying/communities-repository-restructuring-in-aem-6-4.md#twitter-social-login-configurations)
* [その他](/help/sites-deploying/communities-repository-restructuring-in-aem-6-4.md#misc)

## 6.4 へのアップグレード時におこなう変更 {#with-upgrade}

### 電子メール通知テンプレート {#e-mail-notification-templates}

<table> 
 <tbody>
  <tr>
   <td><strong>以前の場所</strong></td> 
   <td><code>/etc/community/notifications</code></td> 
  </tr>
  <tr>
   <td><strong>新しい場所</strong></td> 
   <td><code>/libs/settings/community/notifications</code></td> 
  </tr>
  <tr>
   <td><strong>再構築の手引き</strong></td> 
   <td><p>「<code>/apps/settings</code>". Granite 設定マネージャーを使用して、移行を実行できます。</p> <p>移行は、プロパティを設定して実行できます <code>mergeList</code> から <code>true</code> 」<code>/libs/settings/community/subscriptions</code>」ノードを追加し、 <code>nt:unstructured</code> 子ノード。</p> </td> 
  </tr>
  <tr>
   <td><strong>備考</strong></td> 
   <td>該当なし<br /> </td> 
  </tr>
 </tbody>
</table>

### サブスクリプション設定 {#subscription-configurations}

<table> 
 <tbody>
  <tr>
   <td><strong>以前の場所</strong></td> 
   <td><code>/etc/community/subscriptions</code></td> 
  </tr>
  <tr>
   <td><strong>新しい場所</strong></td> 
   <td><code>/libs/settings/community/subscriptions</code></td> 
  </tr>
  <tr>
   <td><strong>再構築の手引き</strong></td> 
   <td><p>「<code>/apps/settings</code>". Granite 設定マネージャーを使用して、移行を実行できます。</p> <p>移行は、プロパティを設定して実行できます <code>mergeList</code> から <code>true</code> 」<code>/libs/settings/community/subscriptions</code>」ノードを追加し、 <code>nt:unstructured</code> 子ノード。</p> </td> 
  </tr>
  <tr>
   <td><strong>備考</strong></td> 
   <td>該当なし<br /> </td> 
  </tr>
 </tbody>
</table>

### 監視ワード設定 {#watchwords-configurations}

<table> 
 <tbody>
  <tr>
   <td><strong>以前の場所</strong></td> 
   <td>/etc/watchwords</td> 
  </tr>
  <tr>
   <td><strong>新しい場所</strong></td> 
   <td>/libs/community/watchwords</td> 
  </tr>
  <tr>
   <td><strong>再構築の手引き</strong></td> 
   <td>Communities 設定をクリーンアップするために、遅延移行タスクを利用できます。<br /> <p>タスクはウォッチワードを <code>/etc/watchwords</code> から <code>/conf/global/settings/community/watchwords</code>.</p> <p>カスタマイズした監視ワードが SCM に格納されている場合は、 <code>/apps/settings/...</code> そしてオーバーレイがないようにする必要があります <code>/conf/global/settings/...</code> 優先する設定です。</p> <p>移行タスクが削除されました <code>/etc</code> 場所。</p> </td> 
  </tr>
  <tr>
   <td><strong>備考</strong></td> 
   <td>該当なし<br /> </td> 
  </tr>
 </tbody>
</table>

## 6.5 へのアップグレードまでにおこなう変更 {#prior-to-upgrade}

### バッジ設定 {#badging-configurations}

<table> 
 <tbody>
  <tr>
   <td><strong>以前の場所</strong></td> 
   <td><code>/etc/community/badging</code></td> 
  </tr>
  <tr>
   <td><strong>新しい場所</strong></td> 
   <td><p><strong>バッジルール：</strong></p> <p><code>/libs/settings/community/badging</code></p> <p><strong>バッジ画像：</strong></p> <p>デフォルト画像の場合： <code>/etc/community/badging/images are moved to /libs/community/badging/images</code></p> <p>カスタム画像の場合： <code>/content/community/badging/images</code></p> <p> </p> </td> 
  </tr>
  <tr>
   <td><strong>再構築の手引き</strong></td> 
   <td><p>手動移行が必要です。</p> <p>インスタンスがバッジ／スコアルールをカスタマイズしている場合、すべてのルールをバケットの下に自動的に配置する方法はありません。サイトに使用する conf バケット（グローバルまたはサイト固有）に関する顧客からの情報が必要です。</p> <p>サイトのバッジおよびスコア設定に使用できる UI はありません。</p> <p>新しいリポジトリ構造に合わせるには：</p> 
    <ol> 
     <li><strong>ツール</strong>の下の<strong>設定ブラウザー</strong>を使用して、サイトコンテキストバケットを作成します。</li> 
     <li>サイトのルートに移動します。</li> 
     <li>設定 <code>cq:confproperty</code> を、すべての設定を保存するバケットのパスに設定します。 同じ設定をサイトの「<strong>編集ウィザード - クラウド設定入力</strong>」でおこなうこともできます。</li> 
     <li>次の場所に関連するバッジルールとスコアルールを移動します： <code>/etc/community/*</code> を、前の手順で作成したサイトコンテキストバケットに追加します。</li> 
     <li>新しいルールの場所への相対参照を使用するように、サイトルートのバッジルールおよびスコアルールプロパティを調整します。 
      <ol> 
       <li>例えば、 <code>cq:conf = /conf/we-retail</code>を、 <code>badgingRules [] = community/badging/rules</code> （ルールがこの新しいバケットに移動された場合）。</li> 
      </ol> </li> 
     <li>同様に、バッジルールノードのスコアルールへの参照も相対パスに変更します。</li> 
    </ol> <p> </p> <p>最後に、リソースを削除してクリーンアップします <code>/etc/community/badging</code></p> </td> 
  </tr>
  <tr>
   <td><strong>備考</strong></td> 
   <td>該当なし<br /> </td> 
  </tr>
 </tbody>
</table>

### 従来のコミュニティコンソールデザイン {#classic-communities-console-designs}

<table> 
 <tbody>
  <tr>
   <td><strong>以前の場所</strong></td> 
   <td><code>/etc/designs/social/console</code></td> 
  </tr>
  <tr>
   <td><strong>新しい場所</strong></td> 
   <td><p><code>/libs/settings/wcm/designs/social/console</code></p> <p><code>/apps/settings/wcm/designs/social/console</code></p> </td> 
  </tr>
  <tr>
   <td><strong>再構築の手引き</strong></td> 
   <td>該当なし</td> 
  </tr>
  <tr>
   <td><strong>備考</strong></td> 
   <td>該当なし<br /> </td> 
  </tr>
 </tbody>
</table>

### Facebook ソーシャルログイン設定 {#facebook-social-login-configurations}

<table> 
 <tbody>
  <tr>
   <td><strong>以前の場所</strong></td> 
   <td><code>/etc/cloudservices/facebookconnect</code></td> 
  </tr>
  <tr>
   <td><strong>新しい場所</strong></td> 
   <td><p><code class="code">/conf/global/settings/cloudconfigs/facebookconnect
       </code></p> <p><code>/conf/&lt;tenant&gt;/settings/cloudconfigs/facebookconnect</code></p> <p> </p> </td> 
  </tr>
  <tr>
   <td><strong>再構築の手引き</strong></td> 
   <td><p>新しい Facebook クラウド設定をすべて、新しい場所に移行する必要があります。</p> 
    <ol> 
     <li>以前の場所にある既存の設定を新しい場所に移行します。
      <ol> 
       <li><strong>ツール／クラウドサービス／Facebook ソーシャルログイン設定</strong>で、AEM オーサリング UI を使用して新しい Facebook ソーシャルログイン設定を手動で再作成します。<br /> か <br /> のどちらかにする必要があります。 </li> 
       <li>新しいFacebookクラウド設定を以前の場所から適切な新しい場所（の下）にコピーします。 <code>/conf/global or /conf/&lt;tenant&gt;</code>.</li> 
      </ol> </li> 
     <li>新しいAEM Communities Social ログイン設定を参照するように、 Facebookサイトのルートを更新するには、 <code>[cq:Page]/jcr:content@cq:conf</code> プロパティを新しい場所の絶対パスに設定します。</li> 
     <li>新しい場所を参照するように更新した AEM Communities サイトのルートから、従来の Facebook Connect クラウドサービスの関連付けを解除します。</li> 
    </ol> </td> 
  </tr>
  <tr>
   <td><strong>備考</strong></td> 
   <td>該当なし<br /> </td> 
  </tr>
 </tbody>
</table>

### 言語オプション設定 {#language-options-configurations}

<table> 
 <tbody>
  <tr>
   <td><strong>以前の場所</strong></td> 
   <td><code>/etc/social/config/languageOpts</code></td> 
  </tr>
  <tr>
   <td><strong>新しい場所</strong></td> 
   <td><code>/libs/social/translation/languageOpts</code></td> 
  </tr>
  <tr>
   <td><strong>再構築の手引き</strong></td> 
   <td>該当なし<br /> </td> 
  </tr>
  <tr>
   <td><strong>備考</strong></td> 
   <td>該当なし<br /> </td> 
  </tr>
 </tbody>
</table>

### Pinterest ソーシャルログイン設定 {#pinterest-social-login-configurations}

<table> 
 <tbody>
  <tr>
   <td><strong>以前の場所</strong></td> 
   <td><code>/etc/cloudservices/pinterestconnect</code></td> 
  </tr>
  <tr>
   <td><strong>新しい場所</strong></td> 
   <td><p><code class="code">/conf/global/settings/cloudconfigs/pinterestconnect
       </code></p> <p><code>/conf/&lt;tenant&gt;/settings/cloudconfigs/pinterestconnect</code></p> <p> </p> </td> 
  </tr>
  <tr>
   <td><strong>再構築の手引き</strong></td> 
   <td><p>新しい Pinterest クラウド設定をすべて、新しい場所に移行する必要があります。</p> 
    <ol> 
     <li>以前の場所にある既存の設定を新しい場所に移行します。
      <ol> 
       <li><strong>ツール／クラウドサービス／Pinterest ソーシャルログイン設定</strong>で、AEM オーサリング UI を使用して新しい Pinterest ソーシャルログイン設定を手動で再作成します。<br /> または</li> 
       <li>新しいPinterestクラウド設定を以前の場所からの適切な新しい場所 ( <code>/conf/global or /conf/&lt;tenant&gt;</code>.</li> 
      </ol> </li> 
     <li>AEM Communities Site のルートを更新し、新しいPinterest Social ログイン設定を参照するように、 <code>[cq:Page]/jcr:content@cq:conf</code> プロパティを新しい場所の絶対パスに設定します。</li> 
     <li>新しい場所を参照するように更新した AEM Communities サイトのルートから、従来の Pinterest Connect クラウドサービスの関連付けを解除します。</li> 
    </ol> </td> 
  </tr>
  <tr>
   <td><strong>備考</strong></td> 
   <td>該当なし<br /> </td> 
  </tr>
 </tbody>
</table>

### スコアリング設定 {#scoring-configurations}

<table> 
 <tbody>
  <tr>
   <td><strong>以前の場所</strong></td> 
   <td><code>/etc/community/scoring</code></td> 
  </tr>
  <tr>
   <td><strong>新しい場所</strong></td> 
   <td><code>/libs/settings/community/scoring</code></td> 
  </tr>
  <tr>
   <td><strong>再構築の手引き</strong></td> 
   <td><p>新しいリポジトリ構造に合わせるために、スコア付けルールを <code>/apps/settings/</code> または/<code>conf/.../settings</code></p> 
    <ol> 
     <li>の場合 <code>/apps/settings</code>を指定した場合、SCM で管理されるグローバルルールまたはデフォルトルールとして機能します。</li> 
    </ol> <p>でのコンテキスト対応設定の作成 <code>/conf/</code> CRXDE Lite を使用する場合：</p> 
    <ol> 
     <li>目的ので設定を作成します。 <code>/conf/.../settings</code> 場所<br /> </li> 
     <li>コミュニティサイトに <code>cq:conf </code>プロパティプロパティセット。
      <ol> 
       <li>指定しない場合 <code>cq:conf</code> が設定されている場合、スコア付けルールは、プロパティ「 」の指定されたパスから直接読み取られます<code>scoringRules</code>「 」をサイトのルートノードに配置します。例： <code>/content/we-retail/us/en/community/jcr:content</code></li> 
      </ol> </li> 
    </ol> <p>クリーンアップ：リソースを削除 <code>/etc/community/scoring</code></p> </td> 
  </tr>
  <tr>
   <td><strong>備考</strong></td> 
   <td>該当なし<br /> </td> 
  </tr>
 </tbody>
</table>

### Twitter ソーシャルログイン設定 {#twitter-social-login-configurations}

<table> 
 <tbody>
  <tr>
   <td><strong>以前の場所</strong></td> 
   <td><code>/etc/cloudservices/twitterconnect</code></td> 
  </tr>
  <tr>
   <td><strong>新しい場所</strong></td> 
   <td><p><code class="code">/conf/global/settings/cloudconfigs/twitterconnect
       </code></p> <p><code>/conf/&lt;tenant&gt;/settings/cloudconfigs/twitterconnect</code></p> <p> </p> </td> 
  </tr>
  <tr>
   <td><strong>再構築の手引き</strong></td> 
   <td><p>新しい Twitter クラウド設定をすべて、新しい場所に移行する必要があります。</p> 
    <ol> 
     <li>以前の場所にある既存の設定を新しい場所に移行します。
      <ol> 
       <li><strong>ツール／クラウドサービス／Twitter ソーシャルログイン設定</strong>で、AEM オーサリング UI を使用して新しい Twitter ソーシャルログイン設定を手動で再作成します。<br /> か <br /> のどちらかにする必要があります。 </li> 
       <li>新しいTwitterクラウド設定を以前の場所から適切な新しい場所（の下）にコピーします。 <code>/conf/global or /conf/&lt;tenant&gt;</code>.</li> 
      </ol> </li> 
     <li>新しいAEM Communities Social ログイン設定を参照するように、 Twitterサイトのルートを更新するには、 <code>[cq:Page]/jcr:content@cq:conf</code> プロパティを新しい場所の絶対パスに設定します。</li> 
     <li>新しい場所を参照するように更新した AEM Communities サイトのルートから、従来の Twitter Connect クラウドサービスの関連付けを解除します。</li> 
    </ol> </td> 
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
   <td><code>/etc/community/templates</code></td> 
  </tr>
  <tr>
   <td><strong>新しい場所</strong></td> 
   <td><code>/libs/settings/community/templates</code></td> 
  </tr>
  <tr>
   <td><strong>再構築の手引き</strong></td> 
   <td><p>アドビでは、以下で移行ユーティリティを提供しています。</p> <p><a href="https://github.com/Adobe-Marketing-Cloud/aem-communities-ugc-migration/tree/master/bundles/communities-template-migration">https://github.com/Adobe-Marketing-Cloud/aem-communities-ugc-migration/tree/master/bundles/communities-template-migration</a></p> </td> 
  </tr>
  <tr>
   <td><strong>備考</strong></td> 
   <td>既存のカスタムテンプレートの移動先 <code>/conf/global/settings/community/template/&lt;groups/sites/functions&gt;</code></td> 
  </tr>
 </tbody>
</table>
