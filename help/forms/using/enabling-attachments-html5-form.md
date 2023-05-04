---
title: HTML5フォームの添付ファイルの有効化
seo-title: Enabling attachments for an HTML5 form
description: デフォルトでは、添付ファイルのサポートはHTML5 フォームで無効になっています。
seo-description: By default, the attachment support for HTML5 forms is disabled.
uuid: 2c62ac3e-4b27-46c7-a61d-a805fb5d26fb
content-type: reference
products: SG_EXPERIENCEMANAGER/6.4/FORMS
topic-tags: hTML5_forms
discoiquuid: 8eebfcd6-0597-44ed-b718-bf9a1baa6c12
feature: Mobile Forms
exl-id: 82a843c4-5cb2-4f5e-ad4d-cf2e9ea6cdb8
source-git-commit: c5b816d74c6f02f85476d16868844f39b4c47996
workflow-type: tm+mt
source-wordcount: '355'
ht-degree: 42%

---

# HTML5フォームの添付ファイルの有効化 {#enabling-attachments-for-an-html-form}

>[!CAUTION]
>
>AEM 6.4 の拡張サポートは終了し、このドキュメントは更新されなくなりました。 詳細は、 [技術サポート期間](https://helpx.adobe.com/jp/support/programs/eol-matrix.html). サポートされているバージョンを見つける [ここ](https://experienceleague.adobe.com/docs/?lang=ja).

添付ファイルは、HTML5 フォームを使用してアップロード、プレビュー、送信することができます。 デフォルトでは、添付ファイルのサポートは無効になっています。 添付ファイルサポートを有効にするには：

1. の作成 [カスタムプロファイル](/help/forms/using/custom-profile.md) 複数選択文字列プロパティを使用 `mfAttachmentOptions`.
1. カスタムプロファイルで、プロパティを指定します。 `fileSizeLimit`, `multiSelect`、および `buttonTex`ファイル添付ウィジェットのオプションを設定するには、t を使用します。 必要に応じて、追加のカスタムプロパティを指定することもできます。

1. カスタムプロファイルでは、次の設定を使用します。

   * **multiSelect** -> true または false （デフォルトは true）
   * **fileSizeLimit** -> value_in_mb (say 5) （デフォルトで 2 MB）
   * **buttonText** -> ポップアップウィンドウのボタンのテキスト（デフォルトでは「添付」）
   * **承諾** -> 受け入れるファイルタイプ（デフォルトでは&quot;audio/&amp;ast;, video/&amp;ast;, image/&amp;ast;, text/&amp;ast;, .pdf&quot;）

   >[!NOTE]
   >
   >Microsoft Internet Explorer 9 では、ユーザーは指定された制限を超えるファイルを添付できます。 これは既知の問題です。

1. [メタデータエディター](/help/forms/using/manage-form-metadata.md)を使用して、上記で HTML5 のフォームのために作成したカスタムプロファイルを選択します。
1. カスタムプロファイルを使用してフォームテンプレートをレンダリングすると、添付ファイルアイコンがフォームツールバーに表示されます。

   >[!NOTE]
   >
   >デフォルトでは、フォームポータルは、「ドラフトと添付ファイル」機能が有効なカスタムプロファイルを提供します。 **ドラフトとして保存**&#x200B;プロファイルに関する詳細は、[HTML5 フォームをドラフトとして保存](/help/forms/using/saving-html5-form-draft.md)を参照してください。

1. 添付ファイルアイコンをクリックすると、添付ファイル選択ダイアログボックスが表示されます。ファイルを参照して添付ファイルを選択して&#x200B;**「添付」**&#x200B;をクリックします。

   >[!NOTE]
   >
   >添付ファイルをプレビューするには、添付ファイル名をクリックします。

   >[!NOTE]
   >
   >匿名のユーザーは、ファイルプレビューオプションを使用できません。

## 添付ファイルの送信形式 {#attachment-submission-format}

添付ファイルが有効な場合、HTML5 フォームはマルチパートデータを送信します。 マルチパート形式で送信するデータには&#x200B;**dataXml**&#x200B;および&#x200B;**添付ファイル**&#x200B;の2つの部分があります。

>[!NOTE]
>
>下位互換性については、`mfAllowAttachments` オプションがオフになっている場合、HTML5 フォームはマルチパート形式のデータを送信しません。**application/xml**&#x200B;形式の単純なデータ xml を送信します。

mfAllowAttachments フラグがオンになっている場合、[送信サービスのプロキシサービス](/help/forms/using/service-proxy.md)もまたマルチパート形式のデータを dataXml と添付ファイルと共に投稿します。
