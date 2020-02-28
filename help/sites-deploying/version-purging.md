---
title: バージョンのパージ
seo-title: バージョンのパージ
description: この記事では、バージョンのパージで使用できるオプションについて説明します。
seo-description: この記事では、バージョンのパージで使用できるオプションについて説明します。
uuid: 6140c87e-ae1c-409d-bdbb-71b397f0b738
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.4/SITES
topic-tags: configuring
content-type: reference
discoiquuid: 56f36dcf-8fbd-43f8-bf74-e88d5b686160
translation-type: tm+mt
source-git-commit: 510b6765e11a5b3238407322d847745f09183d63

---


# バージョンのパージ{#version-purging}

標準インストールの場合、AEM は、コンテンツの更新後のページのアクティベート時に、ページまたはノードの新しいバージョンを作成します。

>[!NOTE]
>
>コンテンツが変更されない場合は、ページがアクティベートされ、新しいバージョンが作成されないことを示すメッセージが表示されます。

サイドキックの「**バージョン管理**」タブを使用すると、要求で追加のバージョンを作成できます。これらのバージョンはリポジトリに格納され、必要に応じて復元できます。

格納されたバージョンはパージされないので、時間の経過と共にリポジトリのサイズが大きくなっていきます。そこで、管理が必要になります。

AEM には、リポジトリの管理に役立つ様々なメカニズムが備わっています。

* バージ [ョン管理](#version-manager)

   新しいバージョンを作成する際に古いバージョンを削除するように設定できます。

* [バージ [ョンの削除](/help/sites-deploying/monitoring-and-maintaining.md#version-purging) ]ツール

   これは、リポジトリの監視と管理の一部として使用されます。

   このツールを使用すると、次のパラメーターに従って、ノードまたはノードの階層の古いバージョンを削除するためにユーザーが介入できます。

   * リポジトリに保持するバージョンの最大数

      この数値を超えると、最も古いバージョンが削除されます。

   * リポジトリに保持するバージョンの期間の最大値

      バージョンの期間がこの値を超えると、リポジトリからパージされます。

* the [Version Purge maintenance task](/help/sites-administering/operations-dashboard.md#automated-maintenance-tasks). バージョンのパージメンテナンスタスクをスケジュールして、古いバージョンを自動的に削除できます。その結果、バージョンの削除ツールを手動で使用する必要が最小限に抑えられます。

>[!CAUTION]
>
>リポジトリサイズを最適化するためには、バージョン削除タスクを頻繁に実行する必要があります。トラフィックが限られている場合は、営業時間外にタスクをスケジュールする必要があります。

## バージョンマネージャー {#version-manager}

パージツールを使用した明示的なパージに加えて、バージョンマネージャーは、新しいバージョンが作成されると古いバージョンをパージするように設定できます。

バージョンマネージャーを設定するには、次の設定を作成します。

`PID com.day.cq.wcm.core.impl.VersionManagerImpl`

以下のオプションが利用できます。

* `versionmanager.createVersionOnActivation` (ブール値、デフォルト：true)

   ページがアクティブ化されたときにバージョンを作成するかどうか。

   バージョンの作成が許可されない限り、レプリケーションエージェントがバージョンの作成を禁止するように設定されていない場合は、バージョンが作成されます。バージョンマネージャーはこの設定を行います

   バージョンは、versionmanager.ivPathsに含まれるパスでアクティベートが発生した場合にのみ作成されます（以下を参照）。

* `versionmanager.ivPaths` (String[], default:{&quot;/&quot;})

   versionmanager.createVersionOnActivationがtrueの場合に、アクティベーション時にバージョンが暗黙的に作成されるパス。

* `versionmanager.purgingEnabled` (ブール値、デフォルト：false)

   新しいバージョンが作成された場合に削除を有効にするかどうか

* `versionmanager.purgePaths` (String[], default:{&quot;/content&quot;})

   新しいバージョンが作成されたときにバージョンを削除するパス。

* `versionmanager.maxAgeDays` (int、デフォルト：30)

   削除時に、この値より古いバージョンは削除されます。 この値が1未満の場合、バージョンの経過時間に基づいて削除は実行されません

* `versionmanager.maxNumberVersions` （int、デフォルト5）

   削除すると、n番目に新しいバージョンより古いバージョンが削除されます。 この値が1未満の場合、バージョン数に基づいて削除は実行されません

* `versionmanager.minNumberVersions` （int、デフォルト0）

   年齢に関係なく保持するバージョンの最小数。 この値を 1 未満に設定すると、保持するバージョン数の最小数は設定されません。

>[!NOTE]
>
>リポジトリに多数のバージョンを保存することはお勧めできません。そのため、バージョンパージ操作を設定するときは、パージから多くのバージョンを除外しすぎないでください。そうしないと、リポジトリサイズが適切に最適化されません。ビジネス要件が原因で多数のバージョンを維持する場合は、アドビサポートに連絡して、リポジトリサイズを最適化する別の方法を探してください。

### 保持オプションの組み合わせ {#combining-retention-options}

The options defining how which versions should be retained ( `maxAgeDays`, `maxNumberVersions`, `minNumberVersions`), can be combined depending on your requirements.

保持するバージョン数の最大数と、保持する最も古いバージョンを組み合わせて定義する場合の例：

* 次のように設定し、

   * `maxNumberVersions` = 7
   * `maxAgeDays` = 30

* 次の状況になった場合、

   * 過去 60 日以内に 10 個のバージョンが作成されました。
   * そのうちの 3 個が過去 30 日以内に作成されました。

* 結果は次のようになります。

   * 最新の 3 個のバージョンが保持されます。

保持するバージョン数の最大数と最小数、および保持する最も古いバージョンを組み合わせて定義する場合の例：

* 次のように設定し、

   * `maxNumberVersions` = 3
   * `maxAgeDays` = 30
   * `minNumberVersions` = 3

* 次の状況になった場合、

   * 60 日前に 5 個のバージョンが作成されました。

* 結果は次のようになります。

   * 3 個のバージョンが保持されます。

## バージョンのパージツール {#purge-versions-tool}

[バージョンのパージ](/help/sites-deploying/monitoring-and-maintaining.md#purgeversionstool)ツールは、リポジトリ内のノードまたはノードの階層のバージョンをパージします。このツールの主な目的は、古いバージョンのノードを削除して、リポジトリのサイズを削減することです。
