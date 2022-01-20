---
title: HTML5フォームの添付ファイルの有効化
seo-title: Enabling attachments for an HTML5 form
description: デフォルトでは、HTML5フォームの添付ファイルサポートは無効になっています。
seo-description: By default, the attachment support for HTML5 forms is disabled.
uuid: 2c62ac3e-4b27-46c7-a61d-a805fb5d26fb
content-type: reference
products: SG_EXPERIENCEMANAGER/6.4/FORMS
topic-tags: hTML5_forms
discoiquuid: 8eebfcd6-0597-44ed-b718-bf9a1baa6c12
feature: Mobile Forms
exl-id: 82a843c4-5cb2-4f5e-ad4d-cf2e9ea6cdb8
source-git-commit: bd94d3949f0117aa3e1c9f0e84f7293a5d6b03b4
workflow-type: tm+mt
source-wordcount: '319'
ht-degree: 61%

---

# HTML5フォームの添付ファイルの有効化 {#enabling-attachments-for-an-html-form}

HTML5フォームでは、添付ファイルをアップロード、プレビューおよび送信することができます。デフォルトでは、添付ファイルサポートは無効になっています。添付ファイルサポートを有効にするには：

1. [ 文字列プロパティで](/help/forms/using/custom-profile.md)カスタムプロファイル`mfAttachmentOptions`を作成します。
1. カスタムプロファイルで、プロパティを指定します。 `fileSizeLimit`, `multiSelect`、および `buttonTex`ファイル添付ウィジェットのオプションを設定するには、t を使用します。 必要に応じて、追加のカスタムプロパティを指定することもできます。

1. カスタムプロファイルでは、次の設定を使用します。

   * **multiSelect**-> trueまたはfalse （デフォルトでは true）
   * **fileSizeLimit** -> value_in_mb (say 5) （デフォルトで 2 MB）
   * **buttonText** -> ポップアップウィンドウのボタンのテキスト（デフォルトでは「添付」）
   * **承諾** -> 受け入れるファイルタイプ（デフォルトでは&quot;audio/&amp;ast;, video/&amp;ast;, image/&amp;ast;, text/&amp;ast;, .pdf&quot;）

   >[!NOTE]
   >
   >Microsoft Internet Explorer 9 では、指定された制限を超えたサイズのファイルを添付できます。これは既知の問題です。

1. 以下を使用： [メタデータエディター](/help/forms/using/manage-form-metadata.md) をクリックして、上記でHTML5 のフォーム用に作成したカスタムプロファイルを選択します。
1. カスタムプロファイルを使用してフォームテンプレートをレンダリングすると、添付ファイルアイコンがフォームツールバーの上に表示されます。

   >[!NOTE]
   >
   >ドラフトと添付ファイル機能を有効にすると、フォームポータルはデフォルトで、ファイルカスタムプロファイルを提供します。**ドラフトとして保存**&#x200B;プロファイルに関する詳細は、[HTML5 フォームをドラフトとして保存](/help/forms/using/saving-html5-form-draft.md)を参照してください。

1. 添付ファイルアイコンをクリックすると、添付ファイル選択ダイアログボックスが表示されます。ファイルを参照して添付ファイルを選択して&#x200B;**「添付」**&#x200B;をクリックします。

   >[!NOTE]
   >
   >添付ファイルをプレビューするには、添付ファイル名をクリックします。

   >[!NOTE]
   >
   >匿名のユーザーは、ファイルプレビューオプションを使用できません。

## 添付ファイル送信フォーマット {#attachment-submission-format}

添付ファイルが有効である場合、HTML5フォームはマルチパート形式のデータを送信します。マルチパート送信データには 2 つの部分があります **dataXml** および **添付ファイル**.

>[!NOTE]
>
>後方互換性の場合、 `mfAllowAttachments`オプションがオフの場合、HTML5 forms はマルチパートデータを送信しません。 単純なデータ xml を **application/xml** 形式

mfAllowAttachments フラグがオンになっている場合、[送信サービスのプロキシサービス](/help/forms/using/service-proxy.md)もまたマルチパート形式のデータを dataXml と添付ファイルと共に投稿します。
