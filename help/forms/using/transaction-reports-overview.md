---
title: トランザクションレポートの概要
seo-title: Transaction Reports Overview
description: 送信されたすべてのフォーム、インタラクティブ通信のレンダリング、ドキュメントの形式変換などを行う
seo-description: Keep a count of all the forms submitted, interactive communication rendered, Documents converted to one format to another, and more
uuid: b40220e6-88c8-4507-b228-6c57d9b54422
contentOwner: khsingh
products: SG_EXPERIENCEMANAGER/6.4/FORMS
topic-tags: forms-manager
discoiquuid: 1fb11e02-d8f1-41a0-8e23-cb890b4e2244
source-git-commit: 0797eeae57ac5a9676c6d308eaf2aaffab999d18
workflow-type: tm+mt
source-wordcount: '570'
ht-degree: 0%

---


# トランザクションレポートの概要 {#transaction-reports-overview}

送信されたすべてのフォーム、インタラクティブ通信のレンダリング、ドキュメントの形式変換などを行う

## はじめに {#introduction}

AEM Formsのトランザクションレポートを使用すると、AEM Formsのデプロイメントで指定した日以降に発生したすべてのトランザクションの数を保持できます。 目的は、製品の使用状況に関する情報を提供し、ビジネスの関係者がデジタル処理量を理解できるようにすることです。 トランザクションの例を次に示します。

* アダプティブフォーム、HTML5 フォームまたはフォームセットの送信
* インタラクティブ通信の印刷または Web バージョンのレンディション
* あるファイル形式から別のファイル形式へのドキュメントの変換

トランザクションと見なされる項目の詳細については、 [課金対象 API](/help/forms/using/transaction-reports-billable-apis.md).

トランザクションの記録はデフォルトで無効になっています。 以下が可能です。 [トランザクションの記録を有効にする](/help/forms/using/viewing-and-understanding-transaction-reports.md#setting-up-transaction-reports) AEM Web コンソールから。 オーサーインスタンス、処理インスタンスまたはパブリッシュインスタンスのトランザクションレポートを表示できます。 すべてのトランザクションの集計合計について、作成者または処理インスタンスのトランザクションレポートを表示します。 パブリッシュインスタンスで発生したトランザクションレポートのうち、レポートの実行元のパブリッシュインスタンスでのみ発生したすべてのトランザクションの数を表示します。

同じAEMインスタンス上でコンテンツを作成（アダプティブフォーム、インタラクティブ通信、テーマ、その他のオーサリングアクティビティを作成）したり、ドキュメントを処理（ワークフロー、ドキュメントサービス、その他の処理アクティビティを使用）したりしないでください。 コンテンツの作成に使用するAEM Formsサーバーでは、トランザクションの記録を無効にしておきます。 ドキュメントの処理に使用するAEM Formsサーバーに対して、トランザクションの記録を有効にしておきます。

![sample-transaction-report-author-1](assets/sample-transaction-report-author-1.png)

トランザクションは、指定した期間（フラッシュバッファ時間+リバースレプリケーション時間）、バッファに残ります。 デフォルトでは、トランザクション数がトランザクションレポートに反映されるまで、約 90 秒かかります。

PDFフォームの送信、エージェント UI によるインタラクティブ通信のプレビュー、非標準のフォーム送信方法によるアクションは、トランザクションとしては考慮されません。 AEM Formsは、このようなトランザクションを記録する API を提供します。 カスタム実装から API を呼び出して、トランザクションを記録します。

## サポートされるトポロジ {#supported-topology}

トランザクションレポートは、OSGi 環境のAEM Formsでのみ使用できます。 author-publish、author-processing-publish のほか、トポロジの処理のみがサポートされます。 トポロジの例については、 [AEM Formsのアーキテクチャとデプロイメントトポロジ](/help/forms/using/transaction-reports-overview.md).

トランザクション数は、パブリッシュインスタンスからオーサーインスタンスまたは処理インスタンスにリバースレプリケートされます。 参考となるオーサーとパブリッシュのトポロジを次に示します。

![simple-author-publish-topology](assets/simple-author-publish-topology.png)

>[!NOTE]
>
>AEM Formsトランザクションレポートは、パブリッシュインスタンスのみを含むトポロジをサポートしていません。

### トランザクションレポートの使用に関するガイドライン {#guidelines-for-using-transaction-reports}

* オーサーインスタンスのレポートにはオーサリングアクティビティ中に登録されたトランザクションが含まれるので、すべてのオーサーインスタンスのトランザクションレポートを無効にします。
* を有効にします。 **公開のトランザクションのみを表示** オプションを使用して、すべてのパブリッシュインスタンスの累積トランザクションを表示できます。 また、特定のパブリッシュインスタンス上の実際のトランザクションに関するトランザクションレポートは、各パブリッシュインスタンス上でのみ表示することもできます。
* オーサーインスタンスを使用してワークフローを実行し、ドキュメントを処理しないでください。
* トランザクションレポートを使用する前に、パブリッシュサーバーとトポロジを使用する場合は、すべてのパブリッシュインスタンスでリバースレプリケーションが有効になっていることを確認してください。
* トランザクションデータは、パブリッシュインスタンスから、対応するオーサーまたは処理インスタンスにのみリバースレプリケーションされます。 オーサーインスタンスまたは処理インスタンスは、別のインスタンスにデータをレプリケートできません。 例えば、author-processing-publish トポロジがある場合、集計トランザクションデータは処理インスタンスにのみレプリケートされます。

## 関連記事 {#related-articles}

* [取引レポートの表示と理解](/help/forms/using/viewing-and-understanding-transaction-reports.md)
* [トランザクションレポート請求可能 API](/help/forms/using/transaction-reports-billable-apis.md)
* [カスタム実装のトランザクションの記録](/help/forms/using/record-transaction-custom-implementation.md)

