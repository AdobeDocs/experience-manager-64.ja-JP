---
title: 顧客向けのユーザーインターフェイスの推奨事項
seo-title: User Interface Recommendations for Customers
description: 従来のユーザーインターフェイスとタッチ操作向けのユーザーインターフェイスに関連する推奨事項のリストです。
seo-description: A list of recommendations related to the classic and touch-optimized user interfaces.
uuid: c661fb10-4dbc-4f8b-93be-3e77af1ad095
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.4/SITES
content-type: reference
topic-tags: best-practices
discoiquuid: 42bf42cb-0c6c-4390-8170-2c540c4d3ed3
exl-id: 1e5172d9-47a3-4d73-b749-166e201f4eef
source-git-commit: 51358642a2fa8f59f3f5e3996b0c37269632c4cb
workflow-type: tm+mt
source-wordcount: '777'
ht-degree: 28%

---

# 顧客向けのユーザーインターフェイスの推奨事項{#user-interface-recommendations-for-customers}

Adobe Experience Manager 6.4 には、統合Experience CloudUI とクラシック UI の 2 つの UI が付属しています。

このドキュメントは、お客様が状況に応じて使用する UI を選択できるようにガイドすることを目的としています。

目標条件：

* **UI（または標準の UI）** 5.6.0 でテクノロジープレビューとして導入され、以降のリリースで拡張された最新のユーザーインターフェイス。以前はタッチ操作向け UI またはタッチ UI と呼ばれていた Adobe Experience Cloud の統一されたユーザー体験を基盤としています。

* **クラシック UI**
2008 年の CQ 5.1 で導入された、ExtJS テクノロジーに基づくユーザーインターフェイス。

* **サイト管理者**
サイトの階層を管理（参照を移動、アクティベート、管理）して、新しいページを作成する機能。

* **ページオーサリング**
ページのコンテンツを追加および編集する機能。

* **DAM／アセット管理者**
デジタルアセット（画像、ビデオ、ドキュメント、ダウンロードを含む）を管理する機能。

* **ContextHub**&#x200B;訪問者に関する情報を集計し、様々な目的で使用する機能。サイトの訪問者をシミュレートするユーザーインターフェイスを備えています。AEM 6.2 より、以前の ClientContext に代わって ContextHub が使用されています。

## 一般 {#general}

過去数年の間に、Adobeは、すべてのAdobe Experience Cloudソリューションを統合ユーザーインターフェイスで更新しました。 Experience Cloud・ソリューションをまたいだユーザーは、アプリケーションの使用と運用に関する共通のパターンに基づいて、一貫した経験を得ることができます。 各リリースで、Adobeは、様々なソリューションで作業しているお客様からのフィードバックに基づいて、ユーザーインターフェイスを絞り込んでいます。

2008 年に導入され、バージョン 5.0 ～ 5.6.1 を実行するお客様が使用するAdobe Experience Managerの元のユーザーインターフェイス（旧称 CQ5）は、AEM 6.4 に存在します。これにより、お客様は 6.4 に更新でき、同じユーザーインターフェイスを使用し続けながら、新しい機能を備えた更新済みです。

Adobeでは、2018/19で新しい UI への切り替えを計画することをお勧めします。 これは、6.4 へのアップデート中に実行することも、アップデート後に別のプロジェクトで実行することもできます。この場合、カスタマイズとコンポーネントダイアログに対する必要な調整が含まれます。

Adobeでは、AEM 6.4 以降のクラシック UI の機能強化は予定されていません。クラシック UI は非推奨の間も完全にサポートされたままになります。

## ルールと推奨事項 {#rules-and-recommendations}

Adobe Experience Manager 6.4 の製品管理からの推奨事項を次に示します。

<table> 
 <tbody> 
  <tr> 
   <th>私のプロジェクト…</th> 
   <th>推奨事項</th> 
  </tr> 
  <tr> 
   <td>Adobe Experience Managerを使い始めたばかりです。</td> 
   <td>デフォルトの UI を使用します。</td> 
  </tr> 
  <tr> 
   <td><p>しばらくAEMを使用しています。</p> <p>標準搭載の製品 UI を使用し、サイト用のカスタムコンポーネントを開発しました。<br /> </p> </td> 
   <td> 
    <ol> 
     <li>6.4 に更新しました。</li> 
     <li>サイト管理やアセットなどにデフォルトの UI を使用します。 等。<br /> </li> 
     <li>「ページを編集」アクションを設定して、クラシック UI のページエディターを開きます。 詳しくは、 <a href="#selecting-your-ui">UI の選択</a>.</li> 
    </ol> <p>次に、第 2 段階で、次のようになります。</p> 
    <ol> 
     <li>Coral 3 ダイアログ形式を使用するようにコンポーネントダイアログを更新します。 アドビは、コンポーネントの更新に<a href="/help/sites-developing/modernization-tools.md">AEM 最新化ツール</a>を使用することをお勧めします。</li> 
    </ol> </td> 
  </tr> 
  <tr> 
   <td>統合により、ClientContext を使用するサイトを構築したことがある。<br /> </td> 
   <td> 
    <ol> 
     <li>6.4 に更新しました。</li> 
     <li>サイト管理やアセットなどにデフォルトの UI を使用します。 等。</li> 
     <li>「ページを編集」アクションを設定して、クラシック UI のページエディターを開きます。 詳しくは、 <a href="#selecting-your-ui">UI の選択</a>.</li> 
    </ol> <p>次に、第 2 段階で、次のようになります。</p> 
    <ol> 
     <li>Coral 3 ダイアログ形式を使用するようにコンポーネントダイアログを更新します。 アドビは、コンポーネントの更新に <a href="/help/sites-developing/modernization-tools.md">AEM 最新化ツール</a>を使用することをお勧めします。</li> 
     <li>ContextHub を設定し (ClientContextの代わり )、ContextHub を使用するようにページテンプレートを更新します。 ContextHub には、カスタムモードストアを読み込める互換モードがあることに注意してください。</li> 
    </ol> </td> 
  </tr> 
  <tr> 
   <td><p>CQ/AEMを長年使用しています。</p> <p>製品 UI（Site Admin など）を拡張し、広範な編集ダイアログを使用してコンポーネントを構築済み。</p> </td> 
   <td><p>6.4 に更新し、すべてのユーザーのページオーサリングのデフォルトとしてクラシック UI を設定します。 詳しくは、 <a href="#selecting-your-ui">UI の選択</a>.</p> <p>次に、プロジェクトを開始してカスタマイズを適用し、Coral 3 形式のコンポーネントダイアログを最適化します。 詳しくは、 <a href="#resources-to-help">役立つリソース</a>.<br /> </p> </td> 
  </tr> 
 </tbody> 
</table>

## FAQ {#faq}

ナレッジベースの記事を参照してください。 [タッチ操作対応 UI オーサリングに関する FAQ](https://helpx.adobe.com/jp/experience-manager/kb/index/touchui_faq.html)、詳細は。クラシック UI の廃止スケジュールに関する情報を含めます。

## UI の選択 {#selecting-your-ui}

システムを必要に応じて設定する方法について詳しくは、[UI の選択](/help/sites-authoring/select-ui.md)を参照してください。

## タッチ操作向け UI のステータス {#touch-optimized-ui-status}

AEM 6.3 でのタッチ操作向け UI の機能強化について詳しくは、 [最新情報](/help/release-notes/release-notes.md#what-s-new) 」を参照してください。

全体的な概要については、[タッチ操作対応 UI 機能のステータス](/help/release-notes/touch-ui-features-status.md)ページを参照してください。

## 役立つリソース {#resources-to-help}

基本操作の背景情報は次のとおりです。

* [オーサー環境の使用](/help/sites-authoring/home.md).
* [ページのオーサリング](/help/sites-authoring/author-environment-tools.md).

開発に関する詳細な情報は、次のとおりです。

* [タッチ操作向け UI のアーキテクチャ](/help/sites-developing/touch-ui-concepts.md).
* 以下を使用： [AEM Modernization Tools](/help/sites-developing/modernization-tools.md) コンポーネントの編集ダイアログをクラシック UI からタッチ操作向け UI に変換する場合。

* [タッチ操作向け UI の構造](/help/sites-developing/touch-ui-structure.md).

* [タッチ操作向け UI でのコンソールのカスタマイズ](/help/sites-developing/customizing-consoles-touch.md) （サンプルコードが含まれます）。

* [タッチ操作向け UI でのページオーサリングのカスタマイズ](/help/sites-developing/customizing-page-authoring-touch.md) （サンプルコードが含まれます）。

* [Granite UI ドキュメント](https://helpx.adobe.com/experience-manager/6-4/sites/developing/using/reference-materials/granite-ui/api/index.html)。
