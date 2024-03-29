---
title: ビジネス・プロセスを達成し、監査を実行し、コンプライアンスを達成し、基本的な健全性を維持するための資産の処理
description: 形式の変換、レンディションの作成、アセットの管理、アセットの検証、ワークフローの実行を行うためのアセット処理です。
contentOwner: AG
feature: Workflow,Renditions
role: User,Admin
exl-id: 4fb3d12c-feac-45b9-8d09-3b6995591b3d
source-git-commit: c5b816d74c6f02f85476d16868844f39b4c47996
workflow-type: tm+mt
source-wordcount: '1068'
ht-degree: 70%

---

# デジタルアセットの処理 {#process-assets}

>[!CAUTION]
>
>AEM 6.4 の拡張サポートは終了し、このドキュメントは更新されなくなりました。 詳細は、 [技術サポート期間](https://helpx.adobe.com/jp/support/programs/eol-matrix.html). サポートされているバージョンを見つける [ここ](https://experienceleague.adobe.com/docs/?lang=ja).

[!DNL Adobe Experience Manager Assets] では、様々な方法でデジタルアセットを操作し、堅牢なアセット処理を行うことができます。使用可能な処理方法を使用したり、メソッドを拡張して、デジタルアセットの使用、監査とコンプライアンス、検出と配布、基本的なサニティ、および基本的なサニティを使用して、エンドツーエンドのビジネスプロセスを確実に完了させたりできます。 必要なスケールとカスタマイズを達成しながら、これらすべてを実行できます。

## ワークフローについて {#understand-workflows}

アセットを処理する際に、[!DNL Experience Manager] はワークフローを使用します。ワークフローは、ビジネスロジックやアクティビティを自動化するのに役立ちます。特定のタスクを実行するための詳細な手順はデフォルトで提供されており、開発者は独自のカスタム手順を作成できます。これらの手順を論理的な順序で組み合わせて、ワークフローを作成できます。例えば、画像に埋め込まれたメタデータ、アップロード先のフォルダー、画像の解像度などの特定の条件に基づいて、アップロードされた画像に透かしを自動的に適用することができます。 別の例として、画像にこのような透かしを付けるように設定され、メタデータの追加、レンディションの作成、アセット検出用のインテリジェントタグの追加、データストアへの公開、ユーザーアクセス権の設定など、複数のアセット管理ニーズに同時に対処するワークフローがあります。

## Experience Managerで使用可能なデフォルトのワークフロー {#default-workflows}

デフォルトでは、アップロードされたすべてのアセットは、[!UICONTROL DAM アセットの更新]ワークフローを使用して処理されます。ワークフローは、アップロードされたアセットごとに実行され、レンディションの生成、メタデータの書き戻し、ページの抽出、メディアの抽出、トランスコードなど、基本的なアセット管理タスクを実行します。

デフォルトで使用可能な様々なワークフローモデルを確認するには、[!DNL Experience Manager] で[!UICONTROL ツール／ワークフロー／モデル]の順にクリックして内容を参照してください。

![デフォルトのワークフローの一例](assets/aem-default-workflows.png)

*図：デフォルトのワークフローの一部は、 [!DNL Experience Manager].*

## アセットへのワークフローの適用 {#applying-workflows-to-assets}

ワークフローをデジタルアセットに適用する方法は、web サイトページに適用する場合と同様です。ワークフローの作成と使用について詳しくは、[ワークフローの開始](/help/sites-authoring/workflows-participating.md)を参照してください。

デジタルアセットのワークフローを使用して、アセットをアクティベートするか、透かしを作成します。 アセットのワークフローの多くは、自動的にオンになります。 例えば、画像の編集後にレンディションを自動的に作成するワークフローは、自動的にオンになります。

>[!NOTE]
>
>クラシック UI で使用可能なワークフローが、タッチ操作対応 UI で使用できない場合（例： ） [!UICONTROL 有効化のリクエスト] および [!UICONTROL 無効化のリクエスト]を参照してください。 [ワークフローモデルを作成](/help/sites-developing/workflows-models.md#make-workflow-models-available-in-touchui).

## ワークフローの適用先 [!DNL Experience Manager] アセット {#apply-a-workflow-to-an-aem-asset}

<!-- 
TBD: Add animated GIF for these steps instead of all these screenshots.
-->

ワークフローをアセットに適用するには、次の手順に従います。

1. ワークフローを開始するアセットの場所に移動し、アセットをクリックしてアセットのページを開きます。

1. ワークフローを開始するアセットの場所に移動し、アセットをクリックしてアセットのページを開きます。メニューから「**[!UICONTROL タイムライン]**」を選択し、タイムラインを表示します。

   ![timeline-2](assets/timeline-2.png)

1. 下部にある「**[!UICONTROL アクション]**」をクリックして、アセットで使用可能なアクションのリストを開きます。

1. リストの「**[!UICONTROL ワークフローを開始]**」をクリックします。

1. 内 **[!UICONTROL ワークフローを開始]** ダイアログボックスで、リストからワークフローモデルを選択します。

   ![chlimage_1-50](assets/chlimage_1-50.png)

1. （オプション）ワークフローインスタンスを参照するために使用するワークフローのタイトルを指定します。

   ![chlimage_1-51](assets/chlimage_1-51.png)

1. クリック **[!UICONTROL 開始]**&#x200B;を選択し、「 **[!UICONTROL 続行]** をクリックして確定します。 ワークフローの各ステップは、タイムラインにイベントとして表示されます。

   ![chlimage_1-52](assets/chlimage_1-52.png)

## 複数のアセットへのワークフローの適用 {#applying-a-workflow-to-multiple-assets}

1. アセットコンソールから、ワークフローを開始するアセットの場所へ移動して、アセットを選択します。メニューから「**[!UICONTROL タイムライン]**」を選択し、タイムラインを表示します。

   ![chlimage_1-136](assets/chlimage_1-136.png)

1. 下部にある「**[!UICONTROL アクション]**」をクリックします。

1. 「**[!UICONTROL ワークフローを開始]**」をクリックします。**[!UICONTROL ワークフローを開始]**&#x200B;ダイアログで、リストからワークフローモデルを選択します。

   ![chlimage_1-138](assets/chlimage_1-138.png)

1. （オプション）ワークフローインスタンスを参照するために使用するワークフローのタイトルを指定します。

1. ダイアログで「**[!UICONTROL 開始]**」をクリックし、次に「**[!UICONTROL 確認]**」をクリックします。選択したすべてのアセットでワークフローが実行されます。

## 複数フォルダーへのワークフローの適用 {#applying-a-workflow-to-multiple-folders}

ワークフローを複数のフォルダーに適用する手順は、複数のアセットに適用する手順と似ています。アセットコンソールでフォルダーを選択し、手順 2 ～ 7 を実行します [複数のアセットへのワークフローの適用](assets-workflow.md#applying-a-workflow-to-multiple-assets).

## コレクションへのワークフローの適用 {#applying-a-workflow-to-a-collection}

コレクションへのワークフローの適用について詳しくは、 [コレクションに対するワークフローの適用](managing-collections-touch-ui.md#running-a-workflow-on-a-collection).

## アセットを条件付きで処理するワークフローの自動開始 {#auto-execute-workflow-on-some-assets}

管理者は、事前に定義された条件に基づいてアセットを自動的に実行および処理するようにワークフローを設定できます。この機能は、事業部門のユーザーやマーケティング担当者が特定のフォルダーにカスタムワークフローを作成する場合などに役立ちます。具体的には、代理店の撮影したすべてのアセットに透かしを入れたり、フリーランサーがアップロードしたすべてのアセットに特定のレンディションを作成するよう処理したりできます。

ワークフローモデルの場合、ユーザーはワークフローを実行するワークフローランチャーを作成できます。ワークフローランチャーは、コンテンツリポジトリの変更を監視し、事前に定義された条件が満たされた場合にワークフローを実行します。管理者は、マーケティング担当者に対してワークフローの作成とランチャーの設定のためのアクセス権を提供できます。ユーザーはデフォルトの [!UICONTROL DAM アセットの更新]ワークフローを変更して、特定のアセットの処理に必要な追加の手順を追加できます。ワークフローは、新しくアップロードされたすべてのアセットで実行されます。特定のアセットに対する追加の手順の実行を制限するには、次のいずれかの方法を使用します。

* [!UICONTROL DAM アセットの更新]ワークフローのコピーを作成し、特定のフォルダー階層で実行するように変更します。この方法は、数個のフォルダーがある場合に役立ちます。
* 追加の処理手順は、必要な数のフォルダーに条件付きで適用できるように [OR 分岐](/help/sites-developing/workflows-step-ref.md#or-split)を使用して追加できます。

## ベストプラクティスと制限事項 {#best-practices-limitations-tips}

* ワークフローを設計する際には、あらゆる種類のレンディションに対するニーズを考慮します。レンディションが今後必要になることが予測されない場合は、ワークフローからレンディションの作成ステップを削除します。以後、レンディションは一括削除できません。[!DNL Experience Manager] を長時間使用した後、不要なレンディションで大量のストレージ領域が占有される場合があります。個々のアセットについては、ユーザーインターフェイスからレンディションを手動で削除できます。複数のアセットについては、特定のレンディションを削除するように [!DNL Experience Manager] をカスタマイズすることもできますし、アセットを削除して再びアップロードすることもできます。
* デフォルトでは、[!UICONTROL DAM アセットの更新]ワークフローに、サムネールと web レンディションを作成する手順が含まれています。ワークフローからデフォルトのレンディションが削除されると、[!DNL Assets] のユーザーインターフェイスが適切にレンダリングされません。

>[!MORELIKETHIS]
>
>* [ワークフローへの適用と参加](/help/sites-authoring/workflows.md)
>* [ワークフローモデルの作成とワークフロー機能の拡張](/help/sites-developing/workflows.md)
>* [ワークフローを実行するメソッド](/help/sites-administering/workflows-starting.md)
>* [ワークフローのベストプラクティス](/help/sites-developing/workflows-best-practices.md)

