---
title: デプロイメントのライセンスの種類の更新
seo-title: Update the license type for the deployment
description: 管理コンソールのライセンスを変更ページを使用して、デプロイメントのライセンスの種類を更新します。
seo-description: Update the license type for the deployment by using the Change License page in administration console.
uuid: 0152635e-2c00-4944-b9b6-64b368589a91
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/get_started_with_administering_aem_forms_on_jee
products: SG_EXPERIENCEMANAGER/6.4/FORMS
discoiquuid: e4f31377-ccc9-4986-a3bf-ef2e83d12448
exl-id: 07671470-59dd-4290-be9a-465fcd89ac2d
source-git-commit: c5b816d74c6f02f85476d16868844f39b4c47996
workflow-type: tm+mt
source-wordcount: '306'
ht-degree: 14%

---

# デプロイメントのライセンスの種類の更新 {#update-the-license-type-for-the-deployment}

>[!CAUTION]
>
>AEM 6.4 の拡張サポートは終了し、このドキュメントは更新されなくなりました。 詳細は、 [技術サポート期間](https://helpx.adobe.com/jp/support/programs/eol-matrix.html). サポートされているバージョンを見つける [ここ](https://experienceleague.adobe.com/docs/?lang=ja).

AEM forms のインストールプロセスの一環として、Configuration Manager を使用し、必要なAEM forms モジュールの設定とデプロイを行いました。 デフォルトでは、これらのモジュールには 60 日間の評価版ライセンスが設定されています。 デプロイメントのライセンスの種類を変更するには、管理コンソールのライセンスを変更ページを使用します。 現在デプロイされているモジュールが [ ライセンスの変更 ] ページに表示されます。

[ ライセンスの変更 ] ページには、ライセンスに関する情報が表示されます。

* 現在のライセンスの種類
* ライセンスが最後に更新された日時
* 前回の更新を実行したユーザー
* ライセンスの現在のステータス
* AEM forms がインストールされた日付
* 現在のライセンスの有効期限

>[!NOTE]
>
>ライセンスの変更は、展開されているすべてのモジュールに適用されます。 ライセンスの種類を変更する前に、ライセンスを持たないモジュールのデプロイを解除します。 デプロイ済みモジュールのリストに、Adobeから購入したモジュール以外のモジュールが含まれている場合は、実稼動ライセンスの種類を選択しないでください。

## ライセンスの種類を更新する {#update-the-license-type}

1. 管理コンソールで、「ライセンス」をクリックします。
1. AEM forms のエンドユーザー使用許諾契約書を読み、使用許諾契約書の条項に同意する場合は「同意します」を選択し、「次へ」をクリックします。
1. [ ライセンスの変更 ] ページで、ライセンスの種類を選択します。

   * **EVAL:** 60 日間の評価版ライセンス
   * **DEV：**&#x200B;無期限の開発ライセンス
   * **NFR:** 2 年間の評価版ライセンス
   * **IDEV:** Adobe Developer Program の 1 年間の購読
   * **実稼働：**&#x200B;無期限のライセンス

1. [ はい、ライセンスの変更はすべての展開済みモジュールで有効です ] を選択します。
1. 「ライセンスの変更を確認」をクリックします。 ライセンスが正常に更新されたことを示すメッセージが表示されます。
