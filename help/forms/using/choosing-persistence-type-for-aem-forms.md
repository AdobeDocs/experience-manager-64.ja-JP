---
title: AEM Forms のインストールに永続性タイプを選択する
seo-title: Choosing a persistence type for an AEM Forms installation
description: 永続性タイプを選択することをお勧めします。 これにより、効率的で拡張性の高いAEM Forms環境を構築できます。
seo-description: Choose a persistence type wisely. It helps you build an efficient and scale able AEM Forms environment.
uuid: 1c692502-5039-4757-9358-1772772b3904
content-type: reference
products: SG_EXPERIENCEMANAGER/6.4/FORMS
topic-tags: installing
geptopics: SG_AEMFORMS/categories/jee
discoiquuid: a972fb35-38a7-4b83-99bd-6a6dddf8043b
role: Admin
exl-id: ef486673-30fe-410a-83cf-c55be6064ce4
source-git-commit: c5b816d74c6f02f85476d16868844f39b4c47996
workflow-type: tm+mt
source-wordcount: '408'
ht-degree: 17%

---

# AEM Forms のインストールに永続性タイプを選択する {#choosing-a-persistence-type-for-an-aem-forms-installation}

>[!CAUTION]
>
>AEM 6.4 の拡張サポートは終了し、このドキュメントは更新されなくなりました。 詳細は、 [技術サポート期間](https://helpx.adobe.com/jp/support/programs/eol-matrix.html). サポートされているバージョンを見つける [ここ](https://experienceleague.adobe.com/docs/?lang=ja).

永続性タイプを選択することをお勧めします。 これにより、効率的で拡張性の高いAEM Forms環境を構築できます。

永続性は、物理ストレージにコンテンツを保存する方法です。 データの実際のデータ構造と保存メカニズムを定義します。 MicroKernel は、AEM Formsの永続性マネージャーとして機能します。 AEM Formsは、TarMK、MongoMK、RDBMK の永続性 (MicroKernals) をサポートします。 AEM Formsインスタンスの目的とデプロイメントの種類（シングルサーバー、ファーム、クラスター）に応じて、AEM Formsの永続性タイプを選択できます。

>[!NOTE]
>
>LiveCycle ES4 SP1 では TarPM 永続性を使用してコンテンツを格納します。

次の表は、サポートしているすべての永続性タイプと各種のパラメーターを示しています。現在の環境に合わせて永続性タイプを選択する際に、この表を参照してください。

<table> 
 <tbody>
  <tr>
   <th><strong>インストールのタイプ／コスト</strong></th> 
   <th><strong>TarMK</strong></th> 
   <th><strong>MongoMk</strong></th> 
   <th><strong>RDBMK</strong></th> 
  </tr>
  <tr>
   <th><strong>スタンドアロン設定</strong></th> 
   <td>サポート対象<br /> </td> 
   <td>サポート対象</td> 
   <td>サポート対象</td> 
  </tr>
  <tr>
   <th><strong>クラスターの設定</strong></th> 
   <td>サポート対象外</td> 
   <td>サポート対象</td> 
   <td>サポート対象</td> 
  </tr>
  <tr>
   <th><strong>ライセンスコスト</strong></th> 
   <td>AEM に含まれる </td> 
   <td>別途ライセンスが必要です</td> 
   <td>別途ライセンスが必要です</td> 
  </tr>
 </tbody>
</table>

TarMK はパフォーマンスを目的として設計されていますが、MongoMK と RDBMK はスケーラビリティを目的として設計されています。 Adobeでは、オーサーインスタンスとパブリッシュインスタンスの両方について、すべてのAEM Formsデプロイメントシナリオのデフォルトの永続化テクノロジーとして TarMK を強く推奨しています。ただし、の節で説明する使用例は除きます [TarMK での Mongo またはリレーショナルデータベースマイクロカーネルの選択](#p-choosing-mongo-or-a-relational-database-microkernel-over-tarmk-p).

サポートされる Microkernel の一覧については、 [AEM Forms on OSGi の技術要件](/help/sites-deploying/technical-requirements.md) または [JEE 上のAEM Formsでサポートされているプラットフォームの組み合わせ](/help/forms/using/aem-forms-jee-supported-platforms.md) 記事。

## TarMK での Mongo またはリレーショナルデータベースマイクロカーネルの選択 {#choosing-mongo-or-a-relational-database-microkernel-over-tarmk}

スケーラブル（クラスター化）AEM Forms環境は、水平に設定された 2 つ以上のアクティブなオーサーインスタンスのセットです。 すべての同時オーサリングアクティビティをサポートする単一のサーバーが持続可能でなくなった場合は、複数のオーサーインスタンスを実行するよう選択できます。

JEE 環境上のスケーラブルな（クラスター化された）AEM Formsに対しては、MongoMK と RDBMK の永続性タイプのみがサポートされます。 サーバーの数やスケーラブル環境のサイズは、インストールごとに異なります。 考慮事項と例のリストについては、 [推奨されるデプロイメント](/help/sites-deploying/recommended-deploys.md) およびまたは [AEM Formsのアーキテクチャとデプロイメントトポロジ](/help/forms/using/aem-forms-architecture-deployment.md) 記事。 また、RDBMK および TarMK を使用したAEM Formsの容量計画の詳細については、AEM Formsサポートにお問い合わせください。
