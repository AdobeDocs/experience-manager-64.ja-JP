---
title: インタラクティブ通信の設定プロパティ
seo-title: インタラクティブ通信の設定プロパティ
description: インタラクティブ通信で使用するデフォルトの設定プロパティの編集
seo-description: インタラクティブ通信で使用するデフォルトの設定プロパティの編集
uuid: 793da9c0-7e8b-464c-b41d-559a72fac9eb
contentOwner: anujkapo
products: SG_EXPERIENCEMANAGER/6.4/FORMS
content-type: reference
topic-tags: interactive-communications
discoiquuid: 1aef2a51-4391-4075-8841-a62ace5606f9
feature: Interactive Communication
translation-type: tm+mt
source-git-commit: 75312539136bb53cf1db1de03fc0f9a1dca49791
workflow-type: tm+mt
source-wordcount: '544'
ht-degree: 70%

---


# インタラクティブ通信の設定プロパティ {#interactive-communications-configuration-properties}

インタラクティブ通信で使用するデフォルトの設定プロパティの編集

インタラクティブ通信には、[AEM Forms アドオン](/help/forms/using/installing-configuring-aem-forms-osgi.md)パッケージのインストール後に自動的に設定されるプロパティが含まれています。インタラクティブ通信の作成者は、**Adobe Experience Manager Web コンソール設定**&#x200B;ページを使用して、これらのデフォルトの設定プロパティを編集できます。

次のURLを使用して&#x200B;**Adobe Experience ManagerWebコンソール設定**&#x200B;ページを開きます。

https://&lt;サーバー>:&lt;ポート>/&lt;コンテキストパス>/system/console/configMgr

設定プロパティには次のものが含まれます。

* [ドキュメントフラグメントの設定](#document-fragments-configuration)
* [通信設定の作成](#create-correspondence-configuration)
* [アダプティブフォームおよびインタラクティブ通信 Web チャネルの設定](#adaptive-form-and-interactive-communication-web-channel-configuration)
* [アダプティブフォームおよびインタラクティブ通信 Web チャネルテーマの設定](#adaptive-form-and-interactive-communication-web-channel-theme-configuration)

## ドキュメントフラグメントの設定  {#document-fragments-configuration}

**Adobe Experience ManagerWebコンソールの設定**&#x200B;ページで&#x200B;**ドキュメントフラグメントの設定**&#x200B;をタップし、ドキュメントフラグメントの設定プロパティを表示します。

<table> 
 <tbody> 
  <tr> 
   <td>プロパティ</td> 
   <td>説明</td> 
   <td>デフォルト</td> 
   <td>指定できる値</td> 
  </tr> 
  <tr> 
   <td>データの表示形式</td> 
   <td>印刷およびWebチャネル用のインタラクティブ通信を作成する際に使用できる、フィールド、変数、フォームデータモデル要素のロケール固有の表示形式。</td> 
   <td> 
    <ul> 
     <li>locale = en_US、de_DE、fr_FRおよびja_JP</li> 
     <li>dateFormat = dd-MM-yyyy</li> 
     <li>numberDecimalSeparator = .</li> 
     <li>numberGroupSeparator = ,</li> 
     <li>numberUseGroupSeparator = true</li> 
    </ul> </td> 
   <td><p>—</p> </td> 
  </tr> 
  <tr> 
   <td>インデント</td> 
   <td>リストドキュメントフラグメント内のテキストに適用される単一ユニットのインデント幅。</td> 
   <td>12.7 mm</td> 
   <td>数値</td> 
  </tr> 
  <tr> 
   <td>最小幅のローマ数字</td> 
   <td>リストドキュメントフラグメント内でローマ数字を使用する際に、箇条書きフィールドまたは番号フィールドに適用される最小幅。 </td> 
   <td>12.7 mm</td> 
   <td>数値</td> 
  </tr> 
  <tr> 
   <td>最小幅の数字</td> 
   <td>リストドキュメントフラグメント内でローマ数字以外の番号付きリストを使用する際に、箇条書きフィールドまたは番号フィールドに適用される最小幅。</td> 
   <td>8.0 mm</td> 
   <td>数値</td> 
  </tr> 
 </tbody> 
</table>

## 通信設定の作成  {#create-correspondence-configuration}

**Adobe Experience ManagerWebコンソール設定**&#x200B;ページで「通信の設定を作成」**をタップし、エージェントUIの設定プロパティを表示します。**

| プロパティ | 説明 | デフォルト | 指定できる値 |
|---|---|---|---|
| 編集用に解決されたコンテンツの表示 | エージェント UI 上でテキストモジュールを編集する際に、チェックボックスを選択して、解決されたコンテンツ（プレースホルダーではなく実際の値）を表示します。 | 未選択 | 適用なし |
| プレビュー時に透かしの適用 | チェックボックスを選択して、インタラクティブ通信の印刷チャネルのプレビュー表示に透かしを適用します。 | 未選択 | 該当なし |

## アダプティブフォームおよびインタラクティブ通信 Web チャネルの設定  {#adaptive-form-and-interactive-communication-web-channel-configuration}

**Adobe Experience ManagerWebコンソール設定**&#x200B;ページで「**アダプティブフォームと対話型通信Webチャネルの設定**」をタップし、アダプティブFormsおよび対話型通信Webチャネルの設定プロパティを表示します。 次のテーブルに、インタラクティブ通信に関連するプロパティを示します。

| プロパティ | 説明 | デフォルト | 指定できる値 |
|---|---|---|---|
| プレースホルダーを表示 | チェックボックスを選択して、アダプティブフォームおよびインタラクティブ通信に含まれているフィールドのプレースホルダー表示を有効にします。 | 選択 | 適用なし |
| 最大キャッシュエントリ数 | キャッシュメモリを使用して取得できるアダプティブフォームおよびインタラクティブ通信の最大数を設定します。 | 100 | 数値 |
| 一意のファイル名を作成 | チェックボックスを選択して、アダプティブフォームおよびインタラクティブ通信に添付ファイルとして含まれているファイルに一意の名前を付けます。 | 未選択 | 該当なし |

## アダプティブフォームおよびインタラクティブ通信 Web チャネルテーマの設定  {#adaptive-form-and-interactive-communication-web-channel-theme-configuration}

**Adobe Experience ManagerWebコンソール設定**&#x200B;ページで「**アダプティブフォームと対話型通信Webチャネルのテーマ設定**」をタップし、アダプティブFormsおよび対話型通信Webチャネルテーマの設定プロパティを表示します。

<table> 
 <tbody> 
  <tr> 
   <td>プロパティ</td> 
   <td>説明</td> 
   <td>デフォルト</td> 
   <td>指定できる値</td> 
  </tr> 
  <tr> 
   <td>フォントリスト名</td> 
   <td>フォントの一覧は、アダプティブフォームおよびインタラクティブ通信を作成する際に使用できるようになります。</td> 
   <td><p>グルジア</p> <p>Book Antiqua</p> <p>Times New Roman</p> <p>Arial</p> <p>Arial Black</p> <p>影響</p> <p>Palatino Linotype</p> </td> 
   <td>すべての有効な Adobe サーバーフォント</td> 
  </tr> 
 </tbody> 
</table>

