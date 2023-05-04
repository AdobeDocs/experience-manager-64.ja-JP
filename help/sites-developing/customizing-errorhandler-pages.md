---
title: エラーハンドラーによって表示されるページのカスタマイズ
seo-title: Customizing Pages shown by the Error Handler
description: AEMには、HTTP エラーを処理するための標準的なエラーハンドラーが付属しています
seo-description: AEM comes with a standard error handler for handling HTTP errors
uuid: aaf940fd-e428-4c7c-af7f-88b1d02c17c6
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.4/SITES
topic-tags: platform
content-type: reference
discoiquuid: 63c94c82-ed96-4d10-b645-227fa3c09f4b
exl-id: f71b16a9-a233-4129-bbf2-257ded88be25
source-git-commit: c5b816d74c6f02f85476d16868844f39b4c47996
workflow-type: tm+mt
source-wordcount: '554'
ht-degree: 66%

---

# エラーハンドラーによって表示されるページのカスタマイズ{#customizing-pages-shown-by-the-error-handler}

>[!CAUTION]
>
>AEM 6.4 の拡張サポートは終了し、このドキュメントは更新されなくなりました。 詳細は、 [技術サポート期間](https://helpx.adobe.com/jp/support/programs/eol-matrix.html). サポートされているバージョンを見つける [ここ](https://experienceleague.adobe.com/docs/?lang=ja).

AEM には、HTTP エラーを処理するための標準的なエラーハンドラーが付属しています。例えば、次のようなメッセージが表示されます。

![chlimage_1-67](assets/chlimage_1-67.png)

エラーコードに応答するシステム提供のスクリプトが（`/libs/sling/servlet/errorhandler` の下に）あります。標準の CQ インスタンスでは、デフォルトで次のスクリプトを使用できます。

* 403.jsp
* 404.jsp

>[!NOTE]
>
>AEM は Apache Sling に基づいています。Sling エラー処理について詳しくは、[https://sling.apache.org/site/errorhandling.html](https://sling.apache.org/site/errorhandling.html) を参照してください。

>[!NOTE]
>
>オーサーインスタンスで、 [CQ WCM Debug Filter](/help/sites-deploying/osgi-configuration-settings.md) はデフォルトで有効になっています。 これにより、常に応答コード 200 が生成されます。 デフォルトのエラーハンドラーは、応答に完全なスタックトレースを書き込むことで応答します。
>
>パブリッシュインスタンスでは、CQ WCM Debug Filter は、有効として設定されている場合も含めて&#x200B;*常に*&#x200B;無効になります。

## エラーハンドラーによって表示されるページをカスタマイズする方法 {#how-to-customize-pages-shown-by-the-error-handler}

独自のスクリプトを作成して、エラーの発生時にエラーハンドラーで表示されるページをカスタマイズできます。カスタマイズしたページが `/apps` の下に作成され、デフォルトのページ（`/libs` の下）をオーバーレイします。

>[!NOTE]
>
>詳しくは、 [オーバーレイの使用](/help/sites-developing/overlays.md) を参照してください。

1. リポジトリー内で、デフォルトスクリプトを次のようにコピーします。

   * コピー元：`/libs/sling/servlet/errorhandler/`
   * コピー先：`/apps/sling/servlet/errorhandler/`

   コピー先のパスはデフォルトでは存在しないので、最初は作成する必要があります。

1. `/apps/sling/servlet/errorhandler` に移動します。次のどちらかを実行します。

   * 該当する既存のスクリプトを編集し、必要な情報を追加します。
   * 必要なコードの新しいスクリプトを作成および編集します。

1. 変更を保存し、テストします。

>[!CAUTION]
>
>404.jsp および 403.jsp ハンドラーは、CQ5 認証に対応するように特別に設計されています。特に、これらのエラーが発生した場合にシステムログインを許可する場合。
>
>したがって、これら 2 つのハンドラーの交換は慎重に行う必要があります。

### HTTP 500 エラーへの応答のカスタマイズ {#customizing-the-response-to-http-errors}

HTTP 500 エラーはサーバー側の例外によって発生します。

* **[500 内部サーバーエラー](https://www.w3.org/Protocols/rfc2616/rfc2616-sec10.html)**
サーバーで予期しない状況が発生したので、要求を処理できません。

リクエストの処理で例外が発生した場合、Apache Sling フレームワーク（AEM の基盤）は次の処理を実行します。

* 例外をログに記録します。
* 戻り値：

   * HTTP 応答コード 500
   * 例外スタックトレース

   応答の本文に含まれます。

[エラーハンドラーで表示されるページをカスタマイズする](#how-to-customize-pages-shown-by-the-error-handler)ことで、`500.jsp` スクリプトを作成できます。ただし、このスクリプトが使用されるのは、`HttpServletResponse.sendError(500)` が明示的に（例外キャッチャーから）実行される場合に限ります。

それ以外の場合は、応答コードは 500 に設定されますが、`500.jsp` スクリプトは実行されません。

500 エラーを処理するには、エラーハンドラースクリプトのファイル名を例外クラス（またはスーパークラス）と同じにする必要があります。このような例外をすべて処理するには、スクリプト `/apps/sling/servlet/errorhandler/Throwable.js`p または `/apps/sling/servlet/errorhandler/Exception.jsp` を作成します。

>[!CAUTION]
>
>オーサーインスタンスで、 [CQ WCM Debug Filter](/help/sites-deploying/osgi-configuration-settings.md) はデフォルトで有効になっています。 これにより、常に応答コード 200 が生成されます。 デフォルトのエラーハンドラーは、応答に完全なスタックトレースを書き込むことで応答します。
>
>カスタムエラーハンドラーの場合、コード 500 を含む応答が必要です。そのため、[CQ WCM Debug Filter を無効にする必要があります](/help/sites-deploying/osgi-configuration-settings.md)。そうすることで、応答コード 500 が返され、それによって正しい Sling エラーハンドラーがトリガーされます。
>
>パブリッシュインスタンスでは、CQ WCM Debug Filter は、有効として設定されている場合も含めて&#x200B;*常に*&#x200B;無効になります。
