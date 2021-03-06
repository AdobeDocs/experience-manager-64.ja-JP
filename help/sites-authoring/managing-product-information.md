---
title: クリエイティブプロジェクトと PIM 統合
seo-title: Creative Project and PIM Integration
description: クリエイティブプロジェクトにより、写真撮影リクエスト、写真のアップロード、写真での共同作業、および承認されたアセットのパッケージ作成を含む、写真撮影ワークフロー全体が合理化されます。
seo-description: Creative Project streamlines the entire photo shoot workflow that including generating a photo shoot request, uploading a photo shoot, collaborating on a photo shoot, and packaging approved assets
uuid: 09f27d36-e725-45cb-88d1-27383aedceed
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.4/SITES
topic-tags: projects
content-type: reference
discoiquuid: 0e5d0a45-c663-4d91-b793-03d39119d103
exl-id: b477d6ab-126a-489a-a13f-2b6f439ab85b
source-git-commit: bd94d3949f0117aa3e1c9f0e84f7293a5d6b03b4
workflow-type: tm+mt
source-wordcount: '2980'
ht-degree: 97%

---

# クリエイティブプロジェクトと PIM 統合{#creative-project-and-pim-integration}

マーケターやクリエイティブ専門家の場合、Adobe Experience Manager（AEM）のクリエイティブプロジェクトツールを使用して、eコマース関連の製品写真および組織内の関連するクリエイティブプロセスを管理できます。

特に、クリエイティブプロジェクトを使用して、写真撮影ワークフローの以下のタスクを合理化できます。

* 写真撮影リクエストの生成
* 撮影した写真のアップロード
* 写真撮影での共同作業
* 承認されたアセットのパッケージ化

>[!NOTE]
>
>ユーザーの役割とワークフローの特定のユーザータイプへの割り当てについては、[プロジェクトユーザーの役割](/help/sites-authoring/projects.md#user-roles-in-a-project)を参照してください。

## 撮影した製品写真ワークフローの詳細  {#exploring-product-photo-shoot-workflows}

クリエイティブプロジェクトでは、多様なプロジェクト要件に応じた多様なプロジェクトテンプレートが用意されています。「**製品撮影プロジェクト**」テンプレートは、すぐに使用できます。 このテンプレートは、製品撮影リクエストを開始し、管理できる写真撮影ワークフローを含みます。適切なレビューおよび承認プロセスを通じて、製品のデジタル画像を取得できる一連のタスクも含まれます。

このテンプレートには、以下のワークフローが含まれます。

* **撮影した製品写真（コマース統合）ワークフロー**：このワークフローでは、製品情報管理（PIM）システムとのコマース統合を利用し、選択した製品（階層）に基づいて撮影リストを自動的に生成します。ワークフローの完了後、製品データをアセットメタデータの一部として表示できます。
* **撮影した製品写真ワークフロー**：このワークフローでは、コマース統合を利用する代わりに、プロジェクトマネージャーが撮影リストを提供しますこれにより、アップロードされた画像をプロジェクトアセットフォルダー内の CSV ファイルにマップします。

>[!NOTE]
>
>撮影した製品写真ワークフローの「撮影リストをアップロード」タスクでアップロードする CSV ファイルのファイル名は shotlist.csv にしてください。

## 製品撮影プロジェクトを作成 {#create-a-product-photo-shoot-project}

1. **プロジェクト**&#x200B;コンソールで「**作成**」をタップまたはクリックし、リストから「**プロジェクトを作成**」を選択します。

   ![chlimage_1-132](assets/chlimage_1-132.png)

1. **プロジェクトを作成**&#x200B;ページで、写真撮影プロジェクトテンプレートを選択し、「**次へ**」をクリックします。

   ![chlimage_1-133](assets/chlimage_1-133.png)

1. タイトル、説明、期限などプロジェクトの詳細を入力します。ユーザーを追加し、様々な役割を割り当てます。また、プロジェクトのサムネイル画像を追加できます。

   ![chlimage_1-134](assets/chlimage_1-134.png)

1. 「**作成**」をタップまたはクリックします。プロジェクトが作成されたことを示す確認メッセージが表示されます。
1. 「**完了**」をクリックして、**プロジェクト**&#x200B;コンソールに戻ります。または、「**開く**」をタップあるいはクリックして、写真撮影プロジェクト内のアセットを表示します。

## 製品撮影プロジェクトのワークの開始 {#starting-work-in-a-product-photo-shoot-project}

写真撮影リクエストを開始するには、プロジェクトをクリックまたはタップし、プロジェクトの詳細ページ内で「**ワークを追加**」をクリックまたはタップして、ワークフローを開始します。

![chlimage_1-135](assets/chlimage_1-135.png)

製品撮影プロジェクトには、以下の既製のワークフローが含まれています。

* 撮影した製品写真（コマース統合）ワークフロー
* 撮影した製品写真ワークフロー

撮影した製品写真撮影（コマース統合）ワークフローは、AEM の製品に画像アセットをマッピングするときに使用します。このワークフローでは、コマース統合を利用して、承認された画像を */etc/commerce* にある既存の製品データにリンクします。

撮影した製品写真撮影（コマース統合）ワークフローには、以下のタスクが含まれます。

* 撮影リストを作成
* 撮影した写真をアップロード
* 撮影した写真をリタッチ
* レビューおよび承認
* 実稼動に移動タスク

AEM で製品情報が利用できない場合は、撮影した製品写真撮影ワークフローを使用して、CSV ファイルでアップロードする詳細に基づいて、製品に画像アセットをマッピングします。CSV ファイルには、製品 ID、カテゴリ、説明など、製品の基本情報を含める必要があります。このワークフローでは、製品の承認されたアセットを取得します。

このワークフローには、以下のタスクが含まれます。

* 撮影リストをアップロード
* 撮影した写真をアップロード
* 撮影した写真をリタッチ
* レビューおよび承認
* 実稼動に移動タスク

ワークフロー設定オプションを使用して、このワークフローをカスタマイズできます。

どちらのワークフローにも、製品とその承認されたアセットをリンクするステップが含まれます。各ワークフローには、以下のステップが含まれます。

* ワークフロー設定：ワークフローをカスタマイズするためのオプションを記述します。
* プロジェクトワークフローの開始：撮影した製品写真ワークフローを開始する方法を説明します。
* ワークフロータスクの詳細：ワークフローで使用可能なタスクの詳細を指定します。

## プロジェクトの進行状況の追跡 {#tracking-project-progress}

プロジェクト内のアクティブなタスクまたは完了したタスクを監視することによって、プロジェクトの進行状況を追跡できます。

以下のものを使用して、プロジェクトの進行状況を監視します。

* **タスクカード**

* **タスクリスト**

タスクカードは、プロジェクト全体の進行状況を表示します。プロジェクトに関連タスクがある場合のみ、プロジェクトの詳細ページにタスクカードが表示されます。タスクカードは、完了したタスク数に基づいて、プロジェクトの現在の完了ステータスを表示します。今後のタスクは含まれません。

タスクカードには以下の詳細が表示されます。

* アクティブなタスクの割合
* 完了したタスクの割合

![chlimage_1-136](assets/chlimage_1-136.png)

タスクリストには、プロジェクトの現在アクティブなワークフロータスクにかかわる詳細情報が表示されます。リストを表示するには、タスクカードをタップまたはクリックします。タスクカードには、タスクの開始日、終了日、割り当て先、優先度、ステータスなどのメタデータも表示されます。

![chlimage_1-137](assets/chlimage_1-137.png)

## ワークフロー設定 {#workflow-configuration}

このタスクでは、役割に基づいてユーザーにワークフローのステップを割り当てます。

**撮影した製品写真**&#x200B;ワークフローを設定するには：

1. **ツール**／**ワークフロー**&#x200B;に移動し、「**モデル**」タイルをタップして、**ワークフローモデル**&#x200B;ページを開きます。
1. **製品写真撮影**&#x200B;ワークフローを選択して、ツールバーの「**編集**」アイコンをタップして、編集モードで開きます。

   ![chlimage_1-138](assets/chlimage_1-138.png)

1. **製品写真撮影ワークフロー**&#x200B;ページで、プロジェクトタスクを開きます。例えば、**撮影リストをアップロード**&#x200B;タスクを開きます。

   ![chlimage_1-139](assets/chlimage_1-139.png)

1. 「**タスク**」タブをクリックして、以下の項目を設定します。

   * タスクの名前
   * タスクを受信するデフォルトのユーザー（役割）
   * ユーザーのタスクリストに表示される、タスクのデフォルトの優先度
   * 担当者がタスクを開いたときに表示されるタスクの説明
   * タスクが開始された時間に基づいて計算されるタスクの期限

1. 「**OK**」をクリックし、設定を保存します。

   同様に、**撮影した製品写真**&#x200B;ワークフローに対しても以下のタスクを設定できます。

   * 撮影した写真をアップロード
   * 撮影した製品写真をリタッチ
   * 撮影した写真のレビュー
   * 実稼動に移動

   同様の手順を実行して、**製品写真撮影（Commerce 統合）ワークフロー**&#x200B;でタスクを設定します。

このセクションでは、製品情報管理とクリエイティブプロジェクトを統合する方法について説明します。

## プロジェクトワークフローの開始 {#starting-a-project-workflow}

1. 製品撮影プロジェクトに移動して、**ワークフロー**&#x200B;カードの&#x200B;**作業の追加**&#x200B;アイコンをタップまたはクリックします。
1. **製品写真撮影（Commerce 統合）**&#x200B;ワークフローカードを選択して、製品写真撮影（Commerce 統合）ワークフローを開始します。製品情報が /etc/commerce の下で利用できない場合は、**撮影した製品写真**&#x200B;ワークフローを選択して、撮影した製品写真ワークフローを開始します。

   ![chlimage_1-140](assets/chlimage_1-140.png)

1. 「**次へ**」をタップまたはクリックして、プロジェクトでワークフローを開始します。
1. 各ワークフローについては、次のページで詳しく説明します。

   ![chlimage_1-141](assets/chlimage_1-141.png)

   「**送信**」をクリックして、写真撮影ワークフローを開始します。写真撮影プロジェクトのプロジェクトの詳細ページが表示されます。

   ![chlimage_1-142](assets/chlimage_1-142.png)

### ワークフロータスクの詳細 {#workflow-tasks-details}

写真撮影ワークフローには、複数のタスクが含まれています。各タスクは、そのタスク用に定義された設定に基づいて、ユーザーグループに割り当てられます。

#### 撮影リストの作成タスク {#create-shot-list-task}

**撮影リストの作成**&#x200B;タスクを使用して、プロジェクト所有者が画像を必要とする製品を選択できます。ユーザーが選択したオプションに基づいて、製品の基本情報を含む CSV ファイルが生成されます。

1. プロジェクトフォルダーで、[タスクカード](#tracking-project-progress)の中の省略記号をタップまたはクリックして、ワークフローの中のタスク項目を表示します。

   ![chlimage_1-143](assets/chlimage_1-143.png)

1. 「**撮影リストを作成**」タスクを選択して、ツールバーの「**開く**」アイコンをタップまたはクリックします。

   ![chlimage_1-144](assets/chlimage_1-144.png)

1. タスク詳細をプレビューしてから、「**撮影リストを作成**」ボタンをタップまたはクリックします。

   ![chlimage_1-145](assets/chlimage_1-145.png)

1. 製品データに画像が関連付けられていない製品を選択します。

   ![chlimage_1-146](assets/chlimage_1-146.png)

1. 「**撮影リストに追加**」アイコンをタップまたはクリックして、これらすべての製品のリストを含む CSV ファイルを作成します。選択された製品で撮影リストが作成されたことを確認するメッセージが表示されます。「**閉じる**」をクリックして、ワークフローを完了します。
1. 撮影リストを作成すると、「**撮影リストを表示**」リンクが表示されます。撮影リストにさらに商品を追加するには、「**撮影リストに追加**」をタップまたはクリックします。この場合、最初に作成された撮影リストにデータが追加されます。

   ![chlimage_1-147](assets/chlimage_1-147.png)

1. 「**撮影リストを表示**」をタップまたはクリックして、新しい撮影リストを表示します。

   ![chlimage_1-148](assets/chlimage_1-148.png)

   既存のデータを編集または新しいデータを追加するには、ツールバーの「**編集**」をタップまたはクリックします。「製品」フィールドと「**説明**」フィールドのみ編集可能です。

   ![chlimage_1-149](assets/chlimage_1-149.png)

   ファイルを更新した後で、ツールバーの「**保存**」をタップまたはクリックしてファイルを保存します。

1. 製品を追加したら、「撮影リストの作成」タスクの詳細ページの「**完了**」アイコンをクリックして、タスクを「完了」としてマークします。オプションでコメントを追加できます。

   タスクが完了すると、プロジェクト内で以下の変更がおこなわれます。

   * 製品階層に対応するアセットが、ワークフローのタイトルと同じ名前を持つフォルダー内に作成されます。
   * 画像がフォトグラファーから提供される前でも、アセットコンソールを使用してアセットのメタデータを編集できるようになります。
   * フォトグラファーから提供された画像を保存する Photo Shoot フォルダーが作成されます。Photo Shoot フォルダーには、撮影リストの製品エントリごとのサブフォルダーが含まれます。

   撮影した製品写真（コマース統合なし）ワークフローの場合は、撮影リストのアップロードが最初のタスクです。「**撮影リストをアップロード**」をタップまたはクリックして、**shotlist.csv** ファイルをアップロードします。CSV ファイルには、製品 ID を含める必要があります。その他のフィールドはオプションです。オプションのフィールドを使用して、アセットを製品にマップできます。

### 撮影リストのアップロードタスク {#upload-shot-list-task}

このタスクは、製品写真撮影ワークフローの一部です。製品情報が AEM で使用できない場合に、このタスクを実行できます。この場合は、画像アセットが必要な製品のリストを CSV ファイルでアップロードします。CSV ファイルの詳細に基づいて、画像アセットを製品にマップします。

前の手順のプロジェクトカードの下の「**撮影リストを表示**」リンクを使用して、サンプルの CSV ファイルをダウンロードします。サンプルファイルをレビューして、CSV ファイルの通常の内容を理解してください。

製品リストまたは CSV ファイルには、**カテゴリ、製品 ID、説明**&#x200B;および&#x200B;**パス**&#x200B;などのフィールドを含めることができます。「**ID**」フィールドは必須で、製品 ID が格納されます。その他のフィールドはオプションです。

製品は、特定のカテゴリに属することができます。製品カテゴリは、CSV ファイルの「**カテゴリ**」列に表示することができます。「**製品**」フィールドには製品名が格納されます。「**説明**」フィールドに、製品の説明またはフォトグラファーに対する指示を入力します。

>[!NOTE]
>
>アップロードする画像の名前は、「**&lt;ProductId>_」**&#x200B;で始める必要があります。製品 ID は、*shotlist.csv* ファイルの「**ID**」フィールドから参照されます。例えば、撮影リストの **ID が 397122** の製品に対しては、**397122_highcontrast.jpg** または **397122_lowlight.png** などの名前のファイルをアップロードできます。

1. プロジェクトフォルダーで、[タスクカード](#tracking-project-progress)の中の省略記号をタップまたはクリックし、ワークフロー内のタスクのリストを表示します。
1. 「**撮影リストをアップロード**」タスクを選択してから、ツールバーの「**開く**」アイコンをタップまたはクリックします。

   ![chlimage_1-150](assets/chlimage_1-150.png)

1. タスク詳細をレビューしてから「**撮影リストをアップロード**」ボタンをタップまたはクリックします。

   ![chlimage_1-151](assets/chlimage_1-151.png)

1. 「**撮影リストをアップロード**」ボタンをタップまたはクリックして、ファイル名が「shotlist.csv」の CSV ファイルをアップロードします。このファイルは、次のタスクで製品データを抽出するためのソースとして使用されます。
1. 適切な形式の製品情報を含む CSV ファイルをアップロードします。CSV ファイルがアップロードされると、カードの下に「 **アップロードされたアセットを表示** 」リンクが表示されます。

   ![chlimage_1-152](assets/chlimage_1-152.png)

   「**完了**」アイコンをクリックして、タスクを完了します。

1. 「**完了**」アイコンをタップまたはクリックして、タスクを完了します。

### 撮影した写真のアップロードタスク {#upload-photo-shoot-task}

編集者の場合は、前のタスクで作成またはアップロードされた **shotlist.csv**&#x200B;ファイルにリストされている製品の写真をアップロードできます。

アップロードする画像の名前は、「**&lt;productId>_」**&#x200B;で始める必要があります。この製品 ID は、**shotlist.csv** ファイルの「**ID**」フィールドから参照されます。例えば、撮影リストに含まれている **ID 397122** の製品については、**397122_highcontrast.jpg** や **397122_lowlight.png** といった名前の画像ファイルをアップロードできます。

画像を直接アップロードすることも、画像を含む ZIP ファイルをアップロードすることもできます。画像はそれぞれの名前に基づいて、「**撮影した写真**」フォルダー内の製品フォルダーに配置されます。

1. プロジェクトフォルダーで[タスクカード](#tracking-project-progress)の中の省略記号をタップまたはクリックして、ワークフローの中のタスク項目を表示します。
1. 「**撮影した写真のアップロード**」タスクを選択し、ツールバーから「**開く**」アイコンをタップまたはクリックします。

   ![chlimage_1-153](assets/chlimage_1-153.png)

1. 「**撮影した写真をアップロード**」をタップまたはクリックし、撮影した写真の画像をアップロードします。
1. ツールバーの「**完了**」アイコンをタップまたはクリックして、タスクを完了します。

### 撮影した写真のリタッチタスク {#retouch-photo-shoot-task}

権限がある場合は、撮影した写真のリタッチタスクを実行して、撮影した写真フォルダーにアップロードされた画像を編集します。

1. プロジェクトフォルダーで[タスクカード](#tracking-project-progress)の中の省略記号をタップまたはクリックして、ワークフローの中のタスク項目を表示します。
1. 「**撮影した写真のリタッチ**」タスクを選択してから、ツールバーの「**開く**」アイコンをタップまたはクリックします。

   ![chlimage_1-154](assets/chlimage_1-154.png)

1. **撮影した写真のリタッチ**&#x200B;ページで「**アップロードされたアセットを表示**」リンクをタップまたはクリックして、アップロードされた画像を参照します。

   ![chlimage_1-155](assets/chlimage_1-155.png)

   必要に応じて、Adobe Creative Cloud アプリケーションを使用して画像を編集します。

   ![chlimage_1-156](assets/chlimage_1-156.png)

1. ツールバーの「**完了**」アイコンをタップまたはクリックして、タスクを完了します。

### レビューおよび承認タスク {#review-and-approve-task}

このタスクで、フォトグラファーがアップロードした写真画像をレビューし、使用が承認されたものとして画像にマークを付けます。

1. プロジェクトフォルダーで[タスクカード](#tracking-project-progress)の中の省略記号をタップまたはクリックして、ワークフローの中のタスク項目を表示します。
1. 「**レビューおよび承認**」タスクを選択してから、ツールバーの「**開く**」アイコンをタップまたはクリックします。

   ![chlimage_1-157](assets/chlimage_1-157.png)

1. **レビューおよび承認**&#x200B;ページで、レビュアーなどの役割にレビュータスクを割り当ててから、「レビュー」をタップまたはクリックして、アップロードされた製品画像のレビューを開始します。

   ![chlimage_1-158](assets/chlimage_1-158.png)

1. 製品画像を選択して、ツールバーの「承認」アイコンをタップまたはクリックして、それに承認済みマークを付けます。

   ![chlimage_1-159](assets/chlimage_1-159.png)

   画像を承認したら、承認済みバナーがその上に表示されます。

   >[!NOTE]
   製品を画像なしのままにすることもできます。後でこのタスクを再訪問し、完了後に「完了」としてマークできます。

1. 「**完了**」をタップまたはクリックします。承認された画像が、作成済みの空のアセットとリンクされます。

アセット UI を使用してプロジェクトアセットに移動し、承認された画像を確認することができます。

次のレベルをタップまたはクリックして、製品データ階層どおりに製品を表示します。

クリエイティブプロジェクトは、承認されたアセットと参照されている製品を関連付けます。アセットのメタデータは、「**製品データ**」タブの「AEMアセットのメタデータ」セクションに表示されるアセットプロパティで、製品の参照と基本情報で更新されます。

>[!NOTE]
撮影した製品写真ワークフロー（コマース統合なし）では、承認された画像は製品と関連付けられていません。

### 実稼動に移動タスク {#move-to-production-task}

このタスクによって、承認されたアセットが実稼動用フォルダーに移動し、利用できるようになります。

1. プロジェクトフォルダーで[タスクカード](#tracking-project-progress)の中の省略記号をタップまたはクリックして、ワークフローの中のタスク項目を表示します。
1. 「**実稼動に移動**」タスクを選択してから、ツールバーから「**開く**」アイコンをタップまたはクリックします。

   ![chlimage_1-160](assets/chlimage_1-160.png)

1. 実稼動用フォルダーに移動する前に、撮影した写真の承認されたアセットを表示するには、**実稼動に移動**&#x200B;タスクページのプロジェクトのサムネイルの下にある「**承認されたアセットを表示**」リンクをクリックします。

   ![chlimage_1-161](assets/chlimage_1-161.png)

1. 実稼動用フォルダーのパスを「**移動先**」フィールドに入力します。

   ![chlimage_1-162](assets/chlimage_1-162.png)

   「**実稼動に移動**」をタップまたはクリックします。確認メッセージを閉じます。アセットが前述のパスに移動し、フォルダー階層に基づいて、各製品の承認されたアセット用のスピンセットが自動的に作成されます。

1. ツールバーの「**完了**」アイコンをタップまたはクリックします。最後のステップが「完了」とマークされると、ワークフローが完了します。

## DAM アセットメタデータの表示 {#viewing-dam-asset-metadata}

アセットを承認すると、そのアセットが対応する製品にリンクされます。承認されたアセットの[プロパティページ](/help/assets/managing-assets-touch-ui.md#editing-properties)には、「**製品データ**」（リンクされた製品の情報）タブが追加されています。このタブには、製品の詳細、SKU 番号およびアセットにリンクしているその他の製品に関連する詳細が表示されます。「**編集**」アイコンをタップまたはクリックして、アセットプロパティを更新します。製品関連情報は、読み取り専用のままです。

表示されるリンクをタップまたはクリックして、アセットが関連付けられている、製品コンソールの中の適切な製品詳細ページに移動します。

## プロジェクト撮影ワークフローのカスタマイズ {#customizing-the-project-photo-shoot-workflows}

要件に基づいて、プロジェクト撮影ワークフローをカスタマイズできます。これは、役割に基づくオプションのタスクであり、プロジェクト内の変数の値を設定するために実行します。後で、この設定値を判断に使用することができます。

1. AEM のロゴをクリックまたはタップし、**ツール**／**ワークフロー**／**モデル**&#x200B;に移動して、ワークフローのモデルページを開きます。
1. **製品写真撮影（Commerce 統合）**&#x200B;ワークフローまたは&#x200B;**製品写真撮影**&#x200B;ワークフローを選択し、ツールバーから「**編集**」をクリックまたはタップして、ワークフローを編集モードで開きます。
1. サイドキックで&#x200B;**プロジェクト**&#x200B;タスクを開き、**役割に基づくプロジェクトタスクを作成**&#x200B;ステップをワークフローにドラッグします。

   ![chlimage_1-163](assets/chlimage_1-163.png)

1. **役割に基づくタスク**&#x200B;ステップを開きます。
1. 「**タスク**」タブで、**タスク**&#x200B;リストに表示されるタスクの名前を指定します。タスクを役割に割り当て、デフォルトの優先度を設定し、説明を入力し、タスクが期限切れになる時間を指定することもできます。

   ![chlimage_1-164](assets/chlimage_1-164.png)

1. 「**ルーティング**」タブで、タスクのアクションを指定します。複数のアクションを追加するには、「項目を追加」リンクをタップまたはクリックします。

   ![chlimage_1-165](assets/chlimage_1-165.png)

1. オプションを追加したら、「**OK**」をクリックして変更をステップに追加します。

   >[!NOTE]
   「**OK**」をタップまたはクリックしても、ワークフローの変更は保存されません。ワークフローの変更を保存するには、「**保存**」をタップまたはクリックします。

1. サイドキックから&#x200B;**ワークフロー**&#x200B;タスクを開き、**移動**&#x200B;タスクを追加します。
1. **移動**&#x200B;タスクを開き、「**プロセス**」タブをクリックします。
1. 「**スクリプト**」ボックスに次のコードを指定します。

```
   function check() {

   if (workflowData.getMetaDataMap().get("lastTaskAction","") == "Reject All") {

   return true

   }

   // set copywriter user in metadata

   var previousId = workflowData.getMetaDataMap().get("lastTaskCompletedBy", "");

   workflowData.getMetaDataMap().put("copywriter", previousId);

   return false;

   }
```

>[!NOTE]
ワークフローステップのスクリプトの詳細については、[OR 分岐用のルールの定義](/help/sites-developing/workflows-models.md)を参照してください。

![chlimage_1-166](assets/chlimage_1-166.png)

1. 「**OK**」をタップまたはクリックします。

1. 「**保存**」をタップまたはクリックしてワークフローを保存します。

   ![chlimage_1-167](assets/chlimage_1-167.png)

1. [実稼動への移動タスク](#move-to-production-task)が完了し、所有者に割り当てられたら、新しいプロジェクト所有者の同意タスクが表示されます。

   所有者の役割を持つユーザーは、タスクを完了し、コメントポップアップのリスト（ワークフローステップ設定で追加されたアクションのリスト）からアクションを選択できます。

   ![chlimage_1-168](assets/chlimage_1-168.png)

   適切なオプションを選択し、「**完了**」をクリックして、ワークフロー内の&#x200B;**移動ステップ**&#x200B;を実行します。

>[!NOTE]
サーバーを起動すると、プロジェクトタスクリストのサーブレットが、`/libs/cq/core/content/projects/tasktypes`で定義される、タスクタイプと URL のマッピングをキャッシュします。その後、通常のオーバーレイを実行し、`/apps/cq/core/content/projects/tasktypes` の下に配置することによって、カスタムタスクタイプを追加できます。
