---
title: AEM Forms アプリケーションで自動保存を使用
seo-title: Using autosave in AEM Forms app
description: データの損失を防ぐAEM Formsアプリの自動保存機能の使用方法を説明します。
seo-description: Learn how to use autosave feature in AEM Forms app that lets you avoid data loss.
uuid: f18ab6b4-dd4a-4dcb-88e6-e349777d47ea
contentOwner: sashanka
content-type: reference
products: SG_EXPERIENCEMANAGER/6.4/FORMS
topic-tags: forms-app
discoiquuid: 133d93b0-512c-46db-b5f9-f981d77b565f
exl-id: 6eb00c31-6806-478a-99d1-55912798ea69
source-git-commit: c5b816d74c6f02f85476d16868844f39b4c47996
workflow-type: tm+mt
source-wordcount: '330'
ht-degree: 58%

---

# AEM Forms アプリケーションで自動保存を使用 {#using-autosave-in-aem-forms-app}

>[!CAUTION]
>
>AEM 6.4 の拡張サポートは終了し、このドキュメントは更新されなくなりました。 詳細は、 [技術サポート期間](https://helpx.adobe.com/jp/support/programs/eol-matrix.html). サポートされているバージョンを見つける [ここ](https://experienceleague.adobe.com/docs/?lang=ja).

ユーザーがAdobe Experience Manager Formsアプリにデータを入力すると、自動保存機能によって一定の間隔でデータが保存されます。 AEM Formsアプリの自動保存機能は、アプリが誤って閉じられた場合のデータ損失を防ぐのに役立ちます。

アプリが誤って閉じる可能性があります：

* バッテリが低いためにデバイスがシャットダウンした場合
* ユーザーがアプリケーションを故意に終了した場合
* 予期しないクラッシュが発生した場合

入力したデータを保存する間隔を指定できます。

>[!NOTE]
>
>自動保存の頻度は慎重に選択してください。自動保存を頻繁に実行すると、デバイスのパフォーマンスに影響を及ぼすことがあります。

AEM Formsアプリの自動保存機能を使用するには、次の手順を実行します。

1. デスクトップアプリケーションにログインし、に移動します。 **[!UICONTROL 設定/一般]**.
1. 一般画面で「**[!UICONTROL 自動保存頻度]**」オプションを使用し、入力したデータをアプリケーションで保存する間隔を選択します。
   [ ![自動保存頻度の設定](assets/using-autosave-freq-07.png)](assets/using-autosave-freq-07-1.png)

1. アプリケーションを再起動して同じユーザーでログインすると、未保存のタスクの復元ダイアログで、タスクを復元するように求められます。未保存のタスクの復元ダイアログで「**[!UICONTROL OK]**」をクリックすると、保存済みのタスクで作業を再開できます。「**[!UICONTROL キャンセル]**」をクリックし、最後にトリガーされた自動保存の保存済みデータを削除して、新しいタスクで作業を始めることもできます。

   「**[!UICONTROL OK]**」をクリックすると、アプリケーションがクラッシュする前に最後にトリガーされた自動保存に対応するデータが使用されてタスクが復元されます。タスクに関連付けられたフォームデータとすべての添付ファイルも復元されます。
   [ ![タスクの復元&#x200B;](assets/autosave-flow.png)](assets/using-autosave-freq-06.png)**A.** 作業中のフォーム **B.** 強制終了したアプリ **C.** 未保存のタスクを復元ダイアログで再起動したアプリ **D.** 元のデータで復元されたフォーム
