---
title: Tough Day
seo-title: Tough Day
description: Tough Day テストは、すべての操作が同時におこなわれる最悪のシナリオで、約 1,000 人の作成者の日々の負荷をシミュレートします。
seo-description: The Tough Day test simulates the daily load of around 1000 authors in a worst-case scenario with all the operations going on at the same time.
uuid: 7a13efe0-c455-4af0-ad7b-c39cb2479d74
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.4/SITES
topic-tags: testing
content-type: reference
discoiquuid: f48fa5ba-749b-4d3d-a4dd-c802006c8f07
exl-id: 80442184-212a-424d-b320-5b301a54f974
source-git-commit: 51358642a2fa8f59f3f5e3996b0c37269632c4cb
workflow-type: tm+mt
source-wordcount: '1895'
ht-degree: 68%

---

# Tough Day{#tough-day}

## Tough Day 2 とは {#what-is-tough-day}

Tough Day 2 は、AEMインスタンスの制限をストレステストできるアプリケーションです。 デフォルトのテストスイートですぐに使用できる状態にすることも、テストのニーズに合わせて設定することもできます。 ご覧いただけます [この録画](https://experienceleague.adobe.com/docs/experience-manager-gems-events/gems/gems2017/aem-toughday2-stress-testing-benchmarking-tool.html?lang=ja) アプリのプレゼンテーション用。

## Tough Day 2 の実行方法 {#how-to-run-tough-day}

[アドビのリポジトリ](https://repo1.maven.org/maven2/com/adobe/qe/toughday2/)から最新バージョンの Tough Day 2 をダウンロードします。アプリケーションをダウンロードしたら、`host` パラメーターを指定することでアプリケーションをそのまま実行できます。次の例では、AEM インスタンスがローカルで実行されているので、値 `localhost` が使用されています。

```xml
java -jar toughday2.jar --host=localhost
```

パラメーターを追加した後に実行されるデフォルトスイートの名前は `toughday` です。次の使用例が含まれます。

* ページとそのライブコピーを作成する（ロールアウトを含む）
* ホームページを取得
* querybuilder でクエリを実行
* アセット階層の作成
* アセットの削除

このスイートには 15 %の書き込みアクションと 85 %の読み取りアクションが含まれます。

スイートのテストを実行するために、Tough Day 2 によってデフォルトのコンテンツパッケージがインストールされます。この動作は`installsamplecontent`パラメーターを`false`に設定することで回避できます。ただし、実行するテストのデフォルトパスを変更することも必要になります。パラメーターを指定せずに jar を実行した場合は、Tough Day 2 で[ヘルプ情報](/help/sites-developing/tough-day.md#getting-help)が表示されます。

原則として、アプリケーションを使用するには、次のパターンに従います。

```xml
java -jar toughday2.jar [--help | --help_full | --help_tests | --help_publish]  [<global arguments> | <actions> | --runmode | --publishmode]
```

>[!NOTE]
>
>Tough Day 2 にはクリーンアップ手順がありません。 その結果、メインの実稼動インスタンスではなく、クローンのステージングインスタンスで Tough Day 2 を実行することをお勧めします。 テストの後に、ステージングインスタンスを削除する必要があります。

### ヘルプの表示 {#getting-help}

Tough Day 2 には、コマンドラインからアクセスできる様々なヘルプオプションが用意されています。 次に例を示します。

```xml
java -jar toughday2.jar --help_full
```

次の表に、関連するヘルプパラメーターを示します。

<table> 
 <tbody> 
  <tr> 
   <td><strong>パラメーター</strong></td> 
   <td><strong>説明</strong></td> 
   <td><strong>例</strong></td> 
  </tr> 
  <tr> 
   <td>--help</td> 
   <td>グローバルな情報を出力します。例えば、利用可能なアクション、事前定義済みスイート、実行モード、グローバルパラメーターなどです。</td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>--help_publish</td> 
   <td>利用可能なすべてのパブリッシャーを出力します。</td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>--help_tests</td> 
   <td>テストクラスとその説明を出力します。</td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>--help_full</td> 
   <td>上記のすべてを出力し、さらに、テスト、パブリッシャー、スイートコンポーネントを出力します。</td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td> --help --runmode/publishmode type=&lt;Mode&gt;</td> 
   <td>指定した実行またはパブリッシュモードに関する情報を一覧表示します。</td> 
   <td><p>java -jar toughday2.jar --help --runmode type=constantload</p> <p>java -jar toughday2.jar --help --publishmode type=intervals</p> </td> 
  </tr> 
  <tr> 
   <td>--help --suite=&lt;SuiteName&gt;</td> 
   <td>特定のスイートのすべてのテストと、それぞれの設定可能なプロパティを一覧表示します。</td> 
   <td><br /> java -jar toughday2.jar --help --suite=get_tests</td> 
  </tr> 
  <tr> 
   <td> --help --tag=&lt;Tag&gt;</td> 
   <td><br /> 指定したタグを持つすべての項目を一覧表示します。</td> 
   <td>java -jar toughday2.jar --help --tag=publish</td> 
  </tr> 
  <tr> 
   <td>--help &lt;TestClass/PublisherClass&gt;</td> 
   <td><br /> 特定のテストまたはパブリッシャーの設定可能なプロパティをすべて一覧表示します。</td> 
   <td><p>java -jar toughday2.jar --help UploadPDFTest</p> <p>java -jar toughday2.jar --help CSVPublisher</p> </td> 
  </tr> 
 </tbody> 
</table>

### グローバルパラメーター {#global-parameters}

Tough Day 2 では、テストの環境を設定または変更するグローバルパラメーターを提供します。 これには、ターゲットとなるホスト、ポート番号、使用するプロトコル、インスタンスのユーザーとパスワードなどが含まれます。 次に例を示します。

```xml
java -jar toughday2.jar --host=host --protocol=https --port=4502 --duration=30m --dryrun=true 
```

次のリストに、関連するパラメーターが表示されます。

| **パラメーター** | **説明** | **デフォルト値** | **可能な値** |
|---|---|---|---|
| `--installsamplecontent=<Val>` | デフォルトの Tough Day 2 コンテンツパッケージをインストールまたはスキップします。 | true | true または false |
| `--protocol=<Val>` | ホストに使用するプロトコル。 | http | http または https |
| `--host=<Val>` | ターゲットにするホスト名または IP。 |  |  |
| `--port=<Val>` | ホストのポート。 | 4502 |  |
| `--user=<Val>` | インスタンスのユーザー名。 | admin |  |
| `--password=<Val>` | 指定されたユーザーのパスワード。 | admin |  |
| `--duration=<Val>` | テストの期間。（**秒**）単位、（**分**）単位、（**時**）単位、（**日**）単位で表現できます。 | 1d |  |
| `--timeout=<Val>` | テストが中断され、失敗としてマークされるまでのテストの実行時間。秒単位で表現できます。 | 180 |  |
| `--suite=<Val>` | 値は、事前定義済みのテストスイートの 1 つまたはリスト（コンマ区切り）にすることができます。 | toughday |  |
| `--configfile=<Val>` | ターゲットの yaml 設定ファイル。 |  |  |
| `--contextpath=<Val>` | インスタンスのコンテキストパス。 |  |  |
| `--loglevel=<Val>` | Tough Day 2 エンジンのログレベル。 | INFO | ALL、DEBUG、INFO、WARN、ERROR、FATAL、OFF |
| `--dryrun=<Val>` | true の場合は、結果の設定が出力され、テストは実行されません。 | false | true または false |

## カスタマイズ {#customizing}

カスタマイズは、次の 2 つの方法で実行できます。コマンドラインパラメータまたは yaml 設定ファイル。 **設定ファイルは、通常、大規模なカスタムスイートで使用され、Tough Day 2 のデフォルトパラメーターを上書きします。 コマンドラインパラメータは、設定ファイルとデフォルトパラメータの両方を上書きします。**

テスト設定を保存するには、yaml 形式でコピーする方法しかありません。詳しくは、この [toughday.yaml](https://repo.adobe.com/nexus/service/local/repositories/releases/content/com/adobe/qe/toughday2/0.2.1/toughday2-0.2.1.yaml) 設定と、以降のセクションの yaml 設定の例を参照してください。

### 新規テストの追加 {#adding-a-new-test}

デフォルトの `toughday` スイートを使用しない場合は、`add` パラメーターを使用して任意のテストを追加できます。コマンドラインパラメーターまたは yaml 設定ファイルを使用して `CreateAssetTreeTest` テストを追加する方法を以下の例に示します。

コマンドラインパラメータを使用する：

```xml
java -jar toughday2.jar --host=localhost --add CreateAssetTreeTest
```

yaml 設定ファイルを使用すると、次のことができます。

```xml
globals:
  host : localhost
tests:
  - add : CreateAssetTreeTest
```

### 同じテストの複数のインスタンスの追加  {#adding-multiple-instances-of-the-same-test}

同じテストの複数のインスタンスを追加して実行することもできますが、そのためにはそれぞれのインスタンスに一意の名前を付ける必要があります。コマンドラインパラメーターまたは yaml 設定ファイルを使用して同じテストの 2 つのインスタンスを追加する方法を以下の例に示します。

コマンドラインパラメータを使用する：

```xml
java -jar toughday2.jar --host=localhost --add CreateAssetTreeTest name=FirstAssetTree --add CreateAssetTreeTest name=SecondAssetTree
```

yaml 設定ファイルを使用すると、次のことができます。

```xml
globals:
  host : localhost
tests:
  - add : CreateAssetTreeTest
    properties:
      name : FirstAssetTree
  - add : CreateAssetTreeTest
    properties:
      name : SecondAssetTree
```

### テストプロパティの変更 {#changing-the-test-properties}

1 つ以上のテストプロパティを変更する必要がある場合は、そのプロパティをコマンドラインまたは yaml 設定ファイルに追加できます。 使用可能なすべてのテストプロパティを表示するには、コマンドラインに `--help <TestClass/PublisherClass>` パラメーターを追加してください。次に例を示します。

```xml
java -jar toughday2.jar --help CreatePageTreeTest
```

yaml 設定ファイルによって Tough Day 2 のデフォルトのパラメーターが上書きされるので、コマンドラインパラメーターは設定ファイルとデフォルトの両方よりも優先されることに注意してください。

コマンドラインパラメーターまたは yaml 設定ファイルを使用して `CreatePageTreeTest` テストの `template` プロパティを変更する方法を以下の例に示します。

コマンドラインパラメータを使用する：

```xml
java -jar toughday2.jar --host=localhost --add CreatePageTreeTest template=/conf/toughday-templates/settings/wcm/templates/toughday-template
```

yaml 設定ファイルを使用すると、次のことができます。

```xml
globals:
  host : localhost
tests:
  - add : CreatePageTreeTest
    properties:
      template : /conf/toughday-templates/settings/wcm/templates/toughday-template
```

### 定義済みのテストスイートの操作 {#working-with-predefined-test-suites}

事前定義済みのスイートにテストを追加する方法、事前定義済みのスイートの既存のテストを再設定および除外する方法を以下の例に示します。

事前定義済みのスイートに新しいテストを追加するには、`add` パラメーターを使用して、ターゲットとなる事前定義済みのスイートを指定します。

コマンドラインパラメータを使用する：

```xml
java -jar toughday2.jar --host=localhost --suite=toughday --add CreatePageTreeTest
```

yaml 設定ファイルを使用すると、次のことができます。

```xml
globals:
  host : localhost
  suite : toughday
tests:
  - add : CreatePageTreeTest
```

また、特定のスイート内の既存のテストは、`config`* *パラメーターを使用して再設定することもできます。スイート名とテストの実際の名前（テストクラス名ではありません）も指定する必要があることに注意してください。テスト名は、テストクラスの `name` プロパティで確認できます。テストプロパティの確認方法について詳しくは、[テストプロパティの変更](/help/sites-developing/tough-day.md#changing-the-test-properties)を参照してください。

以下の例では0、`CreatePageTreeTest` のデフォルトのアセットタイトル（名前は `UploadAsset`）を「NewAsset」に変更しています。

コマンドラインパラメータを使用する：

```xml
java -jar toughday2.jar --host=localhost --suite=toughday --config UploadAsset title=NewAsset
```

yaml 設定ファイルを使用すると、次のことができます。

```xml
globals:
  host : localhost
  suite : toughday
tests:
  - config : UploadAsset
    properties :
      title : NewAsset 
```

さらに、`exclude` パラメーターを使用して、事前定義済みのスイートからテストを削除したり、デフォルトの設定から公開者を削除したりできます。スイート名とテストの実際の名前（テスト C `lass` 名ではありません）も指定する必要があることに注意してください。テスト名は、テストクラスの `name` プロパティで確認できます。以下の例では、（`UploadAsset` という名前の）`CreatePageTreeTest` テストを toughday スイートから削除しています。

コマンドラインパラメータを使用する：

```xml
java -jar toughday2.jar --host=localhost --suite=toughday --exclude UploadAsset
```

yaml 設定ファイルを使用すると、次のことができます。

```xml
globals:
  host : localhost
  suite : toughday
tests:
  - exclude : UploadAsset 
```

### 実行モード {#run-modes}

Tough Day 2 は、**標準**&#x200B;モードと&#x200B;**定負荷**&#x200B;モードのいずれかで実行できます。

**標準**&#x200B;実行モードには、次の 2 つのパラメーターがあります。

* `concurrency` - テストの実行のために Tough Day 2 によって作成されるスレッドの数を表します。これらのスレッドでは、実行時間が終了するか、実行するテストがなくなるまでテストが実行されます。

* `waittime` - 同じスレッド上の連続した 2 つのテスト実行の間の待機時間。値はミリ秒単位で表す必要があります。

次の例は、コマンドラインを使用してパラメータを追加する方法を示しています。

```xml
java -jar toughday2.jar --host=localhost --add CreateAssetTreeTest --runmode=normal concurrency=20
```

または、yaml 設定ファイルを使用します。

```xml
runmode:
  type : normal
  waittime : 300
  concurrency : 200
```

**定負荷**&#x200B;実行モードは、通常実行モードとは異なり、一定数のスレッドではなく一定数の開始されたテスト実行を生成します。同じ名前の実行モードパラメーターを使用して負荷を設定できます。

### テストの選択 {#test-selection}

テストの選択プロセスはどちらの実行モードでも同じで、次のように進みます。すべてのテストには `weight` プロパティがあり、これによって、スレッドでの実行の可能性が決定します。例えば、テストが 2 つあり、一方の重みを 5、もう一方の重みを 10 とした場合、後者が実行される可能性は前者の 2 倍になります。

さらに、テストには `count` プロパティを指定できます。これにより、実行回数が指定の数に制限されます。この数を超えると、テストはそれ以上実行されません。 既に実行中のすべてのテストインスタンスは、設定どおりに実行を終了します。 次の例は、これらのパラメーターをコマンドラインまたは yaml 設定ファイルを使用して追加する方法を示しています。

```xml
java -jar toughday2.jar --host=localhost --add CreateAssetTreeTest weight=5 --add CreatePageTreeTest weight=10 count=100 --runmode=normal concurrency=20 
```

または

```xml
- add : CreateAssetTreeTest
    properties :
      name : UploadAsset
      weight : 5
      base : 3
      foldertitle : IAmAFolder
      assettitle : IAmAnAsset
      count : 100
```

>[!NOTE]
>
>並列実行が原因で、実際のテスト実行回数は `count` パラメーターで設定された数と正確に一致しません。偏差が（`concurrency parameter` パラメーターによって制御される）実行スレッドの数に比例することを想定してください。

### ドライラン {#dry-run}

ドライランは、指定されたすべての入力（コマンドラインパラメータまたは設定ファイル）を解析し、デフォルトと結合して結果を出力します。 どのテストも実行されません。

```xml
java -jar toughday2.jar --host=localhost --suite=toughday --add CreatePageTreeTest --dryrun=true
```

## 出力 {#output}

Tough Day 2 は、テスト指標とログの両方を出力します。 詳しくは、次の節を参照してください。

### 指標のテスト {#test-metrics}

Tough Day 2 は現在、評価可能な 9 つのテスト指標をレポートします。 指標と **&amp;ast;** シンボルは、正常に実行された後にのみ報告されます。

| **名前** | **説明** |
|---|---|
| Timestamp | 最後に完了したテスト実行のタイムスタンプ。 |
| 渡された | 成功した実行の数。 |
| 失敗 | 失敗した実行の数。 |
| 最小 (&amp;A); | テスト実行の最短期間。 |
| 最大 (&amp;A); | テスト実行の最長期間。 |
| 中央値 (&amp;A); | すべてのテスト実行の算出された中央値時間。 |
| 平均 (&amp;A); | すべてのテスト実行の算出された平均時間。 |
| StdDev&amp;ast; | 標準偏差。 |
| 90p&amp;ast; | 90 パーセンタイル。 |
| 99p&amp;ast; | 99 パーセンタイル。 |
| 99.9p&amp;ast; | 99.9 パーセンタイル。 |
| 実際のスループット (&amp;A); | 実行数を経過した実行時間で割った値。 |

これらの指標は、（テストの追加と同様に）`add` パラメーターを使用して追加できる公開者を利用して記述されています。現在、次の 2 つのオプションがあります。

* **CSVPublisher** - CSV ファイルを出力します。
* **ConsolePublisher** - 出力はコンソールに表示されます。

デフォルトでは、両方の公開者が有効になっています。

さらに、指標の報告には次の 2 つのモードがあります。

* **simple** パブリッシュモード - 実行の開始から公開時点までの結果が報告されます。
* **intervals** パブリッシュモード - 特定の期間内の結果が報告されます。期間は、**interval** パブリッシュモード／パラメーターを使用して設定することができます。

次の例は、コマンドラインまたは yaml 設定ファイルを使用して `intervals` パラメーターを設定する方法を示しています。

コマンドラインパラメータを使用する：

```xml
java -jar toughday2.jar --host=localhost --add CreatePageTreeTest --publishmode type=intervals interval=10s 
```

yaml 設定ファイルを使用すると、次のことができます。

```xml
publishmode:
     type : intervals 
     interval : 10s 
     tests: 
        -add : CreatePageTreeTest
```

### ログ {#logging}

Tough Day 2 では、Tough Day 2 を実行したディレクトリにログフォルダーが作成されます。このフォルダーには、次の 2 種類のログが含まれます。

* **toughday.log**:には、アプリケーションの状態、デバッグ情報およびグローバルメッセージに関連するメッセージが含まれます。
* **強い日&lt;testname>.log**:指定したテストに関連するメッセージ。

ログは上書きされません。その後の実行では、既存のログにメッセージが追加されます。ログには複数のレベルがあります。詳しくは、` [loglevel parameter](/help/sites-developing/tough-day.md#global-parameters)`を参照してください。
