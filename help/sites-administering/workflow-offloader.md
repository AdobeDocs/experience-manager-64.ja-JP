---
title: Assets Workflow Offloader
seo-title: Assets Workflow Offloader
description: Assets Workflow Offloader について説明します。
seo-description: Learn about the Assets Workflow Offloader.
uuid: d1c93ef9-a0e1-43c7-b591-f59d1ee4f88b
contentOwner: Chiradeep Majumdar
products: SG_EXPERIENCEMANAGER/6.4/SITES
topic-tags: content
content-type: reference
discoiquuid: 91f0fd7d-4b49-4599-8f0e-fc367d51aeba
exl-id: 2ca8e786-042b-44f6-ac60-834eca64f79f
source-git-commit: c5b816d74c6f02f85476d16868844f39b4c47996
workflow-type: tm+mt
source-wordcount: '628'
ht-degree: 3%

---

# Assets Workflow Offloader{#assets-workflow-offloader}

>[!CAUTION]
>
>AEM 6.4 の拡張サポートは終了し、このドキュメントは更新されなくなりました。 詳細は、 [技術サポート期間](https://helpx.adobe.com/jp/support/programs/eol-matrix.html). サポートされているバージョンを見つける [ここ](https://experienceleague.adobe.com/docs/?lang=ja).

Assets ワークフローオフローダーを使用すると、Adobe Experience Manager(AEM)Assets の複数のインスタンスを有効にして、プライマリ（リーダー）インスタンスの処理負荷を軽減できます。 処理負荷は、リーダーインスタンスと、それに追加する様々なオフローダー（ワーカー）インスタンスに分散されます。 アセットの処理負荷を分散すると、AEM Assetsでアセットを処理する際の効率と速度が向上します。 また、特定の MIME タイプのアセットを処理するための専用リソースを割り当てるのに役立ちます。 例えば、トポロジ内の特定のノードを割り当てて、InDesignのアセットのみを処理できます。

## オフローダトポロジの設定 {#configure-offloader-topology}

Configuration Manager を使用して、リーダーインスタンスの URL と、リーダーインスタンス上の接続要求のオフローダーインスタンスのホスト名を追加します。

1. AEMロゴをタップまたはクリックし、「 」を選択します。 **ツール** > **運用** > **Web コンソール** をクリックして Configuration Manager を開きます。
1. Web コンソールで、 **Sling** >  **トポロジ管理**.

   ![chlimage_1-44](assets/chlimage_1-44.png)

1. トポロジ管理ページで、 **Discovery.Oak サービスを設定** リンク。

   ![chlimage_1-45](assets/chlimage_1-45.png)

1. Discovery Service の設定ページで、でリーダーインスタンスのコネクタ URL を指定します **トポロジコネクタ URL** フィールドに入力します。

   ![chlimage_1-46](assets/chlimage_1-46.png)

1. 内 **Topology Connector のホワイトリスト** フィールドで、リーダーインスタンスとの接続が許可されるオフローダインスタンスの IP アドレスまたはホスト名を指定します。 「**保存**」をタップまたはクリックします。

   ![chlimage_1-47](assets/chlimage_1-47.png)

1. リーダーインスタンスに接続されているオフローダーインスタンスを確認するには、に移動します。 **ツール** > **導入** > **トポロジ** 「クラスター」表示をタップまたはクリックします。

## オフロードを無効にする {#disable-offloading}

1. AEMロゴをタップまたはクリックし、「 」を選択します。 **ツール** > **導入** > **オフロード**. この **ブラウザーのオフロード** このページには、トピックと、トピックを使用できるサーバーインスタンスが表示されます。

   ![chlimage_1-48](assets/chlimage_1-48.png)

1. を無効にします。 *com/adobe/granite/workflow/offloading* AEMアセットをアップロードまたは変更する際にユーザーがやり取りするリーダーインスタンスに関するトピック。

   ![chlimage_1-49](assets/chlimage_1-49.png)

## リーダーインスタンスでのワークフローランチャーの設定 {#configure-workflow-launchers-on-the-leader-instance}

以下を使用するようにワークフローランチャーを設定する **DAM アセットの更新のオフロード** の代わりにリーダーインスタンス上のワークフロー **DAM アセットの更新** ワークフロー。

1. AEMのロゴをタップまたはクリックし、「 」を選択します。 **ツール** > **ワークフロー** > **ランチャー** 開く **ワークフローランチャー** コンソール。

   ![chlimage_1-50](assets/chlimage_1-50.png)

1. イベントタイプを持つ 2 つのランチャー設定を見つけます。 **作成されたノード** および **変更されたノード** それぞれ、 **DAM アセットの更新** ワークフロー。
1. 各設定で、設定の前のチェックボックスを選択し、 **プロパティを表示** ツールバーのアイコン **ランチャーのプロパティ** ダイアログ。

   ![chlimage_1-51](assets/chlimage_1-51.png)

1. 次の **ワークフロー** リスト、選択 **DAM アセットの更新のオフロード** タップまたはクリック **保存**.

   ![chlimage_1-52](assets/chlimage_1-52.png)

1. AEMのロゴをタップまたはクリックし、「 」を選択します。 **ツール** > **ワークフロー** > **モデル** 開く **ワークフローモデル** ページ。
1. を選択します。 **DAM アセットの更新のオフロード** ワークフローを開き、タップまたはクリックします。 **編集** ツールバーから詳細を表示します。

   ![chlimage_1-53](assets/chlimage_1-53.png)

1. のコンテキストメニューを表示します。 **DAM ワークフローのオフロード** ステップと選択 **編集**. 「 **ジョブトピック** フィールド **汎用引数** 設定ダイアログの「 」タブ

   ![chlimage_1-54](assets/chlimage_1-54.png)

## オフローダーインスタンスのワークフローランチャーを無効にする {#disable-the-workflow-launchers-on-the-offloader-instances}

実行するワークフローランチャーを無効にする **DAM アセットの更新** リーダーインスタンス上のワークフロー

1. AEMのロゴをタップまたはクリックし、「 」を選択します。 **ツール** > **ワークフロー** > **ランチャー** 開く **ワークフローランチャー** コンソール。

   ![chlimage_1-55](assets/chlimage_1-55.png)

1. イベントタイプを持つ 2 つのランチャー設定を見つけます。 **作成されたノード** および **変更されたノード** それぞれ、 **DAM アセットの更新** ワークフロー。
1. 各設定で、設定の前のチェックボックスを選択し、 **プロパティを表示** ツールバーのアイコン **ランチャーのプロパティ** ダイアログ。

   ![chlimage_1-56](assets/chlimage_1-56.png)

1. 「**アクティブ化**」セクションで、スライダーをドラッグしてワークフローランチャーを無効にし、タップまたはクリックします **保存** を無効にします。

   ![chlimage_1-57](assets/chlimage_1-57.png)

1. 画像タイプのアセットがあれば、リーダーインスタンスにアップロードします。 オフロードされたインスタンスによってアセットに対して生成および移植されたサムネールを確認します。
