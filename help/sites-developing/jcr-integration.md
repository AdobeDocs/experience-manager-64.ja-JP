---
title: JCR 統合
seo-title: JCR Integration
description: JCR レベルで統合する必要がある場合のヒント
seo-description: Tips for when you must integrate at the JCR level
uuid: 11518baf-521e-471d-ad4f-2baa76075cfa
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.4/SITES
content-type: reference
topic-tags: best-practices
discoiquuid: e6647a11-a36e-4808-bb61-29b2895c6b1d
exl-id: 3e9727a5-32f8-40ad-aa06-619f50d109b2
source-git-commit: c5b816d74c6f02f85476d16868844f39b4c47996
workflow-type: tm+mt
source-wordcount: '331'
ht-degree: 45%

---

# JCR 統合{#jcr-integration}

>[!CAUTION]
>
>AEM 6.4 の拡張サポートは終了し、このドキュメントは更新されなくなりました。 詳細は、 [技術サポート期間](https://helpx.adobe.com/jp/support/programs/eol-matrix.html). サポートされているバージョンを見つける [ここ](https://experienceleague.adobe.com/docs/?lang=ja).

## JCR API よりも Sling Resource API の方が望ましい {#prefer-the-sling-resource-api-to-jcr-api}

Sling API は、JCR API よりも高い、より抽象的なレベルで機能します。 これにより、コードの再利用性が向上し、基になるストレージとは無関係になります。 これにより、必要に応じて、ResourceProvider メカニズムを介して外部仮想データを簡単に含めることができます。

## 可能な限りクエリを避ける {#avoid-queries-wherever-possible}

クエリを実行するよりも、常にリポジトリ内を移動してデータを取得する方が速くなります。 エンドユーザーのクエリや、リポジトリ全体から構造化されたコンテンツを検索する必要がある場合など、クエリが必要になる場合がありますが、その他の場合はすべて、必要なノードに移動することをお勧めします。 ナビゲーション要素、「最近の項目リスト」、項目数などのレンダリングロジックでは、常にクエリを回避してください。このような場合は、レンダリング時に直接使用できるように、階層を順を追って進むか、結果をプリキャッシュする方が良いです。

## JCR 監視の範囲の制限 {#restrict-the-scope-of-jcr-observation}

リポジトリでイベントをリッスンするときには、できる限り範囲を絞り込むことが重要です。例えば、`/etc` でリッスンするよりも `/etc/mycompany` でイベントをリッスンする方がはるかに効率的です。決してリポジトリルートではイベントをリッスンしないでください。加えて、コールバックメソッドが実行すべき内容が何もない場合は、可能な限り速やかに処理を完了するようにしてください。

## JCR 管理者アクセスの使用を排除する {#eliminate-use-of-jcr-admin-access}

AEM 6 以降、ResourceResolverFactory からの管理セッションが廃止されているのと同様、管理ログインも廃止されています。代わりに、このタイプのアクセスを必要とするバックオフィス操作には、サービスアカウントを作成してください。ResourceResolverFactory を使用して、このアカウントの ResourceResolver を取得できます。
