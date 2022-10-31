---
title: JSON スキーマを使用したアダプティブフォームの作成
seo-title: Creating adaptive forms using JSON Schema
description: アダプティブフォームではフォームモデルとして JSON スキーマを使用できるため、アダプティブフォームの作成に既存の JSON スキーマを活用できます。
seo-description: Adaptive forms can use JSON schema as form model, allowing you to leverage existing JSON schemas to create adaptive forms.
uuid: e73b4b4c-6ad7-4400-b776-5892549970c3
topic-tags: develop
products: SG_EXPERIENCEMANAGER/6.4/FORMS
discoiquuid: bcda96ff-6c7d-46c4-a9e8-7e0fb245cde9
feature: Adaptive Forms
exl-id: 42c41625-7441-479c-bd07-7e96e867cc0a
source-git-commit: bd94d3949f0117aa3e1c9f0e84f7293a5d6b03b4
workflow-type: tm+mt
source-wordcount: '1207'
ht-degree: 86%

---

# JSON スキーマを使用したアダプティブフォームの作成 {#creating-adaptive-forms-using-json-schema}

## 前提条件 {#prerequisites}

フォームモデルとして JSON スキーマを使用してアダプティブフォームをオーサリングする場合、JSON スキーマの基本を理解している必要があります。この記事を読む前に、以下のコンテンツを読んでおくことをお勧めします。

* [アダプティブフォームの作成](/help/forms/using/creating-adaptive-form.md)
* [JSON スキーマ](https://json-schema.org/)

## フォームモデルとしての JSON スキーマの使用  {#using-a-json-schema-as-form-model}

AEM Forms では、既存の JSON スキーマをフォームモデルとして使用したアダプティブフォームの作成がサポートされています。JSON スキーマは、組織内のバックエンドシステムによってデータが作成または使用される構造を表します。使用する JSON スキーマは、[v4 仕様](https://json-schema.org/draft-04/schema)に準拠している必要があります。

JSON スキーマの使用の主な特長は、次のとおりです。

* JSON の構造は、アダプティブフォームのオーサリングモードの「コンテンツファインダー」タブでツリーとして表示されます。JSON 階層からアダプティブフォームに要素をドラッグして追加できます。
* 関連付けられたスキーマに準拠する JSON を使用して、フォームに事前入力できます。
* ユーザーが入力したデータは、送信時には関連付けられたスキーマに適合する JSON として送信されます。

JSON スキーマは、単純型要素と複合型要素で構成されています。要素には、その要素にルールを追加する属性が含まれています。これらの要素や属性がアダプティブフォーム上にドラッグされると、自動的に該当するアダプティブフォームコンポーネントにマッピングされます。

JSON 要素とアダプティブフォームコンポーネントのマッピングは、次のように行われます。

<table> 
 <tbody> 
  <tr> 
   <th><strong>JSON の要素、プロパティ、属性</strong></th> 
   <th><strong>アダプティブフォームコンポーネント</strong></th> 
  </tr> 
  <tr> 
   <td><p>enum および enumNames 制約を含む string プロパティ。</p> <p>構文</p> <p> <code>{</code></p> <p><code>"type" : "string",</code></p> <p><code>"enum" : ["M", "F"]</code></p> <p><code>"enumNames" : ["Male", "Female"]</code></p> <p><code>}</code></p> <p> </p> </td> 
   <td><p>ドロップダウンコンポーネント：</p> 
    <ul> 
     <li>enumNames にリストされた値はドロップボックスに表示されます。</li> 
     <li>enum にリストされた値は計算に使用されます。</li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td><p>format 制約を含む string プロパティ。例えば、電子メール、日付など。</p> <p>構文</p> <p><code>{</code></p> <p><code>"type" : "string",</code></p> <p><code>"format" : "email"</code></p> <p><code>}</code></p> <p> </p> </td> 
   <td> 
    <ul> 
     <li>type が string で format が email の場合、電子メールコンポーネントがマップされます。</li> 
     <li>type が string で format が hostname の場合、検証を含むテキストボックスコンポーネントがマップされます。</li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td><p>{</p> <p>"type" : "string",</p> <p>}</p> </td> 
   <td><br /> <br /> テキストフィールド<br /> <br /> <br /> </td> 
  </tr> 
  <tr> 
   <td>number プロパティ<br /> </td> 
   <td>サブタイプが float に設定された数値フィールド<br /> </td> 
  </tr> 
  <tr> 
   <td>integer プロパティ<br /> </td> 
   <td>サブタイプが integer に設定された数値フィールド<br /> </td> 
  </tr> 
  <tr> 
   <td>boolean プロパティ<br /> </td> 
   <td>切り替え<br /> </td> 
  </tr> 
  <tr> 
   <td>object プロパティ<br /> </td> 
   <td>パネル<br /> </td> 
  </tr> 
  <tr> 
   <td>array プロパティ</td> 
   <td>minItems および maxItems にそれぞれ等しい min および max を持つ繰り返し可能なパネル。同種の配列のみがサポートされます。そのため、項目制限は、配列でなくオブジェクトである必要があります。<br /> </td> 
  </tr> 
 </tbody> 
</table>

### 共通のスキーマプロパティ {#common-schema-properties}

アダプティブフォームは JSON スキーマで使用可能な情報を使用して、生成された各フィールドをマッピングします。具体的には、以下のようになります。

* title プロパティは、アダプティブフォームコンポーネントのラベルとして機能します。
* description プロパティは、アダプティブフォームコンポーネントの詳細な説明として設定されます。
* default プロパティは、アダプティブフォームフィールドの初期値として機能します。
* maxLength プロパティは、テキストフィールドコンポーネントの maxlength 属性として設定されます。
* minimum、maximum、exclusiveMinimum および exclusiveMaximum プロパティは、数値ボックスコンポーネントに使用されます。
* DatePicker コンポーネントの範囲をサポートするために、JSON スキーマの追加のプロパティ minDate および maxDate が提供されます。
* minItems プロパティと maxItems プロパティを使用して、パネルコンポーネントに追加または削除できる項目/フィールドの数を制限します。
* readOnly プロパティは、アダプティブフォームコンポーネントの readonly 属性を設定します。
* 必須プロパティはアダプティブフォームフィールドを必須としてマークします。一方、パネル（タイプはオブジェクト）の場合、最終的に送信される JSON データは、そのオブジェクトに対応する空の値を持つフィールドを持ちます。
* pattern プロパティは、アダプティブフォームの検証パターン（正規表現）として設定されます。
* JSON スキーマファイルの拡張子は、.schema.json を維持する必要があります。例えば、&lt;filename>.schema.json のように指定します。

## JSON スキーマのサンプル {#sample-json-schema}

JSON スキーマの例を示します。

```
{
 "$schema": "https://json-schema.org/draft-04/schema#",
 "definitions": {
  "employee": {
   "type": "object",
   "properties": {
    "userName": {
     "type": "string"
    },
    "dateOfBirth": {
     "type": "string",
     "format": "date"
    },
    "email": {
     "type": "string",
     "format": "email"
    },
    "language": {
     "type": "string"
    },
    "personalDetails": {
     "$ref": "#/definitions/personalDetails"
    },
    "projectDetails": {
     "$ref": "#/definitions/projectDetails"
    }
   },
   "required": [
    "userName",
    "dateOfBirth",
    "language"
   ]
  },
  "personalDetails": {
   "type": "object",
   "properties": {
    "GeneralDetails": {
     "$ref": "#/definitions/GeneralDetails"
    },
    "Family": {
     "$ref": "#/definitions/Family"
    },
    "Income": {
     "$ref": "#/definitions/Income"
    }
   }
  },
  "projectDetails": {
   "type": "array",
   "items": {
    "properties": {
     "name": {
      "type": "string"
     },
     "age": {
      "type": "number"
     },
     "projects": {
      "$ref": "#/definitions/projects"
     }
    }
   },
   "minItems": 1,
   "maxItems": 4
  },
  "projects": {
   "type": "array",
   "items": {
    "properties": {
     "name": {
      "type": "string"
     },
     "age": {
      "type": "number"
     },
     "projectsAdditional": {
      "$ref": "#/definitions/projectsAdditional"
     }
    }
   },
   "minItems": 1,
   "maxItems": 4
  },
  "projectsAdditional": {
   "type": "array",
   "items": {
    "properties": {
     "Additional_name": {
      "type": "string"
     },
     "Additional_areacode": {
      "type": "number"
     }
    }
   },
   "minItems": 1,
   "maxItems": 4
  },
  "GeneralDetails": {
   "type": "object",
   "properties": {
    "age": {
     "type": "number"
    },
    "married": {
     "type": "boolean"
    },
    "phone": {
     "type": "number",
     "aem:afProperties": {
      "sling:resourceType": "/libs/fd/af/components/guidetelephone",
      "guideNodeClass": "guideTelephone"
     }
    },
    "address": {
     "type": "string"
    }
   }
  },
  "Family": {
   "type": "object",
   "properties": {
    "spouse": {
     "$ref": "#/definitions/spouse"
    },
    "kids": {
     "$ref": "#/definitions/kids"
    }
   }
  },
  "Income": {
   "type": "object",
   "properties": {
    "monthly": {
     "type": "number"
    },
    "yearly": {
     "type": "number"
    }
   }
  },
  "spouse": {
   "type": "object",
   "properties": {
    "name": {
     "type": "string"
    },
    "Income": {
     "$ref": "#/definitions/Income"
    }
   }
  },
  "kids": {
   "type": "array",
   "items": {
    "properties": {
     "name": {
      "type": "string"
     },
     "age": {
      "type": "number"
     }
    }
   },
   "minItems": 1,
   "maxItems": 4
  }
 },
 "type": "object",
 "properties": {
  "employee": {
   "$ref": "#/definitions/employee"
  }
 }
}
```

### 再使用可能なスキーマ定義 {#reusable-schema-definitions}

定義キーを使用して、再使用可能なスキーマを識別します。再使用可能なスキーマ定義を使用して、フラグメントを作成します。これは、XSD での複合型の識別と同じです。定義を含む JSON スキーマのサンプルを以下に示します。

```
{
  "$schema": "https://json-schema.org/draft-04/schema#",
 
  "definitions": {
    "address": {
      "type": "object",
      "properties": {
        "street_address": { "type": "string" },
        "city":           { "type": "string" },
        "state":          { "type": "string" }
      },
      "required": ["street_address", "city", "state"]
    }
  },
 
  "type": "object",
 
  "properties": {
    "billing_address": { "$ref": "#/definitions/address" },
    "shipping_address": { "$ref": "#/definitions/address" }
  }
}
```

上記の例では、各顧客が出荷先と請求先の両方の住所を持つ顧客レコードを定義します。どちらの住所も構造（都道府県、市区町村、番地など）が同じ場合は、住所が重複しないようにすることをお勧めします。また、今後変更が行われたときに、簡単にフィールドを追加したり削除したりできます。

## JSON スキーマ定義でのフィールドの事前設定 {#pre-configuring-fields-in-json-schema-definition}

**aem:afProperties** プロパティを使用して JSON スキーマのフィールドを事前構成し、カスタムのアダプティブフォームコンポーネントにマップできます。以下に例を示します。

```
{
    "properties": {
        "sizeInMB": {
            "type": "integer",
            "minimum": 16,
            "maximum": 512,
            "aem:afProperties" : {
                 "sling:resourceType" : "/apps/fd/af/components/guideTextBox",
                 "guideNodeClass" : "guideTextBox"
             }
        }
    },
    "required": [ "sizeInMB" ],
    "additionalProperties": false
}
```

## アダプティブフォームコンポーネントで許容される値の制限 {#limit-acceptable-values-for-an-adaptive-form-component}

JSON スキーマの要素に次の制限を追加して、アダプティブフォームコンポーネントで許容される値を制限できます。

<table> 
 <tbody> 
  <tr> 
   <td><p><strong> スキーマプロパティ</strong></p> </td> 
   <td><p><strong>データタイプ</strong></p> </td> 
   <td><p><strong>説明</strong></p> </td> 
   <td><p><strong>コンポーネント</strong></p> </td> 
  </tr> 
  <tr> 
   <td><p><code>maximum</code></p> </td> 
   <td><p>文字列</p> </td> 
   <td><p>数値および日付の上限を指定します。デフォルトでは、最大値が含まれます。</p> </td> 
   <td> 
    <ul> 
     <li>数値ボックス</li> 
     <li>数値ステッパー<br /> </li> 
     <li>日付選択</li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td><p><code>minimum</code></p> </td> 
   <td><p>文字列</p> </td> 
   <td><p>数値および日付の下限を指定します。デフォルトでは、最小値が含まれます。</p> </td> 
   <td> 
    <ul> 
     <li>数値ボックス</li> 
     <li>数値ステッパー</li> 
     <li>日付選択</li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td><p><code>exclusiveMaximum</code></p> </td> 
   <td><p>ブール値</p> </td> 
   <td><p>true の場合、フォームのコンポーネントで指定された数値または日付は、maximum プロパティに指定された数値または日付よりも小さい値である必要があります。</p> <p>false の場合、フォームのコンポーネントで指定された数値または日付は、maximum プロパティに指定された数値または日付以下の値である必要があります。</p> </td> 
   <td> 
    <ul> 
     <li>数値ボックス</li> 
     <li>数値ステッパー</li> 
     <li>日付選択</li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td><p><code>exclusiveMinimum</code></p> </td> 
   <td><p>ブール値</p> </td> 
   <td><p>true の場合、フォームのコンポーネントで指定された数値または日付は、minimum プロパティに指定された数値または日付よりも大きい値である必要があります。</p> <p>false の場合、フォームのコンポーネントで指定された数値または日付は、minimum プロパティに指定された数値または日付以上の値である必要があります。</p> </td> 
   <td> 
    <ul> 
     <li>数値ボックス</li> 
     <li>数値ステッパー</li> 
     <li>日付選択</li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td><p><code>minLength</code></p> </td> 
   <td><p>文字列</p> </td> 
   <td><p>コンポーネントで許可される最小文字数を指定します。最小の長さは 0 以上である必要があります。</p> </td> 
   <td> 
    <ul> 
     <li>テキストボックス</li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td><code>maxLength</code></td> 
   <td>文字列</td> 
   <td>コンポーネントで許可される最大文字数を指定します。最大の長さは 0 以上である必要があります。</td> 
   <td> 
    <ul> 
     <li>テキストボックス</li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td><p><code>pattern</code></p> </td> 
   <td><p>文字列</p> </td> 
   <td><p>文字のシーケンスを指定します。文字が指定されたパターンに適合すると、コンポーネントはその文字を受け入れます。</p> <p>この pattern プロパティは、対応するアダプティブフォームコンポーネントの検証パターンにマッピされます。</p> </td> 
   <td> 
    <ul> 
     <li>XSD スキーマにマップされるすべてのアダプティブフォームコンポーネント </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td>maxItems</td> 
   <td>文字列</td> 
   <td>配列の項目の最大数を指定します。項目の最大数は 0 以上である必要があります。</td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>minItems</td> 
   <td>文字列</td> 
   <td>配列の項目の最小数を指定します。項目の最小数は 0 以上である必要があります。</td> 
   <td> </td> 
  </tr> 
 </tbody> 
</table>

## サポート対象外の構成  {#non-supported-constructs}

アダプティブフォームは以下の JSON スキーマ構成をサポートしていません。

* Null タイプ
* any などの Union タイプ
* OneOf、AnyOf、AllOf、NOT
* 同種の配列のみがサポートされます。そのため、項目制限は、配列でなくオブジェクトである必要があります。

## よくある質問 {#frequently-asked-questions}

**繰り返し可能なサブフォーム（minOccurs 値または maxOccurs 値が 1 より大きい）では、サブフォーム（任意の複合型から生成された構造）の個々の要素をドラッグできないのはなぜですか？**

繰り返し可能なサブフォームでは、完全なサブフォームを使用する必要があります。選択した一部のフィールドのみを使用する場合は、構造全体を使用し、不要部分を削除します。

**コンテンツファインダーに長く複雑な構造があります。特定の要素を見つけるにはどうすればよいですか？**

以下の 2 つのオプションがあります。

* ツリー構造をスクロールする
* 検索ボックスを使用して、要素を検索する
