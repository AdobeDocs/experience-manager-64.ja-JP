---
title: トランザクションレポートの概要
seo-title: Transaction Reports Overview
description: 送信されたすべてのフォーム、インタラクティブな通信のレンダリング、別の形式に変換されたドキュメントなどの数を保持します
seo-description: Keep a count of all the forms submitted, interactive communication rendered, Documents converted to one format to another, and more
uuid: b40220e6-88c8-4507-b228-6c57d9b54422
contentOwner: khsingh
products: SG_EXPERIENCEMANAGER/6.4/FORMS
topic-tags: forms-manager
discoiquuid: 1fb11e02-d8f1-41a0-8e23-cb890b4e2244
exl-id: a545aa0a-9d71-48ba-ba3e-ed30a7e34f3d
source-git-commit: c5b816d74c6f02f85476d16868844f39b4c47996
workflow-type: tm+mt
source-wordcount: '606'
ht-degree: 95%

---

# トランザクションレポートの概要 {#transaction-reports-overview}

>[!CAUTION]
>
>AEM 6.4 の拡張サポートは終了し、このドキュメントは更新されなくなりました。 詳細は、 [技術サポート期間](https://helpx.adobe.com/jp/support/programs/eol-matrix.html). サポートされているバージョンを見つける [ここ](https://experienceleague.adobe.com/docs/?lang=ja).

送信されたすべてのフォーム、インタラクティブな通信のレンダリング、別の形式に変換されたドキュメントなどの数を保持します

## はじめに {#introduction}

AEM Forms のトランザクションレポートを使用すると、AEM Forms のデプロイメントで指定した日以降に発生したすべてのトランザクション数を保持できます。目的は、製品の使用状況に関する情報を提供し、ビジネスの関係者がデジタル処理量を理解できるようにすることです。トランザクションの例を次に示します。

* アダプティブフォーム、HTML5 フォームまたはフォームセットの送信
* インタラクティブ通信の印刷または web バージョンのレンディション
* あるファイル形式から別のファイル形式へのドキュメントの変換

トランザクションと見なされる項目の詳細については、[課金対象 API](/help/forms/using/transaction-reports-billable-apis.md) を参照してください。

トランザクションの記録はデフォルトで無効になっています。AEM web コンソールから[トランザクションの記録を有効](/help/forms/using/viewing-and-understanding-transaction-reports.md#setting-up-transaction-reports)にすることができます。オーサーインスタンス、処理インスタンスまたはパブリッシュインスタンスのトランザクションレポートを表示できます。すべてのトランザクションの集計合計に対して、作成者または処理インスタンスのトランザクションレポートを表示します。パブリッシュインスタンスで発生したトランザクションレポートのうち、レポートの実行元のパブリッシュインスタンスでのみ発生したすべてのトランザクション数を表示します。

同じ AEM インスタンス上でコンテンツを作成（アダプティブフォーム、インタラクティブ通信、テーマ、その他のオーサリングアクティビティを作成）したり、ドキュメントを処理（ワークフロー、ドキュメントサービス、その他の処理アクティビティを使用）したりしないでください。コンテンツの作成に使用する AEM Forms サーバーでは、トランザクションの記録を無効にしておきます。ドキュメントの処理に使用する AEM Forms サーバーに対して、トランザクションの記録を有効にしておきます。

![sample-transaction-report-author-1](assets/sample-transaction-report-author-1.png)

トランザクションは、指定した期間（フラッシュバッファ時間 + リバースレプリケーション時間）、バッファに残ります。デフォルトでは、トランザクション数がトランザクションレポートに反映されるまで、約 90 秒かかります。

PDF フォームの送信、エージェント UI によるインタラクティブ通信のプレビュー、非標準のフォーム送信方法の使用などのアクションは、トランザクションとしては考慮されません。AEM Forms は、このようなトランザクションを記録する API を提供します。カスタム実装から API を呼び出して、トランザクションを記録します。

## サポートされるトポロジ {#supported-topology}

トランザクションレポートは、OSGi 環境の AEM Forms でのみ使用できます。author-publish、author-processing-publish のほか、トポロジの処理のみがサポートされます。トポロジについて詳しくは、[AEM Forms のアーキテクチャとデプロイメントトポロジ](/help/forms/using/transaction-reports-overview.md)を参照してください。

トランザクション数は、パブリッシュインスタンスからオーサーインスタンスまたは処理インスタンスにリバースレプリケートされます。指標となるオーサーとパブリッシュのトポロジを次に示します。

![simple-author-publish-topology](assets/simple-author-publish-topology.png)

>[!NOTE]
>
>AEM Forms トランザクションレポートは、パブリッシュインスタンスのみを含むトポロジをサポートしていません。

### トランザクションレポートの使用に関するガイドライン {#guidelines-for-using-transaction-reports}

* オーサーインスタンスのレポートにはオーサリングアクティビティ中に登録されたトランザクションが含まれるため、すべてのオーサーインスタンスのトランザクションレポートを無効にします。
* オーサーインスタンスで **パブリッシュのトランザクションのみを表示**&#x200B;オプションを有効にして、すべてのパブリッシュインスタンスの累積トランザクションを表示します。また、特定のパブリッシュインスタンス上のみの実際のトランザクションに関するトランザクションレポートは、各パブリッシュインスタンス上で表示することもできます。
* オーサーインスタンスを、ワークフローの実行とドキュメントの処理のために使用しないでください。
* パブリッシュサーバーにトポロジがある場合は、トランザクションレポートを使用する前に、すべてのパブリッシュインスタンスでリバースレプリケーションが有効になっていることを確認してください。
* トランザクションデータは、パブリッシュインスタンスから、対応するオーサーインスタンスまたは処理インスタンスにのみリバースレプリケーションされます。オーサーインスタンスまたは処理インスタンスは、データを別のインスタンスにレプリケートできません。例えば、author-processing-publish トポロジがある場合、集計トランザクションデータは処理インスタンスにのみレプリケートされます。

## 関連記事 {#related-articles}

* [トランザクションレポートの表示と理解](/help/forms/using/viewing-and-understanding-transaction-reports.md)
* [トランザクションレポート請求可能 API](/help/forms/using/transaction-reports-billable-apis.md)
* [カスタム実装のトランザクションの記録](/help/forms/using/record-transaction-custom-implementation.md)
