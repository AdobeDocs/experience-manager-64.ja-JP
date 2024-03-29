---
title: ベストプラクティス
description: 管理者の立ち上げと実行を支援するAdobe Experience Managerのベストプラクティスを、Adobeエンジニアリングチームとコンサルティングチームがまとめて説明します。
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.4/SITES
content-type: reference
topic-tags: best-practices
exl-id: 8c41dba4-bedc-4747-b67d-fd89d71c8b2c
source-git-commit: c5b816d74c6f02f85476d16868844f39b4c47996
workflow-type: tm+mt
source-wordcount: '573'
ht-degree: 47%

---

# ベストプラクティス{#best-practices}

>[!CAUTION]
>
>AEM 6.4 の拡張サポートは終了し、このドキュメントは更新されなくなりました。 詳細は、 [技術サポート期間](https://helpx.adobe.com/jp/support/programs/eol-matrix.html). サポートされているバージョンを見つける [ここ](https://experienceleague.adobe.com/docs/?lang=ja).

ベストプラクティスでは、AEMをできるだけ効率的かつ効果的に開発、管理または使用する方法について説明します。 このトピックのリストは、AEMの様々な領域で増えています。

次の領域に、ベストプラクティスに関するドキュメントが用意されています。

* [Assets](#assets)
* [Sites](#sites)

オーサリング、デプロイ、メンテナンスまたは開発のベストプラクティスについては、次のページを参照してください。

* [オーサリングのベストプラクティス](/help/sites-authoring/best-practices.md)
* [開発のベストプラクティス](/help/sites-developing/best-practices.md)
* [デプロイのベストプラクティス](/help/sites-deploying/best-practices.md)

以下の表では、特定のドキュメントについて説明し、リンクします。

## Assets {#assets}

Dynamic Media 機能や Dynamic Media Classic 統合などの、Assets のベストプラクティスについては、次のトピックで説明されています。

<table> 
 <tbody>
  <tr>
   <td>負荷時のシステムの安定性とパフォーマンスを向上を実現するための Assets における様々な領域でのベストプラクティス</td> 
   <td><a href="/help/assets/organize-assets.md">Assets のベストプラクティス</a></td> 
   <td>Assets に関する様々な領域でのベストプラクティスガイドへのリンクが記載されています。 これらのガイドを確認すると、エンタープライズアセット管理システムを構築および管理する知識を習得し、そのツールを利用できるようになります。</td> 
  </tr>
  <tr>
   <td>コンテンツの整理方法（フォルダー階層）</td> 
   <td><a href="/help/assets/organize-assets.md">ファイル管理のベストプラクティス</a></td> 
   <td>ビデオ、メタデータ、画像処理は常にフォルダーに適用されるので、処理プロファイルの多くはフォルダーベースです。 このベストプラクティスドキュメントでは、フォルダー階層を定義して設定する方法を説明します。階層は、コンテンツの処理方法に大きな影響を与えるので、この階層を定義して設定する方法を説明します。 </td> 
  </tr>
  <tr>
   <td>Dynamic Media ClassicとAEMの統合</td> 
   <td><a href="/help/sites-administering/scene7.md#best-practices-for-integrating-scene-with-aem">Dynamic Media ClassicとAEMの統合のベストプラクティス</a></td> 
   <td><p>ポーリングインポーターをオンにするタイミング、統合を推進するテスト方法、およびコンテンツブラウザーを使用するタイミングと Assets への直接アップロードを使用するタイミングについて説明します。</p> </td> 
  </tr>
  <tr>
   <td>画像プリセットオプション</td> 
   <td><a href="/help/assets/managing-image-presets.md#understanding-image-presets">画像プリセット</a>の概要および<a href="/help/assets/managing-image-presets.md#image-preset-options">画像プリセットのベストプラクティス</a></td> 
   <td>に関するドキュメントの一部として <a href="/help/assets/managing-image-presets.md">画像プリセットの管理</a>以下のトピックでは、画像プリセットの概要と、画像プリセットオプションの選択に関するベストプラクティスについて説明します。</td> 
  </tr>
  <tr>
   <td>Dynamic MediaとDynamic Media Classicの直接統合</td> 
   <td><a href="/help/sites-administering/scene7.md#aem-scene-integration-versus-dynamic-media">Dynamic Media Classic/AEMとDynamic Mediaの統合</a></td> 
   <td>ダイナミックメディアソリューションの使用が適している状況、Scene7 と AEM を統合すべき状況またはその両方を使用すべき状況について説明します。</td> 
  </tr>
 </tbody>
</table>

## Sites {#sites}

Web サイトコンテンツの管理とオーサリングには、次に示すベストプラクティスがあります。

<table> 
 <tbody>
  <tr>
   <td>GDPR コンプライアンス</td> 
   <td><a href="/help/sites-administering/gdpr-compliance-sites.md">AEM Sites GDPR コンプライアンス</a></td> 
   <td>データのプライバシー権に関する EU 一般データ保護規則（GDPR）が 2018 年 5 月に発効します。AEM Sitesは GDPR に準拠しています。 このページでは、AEM Sitesで GDPR 要求を処理する手順を説明します。 プライベートデータの格納場所や、それらのデータを手動で、またはコードを使用して削除する方法について説明します。</td> 
  </tr>
  <tr>
   <td>インスタンスのデフォルト UI を定義します。</td> 
   <td><p><a href="/help/sites-authoring/select-ui.md#configuring-the-default-ui-for-your-instance">個別の例に合わせたデフォルト UI の設定</a></p> </td> 
   <td>AEMには次の 2 つの UI があります。タッチ操作向けとクラシック。 この節では、インスタンスのデフォルト UI を定義する方法について説明します。</td> 
  </tr>
  <tr>
   <td>マルチサイト管理</td> 
   <td><a href="/help/sites-administering/msm-best-practices.md">MSM のベストプラクティス</a></td> 
   <td>コンテンツのデプロイメントを自動化するための MSM の使用に関するベストプラクティスです。 </td> 
  </tr>
  <tr>
   <td>コンテンツの翻訳</td> 
   <td><a href="/help/sites-administering/tc-bp.md">翻訳のベストプラクティス</a></td> 
   <td>多言語サイトの計画と実装に関するベストプラクティス。</td> 
  </tr>
  <tr>
   <td>ユーザー管理</td> 
   <td><a href="/help/sites-administering/security.md#best-practices">権限と特別な権限のベストプラクティス</a></td> 
   <td>権限と特別な権限を使用する場合のベストプラクティスについて説明しています。 </td> 
  </tr>
  <tr>
   <td>ワークフロー</td> 
   <td><a href="/help/sites-developing/workflows-best-practices.md#configuration">ワークフローのベストプラクティス - 設定</a></td> 
   <td>ワークフローを使用すると、Adobe Experience Manager（AEM）アクティビティを自動化し、AEM 環境で発生する大量のプロセスをワークフローで表現できます。したがって、ワークフローの実装の計画と設定は慎重におこなうことが強く推奨されます。</td> 
  </tr>
 </tbody>
</table>
