---
title: AEM Communities 6.4 におけるリポジトリの再構築
seo-title: Repository Restructuring for AEM Communities in 6.4
description: AEM 6.4 for Communities の新しいリポジトリ構造に移行するために必要な変更を行う方法を説明します。
seo-description: Learn how to make the necessary changes in order to migrate to the new repository structure in AEM 6.4 for Communities.
uuid: d161655f-4074-44a7-8d69-38e80934c58b
products: SG_EXPERIENCEMANAGER/6.4/SITES
content-type: reference
topic-tags: repo_restructuring
discoiquuid: 7383265b-0ed4-4ea7-b741-0a417d187bdd
feature: Upgrading
exl-id: f66e349f-09a1-47f1-88fc-61eb51f65664
source-git-commit: c5b816d74c6f02f85476d16868844f39b4c47996
workflow-type: tm+mt
source-wordcount: '1044'
ht-degree: 72%

---

# AEM Communities 6.4 におけるリポジトリの再構築{#repository-restructuring-for-aem-communities-in}

>[!CAUTION]
>
>AEM 6.4 の拡張サポートは終了し、このドキュメントは更新されなくなりました。 詳細は、 [技術サポート期間](https://helpx.adobe.com/jp/support/programs/eol-matrix.html). サポートされているバージョンを見つける [ここ](https://experienceleague.adobe.com/docs/?lang=ja).

[AEM 6.4 におけるリポジトリの再構築](/help/sites-deploying/repository-restructuring.md)の親ページで説明しているように、AEM 6.4 にアップグレードする場合は、このページを参考に、AEM Communities ソリューションに影響を与えるリポジトリ変更に伴う作業量を評価する必要があります。一部の変更ではAEM 6.4 のアップグレードプロセス中に作業が必要ですが、6.5 のアップグレードまで延期することもできます。

**6.4 へのアップグレード時におこなう変更**

* [メール通知テンプレート](/help/sites-deploying/communities-repository-restructuring-in-aem-6-4.md#e-mail-notification-templates)
* [サブスクリプション設定](/help/sites-deploying/communities-repository-restructuring-in-aem-6-4.md#subscription-configurations)

**6.5 へのアップグレード前**

* [バッジ設定](/help/sites-deploying/communities-repository-restructuring-in-aem-6-4.md#badging-configurations)
* [従来の Communities コンソールデザイン](/help/sites-deploying/communities-repository-restructuring-in-aem-6-4.md#classic-communities-console-designs)
* [Facebook ソーシャルログイン設定](/help/sites-deploying/communities-repository-restructuring-in-aem-6-4.md#facebook-social-login-configurations)
* [言語オプション設定](/help/sites-deploying/communities-repository-restructuring-in-aem-6-4.md#language-options-configurations)

* [Pinterest ソーシャルログイン設定](/help/sites-deploying/communities-repository-restructuring-in-aem-6-4.md#pinterest-social-login-configurations)
* [スコアリング設定](/help/sites-deploying/communities-repository-restructuring-in-aem-6-4.md#scoring-configurations)
* [Twitter ソーシャルログイン設定](/help/sites-deploying/communities-repository-restructuring-in-aem-6-4.md#twitter-social-login-configurations)
* [その他](/help/sites-deploying/communities-repository-restructuring-in-aem-6-4.md#misc)

## 6.4 へのアップグレード時におこなう変更 {#with-upgrade}

### メール通知テンプレート {#e-mail-notification-templates}

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
   <td><p>「<code>/apps/settings</code>」の下の新しいパスに移動する場合は、手動移行が必要です。Granite 設定マネージャーを使用して、移行を実行できます。</p> <p>移行を実行するには、「<code>/libs/settings/community/subscriptions</code>」ノードのプロパティ <code>mergeList</code> を <code>true</code> に設定し、<code>nt:unstructured</code> 子ノードを追加します。</p> </td> 
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
   <td><p>「<code>/apps/settings</code>」の下の新しいパスに移動する場合は、手動移行が必要です。Granite 設定マネージャーを使用して、移行を実行できます。</p> <p>移行を実行するには、「<code>/libs/settings/community/subscriptions</code>」ノードのプロパティ <code>mergeList</code> を <code>true</code> に設定し、<code>nt:unstructured</code> 子ノードを追加します。</p> </td> 
  </tr>
  <tr>
   <td><strong>備考</strong></td> 
   <td>該当なし<br /> </td> 
  </tr>
 </tbody>
</table>

### ウォッチワード設定 {#watchwords-configurations}

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
   <td>Communities 設定をクリーンアップするために、遅延移行タスクを利用できます。<br /> <p>タスクはウォッチワードを <code>/etc/watchwords</code> から <code>/conf/global/settings/community/watchwords</code> に移動します。</p> <p>カスタマイズしたウォッチワードが SCM に格納されている場合は、それらを <code>/apps/settings/...</code> にデプロイしてください。また、優先されるオーバーレイ <code>/conf/global/settings/...</code> 設定がないようにする必要があります。</p> <p>移行タスクで <code>/etc</code> の場所が削除されます。</p> </td> 
  </tr>
  <tr>
   <td><strong>備考</strong></td> 
   <td>該当なし<br /> </td> 
  </tr>
 </tbody>
</table>

## 6.5 へのアップグレード前 {#prior-to-upgrade}

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
   <td><p>手動移行が必要です。</p> <p>インスタンスでバッジ/スコアルールをカスタマイズしている場合、すべてのルールをバケットの下に自動で配置する方法はありません。 サイトで使用する conf バケット（グローバルまたはサイト固有）に関する顧客入力が必要です。</p> <p>サイトのバッジとスコアを設定する UI がありません。</p> <p>新しいリポジトリ構造に合わせるには：</p> 
    <ol> 
     <li>を使用したサイトコンテキストバケットの作成 <strong>設定ブラウザー</strong> under <strong>ツール</strong></li> 
     <li>サイトのルートに移動します。</li> 
     <li><code>cq:confproperty</code> を、すべての設定を格納するバケットのパスに設定します。同じ設定をサイトの「<strong>編集ウィザード - クラウド設定入力</strong>」で行うこともできます。</li> 
     <li>関連するバッジルールおよびスコアルールを <code>/etc/community/*</code> から、前の手順で作成したサイトコンテキストバケットに移動します。</li> 
     <li>新しいルールの場所への相対参照を使用するように、サイトルートのバッジルールとスコアルールの各プロパティを調整します。 
      <ol> 
       <li>例えば、<code>cq:conf = /conf/we-retail</code> のプロパティの場合は <code>badgingRules [] = community/badging/rules</code> となります（ルールをこの新しいバケットに移動した場合）。</li> 
      </ol> </li> 
     <li>同様に、バッジルールノードのスコアルールへの参照も相対パスに変更します。</li> 
    </ol> <p> </p> <p>最後に、リソースを削除してクリーンアップします。 <code>/etc/community/badging</code></p> </td> 
  </tr>
  <tr>
   <td><strong>備考</strong></td> 
   <td>該当なし<br /> </td> 
  </tr>
 </tbody>
</table>

### 従来の Communities コンソールデザイン {#classic-communities-console-designs}

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
   <td><p>新しいFacebookクラウド設定は、すべて新しい場所に移行する必要があります。</p> 
    <ol> 
     <li>以前の場所の既存の設定を新しい場所に移行します。
      <ol> 
       <li>AEMオーサリング UI( ) で新しいFacebook Social ログイン設定を手動で再作成します。 <strong>ツール/Cloud Services/ Facebook Social ログイン設定</strong>.<br /> または <br /> </li> 
       <li>新しい Facebook クラウド設定をすべて、以前の場所から新しい適切な場所（<code>/conf/global or /conf/&lt;tenant&gt;</code> の下）にコピーします。</li> 
      </ol> </li> 
     <li>新しい Facebook ソーシャルログイン設定を参照するように AEM Communities サイトのルートを更新します。それには、<code>[cq:Page]/jcr:content@cq:conf</code> プロパティを新しい場所の絶対パスに設定します。</li> 
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
   <td><p>新しいPinterestクラウド設定は、すべて新しい場所に移行する必要があります。</p> 
    <ol> 
     <li>以前の場所の既存の設定を新しい場所に移行します。
      <ol> 
       <li>AEMオーサリング UI( ) で新しいPinterest Social ログイン設定を手動で再作成します。 <strong>ツール/Cloud Services/ Pinterest Social ログイン設定</strong>.<br />または</li> 
       <li>新しい Pinterest クラウド設定をすべて、以前の場所から適切な新しい場所（<code>/conf/global or /conf/&lt;tenant&gt;</code> の下）にコピーします。</li> 
      </ol> </li> 
     <li>新しい Pinterest ソーシャルログイン設定を参照するように AEM Communities サイトのルートを更新します。それには、<code>[cq:Page]/jcr:content@cq:conf</code> プロパティを新しい場所の絶対パスに設定します。</li> 
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
   <td><p>新しいリポジトリ構造に合わせるには、スコアルールの保存場所を <code>/apps/settings/</code> または次にします：/<code>conf/.../settings</code></p> 
    <ol> 
     <li><code>/apps/settings</code> の場合は、SCM で管理されるグローバルルールまたはデフォルトルールとして機能します。</li> 
    </ol> <p>次のように、CRXDELite を使用して、コンテキストに対応する設定を <code>/conf/</code> に作成します。</p> 
    <ol> 
     <li>目的の<code>/conf/.../settings</code>場所<br />に設定を作成します。 </li> 
     <li>Communities のサイトには <code>cq:conf </code> プロパティが設定されている必要があります。
      <ol> 
       <li><code>cq:conf</code> を設定していない場合、スコアルールは、サイトのルートノードの「<code>scoringRules</code>」プロパティに設定したパスから直接読み取られます。次に例を示します。 <code>/content/we-retail/us/en/community/jcr:content</code></li> 
      </ol> </li> 
    </ol> <p>クリーンアップ：リソースを削除する <code>/etc/community/scoring</code></p> </td> 
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
   <td><p>新しいTwitterクラウド設定は、すべて新しい場所に移行する必要があります。</p> 
    <ol> 
     <li>以前の場所の既存の設定を新しい場所に移行します。
      <ol> 
       <li>AEMオーサリング UI( ) で新しいTwitter Social ログイン設定を手動で再作成します。 <strong>ツール/Cloud Services/ Twitter Social ログイン設定</strong>.<br /> または <br /> </li> 
       <li>新しい Twitter クラウド設定をすべて、以前の場所から適切な新しい場所（<code>/conf/global or /conf/&lt;tenant&gt;</code> の下）にコピーします。</li> 
      </ol> </li> 
     <li>新しい Twitter ソーシャルログイン設定を参照するように AEM Communities サイトのルートを更新します。それには、<code>[cq:Page]/jcr:content@cq:conf</code> プロパティを新しい場所の絶対パスに設定します。</li> 
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
   <td><p>Adobeは、次の場所に移行ユーティリティを提供しています。</p> <p><a href="https://github.com/Adobe-Marketing-Cloud/aem-communities-ugc-migration/tree/master/bundles/communities-template-migration">https://github.com/Adobe-Marketing-Cloud/aem-communities-ugc-migration/tree/master/bundles/communities-template-migration</a></p> </td> 
  </tr>
  <tr>
   <td><strong>備考</strong></td> 
   <td>既存のカスタムテンプレートの移動先： <code>/conf/global/settings/community/template/&lt;groups/sites/functions&gt;</code></td> 
  </tr>
 </tbody>
</table>
