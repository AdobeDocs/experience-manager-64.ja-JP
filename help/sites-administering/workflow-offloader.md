---
title: アセットのワークフローオフローダー
seo-title: アセットのワークフローオフローダー
description: アセットのワークフローオフローダーについて説明します。
seo-description: アセットのワークフローオフローダーについて説明します。
uuid: d1c93ef9-a0e1-43c7-b591-f59d1ee4f88b
contentOwner: Chiradeep Majumdar
products: SG_EXPERIENCEMANAGER/6.4/SITES
topic-tags: content
content-type: reference
discoiquuid: 91f0fd7d-4b49-4599-8f0e-fc367d51aeba
translation-type: tm+mt
source-git-commit: cdec5b3c57ce1c80c0ed6b5cb7650b52cf9bc340
workflow-type: tm+mt
source-wordcount: '601'
ht-degree: 29%

---


# アセットのワークフローオフローダー{#assets-workflow-offloader}

Assets ワークフローオフローダーを使用すると、Adobe Experience Manager（AEM）Assets の複数のインスタンスを有効にして、プライマリ（リーダー）インスタンスでの処理の負荷を軽減できます。処理の負荷は、リーダーインスタンスとそれに追加する各種オフローダー（ワーカー）インスタンスの間で分散されます。アセットの処理の負荷を分散すると、AEM Assets でのアセット処理の効率と速度が上がります。さらに、特定の MIME タイプのアセットの処理に専用リソースを割り当てやすくなります。例えば、トポロジの特定のノードを InDesign アセットの処理専用として割り当てることができます。

## オフローダートポロジの設定  {#configure-offloader-topology}

Configuration Managerを使用して、リーダーインスタンスのURLと、リーダーインスタンスの接続要求のオフローダーインスタンスのホスト名を追加します。

1. AEMのロゴをタップ/クリックし、**ツール**/**操作**/**Webコンソール**&#x200B;を選択して、Configuration Managerを開きます。
1. Webコンソールから、**Sling**/**Topology Management**&#x200B;を選択します。

   ![chlimage_1-44](assets/chlimage_1-44.png)

1. [トポロジの管理]ページで、[**Discovery.Oakサービスを構成**]リンクをタップまたはクリックします。

   ![chlimage_1-45](assets/chlimage_1-45.png)

1. Discovery Service Configurationページの&#x200B;**Topology Connector URLs**&#x200B;フィールドで、リーダーインスタンスのコネクタURLを指定します。

   ![chlimage_1-46](assets/chlimage_1-46.png)

1. **Topology Connector Whitelist**&#x200B;フィールドに、リーダーインスタンスとの接続を許可するオフローダーインスタンスのIPアドレスまたはホスト名を指定します。 「**Save**」をタップまたはクリックします。

   ![chlimage_1-47](assets/chlimage_1-47.png)

1. リーダーインスタンスに接続されているオフローダーインスタンスを確認するには、**ツール**／**導入**／**トポロジ**&#x200B;で、クラスタービューをタップまたはクリックします。

## オフロードの無効化  {#disable-offloading}

1. AEMロゴをタップ/クリックし、**ツール**/**デプロイメント**/**オフロード**&#x200B;を選択します。 **ブラウザー**&#x200B;のオフロードページには、トピックと、そのトピックを使用できるサーバーインスタンスが表示されます。

   ![chlimage_1-48](assets/chlimage_1-48.png)

1. ユーザーがAEMアセットのアップロードまたは変更を操作するリーダーインスタンスで、*com/adobe/granite/workflow/offloading*&#x200B;トピックを無効にします。

   ![chlimage_1-49](assets/chlimage_1-49.png)

## リーダーインスタンスでのワークフローランチャーの設定 {#configure-workflow-launchers-on-the-leader-instance}

**Dam Update Asset**&#x200B;ワークフローの代わりに、リーダーインスタンスで&#x200B;**DAM Update Asset Offloading**&#x200B;ワークフローを使用するように、ワークフローランチャーを設定します。

1. AEMのロゴをタップ/クリックし、**ツール**/**ワークフロー**/**ランチャー**&#x200B;を選択して、**ワークフローランチャー**&#x200B;コンソールを開きます。

   ![chlimage_1-50](assets/chlimage_1-50.png)

1. **DAM Update Asset**&#x200B;ワークフローを実行する、それぞれ&#x200B;**作成されたイベントタイプ**&#x200B;と&#x200B;**変更されたノード**&#x200B;を持つ2つのランチャー設定を探します。
1. 各設定について、チェックボックスを選択する前に、ツールバーの「**表示のプロパティ**」アイコンをタップまたはクリックして、**ランチャーのプロパティ**&#x200B;ダイアログを表示します。

   ![chlimage_1-51](assets/chlimage_1-51.png)

1. **ワークフロー**&#x200B;リストから、**「DAM Update Asset Offloading**」を選択し、**「保存**」をタップまたはクリックします。

   ![chlimage_1-52](assets/chlimage_1-52.png)

1. AEMのロゴをタップ/クリックし、**ツール**/**ワークフロー**/**モデル**&#x200B;を選択して、**ワークフローモデル**&#x200B;ページを開きます。
1. **DAM Update Asset Offloading**&#x200B;ワークフローを選択し、ツールバーの「**編集**」をタップまたはクリックして、詳細を表示します。

   ![chlimage_1-53](assets/chlimage_1-53.png)

1. **DAMワークフローのオフロード**&#x200B;ステップのコンテキストメニューを表示し、**編集**&#x200B;を選択します。 設定ダイアログの「**汎用引数**」タブで「**ジョブトピック**」フィールドのエントリを確認します。

   ![chlimage_1-54](assets/chlimage_1-54.png)

## オフローダーインスタンスでのワークフローランチャーの無効化{#disable-the-workflow-launchers-on-the-offloader-instances}

リーダーインスタンスで&#x200B;**DAM Update Asset**&#x200B;ワークフローを実行するワークフローランチャーを無効にします。

1. AEMのロゴをタップ/クリックし、**ツール**/**ワークフロー**/**ランチャー**&#x200B;を選択して、**ワークフローランチャー**&#x200B;コンソールを開きます。

   ![chlimage_1-55](assets/chlimage_1-55.png)

1. **DAM Update Asset**&#x200B;ワークフローを実行する、それぞれ&#x200B;**作成されたイベントタイプ**&#x200B;と&#x200B;**変更されたノード**&#x200B;を持つ2つのランチャー設定を探します。
1. 各設定について、チェックボックスを選択する前に、ツールバーの「**表示のプロパティ**」アイコンをタップまたはクリックして、**ランチャーのプロパティ**&#x200B;ダイアログを表示します。

   ![chlimage_1-56](assets/chlimage_1-56.png)

1. 「**アクティブ化**」セクションで、スライダーをドラッグしてワークフローランチャーを無効にし、「**保存**」をタップまたはクリックして無効にします。

   ![chlimage_1-57](assets/chlimage_1-57.png)

1. リーダーインスタンスで画像タイプのアセットをアップロードします。 オフロードされたインスタンスによって、アセットに対して生成され、ポートバックされるサムネールを確認します。

