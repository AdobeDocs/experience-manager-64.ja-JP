---
title: モデルの概要
seo-title: Models Overview
description: モデルの概要
seo-description: null
uuid: e09dac52-9515-43f7-9d3b-6637e2283d59
contentOwner: Jyotika Syal
content-type: reference
products: SG_EXPERIENCEMANAGER/6.4/MOBILE
discoiquuid: c8281f98-9811-42f7-9a31-f82dd0f09319
exl-id: 03f06c10-9fe1-497e-89b0-70acb7ca7800
source-git-commit: c5b816d74c6f02f85476d16868844f39b4c47996
workflow-type: tm+mt
source-wordcount: '819'
ht-degree: 2%

---

# モデルの概要{#models-overview}

>[!CAUTION]
>
>AEM 6.4 の拡張サポートは終了し、このドキュメントは更新されなくなりました。 詳細は、 [技術サポート期間](https://helpx.adobe.com/jp/support/programs/eol-matrix.html). サポートされているバージョンを見つける [ここ](https://experienceleague.adobe.com/docs/?lang=ja).

>[!NOTE]
>
>Adobeは、単一ページアプリケーションのフレームワークベースのクライアントサイドレンダリング（React など）を必要とするプロジェクトでは、SPA Editor を使用することをお勧めします。 [詳細情報](/help/sites-developing/spa-overview.md)を参照してください。

モデル管理では、最終的なデータオブジェクトに関連付けるために、モデルの作成と管理をおこないます。 各モデルには、オブジェクトの作成とレンダリングを容易にするために必要なすべてのプロパティとフィールド定義が含まれます。

モデル管理では、 **モデル**, **エンティティ**、および **スペース**. 次の図は、AEMコンテンツとモデルの関係を示しています。

![chlimage_1-81](assets/chlimage_1-81.png)

## コンテンツモデル {#the-content-model}

モデルは、コンテンツのタイプを表し、ネイティブアプリケーションで使用できる情報を示します。 コンテンツの構成要素を示します。 コンテンツモデルとは、コンテンツの一部を構築する方法のルールです。 コンテンツモデルには、使用可能なデータ、使用可能なアセット、アセットとデータの関係、他のコンテンツモデルとの関係、使用可能なメタデータが含まれます。

また、モデルは、既存のAEMコンテンツを、ネイティブのモバイルアプリで簡単に使用できるオブジェクトに変換する方法としても機能します。

コンテンツサービスには、アセット、アセットコレクション、HTMLページ、アプリ設定、チャネルに依存しないページなど、一般的なオブジェクト用に、あらかじめ用意されているいくつかのモデルが用意されています。 これらは、AEMの開発作業を必要とせずに、特定のお客様のニーズに合わせて設定できます。

ユーザーは独自のモデルを作成できます。 これにより、AEMでまだ管理されていない新しいコンテンツタイプを作成できます。 モデルの作成は、既存のプリミティブタイプを使用した UI を通じて行われます。

次の図に、AEM Mobile Apps のコンテンツモデルと、エンティティ、フォルダー、スペースをアプリに割り当てる方法を示します。

![chlimage_1-82](assets/chlimage_1-82.png)

### モデル {#the-models}

モデルは、エンティティの作成方法を決定するために使用されます。 エンティティで使用可能なものと、そのデータをAEMコンテンツから生成する方法を定義します。 スペース、フォルダ、エンティティの操作を開始する前に、モデルの作成と管理に関する知識が必要です。

>[!NOTE]
>
>モデルは、複数のアプリで使用できるので、1 つのアプリの外部に存在します。

詳しくは、 **[モデル](/help/mobile/administer-mobile-apps.md)** を使用して、ダッシュボードとリポジトリでモデルを作成および管理します。

### コンテンツモデル内のエンティティ {#entities-in-content-model}

エンティティは、コンテンツモデルのインスタンスです。 エンティティは、コンテンツサービス API を通じてクライアントサイドライブラリに公開され、ネイティブアプリがチャネルに依存しない方法でコンテンツにアクセスする方法を提供します。

既存のAEMコンテンツの場合、モデルとAEMコンテンツソースを使用してエンティティが生成されます。 例えば、ページエンティティは、AEMページとページモデルから生成される、チャネルとレイアウトに依存しないオブジェクトです。

エンティティの参照コンテンツを変更すると、エンティティが変更されます。 例えば、 *cq:page* が更新されると、そのページに基づくエンティティも更新されます。

詳しくは、 **[エンティティの操作](/help/mobile/spaces-and-entities.md)** モデルからカスタムエンティティを作成する場合。

>[!NOTE]
>
>顧客が新しいモデルを作成したなど、モデルが既存のAEMコンテンツに対応していない場合は、UI が表示され、顧客が新しいエンティティを作成できます。

### コンテンツモデル内のスペース {#spaces-in-content-model}

スペースは、エンティティを整理してアクセスしやすくするために使用します。 1 つのスペースには、1 つ以上のエンティティタイプを含めることができ、サブフォルダーを含めることもできます。

AEM側では、スペースを使用すると、関連するエンティティを簡単に管理できます。 また、認証権限を割り当てる場合にも使用できます。 スペースに対して認証を行い、そのスペース内のエンティティを保護します。

*例*：

ユーザーには、エンティティの一般的な分類が 3 つあります。 1 つは内部でのみ使用するため、もう 1 つは公開用に承認されますが、3 つ目は多くのアプリで使用される一般的なエンティティ用です。 管理を容易にするために、ユーザは、次の 3 つのスペースを作成します。 *内部*, *公開* （英語とフランス語のコンテンツを含む） *共通* 以下に示すように、適切なエンティティを管理する場合：

* /content/entities/internal
* /content/entities/public/en
* /content/entities/public/fr
* /content/entities/common

ネイティブクライアントライブラリがスペースのコンテンツのリストをリクエストできるように、サービスエンドポイントがスペースに提供されます。 この「リスト」は、JSON オブジェクトとして返されます。

詳しくは、 **[スペースとエンティティ](/help/mobile/spaces-and-entities.md)** スペースを作成して公開する場合。

>[!NOTE]
>
>多くのアプリでは 1 つのスペースを使用でき、1 つのアプリで多くのスペースを使用できます。

### コンテンツモデル内のフォルダ {#folders-in-content-model}

フォルダーを使用すると、必要に応じてエンティティを整理し、ACL の細かい制御を容易におこなえます。 スペースには、スペースのコンテンツやアセットをさらに整理するのに役立つフォルダーを含めることができます。 ユーザーは、1 つのスペースの下に独自の階層を作成できます。

詳しくは、 **[スペース内のフォルダの操作](/help/mobile/spaces-and-entities.md)** スペース内のフォルダを作成および管理するには
