---
title: ワークフロープロセスのリファレンス
seo-title: Workflow Process Reference
description: ワークフロープロセスのリファレンス
seo-description: null
uuid: de367aa8-4580-4810-b665-2a7b521e36ca
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.4/SITES
topic-tags: extending-aem
content-type: reference
discoiquuid: dbdf981f-791b-4ff7-8ca8-039d0bdc9c92
exl-id: c828302c-54ad-4171-89d1-f77f4d836277
source-git-commit: bd94d3949f0117aa3e1c9f0e84f7293a5d6b03b4
workflow-type: tm+mt
source-wordcount: '1139'
ht-degree: 60%

---

# ワークフロープロセスのリファレンス{#workflow-process-reference}

AEM には、ワークフローモデルの作成に使用できるプロセスステップがいくつか用意されています。組み込みステップに含まれていないタスクについては、カスタムのプロセスステップを追加することができます（[ワークフローモデルの作成](/help/sites-developing/workflows-models.md)を参照）。

## プロセスの特徴 {#process-characteristics}

プロセスステップごとに特徴を説明します。

### Java クラスか ECMA パスか {#java-class-or-ecma-path}

プロセスステップは、Java クラスまたは ECMAScript によって定義されます。

* Java クラスのプロセスの場合は、完全修飾クラス名を指定します。
* ECMAScript プロセスの場合は、スクリプトへのパスを指定します。

### ペイロード {#payload}

ペイロードは、ワークフローインスタンスの処理対象となるエンティティです。ペイロードは、ワークフローインスタンスが開始されるコンテキストによって暗黙的に選択されます。

例えば、ワークフローが AEM ページ「P **」に適用された場合は、ワークフローが進むたびに「P **」がステップからステップに引き渡され、各ステップで必要に応じて「P **」に対して何らかの処理がおこなわれます。

最も多いのは、ペイロードがリポジトリ内の JCR ノード（例えば AEM ページまたはアセット）である場合です。JCR ノードのペイロードは、JCR パスまたは JCR 識別子 (UUID) のいずれかの文字列として渡されます。 場合によっては、ペイロードは、JCR プロパティ（JCR パスとして渡される）、URL、バイナリオブジェクト、汎用 Java オブジェクトのいずれかです。 ペイロードに対して動作する個々のプロセスステップは、通常、特定のタイプのペイロードを想定するか、ペイロードタイプに応じて異なる動作をします。 以下に説明する各プロセスに対して、期待されるペイロードタイプ（存在する場合）が説明されます。

### 引数 {#arguments}

一部のワークフロープロセスは引数を受け取ります。引数は、ワークフローステップを設定するときに管理者が指定します。

引数は、ワークフローエディターの&#x200B;**プロパティ**&#x200B;ウィンドウの「**プロセスの引数**」プロパティに単一文字列として入力します。以下で説明する各プロセスに対して、引数文字列の形式は単純な EBNF 文法で記述されます。 例えば、次の例では、引数文字列が 1 つ以上のコンマ区切りのペアで構成され、各ペアは名前（文字列）と値で構成され、ダブルコロンで区切られています。

```
    args := name '::' value [',' name '::' value]*
    name := /* A string */
    value := /* A string */
```


### タイムアウト {#timeout}

このタイムアウト期間が経過すると、ワークフローステップは動作しなくなります。タイムアウトを適用するワークフロープロセスもありますが、タイムアウトを適用せず、無視するワークフロープロセスもあります。

### 権限 {#permissions}

セッションが `WorkflowProcess` は、リポジトリのルートに次の権限を持つ、ワークフロープロセスサービスのサービスユーザーに基づいています。

* `jcr:read`
* `rep:write`
* `jcr:versionManagement`
* `jcr:lockManagement`
* `crx:replicate`

この一連の権限では `WorkflowProcess` を実装する場合は、必要な権限を持つセッションを使用する必要があります。

これをおこなうには、必要な（ただし最小限の）権限のサブセットを持つよう作成されたサービスユーザーを使用する方法が推奨されます。

>[!CAUTION]
>
>AEM 6.2 より前のバージョンからアップグレードする場合は、実装の更新が必要になる場合があります。
>
>以前のバージョンでは、管理者セッションが `WorkflowProcess` 実装に渡されたので、特定の ACL を定義しなくてもリポジトリへのフルアクセスが可能でした。
>
>現在、権限は上述のように定義されています（[権限](#permissions)を参照）。実装を更新するために推奨される方法も同様です。
>
>コードの変更が実行できない場合は、短期的な解決方法を後方互換性の確保にも使用できます。
>
>* Web コンソール ( `/system/console/configMgr` を見つけます。 **AdobeGranite Workflow Configuration Service**
>
>* **Workflow Process Legacy Mode** を有効にします。

>
>これにより、管理者セッションを `WorkflowProcess` 実装に渡すという古い動作に戻り、再びリポジトリ全体に無制限にアクセスできるようになります。

## ワークフロー制御プロセス {#workflow-control-processes}

次のプロセスは、コンテンツに対するアクションを実行しません。 ワークフロー自体の動作を制御する役割を果たします。

### AbsoluteTimeAutoAdvancer（絶対時刻自動アドバンサー） {#absolutetimeautoadvancer-absolute-time-auto-advancer}

`AbsoluteTimeAutoAdvancer`（絶対時刻自動アドバンサー）プロセスは、**AutoAdvancer** とまったく同じように動作します。例外は、指定された長さの時間が経過した後ではなく、指定された日時にタイムアウトする点です。

* **Java クラス**: `com.adobe.granite.workflow.console.timeout.autoadvance.AbsoluteTimeAutoAdvancer`
* **ペイロード**：なし
* **引数**：なし
* **タイムアウト**：設定された日時に達すると、プロセスはタイムアウトします。

### AutoAdvancer（自動アドバンサー） {#autoadvancer-auto-advancer}

`AutoAdvancer` プロセスは、ワークフローを次のステップに自動的に進めます。次に生じる可能性のあるステップが複数ある場合（例えば OR 分岐がある場合）、このプロセスは、デフォルトのルートが指定されているときはそのルートに沿ってワークフローを進め、指定されていないときはワークフローを進めません&#x200B;**。

* **Java クラス**: `com.adobe.granite.workflow.console.timeout.autoadvance.AutoAdvancer`

* **ペイロード**：なし
* **引数**：なし
* **タイムアウト**：設定された時間が経過すると、プロセスはタイムアウトします。

### ProcessAssembler（プロセスアセンブラー） {#processassembler-process-assembler}

`ProcessAssembler` プロセスは、単一のワークフローステップ内で複数のサブプロセスを順番に実行します。`ProcessAssembler` を使用するには、ワークフロー内にこのタイプのステップを 1 つ作成し、実行するサブプロセスの名前と引数を示す引数を設定します。

* **Java クラス**: `com.day.cq.workflow.impl.process.ProcessAssembler`

* **ペイロード**：DAM アセット、AEM ページ、ペイロードなしのいずれか（サブプロセスの要件によって異なります）。
* **引数**：

```
        args := arg [',' arg]
        arg := processname ['::' processargs]
        processname := /* A fully qualified Java Class or absolute 
        repository path to an ECMAScript */
        processargs := processarg [';' processarg]*
        processarg := '[' nobracketprocessarg ']' | nobracketprocessarg
        nobracketprocessarg := listitem [':' listitem]*
        listitem := /* A string */
```

* **タイムアウト**：適用されます。

次に例を示します。

* アセットからメタデータを抽出します。
* 指定した 3 つのサイズの 3 つのサムネールを作成します。
* JPEGが元々GIFでも PNG でもない場合 ( この場合はJPEGが作成されない )、アセットからアセット画像を作成します。
* アセットの最終変更日を設定します。

```shell
com.day.cq.dam.core.process.ExtractMetadataProcess,
    com.day.cq.dam.core.process.CreateThumbnailProcess::[140:100];[48:48];[319:319:false],
    com.day.cq.dam.core.process.CreateWebEnabledImageProcess::dimension:1280:1280;mimetype:image/jpeg,
    com.day.cq.dam.core.process.AssetSetLastModifiedProcess
```

## 基本プロセス {#basic-processes}

以下のプロセスは単純なタスクを実行するか、例として機能します。

>[!CAUTION]
>
>`/libs` パス内の設定は&#x200B;***一切***&#x200B;変更しないでください。
>
>これは、 `/libs` は、インスタンスを次回アップグレードするとき（ホットフィックスまたは機能パックを適用すると上書きされる場合があります）に上書きされます。

### 次を削除します。 {#delete}

指定されたパスにある項目が削除されます。

* **ECMAScript パス**: `/libs/workflow/scripts/delete.ecma`

* **ペイロード**:JCR パス
* **引数**:なし
* **タイムアウト**:無視

### noop {#noop}

これはヌルプロセスです。処理は実行しませんが、デバッグメッセージをログに記録します。

* **ECMAScript パス**: `/libs/workflow/scripts/noop.ecma`

* **ペイロード**:なし
* **引数**:なし
* **タイムアウト**:無視

### rule-false {#rule-false}

これは、 `false` の `check()` メソッド。

* **ECMAScript パス**: `/libs/workflow/scripts/rule-false.ecma`

* **ペイロード**:なし
* **引数**:なし
* **タイムアウト**:無視

### sample {#sample}

これは、ECMAScript プロセスのサンプルです。

* **ECMAScript パス**: `/libs/workflow/scripts/sample.ecma`

* **ペイロード**:なし
* **引数**:なし
* **タイムアウト**:無視

### urlcaller {#urlcaller}

これは、指定された URL を呼び出す単純なワークフロープロセスです。 通常、この URL は、単純なタスクを実行する JSP（または同等の他のサーブレット）への参照です。 このプロセスは開発およびデモンストレーションのときにのみ使用し、実稼動環境では使用しないようにする必要があります。引数は、URL、ログイン、パスワードを指定します。

* **ECMAScript パス**: `/libs/workflow/scripts/urlcaller.ecma`

* **ペイロード**:なし
* **引数**：

```
        args := url [',' login ',' password]
        url := /* The URL to be called */
        login := /* The login to access the URL */
        password := /* The password to access the URL */
```

例：`http://localhost:4502/my.jsp, mylogin, mypassword`

* **タイムアウト**:無視

### LockProcess {#lockprocess}

ワークフローのペイロードをロックします。

* **Java クラス:** `com.day.cq.workflow.impl.process.LockProcess`

* **ペイロード：** JCR_PATH と JCR_UUID
* **引数：**&#x200B;なし
* **タイムアウト：**&#x200B;無視されます。

次の状況下では、このステップは無効です。

* ペイロードは既にロックされています
* payload ノードに jcr:content 子ノードが含まれていません

### UnlockProcess {#unlockprocess}

ワークフローのペイロードをロック解除します。

* **Java クラス:** `com.day.cq.workflow.impl.process.UnlockProcess`

* **ペイロード：** JCR_PATH と JCR_UUID
* **引数：**&#x200B;なし
* **タイムアウト：**&#x200B;無視されます。

次の状況下では、このステップは無効です。

* ペイロードは既にロック解除されています
* payload ノードに jcr:content 子ノードが含まれていません

## バージョン管理プロセス {#versioning-processes}

以下のプロセスは、バージョン関連のタスクを実行します。

### CreateVersionProcess {#createversionprocess}

ワークフローペイロード（AEM ページまたは DAM アセット）の新しいバージョンを作成します。

* **Java クラス**: `com.day.cq.wcm.workflow.process.CreateVersionProcess`

* **ペイロード**:ページまたは DAM アセットを参照する JCR パスまたは UUID
* **引数**:なし
* **タイムアウト**:尊重
