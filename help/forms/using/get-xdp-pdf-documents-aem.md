---
title: AEM Forms での XDP および PDF ドキュメントの取得
seo-title: Getting XDP and PDF documents in AEM Forms
description: AEM Forms では、フォームやサポートされているアセットをアップロードし、アダプティブフォームで使用できます。複数のフォームや関連リソースを一括して ZIP としてアップロードすることもできます。
seo-description: AEM Forms allows you to upload forms and supported assets to use with adaptive forms. You can also bulk upload forms and related resources as a ZIP.
uuid: c2a86d89-0c56-4d29-932a-dd09277fa7cb
content-type: reference
products: SG_EXPERIENCEMANAGER/6.4/FORMS
topic-tags: forms-manager
discoiquuid: 99da0d37-726e-42b9-b98a-5dd6c2165af6
role: Admin
exl-id: 50bf178d-7a3c-41df-9d13-99c74d944700
source-git-commit: 3c050c33a384d586d74bd641f7622989dc1d6b22
workflow-type: tm+mt
source-wordcount: '667'
ht-degree: 100%

---

# AEM Forms での XDP および PDF ドキュメントの取得 {#getting-xdp-and-pdf-documents-in-aem-forms}

## 概要 {#overview}

AEM Forms でアップロードすることで、ローカルファイルシステムのフォームを CRX リポジトリに読み込むことができます。アップロード操作は、次のアセットタイプに対してサポートされています。

* フォームテンプレート（XFA フォーム）
* PDF のフォーム
* ドキュメント（非インタラクティブ PDF ドキュメント）

サポートされているアセットタイプを個別にまたは ZIP アーカイブとしてアップロードできます。`Resource` タイプのアセットは、XFA フォームと一緒に ZIP アーカイブでのみアップロードできます。

>[!NOTE]
>
>XDP ファイルをアップロードすることができる `form-power-users` グループのメンバーであることを確認してください。このグループのメンバーになるには、管理者に連絡します。

## フォームのアップロード {#uploading-forms}

1. `https://[server]:[port]/aem/forms.html` にアクセスして AEM Forms ユーザーインターフェイスにログインします。
1. フォームまたはフォームを含むフォルダーをアップロードしたいフォルダーに移動します。
1. アクションツールバーで、**作成／ファイルのアップロード**&#x200B;をタップします。

   ![作成にあるローカルストレージのファイルオプション](assets/step.png)

1. フォームまたはパッケージをアップロードダイアログでは、アップロードするファイルを参照および選択できます。ファイルブラウザーには、サポートされているファイル形式（ZIP、XDP、および PDF）のみが表示されます。

   >[!NOTE]
   >
   >ファイル名には、英数字、ハイフン、下線のみを含めることができます。

1. ファイルを選択したら「アップロード」をクリックしてファイルをアップロードするか、「キャンセル」をクリックしてアップロードを中止します。追加されたアセットおよび現在場所にアップロードされたアセットの一覧がポップアップに表示されます。

   >[!NOTE]
   >
   >ZIP ファイルの場合は、サポートされているすべてのアセットの相対パスが表示されます。ZIP 内の未サポートアセットは無視され、一覧には表示されません。ただし、ZIP アーカイブに未サポートアセットのみが含まれている場合は、エラーメッセージが表示され、ポップアップダイアログは表示されません。

   ![XFA フォームのアップロード時のアップロードダイアログ](assets/upload-scr.png)

1. アセットに無効のファイル名がある場合は、エラーが表示されます。赤で強調表示されているファイル名を修正し、再びアップロードしてください。

   ![XFA フォームのアップロード時のエラーメッセージ](assets/upload-scr-err.png)

アップロードが完了すると、アセットのプレビューに基づいて、バックグラウンドワークフローが各アセットごとにサムネイルを生成します。新しいバージョンのアセットがアップロードされた場合は、既存のアセットに上書きされます。

### 保護モード {#protected-mode}

AEM Forms サーバーを使用することで、JavaScript コードを実行できます。悪質な JavaScript コードの場合、AEM Forms 環境に障害が発生する可能性があります。保護モードは、信頼済みのアセットおよび場所からのみ XDP ファイルを実行するように制限します。AEM Forms UI で使用可能なすべての XDP は、信頼済みのアセットと見なされます。

保護モードは、デフォルトではオンになっています。必要に応じて、保護モードを無効にすることができます。

1. 管理者として AEM Web コンソールにログインします。URL は `https://[server]:[port]/system/console/configMgr` です。
1. Mobile Forms の設定を編集用に開きます。
1. 「保護モード」オプションの選択を解除し、「**保存**」をクリックします。保護モードが無効になります。

## 参照先 XFA フォームの更新 {#updating-referenced-xfa-forms}

AEM Forms では、XFA フォームテンプレートは、アダプティブフォームまたは別の XFA フォームテンプレートによって参照されることができます。また、テンプレートはリソースまたは別の XFA テンプレートを参照することもできます。

XFA を参照しているアダプティブフォームは、そのフィールドが、XFA で使用できるフィールドによってバインディングされています。フォームテンプレートを更新すると、関連のアダプティブフォームは XFA との同期を試みます。詳細については、[アダプティブフォームと関連 XXFA との同期](/help/forms/using/synchronizing-adaptive-forms-xfa.md)を参照してください。

フォームテンプレートを削除すると、依存関係にあるアダプティブフォームまたはフォームテンプレートが破損されます。このようなアダプティブフォームは、dirty なフォームとして非公式に参照されている場合があります。AEM Forms ユーザーインターフェイスで、次の 2 つの方法で dirty フォームを見つけ出すことができます。

* アセットリスト内のアダプティブフォームサムネイルに警告アイコンが表示され、警告アイコンの上にポインターを置くと次のメッセージが表示されます。

   `Schema/Form Template for this adaptive form has been updated so please go to Authoring mode and rebase it with new version.`

![関連 XFA の更新後の非同期のアダプティブフォームの警告](assets/dirtyaf.png)

アダプティブフォームが dirty かどうかを示すフラグが保持されます。この情報は、フォームのメタデータと一緒にフォームプロパティページにあります。dirty アダプティブフォームの場合のみ、メタデータプロパティ `Model Refresh` は `Recommended` 値を表示します。

![アダプティブフォームが XFA モデルと非同期であることを示す](assets/model-refresh.png)
