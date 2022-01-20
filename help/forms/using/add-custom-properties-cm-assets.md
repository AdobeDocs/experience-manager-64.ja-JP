---
title: Correspondence Management アセットへのカスタムプロパティの追加
seo-title: Add custom properties to Correspondence Management assets
description: Correspondence Management アセットへのカスタムプロパティの追加方法について説明します。
seo-description: Learn how to add custom properties to Correspondence Management assets.
uuid: 64b3f92b-6144-4633-b61d-b1a33e263148
content-type: reference
topic-tags: correspondence-management
products: SG_EXPERIENCEMANAGER/6.4/FORMS
discoiquuid: 601108d8-f432-4a6b-9ec9-831cf054e52f
feature: Correspondence Management
exl-id: d58c2468-3e77-41a0-a2ba-c19912c77f73
source-git-commit: bd94d3949f0117aa3e1c9f0e84f7293a5d6b03b4
workflow-type: tm+mt
source-wordcount: '4443'
ht-degree: 66%

---

# Correspondence Management アセットへのカスタムプロパティの追加 {#add-custom-properties-to-correspondence-management-assets}

## 概要 {#overview}

Correspondence Management ユーザーインターフェイスをカスタマイズし、調整したプロパティとタブのセットをユーザーに提示できます。このカスタマイズには、特定のアセットタイプ/レター、またはすべてのアセットタイプ/レターにカスタムフィールド/プロパティとタブを追加することが含まれます。

## Correspondence Management アセットへのカスタムプロパティの追加 {#adding-custom-properties-to-correspondence-management-assets}

以下のシナリオで、Correspondence Management アセットおよびレターにプロパティ／タブを追加する方法について説明します。

* すべてのアセットタイプへの共通プロパティの追加
* すべてのアセットタイプへの共通タブの追加
* 特定のアセットタイプへのカスタムプロパティの追加

これらのシナリオでプロパティ、パスおよび値を調整することにより、要件に従い、様々なアセットのセットにカスタムプロパティおよびタブを追加できます。

### シナリオ：すべてのアセットタイプへの共通フィールド（プロパティ）の追加 {#scenario-adding-a-common-field-property-to-all-the-asset-types}

このシナリオでは、すべてのアセットタイプ（テキスト、リスト、条件およびレイアウトフラグメント）およびレターにカスタムプロパティを追加する方法について説明します。このシナリオを使用して、すべてのアセットとレターにプロパティ「受信者の場所」を追加できます。 Location of recipients プロパティは、配信のどの地域に関連しているかを識別するのに役立ちます。

>[!NOTE]
>
>カスタムプロパティを追加すると、プロパティはアセット作成ページに表示されるようになります。このようなプロパティを非表示にする方法については、「アセット作成ページとプロパティページでのカスタムプロパティの表示／非表示」を参照してください。

![すべてのアセットタイプに追加されたカスタムプロパティ](assets/lcoationofrecipientsui.png)

すべてのアセットタイプおよびレターにカスタムプロパティを追加するには、次の手順を実行します。

1. に移動します。 `https://[server]:[port]/[ContextPath]/crx/de` 管理者としてログインします。
1. 次の手順に従って、apps フォルダーに、（ccrui フォルダー内の）css フォルダーに似たパス/構造で css という名前のフォルダーを作成します。

   1. 次のパスにある items フォルダを右クリックし、を選択します。 **ノードをオーバーレイ**:

      `/libs/fd/cm/ma/gui/content/cmmetadataproperties/commonproperties/col1/items`

      ![ノードをオーバーレイ](assets/itemsoverlaynode.png)

   1. ノードをオーバーレイダイアログに次の値が表示されていることを確認します。

      **パス：** /libs/fd/cm/ma/gui/content/cmmetadataproperties/commonproperties/col1/items

      **場所：** /apps/

      **ノードタイプを一致させる：** 選択済み

      ![ノードをオーバーレイ](assets/cmmetapropertiesoverlaynode.png)

   1. 「**OK**」をクリックします。apps フォルダーにフォルダー構造が作成されます。

   1. 「**すべて保存**」をクリックします。

1. 新しく作成された items フォルダーの下に、すべてのアセットのカスタムプロパティ用のノードを追加します ( 例：GeoLocation) を次の手順で使用します。

   1. items フォルダーを右クリックして、「**作成**／**ノードを作成**」を選択します。

      ![CRX でのノードの作成](assets/itemscreatenode.png)

   1. ノードを作成ダイアログに次の値が表示されていることを確認し、「**OK**」をクリックします。

      **名前：** GeoLocation （またはこのプロパティに与える任意の名前）

      **タイプ：** nt:unstructured

      ![ノードを作成：GeoLocation](assets/geographicallocationcreatenode.png)

   1. 作成した新しいノード（ここでは「GeoLocation」）をクリックします。CRX にノードのプロパティが表示されます。
   1. このノード（ここでは「GeoLocation」）に次のプロパティを追加します。

      | **名前** | **種類** | **値** |
      |---|---|---|
      | fieldLabel | 文字列 | フィールド／プロパティに与える任意の名前。（ここでは「Location of recipients」） |
      | name | 文字列 | `./extendedproperties/GeoLocation` （値は、items ノードで作成したフィールド名と同じにします）。 |
      | renderReadOnly | ブール値 | true |
      | sling:resourceType | 文字列 | granite/ui/components/coral/foundation/form/textfield |

   1. 「**すべて保存**」をクリックします。

1. カスタマイズ内容を表示するには、アセット（テキスト、リスト、条件またはレイアウトフラグメント）またはレターの上にカーソルを置き、「**プロパティを表示**」をクリックし、「**編集**」をクリックします。新しいフィールド（Location of recipients）がアセット／レタープロパティの「基本」タブに表示されます。

   >[!NOTE]
   >
   >カスタマイズ内容を UI に表示するには、ブラウザーのキャッシュをクリアする必要が生じる場合があります。

   ![すべてのアセットに追加されたカスタムプロパティ](assets/lcoationofrecipientsui-1.png)

   >[!NOTE]
   >
   >すべてのアセットに追加する共通プロパティは、アセットプロパティの「基本」タブに表示されます。デフォルトでは、すべてのアセットに追加する共通プロパティは、プロパティページおよびアセット作成ページに表示されます。共通のプロパティを非表示にするには、次の手順を実行します。 `[link to show / hide properties]`.

### シナリオ：カスタムプロパティ／フィールドへのカスタムドロップダウンおよび値の追加 {#scenario-add-custom-drop-down-and-values-to-a-custom-property-field}

このシナリオでは、すべてのアセットタイプにカスタムプロパティを追加し、そのドロップダウン値を追加する方法について説明します。

1. 次のパスにある items フォルダを右クリックし、を選択します。 **ノードをオーバーレイ**:

   `/libs/fd/cm/ma/gui/content/cmmetadataproperties/commonproperties/col1/items`

1. 新しく作成されたオーバーレイノード (/apps/fd/cm/ma/gui/content/cmmetadataproperties/commonproperties/col1/items) の下

   各プロパティ（フィールド）に対して、ドロップダウン ( ここでは `geographicallocation`) タイプ nt:unstructured。

1. 次のプロパティをノード（ここでは「geographicallocation」）に追加し、「**すべて保存**」をクリックします。

   | 名前 | タイプ | 値 |
   |--- |--- |---|
   | fieldLabel | 文字列 | フィールド／プロパティに与える任意の名前。（ここでは「geographicallocation」） |
   | 名前 | 文字列 | `./extendedproperties/geographicallocation` （値は、items ノードで作成したフィールド名と同じにします）。 |
   | renderReadOnly | ブール値 | true |
   | sling:resourceType | 文字列 | granite/ui/components/coral/foundation/form/select |

1. プロパティノード（ここでは「geographicallocation」）に、`items` という名前の新しいノードを追加します。items ノードに、ドロップダウン内の各値のノードを追加します。ドロップダウンのデフォルト値およびユーザーがフィールドに値を指定しないためのオプションとして機能するように、最初のノードを空白として追加することをお勧めします。複数のオプション／ドロップダウン値を追加するには、次の手順を繰り返します。

   1. プロパティノード（ここでは「geographicallocation」）を右クリックし、「 」を選択します。 **作成** > **ノードを作成**.
   1. フィールドの名前をとして入力します。 `item1,` タイプを nt:unstructured として保持し、「 」をクリックします。 **OK**.
   1. 次のプロパティを新しく作成したノード（ここでは item1）に追加し、 **すべて保存**:

      | 名前 | タイプ | 値 |
      |--- |--- |--- |
      | text | 文字列 | これは、ユーザーに表示されるドロップダウンオプションの値です。空白（デフォルト）値の場合は空白のままにします。または、「**海外**」、「**米国内**」などの値を入力します。 |
      | value | 文字列 | テキストの CRXDE に保存される値。 一意のキーワードを入力します。 |

      ![customizationdropdownvaluescrxde](assets/customizationdropdownvaluescrxde.png)

カスタムドロップダウンは、アセットプロパティで次のように表示されます。

![drop_down_customization](assets/drop-down_customization.png)

### シナリオ：すべてのアセットタイプ用の共通タブ {#scenario-common-tab-for-all-asset-types}

このシナリオでは、すべてのアセットタイプ（テキスト、リスト、条件およびレイアウトフラグメント）およびレターにカスタムタブ「Recipients」を追加する方法について説明します。「Recipients」タブに、受信者に関連するすべてのカスタムプロパティを配置することができます。

![すべてのアセットタイプに追加されたカスタムタブ](assets/recipientstab.png)

次の手順を使用して、すべてのアセットにフィールド付きのタブを追加できます。

1. に移動します。 `https://[server]:[port]/[ContextPath]/crx/de` 管理者としてログインします。
1. 次の手順を使用して、apps フォルダーに、（コンテンツフォルダー内の）cmmetadataproperties フォルダーに似たパス/構造で cmmetadataproperties という名前のフォルダーを作成します。

   1. 次のパスにある cmmetadataproperties フォルダを右クリックし、「 」を選択します。 **ノードをオーバーレイ**:

      `/libs/fd/cm/ma/gui/content/cmmetadataproperties`

      ![ノードをオーバーレイ](assets/cmmetadatapropertiesoverlaynode.png)

   1. ノードをオーバーレイダイアログに次の値が表示されていることを確認します。

      **パス：** /libs/fd/cm/ma/gui/content/cmmetadataproperties

      **場所：** /apps/

      **ノードタイプを一致させる：** 選択済み

   1. 「**OK**」をクリックします。apps フォルダーにフォルダー構造が作成されます。

      ![CRX で作成されたオーバーレイフォルダー構造](assets/cmmetadatapropertiesappsfolder.png)

      「**すべて保存**」をクリックします。

1. cmmetadataproperties フォルダーの下に、すべてのアセットのカスタムタブを作成するノードを追加します ( 例：commontab) を次の手順で使用します。

   1. cmmetadataproperties フォルダーを右クリックして、「**作成**／**ノードを作成**」を選択します。

      ![ノードを作成](assets/cmmetadatapropertiescreatenode.png)

   1. ノードを作成ダイアログに次の値が表示されていることを確認し、「**OK**」をクリックします。

      **名前：** commontab（またはこのプロパティに与える任意の名前）

      **タイプ：** nt:unstructured

   1. 新しく作成したノードをクリックします（ここでは「commontab」）。CRX にノードのプロパティが表示されます。
   1. このノード（ここでは「commontab」）に次のプロパティを追加します。

      | 名前 | タイプ | 値 |
      |--- |--- |--- |
      | jcr:title | 文字列 | 列に与える任意の名前。（ここでは「Recipients」） |
      | sling:resourceType | 文字列 | granite/ui/components/coral/foundation/container |

   1. 「**すべて保存**」をクリックします。

1. 次の手順を使用し、最後の手順で作成したタブノード（ここでは「commontab」）に対して item という名前のノードを作成します。

   1. 関連ノード（ここでは「commontab」）を右クリックし、「**作成**／**ノードを作成**」を選択します。
   1. ノードを作成ダイアログに次の値が表示されていることを確認し、「**OK**」をクリックします。

      **名前：** items

      **タイプ：** nt:unstructured

   1. クリック **すべて保存：**

1. 前の手順で作成した items ノード（commontab の下）で、次の手順を使用して（列を追加するには、この手順を繰り返します）、カスタムタブ（commontab の）に列を作成するためのノード（ここでは「Column1」）を追加します。

   1. items ノードを右クリックし、「**作成**／**ノードを作成**」を選択します。
   1. ノードを作成ダイアログに次の値が表示されていることを確認し、「**OK**」をクリックします。

      **名前：** Column1 （または、ノードに与える名前。この名前は、ユーザーインターフェイスには表示されません。）

      **タイプ：** nt:unstructured

   1. 次のプロパティをノード（ここでは「Column1」）に追加し、 **すべて保存**:

      | 名前 | タイプ | 値 |
      |--- |--- |--- |
      | sling:resourceType | 文字列 | granite/ui/components/coral/foundation/container |

1. 前の手順で作成したノード（ここでは「Column1」）に、次の手順を使用して、items というノードを追加します。

   1. ノード（ここでは「Column1」）を右クリックし、「**作成**／**ノードを作成**」を選択します。
   1. ノードを作成ダイアログに次の値が表示されていることを確認し、「**OK**」をクリックします。

      **名前：** items

      **タイプ：** nt:unstructured

   1. 「**すべて保存**」をクリックします。

1. カスタムタブ（ここでは「Recipients」）にフィールドを作成するには、ノード（ここでは「GeographicalLocation」）を追加します。このプロパティは、作成した列に対応します。フィールドの作成手順は次のとおりです（さらにフィールド／ノードを作成するには、この手順を繰り返します）。：

   1. items ノードを右クリックし、「**作成**／**ノードを作成**」を選択します。
   1. ノードを作成ダイアログに次の値が表示されていることを確認し、「**OK**」をクリックします。

      **名前：** GeographicalLocation（または、フィールドプロパティの別の名前）

      **タイプ：** nt:unstructured

   1. 次のプロパティをフィールドノード（ここでは GeographicalLocation）に追加し、「**すべて保存**」をクリックします。

      | **名前** | **種類** | **値** |
      |---|---|---|
      | fieldLabel | 文字列 | Location of recipients（または、フィールドに与える任意の名前。） |
      | 名前 | 文字列 | 。/extendedproperties/GeographicalLocation |
      | renderReadOnly | ブール値 | true |
      | sling:resourceType | 文字列 | /libs/granite/ui/components/coral/foundation/form/textfield |

1. レターにこのタブを追加するには、次のパスにある以下の items フォルダーに類似したパス／構造でオーバーレイフォルダーを作成します。

   `/libs/fd/cm/ma/gui/content/cmmetadataproperties/properties/letter/items/tabs/items`

   レターまたは別のアセットのオーバーレイを作成するには、次のパスを使用して [assettype] テキスト、条件、リスト、データディクショナリ、フラグメントを使用：

   `/libs/fd/cm/ma/gui/content/cmmetadataproperties/properties/[assettype]/items/tabs/items`

   1. 次のパスにある items フォルダを右クリックし、を選択します。 **ノードをオーバーレイ**:

      `/libs/fd/cm/ma/gui/content/cmmetadataproperties/properties/letter/items/tabs/items`

   1. ノードをオーバーレイダイアログに次の値が表示されていることを確認します。

      **パス：** /libs/fd/cm/ma/gui/content/cmmetadataproperties/properties/letter/items/tabs/items

      **場所：** /apps/

      **ノードタイプを一致させる：** 選択済み

   1. 「**OK**」をクリックします。フォルダーが作成されます。「**すべて保存**」をクリックします。

1. 次の手順を使用して、新しく作成した items フォルダーに、アセットのカスタムタブのノードを追加します（ここでは mytab — この名前はユーザーインターフェイスに表示されません）。

   1. items フォルダーを右クリックして、「**作成**／**ノードを作成**」を選択します。
   1. ノードを作成ダイアログに次の値が表示されていることを確認し、「**OK**」をクリックします。

      **名前：** mytab（または、このプロパティに与える任意の名前）

      **タイプ：** nt:unstructured

   1. 新しく作成したノードをクリックします（ここでは「mytab」）。CRX にノードのプロパティが表示されます。
   1. このノード（ここでは「customtab」）に次の 2 つのプロパティを追加します。

      | 名前 | タイプ | 値 |
      |--- |--- |--- |
      | path | 文字列 | fd/cm/ma/gui/content/cmmetadataproperties/commontab |
      | sling:resourceType | 文字列 | granite/ui/components/coral/foundation/include |

   1. 「**すべて保存**」をクリックします。

1. カスタマイズ内容を表示するには、関連するアセット（ここではレター）の上にカーソルを置き、「プロパティを表示」をクリックし、「**編集**」をクリックします。新しいタブ（Recipients）とフィールド（Location of Recipients）がユーザーインターフェイスに表示されます。

   >[!NOTE]
   >
   >カスタマイズ内容を UI に表示するには、ブラウザーのキャッシュをクリアする必要が生じる場合があります。

   ![レターに追加されたカスタムタブ](assets/recipientstab-1.png)

### シナリオ：特定のアセットタイプのカスタムプロパティの追加 {#scenario-adding-custom-properties-for-specific-asset-types}

このシナリオでは、すべてのテキストアセットに対するフィールドなど、特定のアセットタイプにプロパティを追加する方法について説明します。このプロセスを使用して、次のいずれかにプロパティを追加できます。

* テキスト
* 条件
* リスト
* レイアウトフラグメント
* データディクショナリ
* レター

例えば、テキストアセットにのみプロパティ「受信者の場所」を追加して、アセットが関連する地理的領域を識別します。  ![アセットに追加されたカスタムプロパティ](assets/newtabui.png)

アセットタイプにプロパティを追加するには、次の手順を実行します。

1. に移動します。 `https://[server]:[port]/[ContextPath]/crx/de` 管理者としてログインします。
1. アセットタイプ（テキストなど）でタブを作成するには、apps フォルダーに次のフォルダー構造を作成します。

   `/libs/fd/cm/ma/gui/content/cmmetadataproperties/properties/[AssetType]/items/tabs/items`

   [AssetType] =テキスト、条件、リスト、レター、データ辞書、フラグメント

   次の手順に従って、このフォルダー構造を作成します。

   1. 次のパスにある items フォルダを右クリックし、を選択します。 **ノードをオーバーレイ**:

      `/libs/fd/cm/ma/gui/content/cmmetadataproperties/properties/[AssetType]/items/tabs/items`

      例えば、テキストアセットのプロパティを作成する場合は、次のフォルダーを選択します。

      `/libs/fd/cm/ma/gui/content/cmmetadataproperties/properties/text/items/tabs/items`

      ![ノードをオーバーレイ](assets/textitemstabsitemsoverlaynode1.png)

   1. ノードをオーバーレイダイアログに次の値が表示されていることを確認します。

      **パス：** /libs/fd/cm/ma/gui/content/cmmetadataproperties/properties/[AssetType]/items/tabs/items

      **場所：** /apps/

      **ノードタイプを一致させる：** 選択済み

   1. 「**OK**」をクリックします。apps フォルダーにフォルダー構造が作成されます。

      「**すべて保存**」をクリックします。

1. 新しく作成された items フォルダーに、アセットのカスタムタブのノードを追加します ( 例：customtab) を次の手順で使用します。

   1. items フォルダーを右クリックして、「**作成**／**ノードを作成**」を選択します。
   1. ノードを作成ダイアログに次の値が表示されていることを確認し、「**OK**」をクリックします。

      **名前：** customtab（または、このプロパティに与える任意の名前）

      **タイプ：** nt:unstructured

   1. 新しく作成したノードをクリックします（ここでは「customtab」）。CRX にノードのプロパティが表示されます。
   1. このノード（ここでは「customtab」）に次の 2 つのプロパティを追加します。

      | **名前** | **種類** | **値** |
      |---|---|---|
      | sling:resourceType | 文字列 | granite/ui/components/coral/foundation/container |
      | jcr:title | 文字列 | ユーザーインターフェイス上のフィールドの名前（ここでは「My tab」） |

   1. 「**すべて保存**」をクリックします。

1. 前の手順で作成したノード（ここでは「customtab」）に、次の手順を使用して、items と呼ばれるノードを追加します。

   1. ノード（ここでは「customtab」）を右クリックし、「**作成**／**ノードを作成**」を選択します。
   1. ノードを作成ダイアログに次の値が表示されていることを確認し、「**OK**」をクリックします。

      **名前：** items

      **タイプ：** nt:unstructured

   1. 「**すべて保存**」をクリックします。

1. 前の手順（customtab の下）で作成した items ノードで、次の手順を使用して、カスタムタブに列（ここでは「Column1」）を作成するノードを追加します（列を追加するには、この手順を繰り返します）。

   1. items ノードを右クリックし、「**作成**／**ノードを作成**」を選択します。
   1. ノードを作成ダイアログに次の値が表示されていることを確認し、「**OK**」をクリックします。

      **名前：** 列 1 （またはノードに与える任意の名前）

      **タイプ：** nt:unstructured

   1. 次のプロパティをノード（ここでは「Column1」）に追加し、 **すべて保存**.

      | 名前 | タイプ | 値 |
      |--- |--- |--- |
      | sling:resourceType | 文字列 | granite/ui/components/coral/foundation/container |

1. 作成する各列 ( 前の手順（ここでは「Column1」）で指定 ) に対して、次の手順で「item」というノードを作成します。

   1. 関連する列ノード（ここでは「Column1」）を右クリックし、「**作成**／**ノードを作成**」を選択します。
   1. ノードを作成ダイアログに次の値が表示されていることを確認し、「**OK**」をクリックします。

      **名前：** items

      **タイプ：** nt:unstructured

   1. クリック **すべて保存：**

1. 作成した各列で、items ノードに、ユーザーインターフェイス内の新しいタブにフィールドを作成するためのノードを作成します。列でさらにフィールドを作成するには、この手順を繰り返します。

   1. 関連ノード（ここでは「Column1」の下の「items」）を右クリックし、「**作成**／**ノードを作成**」を選択します。
   1. ノードを作成ダイアログに次の値が表示されていることを確認し、「**OK**」をクリックします。

      **名前：** 任意の名前（ここでは「GeoLocation」）

      **タイプ：** nt:unstructured

   1. 次のプロパティをノードに追加して、「**すべて保存**」をクリックします。

      | **名前** | **種類** | **値** |
      |---|---|---|
      | fieldLabel | 文字列 | Location of recipients（または、フィールドに与える任意の名前。） |
      | 名前 | 文字列 | 。/extendedproperties/GeoLocation |
      | renderReadOnly | ブール値 | true |
      | sling:resourceType | 文字列 | granite/ui/components/coral/foundation/form/textfield |

1. カスタマイズ内容を表示するには、関連するアセット（ここではテキスト）の上にカーソルを置き、「プロパティを表示」をクリックし、「**編集**」をクリックします。新しいタブとフィールド（Location of Recipients）がユーザーインターフェイスに表示されます。

   >[!NOTE]
   >
   >カスタマイズ内容を UI に表示するには、ブラウザーのキャッシュをクリアする必要が生じる場合があります。

   ![特定のアセットに追加されたカスタムプロパティ](assets/newtabui-1.png)

### アセット作成ページでのカスタムプロパティの表示 {#display-custom-properties-on-the-asset-creation-page}

デフォルトでは、新しいタブに追加されるカスタムプロパティは、プロパティページにのみ表示され、アセット作成ページにはタブレイアウトがないので、アセット作成ページには表示されません。 アセット作成ページに他のプロパティと共にカスタムプロパティを表示するには、次の手順を実行する必要があります。

1. 次のパスにある items フォルダを右クリックし、を選択します。 **ノードをオーバーレイ**:

   `/libs/fd/cm/ma/gui/content/createasset/createletter/jcr:content/body/items/form/items/letterWizard/items/properties/items/properties/items/letterproperties/items`

1. ノードをオーバーレイダイアログで、レターに次の値が表示されていることを確認します。他のアセットタイプのパスは以下の表に示されています。

   **パス：** /libs/fd/cm/ma/gui/content/createasset/createletter/jcr:content/body/items/form/items/letterWizard/items/properties/items/properties/items/letterproperties/items

   **場所：** /apps/

   **ノードタイプを一致させる：** 選択済み

   アセットの種類に応じたパスを使用する必要があります。

   | **アセット／ドキュメントタイプ** | **追加するパス** |
   |---|---|
   | テキスト | /libs/fd/cm/ma/gui/content/createasset/createtext/jcr:content/body/items/form/items/textwizard/items/editproperties/items/properties/items/tabs/items/tab1/items |
   | リスト | /libs/fd/cm/ma/gui/content/createasset/createlist/jcr:content/body/items/form/items/listwizard/items/editproperties/items/properties/items/tabs/items/tab1/items |
   | 条件 | /libs/fd/cm/ma/gui/content/createasset/createcondition/jcr:content/body/items/form/items/conditionwizard/items/editproperties/items/properties/items/tabs/items/tab1/items |
   | フラグメント | /libs/fd/cm/ma/gui/content/createasset/createfragment/jcr:content/body/items/form/items/fragmentwizard/items/properties/items/properties/items/tabs2/items/tab1/items |
   | レター | /libs/fd/cm/ma/gui/content/createasset/createletter/jcr:content/body/items/form/items/letterWizard/items/properties/items/properties/items/letterproperties/items |

1. 「**OK**」をクリックします。apps フォルダーにフォルダー構造が作成されます。

1. 作成したオーバーレイ項目ノードの下に、名前 col4 （または他の名前）のノードを作成し、 **すべて保存**.

   例えば、以下は、レターに対して作成されたオーバーレイノードです。

   `/apps/fd/cm/ma/gui/content/createasset/createletter/jcr:content/body/items/form/items/letterWizard/items/properties/items/properties/items/letterproperties/items`

1. 次のプロパティを新しく作成したノード（ここでは「col4」）に追加し、「**すべて保存**」をクリックします。

   <table> 
   <tbody> 
   <tr> 
      <td><strong>名前</strong></td> 
      <td><strong>タイプ</strong></td> 
      <td><strong>値</strong></td> 
   </tr> 
   <tr> 
      <td>パス</td> 
      <td>文字列</td> 
      <td><p>このパスは、以下の場所で作成された列へのポインターです。</p> 
      <ul> 
      <li>すべてのアセットタイプの共通タブの場合：/apps/fd/cm/ma/gui/content/cmmetadataproperties/commontab/items/col1</li> 
      <li>アセットタイプごとに異なるプロパティを使用する場合：/apps/fd/cm/ma/gui/content/cmmetadataproperties/properties//items/tabs/items/customtab/items/col1</li> 
      </ul> </td> 
   </tr> 
   <tr> 
      <td>sling:resourceType</td> 
      <td>文字列</td> 
      <td> granite/ui/components/coral/foundation/include<br /> </td> 
   </tr> 
   </tbody> 
   </table>

   ![customfieldappearinginmainproperties](assets/customfieldappearinginmainproperties.png)

   レターを作成するための UI に表示される、カスタムプロパティ、言語

## カスタムプロパティを表示するための一覧表示のカスタマイズ {#customize-the-list-view-to-show-custom-properties}

Correspondence Management アセットにカスタムプロパティを追加した後、CRX/DE でさらに変更を行って、カスタムプロパティが Correspondence Management UI に表示されるようにする必要があります。

次の手順を実行して、Correspondence Management のアセットリスト UI にカスタムプロパティを表示します。

1. に移動します。 `https://[server]:[port]/[ContextPath]/crx/de` 管理者としてログインします。
1. apps フォルダーに以下のフォルダー構造を作成します。

   `/libs/fd/cm/ma/gui/content/cmassets/jcr:content/views/lists/columns`

   次の手順に従って、このフォルダー構造を作成します。

   1. 次のパスにある columns フォルダーを右クリックし、「 」を選択します。 **ノードをオーバーレイ**:

      `/libs/fd/cm/ma/gui/content/cmassets/jcr:content/views/lists/columns`

   1. ノードをオーバーレイダイアログに次の値が表示されていることを確認します。

      **パス：** /libs/fd/cm/ma/gui/content/cmassets/jcr:content/views/lists/columns

      **場所：** /apps/

      **ノードタイプを一致させる：** 選択済み

   1. 「**OK**」をクリックします。apps フォルダーにフォルダー構造が作成されます。

      「**すべて保存**」をクリックします。

1. 作成した各プロパティで、columns ノードに、ユーザーインターフェイス内に列を作成するためのノードを作成します。UI でさらに列を作成するには、この手順を繰り返します。

   1. 関連ノード（ここでは「columns」）を右クリックし、「**作成**／**ノードを作成**」を選択します。
   1. ノードを作成ダイアログに次の値が表示されていることを確認し、「**OK**」をクリックします。

      **名前：** 任意の名前（ここでは GeographicalLocation）

      **タイプ：** nt:unstructured

   1. 次のプロパティをノードに追加して、「**すべて保存**」をクリックします。

      | 名前 | タイプ | 値 |
      |--- |--- |--- |
      | jcr:primaryType | 名前 | nt:unstructured |
      | jcr:title | 文字列 | GeographicalLocation この値は、UI の列ヘッダーとして表示されます。 |
      | sortable | ブール値 | true 値が true の場合、ユーザーはこの列の値を並べ替えることができます。 |

1. apps フォルダーに以下のフォルダー構造を作成します。

   `/libs/fd/cm/ma/gui/components/admin/childpagerenderer/childlistpage`

   次の手順に従って、このフォルダー構造を作成します。

   1. 次のパスにある columns フォルダーを右クリックし、「 」を選択します。 **ノードをオーバーレイ**:

      `/libs/fd/cm/ma/gui/components/admin/childpagerenderer/childlistpage`

   1. ノードをオーバーレイダイアログに次の値が表示されていることを確認します。

      **パス：** /libs/fd/cm/ma/gui/components/admin/childpagerenderer/childlistpage

      **場所：** /apps/

      **ノードタイプを一致させる：** 選択済み

   1. 「**OK**」をクリックします。apps フォルダーにフォルダー構造が作成されます。

      「**すべて保存**」をクリックします。

1. 次の場所から childlistpage.jsp ファイルをコピーします。

   /libs/fd/cm/ma/gui/components/admin/childpagerenderer/childlistpage/childlistpage.jsp

   このファイルを次の場所に貼り付けます。

   /apps//fd/cm/ma/gui/components/admin/childpagerenderer/childlistpage/.

1. childlistpage.jsp ファイル（/apps/fd/cm/ma/gui/components/admin/childpagerenderer/childlistpage/childlistpage.jsp）を開き、次のように変更します。

   1. ファイルの 19 行目に以下を追加します（著作権情報の後）。

      ```
      <%@page import="java.util.Map"%>
      ```

   1. ファイルの末尾に、各カスタムプロパティの値を取得する以下の関数コードを追加します。

      ```
      <%!
          private String getCustomPropertyValue(Map<String, Object> extendedProperties, String propertyName) {
      
              String propertyValue = "";
              if (extendedProperties.containsKey(propertyName)) {
                  propertyValue = (String) extendedProperties.get(propertyName);
              }
      
              return propertyValue;
          }
      %>
      ```

   1. の開始前に、以下を追加します。 &lt;tr> タグ (&lt;tr attrs.build=&quot;&quot;>>):

      ```
      <%
          String GeoLocation = "";
          if (asset != null) {
                  Map<String, Object> extendedProperties = asset.getExtendedProperties();
                  if (extendedProperties != null) {
                      GeoLocation = getCustomPropertyValue(extendedProperties,"GeoLocation");
                  }
          }
      %>
      ```

      コード内の GeoLocation は、カスタムノード／フィールドの作成時に名前プロパティで設定した値です。カスタムノード／フィールドの作成時、プロパティの名前を /extendedproperties/ prefix: ./extendedproperties/GeoLocation で指定しました。コードの prefix は必須ではありません。

   1. UI に新しいプロパティを表示するには、次のように TD タグを終了 tr (&lt;/tr>) タグで使用できます。

      ```
      <td is="coral-td" value="<%= xssAPI.encodeForHTMLAttr(geographicalLocation) %>"><%= xssAPI.encodeForHTML(geographicalLocation) %></td>
      ```

      さらに列を追加するには、手順 6.3 と 6.4 を繰り返します。

   1. 「**すべて保存**」をクリックします。

1. カスタマイズ内容を表示するには、カスタムプロパティを追加したドキュメントフラグメント（レター）の一覧表示を開きます。

   この手順で追加した UI 列およびプロパティは、すべてのアセットタイプで表示されます。ただし、これらのプロパティの値は、最初にカスタムプロパティを追加したアセットタイプに対してのみ入力および表示できます。

   例えば、次のシナリオを使用します。特定のアセットタイプのカスタムプロパティを追加してカスタムプロパティをテキストアセットに追加する場合、カスタムプロパティを入力できるのはテキストアセットに対してのみです。 ただし、そのカスタムプロパティを UI に表示する場合、列はすべてのアセットタイプで表示されます。

   ![custompropertyinlistview](assets/custompropertyinlistview.png)

1. （オプション）デフォルトでは、新しい列は、UI で最後の列として表示されます。列を特定の位置に表示するには、次のプロパティを列ノードに追加します。

   | 名前 | タイプ | 値 |
   |--- |--- |--- |
   | sling:orderBefore | 文字列 | パス「 」の列ノードの名前`/libs/fd/cm/ma/gui/content/cmassets/jcr:content/views/list/columns`」をクリックします。 ここで、「地理的な場所」列を「バージョン」列の前（左）に表示する場合は、プロパティを追加します。 `sling:orderBefore` パス「 」の GeoLocation ノードに`/apps/fd/cm/ma/gui/content/cmassets/jcr:content/views/list/columns/GeoLocation`」と入力し、プロパティの値を version に設定します。 |

   sling:orderBefore プロパティを追加して列の位置を指定する場合は、この手順の手順 6.4 で指定した、対応する &lt;td> タグの順序も更新する必要があります。例えば、この場合、Geographical Location の &lt;td> タグを Version 列の &lt;td> タグの前に配置する必要があります。

   ```xml
   <td is="coral-td" value="<%= xssAPI.encodeForHTMLAttr(geographicalLocation) %>"><%= xssAPI.encodeForHTML(geographicalLocation) %></td>
   <td is="coral-td" value="<%= xssAPI.encodeForHTMLAttr(version) %>"><%= xssAPI.encodeForHTML(version) %></td>
   ```

## カスタムプロパティの検索の有効化 {#enable-search-for-custom-properties}

デフォルトでは、フルテキスト検索には、CRX/DE を使用して UI に追加するカスタムプロパティは含まれません。

カスタムプロパティを検索に含めるには、カスタムプロパティのインデックス作成を可能にする必要があります。

カスタムプロパティのインデックス作成を可能にするには、次の手順を実行します。

1. に移動します。 `https://[server]:[port]/[ContextPath]/crx/de` 管理者としてログインします。
1. に移動します。 `/oak:index/cmLucene`次に、 **集計** その下に

   1. cmLucene フォルダーを右クリックして、「**作成**／**ノードを作成**」を選択します。
   1. ノードを作成ダイアログに次の値が表示されていることを確認し、「**OK**」をクリックします。

      **名前：** aggregates

      **タイプ：** nt:unstructured

   1. 「**すべて保存**」をクリックします。

1. 新しく作成した aggregates フォルダーの下に、ノード cm:resource を追加します。 cm:resource の下に、include0 という名前のノードを追加します。

   1. aggregates フォルダーを右クリックして、「**作成**／**ノードを作成**」を選択します。ノードを作成ダイアログに次の値が表示されていることを確認し、「**OK**」をクリックします。

      **名前：** cm:resource

      **タイプ：** nt:unstructured

   1. cm:resource フォルダーを右クリックし、「 」を選択します。 **作成** > **ノードを作成**. ノードを作成ダイアログに次の値が表示されていることを確認し、「**OK**」をクリックします。

      **名前：** include0

      **タイプ：** nt:unstructured

   1. 新しく作成したノードをクリックします（ここでは「include0」）。CRX にノードのプロパティが表示されます。
   1. このノード（ここでは「include0」）に次のプロパティを追加します。

      | 名前 | タイプ | 値 |
      |--- |--- |--- |
      | パス | 文字列 | extendedProperties |
   1. 「**すべて保存**」をクリックします。

1. 次の場所にあるプロパティに移動し、その下にノードの場所を追加します。 `/oak:index/cmLucene/indexRules/cm:resource/properties`

   検索に追加する各カスタムプロパティについて、この手順を繰り返します。

   1. properties フォルダーを右クリックして、「**作成**／**ノードを作成**」を選択します。
   1. ノードを作成ダイアログに次の値が表示されていることを確認し、「**OK**」をクリックします。

      **名前：** 場所（または検索に追加するカスタムプロパティの名前）

      **タイプ：** nt:unstructured

   1. 作成した新しいノード（ここでは「location」）をクリックします。CRX にノードのプロパティが表示されます。
   1. このノード（ここでは「location」）に次のプロパティを追加します。

      | **名前** | **種類** | **値** |
      |---|---|---|
      | analyzed | 文字列 | true |
      | 名前 | 文字列 | extendedProperties/location（または、検索に追加するプロパティの名前） |
      | propertyIndex | ブール値 | true |
      | useInSuggest | ブール値 | true |

   1. 「**すべて保存**」をクリックします。

1. フルテキスト検索でカスタムプロパティの値を使用して関連アセットを検索できるようになりました。

>[!NOTE]
>
>まだ検索できない場合は、インデックス作成の問題が原因の可能性があります。インデックスを再作成する場合は、次のノードに移動し、「re-index」プロパティの値を true に変更します。
>
>/oak:index/cmLucene およびプロパティの値の変更

## 検索ページのデフォルト表示の変更 {#change-default-view-of-the-search-page}

1. に移動します。 `https://[server]:[port]/[ContextPath]/crx/de` 管理者としてログインします。
1. apps フォルダーに、 /libs/granite/ui/content/shell/omnisearch/searchresults/singleresults/views にある list フォルダーに似たパス/構造で list という名前のフォルダーを作成します。

   1. 次のパスにある items フォルダを右クリックし、を選択します。 **ノードをオーバーレイ**:

      `/libs/granite/ui/content/shell/omnisearch/searchresults/singleresults/views/list`

   1. ノードをオーバーレイダイアログに次の値が表示されていることを確認します。

      **パス：** /libs/granite/ui/content/shell/omnisearch/searchresults/singleresults/views/list

      **場所：** /apps/

      **ノードタイプを一致させる：** 選択済み

   1. 「**OK**」をクリックします。apps フォルダーにフォルダー構造が作成されます。

   1. 「**すべて保存**」をクリックします。

1. 新しく作成したノード list で、次のプロパティを追加し、「**すべて保存**」をクリックします。

   | 名前 | タイプ | 値 |
   |---|---|---|
   | sling:orderBefore | 文字列 | card |

1. カスタマイズにより、フォームとドキュメント、アセット、サイトを含むすべてのコンソールで一覧表示に検索結果が表示されるようになりました。

## アセットページのデフォルト表示の変更 {#change-default-view-of-the-assets-page}

>[!NOTE]
>
>以下の手順は、フォームとドキュメント、アセット、サイトなどのすべてのコンソールのデフォルト表示を変更します。

1. に移動します。 `https://[server]:[port]/[ContextPath]/crx/de` 管理者としてログインします。
1. apps フォルダーに、次の場所にある list フォルダーと同様のパス/構造で list という名前のフォルダーを作成します。

   /libs/fd/cm/ma/gui/content/cmassets/jcr:content/views/

   1. 次のパスにある items フォルダを右クリックし、を選択します。 **ノードをオーバーレイ**:

      `/libs/fd/cm/ma/gui/content/cmassets/jcr:content/views/list`

   1. ノードをオーバーレイダイアログに次の値が表示されていることを確認します。

      **パス：** /libs/fd/cm/ma/gui/content/cmassets/jcr:content/views/list

      **場所：** /apps/

      **ノードタイプを一致させる：** 選択済み

   1. 「**OK**」をクリックします。apps フォルダーにフォルダー構造が作成されます。

   1. 「**すべて保存**」をクリックします。

1. 新しく作成したノード list で、次のプロパティを追加し、「**すべて保存**」をクリックします。

   | 名前 | タイプ | 値 |
   |---|---|---|
   | sling:orderBefore | 文字列 | カード |

1. ブラウザーの Cookie をクリアするか、ブラウザーの匿名モードを使用して、アセットを表示します。アセットページは、デフォルトで、カードレイアウトで表示されます。

## アセット作成ページとプロパティページでのカスタムプロパティの表示／非表示 {#show-hide-custom-properties-on-asset-creation-and-properties-pages}

カスタムプロパティを表示または非表示にするには、次の手順を実行します。

1. geographicallocation などのカスタムプロパティノードの下に、「granite:rendercondition」という名前で「nt:unstructured」タイプの新しいノードを作成します。
1. 次のプロパティをノードに追加し、「**すべて保存**」をクリックします。

   | 名前 | タイプ | 値 |
   |---|---|---|
   | sling:resourceType | 文字列 | fd/cm/ma/gui/components/admin/assetsproperties/custompropertyconfig |

1. アセット作成ページでこのプロパティを非表示にするには、このプロパティに次のプロパティを追加し、 **すべて保存**:

   | 名前 | タイプ | 値 |
   |---|---|---|
   | hideOnCreate | ブール値 | true |

1. アセットのプロパティページでカスタムプロパティを非表示にするには、次のプロパティを追加し、「**すべて保存**」をクリックします。

   | 名前 | タイプ | 値 |
   |---|---|---|
   | hideOnEdit | ブール値 | true |

   値を再度表示するには、プロパティ値をにリセットします。 `false` またはプロパティエントリを削除します。
