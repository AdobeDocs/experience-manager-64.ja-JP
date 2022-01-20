---
title: レターインスタンスにアクセスするための API
seo-title: APIs to access letter instances
description: レターインスタンスにアクセスするための API を使用する方法について説明します。
seo-description: Learn how to use APIs to access letter instances.
uuid: e7fb7798-f49d-458f-87f5-22df5f3e7d10
content-type: reference
products: SG_EXPERIENCEMANAGER/6.4/FORMS
topic-tags: correspondence-management
discoiquuid: 9c27f976-972a-4250-b56d-b84a7d72f8c8
feature: Correspondence Management
exl-id: 64ca6baa-5534-4227-a969-fb67cc6eb207
source-git-commit: bd94d3949f0117aa3e1c9f0e84f7293a5d6b03b4
workflow-type: tm+mt
source-wordcount: '578'
ht-degree: 57%

---

# レターインスタンスにアクセスするための API {#apis-to-access-letter-instances}

## 概要 {#overview}

Correspondence Management の「通信を作成」UI を使用して、作成中のレターインスタンスのドラフトを保存することができます。また、この UI には送信済みのレターインスタンスが存在します。

Correspondence Management には、送信済みまたはドラフトのレターインスタンスを取り扱うための一覧表示インターフェイスを構築できる API が用意されています。この API は、エージェントの送信済みおよびドラフトのレターインスタンスを一覧表示して開き、エージェントがドラフトまたは送信済みのレターインスタンスで作業を続行できるようにします。

## レターインスタンスの取得 {#fetching-letter-instances}

Correspondence Management は API を使用して、LetterInstanceService サービスからレターインスタンスを取得します。

| メソッド | 説明 |
|--- |--- |
| getAllLetterInstances | 入力クエリパラメーターに基づいてレターインスタンスを取得します。 すべてのレターインスタンスを取得するには、クエリパラメーターをヌルとして渡します。 |
| getLetterInstance | レターインスタンス ID に基づいて指定したレターインスタンスを取得します。 |
| letterInstanceExists | LetterInstance が指定した名前で存在するかどうかをチェックします。 |

>[!NOTE]
>
>LetterInstanceService は OSGI サービスで、Java で@Referenceを使用してインスタンスを取得できます\
>クラスまたは sling.getService(LetterInstanceService. クラス ) を JSP で使用します。

### getAllLetterInstances の使用 {#using-nbsp-getallletterinstances}

下記の API は、クエリオブジェクトに基づいてレターインスタンスを検索します（送信済みとドラフトの両方）。クエリオブジェクトが null の場合は、すべてのレターインスタンスを返します。 この API は、 [LetterInstanceVO](https://helpx.adobe.com/experience-manager/6-2/forms/javadocs/com/adobe/icc/dbforms/obj/LetterInstanceVO.html) レターインスタンスの追加情報を抽出するために使用できるオブジェクト

**構文**: `List getAllLetterInstances(Query query) throws ICCException;`

<table> 
 <tbody> 
  <tr> 
   <td><strong>パラメーター</strong></td> 
   <td><strong>説明</strong></td> 
  </tr> 
  <tr> 
   <td>query</td> 
   <td>query パラメーターは、レターインスタンスの検索またはフィルタリングに使用されます。ここでは、クエリはオブジェクトの最上位の属性/プロパティのみをサポートします。 クエリは、ステートメントで構成されます。ステートメントのオブジェクトで使用される「attributeName」は、レターインスタンスオブジェクト内のプロパティの名前です。<br /> </td> 
  </tr> 
 </tbody> 
</table>

#### 例 1：送信済みタイプのすべてのレターインスタンスを取得する {#example-fetch-all-the-letter-instances-of-type-submitted}

以下のコードで送信済みのレターインスタンスの一覧が返されます。下書きのみを取得するには、 `LetterInstanceType.COMPLETE.name()` から `LetterInstanceType.DRAFT.name().`

```java
@Reference
LetterInstanceService letterInstanceService;
Query query = new Query();
 
List<LetterInstanceVO> submittedLetterInstances = new ArrayList<LetterInstanceVO>();
 
Statement statementForInstanceType = new Statement();
statementForInstanceType.setAttributeName("letterInstanceType");
statementForInstanceType.setOperator(Operator.EQUALS);
statementForInstanceType.setAttributeValue(LetterInstanceType.COMPLETE.name());
query.addStatement(statementForInstanceType);
submittedLetterInstances = letterInstanceService.getAllLetterInstances(query);
```

#### 例 2：特定のユーザーによって送信されたドラフトタイプのすべてのレターインスタンスを取得する {#example-nbsp-fetch-all-the-letter-instances-submitted-by-a-user-and-letter-instance-type-is-draft}

次のコードは、同じクエリ内に複数のステートメントを持ち、異なる条件 ( ユーザーが送信したレターインスタンス（属性 submittedby）など ) に基づいて結果をフィルタリングし、letterInstanceType のタイプが DRAFT の場合など ) を取得します。

```java
@Reference
LetterInstanceService letterInstanceService;
 
String submittedBy = "tglodman";
Query query = new Query();
 
List<LetterInstanceVO> submittedLetterInstances = new ArrayList<LetterInstanceVO>();
 
Statement statementForInstanceType = new Statement();
statementForInstanceType.setAttributeName("letterInstanceType");
statementForInstanceType.setOperator(Operator.EQUALS);
statementForInstanceType.setAttributeValue(LetterInstanceType.COMPLETE.name());
query.addStatement(statementForInstanceType);
 
Statement statementForSubmittedBy = new Statement();
statementForSubmittedBy .setAttributeName("submittedby");
statementForSubmittedBy .setOperator(Operator.EQUALS);
statementForSubmittedBy .setAttributeValue(submittedBy);
query.addStatement(statementForSubmittedBy );
submittedLetterInstances = letterInstanceService.getAllLetterInstances(query);
```

### getLetterInstance の使用 {#using-nbsp-getletterinstance}

特定のレターインスタンス ID で識別されるレターインスタンスを取得します。インスタンス ID が一致しない場合は、「 null 」を返します。

**構文：** `public LetterInstanceVO getLetterInstance(String letterInstanceId) throws ICCException;`

```java
@Reference
LetterInstanceService letterInstanceService;
String letterInstanceId = "/content/apps/cm/letterInstances/1001/sampleLetterInstance";
LetterInstanceVO letterInstance = letterInstanceService.getLetterInstance(letterInstanceId );
```

### レターインスタンスの有無の確認 {#verifying-if-letterinstance-exist}

レターインスタンスが指定した名前で存在するかどうかを確認します

**構文**: `public Boolean letterInstanceExists(String letterInstanceName) throws ICCException;`

| **パラメーター** | **説明** |
|---|---|
| letterInstanceName | 有無を確認するレターインスタンスの名前。 |

```java
@Reference
LetterInstanceService letterInstanceService;
String letterInstanceName = "sampleLetterInstance";
Boolean result = letterInstanceService.letterInstanceExists(letterInstanceName );
```

## レターインスタンスを開く {#opening-letter-instances}

レターインスタンスには、送信済みタイプまたはドラフトタイプがあります。両タイプのレターインスタンスを開くと、それぞれ異なる動作を示します。

* 送信済みのレターインスタンスの場合、レターインスタンスを示す PDF が開きます。サーバー上に残存する送信済みのレターインスタンスにも dataXML と処理された XDP が含まれ、それらを PDF/A の作成のようなケースの実行やカスタマイズに使用することができます。
* ドラフトレターインスタンスの場合、通信を作成用 UI が正確に前の状態に再読み込みされます。これは、ドラフトが作成された時点の状態です。

### ドラフトのレターインスタンスを開く {#opening-draft-letter-instance-nbsp}

CCR UI  は、再読み込みされたレターに使用できる cmLetterInstanceId パラメータをサポートしています。

`https://[hostName]:[portNo]/[contextPath]//aem/forms/createcorrespondence.html?random=[randomNo]&cmLetterInstanceId=[letterInstanceId]`

>[!NOTE]
>
>通信の再読み込み時に cmLetterId または cmLetterName/State/Version を指定する必要はありません。再読み込みされた通信に関するすべての詳細が、送信済みのデータに既に含まれているからです。 RandomNo は、ブラウザーのキャッシュの問題を回避するために使用されます。タイムスタンプを乱数として使用できます。

### 送信済みのレターインスタンスを開く {#opening-submitted-letter-instance}

送信済み PDF は、次のレターインスタンス ID を使用して直接開くことができます。

`https://[hostName]:[portNo]/[contextPath]/[letterInstanceId]`
