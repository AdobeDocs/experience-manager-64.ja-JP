---
title: オーディエンスの管理
seo-title: Managing Audiences
description: オーディエンスコンソールを使用して、Adobe Target アカウント用のオーディエンスを作成、整理および管理したり、ContextHub 用のセグメントを管理したりできます。または ClientContext
seo-description: The Audiences console enables you to create, organize, and manage audiences for your Adobe Target account or manage segments for ContextHub or Client Context
uuid: 7112a192-5f58-47ce-95fa-90638c7cdb18
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.4/SITES
content-type: reference
topic-tags: personalization
discoiquuid: 0e842725-57be-4a16-b972-f5677eaad8cb
exl-id: dcd54a52-f610-4c68-8547-39562c062d84
source-git-commit: 0f4f8c2640629f751337e8611a2c8f32f21bcb6d
workflow-type: tm+mt
source-wordcount: '977'
ht-degree: 48%

---

# オーディエンスの管理 {#managing-audiences}

オーディエンスコンソールを使用して、Adobe Target アカウント用のオーディエンスを作成、整理および管理したり、ContextHub 用のセグメントを管理したりできます。または ClientContext：

* オーディエンスの追加 — Adobe Targetオーディエンスまたは ContextHub セグメント。
* オーディエンスの管理 

オーディエンス *セグメント* ContextHub と ClientContext のは、特定の条件によって定義される訪問者のクラスで、ターゲットアクティビティが表示される対象を決定します。 アクティビティをターゲット設定する場合は、ターゲット設定プロセスで直接オーディエンスを選択するか、オーディエンスコンソールで新しいオーディエンスを作成できます。

オーディエンスコンソールでは、オーディエンスはブランド別に整理されます。

オーディエンスは、ターゲット設定モードで[ターゲットコンテンツのオーサリング](/help/sites-authoring/content-targeting-touch.md)に使用できます。その際、オーディエンスを作成することもできます（ただし、オーディエンスコンソールで Adobe Target オーディエンスを作成する必要があります）。ターゲットモードで作成したオーディエンスは、オーディエンスコンソールに表示されます。

オーディエンスは、定義されているオーディエンスの種類を示すラベルと共に表示されます。

* CH - ContextHub セグメント
* CC - ClientContext セグメント
* AT - Adobe Targetオーディエンス

## オーディエンスコンソールでの ContextHub セグメントの作成 {#creating-a-contexthub-segment-in-the-audiences-console}

ContextHub セグメントは、オーディエンスコンソールまたはターゲット設定プロセスで作成できます。

オーディエンスコンソールで ContextHub セグメントを作成するには：

1. ナビゲーションコンソールで、「**パーソナライズ機能**」をクリックまたはタップします。「**オーディエンス**」をクリックまたはタップします。
1. 「**ContextHub セグメントを作成**」をタップまたはクリックします。

   ![chlimage_1-298](assets/chlimage_1-298.png)

1. **新しい ContextHub セグメント**&#x200B;ダイアログボックスで、タイトルを入力し、ブーストを調整して、「**作成**」をクリックします。新しい ContextHub セグメントがオーディエンスリストに表示されます。

   >[!NOTE]
   >
   >新しく作成したオーディエンスがあるか確認するために降順に並べ替えるには、「**変更済み**」をタップまたはクリックして、変更済みのリストを並べ替えることができます。

ContextHub を使用したセグメントの作成について詳しくは、 [ContextHub でのセグメント化の設定](/help/sites-administering/segmentation.md) ドキュメント。

## オーディエンスコンソールを使用した Adobe Target オーディエンスの作成 {#creating-an-adobe-target-audience-using-the-audience-console}

オーディエンスコンソールを使用して、Adobe TargetオーディエンスをAEMで直接作成できます。

オーディエンスは、誰がターゲットアクティビティに含まれるかを決定するルールによって定義されます。 オーディエンス定義には複数のルールを含めることができ、各ルールには複数のパラメーターを含めることができます。

複数のルールを使用する場合、これらのルールはブール演算子 AND で結合されます。つまり、任意の潜在的なオーディエンスメンバーが、アクティビティに含めるために定義された条件をすべて満たす必要があります。 例えば、AND を使用して OS ルールとブラウザールールを定義した場合、定義された OS と定義されたブラウザーの両方を使用する訪問者のみがアクティビティに含まれます。

>[!NOTE]
>
>**作成**&#x200B;メニューに「**Target オーディエンスを作成**」が表示されない場合は、オーディエンスの作成に必要な権限がありません。オーディエンスを作成するには、**/etc/segmentation** より下の階層における書き込み権限が必要です。content-authors グループには、デフォルトで書き込み権限があります。

Adobe Target オーディエンスを作成するには：

1. ナビゲーションコンソールで、「**パーソナライズ機能**」をクリックまたはタップします。「**オーディエンス**」をクリックまたはタップします。

   ![chlimage_1-299](assets/chlimage_1-299.png)

1. オーディエンスコンソールで、「**作成**」、「**ターゲットオーディエンスを作成**」の順にタップまたはクリックします。

   ![chlimage_1-300](assets/chlimage_1-300.png)

1. **Adobe Target 設定**&#x200B;ダイアログボックスで、Target 設定を選択し、「**OK**」をタップまたはクリックします。
1. 「ルール#1」領域で、属性タイプをタップまたはクリックし、使用可能なフィールドに属性情報を入力します。 終了したら、属性の右側にあるチェックマークを選択して保存します。 詳しくは、 [属性とそのオプション](#attributes-and-their-options) を参照してください。
1. 「**ルールを追加**」をクリックして、別のルールを追加します。必要な数だけルールを入力します。複数のルールを指定した場合は、ルールがブール演算子 AND で結合されます。これは、各ルールの要件をすべて満たすオーディエンスだけが、そのアクティビティの対象になるということです。
1. 「**次へ**」をタップまたはクリックします。
1. オーディエンスの名前を入力し、タップまたはクリックします **保存**.
1. 「**保存**」をタップまたはクリックします。オーディエンスがオーディエンスリストに表示されます。

### 属性とそのオプション {#attributes-and-their-options}

次の各属性に対して、ターゲット設定ルールを作成できます。

| **属性** | **説明** | **詳しくは、** |
|---|---|---|
| **モバイル** | モバイルデバイス、デバイスの種類、デバイスのベンダー、画面の寸法（ピクセル単位）などのパラメーターに基づく Target モバイルデバイス。 | 詳しくは、 [モバイルドキュメント](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/mobile.html?lang=ja) Adobe Targetで |
| **カスタム** | カスタムパラメーターは、mbox パラメーターです。mbox に対して mbox パラメーターを渡した場合、または targetPageParams 関数を使用した場合、それらのパラメーターはここに表示され、オーディエンスで使用できます。 | 詳しくは、 [カスタムパラメータードキュメント](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/custom-parameters.html?lang=ja) Adobe Targetで |
| **OS** | 特定のオペレーティングシステムを使用している訪問者をターゲットに設定することができます。 | Linux、Macintosh または Windows を使用しているユーザーをターゲットにします。 |
| **サイトページ** | 特定のページを閲覧している、または特定の mbox パラメーターを持つ訪問者をターゲットに設定します。 | Adobe Target で[サイトページに関するドキュメント](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/site-pages.html?lang=ja)を参照してください。 |
| **ブラウザー** | ページの訪問時に特定のブラウザーまたは特定のブラウザーオプションを使用しているユーザーをターゲットに設定できます。 | Adobe Target で[ブラウザーオプションに関するドキュメント](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/browser.html?lang=ja)を参照してください。 |
| **訪問者プロファイル** | 特定のプロファイルパラメーターに一致する訪問者をターゲット設定します。 | Adobe Target で[訪問者プロファイルに関するドキュメント](https://experienceleague.adobe.com/docs/target/using/audiences/visitor-profiles/visitor-profile.html?lang=ja)を参照してください。 |
| **トラフィックソース** | サイトに導いた検索エンジンやランディングページに基づいて訪問者をターゲット設定します。 | Adobe Target で[トラフィックソースに関するドキュメント](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/traffic-sources.html?lang=ja)を参照してください。 |

## オーディエンスコンソールでのオーディエンスの変更 {#modifying-an-audience-in-the-audiences-console}

>[!NOTE]
>
>編集中のAEMインスタンスと同じ AEM インスタンスで作成されたAdobe Targetオーディエンスのみを編集できます。 異なるAEM環境で作成された Target オーディエンスは編集できません。

ContextHub オーディエンスまたは ClientContext オーディエンスは、オーディエンスコンソールから編集できます。 Adobe Targetオーディエンスの編集は可能ですが、AEMで作成されたオーディエンスのみを編集できます。

1. ナビゲーションコンソールで、「**パーソナライズ機能**」をクリックまたはタップします。「**オーディエンス**」をクリックまたはタップします。
1. 編集する ContextHub または ClientContext セグメントの横のアイコンをタップまたはクリックし、をタップまたはクリックします **編集**.
1. セグメントエディターで編集を行います。詳しくは、 [ClientContext](/help/sites-administering/campaign-segmentation.md) または [ContextHub](/help/sites-administering/contexthub-config.md) ドキュメント。
