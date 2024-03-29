---
title: AEM ドキュメントサービスの概要
seo-title: Overview of AEM Document Services
description: AEM Document Services は、PDFドキュメントを作成、アセンブリ、および保護するための OSGi サービスのセットです。
seo-description: AEM Document Services are a set of OSGi Services for creating, assembling, and securing PDF Documents.
uuid: 17fd42ef-9950-4b51-9ae7-82e8b4759fe8
content-type: reference
products: SG_EXPERIENCEMANAGER/6.4/FORMS
topic-tags: document_services
discoiquuid: 0685478b-d08e-4d69-8dd3-f75270772167
exl-id: aabfd05d-581b-4205-8e61-5667d5713cb1
source-git-commit: c5b816d74c6f02f85476d16868844f39b4c47996
workflow-type: tm+mt
source-wordcount: '1435'
ht-degree: 25%

---

# AEM ドキュメントサービスの概要 {#overview-of-aem-document-services}

>[!CAUTION]
>
>AEM 6.4 の拡張サポートは終了し、このドキュメントは更新されなくなりました。 詳細は、 [技術サポート期間](https://helpx.adobe.com/jp/support/programs/eol-matrix.html). サポートされているバージョンを見つける [ここ](https://experienceleague.adobe.com/docs/?lang=ja).

AEM Document Services は、PDFドキュメントを作成、アセンブリ、および保護するための OSGi サービスのセットです。 ドキュメントサービスには、次のサービスが含まれています。

## Output サービス {#output-service}

Output サービスを使用すると、PDF、レーザープリンター形式、ラベルプリンター形式など、様々な形式のドキュメントを作成できます。 レーザープリンター形式には、PostScript とプリンター制御言語（PCL）があります。次のリストでは、ラベルプリンタの形式を指定します。

* ゼブラ (ZPL)
* Intermec (IPL)
* Datamax(DPL)
* TecToshiba(TPCL)

ドキュメントは、ネットワークプリンター、ローカルプリンター、またはファイルシステム上のファイルに送信できます。 Output サービスは、XML フォームデータをフォームデザインとマージして、ドキュメントを生成します。 Output サービスは、XML フォームデータをドキュメントに結合せずにドキュメントを生成できます。 ただし、データをドキュメントに結合するのが本来のワークフローです。

>[!NOTE]
>
>フォームデザインは通常、Designer を使用して作成されます。 Output サービスのフォームデザインの作成について詳しくは、Designer ヘルプを参照してください。

Output サービスを使用して XML データをフォームデザインと結合すると、結果は非インタラクティブPDFドキュメントになります。 非インタラクティブな PDF ドキュメントのフィールドには、ユーザーがデータを入力することはできません。これに対し、Formsサービスを使用して、ユーザーがフィールドにデータを入力できるインタラクティブなPDFフォームを作成することもできます。

次の 4 つの Output サービス操作を使用できます。

* **generatePDFOuput**:フォームデザインをデータとマージしてPDFドキュメントを生成
* **generatePrintedOutput**：フォームデザインをフォームデータと結合して、レーザーネットワークプリンターまたはラベルネットワークプリンターに送信するドキュメントを生成します。

* **generatePDFOutputBatch**:複数のテンプレートと複数のデータレコードを結合して、1 回の呼び出しで複数のPDFファイルを生成します。 すべてのオプションを組み合わせて 1 つのPDFを生成するPDFもあります
* **generatePrintedOutputBatch**：複数のテンプレートと複数のデータレコードを結合して、1 回の実行で複数の印刷ドキュメント（PS、PCL、ZPL、DPL、IPL、TPCL）を生成します。1 つの印刷ドキュメントを生成するオプションもあります。

## Assembler サービス {#assembler-service}

Assembler サービスを使用すると、PDFドキュメントと XDP ドキュメントを組み合わせ、並べ替え、拡張し、PDFドキュメントに関する情報を取得できます。 Assembler サービスに送信される各ジョブには、Document Description XML(DDX) ドキュメント、ソースドキュメント、および外部リソース（文字列とグラフィック）が含まれます。 DDX ドキュメントには、ソースドキュメントを使用して一連の結果ドキュメントを生成する方法に関する指示が記載されています。

上記の機能以外に、Assembler サービスは、次の場合に使用します。

* PDFドキュメントをPDF/A 標準に変換します。
* PDF フォーム、XML フォーム（Designer で作成）および PDF フォーム（Acrobat で作成）を、PDF/A-1b、PDF/A-2b、PDFA/A-3b に変換します。
* 署名済みまたは未署名の PDF ドキュメントを変換します（電子署名が必要）。
* PDF/A ファイルのコンプライアンスを検証し、必要に応じて変換します。

### DDX について {#about-ddx}

Assembler サービスを利用するときは、必要な出力を記述するために Document Description XML（DDX）と呼ばれる XML ベースの言語を使用します。DDX は宣言的マークアップ言語で、その要素がドキュメントの構築ブロックを表します。 これらの構築ブロックには、PDFドキュメント、XDP ドキュメント、XDP フォームフラグメント、およびコメント、しおり、スタイル設定されたテキストなどのその他の要素が含まれます。

DDX ドキュメントは、次の特性を持つ結果ドキュメントを指定できます。

* 複数の PDF ドキュメントからアセンブリされた PDF ドキュメント
* 1 つの PDF ドキュメントから分割された複数の PDF ドキュメント
* 独立したユーザーインターフェイス、複数の PDF および非 PDF ドキュメントを含む PDF ポートフォリオ
* 複数の XDP ドキュメントからアセンブリされた XDP ドキュメント
* XDP ドキュメントに動的に挿入される XML フラグメントを含む XDP ドキュメント
* XDP ドキュメントをパッケージ化する PDF ドキュメント
* PDF・ドキュメントの特性を報告する XML ファイル。 レポートされる特性には、テキスト、コメント、フォームデータ、添付ファイル、PDFPortfolioで使用されるファイル、ブックマーク、PDFプロパティなどがあります。 PDFのプロパティには、フォームのプロパティ、ページの回転、ドキュメントの作成者が含まれます。

DDX を使用して、ドキュメントのアセンブリまたは分解の一環としてPDFドキュメントを拡張できます。 次の効果を任意に組み合わせて指定できます。

* 選択したページへの透かしまたは背景の追加または削除。
* 選択したページへのヘッダーとフッターの追加または削除。
* PDFパッケージまたはナビゲーションPortfolioの構造とPDF機能を削除します。 結果は 1 つのPDF・ファイルです。
* ページラベルの番号を変更します。 ページラベルは通常、ページの番号付けに使用されます。
* 別のソースドキュメントからのメタデータのインポート。
* 添付ファイル、しおり、リンク、コメントおよび JavaScript の追加または削除。
* 初期ビューの特性の設定と、web 上で表示する際の最適化。
* 暗号化された PDF に対する権限の設定。
* ページの回転またはページ上のコンテンツの回転およびシフト。
* 選択したページのサイズの変更。
* XFA ベースの PDF とのデータの統合。

単純な入力マップを使用して、ソースドキュメントと結果ドキュメントの場所を指定できます。 次の外部データ URL タイプも使用できます。

* File
* FTP
* HTTP／HTTPS

## Doc Assurance サービス {#doc-assurance-service}

Doc Assurance サービスを使用すると、ドキュメントの暗号化と復号化、追加の使用権限によるAdobe Readerの機能の拡張、ドキュメントへの電子署名の追加をおこなうことができます。 ユーザーはPDF formsやドキュメントと簡単にやり取りでき、組織はセキュリティ、アーカイブ、コンプライアンスを強化できます。

DocAssurance サービスには、3 つのサービス（署名、暗号化および Reader 拡張機能）があります。

### Signature Service {#signature-service}

Signature サービスを使用すると、AEMサーバー上で電子署名とドキュメントを操作できます。 例えば、通常、Signature サービスは次の状況で使用されます。

* AEMサーバーは、AcrobatまたはAdobe Readerを使用して開くユーザーにフォームが送信される前に、フォームを認証します。
* AEMサーバーは、AcrobatまたはAdobe Readerを使用してフォームに追加された署名を検証します。
* AEMサーバーは公証人に代わってフォームに署名します。

Signature サービスは、Trust Store に保存されている証明書と秘密鍵証明書にアクセスします。

### 暗号化サービス {#encryption-service}

Encryption サービスを使用すると、ドキュメントの暗号化と復号化をおこなうことができます。 ドキュメントが暗号化されると、その内容が読み取れなくなります。 PDFドキュメント全体（コンテンツ、メタデータ、添付ファイルを含む）、メタデータ以外のすべて、または添付ファイルのみを暗号化できます。 許可されたユーザーは、ドキュメントを復号化して、コンテンツにアクセスできます。 PDFドキュメントがパスワードで暗号化されている場合、ユーザーは開くパスワードを指定してから、Adobe ReaderまたはAcrobatでドキュメントを表示する必要があります。 PDFドキュメントが証明書で暗号化されている場合、ユーザーはPDFドキュメントを秘密鍵（証明書）で復号化する必要があります。 PDFドキュメントの復号化に使用する秘密鍵は、暗号化に使用した公開鍵に対応している必要があります。

### Reader拡張サービス {#reader-extension-service}

Reader拡張サービスを使用すると、Adobe Readerの機能を拡張し、追加の使用権限を付与して、組織でインタラクティブなPDFドキュメントを簡単に共有できます。 Reader拡張サービスは、Adobe Reader 7.0 以降で動作します。 このサービスは、使用権限をPDFドキュメントに追加します。 このアクションは、ドキュメントへのコメントの追加、フォームへの入力、ドキュメントの保存など、Adobe Readerを使用してPDFドキュメントを開いた場合は通常使用できない機能をアクティブにします。 サードパーティユーザーは、使用権限を付与されたドキュメントを扱うためにソフトウェアまたはプラグインを追加する必要はありません。

PDFドキュメントに適切な使用権限が追加されている場合、受信者はAdobe Reader内で次のアクティビティを実行できます。

* PDFのドキュメントとフォームをオンラインまたはオフラインで入力し、受信者がレコードのコピーをローカルに保存し、追加された情報をそのまま保持できるようにします。
* PDFドキュメントをローカルハードドライブに保存して、元のドキュメントと追加のコメント、データ、または添付ファイルを保持する
* ファイルとメディアクリップをPDFドキュメントに添付
* 業界標準の公開鍵基盤 (PKI) テクノロジーを使用して電子署名を適用し、PDFドキュメントの署名、認証、および認証を行います
* 完了したPDF文書または注釈付きドキュメントを電子的に送信
* PDFドキュメントとフォームを、内部データベースと Web サービスに対する直感的な開発フロントエンドとして使用
* PDFドキュメントを他のユーザーと共有して、レビュー担当者が直感的なマークアップツールを使用してコメントを追加できるようにします。 これらのツールには、電子付箋、スタンプ、ハイライト、テキスト取り消し線が含まれます。 Acrobatでも同じ機能を使用できます。
* バーコードフォームのデコードをサポートします。

これらの特別なユーザー機能は、権限が付与されたユーザードキュメントをAdobe Reader内で開くと、PDFが自動的に有効になります。 ユーザーが権限を付与されたドキュメントの操作を終了すると、Adobe Readerではこれらの関数が再び無効になります。 ユーザーが別の権限を付与されたPDF・ドキュメントを受け取るまで、これらは無効のままです。

DocAssurance サービスは、デフォルトでは使用できません。 DocAssurance サービスを設定するには、 [Document Services の設定](/help/forms/using/install-configure-document-services.md).

## プリンターへの送信サービス {#send-to-printer-service}

プリンターへの送信サービスは、ドキュメントを指定したプリンターに送信して印刷するための API を提供します。
