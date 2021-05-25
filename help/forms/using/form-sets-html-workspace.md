---
title: AEM Forms Workspace のフォームセットの使用
seo-title: AEM Forms Workspace のフォームセットの使用
description: フォームセットは HTML5 フォームの集まりであり、エンドユーザーには 1 つのフォームのセットとして提供されます。AEM Forms Workspace でフォームセットを使用する方法について説明します。
seo-description: フォームセットは HTML5 フォームの集まりであり、エンドユーザーには 1 つのフォームのセットとして提供されます。AEM Forms Workspace でフォームセットを使用する方法について説明します。
uuid: 77f81465-bd60-4aee-8507-585fe08adb78
contentOwner: vishgupt
content-type: reference
products: SG_EXPERIENCEMANAGER/6.4/FORMS
topic-tags: forms-workspace
discoiquuid: c1793e2e-413c-4b6f-b96b-09e011f06263
exl-id: 4e39f6dd-b7a3-4c6c-be1f-66b9a5743352
source-git-commit: bd94d3949f0117aa3e1c9f0e84f7293a5d6b03b4
workflow-type: tm+mt
source-wordcount: '384'
ht-degree: 73%

---

# AEM Forms Workspace のフォームセットの使用 {#working-with-formsets-in-aem-forms-workspace}

フォームセットは HTML5 フォームの集まりであり、エンドユーザーには 1 つのフォームのセットとして提供されます。エンドユーザーがフォームセットへの入力を始めると、フォームセットはその内容を別のフォームにもシームレスに移行します。フォームセットは 1 回クリックすれば送信できます。フォームセットとその設定方法について詳しくは、「AEM Formsの[フォームセット](/help/forms/using/formset-in-aem-forms.md)」を参照してください。

AEM Forms Workspace はフォームセットをサポートします。フォームセットでは、サービスやプロセスに関連する複数のフォームをグループ化し、ビジネス上のプロセスを自動化するとともにエンドユーザーに表示します。このようなシナリオでは、ユーザーはセット全体を 1 つとして記入し、個々のフォームやプロセスをファイル、送信、追跡する必要はありません。

## AEM Forms Workspace アプリケーションにおけるフォームセットのスタートポイントへの割り当て {#attaching-a-formset-to-startpoint-in-an-aem-forms-workspace-app-br}

1. Workbench でビジネスプロセスのワークフローを作成します。詳しくは、[Workbenchヘルプ](https://www.adobe.com/go/learn_aemforms_workbench_63)を参照してください。
1. スタートポイントのプロセスプロパティから、「Presentation &amp; Data」で「**Use A CRX Asset**」を選択します。

   ![3-1](assets/1-1.png)

1. CRXアセットパスの横にある![browse](assets/browse.png)(Browse)をクリックします。 フォームアセットを選択ダイアログが表示されます。

   ![2](assets/2.png)

1. 「**フォームセット**」タブをクリックし、リストから目的のフォームセットを選択して、「**OK**」をクリックします。

1. 他の関連するプロセスプロパティを更新した後に、アプリケーションをデプロイします。

## AEM Forms Workspace でのフォームセットの使用 {#using-formset-in-nbsp-aem-forms-workspace}

フォームセットをスタートポイントに関連付けると、他のスタートポイントが呼び出されると同時に、AEM Forms Workspaceからスタートポイントを呼び出すことができます。

AEM Forms Workspace を通じてフォームセットでサポートされる操作は次のとおりです。

* ドラフトとして保存
* Lock
* 中断
* 送信
* 添付ファイルを追加
* メモを追加
* 「戻る」または「次へ」ボタンを使用したフォームセット内の移動

![3-1](assets/3-1.png)

>[!NOTE]
>
>フォームセット内で前のフォームや次のフォームに移動する際のパフォーマンスを向上するため、Workspace のすべてのボタン（「戻る」、「次へ」、「保存」、「送信」、「...」（詳細））は、関連フォームのレンダリングが終了するまで無効になります。
