---
title: Dynamic Media - Scene7 モードのトラブルシューティング
description: Dynamic Media - Scene7実行モードのトラブルシューティング。
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.4/ASSETS
topic-tags: dynamic-media
content-type: reference
exl-id: d8cc94b0-eacf-4e76-bd50-7934bbc28c92
feature: トラブルシューティング
role: Admin,User
source-git-commit: 5d96c09ef764b02e08dcdf480da1ee18f4d9a30c
workflow-type: tm+mt
source-wordcount: '1296'
ht-degree: 87%

---

# Dynamic Media - Scene7 モードのトラブルシューティング {#troubleshooting-dynamic-media-scene-mode}

以下のドキュメントでは、**dynamicmedia_scene7** 実行モードで実行している Dynamic Media のトラブルシューティングについて説明します。

## セットアップと設定 {#setup-and-configuration}

以下の手順で、Dynamic Media が適切に設定されていることを確認します。

* 起動コマンドには、`-r dynamicmedia_scene7`実行モード引数が含まれます。
* 使用可能な Dynamic Media 機能パックよりも先に、AEM 6.4 累積修正パック（CFP）がインストールされていることを確認します。**
* オプションの機能パック 18912 がインストールされていることを確認します。

   このオプションの機能パックは、FTPサポート用、またはDynamic Media ClassicからDynamic Mediaにアセットを移行する場合に使用します。

* クラウドサービスのユーザーインターフェイスに移動して、「**[!UICONTROL 利用可能な設定]**」の下に割り当てられたアカウントが表示されることを確認します。
* **[!UICONTROL Dynamic Media Asset Activation(scene7)]**&#x200B;レプリケーションエージェントが有効になっていることを確認します。

   このレプリケーションエージェントは、オーサーの&#x200B;**[!UICONTROL エージェント]**&#x200B;の下にあります。

## 一般（すべてのアセット） {#general-all-assets}

次に全般的なヒントやテクニックを示します。

### アセット同期ステータスプロパティ {#asset-synchronization-status-properties}

CRXDE Lite で次のアセットプロパティを見直すと、AEM から Dynamic Media へのアセットの同期に成功したことが確認できます。

| **プロパティ** | **例** | **説明** |
|---|---|---|
| `<object_node>/jcr:content/metadata/dam:scene7ID` | `a|364266` | ノードが Dynamic Media にリンクされていることを示す全般的インジケーター。 |
| `<object_node>/jcr:content/metadata/dam:scene7FileStatus` | **[!UICONTROL PublishComplete]** またはエラーテキスト | Dynamic Media へのアセットアップロードのステータス。 |
| `<object_node>/jcr:content/metadata/dam:scene7File` | `myCompany/myAssetID` | Dynamic Media のリモートアセットへの URL を生成するには、これを入力する必要があります。 |
| `<object_node>/jcr:content/dam:lastSyncStatus` | `success` か `failed:<error text>` のどちらかにする必要があります。 | セット（スピンセット、画像セットなど）、画像プリセット、ビューアプリセット、アセットの画像マップの更新、編集された画像などの同期ステータス。 |

### 同期のログ {#synchronization-logging}

同期のエラーと問題は `error.log`（AEM サーバーディレクトリの `/crx-quickstart/logs/`）に記録されます。ログにはほとんどの問題の根本原因を突き止めるのに十分な情報が記録されますが、Slingコンソール([http://localhost:4502/system/console/slinglog](http://localhost:4502/system/console/slinglog))を通じて`com.adobe.cq.dam.ips`パッケージのログをデバッグに増やして、詳細を収集できます。

### 移動、コピー、削除 {#move-copy-delete}

移動、コピーまたは削除の処理を実行する前に次をおこなってください。

* 画像やビデオの移動、コピーまたは削除操作の前に `<object_node>/jcr:content/metadata/dam:scene7ID` の値が存在することを確認します。
* 画像やビューアプリセットの移動、コピーまたは削除操作の前に `https://<server>/crx/de/index.jsp#/etc/dam/presets/viewer/testpreset/jcr%3Acontent/metadata` の値が存在することを確認します。
* 上記のメタデータ値がない場合、移動、コピーまたは削除処理の前にアセットを再度アップロードする必要があります。

### バージョン管理 {#version-control}

既存のDynamic Mediaアセット（同じ名前と場所）を置き換える場合、両方のアセットを保持するか、バージョンを置き換えるか、作成するかを選択できます。

* 両方を保持すると、公開済みアセットURLの一意の名前を持つ新しいアセットが作成されます。例えば、 **[!UICONTROL image.jpg]**&#x200B;は元のアセット、 **[!UICONTROL image1.jpg]**&#x200B;は新しくアップロードされたアセットです。

* Dynamic Media - Scene7 モードの配信ではバージョン作成はサポートされていません。配信の既存アセットが新しいバージョンに置き換わります。

## 画像とセット {#images-and-sets}

画像とセットで問題が発生している場合、次のトラブルシューティングガイドに従ってください。

<table> 
 <tbody> 
  <tr> 
   <td><strong>問題</strong></td> 
   <td><strong>デバッグの方法</strong></td> 
   <td><strong>解決策</strong></td> 
  </tr> 
  <tr> 
   <td>アセットの詳細表示で URL／埋め込みコードのコピーボタンにアクセスできない</td> 
   <td> 
    <ol> 
     <li><p>CRX/DE に移動します。</p> 
      <ul> 
       <li>JCR 内のプリセット <code>/etc/dam/presets/viewer/&lt;preset&gt; has lastReplicationAction</code> が定義されているかどうかを確認します。この場所は、AEM 6.x から 6.4 にアップグレードし、移行をオプトアウトした場合に適用されます。それ以外の場合、場所は <code>/conf/global/settings/dam/dm/presets/viewer</code> になります。</li> 
       <li>JCR のアセットに <code>dam:scene7FileStatus</code><strong> </strong> があり、それが「メタデータ」で <code>PublishComplete</code> と表示されていることを確認します。</li> 
      </ul> </li> 
    </ol> </td> 
   <td><p>ページを更新するか、別のページに移動してから戻ります（サイドレール JSP を再コンパイルする必要があります）。</p> <p>それでも解決しない場合：</p> 
    <ul> 
     <li>アセットを公開します。</li> 
     <li>アセットを再度アップロードして公開します。</li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td>設定エディターのアセットセレクターが永続的に読み込み中の状態になっている</td> 
   <td><p>6.4 で解決予定の既知の問題です。</p> </td> 
   <td><p>セレクターを閉じて再度開きます。</p> </td> 
  </tr> 
  <tr> 
   <td>セットの編集でアセットを選択した後、<strong>選択</strong>ボタンが有効にならない</td> 
   <td><p> </p> <p>6.4 で解決予定の既知の問題です。</p> <p> </p> </td> 
   <td><p>アセットセレクターで別のフォルダーをクリックしてからアセットの選択に戻ります。</p> </td> 
  </tr> 
  <tr> 
   <td>スライドを切り替えた後、カルーセルホットスポットが移動する</td> 
   <td><p>すべてのスライドが同じサイズであることを確認します。</p> </td> 
   <td><p>カルーセルにはすべて同じサイズの画像のみを利用します。</p> </td> 
  </tr> 
  <tr> 
   <td>Dynamic Media ビューアで画像がプレビューされない</td> 
   <td><p>アセットのメタデータプロパティに <code>dam:scene7File</code> が含まれていることを確認します（CRXDE Lite）。</p> </td> 
   <td><p>すべてのアセットの処理が終わるまで待ちます。</p> </td> 
  </tr> 
  <tr> 
   <td>アップロードしたアセットがアセットセレクターに表示されない</td> 
   <td><p>アセットのプロパティ <code>jcr:content</code> &gt; <strong><code>dam:assetState</code></strong> が <code>processed</code> であることを確認します（CRXDE Lite）。</p> </td> 
   <td><p>すべてのアセットの処理が終わるまで待ちます。</p> </td> 
  </tr> 
  <tr> 
   <td>アセットの処理がまだ開始していないときに、カード表示のバナーに「<strong>新規</strong>」と表示される</td> 
   <td>アセットの <code>jcr:content</code> &gt; <code>dam:assetState</code> を確認します。<code>unprocessed</code> の場合は、アセットの処理がワークフローで開始されていません。</td> 
   <td>ワークフローがアセットの処理を始めるまで待ちます。</td> 
  </tr> 
  <tr> 
   <td>画像やセットでビューア URL や埋め込みコードが表示されない</td> 
   <td>ビューアプリセットが公開されているかどうかを確認します。</td> 
   <td><p><strong>ツール</strong>／<strong>アセット</strong>／<strong>ビューアプリセット</strong>に移動し、ビューアプリセットを公開します。</p> </td> 
  </tr> 
 </tbody> 
</table>

## ビデオ {#video}

ビデオで問題が発生している場合、次のトラブルシューティングガイドに従ってください。

<table> 
 <tbody> 
  <tr> 
   <td><strong>問題</strong></td> 
   <td><strong>デバッグの方法</strong></td> 
   <td><strong>解決策</strong></td> 
  </tr> 
  <tr> 
   <td>ビデオをプレビューできない</td> 
   <td> 
    <ul> 
     <li>フォルダーにビデオプロファイルが割り当てられていることを確認します（サポートされていないファイル形式の場合）。サポートされていない場合、画像だけが表示されます。</li> 
     <li>ビデオプロファイルには AVS セットを生成するためのエンコーディングプリセットが 2 つ以上含まれている必要があります（MP4 ファイルでは 1 つのエンコーディングがビデオコンテンツとして扱われます。サポートされていないファイルでは、処理されていないものと同じ扱いになります）。</li> 
     <li>メタデータで <code>dam:scene7File</code> の <code>dam:scene7FileAvs</code> を確認して、ビデオの処理が終了したことを確かめます。</li> 
    </ul> </td> 
   <td> 
    <ol> 
     <li>ビデオプロファイルをフォルダーに割り当てます。</li> 
     <li>エンコーディングプリセットを 2 つ以上含むよう、ビデオプロファイルを編集します。</li> 
     <li>ビデオの処理が終わるのを待ちます。</li> 
     <li>ビデオを再度読み込み、「Dynamic Media エンコーディングビデオ」ワークフローが実行されていないことを確認します。<br /> </li> 
     <li>ビデオを再度アップロードします。</li> 
    </ol> </td> 
  </tr> 
  <tr> 
   <td>ビデオがエンコードされていない</td> 
   <td> 
    <ul> 
     <li>実行モードが <span class="kbd">dynamicmedia_scene7</span> になっていることを確認します。</li> 
     <li>Dynamic Media クラウドサービスが設定されていることを確認します。</li> 
     <li>ビデオプロファイルがアップロードフォルダーに関連付けられていることを確認します。</li> 
    </ul> </td> 
   <td> 
    <ol> 
     <li><span class="kbd">-r dynamicmedia_scene7</span> で AEM インスタンスを起動します。</li> 
     <li>クラウドサービスページで Dynamic Media 設定が正しくセットアップされていることを確認します。</li> 
     <li>フォルダーにビデオプロファイルがあることを確認します。そのビデオプロファイルも確認します。</li> 
    </ol> </td> 
  </tr> 
  <tr> 
   <td>ビデオの処理に時間がかかりすぎる</td> 
   <td><p>ビデオのエンコーディングがまだ進行中か、エラー状態になっているかを判断するには：</p> 
    <ul> 
     <li>ビデオのステータスを確認します。<code>http://localhost:4502/crx/de/index.jsp#/content/dam/folder/videomp4/jcr%3Acontent</code> &gt;  <span class="kbd">dam:assetState</span></li> 
     <li>ワークフローコンソールでビデオを監視します。<code>http://localhost:4502/libs/cq/workflow/content/console.html</code> &gt; 「インスタンス」タブ、「アーカイブ」タブ、「エラー」タブ。</li> 
    </ul> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>ビデオレンディションがない</td> 
   <td><p>ビデオがアップロードされても、エンコードされたレンディションがない場合：</p> 
    <ul> 
     <li>フォルダーにビデオプロファイルが割り当てられていることを確認します。</li> 
     <li>メタデータで <code>dam:scene7FileAvs</code> を確認して、ビデオの処理が終了したことを確かめます。</li> 
    </ul> </td> 
   <td> 
    <ol> 
     <li>ビデオプロファイルをフォルダーに割り当てます。</li> 
     <li>ビデオの処理が終わるのを待ちます。<br /> </li> 
    </ol> </td> 
  </tr> 
 </tbody> 
</table>

## ビューア {#viewers}

ビューアで問題が発生している場合、次のトラブルシューティングガイドに従ってください。

<table> 
 <tbody> 
  <tr> 
   <td><strong>問題</strong></td> 
   <td><strong>デバッグの方法</strong></td> 
   <td><strong>解決策</strong></td> 
  </tr> 
  <tr> 
   <td>ビューアプリセットが公開されていない</td> 
   <td><p>次のサンプルマネージャー診断ページに移動します。 <code>http://localhost:4502/libs/dam/gui/content/s7dam/samplemanager/samplemanager.html</code></p> <p>計算された値を確認します。正常に動作している場合は、次のようになります。</p> <p><code class="code">_DMSAMPLE status: 0 unsyced assets - activation not necessary
       _OOTB status: 0 unsyced assets - 0 unactivated assets</code></p> <p><strong>注意</strong>：Dynamic Media クラウドの設定後、ビューアアセットが同期するまで 10 分ほどかかることがあります。</p> <p>アクティブでないアセットが残る場合は、「<strong>アクティブでないアセットをすべて表示</strong>」ボタンのどちらかをクリックして詳細を確認してください。</p> </td> 
   <td> 
    <ol> 
     <li>管理ツールのビューアプリセットリストに移動します。 <code>http://localhost:4502/libs/dam/gui/content/s7dam/samplemanager/samplemanager.html</code></li> 
     <li>すべてのビューアプリセットを選択し、「<strong>公開</strong>」をクリックします。</li> 
     <li>サンプルマネージャーに戻り、アクティブでないアセット数がゼロになったことを確認します。</li> 
    </ol> </td> 
  </tr> 
  <tr> 
   <td>ビューアプリセットのアートワークが、アセット詳細のプレビューまたは URL／埋め込みコードのコピーで 404 を返す場合</td> 
   <td><p>CRXDE Lite で以下を行います。</p> 
    <ol> 
     <li>Dynamic Media 同期フォルダー内の <code>&lt;sync-folder&gt;/_CSS/_OOTB</code> フォルダー（例えば <code>/content/dam/_CSS/_OOTB</code>）に移動します。</li> 
     <li>問題のあるアセットのメタデータノードを見つけます（例えば <code>&lt;sync-folder&gt;/_CSS/_OOTB/CarouselDotsLeftButton_dark_sprite.png/jcr:content/metadata/</code>）。</li> 
     <li><code>dam:scene7*</code> プロパティがあることを確認します。アセットの同期と公開に成功した場合は <code>dam:scene7FileStatus</code> が <strong>PublishComplete</strong> に設定されています。</li> 
     <li>次のプロパティと文字列リテラルの値を連結して Dynamic Media に直接アートワークを要求します。 
      <ul> 
       <li><code>dam:scene7Domain</code></li> 
       <li><code>"is/content"</code></li> 
       <li><code>dam:scene7Folder</code></li> 
       <li><code>&lt;asset-name&gt;</code></li> 
       <li>例： <code>https://&lt;server&gt;/is/content/myfolder/_CSS/_OOTB/CarouselDotsLeftButton_dark_sprite.png</code></li> 
      </ul> </li> 
    </ol> </td> 
   <td><p>サンプルアセットまたはビューアプリセットのアートワークが同期されていないか、公開されてない場合は、コピー／同期処理全体をやり直します。</p> 
    <ol> 
     <li>CRXDE Lite に移動します。 
      <ul> 
       <li><code>&lt;sync-folder&gt;/_CSS/_OOTB</code> を削除します。</li> 
      </ul> </li> 
     <li>CRX パッケージマネージャー（<code>http://localhost:4502/crx/packmgr/</code><a href="http://localhost:4502/crx/packmgr/"></a>）に移動します。 
      <ol> 
       <li>リストでビューアパッケージを検索します（<span class="kbd">cq-dam-scene7-viewers-content</span> で始まります）。</li> 
       <li>「<strong>再インストール</strong>」をクリックします。</li> 
      </ol> </li> 
     <li>クラウドサービスページで、Dynamic Media 設定ページに移動した後、Dynamic Media - Scene7 設定の設定ダイアログボックスを開きます。 
      <ul> 
       <li>何も変更せず、「<strong>保存</strong>」をクリックします。これで、サンプルアセット、ビューアプリセット CSS およびアートワークを作成および同期するロジックが再度トリガーされます。<br />  <br /> </li> 
      </ul> </li> 
    </ol> </td> 
  </tr> 
 </tbody> 
</table>
