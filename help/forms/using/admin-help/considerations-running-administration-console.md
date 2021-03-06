---
title: 管理コンソール実行時の考慮事項
seo-title: Considerations when running AdministrationConsole
description: 管理コンソール実行時のいくつかの考慮事項について説明します。
seo-description: This document lists a few points to consider when running Administration Console.
uuid: e260f187-4728-44f3-a5c1-7388ff3965c4
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_the_application_server
products: SG_EXPERIENCEMANAGER/6.4/FORMS
discoiquuid: 525c4afc-e109-4546-b78c-1efee63edc43
exl-id: 991418fd-5ff8-491e-834e-2324e029e499
source-git-commit: bd94d3949f0117aa3e1c9f0e84f7293a5d6b03b4
workflow-type: tm+mt
source-wordcount: '130'
ht-degree: 87%

---

# 管理コンソール実行時の考慮事項 {#considerations-when-running-administrationconsole}

管理コンソールの実行時には、以下のことを考慮してください。

* URL を使用して管理コンソールにアクセスする場合 `https://*[hostname]*:*[port]*/adminui`を指定した場合、指定したホスト名にアンダースコア文字を含めることはできません。 アンダースコア文字を含めると、管理コンソールの一部の領域へのリンクが正しく機能しない場合があります。
* 日本語の OS 上の Windows エクスプローラーで管理コンソールを実行すると、次の問題が発生することがあります。

   * リンクをクリックすると、予期するリンクではなく、ログインページに戻る。
   * リンクをクリックすると、アクセス権エラーが表示される。

   ベストプラクティスとしては、Mozilla Firefox などの別のブラウザーから管理コンソールを実行し、リンクの失敗がないことを確認します。

* 管理コンソールで検索を実行するときはバックスラッシュ文字（）を使用しないでください。
