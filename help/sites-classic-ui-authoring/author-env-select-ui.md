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
ht-degree: 76%

---

# UI の選択 {#selecting-your-ui}

タッチ操作向け UI はクラシック UI より優先されるので、クラシック UI の使用を続行するには、AEM インスタンスのユーザーまたは管理者が自発的に決定する必要があります。クラシック UI のサポートは既に終了しています。そのため、オーサリングユーザーはクラシック UI からタッチ対応 UI の同等の機能に簡単に切り替えることはできません。

オーサリングユーザーが使用しやすいように、タッチ対応 UI は必要に応じてクラシック UI に切り替えることができます。詳しくは、 [UI の選択](/help/sites-authoring/select-ui.md) 詳しくは、標準のオーサリングドキュメントを参照してください。

>[!NOTE]
>
>以前のバージョンからアップグレードされたインスタンスでは、ページオーサリング用にクラシック UI が保持されます。
>
>アップグレード後、ページオーサリングが自動的にタッチ対応 UI に切り替わることはありませんが、**WCM オーサリング UI モードサービス**（`AuthoringUIMode` サービス）の [OSGi 設定](/help/sites-deploying/configuring-osgi.md)を使用すると、その切り替えを設定できます。[エディターの UI 上書き](#uioverridesfortheeditor)を参照してください。

## インスタンスのデフォルト UI の設定 {#configuring-the-default-ui-for-your-instance}

システム管理者は、起動時とログイン時に表示される UI を、 [ルートマッピング](/help/sites-deploying/osgi-configuration-settings.md#daycqrootmapping).

この設定は、ユーザーの既定値またはセッション設定で上書きできます。
