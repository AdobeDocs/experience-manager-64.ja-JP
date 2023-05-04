---
title: インタラクティブ通信の設定プロパティ
seo-title: Interactive Communication configuration properties
description: インタラクティブ通信のデフォルトの設定プロパティを編集
seo-description: Edit default configuration properties for Interactive Communications
uuid: 793da9c0-7e8b-464c-b41d-559a72fac9eb
contentOwner: anujkapo
products: SG_EXPERIENCEMANAGER/6.4/FORMS
content-type: reference
topic-tags: interactive-communications
discoiquuid: 1aef2a51-4391-4075-8841-a62ace5606f9
feature: Interactive Communication
exl-id: 2caf7242-8588-4fc9-9429-40e24416d6eb
source-git-commit: c5b816d74c6f02f85476d16868844f39b4c47996
workflow-type: tm+mt
source-wordcount: '567'
ht-degree: 48%

---

# インタラクティブ通信の設定プロパティ {#interactive-communications-configuration-properties}

>[!CAUTION]
>
>AEM 6.4 の拡張サポートは終了し、このドキュメントは更新されなくなりました。 詳細は、 [技術サポート期間](https://helpx.adobe.com/jp/support/programs/eol-matrix.html). サポートされているバージョンを見つける [ここ](https://experienceleague.adobe.com/docs/?lang=ja).

インタラクティブ通信のデフォルトの設定プロパティを編集

インタラクティブ通信には、[AEM Forms アドオン](/help/forms/using/installing-configuring-aem-forms-osgi.md)パッケージのインストール後に自動的に設定されるプロパティが含まれています。インタラクティブ通信の作成者は、**Adobe Experience Manager Web コンソール設定**&#x200B;ページを使用して、これらのデフォルトの設定プロパティを編集できます。

次の URL を使用して、**Adobe Experience Manager Web コンソール設定**&#x200B;ページを開きます。

https://&lt;server>:&lt;port>/&lt;contextpath>/system/console/configMgr

設定プロパティには次のものが含まれます。

* [ドキュメントフラグメントの設定](#document-fragments-configuration)
* [通信設定の作成](#create-correspondence-configuration)
* [アダプティブフォームおよびインタラクティブ通信 web チャネルの設定](#adaptive-form-and-interactive-communication-web-channel-configuration)
* [アダプティブフォームおよびインタラクティブ通信 web チャネルテーマの設定](#adaptive-form-and-interactive-communication-web-channel-theme-configuration)

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
   <td>印刷チャネルと web チャネル用のインタラクティブ通信を作成する際に使用可能なフィールド、変数、フォームデータモデル要素用のロケール固有の表示形式。</td> 
   <td> 
    <ul> 
     <li>locale = en_US, de_DE, fr_FR, and ja_JP</li> 
     <li>dateFormat = dd-MM-yyyy</li> 
     <li>numberDecimalSeparator = .</li> 
     <li>numberGroupSeparator = ,</li> 
     <li>numberUseGroupSeparator = true</li> 
    </ul> </td> 
   <td><p>--</p> </td> 
  </tr> 
  <tr> 
   <td>インデント</td> 
   <td>リストドキュメントフラグメント内のテキストに適用される 1 単位のインデントの幅です。</td> 
   <td>12.7mm</td> 
   <td>数値</td> 
  </tr> 
  <tr> 
   <td>最小幅のローマ数字</td> 
   <td>リストドキュメントフラグメントでローマ数字を使用する場合に、箇条書きフィールドまたは数値フィールドに適用される最小の幅です。 </td> 
   <td>12.7mm</td> 
   <td>数値</td> 
  </tr> 
  <tr> 
   <td>最小幅の数値</td> 
   <td>リストドキュメントフラグメントでローマ数字以外の番号付きリストを使用する場合に、箇条書きまたは番号フィールドに適用される最小幅。</td> 
   <td>8.0mm</td> 
   <td>数値</td> 
  </tr> 
 </tbody> 
</table>

## 通信設定の作成 {#create-correspondence-configuration}

**Adobe Experience Manager web コンソール設定**&#x200B;ページの、「**通信の作成設定**」をタップして、エージェント UI の設定プロパティを表示します。

| プロパティ | 説明 | デフォルト | 指定できる値 |
|---|---|---|---|
| 編集用に解決されたコンテンツを表示 | このチェックボックスを選択すると、エージェント UI でテキストモジュールを編集中に、解決されたコンテンツ（プレースホルダーではなく実際の値）が表示されます。 | 未選択 | 該当なし |
| プレビュー中に透かしを適用 | プレビューモードでインタラクティブ通信の印刷チャネルに透かしを適用する場合は、このチェックボックスをオンにします。 | 未選択 | 適用なし |

## アダプティブフォームおよびインタラクティブ通信 web チャネルの設定 {#adaptive-form-and-interactive-communication-web-channel-configuration}

**Adobe Experience Manager web コンソール設定**&#x200B;ページの「**アダプティブフォームおよびインタラクティブ通信 web チャネルの設定**」をタップして、アダプティブフォームおよびインタラクティブ通信 web チャネルの設定プロパティを表示します。次の表に、インタラクティブ通信に関連するプロパティを示します。

| プロパティ | 説明 | デフォルト | 指定できる値 |
|---|---|---|---|
| プレースホルダーを表示 | このチェックボックスをオンにすると、アダプティブフォームおよびインタラクティブ通信に含まれるフィールドのプレースホルダーが表示されます。 | 選択 | 適用なし |
| 最大キャッシュエントリ数 | キャッシュメモリを使用して取得できるアダプティブフォームおよびインタラクティブ通信の最大数を設定します。 | 100 | 数値 |
| ファイル名を一意にする | アダプティブFormsおよびインタラクティブ通信で添付ファイルとして含まれるファイルに一意の名前を付ける場合は、このチェックボックスを選択します。 | 未選択 | 適用なし |

## アダプティブフォームおよびインタラクティブ通信 web チャネルテーマの設定 {#adaptive-form-and-interactive-communication-web-channel-theme-configuration}

**Adobe Experience Manager Web コンソール設定**&#x200B;ページの「**アダプティブフォームおよびインタラクティブ通信 web チャネルテーマの設定**」をタップして、アダプティブフォームおよびインタラクティブ通信 web チャネルテーマの設定プロパティを表示します。

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
   <td>Adaptive Formsおよび Interactive Communications の作成時に使用できるフォントのリストです。</td> 
   <td><p>グルジア</p> <p>Book Antiqua</p> <p>Times New Roman</p> <p>Arial</p> <p>Arial Black</p> <p>Impact</p> <p>Palatino Linotype</p> </td> 
   <td>すべての有効なAdobeサーバーフォント</td> 
  </tr> 
 </tbody> 
</table>
