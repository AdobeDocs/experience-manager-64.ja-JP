---
title: フォームとドキュメントの公開と非公開
seo-title: Publishing and unpublishing forms and documents
description: フォームの公開と非公開をスケジュールできます。公開されたフォームはパブリッシュインスタンスに複製されます。
seo-description: You can schedule publishing and unpublishing of forms. Published forms are replicated on the publish instance.
uuid: 4de958f8-46d0-4356-ab88-70fa3d480216
content-type: reference
products: SG_EXPERIENCEMANAGER/6.4/FORMS
topic-tags: publish
content-strategy: max-2018
discoiquuid: 7dd08e81-5df6-4522-9f8c-48b4bba8927b
exl-id: 1afef311-c1e6-48ec-ae23-dbd553a99ac6
source-git-commit: c5b816d74c6f02f85476d16868844f39b4c47996
workflow-type: tm+mt
source-wordcount: '1449'
ht-degree: 77%

---

# フォームとドキュメントの公開と非公開 {#publishing-and-unpublishing-forms-and-documents}

>[!CAUTION]
>
>AEM 6.4 の拡張サポートは終了し、このドキュメントは更新されなくなりました。 詳細は、 [技術サポート期間](https://helpx.adobe.com/jp/support/programs/eol-matrix.html). サポートされているバージョンを見つける [ここ](https://experienceleague.adobe.com/docs/?lang=ja).

AEM Forms では、フォームを簡単に作成し、公開したり非公開にしたりできます。AEM Formsについて詳しくは、 [フォーム管理の概要](/help/forms/using/introduction-managing-forms.md).

AEM Forms サーバーは 2 つのインスタンス（オーサーとパブリッシュ）を提供します。オーサーインスタンスは、フォームのアセットとリソースを作成し管理するためのものです。パブリッシュインスタンスは、エンドユーザーが使用できるアセットと関連リソースを保持するためのものです。 XDP およびPDF formsは、オーサーモードで読み込むことができます。 詳しくは、[AEM Forms での XDP および PDF ドキュメントの取得](/help/forms/using/get-xdp-pdf-documents-aem.md)を参照してください。

## サポートしているアセット {#supported-assets-nbsp}

AEM Forms では、次のアセットタイプをサポートしています。

* アダプティブフォーム
* アダプティブドキュメント
* アダプティブフォームフラグメント
* テーマ
* フォームテンプレート（XFA フォーム）
* PDF のフォーム
* ドキュメント ( フラットPDFドキュメント )
* フォームセット
* リソース（画像、スキーマ、スタイルシート）

最初は、すべてのアセットがオーサーインスタンスでのみ使用可能です。 管理者またはフォーム作成者は、リソースを除くすべてのアセットを公開できます。

フォームを選択して公開すると、関連のアセットとリソースも公開されます。ただし、依存アセットは公開されません。このコンテキストでは、関連のアセットやリソースは、公開済みアセットが使用または参照するアセットです。依存アセットは、公開済みアセットを参照するアセットです。

アダプティブフォームには、自動的に公開されない構成、設定、カスタマイズが含まれる場合があります。アダプティブフォームを発行する前に、これらのリソースを発行またはアクティブ化することをお勧めします。

* 編集可能なアダプティブフォームテンプレート
* Acrobat Sign、Typekit、reCAPTCHA、およびフォームデータモデルのCloud Service設定
* その他のクラウドサービスの設定は、ユーザーが管理者権限を保有している場合にのみアクティブ化されます。
* カスタマイズ. 以下のようなものが含まれます。

   * カスタムレイアウト
   * カスタム外観
   * CSS ファイル - アダプティブフォームのコンテナプロパティダイアログで入力値として使用
   * クライアントライブラリカテゴリ - アダプティブフォームのコンテナプロパティダイアログで入力値として使用
   * アダプティブフォームテンプレートの一部として含まれる可能性のあるその他のクライアントライブラリ
   * デザインパス

## アセットの状態 {#asset-states}

アセットは次のステータスを持つことができます。

* **非公開**：一度も公開されていないアセット（未公開状態は、フォームアセットのみに適用されます。Correspondence Management アセットには、非公開状態がありません）。
* **公開済み**：公開済みアセット。パブリッシュインスタンスで使用できます。
* **変更済み**： 公開後に変更されたアセット。

## アセットの公開 {#publish-an-asset}

1. AEM Forms サーバーにログインします。
1. 次のいずれかの手順を使って、アセットを選択して公開します。

   1. ポインターをアセットの上に置き、「**[!UICONTROL 公開]** ![aem6forms_globe](assets/aem6forms_globe.pngasset.png)」をタップします。
   1. 次のいずれかを実行し、「公開」をタップします。

      * カード表示になっている場合は、「**[!UICONTROL 選択を入力]** ![aem6forms_check-circle](assets/aem6forms_check-circle.png)」をタップし、アセットをタップします。アセットが選択されます。
      * リスト表示の場合は、アセットのチェックボックスを選択します。 アセットが選択されます。
      * 詳細を表示するアセットを表示します。
      * 「プロパティを表示 ![viewproperties](assets/viewproperties.png)」をタップしてアセットのプロパティを表示します。

      >[!NOTE]
      >
      >複数のアセットを選択しないでください。複数のアセットを一度に公開することはサポートされていません。


1. 公開プロセスが始まるときに、確認ダイアログが表示され、関連するすべてのアセットとリソースが表示されます。関連アセットを含むダイアログボックスで、「**[!UICONTROL 公開]**」をタップします。アセットが公開され、「アセット公開成功」ダイアログが表示されます。

   >[!NOTE]
   >
   >アダプティブフォームの場合、関連アセットと一緒に、アダプティブフォームページ名も表示されます。

   ![関連するすべてのアセットとリソースが表示されている確認ダイアログ](assets/p4.png)

   関連するすべてのアセットとリソースが表示されている確認ダイアログ。

   >[!NOTE]
   >
   >Forms Manager を使用する場合で、ユーザーが表示されているアセットを公開する権限を持っていないときは、公開アクションは無効化されます。特別な権限を必要とするアセットは、赤色で表示されます。

   アセットが公開されると、そのアセットのメタデータプロパティがパブリッシュインスタンスにコピーされ、アセットのステータスが公開済みに変更されます。公開される依存アセットのステータスも公開済みに変更されます。

   アセットを公開した後、 Forms Portal を使用して、Web ページにすべてのアセットを表示できます。 詳しくは、 [ポータル上のフォーム発行の概要](/help/forms/using/introduction-publishing-forms.md).

## すべての Correspondence Management アセットの公開 {#publish-all-the-correspondence-management-assets}

AEM Forms では、サーバー上のすべての Correspondence Management アセットを 1 度で公開します。公開済みのアセットには、すべての Correspondence Management アセットと関連する依存性が含まれます。

サーバー上のすべての Correspondence Management アセットを公開するには、次の手順を実行します。

1. AEM Forms サーバーにログインします。
1. グローバルナビゲーションバーで「**Adobe Experience Manager**」をタップします。
1. タップ ![tools-1](assets/tools-1.png)次に、 **Forms**.
1. 「**Correspondence Management アセットを公開する**」をタップします。

   ![publish-cmp-assets-1](assets/publish-cmp-assets-1.png)

   「すべての Correspondence Management アセットを公開する」ページが表示され、前回の Correspondence Management アセットの公開処理についての情報が示されます。

   ![publish-last-run-details](assets/publish-last-run-details.png)

1. 「**公開**」をタップし、確認メッセージで「**OK**」をタップします。

   バッチ処理が完了したら、最後の実行の詳細を表示できます。 これには管理者ログインや、バッチの実行が成功したか失敗したかなどの情報が含まれます。

   >[!NOTE]
   >
   >公開処理は、一度開始するとキャンセルすることはできません。また、公開処理の進行中は、アセットの作成、削除、修正、公開や、「すべての Correspondence Management アセットを書き出し」を開始しないでください。

## フォームとドキュメントの公開と非公開の自動化 {#automate-publishing-and-unpublishing-for-forms-amp-documents}

AEM Forms では、フォームとドキュメントでアセットの公開と非公開をスケジュールできます。スケジュールはメタデータエディターで指定できます。フォームメタデータの管理について詳しくは、[フォームメタデータの管理](/help/forms/using/manage-form-metadata.md)を参照してください。

以下の手順に従って、フォームとドキュメントのアセットを公開および非公開する日時をスケジュールします。

1. アセットを選択し、「**[!UICONTROL プロパティの表示]**」をタップします。メタデータプロパティページが開きます。
1. メタデータプロパティページで、「**[!UICONTROL 詳細]**」をタップし、「**[!UICONTROL 編集]** ![illustratorcc_penciltool_cur_edit_2_17](assets/illustratorcc_penciltool_cur_edit_2_17.png)」をタップします。
1. 「**[!UICONTROL オンタイムに公開]**」フィールドと「**[!UICONTROL オフタイムに公開]**」フィールドで、日時を選択します。

   「**[!UICONTROL 完了]** ![aem6forms_check](assets/aem6forms_check.png)」をタップします。

## アセットの非公開 {#unpublish-an-asset}

1. 公開されるアセットを選択し、「**[!UICONTROL 非公開]** ![非公開](assets/unpublish.png)」をタップします。
1. 次のいずれかの手順を使用して、アセットを選択し非公開にします。

   1. ポインターをアセットの上に置き、「**[!UICONTROL 非公開]** ![非公開](assets/unpublish.png)」をタップします。
   1. 次のいずれかを行い、「非公開」をタップします。

      * カード表示になっている場合は、「**[!UICONTROL 選択を入力]** ![aem6forms_check-circle](assets/aem6forms_check-circle.png)」をタップし、アセットをタップします。アセットが選択されます。
      * リスト表示になっている場合は、マウスをアセットに移動して ![selectassetcheckmark](assets/selectassetcheckmark.png) をタップします。アセットが選択されます。
      * 詳細を表示するアセットを表示します。
      * 「プロパティを表示 ![viewproperties](assets/viewproperties.png)」をタップしてアセットのプロパティを表示します。

1. 非公開プロセスが始まるときに、確認ダイアログが表示されます。「**[!UICONTROL 非公開]**」をタップします。

   >[!NOTE]
   >
   >選択されているアセットだけが非公開になり、子アセットと参照されているアセットは非公開にはなりません。

## アセットまたはレターを以前の公開済みバージョンに戻す {#revert-an-asset-or-letter-to-the-previously-published-version}

アセットまたはレターを編集して公開するたびに、アセットまたはレターのバージョンが作成されます。アセットまたはレターを、以前に公開したバージョンに戻すことができます。アセットまたはドキュメントの現在のバージョンで問題が発生した場合は、問題の解決が必要になる場合があります。

>[!NOTE]
>
>公開済みのレターで使用されている依存アセットがシステムから削除されている場合、そのレターを最後に公開した状態に戻さないでください。

1. アセットを選択し、「**[!UICONTROL 以前に公開したバージョンに戻す]** ![reverttopreviouslypublishedversion](assets/reverttopreviouslypublishedversion.png)」をタップします。
1. アセットが戻される前に、確認ダイアログが表示されます。「**[!UICONTROL 元に戻す]**」をタップします。

   アセットまたはレターが、以前に公開したバージョンにロールバックされます。

## アセットの削除 {#delete-an-asset}

>[!NOTE]
>
>アセットを削除すると、そのアセットはパブリッシュインスタンスから削除されます。 アセットを削除すると、ベースバージョンを除くバージョン履歴も削除されます。

1. アセットを選択し、「**[!UICONTROL 削除]** ![削除](assets/delete.png)」をタップします。

   >[!NOTE]
   >
   >「削除」オプションは、アセットをタップしてアセットの詳細を表示する場合や、「プロパティを表示 ![viewproperties](assets/viewproperties.png)」をタップしてアセットのプロパティを表示する場合にも使用できます。

1. アセットを削除する前に、確認ダイアログが表示されます。「**[!UICONTROL 削除]**」をタップします。

   >[!NOTE]
   >
   >選択されているアセットだけが削除され、従属アセットは削除されません。アセットの参照を確認するには、 ![参照](assets/references.png) をタップしてからアセットを選択します。
   >
   >削除しようとしているアセットが別のアセットの子アセットの場合、そのアセットは削除されません。 このようなアセットを削除するには、他のアセットからこのアセットの参照を削除してから、再試行してください。

## 保護されたアダプティブフォーム {#protected-adaptive-forms}

選択したユーザーがアクセスできるフォームの認証を有効にすることができます。 フォームの認証を有効にすると、ユーザーはアクセス前にログイン画面を表示します。 フォームにアクセスできるのは、認証済みの資格情報を持つユーザーだけです。

フォームの認証を有効にするには：

1. ブラウザーで、パブリッシュインスタンスの configMgr を開きます。

   URL：`https://<hostname>:<PublishPort>/system/console/configMgr`

1. Adobe Experience Manager Web Console Configuration で、「**Apache Sling Authentication Service**」をクリックして設定します。
1. 表示された Apache Sling Authentication Service ダイアログで、「**+**」ボタンを使用してパスを追加します。

   パスを追加すると、そのパスのフォームに対して認証サービスが有効になります。
