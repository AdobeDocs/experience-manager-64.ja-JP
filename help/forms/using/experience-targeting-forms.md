---
title: AEM Forms でターゲット設定されたエクスペリエンスを作成する
seo-title: Create targeted experiences in AEM Forms
description: 'AEM Forms の Target を使用して、対象となる顧客向けにカスタマイズされたエクスペリエンスを作成します。 '
seo-description: Use Target in AEM Forms to create customized experiences for targeted customers.
uuid: 174b6054-8fe3-4ab2-8afd-435e5dff9044
content-type: reference
products: SG_EXPERIENCEMANAGER/6.4/FORMS
topic-tags: integrations
discoiquuid: 6cf54a08-d429-4a58-8429-a1cb784448d1
exl-id: 5a10ffea-2c69-4902-9754-399bd2e125f1
source-git-commit: bd94d3949f0117aa3e1c9f0e84f7293a5d6b03b4
workflow-type: tm+mt
source-wordcount: '838'
ht-degree: 29%

---

# AEM Forms でターゲット設定されたエクスペリエンスを作成する {#create-targeted-experiences-in-aem-forms}

## Adobe TargetとAEM Formsの統合 {#integrate-adobe-target-with-aem-forms}

Adobe Target は AEM と統合されて、対象オーディエンスに向けてカスタマイズされたエクスペリエンスを作成することが可能になりました。Adobe Target では、対象ユーザーに向けて A/B テストを作成し、ユーザーの反応を評価し、カスタマイズされた Web コンテンツを生成します。Adobe TargetをAEM Formsと統合して、アダプティブフォームやインタラクティブ通信の画像コンポーネントをターゲットに設定することができます。

AEMでAdobe Targetを設定し、アダプティブフォームやインタラクティブ通信で使用する場合は、 [AEMでの Target 設定の作成](/help/sites-administering/target.md) および [フレームワークを追加](/help/sites-administering/target.md).

>[!NOTE]
>
>ターゲティングは、アダプティブフォームまたはインタラクティブ通信がホスト名または IP アドレスを使用してレンダリングされる場合に機能します。 アダプティブフォームまたはインタラクティブ通信が localhost を使用してレンダリングされると、失敗します。

## Target アクティビティを作成する {#creating-a-target-activity}

1. タップ **Adobe Experience Manager /パーソナライズ機能/アクティビティ**.

   `https://<hostname>:<port>/libs/cq/personalization/touch-ui/content/v2/activities.html`

1. アクティビティページで、をタップします。 **作成/ブランドを作成**.
1. テンプレートを選択し、プロパティを入力します。

   テンプレートを選択して、 **次へ** 「プロパティ」セクションにブランドのタイトルを入力し、をタップします。 **を作成します。**
ブランドがアクティビティページに表示されます。

1. アクティビティページのブランドをタップします。
1. ブランドのマスター領域で、をタップします。 **作成** > **アクティビティを作成**.

   アクティビティを作成したら、その詳細、対象、および設定を指定します。

   詳細セクションには、名前、対象のエンジン、および目的が含まれます。対象のエンジンとして Adobe Target を選択した場合、Target のクラウド設定オプションが有効になります。Target クラウド設定を選択し、「アクティビティタイプ」を選択し、アクティビティの目的を指定して、をタップします。 **次へ**. インタラクティブ通信は、エクスペリエンスのターゲット設定アクティビティタイプのみをサポートします。

   Target セクションでは、オーディエンスのエクスペリエンスを追加し、名前を付けることができます。クリック **エクスペリエンスを追加** 有効にする **オーディエンスを選択** および **名前エクスペリエンス** オプション。 タップ **オーディエンスを選択** をクリックして、オーディエンスとそのソースのリストを表示します。 オーディエンス名のリストからオーディエンスを選択します。タップ **エクスペリエンスを追加** エクスペリエンスの名前を設定するには、 **次へ**.

   「目標と設定」セクションでは、アクティビティのスケジュールと優先度の設定ができます。アクティビティの開始日、終了日、優先度、目標指標、追加の指標を設定して、をタップします。 **保存**.

   アクティビティが、ブランドページのリストに表示されました。

   >[!NOTE]
   >
   >「アクティビティは保存されましたが、Target に同期されませんでした。 理由：次のエクスペリエンスには、アクティビティの保存時に「オファーがありません」と表示される場合は、

1. ターゲットを有効にするには、.jsp ファイルを編集して、アダプティブフォームテンプレートで使用するクライアントライブラリを含めます。

   例えば、標準実装では、「 **ツール** >  **CRXDE Lite**.

   CRXDE Liteのアドレスバーに/libs/fd/af/components/page/base/head.jspと入力して、head.jsp ファイルを編集します。

   この実装では simpleEnrollment テンプレートを使用します。 この実装では、head.jsp ファイルを変更して、次のクライアントライブラリを含めます。

   `<cq:include script="/libs/cq/cloudserviceconfigs/components/servicelibs/servicelibs.jsp"/>`

   `<cq:include path="clientcontext_optimized" resourceType="/libs/cq/personalization/components/clientcontext_optimized"/>`

   `<cq:include path="config" resourceType="cq/personalization/components/clientcontext_optimized/config"/>`

1. アダプティブフォームのターゲットフレームワークを有効にするには、フォームまたはインタラクティブ通信に移動し、編集モードで開きます。

   フォームまたはインタラクティブ通信を編集モードで開くには、 **選択** 次に、 **開く**.

   または、フォームまたはインタラクティブ通信のアイコンにポインタを移動したときに、選択せずに 4 つのボタンが表示されます。 次をタップします。 **編集** ボタンが表示され、フォームが編集モードで開きます。

1. ページツールバーで、 **ページ情報** ![theme-options](assets/theme-options.png) > **プロパティを開く**.
1. 「一般」タブで、 **Adobe Target** フィールドに入力します。 「**保存して閉じる**」をタップします。

## 作成したアクティビティをアダプティブフォームの画像またはインタラクティブ通信の画像に適用する {#applying-created-activity-to-an-adaptive-form-image-or-an-interactive-communication-image}

1. アダプティブフォームとインタラクティブ通信を開いて編集します。 インタラクティブ通信を開く場合は、Web チャネルを開きます。

1. インタラクティブ通信またはアダプティブフォームのオーサリングモードで、ターゲットとする画像を追加します。

   >[!NOTE]
   >
   >AEM Formsは、画像コンポーネントのターゲティングのみをサポートしています。 画像コンポーネントをホストするパネルに他のコンポーネントが含まれていないこと、およびパネルの列数が 1 に設定されていることを確認します。

1. 切り替え元 **編集** から **ターゲット設定** モード。 モードを切り替えるオプションは、右上隅付近にあります。
1. を選択します。 **ブランド**&#x200B;を選択します。 **アクティビティ**&#x200B;をタップし、 **ターゲット設定を開始**. この **オーディエンス** メニューがエディターの右側に表示されます。

   ![ターゲティングメニュー](assets/targeting-menu.png)

1. オーディエンスを **オーディエンス** メニューを開き、ターゲットにする画像をタップします。 メニューが表示されます。 メニューで、 **ターゲット**. 画像をタップし、 **設定**. プロパティウィンドウで、選択したオーディエンスに対して表示する画像を選択します。 すべてのオーディエンスに対して手順を繰り返します。 エクスペリエンスのターゲット設定は、インタラクティブ通信またはアダプティブフォーム内の画像に対して有効になります。

## 作成したアクティビティと Target サーバーとの同期を確認する {#check-if-the-created-activity-syncs-with-the-target-server}

ターゲット設定に使用したアクティビティは、Target サーバーと同期します。アクティビティが Target サーバーと同期しているか確認するには、ブランドページでアクティビティのステータスを確認します。

アクティビティのステータスが同期していることを確認してください。

## Target の動作を検証する {#validate-target-behavior}

Target の動作は次のように検証します。

* でターゲティングを使用 `wcmmode preview` オーサーモードで
* でターゲティングを使用 `wcmmode preview` および `wcmmode disabled` パブリッシュモードで

## 画像コンポーネントのターゲット設定を監視する {#monitor-targeting-for-the-image-component}

フォームの画像コンポーネントのターゲット設定を監視するには、画像、アクティビティ、アダプティブフォームを発行します。

## 未解決の問題 {#open-issues}

表示式のフォーカスの設定は、アダプティブフォームでターゲット設定された画像では機能しません。
