---
title: HTML Workspace でのアダプティブフォームの使用
seo-title: Using an adaptive form in HTML Workspace
description: HTML Workspace でのアダプティブフォームの使用
seo-description: Using an adaptive form in HTML Workspace
uuid: 1ebe81ae-5c0b-4c07-8cd1-86efdf8415be
content-type: reference
products: SG_EXPERIENCEMANAGER/6.4/FORMS
topic-tags: forms-workspace
discoiquuid: 2f514072-81d9-48de-8369-cca94a330f1d
exl-id: 88fa9c80-4eae-4663-a6c8-abbf1921444e
source-git-commit: bd94d3949f0117aa3e1c9f0e84f7293a5d6b03b4
workflow-type: tm+mt
source-wordcount: '677'
ht-degree: 67%

---

# HTML Workspace でのアダプティブフォームの使用 {#using-an-adaptive-form-in-html-workspace}

JEE 上のAEM Formsでは、Workspace でアダプティブフォームを使用することができます。HTML

プロセスデザイン時に XDP を選択できるので、既存のアダプティブフォームのAEMリポジトリから参照する機能が追加されました。 この機能により、プロセスデザイナーはアダプティブフォームを Task 内と Starting Point 内で設定できます。

## プロセスデザインのエクスペリエンス {#process-design-experience}

プロセスデザインでアダプティブフォームの使用を有効化するには、次の手順を実行します。

* 「Assign Task」および「Start Point」では、タスクにフォームアセットを割り当てる際に、CRX リポジトリ内のアダプティブフォームアセットを参照することができます。
* 「Assign Task」および「Start Point」の Workbench プロパティシートでは、アダプティブフォームのトップレベル / グローバルツールバーを非表示にすることができます。
* 新しいアクションプロファイルを、アダプティブフォームでのレンダリングおよび送信アクションに使用することができます。

### LiveCycle アプリケーションのエクスポートおよびインポート {#livecycle-application-export-and-import}

アダプティブフォームは AEM リポジトリにあるため、LiveCycle アプリケーションのエクスポートには、使用されているアダプティブフォームへのリファレンスのみが含まれています。したがって、LiveCycleアプリケーションの書き出しと読み込みは、2 つの手順で構成されます。 LiveCycle アプリケーションには、プロセスの定義などが含まれています。アダプティブフォームを含む別のパッケージが、AEM より ZIP ファイルにてエクスポートされます。インポート中、LiveCycle アプリケーションは Workbench を通してインポートされ、アダプティブフォームは AEM を通してインポートされます。

## HTML Workspace におけるアダプティブフォームのユーザーエクスペリエンス {#user-experience-of-adaptive-form-in-html-workspace}

HTML Workspace は、モバイルフォームに使用できるコントロールのほかに、アダプティブフォーム特有のコントロールをいくつか提供しています。HTML Workspace で「Task」または「Start Point」を開くと、ユーザーは、アダプティブフォームをナビゲートし、保存、署名、送信、添付ファイルの追加を行うことができます。詳しい内容は次のとおりです。

1. ファイルを**添付するには、Mobile Formsと同様に Task 添付ファイルを使用します。 アダプティブフォームでは、File Attachment タイプのボタンは非表示になっています。

1. アダプティブフォームを保存するには、「**保存**」をクリックします。アダプティブフォームでは、Save タイプのボタンは非表示になっています。

1. アダプティブフォームを送信するには、Mobile Forms と同じように、「**送信**」ボタンを使うか、またはルートアクションを使用します。アダプティブフォームでは、Submit タイプのボタンは非表示になっています。

1. **アダプティブフォームグローバルツールバーの表示**:プロセスデザイナーによってグローバル/トップレベルのツールバーが非表示になっている場合、ツールバーとボタンはアダプティブフォームに表示されません。

1. **アダプティブFormsの Workspace ナビゲーションコントロール**:Workspace のアダプティブフォームでは、「保存」、「送信」、「ルートアクション」の各ボタンと共に「次へ」/「前へ」の各ボタンを使用できます。 HTML Workspace でアダプティブフォームのパネルをナビゲートするには、次へ / 前へのボタンをクリックします。次へ／前へのボタンは、アダプティブフォームのモバイル表示のナビゲーションコントロールに似た精密なナビゲーションを提供します。

1. **アダプティブフォームの eSign サービスと Summary コンポーネント**:Summary コンポーネントは、Workspace では操作できません。HTML。 つまり、アダプティブフォームに Summary コンポーネントが含まれていても、ワークスペースでは表示されません。HTML Workspace では、ユーザーは、Esign コンポーネントの自動送信の代わりに、送信またはルートアクションをクリックします。ドキュメントが署名された後は、フラット（非インタラクティブ）な署名済みドキュメントとして表示されます。「**送信**」またはルートアクションをクリックして、タスクまたは Start Point を閉じます。

   署名済みのドキュメントが eSign サービスサーバーから収集され、データ xml ファイルがプロセス内の次のステップへと転送されます。

## アダプティブフォームをプロセスデザインで使用するための手順 {#steps-to-use-adaptive-forms-in-process-design}

1. Adobe Experience Manager Forms Workbench を開きます。

1. に移動します。 **ファイル/新規/アプリケーション** または、既存のアプリケーションを使用してアプリケーションを作成します。

   ![新しいアプリケーションの作成](assets/create_new_appl.png)

1. プロセスを作成するか、アプリケーション内の既存のプロセスを使用します。

   ![新しいプロセスの作成](assets/create_new_process.png)

1. Start Point または Assign Task を作成し、ダブルクリックします。
1. **[!UICONTROL Presentation &amp; Data]** セクションで、**[!UICONTROL CRX アセットの使用]**&#x200B;を選択し、アセットの前の三点リーダーをクリックします。

   ![CRX アセットを使用する](assets/use_crx_asset.png)

1. 「アセット管理」UI で作成したアダプティブフォームを選択し、 **[!UICONTROL OK]**.

   ![アダプティブフォームの選択](assets/selecting_form.png)

   >[!NOTE]
   >
   >アダプティブフォームの作成について詳しくは、「[アダプティブフォームの作成](/help/forms/using/creating-adaptive-form.md)」を参照してください。
   >
   >プロセスの作成について詳しくは、 [プロセスの作成と管理](https://help.adobe.com/en_US/AEMForms/6.1/WorkbenchHelp/WS92d06802c76abadb-1cc35bda128261a20dd-7ff7.2.html).
