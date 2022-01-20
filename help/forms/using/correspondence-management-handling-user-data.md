---
title: Correspondence Management | ユーザーデータの処理
seo-title: Correspondence Management | Handling user data
description: AEM Forms Correspondence Management を使用すると、顧客向けに安全でパーソナル化された通信を作成して管理し、効率性を向上できます。AEMリポジトリでドラフトおよび送信済みレターのデータの保存を設定し、保存済みデータにアクセスして、保存済みデータを削除する方法について説明します。
seo-description: AEM Forms Correspondence Management enables you to create, manage, and streamline secure and personalized customer correspondences. Learn how to configure storing data for draft and submitted letters in AEM repository, access stored data, and delete stored data.
uuid: d5bb190b-d668-4da3-95da-b7705ad302d9
topic-tags: grdp
products: SG_EXPERIENCEMANAGER/6.4/FORMS
discoiquuid: 764d8e0d-604d-4c7b-89cd-7686ce5f03ff
role: Admin
exl-id: 4a6b3403-2941-4098-bb30-769281adedc2
source-git-commit: 3c050c33a384d586d74bd641f7622989dc1d6b22
workflow-type: tm+mt
source-wordcount: '572'
ht-degree: 78%

---

# Correspondence Management | ユーザーデータの処理 {#correspondence-management-handling-user-data}

AEM Forms Correspondence Management を使用すると、顧客向けに安全でパーソナル化された通信を作成して管理し、効率性を向上できます。ビジネスユーザー向けに直感的なユーザーインターフェイスを提供し、事前に承認されたコンテンツブロックとメディア要素を使用して通信を作成できるようにします。通信の作成について詳しくは、 [通信を作成](/help/forms/using/create-correspondence.md).

ビジネスユーザーまたはエージェントが通信をドラフトとして格納したり送信したりする場合、レターインスタンスが AEM リポジトリに格納されます。レターインスタンスには、通信データとメタデータが含まれます。

>[!NOTE]
>
>AEM 6.4 Forms では、通信の管理は初期状態では使用できません。以前のバージョンの AEM Forms からアップグレードする場合は、互換パッケージをインストールして Correspondence Management のアセットを移行し、AEM 6.4 Forms で引き続き使用できるようにします。詳しくは、「[互換パッケージ](/help/forms/using/compatibility-package.md)」を参照してください。

## ユーザーデータとデータストア {#data}

Correspondence Management では、発行インスタンスがレターインスタンスを管理するように設定されている場合にのみ、ドラフトのデータおよび送信済みレターのデータが AEM リポジトリに格納されます。この設定について詳しくは、「[Correspondence Management 設定プロパティ](/help/forms/using/cm-configuration-properties.md)」を参照してください。

AEM デプロイメント用に設定されたデータストアの永続性に応じて、ドラフトおよび送信済み通信データは次の場所に格納されます。

<table> 
 <tbody>
  <tr>
   <td><p><strong>永続性タイプ</strong></p> </td> 
   <td><p><strong>データストア</strong></p> </td> 
   <td><p><strong>場所</strong></p> </td> 
  </tr>
  <tr>
   <td><p>デフォルト</p> </td> 
   <td><p>逆複製設定で指定された発行インスタンスおよびオーサーインスタンスの AEM リポジトリ</p> </td> 
   <td><p><code>/content/apps/cm/letterInstances/[yyyy]/[mm]/[dd]/[node-id]/[letter-instance-name]/</code> </p> </td> 
  </tr>
  <tr>
   <td><p>リモート</p> </td> 
   <td><p>オーサーインスタンスを処理するリモートの AEM リポジトリ</p> </td> 
   <td><p><code>/content/apps/cm/letterInstances/[yyyy]/[mm]/[dd]/[node-id]/[letter-instance-name]/</code></p> </td> 
  </tr>
 </tbody>
</table>

上記の AEM リポジトリの場所で：

* `[yyyy]/[mm]/[dd]` は、レターインスタンスが作成された日付に基づくノード構造です
* `[node-id]` は、レターを含むフォルダーに割り当てられた ID です
* `[letter-instance-name]` は、レターを保存または送信する際に指定された名前です

以下 [letter-instance-name] ノードの場合は、次のノード構造が作成され、各レターインスタンスのデータがAEMリポジトリに保存されます。

| ノード | 説明 |
|---|---|
| `extendedProperties` | レターインスタンスのメタデータのプロパティを格納します。 |
| `dataXML` | 通信データを含むダウンロード可能な dataXML ファイルをバイナリ形式で格納します。 |
| `processedXDP` | 送信済みレターを作成するために使用される XDP テンプレートの詳細が含まれています。このノードは、送信された通信に対してのみ作成されます。 |
| `submittedLetter` | 送信済みレターデータをダウンロード可能なバイナリ形式で格納します。このノードは、送信された通信に対してのみ作成されます。 |

## ユーザーデータへのアクセスと削除 {#access-and-delete-user-data}

設定されたデータストアのドラフトおよび送信済み通信データにアクセスし、必要に応じて削除することができます。

### ユーザーデータへのアクセス {#access-user-data}

Correspondence Management には、ドラフトおよび送信済みレターインスタンスを検索してアクセスするために使用できる API が用意されています。API を使用すると、レターインスタンス ID または通信を保存または送信したユーザーを使用して、レターインスタンスを検索して開くことができます。詳しくは、 [レターインスタンスにアクセスする API](/help/forms/using/cm-apis-to-access-letter-instances.md).

または、CRX DELite を使用して AEM リポジトリのレターインスタンスに移動することもできます。格納されたデータおよびリポジトリの場所について詳しくは、「[ユーザーデータとデータストア](/help/forms/using/correspondence-management-handling-user-data.md#data)」を参照してください。

### ユーザーデータの削除 {#delete-user-data}

特定ユーザーのデータを含むレターインスタンスを検索するには、次の操作を実行します。

* レターインスタンス名、ドラフトを保存したユーザー、または通信を送信したユーザーが分かっている場合は、Correspondence Management の API を使用します
* 電子メール ID や名前などの個人を特定できる情報を使用してAEMリポジトリ検索を使用し、情報が保存されるノードを検索します

AEM システムでドラフトおよび送信済み通信に含まれるユーザーデータを完全に削除するには、適用可能なすべての AEM インスタンスからレターインスタンスノードを手動で削除する必要があります。
