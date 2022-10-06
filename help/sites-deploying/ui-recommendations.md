---
title: 顧客向けのユーザーインターフェイスの推奨事項
seo-title: User Interface Recommendations for Customers
description: クラシックユーザーインターフェイスおよびタッチ操作向けユーザーインターフェイスに関連する推奨事項のリスト。
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
ht-degree: 97%

---

# 顧客向けのユーザーインターフェイスの推奨事項{#user-interface-recommendations-for-customers}

Adobe Experience Manager 6.4 には、統一された Experience Cloud UI とクラシック UI という 2 つの UI が付属しています。

ここでは、状況に応じて顧客がどの UI の使用を選択する必要があるかについて説明します。

関連用語：

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

過去数年にわたり、アドビではすべての Adobe Experience Cloud ソリューションを統一されたユーザーインターフェイスに更新してきました。Experience Cloud ソリューションのユーザーには、アプリケーションの使用および操作方法について共通のパターンを持つ一貫性のある体験が提供されます。すべてのリリースで、様々なソリューションを使用している顧客からのフィードバックに基づいて、アドビはユーザーインターフェイスを改善しています。

2008 年に登場し、Adobe Experience Manager（旧称 CQ5）のバージョン 5.0 ～ 5.6.1 で使用されていた元のユーザーインターフェイスも、引き続き AEM 6.4 に残されています。そのため、6.4 にアップデートしても、従来と同じユーザーインターフェイスを使用して、新しい機能を含むアップデートされたプラットフォームを利用することができます。

お客様には、2018 年または 2019 年に新しい UI への切り替えを予定することをお勧めしています。この切り替えは、6.4 にアップデートするときに（またはアップデート後に個別のプロジェクトで）おこなうことができます。その際に、カスタマイズとコンポーネントダイアログの調整が必要になります。

アドビでは、AEM 6.4 以降、クラシック UI のさらなる機能強化を予定しておりません。クラシック UI は廃止されますが、引き続き完全にサポートされます。

## ルールと推奨事項 {#rules-and-recommendations}

Adobe Experience Manager 6.4 に関する製品管理からの推奨事項を以下のリストに示します。

<table> 
 <tbody> 
  <tr> 
   <th>プロジェクトの状況</th> 
   <th>推奨事項</th> 
  </tr> 
  <tr> 
   <td>Adobe Experience Manager を使い始めようとしている。</td> 
   <td>デフォルトの UI を使用します。</td> 
  </tr> 
  <tr> 
   <td><p>AEM をしばらくの間使用している。</p> <p>製品の UI をそのまま使用していて、サイトのカスタムコンポーネントを開発している。<br /> </p> </td> 
   <td> 
    <ol> 
     <li>6.4 にアップデートします。</li> 
     <li>サイト管理、アセットなどには、デフォルトの UI を使用します。等。<br /> </li> 
     <li>クラシック UI のページエディターを表示するよう「ページを編集」のアクションを設定します。<a href="#selecting-your-ui">UI の選択</a>を参照してください。</li> 
    </ol> <p>次に第 2 段階として、</p> 
    <ol> 
     <li>Coral 3 ダイアログ形式を使用するようにコンポーネントダイアログを更新します。アドビは、コンポーネントの更新に<a href="/help/sites-developing/modernization-tools.md">AEM 最新化ツール</a>を使用することをお勧めします。</li> 
    </ol> </td> 
  </tr> 
  <tr> 
   <td>統合により、ClientContext を使用するサイトを構築したことがある。<br /> </td> 
   <td> 
    <ol> 
     <li>6.4 にアップデートします。</li> 
     <li>サイト管理、アセットなどには、デフォルトの UI を使用します。等。</li> 
     <li>クラシック UI のページエディターを表示するよう「ページを編集」のアクションを設定します。<a href="#selecting-your-ui">UI の選択</a>を参照してください。</li> 
    </ol> <p>次に第 2 段階として、</p> 
    <ol> 
     <li>Coral 3 ダイアログ形式を使用するようにコンポーネントダイアログを更新します。アドビは、コンポーネントの更新に <a href="/help/sites-developing/modernization-tools.md">AEM 最新化ツール</a>を使用することをお勧めします。</li> 
     <li>ContextHub（ClientContext の後継）を設定し、ContextHub を使用するようページテンプレートを更新します。ContextHub には、カスタムの ClientContext のストアを読み込むことができる互換モードがあります。</li> 
    </ol> </td> 
  </tr> 
  <tr> 
   <td><p>CQ／AEM を長年使用している。</p> <p>製品 UI（サイト管理者など）を拡張し、詳細な編集ダイアログでコンポーネントを構築したことがある。</p> </td> 
   <td><p>6.4 にアップデートし、すべてのユーザーに対するページオーサリングのデフォルトとしてクラシック UI を設定します。<a href="#selecting-your-ui">UI の選択</a>を参照してください。</p> <p>次に、プロジェクトを開始してカスタマイズを適用し、コンポーネントダイアログを Coral 3 形式で最適化します。<a href="#resources-to-help">役に立つリソース</a>を参照してください。<br /> </p> </td> 
  </tr> 
 </tbody> 
</table>

## FAQ {#faq}

詳しくは、ナレッジベースの記事 [Touch UI Authoring FAQ](https://helpx.adobe.com/jp/experience-manager/kb/index/touchui_faq.html) を参照してください。クラシック UI の廃止予定に関する情報も提供しています。

## UI の選択 {#selecting-your-ui}

システムを必要に応じて設定する方法について詳しくは、[UI の選択](/help/sites-authoring/select-ui.md)を参照してください。

## タッチ操作向け UI の状況 {#touch-optimized-ui-status}

AEM 6.3 でのタッチ操作向け UI の機能強化について詳しくは、リリースノートの[新機能](/help/release-notes/release-notes.md#what-s-new)を参照してください。

全体的な概要については、[タッチ操作対応 UI 機能のステータス](/help/release-notes/touch-ui-features-status.md)ページを参照してください。

## 役に立つリソース {#resources-to-help}

基本処理の背景情報については、以下を参照してください。

* [オーサー環境の使用](/help/sites-authoring/home.md)。
* [ページのオーサリング](/help/sites-authoring/author-environment-tools.md).

開発情報について詳しくは、以下を参照してください。

* [タッチ操作向け UI のアーキテクチャ](/help/sites-developing/touch-ui-concepts.md)。
* 以下を使用： [AEM Modernization Tools](/help/sites-developing/modernization-tools.md) コンポーネントの編集ダイアログをクラシック UI からタッチ操作向け UI に変換する場合。

* [タッチ操作向け UI の構造](/help/sites-developing/touch-ui-structure.md)。

* [タッチ操作向け UI のコンソールのカスタマイズ](/help/sites-developing/customizing-consoles-touch.md)（サンプルコードを含む）。

* [タッチ操作向け UI のページオーサリングのカスタマイズ](/help/sites-developing/customizing-page-authoring-touch.md)（サンプルコードを含む）。

* [Granite UI ドキュメント](https://helpx.adobe.com/jp/experience-manager/6-4/sites/developing/using/reference-materials/granite-ui/api/index.html)。
