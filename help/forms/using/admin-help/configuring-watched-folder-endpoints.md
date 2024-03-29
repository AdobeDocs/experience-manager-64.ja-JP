---
title: 監視フォルダーのエンドポイントの設定
seo-title: Configuring watched folder endpoints
description: 監視フォルダーエンドポイントを設定する方法について説明します。
seo-description: Learn how to configure watched folder endpoints.
uuid: 01fb5ff8-2071-44bd-9241-7d5d41a5b26e
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/managing_endpoints
products: SG_EXPERIENCEMANAGER/6.4/FORMS
discoiquuid: 761e7909-43ba-4642-bcfc-8d76f139b9a3
exl-id: bce7eee6-17c6-4eaf-b679-b47e611bed87
source-git-commit: c5b816d74c6f02f85476d16868844f39b4c47996
workflow-type: tm+mt
source-wordcount: '7199'
ht-degree: 25%

---

# 監視フォルダーのエンドポイントの設定 {#configuring-watched-folder-endpoints}

>[!CAUTION]
>
>AEM 6.4 の拡張サポートは終了し、このドキュメントは更新されなくなりました。 詳細は、 [技術サポート期間](https://helpx.adobe.com/jp/support/programs/eol-matrix.html). サポートされているバージョンを見つける [ここ](https://experienceleague.adobe.com/docs/?lang=ja).

管理者は、ネットワークフォルダー ( *監視フォルダー*&#x200B;を使用して監視フォルダーにファイル (PDFファイルなど ) を配置すると、設定済みのサービス操作が呼び出され、ファイルが操作されます。 サービスが指定の操作を実行した後に、変更されたファイルが指定の出力フォルダーに保存されます。

## Watched Folder サービスの設定 {#configuring-the-watched-folder-service}

監視フォルダーエンドポイントを設定する前に、Watched Folder サービスを設定します。 Watched Folder サービスの設定パラメーターには、次の 2 つの目的があります。

* すべての監視フォルダーエンドポイントに共通する属性を設定するには
* すべての監視フォルダーエンドポイントのデフォルト値を指定する

Watched Folder サービスを設定した後、ターゲットサービスの Watched Folder エンドポイントを追加します。 エンドポイントを追加する際には、設定済みの Watched Folder サービスの入力フォルダーにファイルやフォルダーが配置されている場合に呼び出すサービス名や操作名などの値を設定します。 Watched Folder サービスの設定について詳しくは、 [Watched Folder サービスの設定](/help/forms/using/admin-help/configure-service-settings.md#watched-folder-service-settings).

## 監視フォルダーの作成 {#creating-a-watched-folder}

監視フォルダーは、次の 2 つの方法で作成できます。

* 監視フォルダーエンドポイントを設定する際には、次の例に示すように、「パス」ボックスに親ディレクトリの完全パスを入力し、作成する監視フォルダーの名前を追加します。
   `  C:\MyPDFs\MyWatchedFolder`MyWatchedFolder フォルダーはもともと存在していないので、AEM Forms は指定した場所にこのディレクトリを作成しようとします。

* 監視フォルダーエンドポイントを設定する前に、ファイルシステム上にフォルダーを作成し、「パス」ボックスにフルパスを入力します。

クラスター環境では、監視フォルダーとして使用されるフォルダーは、ファイルシステムまたはネットワーク上でアクセス、書き込み、共有が可能である必要があります。 このシナリオでは、クラスターの各アプリケーションサーバーインスタンスが同じ共有フォルダーにアクセスできる必要があります。

Windows では、アプリケーションサーバーがサービスとして実行されている場合、次のいずれかの方法で、共有フォルダーへの適切なアクセス権でアプリケーションサーバーを起動する必要があります。

* アプリケーションサーバーサービスの「ログオン」**パラメーター**&#x200B;を設定し、共有監視フォルダーへの適切なアクセス権を持つ特定のユーザーとして起動します。
* アプリケーションサーバーサービスの「ローカルシステムアカウント」オプションで「デスクトップとの対話をサービスに許可」を設定します。このオプションを使用するには、共有監視フォルダーが全員がアクセス可能で書き込み可能である必要があります。

## 監視フォルダーの連結 {#chaining-together-watched-folders}

複数の監視フォルダーを連結して、1 つの監視フォルダーの結果ドキュメントを次の監視フォルダーの入力ドキュメントにすることができます。 各監視フォルダーは、異なるサービスを呼び出すことができます。 この方法で監視フォルダーを設定すると、複数のサービスを呼び出すことができます。 例えば、1 つの監視フォルダーではPDFファイルをAdobe PostScript®に、もう 1 つの監視フォルダーでは PostScript ファイルをPDF/A 形式に変換することができます。 そのためには、最初のエンドポイントで定義されている監視フォルダーの&#x200B;*結果*&#x200B;フォルダーを、次のエンドポイントで定義されている監視フォルダーの&#x200B;*入力*&#x200B;フォルダーに設定します。

そうすると、最初の変換処理からの出力は、\path\result に送られます。2 回目の変換処理に対する入力は \path\result になり、2 回目の変換処理からの出力は \path\result\result（または 2 回目の変換処理用に「結果フォルダー」ボックスで定義したディレクトリ）に送られます。

## ユーザーが監視フォルダーとやり取りする方法 {#how-users-interact-with-watched-folders}

監視フォルダーエンドポイントの場合、ユーザーは、入力ファイルやフォルダーをデスクトップから監視フォルダーにコピーまたはドラッグすることで、を呼び出すことができます。 ファイルは、到着した順に処理されます。

監視フォルダーエンドポイントの場合、ジョブに必要な入力ファイルが 1 つだけの場合、ユーザーはそのファイルを監視フォルダーのルートにコピーできます。

ジョブに複数の入力ファイルが含まれる場合、ユーザーは監視フォルダー階層の外側に、必要なファイルをすべて含むフォルダーを作成する必要があります。 この新しいフォルダーには、入力ファイルが含まれている必要があります（プロセスで必要に応じて DDX ファイルも含まれます）。 ジョブフォルダーが構築されたら、ユーザーはそのフォルダーを監視フォルダーの入力フォルダーにコピーします。

>[!NOTE]
>
>アプリケーションサーバーが監視フォルダー内のファイルへのアクセス権を削除したことを確認します。 スキャン後にAEM forms が入力フォルダーからファイルを削除できない場合、関連するプロセスは無期限に呼び出されます。

## 監視フォルダーの出力 {#watched-folder-output}

入力がフォルダーで、出力が複数のファイルで構成されている場合、AEM forms は入力フォルダーと同じ名前の出力フォルダーを作成し、出力ファイルをそのフォルダーにコピーします。 出力がキーと値のペアを含むドキュメントマップで構成されている場合（Output プロセスの出力など）、キーが出力ファイル名として使用されます。

エンドポイントプロセスによって生成される出力ファイル名に、文字、数字、ピリオド (.) 以外の文字を含めることはできません を追加します。 AEM forms は、その他の文字を 16 進数値に変換します。

クライアントアプリケーションは、監視フォルダーの結果フォルダーから結果ドキュメントを取得します。 プロセスエラーは、監視フォルダーの失敗フォルダーに記録されます。

## 監視フォルダーの仕組み {#how-watched-folder-works}

監視フォルダーモジュールには、次のサービスが含まれています。

* Watched Folder サービス
* provider.file_scan_service
* provider.file_write_results_service

上記のサービスに加えて、監視フォルダーは、ジョブをスケジュールするスケジューラーサービスや、ターゲットサービスの非同期呼び出しをサポートする Job Manager サービスなど、他のサービスにも依存します。

### 監視フォルダーによる呼び出し要求の処理方法 {#how-watched-folder-processes-an-invocation-request}

Watched Folder サービスは、エンドポイントの作成、更新および削除を処理します。 管理者がエンドポイントを作成した後、エンドポイントは、指定された繰り返し間隔または Cron 式に基づいて、スケジューラーサービスによってトリガーされるようにスケジュールされます。

次の図は、監視フォルダーが呼び出し要求を処理する方法を示しています。

![en_watchedfolder](assets/en_watchedfolder.png)

監視フォルダーを使用してサービスを呼び出すプロセスは、次のとおりです。

1. クライアントアプリケーションは、ファイルまたはフォルダーを監視フォルダーの入力フォルダーに配置します。
1. ジョブスキャン間隔が発生すると、スケジューラーサービスは provider.file_scan_service を呼び出して、入力フォルダー内のファイルまたはフォルダーを処理します。
1. provider.file_scan_service は次のタスクを実行します。

   * 「ファイルを含める」パターンに一致するファイルまたはフォルダーが入力フォルダー内にないかをスキャンし、指定した「ファイルを除外」パターンのファイルまたはフォルダーを除外します。 最も古いファイルまたはフォルダーが最初に取得されます。 待機時間よりも古いファイルやフォルダーも取得されます。 1 回のスキャンでは、処理されるファイルまたはフォルダーの数はバッチサイズに基づきます。 ファイルパターンについて詳しくは、 [ファイルパターンについて](configuring-watched-folder-endpoints.md#about-file-patterns). バッチサイズの設定については、 [Watched Folder サービスの設定](/help/forms/using/admin-help/configure-service-settings.md#watched-folder-service-settings).
   * 処理するファイルまたはフォルダーを取得します。 ファイルまたはフォルダーが完全にダウンロードされない場合は、次のスキャンで取得されます。 フォルダーが完全にダウンロードされるようにするには、管理者は、「ファイルを除外」パターンを使用して、名前の付いたフォルダーを作成する必要があります。 フォルダーにすべてのファイルが含まれたら、その名前を、「ファイルパターンを含める」で指定したパターンに変更する必要があります。 この手順により、サービスを呼び出すのに必要なファイルがフォルダーにすべて含まれるようになります。 フォルダーが完全にダウンロードされるようにする方法について詳しくは、 [監視フォルダーのヒントとテクニック](configuring-watched-folder-endpoints.md#tips-and-tricks-for-watched-folders).
   * 処理対象として選択したファイルまたはフォルダをステージフォルダに移動します。
   * エンドポイント入力パラメーターのマッピングに基づいて、ステージフォルダー内のファイルまたはフォルダーを適切な入力に変換します。 入力パラメーターのマッピングの例については、 [監視フォルダーのヒントとテクニック](configuring-watched-folder-endpoints.md#tips-and-tricks-for-watched-folders).

1. エンドポイントに設定されたターゲットサービスは、同期または非同期で呼び出されます。 ターゲットサービスは、エンドポイントに設定されたユーザー名とパスワードを使用して呼び出されます。

   * 同期呼び出しは、ターゲットサービスを直接呼び出し、応答を直ちに処理します。
   * 非同期呼び出しの場合、ターゲットサービスは Job Manager サービスを通じて呼び出され、リクエストがキューに配置されます。 次に、Job Manager サービスは、provider.file_write_results_service を呼び出して結果を処理します。

1. provider.file_write_results_service は、ターゲットサービス呼び出しの応答または失敗を処理します。 成功した場合、出力はエンドポイントの設定に基づいて結果フォルダーに保存されます。 また、正常に完了した場合に結果を保持するようにエンドポイントが設定されている場合は、provider.file_write_results_service もソースを保持します。

   ターゲットサービスの呼び出しでエラーが発生すると、provider.file_write_results_service は失敗の理由を failure.log ファイルに記録し、そのファイルを failure フォルダーに配置します。 失敗フォルダーは、エンドポイントに指定された設定パラメーターに基づいて作成されます。 管理者がエンドポイント設定に対して「Preserve On Failure」オプションを設定すると、provider.file_write_results_service もソースファイルを失敗フォルダーにコピーします。 失敗フォルダからファイルを回復する方法については、 [障害点と回復](configuring-watched-folder-endpoints.md#failure-points-and-recovery).

## 監視フォルダーエンドポイントの設定 {#watched-folder-endpoint-settings}

次の設定を使用して、監視フォルダーエンドポイントを設定します。

**名前：**（必須）エンドポイントを識別します。&lt; は含めないでください。含めると、Workspace に表示される名前の一部が省略されます。エンドポイント名として URL を入力する場合は、RFC1738 で指定された構文規則に準拠していることを確認します。

**説明：** エンドポイントの説明。&lt; は含めないでください。含めると、Workspace に表示される説明の一部が省略されます。

**パス：**：（必須）監視フォルダーの場所を指定します。クラスター環境では、クラスター内のすべてのコンピューターからアクセスできる共有ネットワークフォルダーを指定する必要があります。

**非同期：** 呼び出しを非同期型にするか同期型にするかを指定します。デフォルト値は asynchronous（非同期）です。長期間有効なプロセスでは非同期を、一時的なプロセスまたは短時間有効なプロセスでは同期をお勧めします。

**Cron 式：** Cron 式を使用して監視フォルダーをスケジュールする必要がある場合は Cron 式を入力します。これを設定すると、「繰り返し間隔」は無視されます。

**繰り返し間隔：**&#x200B;入力用の監視フォルダーをスキャンする間隔（秒）。「スロットル」設定が有効になっていない場合、「繰り返し間隔」は平均ジョブの処理時間より長くする必要があります。そうしないと、システムが過負荷になる場合があります。 デフォルト値は 5 です。詳しくは、バッチサイズの説明を参照してください。

**繰り返し回数：**&#x200B;監視フォルダーでフォルダーまたはディレクトリをスキャンする回数。値を —1 にすると、無限にスキャンされます。 デフォルト値は -1 です。

**スロットル：**&#x200B;このオプションを選択すると、AEM Forms で同時に処理できる監視フォルダーのジョブ数が制限されます。ジョブの最大数は、バッチサイズ値によって決まります（「ジョブ数の制限について」を参照）。

**ユーザー名：**（必須）監視フォルダーからターゲットサービスを呼び出すときに使用されるユーザー名です。デフォルト値は「SuperAdmin」です。

**ドメイン名：**（必須）ユーザーのドメイン。デフォルト値は「DefaultDom」です。

**バッチサイズ：** 1 回のスキャンで取得されるファイルまたはフォルダーの数を指定します。システムの過負荷を防ぐには、を使用します。一度にスキャンするファイル数が多すぎると、クラッシュが発生する可能性があります。 デフォルト値は 2 です。

「繰り返し間隔」および「バッチサイズ」の設定により、監視フォルダーがスキャンごとに取得するファイルの数が決まります。 監視フォルダーは、Quartz スレッドプールを使用して入力フォルダーをスキャンします。 スレッドプールは他のサービスと共有されます。 スキャンの間隔が小さい場合、スレッドは入力フォルダーを頻繁にスキャンします。 ファイルが頻繁に監視フォルダーに配置される場合は、スキャンの間隔を小さくする必要があります。 ファイルが頻繁に配置されない場合は、他のサービスがスレッドを使用できるように、より大きなスキャン間隔を使用します。

大量のファイルがドロップされる場合は、バッチサイズを大きくします。 例えば、監視フォルダーエンドポイントによって呼び出されたサービスが 1 分あたり 700 個のファイルを処理し、ユーザーが同じ速度で入力フォルダーにファイルをドロップした場合、バッチサイズを 350 に設定し、繰り返し間隔を 30 秒に設定すると、監視フォルダーのパフォーマンスが向上します。

ファイルが監視フォルダーに配置されると、入力内のファイルが一覧表示されます。これにより、スキャンが 1 秒ごとにおこなわれるとパフォーマンスが低下する可能性があります。 スキャン間隔を長くすると、パフォーマンスが向上します。 ドロップされるファイルの量が少ない場合は、それに応じて [ バッチサイズ ] と [ 繰り返し間隔 ] を調整します。 例えば、1 秒ごとに 10 個のファイルが配置される場合は、「繰り返し間隔」を 1 秒に、「バッチサイズ」を 10 に設定します。

**待機時間：**&#x200B;フォルダーまたはファイルの作成後にスキャンを実行するまでの待機時間（ミリ秒単位）。例えば、待機時間が 3,600,000 ミリ秒（1 時間）で、1 分前にファイルが作成された場合、このファイルは 59 分以上経過した後に取得されます。 デフォルト値は 0 です。

この設定は、ファイルまたはフォルダーを入力フォルダーに完全にコピーする場合に便利です。 例えば、処理の対象となるファイルサイズが大きく、そのファイルをダウンロードするのに 10 分かかる場合は、待機時間を 10 x 60 x 1000 ミリ秒に設定します。この設定により、ファイルが作成されてから 10 分が経過していない場合は、監視フォルダーはそのファイルをスキャンしなくなります。

**ファイルパターンを除外：**&#x200B;スキャンおよび取得の対象とするファイルとフォルダーを決めるために監視フォルダーで使用されるパターンのセミコロン（**;**）区切りのリスト。このパターンを持つファイルまたはフォルダーは、スキャンされて処理されません。

この設定は、入力が複数のファイルを含むフォルダーの場合に役立ちます。 フォルダーの内容を、監視フォルダーで取得される名前のフォルダーにコピーできます。 これにより、フォルダーが入力フォルダーに完全にコピーされる前に、監視フォルダーが処理対象のフォルダーを取得するのを防ぎます。

  次のように、除外するファイルパターンを指定できます。

* 特定のファイル拡張子を持つファイル例： &amp;ast;.dat, &amp;ast;.xml, &amp;ast;.pdf
* data.&amp;ast;次の名前のファイルとフォルダを除外します： *data1*、*data2* など。
* 次のような名前および拡張子が混在する式に一致するファイル。

   * Data[0-9][0-9][0-9].[dD][aA][tT]
   * &amp;ast;。[dD][Aa][Tt]
   * &amp;ast;。[Xx][Mm][Ll]

ファイルパターンについて詳しくは、「[ファイルパターンについて](configuring-watched-folder-endpoints.md#about-file-patterns)」を参照してください。

**ファイルパターンを含める：**（必須）スキャンおよび取得の対象とするファイルとフォルダーを決めるために監視フォルダーで使用されるパターンのセミコロン（**;**）区切りのリスト。例えば、「ファイルパターンを含める」が「input&amp;ast;」の場合、名前が input&amp;ast; に一致するすべてのファイルおよびフォルダーが取得されます。input1、input2 などの名前を持つファイルおよびフォルダーが含まれます。

デフォルト値は &amp;ast; です。すべてのファイルとフォルダーが対象となります。

次のように、含めるファイルパターンを指定できます。

* 特定のファイル拡張子を持つファイル例： &amp;ast;.dat, &amp;ast;.xml, &amp;ast;.pdf
* data.&amp;ast; を指定すると、*data1* や *data2* などの名前を持つファイルおよびフォルダーが対象に含まれます。
* 次のような名前および拡張子が混在する式に一致するファイル。

   * Data[0-9][0-9][0-9].[dD][aA][tT]
   * &amp;ast;。[dD][Aa][Tt]
   * &amp;ast;。[Xx][Mm][Ll]

ファイルパターンについて詳しくは、「[ファイルパターンについて](configuring-watched-folder-endpoints.md#about-file-patterns)」を参照してください。

**結果フォルダー：**&#x200B;保存結果を格納するフォルダー。結果がこのフォルダーに表示されない場合は、失敗フォルダーを確認します。 読み取り専用ファイルは処理されず、失敗フォルダーに保存されます。この値は、絶対パスまたは相対パスに指定でき、次のファイルパターンを使用します。

* %F =ファイル名のプレフィックス
* %E =ファイル名拡張子
* %Y =年（全角）
* %y =年（下 2 桁）
* %M =月
* %D =日
* %d =日（通日）
* %H =時（24 時間）
* %h =時（12 時間）
* %m =分
* %s =秒
* %l =ミリ秒
* %R =乱数 (0 ～ 9)
* %P =プロセスまたはジョブ ID

例えば、 2009年7月17日午後8時に `C:/Test/WF0/failure/%Y/%M/%D/%H/` と指定した場合、結果フォルダーは `C:/Test/WF0/failure/2009/07/17/20` になります。

絶対パスではなく相対パスを指定した場合、そのフォルダーは監視フォルダー内に作成されます。 デフォルト値は result/%Y/%M/%D/です。これは、監視フォルダー内の結果フォルダーです。 ファイルパターンについて詳しくは、「[ファイルパターンについて](configuring-watched-folder-endpoints.md#about-file-patterns)」を参照してください。

>[!NOTE]
>
>結果フォルダーのサイズが小さいほど、監視フォルダーのパフォーマンスが向上します。 例えば、監視フォルダーの推定負荷が 1 時間に 1000 個のファイルである場合、1 時間ごとに新しいサブフォルダーが作成されるように `result/%Y%M%D%H` のようなパターンを使用します。これよりも負荷が小さい場合（例えば、1 日に 1000 個のファイル）、`result/%Y%M%D` のようなパターンを使用することもできます。

**保存用フォルダー：** 正常にスキャンされ、取得されたファイルが格納される場所。パスは、絶対パス、相対パス、または null のディレクトリパスにすることができます。 「結果フォルダ」の説明に従って、ファイルパターンを使用できます。 デフォルト値は preserve/%Y/%M/%D/です。

**失敗フォルダー：** 失敗ファイルが保存されるフォルダーです。この場所は、常に監視フォルダーからの相対パスで指定します。「結果フォルダ」の説明に従って、ファイルパターンを使用できます。

読み取り専用ファイルは処理されず、失敗フォルダーに保存されます。

デフォルト値は failure/%Y/%M/%D/です。

**エラー時に保存：**&#x200B;サービスで操作の実行に失敗した場合に入力ファイルを保存します。デフォルト値は true です。

**重複したファイル名を上書き：**&#x200B;この値を True に設定すると、結果フォルダーと保存用フォルダーにあるファイルが上書きされます。False に設定すると、名前には数値インデックスサフィックスを持つファイルおよびフォルダが使用されます。 デフォルト値は False です。

**クリア期間：**（必須）結果フォルダー内にこの値より古いファイルまたはフォルダーがあると、それらは削除されます。この値の単位は日です。この設定は、結果フォルダーがいっぱいにならないようにするのに役立ちます。

-1 日の値は、結果フォルダーを削除しないことを示します。 デフォルト値は -1 です。

**操作名：**（必須）監視フォルダーエンドポイントに割り当てることができる操作のリストです。

**入力パラメーターのマッピング：**&#x200B;サービスおよび操作を処理するために必要な入力を設定するために使用します。使用できる設定は、監視フォルダーエンドポイントを使用しているサービスによって異なります。 次の 2 種類の入力があります。

**リテラル：**&#x200B;監視フォルダーでは、フィールドに入力された値が表示どおりに使用されます。すべての基本 Java 型がサポートされます。例えば、String、long、int および Boolean などの入力が使用される API の場合、文字列は適切な型に変換され、サービスが呼び出されます。

**変数：**&#x200B;監視フォルダーでは、入力された値をファイルパターンとして使用して入力を取得します。例えば、パスワード暗号化サービスで、入力ドキュメントが PDF ファイルであることが必須の場合、ユーザーはファイルパターンとして *.pdf を使用できます。監視フォルダーは、このパターンに一致する監視フォルダー内のすべてのファイルを取得し、各ファイルに対してサービスを呼び出します。 変数を使用すると、すべての入力ファイルがドキュメントに変換されます。 Document を入力タイプとして使用する API のみがサポートされます。

**出力パラメーターのマッピング：**&#x200B;サービスおよび操作の出力を設定するために使用します。使用できる設定は、監視フォルダーエンドポイントを使用しているサービスによって異なります。

監視フォルダーの出力には、単一のドキュメント、ドキュメントのリスト、またはドキュメントのマップを指定できます。 その後、「出力パラメータのマッピング」で指定したパターンを使用して、これらの出力ドキュメントが結果フォルダに保存されます。

>[!NOTE]
>
>一意の出力ファイル名を生成する名前を指定すると、パフォーマンスが向上します。 例えば、サービスによって 1 つの出力ドキュメントが返され、「出力パラメーターのマッピング」により、これが `%F.%E`（入力ファイルのファイル名と拡張子）にマッピングされる場合を考えてみます。この場合、ユーザーが 1 分ごとに同じ名前のファイルを配置したときに、結果フォルダーが `result/%Y/%M/%D` に設定されており、「重複したファイル名を上書き」設定が無効になっていると、監視フォルダーは重複したファイル名を解決しようとします。この重複したファイル名を解決するプロセスが、パフォーマンスに影響を与えることがあります。この状況では、「出力パラメーターのマッピング」を `%F_%h_%m_%s_%l` に変更して名前に時、分、秒、ミリ秒を追加するか、または配置されるファイルに必ず一意の名前を使用すると、パフォーマンスが向上する可能性があります。

## ファイルパターンについて {#about-file-patterns}

管理者は、サービスを呼び出すことができるファイルの種類を指定できます。 監視フォルダーごとに複数のファイルパターンを設定できます。 ファイルパターンは、次のファイルプロパティのいずれかになります。

* 特定のファイル名拡張子を持つファイルの例：*.dat、*.xml、*.pdf
* data.&amp;ast;
* 次のような名前および拡張子が混在する式に一致するファイル。

   * Data[0-9][0-9][0-9].[dD][aA][tT]
   * &amp;ast;。[dD][Aa][Tt]
   * &amp;ast;。[Xx][Mm][Ll]

管理者は、結果を保存する出力フォルダーのファイルパターンを定義できます。 出力フォルダー（結果、保存、失敗）に関しては、管理者は次のファイルパターンを指定できます。

* %Y =年（全角）
* %y =年（下 2 桁）
* %M =月
* %D =日（通日）
* %d =日（通日）
* %h =時
* %m =分
* %s =秒
* %R =乱数 (0 ～ 9)
* %J =ジョブ名

例えば、結果フォルダーへのパスは `C:\Adobe\Adobe_Experience_Manager_forms\BarcodedForms\%y\%m\%d` のようになります。

出力パラメーターのマッピングでは、次のような追加のパターンも指定できます。

* %F =ソースファイル名
* %E =ソースファイル名の拡張子

出力パラメーターのマッピングパターンが「File.separator」（パスセパレーター）で終わる場合、フォルダーが作成され、内容がそのフォルダーにコピーされます。 パターンが「File.separator」で終わらない場合、コンテンツ（結果ファイルまたはフォルダー）がその名前で作成されます。出力パラメーターのマッピングについて詳しくは、 [監視フォルダーのヒントとテクニック](configuring-watched-folder-endpoints.md#tips-and-tricks-for-watched-folders).

## スロットルについて {#about-throttling}

監視フォルダーエンドポイントのジョブ数の制限を有効にすると、一度に処理できる監視フォルダーのジョブ数が制限されます。 ジョブの最大数はバッチサイズの値によって決まり、監視フォルダーエンドポイントでも設定できます。 制限の制限に達した場合、監視フォルダーの入力ディレクトリに入るドキュメントはポーリングされません。 ドキュメントは、他の監視フォルダージョブが完了し、別のポーリングが実行されるまで、入力ディレクトリに残ります。 同期処理の場合、ジョブが単一のスレッドで連続して処理される場合でも、1 回のポーリングで処理されたすべてのジョブがジョブ数の制限に加算されます。

>[!NOTE]
>
>スロットルは、クラスターでは拡大/縮小されません。 スロットルが有効な場合、クラスター全体では、いつでもバッチサイズで指定されたジョブ数を超えるジョブを処理できません。 この制限は、クラスター全体に適用され、クラスター内の各ノードに固有のものではありません。 例えば、バッチサイズが 2 の場合、2 つのジョブを処理する 1 つのノードでスロットル制限に達し、1 つのジョブが完了するまで他のノードは入力ディレクトリをポーリングしません。

### スロットルの仕組み {#how-throttling-works}

監視フォルダーは、繰り返し間隔ごとに入力フォルダーをスキャンし、バッチサイズで指定された数のファイルを取得し、それぞれのファイルのターゲットサービスを呼び出します。 例えば、バッチサイズが各スキャンで 4 の場合、監視フォルダーは 4 つのファイルを取得し、4 つの呼び出し要求を作成して、ターゲットのサービスを呼び出します。 これらの要求が完了する前に監視フォルダーが呼び出された場合は、前の 4 つのジョブが完了しているかどうかに関係なく、再び 4 つのジョブが開始されます。

ジョブ数の制限を使用すると、前のジョブが完了していない場合に、監視フォルダーが新しいジョブを呼び出さないようにできます。 監視フォルダーは、進行中のジョブを検出し、バッチサイズから進行中のジョブを引いた値に基づいて新しいジョブを処理します。 例えば、2 回目の呼び出しでは、完了したジョブの数が 3 つで、まだ処理中のジョブが 1 つだけの場合、監視フォルダーは 3 つのジョブのみを呼び出します。

* 監視フォルダーは、ステージフォルダーに存在するファイルの数に基づいて、進行中のジョブの数を調べます。 ステージフォルダーにファイルが未処理のまま残っている場合、監視フォルダーはこれ以上ジョブを呼び出しません。 例えば、バッチサイズが 4 で、3 つのジョブが停止している場合、監視フォルダーは以降の呼び出しで 1 つのジョブのみを呼び出します。 複数のシナリオが原因で、ファイルがステージフォルダーに未処理のまま残る場合があります。 ジョブが停止している場合、管理者は forms ワークフロー管理ページでプロセスを終了し、監視フォルダーによってファイルがステージフォルダーから移動されるようにします。
* 監視フォルダーがジョブを呼び出す前に forms サーバーがダウンした場合は、管理者がステージフォルダーからファイルを移動できます。 詳しくは、 [障害点と回復](configuring-watched-folder-endpoints.md#failure-points-and-recovery).
* Job Manager サービスが呼び出しを呼び出したときに Forms サーバーが実行されているが監視フォルダーが実行されていない場合は、サービスが順序どおりに開始されないときに監視フォルダーが実行されていない場合は、管理者がステージフォルダーからファイルを移動できます。 詳しくは、 [障害点と回復](configuring-watched-folder-endpoints.md#failure-points-and-recovery).

## パフォーマンスと拡張性 {#performance-and-scalability}

監視フォルダーは、1 つのノード上で合計 100 個のフォルダーを提供できます。 監視フォルダーのパフォーマンスは、forms サーバーのパフォーマンスによって異なります。 非同期呼び出しの場合、パフォーマンスは、Job Manager キュー内のシステム負荷とジョブにより大きく依存します。

監視フォルダーのパフォーマンスは、ノードをクラスターに追加することで向上できます。 監視フォルダーのジョブは、Quartz スケジューラーによってクラスターノード間で、また、非同期要求の場合は Job Manager サービスによって分散されます。 すべてのジョブはデータベースに保持されます。

監視フォルダーでのジョブのスケジュール設定、スケジュール解除、再スケジュールは、スケジューラーサービスに依存します。 スケジューラーサービススレッドプールを共有する他のサービス（イベント管理サービス、User Manager サービス、Email Provider サービスなど）を使用できます。 これは監視フォルダーのパフォーマンスに影響を与える可能性があります。 スケジューラーサービススレッドプールの調整は、すべてのサービスが使用を開始する際に必要になります。

## クラスター内の監視フォルダー {#watched-folders-in-a-cluster}

クラスターでは、監視フォルダーは Quartz スケジューラーと Job Manager サービスに依存して、ロードバランシングとフェイルオーバーをおこないます。 Quartz クラスターの動作について詳しくは、 [Quartz ドキュメント](https://www.quartz-scheduler.org/documentation).

監視フォルダーは、ポーリングごとに次の 3 つの主なタスクを実行します。

* フォルダーをスキャン
* ターゲットサービスを呼び出す
* 結果の処理

ロードバランシングとフェイルオーバーの動作は、監視フォルダーが同期呼び出し用に設定されているか非同期呼び出し用に設定されているかによって異なります。

### クラスター内の同期監視フォルダー {#synchronous-watched-folder-in-a-cluster}

同期呼び出しの場合、Quartz ロードバランサーは、ポーリングイベントを取得するノードを決定します。 ポーリングイベントを取得したノードは、次のすべてのタスクを実行します。フォルダーをスキャンし、ターゲットサービスを呼び出して、結果を処理します。

![en_synchwatchedfoldercluster](assets/en_synchwatchedfoldercluster.png)

同期呼び出しの場合、あるノードが失敗すると、Quartz スケジューラーは新しいポーリングイベントを他のノードに送信します。 失敗したノードで開始された呼び出しは失われます。 失敗したジョブに関連付けられたファイルを復元する方法の詳細については、 [障害点と回復](configuring-watched-folder-endpoints.md#failure-points-and-recovery).

### クラスター内の非同期監視フォルダー {#asynchronous-watched-folder-in-a-cluster}

非同期呼び出しの場合、Quartz ロードバランサーは、ポーリングイベントを取得するノードを決定します。 ポーリングイベントを取得したノードは、Job Manager サービスキューにリクエストを配置することで、入力フォルダーをスキャンし、ターゲットサービスを呼び出します。 次に、Job Manager サービスのロードバランサーが、呼び出し要求を処理するノードを決定します。 ノード A が呼び出し要求を作成した場合でも、ノード B が最終的に要求を処理する可能性があります。 または、呼び出し要求を開始したノードも、要求を処理することになる場合があります。

![en_asynchwatchedfoldercluster](assets/en_asynchwatchedfoldercluster.png)

非同期呼び出しの場合、あるノードが失敗すると、Quartz スケジューラーは新しいポーリングイベントを他のノードに送信します。 失敗したノードで作成された呼び出し要求は、Job Manager サービスキューに含まれ、他のノードに送信されて処理されます。 呼び出し要求が作成されないファイルは、ステージフォルダーに残ります。 失敗したジョブに関連付けられたファイルを復元する方法の詳細については、 [障害点と回復](configuring-watched-folder-endpoints.md#failure-points-and-recovery).

## 障害点と回復 {#failure-points-and-recovery}

ポーリングイベントのたびに、監視フォルダーは入力フォルダーをロックし、「ファイルを含める」パターンに一致するファイルをステージフォルダーに移動し、入力フォルダーのロックを解除します。 2 つのスレッドが同じファイルのセットを取得して 2 回処理しないように、ロックが必要です。 このような状況が発生する可能性は、繰り返し間隔を短くし、バッチサイズを大きくすると高くなります。 ファイルがステージフォルダーに移動されると、入力フォルダーはロック解除され、他のスレッドがフォルダーをスキャンできるようになります。 この手順は、あるスレッドがファイルを処理している間に他のスレッドがスキャンできるので、高いスループットを提供するのに役立ちます。

ファイルがステージフォルダーに移動されると、ファイルごとに呼び出し要求が作成され、ターゲットのサービスが呼び出されます。 監視フォルダーがステージフォルダー内のファイルを復元できない場合があります。

* 監視フォルダーが呼び出し要求を作成する前にサーバーがダウンした場合、ステージフォルダー内のファイルはステージフォルダーに残り、復元されません。
* 監視フォルダーがステージフォルダー内の各ファイルに対する呼び出し要求を正常に作成し、サーバーがクラッシュした場合、呼び出しの種類に応じて次の 2 つの動作が実行されます。

**同期：** 監視フォルダーがサービスを同期的に呼び出すように設定されている場合、ステージフォルダー内のすべてのファイルは未処理のままステージフォルダーに残ります。

**非同期：** この場合、監視フォルダーは Job Manager サービスに依存します。 Job Manager Service が監視フォルダーを呼び出すと、ステージフォルダー内のファイルは、呼び出しの結果に基づいて、保存フォルダーまたは失敗フォルダーに移動されます。 Job Manager サービスが監視フォルダーを呼び出さない場合、ファイルは未処理のままステージフォルダーに残ります。 この状況は、Job Manager がコールバックする際に監視フォルダーが実行されていない場合に発生します。

### ステージフォルダー内の未処理のソースファイルを復元しています {#recovering-unprocessed-source-files-in-the-stage-folder}

監視フォルダーがステージフォルダー内のソースファイルを処理できない場合は、未処理のファイルを復元できます。

1. アプリケーションサーバーまたはノードを再起動します。
1. （オプション）監視フォルダーが新しい入力ファイルを処理しないようにします。 この手順をスキップすると、どのファイルがステージフォルダーで未処理かを判断するのがはるかに難しくなります。 監視フォルダーが新しい入力ファイルを処理しないようにするには、次のいずれかのタスクを実行します。

   * アプリケーションおよびサービスで、監視フォルダーエンドポイントに対する「ファイルパターンを含める」パラメーターを新しい入力ファイルのいずれにも一致しない値に変更します（例えば、「`NOMATCH`」と入力します）。
   * 新しい入力ファイルを作成するプロセスを休止します。
   AEM forms がすべてのファイルを回復して処理するまで待ちます。 大部分のファイルが復元され、新しい入力ファイルが正しく処理されます。 監視フォルダーがファイルを回復して処理するまでの待ち時間の長さは、呼び出す操作の長さと回復するファイルの数によって異なります。

1. 処理できないファイルを決定します。 適切な時間待って前の手順を完了し、ステージフォルダーに未処理のファイルが残っている場合は、次の手順に進みます。

   >[!NOTE]
   >
   >ステージディレクトリ内のファイルの日付とタイムスタンプを確認できます。 ファイルの数と通常の処理時間に応じて、停止していると見なされるだけの古いファイルを判断できます。

1. 未処理のファイルをステージディレクトリから入力ディレクトリにコピーします。
1. 手順 2 で監視フォルダーが新しい入力ファイルを処理できない場合は、「ファイルパターンを含める」を以前の値に変更するか、無効にしたプロセスを再度有効にします。

## 監視フォルダーのセキュリティに関する考慮事項 {#security-considerations-for-watched-folders}

各監視フォルダーには、ユーザー名とパスワードが設定されます。 これらの資格情報は、サービスを呼び出す際に使用されます。 監視フォルダーは、基になるセキュリティファイルシステムで共有フォルダーを保護しているので、監視フォルダーの所有者だけが共有フォルダーにアクセスできるようになっています。

## 監視フォルダーのヒントとテクニック {#tips-and-tricks-for-watched-folders}

次に、監視フォルダーエンドポイントを設定する際のヒントとテクニックを示します。

* Windows 上に画像ファイルを処理する監視フォルダーがある場合は、「ファイルパターンを含める」または「ファイルパターンを除外」オプションの値を指定して、Windows によって自動生成された Thumbs.db ファイルが監視フォルダーによってポーリングされないようにします。
* cron 式を指定した場合、繰り返し間隔は無視されます。 Cron 式の使用方法は、Quartz オープンソースジョブスケジューリングシステムのバージョン 1.4.0 に基づいています。
* バッチサイズは、監視フォルダーの各スキャンで取得されるファイルまたはフォルダーの数です。 バッチサイズを 2 に設定し、10 個のファイルまたはフォルダーが監視フォルダーの入力フォルダーにドロップされた場合、各スキャンでは 2 個のファイルまたはフォルダーのみが取得されます。 繰り返し間隔で指定された時間の後に発生する次のスキャンでは、次の 2 つのファイルが取得されます。
* ファイルパターンの場合、管理者は正規表現を指定できます。また、ワイルドカードパターンもサポートされているので、ファイルパターンを指定することができます。 監視フォルダーでは正規表現が変更されており、&amp;ast;.&amp;ast; や &amp;ast;.pdf などのワイルドカードパターンがサポートされます。これらのワイルドカードパターンは、正規表現ではサポートされていません。
* 監視フォルダーは入力フォルダーをスキャンし、入力フォルダーの処理を開始する前に、ソースファイルまたはフォルダーが入力フォルダーに完全にコピーされたかどうかを判断しません。 ソースファイルまたはフォルダーを取得する前に、ソースファイルまたはソースフォルダーを監視フォルダーの入力フォルダーに完全にコピーするには、次のタスクを実行します。

   * 待機時間を使用します。これは、最終変更時間から監視フォルダが待機する時間（ミリ秒単位）です。 処理する大きなファイルがある場合は、この機能を使用します。 例えば、ファイルのダウンロードに 10 分かかる場合は、待機時間を 10 x 60 x 1000 ミリ秒に指定します。これにより、監視フォルダーが 10 分も古くない場合は、ファイルを取得できなくなります。
   * 「ファイルパターンを除外」と「ファイルパターンを含める」を使用します。 例えば、「ファイルパターンを除外」を `ex*`、「ファイルパターンを含める」を `in*` とした場合、監視フォルダーは「in」で始まるファイルを取得し、「ex」で始まるファイルを取得しません。大きなファイルまたはフォルダーをコピーするには、まず「ex」で始まるようにファイルまたはフォルダーの名前を変更します。「ex」という名前のファイルまたはフォルダーが監視フォルダーに完全にコピーされたら、その名前を「in&amp;ast;」に変更します。

* 結果フォルダーをクリーンな状態に保つには、パージ期間を使用します。 監視フォルダーは、パージ期間に指定された期間より古いすべてのファイルをクリーンアップします。 期間は日数で指定します。
* 監視フォルダーエンドポイントを追加する際に、操作名を選択すると、入力パラメーターのマッピングが設定されます。 操作の入力ごとに、1 つの入力パラメータマッピングフィールドが生成されます。 次に、入力パラメーターのマッピングの例を示します。

   * `com.adobe.idp.Document` 入力の場合：サービス操作の入力タイプが `Document` である場合、マッピングの種類を `Variable` に指定できます。監視フォルダーは、入力パラメーター用に指定されているファイルパターンに基づいて監視フォルダーの入力フォルダーから入力を取得します。管理者が `*.pdf` をパラメーターとして指定した場合、拡張子が .pdf の各ファイルが取得され、`com.adobe.idp.Document` に変換されてから、サービスが呼び出されます。
   * `java.util.Map` 入力の場合：サービス操作の入力タイプが `Map` である場合、マッピングの種類を `Variable` に指定し、`*.pdf` のようなパターンを使用してマッピング値を入力できます。例えば、サービスが 1.pdf や 2.pdf など入力フォルダー内のファイルを表す 2 つの `com.adobe.idp.Document` オブジェクトのマップを必要としているとします。監視フォルダーは、キーがファイル名で、値が `com.adobe.idp.Document` であるマップを作成します。
   * `java.util.List` 入力の場合：サービス操作の入力タイプが List である場合、マッピングの種類を `Variable` に指定し、`*.pdf` のようなパターンを使用してマッピング値を入力できます。PDF ファイルが入力フォルダーに入ると、監視フォルダーは PDF ファイルを表す `com.adobe.idp.Document` オブジェクトのリストを作成し、ターゲットのサービスを呼び出します。
   * `java.lang.String` の場合：管理者にはオプションが 2 つ用意されています。1 つは、マッピングの種類を `Literal` に指定し、マッピング値に `hello.` などの文字列を入力することです。監視フォルダーは、文字列 `hello` でサービスを呼び出します。もう 1 つは、マッピングの種類を `Variable` に指定し、`*.txt` のようなパターンを使用してマッピング値を入力することです。後者の場合、拡張子が .txt のファイルは、サービスを呼び出す文字列となるドキュメントとして読み込まれます。
   * Java プリミティブ型：マッピングの種類を `Literal` に指定し、値を指定できます。監視フォルダーは、指定された値でサービスを呼び出します。

* 監視フォルダーは、ドキュメントを操作するためのものです。 サポートされている出力は、`com.adobe.idp.Document`、`org.w3c.Document`、`org.w3c.Node` のほか、これらのタイプのリストおよびマップです。その他のタイプの場合は、失敗フォルダーに失敗出力が出力されます。
* 結果が結果フォルダーにない場合は、失敗フォルダーを検証して、失敗が発生したかどうかを確認します。
* 監視フォルダーは、非同期モードで使用する場合に最も適しています。 このモードでは、監視フォルダーは呼び出し要求をキューに入れ、コールバックします。 その後、キューは非同期で処理されます。 Asynchronous オプションを設定しない場合、監視フォルダーはターゲットサービスを同期的に呼び出し、プロセスエンジンは、要求と結果が生成されるまで、サービスが完了するのを待ちます。 ターゲットのサービスが要求の処理に長い時間を要する場合、監視フォルダーはタイムアウトエラーを受け取る可能性があります。
* 読み込みおよび書き出し操作用の監視フォルダーを作成する場合、ファイル名拡張子を抽象化することはできません。 監視フォルダーを使用して Form Data Integration サービスを呼び出すとき、出力ファイルのファイル名拡張子の種類が、ドキュメントオブジェクトの種類で意図されている出力形式と一致しない場合があります。 例えば、書き出し操作を呼び出す監視フォルダーへの入力ファイルが、データを含む XFA フォームの場合、出力は XDP データファイルである必要があります。 正しいファイル名拡張子を持つ出力ファイルを取得するには、出力パラメーターマッピングで指定します。 この例では、出力パラメーターのマッピングに%F.xdp を使用できます。
* 監視フォルダーが入力ファイルをフォルダーに完全にコピーする前に処理する場合があります。 Windows の場合とは異なり、UNIX ではファイルのロックは必須ではありません。 このため、ファイルが監視フォルダーにコピーされる際に、監視フォルダーはファイルのコピーが完了するのを待たずに、ファイルをステージに移動する場合があります。 この動作により、入力ファイルの一部のみが処理されます。 現在、次の 2 つの回避策があります。

   * 回避策 1

      1. 「ファイルパターンを除外」に emp&amp;ast;.ps などのパターンを指定します。
      1. temp で始まるファイル（temp1.ps など）を監視フォルダーにコピーします。
      1. ファイルを監視フォルダーに完全にコピーした後で、「ファイルパターンを含める」に指定されているパターンに合わせてファイル名を変更します。監視フォルダーは、完了したファイルをステージに移動します。
   * 回避策 2

      ファイルを監視フォルダーにコピーするのにかかる最大時間がわかっている場合は、「待機時間」に秒単位で時間を指定します。 監視フォルダーは、指定された時間だけ待ってから、ファイルをステージに移動します。

      Windows では、1 つのスレッドが書き込み中にファイルがロックされるので、Windows 上のファイルに対しては、この問題は発生しません。 ただし、これは、Windows 上のフォルダーに関する問題です。 フォルダーの場合は、回避策 1 の手順に従う必要があります。


* 監視フォルダーの「フォルダー名を保持」エンドポイント属性が null ディレクトリパスに設定されている場合、ステージングディレクトリは必要に応じてクリーンアウトされません。 このディレクトリには、処理されたファイルと一時フォルダーが含まれます。

## 監視フォルダーに関するサービス固有の推奨事項 {#service-specific-recommendations-for-watched-folders}

すべてのサービスで、監視フォルダーのバッチサイズと繰り返し間隔を調整して、新しいファイルやフォルダーを監視フォルダーが取得する割合が、AEM forms サーバーで処理できるジョブの割合を超えないようにする必要があります。 実際に使用するパラメーターは、設定されている監視フォルダーの数、監視フォルダーを使用しているサービス、およびプロセッサーでのジョブの集中的な使用状況によって異なる場合があります。

### Generate PDF サービスの推奨事項 {#generate-pdf-service-recommendations}

* GeneratePDFサービスでは、次のファイル形式のファイルを一度に 1 つのみ変換できます。Microsoft Word、Microsoft Excel、Microsoft PowerPoint、Microsoft Project、AutoCAD、Adobe Photoshop®、Adobe FrameMaker®、およびAdobePageMaker®。 これらは長い間続いている仕事です。したがって、必ずバッチサイズを低い設定にしてください。 また、クラスター内にノードが他に存在する場合は、繰り返し間隔を長くします。
* PostScript(PS)、Encapsulated PostScript(EPS) および画像ファイルタイプの場合、GeneratePDFサービスは複数のファイルを並行して処理できます。 サーバーの容量とクラスタ内のノード数に応じて、セッション Bean プールのサイズを慎重に調整する必要があります（これは、並行して実行される変換の数を管理します）。 次に、変換しようとしているファイルタイプのセッション Bean プールサイズに等しい数にバッチサイズを増やします。 ポーリング頻度は、クラスター内のノード数によって決まります。ただし、GeneratePDFサービスはこの種のジョブを非常に高速に処理するので、繰り返し間隔を 5 や 10 などの低い値に設定できます。
* GeneratePDFサービスでは一度に 1 つの OpenOffice ファイルしか変換できませんが、変換処理は非常に高速です。 PS、EPS、画像の変換に関する上記のロジックは、OpenOffice の変換にも当てはまります。
* クラスタで均等な負荷分布を可能にするには、バッチサイズを低く保ち、繰り返し間隔を長くします。

### barcoded forms サービスに関する推奨事項 {#barcoded-forms-service-recommendations}

* バーコードフォーム（小さいファイル）の処理で最良のパフォーマンスを得るには、バッチサイズに `10`、繰り返し間隔に `2` を入力します。
* 数多くのファイルが入力フォルダーに配置されていると、*thumbs.db* という隠しファイルに関するエラーが発生することがあります。このため、インクルードファイルの「ファイルパターンを含める」を、入力変数用に指定されているのと同じ値（例：`*.tiff`）に設定することをお勧めします。これで、監視フォルダーが DB ファイルを処理できないようになります。
* Barcoded Forms サービスは通常 1 つのバーコードを処理するのに約 0.5 秒かかるので、通常はバッチサイズを `5`、繰り返し間隔を`2` とすれば十分です。
* 監視フォルダーは、プロセスエンジンがジョブを完了するのを待たずに、新しいファイルまたはフォルダーを取得します。 監視フォルダーのスキャンとターゲットサービスの呼び出しを継続します。 この動作がエンジンを過負荷にし、リソースの問題やタイムアウトを引き起こす可能性があります。 繰り返し間隔とバッチサイズを使用して、監視フォルダーの入力をスロットルします。 監視フォルダーが増えた場合は、繰り返し間隔を長くし、バッチサイズを小さくすることができます。また、エンドポイントでスロットルを有効にすることもできます。 スロットルについて詳しくは、 [スロットルについて](configuring-watched-folder-endpoints.md#about-throttling).
* 監視フォルダーは、ユーザー名とドメイン名で指定されたユーザーになりすまします。 直接呼び出す場合、またはプロセスが短時間のみ有効な場合は、監視フォルダーはこのユーザーとしてサービスを呼び出します。 長期間有効なプロセスの場合、プロセスは System コンテキストで呼び出されます。 管理者は、監視フォルダーのオペレーティングシステムポリシーを設定して、アクセスを許可または拒否するユーザーを決定できます。
* 結果、失敗、保存の各フォルダーを整理するには、ファイルパターンを使用します。 ( [ファイルパターンについて](configuring-watched-folder-endpoints.md#about-file-patterns).)
* 監視フォルダーでは、監視フォルダーのスキャンに Quartz スケジューラーを使用します。 Quartz スケジューラーには、スキャンするスレッドプールがあります。 監視フォルダーの繰り返し間隔が非常に短く（&lt; 5 秒）、バッチサイズが大きい (> 2) 場合は、競合状態が発生する可能性があります。 この状態が発生した場合、1 つのファイルが 2 つの Quartz スレッドで取得されます。

   * スレッドの 1 つが正常にファイルを検出し、そのファイルを使用してターゲットサービスを呼び出します。
   * 2 番目のスレッドは、ファイルを確認しますが、ファイルが有効（読み取りまたは書き込みファイル）かどうかを調べようとすると失敗し、ファイルが読み取り専用であるために処理できないことを示す誤ったエラーが発生します。 これは、繰り返し間隔が短く、バッチサイズが大きい場合にのみ発生します。
