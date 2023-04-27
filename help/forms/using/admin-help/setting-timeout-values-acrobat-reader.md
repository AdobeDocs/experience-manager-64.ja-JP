---
title: Acrobat Reader DC Extensions で使用するタイムアウト値の設定
seo-title: Setting timeout values for use with Acrobat Reader DC extensions
description: Acrobat Reader DC拡張機能で使用するタイムアウト値を設定する方法について説明します。
seo-description: Learn how to set timeout values for use with Acrobat Reader DC extensions.
uuid: d6d072a0-0a30-417a-98b1-df8b4ff8f911
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_acrobat_reader_dc_extensions
products: SG_EXPERIENCEMANAGER/6.4/FORMS
discoiquuid: a9aeeb89-45e9-4d5d-aa25-8145c89b64f2
exl-id: e7de9971-3eac-4248-8709-0da7dd709d1b
source-git-commit: bd94d3949f0117aa3e1c9f0e84f7293a5d6b03b4
workflow-type: tm+mt
source-wordcount: '172'
ht-degree: 36%

---

# Acrobat Reader DC Extensions で使用するタイムアウト値の設定  {#setting-timeout-values-for-use-with-acrobat-reader-dc-extensions}

Acrobat Reader DC拡張機能の多くのPDFファイルで作業する場合は、ジョブのタイムアウトと失敗を防ぐために、次のタイムアウト値が適切に設定されていることを確認してください。

**ドキュメント廃棄タイムアウト：**

この値は管理コンソールで設定できます。 設定/コアシステム設定/設定をクリックし、「デフォルトのドキュメント廃棄タイムアウト」の値を指定します。

**User Manager AEM Forms のタイムアウト：**&#x200B;この値を設定するには、config.xml ファイルを編集してください。管理コンソールで、設定/User Management/設定/設定ファイルの読み込みと書き出しをクリックし、「書き出し」をクリックします。 書き出された config.xml ファイルを開き、次の行を編集します。

&lt;entry key=&quot;assertionValidityInMinutes&quot; value=&quot;600&quot;/>

&lt;entry key=&quot;SessionTimeout&quot; value=&quot;600&quot;/>

config.xml ファイルを保存し、管理コンソールに再度読み込みます。

**アプリケーションサーバーセッションタイムアウト：**&#x200B;この値は、アプリケーションサーバーで設定できます。詳しくは、アプリケーションサーバーに付属するマニュアルを参照してください。
