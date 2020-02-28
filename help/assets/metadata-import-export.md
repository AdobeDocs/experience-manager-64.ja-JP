---
title: バルクメタデータ読み込みおよび書き出し
description: この記事では、メタデータの読み込みおよび書き出しを一括でおこなう方法について説明します。
contentOwner: AG
translation-type: tm+mt
source-git-commit: 0d70a672a2944e2c03b54beb3b5f734136792ab1

---


# バルクメタデータ読み込みおよび書き出し {#bulk-metadata-import-and-export}

AEM Assets では、CSV ファイルを使用して、アセットのメタデータを一括で読み込むことができます。CSV ファイルを読み込むことで、最近アップロードされたアセットや既存のアセットの一括更新をおこなうことができます。また、サードパーティシステムから CSV 形式でアセットメタデータを一括で取り込むこともできます。

## メタデータの読み込み {#import-metadata}

メタデータの読み込みは非同期であり、システムのパフォーマンスに影響はありません。ワークフロー実行フラグがチェックされている場合、XMP 書き戻しアクティビティが発生するので、複数のアセットのメタデータを同時に更新すると、リソースが集中的に使用されるおそれがあります。このようなインポートは、他のユーザーのパフォーマンスに影響しないように、サーバー使用率が低いときに計画します。

>[!NOTE]
>
>カスタム名前空間にメタデータを読み込むには、まず、その名前空間を登録します。

1. Assets ユーザーインターフェイスに移動して、ツールバーの「**[!UICONTROL 作成]**」をタップまたはクリックします。
1. メニューから「**[!UICONTROL メタデータ]**」を選択します。
1. On the **[!UICONTROL Metadata Import]** page, tap/click the **[!UICONTROL Select File]**.  メタデータが入った CSV ファイルを選択します。
1. 以下のパラメーターを指定します。

   | メタデータの読み込みパラメーター | 説明 |
   |:---|:---|
   | [!UICONTROL バッチサイズ] | メタデータを読み込むバッチ内のアセット数。デフォルト値は 50 です。最大値は 100 です。 |
   | [!UICONTROL フィールドセパレーター] | デフォルト値はコンマです。他の文字も指定できます。 |
   | [!UICONTROL 複数の値の区切り文字] | メタデータ値のセパレーター。デフォルト値は です。 | 。 |
   | [!UICONTROL ワークフローを開始] | デフォルトでは false です。trueに設定し、DAMメタデータ書き込みバックワークフロー（バイナリXMPデータにメタデータを書き込むワークフロー）に対してデフォルトのランチャー設定が有効な場合。 「ワークフローを開始」を有効にすると、システムの反応が遅くなります。 |
   | [!UICONTROL アセットパス列名] | アセットが含まれている、CSV ファイルの列名を定義します。 |

1. ツールバーの「**[!UICONTROL 読み込み]**」をタップまたはクリックします。メタデータが読み込まれると、通知が通知インボックスに送信されます。アセットのプロパティページに移動し、メタデータ値がアセットに正常に読み込まれたかどうかを確認します。

<!-- TBD: Format characters in the table using backticks and add UICONTROL after table is converted to MD
-->

## メタデータの書き出し {#export-metadata}

複数のアセットのメタデータを CSV 形式で書き出すことができます。メタデータは非同期的に書き出され、システムのパフォーマンスに影響を及ぼしません。To export metadata, AEM traverses through the properties of the asset node `jcr:content/metadata` and its child nodes and exports the metadata properties in a CSV file.

メタデータの一括書き出しの使用例は次のとおりです。

* アセットの移行時にサードパーティシステムにメタデータを読み込む。
* より広範なプロジェクトチームとアセットメタデータを共有する。
* メタデータをテストまたは監査してコンプライアンスを確保する。
* メタデータを外部化して個別にローカライズできるようにする。

1. メタデータを書き出すアセットを含んだアセットフォルダーを選択します。ツールバーの「**[!UICONTROL メタデータを書き出し]**」を選択します。

1. メタデータの書き出しダイアログで、CSV ファイルの名前を指定します。サブフォルダーのアセットのメタデータを書き出すには、「**[!UICONTROL サブフォルダーのアセットを含める]**」を選択します。

   ![export_metadata_page](assets/export_metadata_page.png)

1. 目的のオプションを選択します。ファイル名を指定し、必要に応じて日付を指定します。
1. In the **[!UICONTROL Properties to be exported]** specify whether you want to export all or specific properties. If you choose **[!UICONTROL Selective]** properties to be exported, add the desired properties.

1. ツールバーの「**[!UICONTROL 書き出し]**」をタップまたはクリックします。メタデータが書き出されることを確認するメッセージが表示されます。メッセージを閉じます。

1. 書き出しジョブのインボックス通知を開きます。ジョブを選択し、ツールバーの「**[!UICONTROL 開く]**」をクリックします。メタデータが含まれている CSV ファイルをダウンロードするには、ツールバーの「**[!UICONTROL CSV ダウンロード]**」をタップまたはクリックします。「**[!UICONTROL 閉じる]**」をクリックします。

   ![csv_download](assets/csv_download.png)
