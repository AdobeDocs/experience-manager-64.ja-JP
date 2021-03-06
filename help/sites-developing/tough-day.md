---
title: Tough Day
seo-title: Tough Day
description: Tough Day テストでは、約 1,000 人の作成者がいる環境で、すべての操作が同時進行しているという最悪の状況を想定して、1 日の負荷をシミュレートします。。
seo-description: The Tough Day test simulates the daily load of around 1000 authors in a worst-case scenario with all the operations going on at the same time.
uuid: 7a13efe0-c455-4af0-ad7b-c39cb2479d74
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.4/SITES
topic-tags: testing
content-type: reference
discoiquuid: f48fa5ba-749b-4d3d-a4dd-c802006c8f07
exl-id: 80442184-212a-424d-b320-5b301a54f974
source-git-commit: 119023a24d5f21fd003439992fe5a520f48b6861
workflow-type: tm+mt
source-wordcount: '1894'
ht-degree: 50%

---

# Tough Day{#tough-day}

## Tough Day 2 について {#what-is-tough-day}

Tough Day 2 は、AEMインスタンスの制限をストレステストできるアプリケーションです。 Tough Day 2 は、デフォルトのテストスイートを使用してそのまま実行することも、テストのニーズに合わせて設定することも可能です。このアプリケーションのプレゼンテーションについては、[こちらの録画](https://docs.adobe.com/ddc/en/gems/Toughday2---A-new-and-improved-stress-testing-and-benchmarking-tool.html)を参照してください。

## Tough Day 2 の実行方法 {#how-to-run-tough-day}

[アドビのリポジトリ](https://repo1.maven.org/maven2/com/adobe/qe/toughday2/)から最新バージョンの Tough Day 2 をダウンロードします。アプリケーションをダウンロードした後、 `host` パラメーター。 次の例では、AEMインスタンスがローカルで実行され、 `localhost` 値は次の場合に使用されます。

```xml
java -jar toughday2.jar --host=localhost
```

パラメーターを追加した後に実行されるデフォルトスイートの名前は `toughday` です。このスイートには次のユースケースが含まれています。

* ページとそのページのライブコピーを作成する（ロールアウトを含む）
* ホームページを取得する
* querybuilder でクエリを実行する
* アセット階層を作成する
* アセットの削除

このスイートには、15 ％の書き込みアクションと 85 ％の読み取りアクションが含まれています。

スイートのテストを実行するために、Tough Day 2 によってデフォルトのコンテンツパッケージがインストールされます。これは、 `installsamplecontent` パラメータ `false`ただし、実行するテストのデフォルトのパスも変更する必要があります。 jar がパラメーターなしで実行されている場合、Tough Day 2 では [ヘルプ情報](/help/sites-developing/tough-day.md#getting-help).

原則として、アプリケーションを使用するには、次のパターンに従います。

```xml
java -jar toughday2.jar [--help | --help_full | --help_tests | --help_publish]  [<global arguments> | <actions> | --runmode | --publishmode]
```

>[!NOTE]
>
>Tough Day 2 にはクリーンアップステップが用意されていません。したがって、メインの実稼動インスタンスではなく、クローンされたステージングインスタンスで Tough Day 2 を実行することをお勧めします。ステージングインスタンスは、テスト後に削除する必要があります。

### ヘルプの入手 {#getting-help}

Tough Day 2 には、コマンドラインからアクセスできる幅広いヘルプオプションが用意されています。次に例を示します。

```xml
java -jar toughday2.jar --help_full
```

以下の表に、関連するヘルプパラメーターを示します。

<table> 
 <tbody> 
  <tr> 
   <td><strong>パラメーター</strong></td> 
   <td><strong>説明</strong></td> 
   <td><strong>例</strong></td> 
  </tr> 
  <tr> 
   <td>--help</td> 
   <td>グローバル情報を出力します。次に例を示します。使用可能なアクション、定義済みスイート、実行モードおよびグローバルパラメーター。</td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>—help_publish</td> 
   <td>利用可能なすべての発行元を印刷します。</td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>—help_tests</td> 
   <td>テストクラスとその説明を出力します。</td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>—help_full</td> 
   <td>上記のすべてを印刷し、さらに、テスト、パブリッシャー、スイートコンポーネントを印刷します。</td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td> —help —runmode/publishmode type=&lt;mode&gt;</td> 
   <td>指定した実行または公開モードに関する情報を表示します。</td> 
   <td><p>java -jar toughday2.jar —help —runmode type=constantload</p> <p>java -jar toughday2.jar —help —publishmode type=intervals</p> </td> 
  </tr> 
  <tr> 
   <td>—help —suite=&lt;suitename&gt;</td> 
   <td>特定のスイートのすべてのテストと、それぞれの設定可能なプロパティをリストします。</td> 
   <td><br /> java -jar toughday2.jar —help —suite=get_tests</td> 
  </tr> 
  <tr> 
   <td> —help —tag=&lt;tag&gt;</td> 
   <td><br /> 指定したタグを持つすべての項目をリストします。</td> 
   <td>java -jar toughday2.jar —help —tag=publish</td> 
  </tr> 
  <tr> 
   <td>—help &lt;testclass publisherclass=""&gt;</td> 
   <td><br /> 特定のテストまたはパブリッシャーの設定可能なプロパティをすべてリストします。</td> 
   <td><p>java -jar toughday2.jar —help UploadPDFTest</p> <p>java -jar toughday2.jar —help CSVPublisher</p> </td> 
  </tr> 
 </tbody> 
</table>

### グローバルパラメーター {#global-parameters}

Tough Day 2 には、テストの環境を設定または変更するグローバルパラメーターが用意されています。これには、ターゲットのホスト、ポート番号、使用されるプロトコル、インスタンスのユーザーとパスワードなどが含まれます。次に例を示します。

```xml
java -jar toughday2.jar --host=host --protocol=https --port=4502 --duration=30m --dryrun=true 
```

以下のリストには、関連のあるパラメーターがあります。

| **パラメーター** | **説明** | **デフォルト値** | **可能な値** |
|---|---|---|---|
| `--installsamplecontent=<Val>` | デフォルトの Tough Day 2 コンテンツパッケージをインストールまたはスキップします。 | true | true または false |
| `--protocol=<Val>` | ホストに使用するプロトコル。 | http | http または https |
| `--host=<Val>` | ターゲットにするホスト名または IP。 |  |  |
| `--port=<Val>` | ホストのポート。 | 4502 |  |
| `--user=<Val>` | インスタンスのユーザー名。 | admin |  |
| `--password=<Val>` | 指定したユーザーのパスワード。 | admin |  |
| `--duration=<Val>` | テストの期間。 は (**s**)econds, (**m**)inutes, (**h**)ours および (**d**)ays. | 1d |  |
| `--timeout=<Val>` | テストが中断され、失敗とマークされるまでに実行される期間。 秒単位で表現できます。 | 180 |  |
| `--suite=<Val>` | 値は、事前定義済みのテストスイートの 1 つまたはリスト（コンマ区切り）にすることができます。 | 厳しい日 |  |
| `--configfile=<Val>` | ターゲットの yaml 設定ファイル。 |  |  |
| `--contextpath=<Val>` | インスタンスのコンテキストパス。 |  |  |
| `--loglevel=<Val>` | Tough Day 2 エンジンのログレベルです。 | INFO | ALL, DEBUG, INFO, WARN, ERROR, FATAL, OFF |
| `--dryrun=<Val>` | true の場合は、結果の設定が出力され、テストは実行されません。 | false | true または false |

## カスタマイズ {#customizing}

カスタマイズの方法には、コマンドラインパラメーターを使用する方法と yaml 設定ファイルを使用する方法の 2 つがあります。**通常、設定ファイルは大規模なカスタムスイートに使用します。設定ファイルは、Tough Day 2 のデフォルトパラメーターよりも優先されます。コマンドラインパラメーターは、設定ファイルとデフォルトパラメーターの両方よりも優先されます。**

テスト設定を保存するには、yaml 形式でコピーする方法しかありません。詳しくは、 [toughday.yaml](https://repo.adobe.com/nexus/service/local/repositories/releases/content/com/adobe/qe/toughday2/0.2.1/toughday2-0.2.1.yaml) 設定および yaml の設定例については、以下の節を参照してください。

### 新規テストの追加 {#adding-a-new-test}

デフォルトの `toughday` スイートを使用しない場合は、`add` パラメーターを使用して任意のテストを追加できます。コマンドラインパラメーターまたは yaml 設定ファイルを使用して `CreateAssetTreeTest` テストを追加する方法を以下の例に示します。

コマンドラインパラメーターを使用する場合：

```xml
java -jar toughday2.jar --host=localhost --add CreateAssetTreeTest
```

yaml 設定ファイルを使用する場合：

```xml
globals:
  host : localhost
tests:
  - add : CreateAssetTreeTest
```

### 同じテストの複数のインスタンスの追加  {#adding-multiple-instances-of-the-same-test}

同じテストの複数のインスタンスを追加して実行することもできますが、そのためにはそれぞれのインスタンスに一意の名前を付ける必要があります。以下の例は、コマンドラインパラメーターまたは yaml 設定ファイルを使用して、同じテストの 2 つのインスタンスを追加する方法を示しています。

コマンドラインパラメーターを使用する場合：

```xml
java -jar toughday2.jar --host=localhost --add CreateAssetTreeTest name=FirstAssetTree --add CreateAssetTreeTest name=SecondAssetTree
```

yaml 設定ファイルを使用する場合：

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

1 つ以上のテストプロパティを変更する必要がある場合は、そのプロパティをコマンドラインまたは yaml 設定ファイルに追加できます。使用可能なすべてのテストプロパティを表示するには、 `--help <TestClass/PublisherClass>` コマンドラインのパラメータ。次に例を示します。

```xml
java -jar toughday2.jar --help CreatePageTreeTest
```

yaml 設定ファイルによって Tough Day 2 のデフォルトのパラメーターが上書きされるので、コマンドラインパラメーターは設定ファイルとデフォルトの両方よりも優先されることに注意してください。

以下の例は、 `template` プロパティ `CreatePageTreeTest` コマンドラインパラメーターまたは yaml 設定ファイルを使用してテストします。

コマンドラインパラメーターを使用する場合：

```xml
java -jar toughday2.jar --host=localhost --add CreatePageTreeTest template=/conf/toughday-templates/settings/wcm/templates/toughday-template
```

yaml 設定ファイルを使用する場合：

```xml
globals:
  host : localhost
tests:
  - add : CreatePageTreeTest
    properties:
      template : /conf/toughday-templates/settings/wcm/templates/toughday-template
```

### 事前定義済みのテストスイートの使用 {#working-with-predefined-test-suites}

次の例は、事前定義済みのスイートにテストを追加する方法、および事前定義済みのスイートから既存のテストを再設定および除外する方法を示しています。

事前定義済みのスイートに新しいテストを追加するには、`add` パラメーターを使用して、ターゲットとなる事前定義済みのスイートを指定します。

コマンドラインパラメーターを使用する場合：

```xml
java -jar toughday2.jar --host=localhost --suite=toughday --add CreatePageTreeTest
```

yaml 設定ファイルを使用する場合：

```xml
globals:
  host : localhost
  suite : toughday
tests:
  - add : CreatePageTreeTest
```

特定のスイート内の既存のテストは、 `config`* *パラメーターです。 また、（テストクラス名ではなく）スイート名とテストの実際の名前も指定する必要があります。 テスト名は、テストクラスの `name` プロパティで確認できます。テストプロパティの確認方法について詳しくは、[テストプロパティの変更](/help/sites-developing/tough-day.md#changing-the-test-properties)を参照してください。

以下の例では、 `CreatePageTreeTest` ( 名前 `UploadAsset`) が「NewAsset」に変更されます。

コマンドラインパラメーターを使用する場合：

```xml
java -jar toughday2.jar --host=localhost --suite=toughday --config UploadAsset title=NewAsset
```

yaml 設定ファイルを使用する場合：

```xml
globals:
  host : localhost
  suite : toughday
tests:
  - config : UploadAsset
    properties :
      title : NewAsset 
```

さらに、`exclude` パラメーターを使用して、事前定義済みのスイートからテストを削除したり、デフォルトの設定から公開者を削除したりできます。また、（テスト C ではなく）テストのスイート名と実際の名前も指定する必要があります `lass` 名前 ) を参照してください。 テスト名は、 `name` プロパティを設定します。 次の例では、 `CreatePageTreeTest` ( 名前 `UploadAsset`) テストは toughday スイートから削除されます。

コマンドラインパラメーターを使用する場合：

```xml
java -jar toughday2.jar --host=localhost --suite=toughday --exclude UploadAsset
```

yaml 設定ファイルを使用する場合：

```xml
globals:
  host : localhost
  suite : toughday
tests:
  - exclude : UploadAsset 
```

### 実行モード {#run-modes}

Tough Day 2 は、次のいずれかのモードで実行できます。 **標準** および **一定荷重**.

この **標準** 実行モードには次の 2 つのパラメーターがあります。

* `concurrency` - concurrency は、Tough Day 2 でテスト実行用に作成されるスレッドの数を表します。 これらのスレッドでは、実行時間が終了するか、実行するテストがなくなるまでテストが実行されます。

* `waittime` - 同じスレッド上の連続した 2 つのテスト実行の間の待機時間。この値はミリ秒単位で指定する必要があります。

次の例は、コマンドラインを使用してパラメーターを追加する方法を示しています。

```xml
java -jar toughday2.jar --host=localhost --add CreateAssetTreeTest --runmode=normal concurrency=20
```

または、yaml 設定ファイルを使用してパラメーターを追加する方法もあります。

```xml
runmode:
  type : normal
  waittime : 300
  concurrency : 200
```

この **一定荷重** 実行モードは、一定数のスレッドではなく、開始されたテスト実行の定数を生成することで、通常の実行モードとは異なります。 同じ名前の実行モードパラメーターを使用して、読み込みを設定できます。

### テストの選択 {#test-selection}

テストの選択プロセスは、両方の実行モードで同じで、次のように実行されます。すべてのテストには `weight` スレッドでの実行の可能性を決定するプロパティ。 例えば、テストが 2 つあり、一方の重みを 5、もう一方の重みを 10 とした場合、後者が実行される可能性は前者の 2 倍になります。

さらに、テストには `count` プロパティを使用します。このプロパティの場合、実行回数を指定した数に制限します。 この回数に達すると、それ以上テストは実行されません。既に実行中のテストインスタンスはすべて、設定されたとおりに実行を終了します。次の例は、コマンドラインまたは yaml 設定ファイルを使用してこれらのパラメーターを追加する方法を示しています。

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
>同時実行により、実際のテスト実行数が、 `count` パラメーター。 偏差は、実行中のスレッドの数に比例します ( `concurrency parameter`) をクリックします。

### ドライラン {#dry-run}

ドライランでは、指定されたすべての入力（コマンドラインパラメーターまたは設定ファイル）が解析され、デフォルト値と統合された結果が出力されます。テストは実行されません。

```xml
java -jar toughday2.jar --host=localhost --suite=toughday --add CreatePageTreeTest --dryrun=true
```

## 出力 {#output}

Tough Day 2 では、テストの指標とログの両方が出力されます。詳しくは、これ以降の項を参照してください。

### テスト指標 {#test-metrics}

現在、Tough Day 2 では、ユーザーが評価できる 9 種類のテスト指標が報告されます。指標と **&amp;ast;** シンボルは、正常に実行された後にのみ報告されます。

| **名前** | **説明** |
|---|---|
| Timestamp | 最後に完了したテスト実行のタイムスタンプ。 |
| 渡された | 成功した実行の数。 |
| 失敗 | 失敗した実行の数。 |
| 最小 (&amp;A); | テスト実行の最短期間。 |
| 最大 (&amp;A); | テスト実行の最長期間。 |
| 中央値 (&amp;A); | すべてのテスト実行の計算された中央値時間。 |
| 平均 (&amp;A); | すべてのテスト実行の平均時間を計算しました。 |
| StdDev&amp;ast; | 標準偏差です。 |
| 90p&amp;ast; | 90 百分位 |
| 99p&amp;ast; | 99 百分位 |
| 99.9p&amp;ast; | 99.9 百分位 |
| 実際のスループット (&amp;A); | 実行回数を経過した実行時間で割った値です。 |

これらの指標は、 `add` パラメーター（テストの追加と同様） 現在、次の 2 つのオプションがあります。

* **CSVPublisher**  — 出力は CSV ファイルです。
* **ConsolePublisher**  — 出力はコンソールに表示されます。

デフォルトでは、両方の公開者が有効になっています。

さらに、指標がレポートされるモードは 2 つあります。

* この **単純** 公開モード — 実行の開始から公開時までの結果をレポートします。
* この **間隔** 公開モード — 指定された時間枠で結果を報告します。 時間枠は、 **間隔** 公開モードパラメーター。

次の例は、コマンドラインまたは yaml 設定ファイルを使用して `intervals` パラメーターを設定する方法を示しています。

コマンドラインパラメーターを使用する場合：

```xml
java -jar toughday2.jar --host=localhost --add CreatePageTreeTest --publishmode type=intervals interval=10s 
```

yaml 設定ファイルを使用する場合：

```xml
publishmode:
     type : intervals 
     interval : 10s 
     tests: 
        -add : CreatePageTreeTest
```

### ログ {#logging}

Tough Day 2 では、Tough Day 2 を実行したのと同じディレクトリにログフォルダーが作成されます。 このフォルダーには次の 2 種類のログが格納されます。

* **toughday.log**：アプリケーションの状態に関連したメッセージ、デバッグ情報およびグローバルメッセージが格納されます。
* **toughday_&lt;testname>.log**：指定したテストに関連するメッセージ。

ログは上書きされません。その後の実行では、既存のログにメッセージが追加されます。ログには複数のレベルがあります。詳しくは、 ` [loglevel parameter](/help/sites-developing/tough-day.md#global-parameters)`.
