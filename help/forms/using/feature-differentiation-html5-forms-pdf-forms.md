---
title: 'HTML5 フォームと PDF フォーム の機能の違い '
seo-title: Feature differentiation between HTML5 forms and PDF forms
description: HTML5 フォームと PDF フォームでサポートされている機能
seo-description: Feature supported in HTML5 forms and PDF forms
uuid: b0a96da5-31d3-4f99-b100-91ad51736ffb
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.4/FORMS
topic-tags: hTML5_forms
discoiquuid: 273096d0-b0e1-4519-8af6-11b3414cc172
feature: Mobile Forms
exl-id: 2b82e68c-ec11-417d-a8e2-769da9b35140
source-git-commit: bd94d3949f0117aa3e1c9f0e84f7293a5d6b03b4
workflow-type: tm+mt
source-wordcount: '485'
ht-degree: 79%

---

# HTML5 フォームと PDF フォーム の機能の違い {#feature-differentiation-between-html-forms-and-pdf-forms}

次の表では、HTML5 フォームと PDF フォームでサポートされている機能について説明します。

<table> 
 <tbody>
  <tr>
   <th>機能</th> 
   <th>HTML5 のフォーム</th> 
   <th>PDF</th> 
  </tr>
  <tr>
   <td>バーコード<br /> </td> 
   <td>ユーザーインターフェイスレベルでは使用できません。 </td> 
   <td>サポート対象</td> 
  </tr>
  <tr>
   <td>署名フィールド<br /> </td> 
   <td><strong>電子署名</strong>はサポートされてませんが、紙上のような署名のために新しい「<strong>Scribble Signature</strong>」フィールドが追加されました。「<strong>Scribble Signature</strong>」フィールドを使用し、フォームに署名を手で書くことができます。署名はフォーム上で画像として保存されます。「<strong>Scribble Signature</strong>」フィールドには位置情報を保存できます。</td> 
   <td><strong>電子署名</strong>用の署名フィールドが使用可能。</td> 
  </tr>
  <tr>
   <td>データの結合</td> 
   <td>サポート対象</td> 
   <td>サポート対象</td> 
  </tr>
  <tr>
   <td>画像</td> 
   <td>データ URI スキームは画像の表示に使用されます。すべてのブラウザーの最新バージョンはこのスキームをサポートしていますが、それぞれのブラウザーでサポートされる画像形式の範囲に違いがあります。<br /> </td> 
   <td>.gif、.png、.jpeg、.bmp、.tiff 形式がサポートされます。</td> 
  </tr>
  <tr>
   <td>ページネーション<br /> </td> 
   <td><p>HTML5 フォームは、PDF フォームと同様の外観を提供するためにパネルとボックスに分けられています。ページのサイズは動的に計算されます。HTML5 フォーム内のページのすべてのコンテンツが削除されたか非表示としてマークされた場合、空白ページは非表示になり、ページ間にある空白ページの空白スペースは表示されません。</p> <p>データをマージするかスクリプトのコンテンツをページに追加した場合、新しく追加したコンテンツを取り込めるようにページの長さが拡張されます。新しく追加したコンテンツを取り込むために新しいページがフォームに追加されることはありません。 </p> <p><strong>注意：</strong>HTML5 フォーム内のページのすべてのコンテンツが削除されたか非表示としてマークされた場合、1 ページと 2 ページ間にある空白ページ（空白スペース）は表示されますが、その他のページ間にある空白ページ（空白スペース）は表示されません。</p> </td> 
   <td>PDFでのページネーションは、結合されたデータコンテンツまたはユーザーコンテンツに依存し、それに基づいてページ数が増減します。</td> 
  </tr>
  <tr>
   <td>ヘッダー/フッター </td> 
   <td>サポート対象。<br /> <br /> HTML5 モバイルフォームは改ページをサポートしていないので、ヘッダーとフッターは 1 回だけ表示されます。 ただし、レイアウトを設定することにより、モバイルフォームプレビュー内の複数の場所に表示させることができます。<br /> </td> 
   <td>サポート対象。</td> 
  </tr>
  <tr>
   <td>カスタムウィジェット</td> 
   <td>モバイルデバイスでのユーザーエクスペリエンスを強化するために、ウィジェットをカスタマイズすることができます。<br /> </td> 
   <td>すべてのウィジェットはロックダウンされ、カスタムウィジェットはプラグインできない。<br /> </td> 
  </tr>
  <tr>
   <td>XFA スクリプト API</td> 
   <td>最もよく使用される XFA スクリプト構文をサポートします。 サポートされている構成の詳細なリストについては、 <a href="/help/forms/using/scripting-support.md">スクリプトサポート</a>.</td> 
   <td>すべての XFA スクリプトの構成要素をサポート。</td> 
  </tr>
  <tr>
   <td>Acrobat スクリプト API </td> 
   <td>HTML5 フォームは、最も一般的に使用される API をサポートしています。詳しくは、 <a href="/help/forms/using/scripting-support.md">スクリプトサポート</a>.</td> 
   <td>PDF ファイルが Acrobat または Reader 内で開かれる場合も、それは Acrobat が提供するすべてのスクリプト API をサポートします。</td> 
  </tr>
  <tr>
   <td>右から左に書く言語のサポート </td> 
   <td>サポート対象</td> 
   <td>サポート対象</td> 
  </tr>
 </tbody>
</table>

ベストプラクティスに従って、HTML5 レンディションのフォームHTMLを有効にし、Template5 フォームと XFA ベースのPDFの動作と外観の一貫性を確保します。 ベストプラクティスの詳しい一覧については、「[HTML5 フォームをデザインする上でのベストプラクティス](/help/forms/using/best-practices-for-html5-forms.md)」を参照してください。
