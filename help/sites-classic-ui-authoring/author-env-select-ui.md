---
title: UI の選択
seo-title: Selecting your UI
description: オーサリングユーザーが使用しやすいように、タッチ対応 UI は必要に応じてクラシック UI に切り替えることができます。
seo-description: For convenience to authoring users, the touch-enabled UI does allow for switching to the classic UI when necessary.
uuid: 755e513e-990c-4dba-8316-623f17bf5c33
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.4/SITES
topic-tags: introduction
content-type: reference
discoiquuid: dcac2a3a-3241-47de-96ce-982ab0bc05eb
exl-id: 997040d4-cf8f-4240-8423-a98d562aae02
source-git-commit: bd94d3949f0117aa3e1c9f0e84f7293a5d6b03b4
workflow-type: tm+mt
source-wordcount: '196'
ht-degree: 55%

---

# UI の選択{#selecting-your-ui}

タッチ操作対応 UI はクラシック UI より優先されるので、クラシック UI を使用し続けるには、AEMインスタンスのユーザーまたは管理者がアクティブな決定を下す必要があります。 クラシック UI はメンテナンスされなくなったので、オーサリングユーザーがクラシック UI からタッチ操作対応 UI の同等の UI に切り替えるだけで済みません。

オーサリングユーザーが使用しやすいように、タッチ対応 UI は必要に応じてクラシック UI に切り替えることができます。詳しくは、標準オーサリングのドキュメントの [UI の選択](/help/sites-authoring/select-ui.md)を参照してください。

>[!NOTE]
>
>以前のバージョンからアップグレードされたインスタンスでは、ページオーサリング用にクラシック UI が保持されます。
>
>アップグレード後、ページオーサリングは自動的にタッチ操作対応 UI に切り替わりませんが、次を使用して設定できます： [OSGi 設定](/help/sites-deploying/configuring-osgi.md) の **WCM オーサリング UI モードサービス** ( `AuthoringUIMode` サービス )。 [エディターの UI 上書き](#uioverridesfortheeditor)を参照してください。

## ユーザーのインスタンス用のデフォルト UI の設定 {#configuring-the-default-ui-for-your-instance}

システム管理者は、[ルートマッピング](/help/sites-deploying/osgi-configuration-settings.md#daycqrootmapping)を使用して、起動時およびログイン時に表示される UI を設定できます。

この設定はユーザーデフォルトまたはセッション設定によって上書きできます。
