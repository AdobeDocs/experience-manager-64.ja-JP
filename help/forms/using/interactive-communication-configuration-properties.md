---
title: インタラクティブ通信の設定プロパティ
seo-title: Interactive Communication configuration properties
description: インタラクティブ通信で使用するデフォルトの設定プロパティの編集
seo-description: Edit default configuration properties for Interactive Communications
uuid: 793da9c0-7e8b-464c-b41d-559a72fac9eb
contentOwner: anujkapo
products: SG_EXPERIENCEMANAGER/6.4/FORMS
content-type: reference
topic-tags: interactive-communications
discoiquuid: 1aef2a51-4391-4075-8841-a62ace5606f9
feature: Interactive Communication
exl-id: 2caf7242-8588-4fc9-9429-40e24416d6eb
source-git-commit: bd94d3949f0117aa3e1c9f0e84f7293a5d6b03b4
workflow-type: tm+mt
source-wordcount: '531'
ht-degree: 69%

---

# インタラクティブ通信の設定プロパティ {#interactive-communications-configuration-properties}

インタラクティブ通信で使用するデフォルトの設定プロパティの編集

インタラクティブ通信には、[AEM Forms アドオン](/help/forms/using/installing-configuring-aem-forms-osgi.md)パッケージのインストール後に自動的に設定されるプロパティが含まれています。インタラクティブ通信の作成者は、**Adobe Experience Manager Web コンソール設定**&#x200B;ページを使用して、これらのデフォルトの設定プロパティを編集できます。

を開きます。 **Adobe Experience Manager Web コンソール設定** 次の URL を使用してページを表示します。

https://&lt;server>:&lt;port>/&lt;contextpath>/system/console/configMgr

設定プロパティには次のものが含まれます。

* [ドキュメントフラグメントの設定](#document-fragments-configuration)
* [通信設定の作成](#create-correspondence-configuration)
* [アダプティブフォームおよびインタラクティブ通信 Web チャネルの設定](#adaptive-form-and-interactive-communication-web-channel-configuration)
* [アダプティブフォームおよびインタラクティブ通信 Web チャネルテーマの設定](#adaptive-form-and-interactive-communication-web-channel-theme-configuration)

## ドキュメントフラグメントの設定 {#document-fragments-configuration}

タップ **ドキュメントフラグメントの設定** の **Adobe Experience Manager Web コンソール設定** ページを開き、ドキュメントフラグメントの設定プロパティを表示します。

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
   <td>印刷チャネルと Web チャネル用のインタラクティブ通信を作成する際に使用できるフィールド、変数、フォームデータモデル要素のロケール固有の表示形式。</td> 
   <td> 
    <ul> 
     <li>locale = en_US, de_DE, fr_FR, and ja_JP</li> 
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

## 通信設定の作成 {#create-correspondence-configuration}

タップ **通信設定を作成** の **Adobe Experience Manager Web コンソール設定** ページを開き、エージェント UI の設定プロパティを表示します。

| プロパティ | 説明 | デフォルト | 指定できる値 |
|---|---|---|---|
| 編集用に解決されたコンテンツの表示 | エージェント UI 上でテキストモジュールを編集する際に、チェックボックスを選択して、解決されたコンテンツ（プレースホルダーではなく実際の値）を表示します。 | 未選択 | 適用なし |
| プレビュー時に透かしの適用 | チェックボックスを選択して、インタラクティブ通信の印刷チャネルのプレビュー表示に透かしを適用します。 | 未選択 | 適用なし |

## アダプティブフォームおよびインタラクティブ通信 Web チャネルの設定 {#adaptive-form-and-interactive-communication-web-channel-configuration}

タップ **アダプティブフォームとインタラクティブ通信の Web チャネル設定** の **Adobe Experience Manager Web コンソール設定** アダプティブFormsおよびインタラクティブ通信 Web チャネルの設定プロパティを表示するページ 次のテーブルに、インタラクティブ通信に関連するプロパティを示します。

| プロパティ | 説明 | デフォルト | 指定できる値 |
|---|---|---|---|
| プレースホルダーを表示 | チェックボックスを選択して、アダプティブフォームおよびインタラクティブ通信に含まれているフィールドのプレースホルダー表示を有効にします。 | 選択 | 適用なし |
| 最大キャッシュエントリ数 | キャッシュメモリを使用して取得できるアダプティブフォームおよびインタラクティブ通信の最大数を設定します。 | 100 | 数値 |
| 一意のファイル名を作成 | チェックボックスを選択して、アダプティブフォームおよびインタラクティブ通信に添付ファイルとして含まれているファイルに一意の名前を付けます。 | 未選択 | 適用なし |

## アダプティブフォームおよびインタラクティブ通信 Web チャネルテーマの設定 {#adaptive-form-and-interactive-communication-web-channel-theme-configuration}

タップ **アダプティブフォームとインタラクティブ通信 Web チャネルのテーマの設定** の **Adobe Experience Manager Web コンソール設定** アダプティブFormsおよびインタラクティブ通信 Web チャネルテーマの設定プロパティを表示するページ

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
