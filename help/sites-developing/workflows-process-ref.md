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
source-git-commit: c5b816d74c6f02f85476d16868844f39b4c47996
workflow-type: tm+mt
source-wordcount: '1175'
ht-degree: 67%

---

# ワークフロープロセスのリファレンス{#workflow-process-reference}

>[!CAUTION]
>
>AEM 6.4 の拡張サポートは終了し、このドキュメントは更新されなくなりました。 詳細は、 [技術サポート期間](https://helpx.adobe.com/jp/support/programs/eol-matrix.html). サポートされているバージョンを見つける [ここ](https://experienceleague.adobe.com/docs/?lang=ja).

AEMには、ワークフローモデルの作成に使用できる複数のプロセスステップが用意されています。 カスタムプロセスステップは、組み込みステップでカバーされていないタスクにも追加できます ( [ワークフローモデルの作成](/help/sites-developing/workflows-models.md)) をクリックします。

## プロセスの特性 {#process-characteristics}

プロセスステップごとに、次の特性について説明します。

### Java クラスまたは ECMA パス {#java-class-or-ecma-path}

プロセスステップは、Java クラスまたは ECMAScript によって定義されます。

* Java クラスプロセスの場合は、完全修飾クラス名が提供されます。
* ECMAScript 処理の場合、スクリプトへのパスが提供されます。

### ペイロード {#payload}

ペイロードは、ワークフローインスタンスが機能するエンティティです。 ペイロードは、ワークフローインスタンスが開始されるコンテキストによって暗黙的に選択されます。

例えば、ワークフローが AEM ページ「*P*」に適用された場合は、ワークフローが進むたびに「*P*」が手順から手順に引き渡され、各手順で必要に応じて「*P*」に対して何らかの処理がおこなわれます。

最も一般的なケースでは、ペイロードはリポジトリ内の JCR ノード (AEM Page や Asset など ) です。 JCR ノードのペイロードは、JCR パスまたは JCR 識別子（UUID）のいずれかの文字列として渡されます。ペイロードは、JCR プロパティ（JCR パスとして渡されます）、URL、バイナリオブジェクト、汎用 Java オブジェクトのいずれかである場合もあります。ペイロードに対して動作するプロセスの個々の手順は、通常、特定のタイプのペイロードを想定しているか、ペイロードタイプに応じて異なる動作をします。次の各プロセスでは、想定するペイロードタイプ（存在する場合）を記述しています。

### 引数 {#arguments}

一部のワークフロープロセスは、ワークフローステップの設定時に管理者が指定した引数を受け取ります。

引数は、単一の文字列として **プロセスの引数** プロパティを **プロパティ** ワークフローエディターのウィンドウ 次の各プロセスでは、引数文字列の形式を単純な EBNF 文法で記述しています。次のように、引数の文字列は 1 つまたは複数のコンマ区切りのペアで構成されています。各ペアは、2 つのコロンで区切られた名前（文字列）と値で構成されます。

```
    args := name '::' value [',' name '::' value]*
    name := /* A string */
    value := /* A string */
```


### タイムアウト {#timeout}

このタイムアウト期間が過ぎると、ワークフローステップは動作しなくなります。 一部のワークフロープロセスはタイムアウトを考慮しますが、それ以外のプロセスはタイムアウトを適用せず、無視します。

### 権限 {#permissions}

`WorkflowProcess` に渡されたセッションは、ワークフロープロセスサービスのサービスユーザーをベースとしています。このユーザーは、リポジトリのルートで次の権限を持っています。

* `jcr:read`
* `rep:write`
* `jcr:versionManagement`
* `jcr:lockManagement`
* `crx:replicate`

この権限セットが `WorkflowProcess` の実装に十分でない場合は、必要な権限を持つセッションを使用する必要があります。

この方法として、必要最小限の権限のサブセットで必要に応じて作成したサービスユーザーを使用することをお勧めします。

>[!CAUTION]
>
>AEM 6.2 より前のバージョンからアップグレードする場合は、実装を更新する必要が生じる場合があります。
>
>以前のバージョンでは、管理者セッションが `WorkflowProcess` 実装に渡されたので、特定の ACL を定義しなくてもリポジトリへのフルアクセスが可能でした。
>
>権限は、上記のように定義されました ([権限](#permissions)) をクリックします。 は、実装を更新するための推奨される方法です。
>
>コード変更が不可能な場合には、下位互換性を維持する目的で、短期的なソリューションも使用できます。
>
>* Web コンソール（`/system/console/configMgr`/）を使用して、**Adobe Granite ワークフロー設定サービス**&#x200B;を探します
>
>* **ワークフロープロセスのレガシーモード**&#x200B;を有効にします
>
>これにより、管理者セッションを `WorkflowProcess` 実装に渡すという古い動作に戻り、再びリポジトリ全体に無制限にアクセスできるようになります。

## ワークフロー制御プロセス {#workflow-control-processes}

次のプロセスは、コンテンツに対するアクションを実行しません。ワークフロー自体の動作を制御する役割を果たします。

### AbsoluteTimeAutoAdvancer（絶対時刻自動アドバンサー） {#absolutetimeautoadvancer-absolute-time-auto-advancer}

`AbsoluteTimeAutoAdvancer`（絶対時刻自動アドバンサー）プロセスは、**AutoAdvancer** と同じように動作します。ただし、指定された長さの時間が経過した後ではなく、指定された日時にタイムアウトする点が異なります。

* **Java クラス**：`com.adobe.granite.workflow.console.timeout.autoadvance.AbsoluteTimeAutoAdvancer`
* **ペイロード**：なし.
* **引数**：なし.
* **タイムアウト**：設定された日時に達すると、プロセスはタイムアウトします。

### AutoAdvancer（自動アドバンサー） {#autoadvancer-auto-advancer}

`AutoAdvancer` プロセスは、ワークフローを次の手順に自動的に進めます。次に生じる可能性のある手順が複数ある場合（例えば OR 分岐がある場合）、このプロセスは、*デフォルトのルート*&#x200B;が指定されているときはそのルートに沿ってワークフローを進め、指定されていないときはワークフローを進めません。

* **Java クラス**：`com.adobe.granite.workflow.console.timeout.autoadvance.AutoAdvancer`

* **ペイロード**：なし.
* **引数**：なし.
* **タイムアウト**：設定された時間が経過すると、プロセスはタイムアウトします。

### ProcessAssembler（プロセスアセンブラー） {#processassembler-process-assembler}

`ProcessAssembler` プロセスは、ワークフローの単一の手順内で複数のサブプロセスを順番に実行します。`ProcessAssembler` を使用するには、ワークフロー内にこのタイプの手順を 1 つ作成し、実行するサブプロセスの名前と引数を示す引数を設定します。

* **Java クラス**：`com.day.cq.workflow.impl.process.ProcessAssembler`

* **ペイロード**：DAM アセット、AEM ページ、ペイロードなしのいずれか（サブプロセスの要件に応じて異なります）。
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

* **タイムアウト**:尊敬される。

次は例です。

* アセットからメタデータを抽出します。
* 指定した 3 つのサイズの 3 つのサムネールを作成します。
* アセットが元々 GIF でも PNG でもない場合（この場合は JPEG が作成されない）、アセットから JPEG 画像を作成します。
* アセットの最終更新日を設定します。

```shell
com.day.cq.dam.core.process.ExtractMetadataProcess,
    com.day.cq.dam.core.process.CreateThumbnailProcess::[140:100];[48:48];[319:319:false],
    com.day.cq.dam.core.process.CreateWebEnabledImageProcess::dimension:1280:1280;mimetype:image/jpeg,
    com.day.cq.dam.core.process.AssetSetLastModifiedProcess
```

## 基本プロセス {#basic-processes}

次のプロセスは単純なタスクを実行するか、例として機能します。

>[!CAUTION]
>
>`/libs` パス内の設定は&#x200B;***一切***&#x200B;変更しないでください。
>
>`/libs` のコンテンツは、インスタンスを次回アップグレードするとき（場合によってはホットフィックスまたは機能パックを適用したとき）に上書きされるからです。

### delete {#delete}

指定されたパスの項目が削除されます。

* **ECMAScript パス**：`/libs/workflow/scripts/delete.ecma`

* **ペイロード**：JCR パス
* **引数**：なし
* **タイムアウト**：無視されます

### noop {#noop}

これは null プロセスです。 処理は実行しませんが、デバッグメッセージをログに記録します。

* **ECMAScript パス**：`/libs/workflow/scripts/noop.ecma`

* **ペイロード**：なし
* **引数**：なし
* **タイムアウト**：無視されます。

### rule-false {#rule-false}

これは、`check()` メソッドで `false` を返す null プロセスです。

* **ECMAScript パス**：`/libs/workflow/scripts/rule-false.ecma`

* **ペイロード**：なし
* **引数**：なし
* **タイムアウト**：無視されます。

### サンプル {#sample}

これは、サンプルの ECMAScript プロセスです。

* **ECMAScript パス**：`/libs/workflow/scripts/sample.ecma`

* **ペイロード**：なし
* **引数**：なし
* **タイムアウト**：無視されます。

### urlcaller {#urlcaller}

これは、指定された URL を呼び出す単純なワークフロープロセスです。 通常、この URL は、単純なタスクを実行する JSP（または他のサーブレットに相当するもの）への参照です。 このプロセスは、開発およびデモの際にのみ使用し、実稼動環境では使用しないでください。 引数は、URL、ログイン、パスワードを指定します。

* **ECMAScript パス**：`/libs/workflow/scripts/urlcaller.ecma`

* **ペイロード**：なし
* **引数**：

```
        args := url [',' login ',' password]
        url := /* The URL to be called */
        login := /* The login to access the URL */
        password := /* The password to access the URL */
```

例：`http://localhost:4502/my.jsp, mylogin, mypassword`

* **タイムアウト**：無視されます。

### LockProcess {#lockprocess}

ワークフローのペイロードをロックします。

* **Java クラス：** `com.day.cq.workflow.impl.process.LockProcess`

* **ペイロード：** JCR_PATH と JCR_UUID
* **引数：** なし
* **タイムアウト：** 無視

この手順は、次の場合には無効です。

* ペイロードが既にロックされている
* ペイロードノードに jcr:content 子ノードが含まれていない

### UnlockProcess {#unlockprocess}

ワークフローのペイロードをロック解除します。

* **Java クラス：** `com.day.cq.workflow.impl.process.UnlockProcess`

* **ペイロード：** JCR_PATH と JCR_UUID
* **引数：** なし
* **タイムアウト：** 無視

この手順は、次の場合には無効です。

* ペイロードが既にロック解除されている
* ペイロードノードに jcr:content 子ノードが含まれていない

## プロセスのバージョン管理 {#versioning-processes}

次のプロセスは、バージョン関連のタスクを実行します。

### CreateVersionProcess {#createversionprocess}

ワークフローペイロード (AEMページまたは DAM アセット ) の新しいバージョンを作成します。

* **Java クラス**：`com.day.cq.wcm.workflow.process.CreateVersionProcess`

* **ペイロード**：ページまたは DAM アセットを参照する JCR パスまたは UUID。
* **引数**：なし
* **タイムアウト**：適用されます。
