---
title: アダプティブフォームの自動保存
seo-title: Auto-save an adaptive form
description: アダプティブフォームを設定して、イベントまたは事前定義された時間間隔に基づいてコンテンツの自動保存を開始することができます
seo-description: You can configure an adaptive form to automatically start saving the content based on an event or a pre-defined time-interval
uuid: 0fe9a389-269b-438a-9489-d9d1d09558a1
products: SG_EXPERIENCEMANAGER/6.4/FORMS
topic-tags: author
discoiquuid: d519ac4e-6d29-4a69-874e-792acabe87ff
feature: Adaptive Forms
exl-id: 073734e9-449b-463a-b539-d73e11f50fa4
source-git-commit: c5b816d74c6f02f85476d16868844f39b4c47996
workflow-type: tm+mt
source-wordcount: '724'
ht-degree: 39%

---

# アダプティブフォームの自動保存 {#auto-save-an-adaptive-form}

>[!CAUTION]
>
>AEM 6.4 の拡張サポートは終了し、このドキュメントは更新されなくなりました。 詳細は、 [技術サポート期間](https://helpx.adobe.com/jp/support/programs/eol-matrix.html). サポートされているバージョンを見つける [ここ](https://experienceleague.adobe.com/docs/?lang=ja).

アダプティブフォームを設定して、イベントまたは事前定義された時間間隔に基づいてコンテンツの保存を自動的に開始することができます。 デフォルトでは、アダプティブフォームのコンテンツは、保存ボタンを押したときなど、ユーザーの操作時に保存されます。 自動保存オプションは、次の場合に便利です。

* 匿名ユーザーおよびログインユーザー向けにコンテンツを自動的に保存
* ユーザーの介入をほとんどまたはほとんど必要とせずにフォームのコンテンツを保存する
* ユーザーイベントに基づいてフォームのコンテンツの保存を開始する
* 指定した時間間隔の後で繰り返しフォームのコンテンツを保存する

## アダプティブフォームの自動保存を有効にする {#enable-autosave-for-an-adaptive-form}

アダプティブフォームの場合、自動保存オプションは初期状態では有効になっていません。 自動保存オプションは、 **自動保存** 」セクションを使用して、アダプティブフォームのプロパティに関する情報を入力できます。 「**自動保存**」セクションには、その以外の設定オプションがいくつか用意されています。次の手順を実行して、アダプティブフォームの自動実行オプションを有効にし設定します。

1. プロパティの「自動保存」セクションにアクセスするには、コンポーネントを選択して、![フィールドレベル](assets/field-level.png)／**[!UICONTROL アダプティブフォームコンテナ]**／ ![cmppr](assets/cmppr.png) の順にタップします。
1. 内 **[!UICONTROL 自動保存]** セクション **[!UICONTROL 有効にする]** 自動保存オプション
1. 内 **[!UICONTROL アダプティブフォームイベント]** ボックスに 1 を指定するか、TRUE を指定すると、フォームがブラウザに読み込まれたときに自動的にフォームの保存が開始されます。 また、イベントの条件式を指定すると、そのイベントがトリガーされて true が返され、フォームのコンテンツの保存が開始されます。
1. トリガー 自動保存は、設定に基づいてトリガーされます。 以下のオプションがあります。

   * **[!UICONTROL 時刻ベース]**：指定の時間間隔に基づいてコンテンツの保存を開始するには、このオプションを選択します。
   * **[!UICONTROL イベントベース]**：イベントがトリガーされたときにコンテンツの保存を開始するには、このオプションを選択します。

   「トリガー」を選択すると、「方法の設定」ボックスが有効になります。 「方法の設定」ボックスでは、次の操作を実行できます。

   * **[!UICONTROL 時刻ベース]**&#x200B;のトリガーを選択した場合は、時間間隔を指定します。
   * **[!UICONTROL イベントに基づく]**&#x200B;トリガーを選択した場合は、イベントの名前を指定します。

   また、独自のカスタム方法を作成してリストに追加することもできます。 詳しくは、 [フォームを自動保存するためのカスタム方法の実装](/help/forms/using/auto-save-an-adaptive-form.md#p-implement-a-custom-strategy-to-enable-autosave-for-adaptive-forms-p).

1. （時間ベースの自動保存のみ）次の手順を実行して、時間ベースの自動保存のオプションを設定します。

   1. 内 **[!UICONTROL この間隔で自動保存]** ボックスに、時間間隔を秒単位で指定します。 「間隔」ボックスに指定した秒数が経過すると、フォームは繰り返し保存されます。

1. （イベントベースの自動保存のみ）次の手順を実行して、イベントベースの自動保存のオプションを設定します。

   1. 「**このイベント後に自動保存**」ボックスで、[GuideBridge](https://helpx.adobe.com/jp/aem-forms/6/javascript-api/GuideBridge.html) イベントを指定します。式が TRUE に評価されるたびに、フォームが保存されます。

1. （オプション）匿名ユーザーに対するコンテンツを自動的に保存するには、「**匿名ユーザーの自動保存を有効にする**」オプションを選択し、「**[!UICONTROL OK]**」をクリックします。

   >[!NOTE]
   >
   >自動保存オプションを匿名ユーザーに対して機能させるには、すべてのユーザーがフォームのプレビュー、確認および署名を行えるように Forms 共通設定サービスが設定されていることを確認します。
   >
   >このサービスを設定するには、`https://[server]:[host]/system/console/configMgr` にある AEM web コンソール設定に移動して **[!UICONTROL Forms 共通設定サービス]** を編集し、「**[!UICONTROL 許可]**」フィールドで「**[!UICONTROL すべてのユーザー]**」オプションを選択して、設定を保存します。

## アダプティブフォームの自動保存を有効にするカスタム方法を実装する {#implement-a-custom-strategy-to-enable-autosave-for-adaptive-forms}

カスタムイベントを実装して自動保存機能をトリガー化できます。 次の手順を実行して、カスタムイベントを作成し実装します。

1. クライアントライブラリとクライアントライブラリフォルダーを作成します。 詳細な手順については、 [クライアント側ライブラリドキュメントの使用](/help/sites-developing/clientlibs.md).

   例えば、次のスクリプトでは、カスタムの `emailFocusChange` イベントを使用して自動保存機能をトリガーしています。

   ```
   window.addEventListener("bridgeInitializeStart", function (){   
       guideBridge.connect(function () { guideBridge.on("elementFocusChanged", function (event,data) { 
           if(data.target.name === 'Email') {
               guideBridge.trigger("emailFocusChange");
           }
       });
      });
   });
   ```

   >[!NOTE]
   >
   >クライアントライブラリフォルダーの作成時に、カテゴリプロパティが定義されます。カテゴリプロパティに割り当てた値を書き留めておきます。

1. アダプティブフォームを作成者モードで開きます。

1. 編集モードでコンポーネントを選択し、![フィールドレベル](assets/field-level.png)／**[!UICONTROL アダプティブフォームコンテナ]**／![cmppr](assets/cmppr.png) をタップします。
1. プロパティで、 **[!UICONTROL 基本]** 」セクションに入力します。 内 **[!UICONTROL クライアントライブラリカテゴリ]** 「 」ボックスに、クライアントライブラリフォルダーの作成時に定義した category プロパティの値を入力します。
1. 「自動保存」セクションを開きます。 内 **[!UICONTROL このイベント後に自動保存]** ボックスに、クライアントライブラリで既に定義されているカスタムイベントを指定します。 「**[!UICONTROL OK]**」をクリックします。
