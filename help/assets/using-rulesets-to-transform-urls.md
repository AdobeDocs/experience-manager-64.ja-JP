---
title: ルールセットを使用した URL の変換
description: Dynamic Media でルールセットをデプロイして、URL を変換できます。ルールセットはスクリプティング言語（JavaScript など）で記述された命令セットで、XML データを評価して、そのデータが特定の条件を満たす場合に特定のアクションを実行します。
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.4/ASSETS
topic-tags: dynamic-media
content-type: reference
exl-id: f0cd3a75-03ed-40a9-b336-8a782f3cfe69
feature: Rulesets
role: Admin,User,Developer
source-git-commit: c5b816d74c6f02f85476d16868844f39b4c47996
workflow-type: tm+mt
source-wordcount: '798'
ht-degree: 71%

---

# ルールセットを使用した URL の変換 {#using-rulesets-to-transform-urls}

>[!CAUTION]
>
>AEM 6.4 の拡張サポートは終了し、このドキュメントは更新されなくなりました。 詳細は、 [技術サポート期間](https://helpx.adobe.com/jp/support/programs/eol-matrix.html). サポートされているバージョンを見つける [ここ](https://experienceleague.adobe.com/docs/?lang=ja).

Dynamic Media でルールセットをデプロイして、URL を変換できます。ルールセットはスクリプティング言語（JavaScript など）で記述された命令セットで、XML データを評価して、そのデータが特定の条件を満たす場合に特定のアクションを実行します。各ルールは、少なくとも 1 つの条件と、少なくとも 1 つのアクションで構成されます。 ルールは、XML データを条件と照らし合わせて評価し、条件が満たされた場合は、適切なアクションを実行します。 ルールセットの例を次に示します。

* MIME タイプのサフィックスの追加 多くのサービスや Web サイトでは、`.jpg` を URL に付加するなど、画像のサフィックスが必要です。
* SEO（検索エンジン最適化）のための URL へのフォルダーパスの作成。

   「[Adobe Dynamic Media Classic が SEO をサポートする方法](/help/assets/assets/s7_seo.pdf)」を参照してください。

* SEO（検索エンジン最適化）のための URL へのメタデータの付加。

   「[Adobe Dynamic Media Classic が SEO をサポートする方法](/help/assets/assets/s7_seo.pdf)」を参照してください。

* ダウンロードをトリガーするコンテンツ廃棄の設定
* パーソナライズのための画像サービングテンプレート URL を簡素化します。 例えば、`rgb{XX,YY,ZZ}` を RTF 対応の `\redXX\greenYY\blueZZ` に変換します。

* `$`、`{`、`}` などの特定の文字のエンコードと、ImageServer への特定の文字のデコードのリクエスト。例えば、Facebook は特殊文字を含む URL では正しく機能しません。

   [URL からの特殊文字の削除](https://helpx.adobe.com/jp/experience-manager/scene7/kb/base/scene7-rulesets/remove-special-characters-urls.html)を参照してください。

Dynamic Mediaのコンテキストでは、XML ベースのシステムを使用してアセット情報を管理する Web サイトは、XML ファイルをDynamic Mediaにアップロードできます。 これらのファイルの 1 つを、Dynamic Mediaアセットを処理する前処理ルールセットファイルとして指定できます。 このファイルは、Dynamic Mediaと統合するシステムのビジネスロジックを満たすように、標準 URL プロトコル形式を再構成します。 XML ファイルをルールセット定義ファイルのパスとして指定します。

>[!CAUTION]
>
>ルールセットを使用する場合は、Dynamic Media のコンテンツが Web サイトに表示されなくなる可能性があるので、注意してください。

用意されているサンプルルールセットを使用して、独自のルールセットを作成できます。\
[ルールセットのリファレンス](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/rule-set-reference/c-rule-set-reference.html?lang=ja)を参照してください。

すべてのルールセットの作成と同様に、xmlvalid などの XML バリデータープログラムを使用して、XML ファイルが有効であることを確認してからアップロードしてください。\
[ルールセットのトラブルシューティング](https://helpx.adobe.com/jp/experience-manager/scene7/kb/base/scene7-rulesets/scene7-ruleset-troubleshooting.html)も参照してください。

また、最初は実稼動環境に影響を与えないステージング環境でルールセットをテストしてください。\
通常、実稼動環境とステージング環境では異なるログイン情報が必要となります。

ログイン情報については、「[Adobe Dynamic Media クラシックにサインイン](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html?lang=ja#sign-in-dmc-app)」を参照してください。

<!-- * **NA staging environment** login page: [https://s7sps1-staging.scene7.com/IpsWeb/](https://s7sps1-staging.scene7.com/IpsWeb/)
* **EMEA staging environment** login page: [https://s7sps3-staging.scene7.com/IpsWeb/](https://s7sps3-staging.scene7.com/IpsWeb/)
* **JAPAC staging environment** login page: [https://s7sps5-staging.scene7.com/IpsWeb/](https://s7sps5-staging.scene7.com/IpsWeb/) -->

[ルールセットでの &#39;is&#39; イメージに代わる &#39;asset&#39; の使用](https://helpx.adobe.com/jp/experience-manager/scene7/kb/base/scene7-rulesets/ruleset-asset-instead-image.html)も参照してください。

**XML ルールセットをデプロイするには：**

1. [Dynamic Media Classic デスクトップアプリケーション](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html?lang=ja)にサインインします。

   資格情報とログインは、プロビジョニング時にAdobeから提供されました。 この情報をお持ちでない場合は、テクニカルサポートにお問い合わせください。

1. 次の手順を実行して、ルールセットファイルをアップロードします。

   * グローバルナビゲーションバーで、 **[!UICONTROL アップロード]**.
   * **[!UICONTROL アップロード]**&#x200B;ページで、左上隅付近の「**[!UICONTROL 参照]**」をクリックします。
   * **[!UICONTROL 開く]**&#x200B;ダイアログボックスで、ルールセットファイル（XML）を参照します。
   * ファイルを選択して、「**[!UICONTROL 開く]**」をクリックします。
   * **[!UICONTROL アップロード]**&#x200B;ページの右側で、ルールセットファイルの公開先フォルダーを選択します。
   * ページ下部付近で、 **[!UICONTROL アップロード後に公開]** がオンになっている。
   * ページの右下隅で、 **[!UICONTROL アップロードを送信]**.
   * グローバルナビゲーションバーの「**[!UICONTROL ジョブ]**」をクリックして、アップロードジョブのステータスを確認します。**[!UICONTROL ジョブ]**&#x200B;ページの「**[!UICONTROL ステータス]**」列に「アップロード完了」と表示されたら、次のステップに進みます。

1. ページ上部付近のナビゲーションバーで、**[!UICONTROL 設定／アプリケーション設定／公開設定／Image Server]** をクリックします。
1. **[!UICONTROL Image Server 公開]**&#x200B;ページの「**[!UICONTROL カタログ管理]**」グループで、**[!UICONTROL ルールセット定義ファイルのパス]**&#x200B;を探し、「**[!UICONTROL 選択]**」をクリックします。
1. **[!UICONTROL ルールセット定義ファイル（XML）を選択]**&#x200B;ページでルールセットファイルを参照し、ページ右下隅の「**[!UICONTROL 選択]**」をクリックします。
1. 設定ページの右下隅で、 **[!UICONTROL 閉じる]**.
1. Image Server 公開ジョブを実行します。

   ルールセットの条件は、ライブDynamic Media Image Servers へのリクエストに適用されます。

   ルールセットファイルを変更した場合、変更したルールセットファイルを再アップロードして再公開すると、変更内容が直ちに適用されます。
