---
title: OSGi 上のフォームベース AEM ワークフローおよび AEM Forms JEE ワークフローのアクションと機能
seo-title: Actions and capabilities of Form-centric AEM Workflows on OSGi and AEM Forms JEE workflows
description: AEM Inbox とHTMLWorkspace でサポートされるアクションの違い、OSGi 上の Forms 中心のAEM Workflows とAEM Forms JEE ワークフローでサポートされる機能の違い、AEM Inbox とAEM Formsアプリの機能の違いについて詳しく説明します。
seo-description: Learn more about the differences in actions supported by AEM Inbox and HTML Workspace, differences in capabilities supported by Form-centric AEM Workflows on OSGi and AEM Forms JEE Workflows, and differences between AEM Inbox and AEM Forms app features.
uuid: ce2a05fe-ba45-42ed-880e-fb1d6efc1d26
contentOwner: khsingh
topic-tags: publish
discoiquuid: 4c7ba430-25b2-4ba2-a5eb-4edaed0d599a
exl-id: 6172d936-9348-4f3f-a437-6465dd156f3b
source-git-commit: f8b19b6723d333e76fed111b9fde376b3bb13a1d
workflow-type: tm+mt
source-wordcount: '878'
ht-degree: 46%

---

# OSGi 上のフォームベース AEM ワークフローおよび AEM Forms JEE ワークフローのアクションと機能  {#actions-and-capabilities-of-form-centric-aem-workflows-on-osgi-and-aem-forms-jee-workflows}

## AEM Inbox とHTMLWorkspace {#aem-inbox-and-html-workspace}

AEM Inbox は、OSGi 上でForms中心のAEMワークフローを実行および監視するために使用されます。 HTMLWorkspace を使用すると、AEM Forms JEE ワークフローを実行および監視できます。 次の表に、OSGi 上のForms中心のAEM Workflows 用AEMインボックスと、AEM Forms JEE ワークフロー用の WorkspaceHTMLで使用できる重要なアクションを示します。

<table> 
 <tbody>
  <tr>
   <td>アクション</td> 
   <td>AEM インボックス</td> 
   <td>HTMLワークスペース</td> 
  </tr>
  <tr>
   <td>プロセス、タスクまたはフォームアプリケーションの開始<br /> </td> 
   <td>サポート対象<br /> </td> 
   <td>サポート対象<br /> </td> 
  </tr>
  <tr>
   <td>タスクの送信</td> 
   <td>サポート対象<br /> </td> 
   <td>サポート対象<br /> </td> 
  </tr>
  <tr>
   <td>グループへのタスクの割り当て</td> 
   <td>サポート対象<br /> </td> 
   <td>サポート対象<br /> </td> 
  </tr>
  <tr>
   <td>複数のルートへの送信</td> 
   <td>サポート対象<br /> </td> 
   <td>サポート対象<br /> </td> 
  </tr>
  <tr>
   <td>タスク履歴とタスクの概要の追跡</td> 
   <td>サポート対象<br /> </td> 
   <td>サポート対象<br /> </td> 
  </tr>
  <tr>
   <td>電子メール通知</td> 
   <td>サポート対象<br /> </td> 
   <td>サポート対象<br /> </td> 
  </tr>
  <tr>
   <td>タスクの再割り当て</td> 
   <td>サポート対象</td> 
   <td>サポート対象</td> 
  </tr>
  <tr>
   <td>アダプティブフォームのフィールドレベルの添付ファイル</td> 
   <td>サポート対象</td> 
   <td>サポート対象外</td> 
  </tr>
  <tr>
   <td>カレンダー表示</td> 
   <td>サポート対象</td> 
   <td>サポート対象外</td> 
  </tr>
  <tr>
   <td>タスクレベルのコメント</td> 
   <td>サポート対象</td> 
   <td>サポート対象外</td> 
  </tr>
  <tr>
   <td>キュー（共有個人キュー、キューからタスクを要求）</td> 
   <td>サポート対象外</td> 
   <td>サポート対象</td> 
  </tr>
  <tr>
   <td>不在通知</td> 
   <td>サポート対象外</td> 
   <td>サポート対象</td> 
  </tr>
  <tr>
   <td>複数のユーザーへのタスクの割り当て</td> 
   <td>サポート対象外</td> 
   <td>サポート対象</td> 
  </tr>
 </tbody>
</table>

## OSGi 上の Forms 中心のAEM Workflows とAEM Forms JEE ワークフロー {#form-centric-aem-workflows-on-osgi-and-aem-forms-jee-workflows}

OSGi 上の Forms 中心のAEM Workflows とAEM Forms JEE Workflows(JEE 上のAEM Forms Process Management) には、異なる機能セットがあります。 次の表に、OSGi 上の Forms 中心のAEM Workflows および JEE 上のAEM Formsワークフローで使用可能な重要な機能とサポートを示します。

<table> 
 <tbody>
  <tr>
   <td>機能</td> 
   <td>OSGi 上のフォームベース AEM ワークフロー<br /> </td> 
   <td>AEM Forms JEE ワークフロー</td> 
  </tr>
  <tr>
   <td>アダプティブフォーム</td> 
   <td>サポート対象</td> 
   <td>サポート対象<br /> </td> 
  </tr>
  <tr>
   <td>他のAEMソリューションとの統合</td> 
   <td>サポート対象</td> 
   <td>サポート対象</td> 
  </tr>
  <tr>
   <td>手書き署名</td> 
   <td>サポート対象</td> 
   <td>サポート対象<br /> </td> 
  </tr>
  <tr>
   <td>カスタム電子メールテンプレート</td> 
   <td>サポート対象</td> 
   <td>サポート対象<br /> </td> 
  </tr>
  <tr>
   <td>タスクの優先度の定義</td> 
   <td>サポート対象</td> 
   <td>サポート対象</td> 
  </tr>
  <tr>
   <td>期限後にタスクをタイムアウトします</td> 
   <td>サポート対象</td> 
   <td>サポート対象</td> 
  </tr>
  <tr>
   <td>ワークフロー内のループ</td> 
   <td>サポート対象</td> 
   <td>サポート対象</td> 
  </tr>
  <tr>
   <td>担当者の動的な選択 </td> 
   <td>サポート対象</td> 
   <td>サポート対象</td> 
  </tr>
  <tr>
   <td>カスタムメタデータの使用</td> 
   <td>サポート対象</td> 
   <td>サポート対象</td> 
  </tr>
  <tr>
   <td>電子署名 (Acrobat Sign)</td> 
   <td>サポート対象 <sup>[1]</sup></td> 
   <td>サポート対象 <sup>[5]</sup></td> 
  </tr>
  <tr>
   <td>タスクとフォームのアプリケーションを管理</td> 
   <td>サポート対象 <sup>[2]</sup><br /> </td> 
   <td>サポート対象 <sup>[2]</sup></td> 
  </tr>
  <tr>
   <td>ドキュメントサービス</td> 
   <td>サポート対象 <sup>[3]</sup></td> 
   <td>サポート対象 <sup>[3]</sup></td> 
  </tr>
  <tr>
   <td>完了したタスクをアダプティブフォームまたはPDFドキュメントとしてレンダリング</td> 
   <td>サポート対象</td> 
   <td>サポート対象[4]</td> 
  </tr>
  <tr>
   <td>Correspondence Management との統合</td> 
   <td>サポート対象</td> 
   <td>サポート対象</td> 
  </tr>
  <tr>
   <td>リセットボタン</td> 
   <td>サポート対象</td> 
   <td>サポート対象外</td> 
  </tr>
  <tr>
   <td>ワークフローステージ</td> 
   <td>サポート対象</td> 
   <td>サポート対象外</td> 
  </tr>
  <tr>
   <td>読み取り専用のアダプティブフォーム</td> 
   <td>サポート対象</td> 
   <td>サポート対象外</td> 
  </tr>
  <tr>
   <td>デフォルトの保存ボタンを非表示にする</td> 
   <td>サポート対象</td> 
   <td>サポート対象外</td> 
  </tr>
  <tr>
   <td>ワークフローの詳細セクションの詳細なコントロール</td> 
   <td>サポート対象</td> 
   <td>サポート対象外</td> 
  </tr>
  <tr>
   <td>HTML5 フォーム、インタラクティブ PDF フォーム、フォームセット<br /> </td> 
   <td>サポート対象外<br /> </td> 
   <td>サポート対象</td> 
  </tr>
  <tr>
   <td>プロセスレポート</td> 
   <td>サポート対象外<br /> </td> 
   <td>サポート対象<br /> </td> 
  </tr>
  <tr>
   <td>デジタル署名</td> 
   <td>サポート対象<br /> </td> 
   <td>サポート対象<br /> </td> 
  </tr>
  <tr>
   <td>スタートポイントカテゴリ</td> 
   <td>サポート対象外 </td> 
   <td>サポート対象 </td> 
  </tr>
  <tr>
   <td>タスクの一括承認 </td> 
   <td>サポート対象外 </td> 
   <td>サポート対象 </td> 
  </tr>
  <tr>
   <td>ドラフトをカスタム名で保存</td> 
   <td>サポート対象外 </td> 
   <td>サポート対象 </td> 
  </tr>
  <tr>
   <td>既存のプロセスデータを使用したプロセスの開始<br /> </td> 
   <td>サポート対象外</td> 
   <td>サポート対象 </td> 
  </tr>
  <tr>
   <td>スタートポイントをドラフトとして保存中</td> 
   <td>サポート対象外</td> 
   <td>サポート対象</td> 
  </tr>
  <tr>
   <td>ユーザーアバター</td> 
   <td>サポート対象</td> 
   <td>サポート対象</td> 
  </tr>
  <tr>
   <td>マネージャビュー</td> 
   <td>サポート対象外</td> 
   <td>サポート対象<br /> </td> 
  </tr>
  <tr>
   <td>テンプレートを検索</td> 
   <td>サポート対象外</td> 
   <td>サポート対象<br /> </td> 
  </tr>
  <tr>
   <td>サードパーティアプリケーションとの統合</td> 
   <td>サポート対象 <sup>[6]</sup></td> 
   <td>サポート対象</td> 
  </tr>
  <tr>
   <td>ワークフローアプリケーションまたはスタートポイントのタスクレベルの添付ファイル</td> 
   <td>サポート対象外</td> 
   <td>サポート対象</td> 
  </tr>
  <tr>
   <td>リマインダーの電子メール</td> 
   <td>サポート対象外</td> 
   <td>サポート対象</td> 
  </tr>
  <tr>
   <td>タスクタイムアウト時にタイトルを変更</td> 
   <td>サポート対象外</td> 
   <td>サポート対象</td> 
  </tr>
  <tr>
   <td>タスクの委任とタスクの要求に関するメール</td> 
   <td>サポート対象外</td> 
   <td>サポート対象</td> 
  </tr>
  <tr>
   <td>ワークフローの最後に E メールを送信</td> 
   <td>サポート対象 <sup>[7]</sup></td> 
   <td>サポート対象</td> 
  </tr>
  <tr>
   <td>異なるグループ間で委任</td> 
   <td>サポート対象外</td> 
   <td>サポート対象</td> 
  </tr>
  <tr>
   <td>ワークフローからの Web サービスの呼び出し</td> 
   <td>サポート対象 <sup>[6]</sup></td> 
   <td>サポート対象</td> 
  </tr>
  <tr>
   <td>XSLT 変換</td> 
   <td>サポート対象外</td> 
   <td>サポート対象</td> 
  </tr>
  <tr>
   <td>ゲートウェイ、NO WAIT</td> 
   <td>サポート対象 </td> 
   <td>サポート対象 </td> 
  </tr>
  <tr>
   <td>OR、AND 分岐</td> 
   <td>サポート対象外</td> 
   <td>サポート対象</td> 
  </tr>
  <tr>
   <td>動的タスクの優先度</td> 
   <td>サポート対象外</td> 
   <td>サポート対象外</td> 
  </tr>
 </tbody>
</table>

1. OSGi 上のフォーム中心のAEMワークフローを使用して、既に入力済みのアダプティブフォームに署名することができます。 OSGi 上の Forms 中心の AEM ワークフローでは、フォーム外署名機能がサポートされています。[フォーム内署名](/help/forms/using/working-with-adobe-sign.md#create-in-form-signing-experience)エクスペリエンスはサポートされていません。

1. AEM Forms OSGi AEM Workflows を実行して監視し、AEM Forms JEE ワークフローを実行して監視するには、AEM Inbox へのアクセス権が必要です。
1. ネイティブの AEM Forms ドキュメントサービスは、OSGi 上のフォーム中心の AEM ワークフローと AEM Forms JEE ワークフローの両方で使用することができます。AEM ワークフローでは、OSGi 上のフォーム中心の AEM ワークフローと AEM Forms JEE ワークフローに対して、ネイティブのドキュメントサービスが使用されます。
1. AEM Forms JEE ワークフローは、アダプティブフォームのみをレンダリングできます。 アダプティブフォームをPDFドキュメントとしてレンダリングすることはできません。
1. AEM forms JEE ワークフローには、Acrobat Sign用の個別の手順はありません。 AEM forms JEE ワークフローに対して、Acrobat Sign対応のアダプティブフォームが必要です。 詳しくは、 [Acrobat Signドキュメント](/help/forms/using/working-with-adobe-sign.md#add-and-configure-the-signature-step-component).
1. [フォームデータモデルサービスを呼び出し](/help/forms/using/aem-forms-workflow-step-reference.md#p-invoke-form-data-model-service-step-p)する手順を使用して、Web サービスのサービスを呼び出し、サードパーティアプリケーションからデータを投稿または取得できます。
1. [メールの送信](/help/forms/using/aem-forms-workflow-step-reference.md#send-email-step)手順を使用して、メールを送信できます。

## AEM インボックスの機能と AEM Forms アプリケーションの機能との違い {#differences-between-aem-inbox-and-aem-forms-app-features}

Forms 中心のワークフローを起動するには、[AEM インボックス](/help/forms/using/manage-applications-inbox.md)と AEM Forms アプリケーションの 2 つの方法があります。ただし、AEM インボックスの機能と AEM Forms アプリケーションの機能は異なっています。AEM インボックスは [Forms 中心のワークフロー](/help/forms/using/aem-forms-workflow.md)でのみ機能するのに対して、AEM Forms アプリケーションは Forms 中心のワークフローだけでなく、Process Management でも機能します。

以下の表に、AEM インボックスの機能と AEM Forms アプリケーションの機能を示します。

<table> 
 <tbody>
  <tr>
   <td><p><strong>アクション</strong></p> </td> 
   <td><p><strong>AEM インボックス</strong></p> </td> 
   <td><p><strong>AEM Forms アプリケーション</strong></p> </td> 
  </tr>
  <tr>
   <td><p>フォームアプリケーションの開始</p> </td> 
   <td><p>サポート対象</p> </td> 
   <td><p>サポート対象</p> </td> 
  </tr>
  <tr>
   <td><p>タスクの送信</p> </td> 
   <td><p>サポート対象</p> </td> 
   <td><p>サポート対象</p> </td> 
  </tr>
  <tr>
   <td><p>タスクの委任</p> </td> 
   <td><p>サポート対象</p> </td> 
   <td><p>サポート対象外</p> </td> 
  </tr>
  <tr>
   <td><p>タスク履歴とタスクの概要の追跡</p> </td> 
   <td><p>サポート対象</p> </td> 
   <td><p>サポート対象外</p> </td> 
  </tr>
  <tr>
   <td><p>タスクレベルの添付ファイルの追加</p> </td> 
   <td><p>サポート対象</p> </td> 
   <td><p>サポート対象</p> </td> 
  </tr>
  <tr>
   <td><p>タスクレベルの添付ファイルの表示</p> </td> 
   <td><p>サポート対象</p> </td> 
   <td><p>サポート対象</p> </td> 
  </tr>
  <tr>
   <td><p>フィールドレベルの添付ファイルの追加</p> </td> 
   <td><p>サポート対象</p> </td> 
   <td><p>サポート対象</p> </td> 
  </tr>
  <tr>
   <td><p>カレンダービューの表示</p> </td> 
   <td><p>サポート対象</p> </td> 
   <td><p>サポート対象外</p> </td> 
  </tr>
  <tr>
   <td><p>コメントの追加</p> </td> 
   <td><p>サポート対象</p> </td> 
   <td><p>サポート対象</p> </td> 
  </tr>
 </tbody>
</table>
