---
title: バージョンのパージ
seo-title: Version Purging
description: この記事では、バージョンのパージに使用できるオプションについて説明します。
seo-description: This article describes the available options for version purging.
uuid: 6140c87e-ae1c-409d-bdbb-71b397f0b738
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.4/SITES
topic-tags: configuring
content-type: reference
discoiquuid: 56f36dcf-8fbd-43f8-bf74-e88d5b686160
feature: Configuring
exl-id: 357d5f23-3e75-44e3-905f-4efe960858bf
source-git-commit: c5b816d74c6f02f85476d16868844f39b4c47996
workflow-type: tm+mt
source-wordcount: '752'
ht-degree: 11%

---

# バージョンのパージ{#version-purging}

>[!CAUTION]
>
>AEM 6.4 の拡張サポートは終了し、このドキュメントは更新されなくなりました。 詳細は、 [技術サポート期間](https://helpx.adobe.com/jp/support/programs/eol-matrix.html). サポートされているバージョンを見つける [ここ](https://experienceleague.adobe.com/docs/?lang=ja).

標準インストールでは、コンテンツの更新後にページをアクティベートすると、AEMはページまたはノードの新しいバージョンを作成します。

>[!NOTE]
>
>コンテンツを変更しない場合は、ページがアクティベートされたが新しいバージョンは作成されないことを示すメッセージが表示されます

リクエストに応じて、 **バージョン管理** サイドキックのタブ これらのバージョンはリポジトリに保存され、必要に応じて復元できます。

これらのバージョンはパージされないので、リポジトリのサイズは時間の経過と共に大きくなるので、管理する必要があります。

AEMには、リポジトリの管理に役立つ様々なメカニズムが付属しています。

* の [バージョンマネージャー](#version-manager)

   これは、新しいバージョンが作成されたときに古いバージョンをパージするように設定できます。

* の [バージョンをパージ](/help/sites-deploying/monitoring-and-maintaining.md#version-purging) ツール

   これは、リポジトリの監視および管理の一環として使用されます。

   これにより、次のパラメーターに従って、ノードの古いバージョンまたはノードの階層を削除するように介入できます。

   * リポジトリに保持するバージョンの最大数。

      この数を超えると、最も古いバージョンが削除されます。

   * リポジトリに保持されるバージョンの最大期間。

      バージョンの期間がこの値を超えると、リポジトリからパージされます。

* [バージョンパージのメンテナンスタスク](/help/sites-administering/operations-dashboard.md#automated-maintenance-tasks)。バージョンのパージメンテナンスタスクをスケジュールして、古いバージョンを自動的に削除できます。これにより、バージョンのパージツールを手動で実行する必要性を最小限に抑えることができます。

>[!CAUTION]
>
>リポジトリサイズを最適化するには、バージョンパージタスクを頻繁に実行する必要があります。 トラフィック量が限られている場合、タスクは営業時間外にスケジュールする必要があります。

## バージョンマネージャー {#version-manager}

パージツールによる明示的なパージに加えて、バージョンマネージャーを設定して、新しいバージョンが作成されたときに古いバージョンをパージすることができます。

バージョンマネージャーを設定するには、次の設定を作成します。

`PID com.day.cq.wcm.core.impl.VersionManagerImpl`

以下のオプションが利用できます。

* `versionmanager.createVersionOnActivation` ( ブール値、デフォルト：true)

   ページがアクティベートされたときにバージョンを作成するかどうか。

   バージョンは、バージョンの作成を抑制するようにレプリケーションエージェントが設定されていない限り作成されます。バージョンマネージャーは、このバージョンを受け入れます

   バージョンは、versionmanager.ivPaths に含まれるパスでアクティベーションが発生した場合にのみ作成されます（以下を参照）。

* `versionmanager.ivPaths` ( 文字列[]、デフォルト：{&quot;/&quot;})

   versionmanager.createVersionOnActivation が true の場合に、アクティベーション時にバージョンが暗黙的に作成されるパス。

* `versionmanager.purgingEnabled` ( ブール値、デフォルト：false)

   新しいバージョンが作成されたときにパージを有効にするかどうか

* `versionmanager.purgePaths` ( 文字列[]、デフォルト：{&quot;/content&quot;})

   新しいバージョンの作成時にバージョンをパージするパス。

* `versionmanager.maxAgeDays` ( 整数、デフォルト：30)

   パージ時に、この値より古いバージョンが削除されます。 この値が 1 未満の場合、バージョンの年齢に基づいてパージは実行されません。

* `versionmanager.maxNumberVersions` （整数、デフォルト 5）

   パージ時に、n 番目に新しいバージョンより古いバージョンが削除されます。 この値が 1 未満の場合、バージョン数に基づいてパージは実行されません

* `versionmanager.minNumberVersions` （整数、デフォルト 0）

   年齢に関係なく保持するバージョンの最小数。 この値を 1 未満の値に設定すると、保持されるバージョンの最小数はありません。

>[!NOTE]
>
>多数のバージョンをリポジトリに保持することはお勧めしません。 そのため、バージョンのパージ操作を設定する際は、パージから多くのバージョンが除外されないように注意してください。除外しないと、リポジトリのサイズが適切に最適化されません。 ビジネス要件が原因で多数のバージョンを保持している場合は、Adobeサポートに連絡して、リポジトリサイズを最適化する別の方法を見つけてください。

### 保持オプションの組み合わせ {#combining-retention-options}

どのバージョンを保持するかを定義するオプション（`maxAgeDays`、`maxNumberVersions`、`minNumberVersions`）は、要件に応じて組み合わせることができます。

例えば、保持するバージョンの最大数と、保持する最も古いバージョンを定義する場合は、次のようになります。

* 設定:

   * `maxNumberVersions` = 7
   * `maxAgeDays` = 30

* 次を使用：

   * 過去 60 日以内に作成された 10 個のバージョン
   * 過去 30 日以内に作成されたバージョンのうち 3 つ

* 次のことを意味します。

   * 最新 3 つのバージョンが保持されます

例えば、保持するバージョンの最大数と最小数、および保持する最も古いバージョンを定義する場合は、次のようになります。

* 設定:

   * `maxNumberVersions` = 3
   * `maxAgeDays` = 30
   * `minNumberVersions` = 3

* 次を使用：

   * 60 日前に作成された 5 つのバージョン

* 次のことを意味します。

   * 3 つのバージョンが保持されます

## バージョンのパージツール {#purge-versions-tool}

この [バージョンをパージ](/help/sites-deploying/monitoring-and-maintaining.md#purgeversionstool) このツールは、リポジトリ内のノードまたはノードの階層のバージョンをパージすることを目的としています。 その主な目的は、古いバージョンのノードを削除して、リポジトリのサイズを小さくすることです。
