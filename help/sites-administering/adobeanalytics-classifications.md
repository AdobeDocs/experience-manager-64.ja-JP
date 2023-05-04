---
title: Adobe Classifications
seo-title: Adobe Classifications
description: Adobe分類の詳細。
seo-description: Learn about Adobe Classifications.
uuid: 57fb59f4-da90-4fe7-a5b1-c3bd51159a16
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.4/SITES
topic-tags: integration
content-type: reference
discoiquuid: 6787511a-2ce0-421a-bcfb-90d5f32ad35e
exl-id: 25e58c68-5c67-4894-9a54-1717d90d7831
source-git-commit: c5b816d74c6f02f85476d16868844f39b4c47996
workflow-type: tm+mt
source-wordcount: '609'
ht-degree: 36%

---

# Adobe Classifications{#adobe-classifications}

>[!CAUTION]
>
>AEM 6.4 の拡張サポートは終了し、このドキュメントは更新されなくなりました。 詳細は、 [技術サポート期間](https://helpx.adobe.com/jp/support/programs/eol-matrix.html). サポートされているバージョンを見つける [ここ](https://experienceleague.adobe.com/docs/?lang=ja).

Adobe Classifications は、分類データをスケジュールに従って [Adobe Analytics](/help/sites-administering/adobeanalytics.md) にエクスポートします。エクスポーターは、 **com.adobe.cq.scheduled.exporter.Exporter**.

次の手順で設定します。

1. 次の場所に移動： **ツール/クラウドサービス** から **Adobe Analytics** 」セクションに入力します。
1. 新しい設定を追加します。 次のように表示されます。 **Adobe Analytics Classifications** 設定テンプレートが **Adobe Analytics Framework** 設定。 を指定します。 **タイトル** および **名前** 必要に応じて：

   ![aa-25](assets/aa-25.png)

1. クリック **作成** をクリックして設定を行います。

   ![chlimage_1](assets/chlimage_1.png)

   プロパティには次のものがあります。

   | **フィールド** | **説明** |
   |---|---|
   | Enabled | 選択 **はい** をクリックして、Adobeの分類設定を有効にします。 |
   | 競合時に上書き | 選択 **はい** データの競合を上書きする場合はを選択します。 デフォルトでは、これはに設定されています。 **いいえ**. |
   | 削除実行  | 次に設定した場合： **はい**：書き出し後に処理されたノードを削除します。 デフォルトはです。 **False**. |
   | ジョブの書き出しに関する説明 | 分類ジョブの説明をAdobeします。 |
   | 通知電子メール | Adobe Classifications の通知用のメールアドレスを入力します。 |
   | レポートスイート | インポートジョブを実行するレポートスイートを入力します。 |
   | データセット | インポートジョブを実行するデータセット関係 ID を入力します。 |
   | 変換サービス | ドロップダウンメニューから、変換サービスの実装を選択します。 |
   | データソース | データコンテナのパスに移動します。 |
   | スケジュールを書き出し | エクスポートのスケジュールを選択します。 デフォルトは 30 分ごとです。 |

1. クリック **OK** 設定を保存します。

## ページサイズの変更 {#modifying-page-size}

レコードはページで処理されます。 デフォルトでは、Adobe Classifications はページサイズが 1,000 のページを作成します。

Adobe Classifications の定義に従い、ページの最大サイズは 25,000 に設定ができます（Felix コンソールから変更可）。エクスポート中に、Adobe Classifications はソースノードをロックして、同時変更を防ぎます。ノードは、書き出し後、エラー時、またはセッションが閉じられたときに、ロックが解除されます。

ページサイズを変更するには：

1. **https://&lt;host>:&lt;port>/system/console/configMgr** にある OSGI コンソールに移動し、「**Adobe AEM Classifications Exporter**」を選択します。

   ![aa-26](assets/aa-26.png)

1. を更新します。 **書き出しページサイズ** 必要に応じて、「 」をクリックします。 **保存**.

## SAINTDefaultTransformer {#saintdefaulttransformer}

>[!NOTE]
>
>Adobe分類は、以前はSAINTエクスポータと呼ばれていました。

エクスポータは、変換サービスを使用して、書き出しデータを特定の形式に変換できます。 Adobe Classifications では、Transformer インターフェイスを実装するサブインターフェイス `SAINTTransformer<String[]>` が提供されています。このインターフェイスは、データタイプを SAINT API で使用される `String[]` に制限し、マーカーインターフェイスで対応するサービスを検索して選択するために使用されます。

デフォルト実装の SAINTDefaultTransformer では、書き出しソースの子リソースは、keys というプロパティ名と values というプロパティ値を持つレコードとして扱われます。**キー**&#x200B;列は、最初の列として自動的に追加され、その値がノード名になります。名前空間プロパティ（：を含む）は無視されます。

*ノード構造：*

* id-classification `nt:unstructured`

   * 1 `nt:unstructured`

      * Product = My Product Name (String)
      * Price = 120.90（文字列）
      * サイズ= M（文字列）
      * Color = black (String)
      * Color^Code = 101 (String)

**SAINTヘッダーとレコード：**

| **キー** | **製品** | **価格** | **サイズ** | **カラー** | **Color^Code** |
|---|---|---|---|---|---|
| 1 | 製品名 | 120.90 | M | black | 101 |

プロパティには次のものがあります。

<table> 
 <tbody> 
  <tr> 
   <td><strong>プロパティのパス</strong></td> 
   <td><strong>説明</strong></td> 
  </tr> 
  <tr> 
   <td>変圧器</td> 
   <td>SAINTransformer 実装のクラス名</td> 
  </tr> 
  <tr> 
   <td>email</td> 
   <td>通知用電子メールアドレス。</td> 
  </tr> 
  <tr> 
   <td>reportsuites</td> 
   <td>インポートジョブを実行するレポートスイート ID。 </td> 
  </tr> 
  <tr> 
   <td>データセット</td> 
   <td>インポートジョブを実行するデータセット関係 ID。 </td> 
  </tr> 
  <tr> 
   <td>description</td> 
   <td>ジョブの説明。<br /> </td> 
  </tr> 
  <tr> 
   <td>上書き</td> 
   <td>データの競合を上書きするフラグ。 デフォルトはです。 <strong>false</strong>.</td> 
  </tr> 
  <tr> 
   <td>checkdivisions</td> 
   <td>レポートスイートの互換性を確認するフラグ。 デフォルトはです。 <strong>true</strong>.</td> 
  </tr> 
  <tr> 
   <td>deleteprocessed</td> 
   <td>書き出し後に処理されたノードを削除するフラグ。 デフォルトはです。 <strong>false</strong>.</td> 
  </tr> 
 </tbody> 
</table>

## Adobe分類の書き出しの自動化 {#automating-adobe-classifications-export}

独自のワークフローを作成し、新しいインポートを実行すると、に適切で正しく構造化されたデータが作成されます。 **/var/export/** 分類に書き出せるようにするAdobe。
