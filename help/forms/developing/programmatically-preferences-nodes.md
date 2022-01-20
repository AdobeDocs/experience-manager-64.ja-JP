---
title: PreferencesNodes をプログラムで管理する
seo-title: Programmatically managing the PreferencesNodes
description: Preferences Manager Service API(Java) を使用して、Preferences ノードをプログラムで管理します。
seo-description: Use the Preferences Manager Service API (Java) to programmatically manage the Preferences Nodes.
uuid: f0cb117a-a6cc-4ca5-8511-b3bc9f6738e9
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.4/FORMS
topic-tags: operations
discoiquuid: 9d4dba7f-49d8-4112-bc8a-04dafc99a936
role: Developer
exl-id: d580b32c-a344-4a8c-bd61-0949da76d981
source-git-commit: bd94d3949f0117aa3e1c9f0e84f7293a5d6b03b4
workflow-type: tm+mt
source-wordcount: '231'
ht-degree: 0%

---

# 環境設定ノードをプログラムで管理する {#programmatically-managing-the-preferencesnodes}

このトピックでは、Preferences Manager Service API(Java) を使用して、Preferences ノードをプログラムで管理する方法について説明します。

構成設定は、Administrator UI から手動で変更できます。 オプションを変更するには、次に移動します。 `Home>Settings>User Management> Configuration>Manual Configuration`. インポート `config.xml` 変更を加えた後、ノードで行われた変更以外のすべての変更に気がつきます。 `/Adobe/Adobe Experience Manager Forms/Config/UM persist` が失われました。 User Management の読み込みと書き出しのプレビューでは、他のコンポーネントの設定の変更はサポートされていません。 現在は、 `PreferencesManagerServiceClient` API

**手順の概要**&#x200B;プログラムによって環境設定ノードを管理するには、次の手順を実行します。

1. プロジェクトファイルを含めます。
1. PreferencesManagerService クライアントの作成
1. 適切な役割または権限の操作を呼び出す

**プロジェクトファイルを含める**

開発プロジェクトに必要なファイルを含めます。 Java を使用してクライアントアプリケーションを作成する場合は、必要な JAR ファイルを含めます。 Web サービスを使用している場合は、プロキシファイルを必ず含めてください。

**PreferencesManagerService クライアントの作成**

User Management PreferencesManagerService 操作をプログラムで実行する前に、PreferencesManagerService クライアントを作成する必要があります。 Java API を使用すると、PreferencesManagerServiceClient オブジェクトを作成することでこれを実現できます。

**適切な役割または権限の操作を呼び出す**

サービスクライアントを作成したら、Preferences Manager 操作を呼び出すことができます。 サービスクライアントを使用すると、権限の読み取りと設定が可能です。
