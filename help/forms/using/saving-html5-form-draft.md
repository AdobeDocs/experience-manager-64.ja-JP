---
title: HTML5 フォームのドラフトでの保存
seo-title: Saving an HTML5 form as a draft
description: HTML5 フォームをドラフトとして保存し、後でフォームへの記入を再開します。
seo-description: Save an HTML5 form as a draft and resume filling the form at a later stage.
uuid: 70cd5f6f-f125-470c-8cee-ee14d2127713
content-type: reference
products: SG_EXPERIENCEMANAGER/6.4/FORMS
topic-tags: hTML5_forms
discoiquuid: 445e24af-cd1a-414d-bd01-9feb6631bbef
feature: Mobile Forms
exl-id: 8e4ffda9-ea92-4abc-8746-5d1852e4599b
source-git-commit: c5b816d74c6f02f85476d16868844f39b4c47996
workflow-type: tm+mt
source-wordcount: '336'
ht-degree: 50%

---

# HTML5 フォームのドラフトでの保存 {#saving-an-html-form-as-a-draft}

>[!CAUTION]
>
>AEM 6.4 の拡張サポートは終了し、このドキュメントは更新されなくなりました。 詳細は、 [技術サポート期間](https://helpx.adobe.com/jp/support/programs/eol-matrix.html). サポートされているバージョンを見つける [ここ](https://experienceleague.adobe.com/docs/?lang=ja).

HTML5 のフォームをドラフトとして保存し、後でフォームへの記入を再開できます。 Forms Portal を使用すると、すべてのユーザーが Adobe Portal フォームを保存および復元することができます。5. 「ドラフトとして保存」機能を有効にするには、プロファイルのノードに次の設定を追加します。

## 「ドラフトとして保存」機能を許可するためのカスタムプロファイル {#custom-profile-to-allow-save-as-draft-feature}

AEM Forms では初期状態で「**ドラフトとして保存**」プロファイルを使用できます。「ドラフトとして保存」プロファイルを使用してフォームをレンダリングすると、HTML5 フォームのドラフト機能を有効にすることができます。 フォームのHTMLレンダリングプロファイルを [Forms Manager](/help/forms/using/introduction-managing-forms.md).

既存の[カスタムプロファイル](/help/forms/using/custom-profile.md)に対して「ドラフトとして保存」機能を有効にするには、カスタムプロファイルのノードに次のプロパティを追加します。

<table> 
 <tbody> 
  <tr> 
   <td><strong>プロパティ名</strong></td> 
   <td><strong>タイプ</strong></td> 
   <td><strong>値</strong></td> 
   <td><strong>説明</strong></td> 
  </tr> 
  <tr> 
   <td>mfAllowFPDraft</td> 
   <td>文字列</td> 
   <td>true</td> 
   <td><p>ドラフトとして保存機能を有効にする</p> <p>を設定します。</p> </td> 
  </tr> 
  <tr> 
   <td>mfAllowAttachments</td> 
   <td>文字列</td> 
   <td>true</td> 
   <td><p>添付ファイルのアップロードを許可</p> <p>をこのプロファイルに設定します。</p> </td> 
  </tr> 
 </tbody> 
</table>

## ドラフトの保存と一覧表示 {#drafts-storage-and-listing}

フォームの「ドラフトとして保存」機能を有効にした後フォームを保存すると、 [ドラフトと送信コンポーネント](/help/forms/using/draft-submission-component.md). ドラフトと送信コンポーネントから保存されたフォームを取得し、入力を開始することができます。

ドラフトと送信コンポーネントのフォームの一覧表示を有効にするには、プロファイルのノードに次のプロパティを追加します。

<table> 
 <tbody> 
  <tr> 
   <td><strong>プロパティ名</strong></td> 
   <td><strong>タイプ</strong></td> 
   <td><strong>値</strong></td> 
   <td><strong>説明</strong></td> 
  </tr> 
  <tr> 
   <td>fp.enablePortalSubmit</td> 
   <td>文字列</td> 
   <td>true</td> 
   <td>ドラフトとフォームを送信した後、<br />フォームポータルのドラフトと送信コンポーネントに一覧表示できるようにします</td> 
  </tr> 
 </tbody> 
</table>

デフォルトでは、AEM Forms はフォームのドラフトと送信に関連付けられたユーザーデータをパブリッシュインスタンスの /content/forms/fp ノードに保存します。カスタムのストレージプロバイダーを追加できます。詳細は、[ドラフトと送信コンポーネントのカスタムストレージ](/help/forms/using/adding-custom-storage-provider-forms.md)を参照してください。
