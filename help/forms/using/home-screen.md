---
title: ホーム画面
seo-title: Home screen
description: AEM Formsアプリのホーム画面のコンポーネントの説明
seo-description: Description of the components of the AEM Forms app Home screen
uuid: 7705b499-8b38-4c2e-abd8-6901cf268428
content-type: reference
products: SG_EXPERIENCEMANAGER/6.4/FORMS
topic-tags: forms-app
discoiquuid: e4636b25-20a4-4326-82fb-f22f735e43c0
exl-id: b8f515fd-7ab7-4237-9a35-2840f708e856
source-git-commit: bd94d3949f0117aa3e1c9f0e84f7293a5d6b03b4
workflow-type: tm+mt
source-wordcount: '334'
ht-degree: 26%

---

# ホーム画面 {#home-screen}

AEM Formsアプリケーションにログインすると、ホーム画面にリダイレクトされます。

## デフォルトのホーム画面 {#default-home-screen}

デフォルトでは、ホーム画面には、スタートポイントとタスク ( 接続サーバーでAEM Forms Workflow が有効になっている場合 ) を含むすべてのフォームと、関連するサムネールが表示されます。 AEM Formsサーバーでサムネールを指定できます。

次の図では、デフォルトのホーム画面で基本的なコンポーネントに引き出し線の注釈が付けられています。
![Formsアプリのホーム画面](assets/home-screen-1.png)
[クリックして拡大](assets/home-screen-1-1.png)

1. **メニューボタン**：「**メニュー**」ボタンをタップして、タスク、フォーム、アウトボックス、設定に移動します。AEM FormsアプリがAEM Forms JEE サーバーに接続されている場合は、「タスク」オプションが表示されます。 「タスク」オプションは、プロセス内のタスクから作成されたドラフトも保存します。 AEM Forms OSGi サーバーでは、「Tasks」オプションは非表示になっています。 Outbox は、サーバーと同期する前に、保存されたフォームとドラフトを保存します。 アウトボックスに保存されたすべてのフォームとドラフトは、アプリケーションが[サーバーと同期された](/help/forms/using/sync-app.md)ときに AEM Forms サーバーにアップロードされます。設定については、[一般設定の更新](/help/forms/using/update-general-settings.md)を参照してください。
1. **タスクまたはフォーム**:リストに表示された、作業対象のタスクまたはフォームをタップします。
1. **水平省略記号**:フォームでアクションを使用できることを示します。 省略記号をタップすると、作成者が提供したアクションと説明が表示されます。 「**ドラフトを削除**」および「**完了**」オプションは、省略記号をタップすると表示されます。
1. **更新アイコン**:更新アイコンをタップして、アプリをAEM Formsサーバーと同期します。

## ホーム画面のカスタマイズ {#customizing-the-home-screen}

![一般設定](assets/gen-settings.png)

アプリケーションの「**[一般設定](/help/forms/using/update-general-settings.md)**」か、または HTML Workspace の「**環境設定**」タブから、アプリケーションのデフォルトのホーム画面を変更できます。

アプリケーションのホーム画面設定に加えた変更は、現在のモバイルデバイスに現在ログインしているユーザーのホーム画面に反映されます。

ただし、HTMLWorkspace での変更は、AEM FormsサーバーにログオンしているすべてのAEM Formsアプリユーザーに影響します。
