---
title: バルクメタデータ読み込みおよび書き出し
description: この記事では、メタデータの読み込みおよび書き出しを一括でおこなう方法について説明します。
contentOwner: AG
translation-type: tm+mt
source-git-commit: 093524d47565f63c8179abee704720fe23b0d09a

---


# Bulk metadata import and export {#bulk-metadata-import-and-export}

AEM Assets では、CSV ファイルを使用して、アセットのメタデータを一括で読み込むことができます。CSV ファイルを読み込むことで、最近アップロードされたアセットや既存のアセットの一括更新をおこなうことができます。また、サードパーティシステムから CSV 形式でアセットメタデータを一括で取り込むこともできます。

## メタデータの読み込み {#import-metadata}

メタデータの読み込みは非同期であり、システムのパフォーマンスに影響はありません。ワークフロー実行フラグがチェックされている場合、XMP 書き戻しアクティビティが発生するので、複数のアセットのメタデータを同時に更新すると、リソースが集中的に使用されるおそれがあります。他のユーザーのパフォーマンスへの影響を防ぐために、リーンサーバーの使用中にこのようなインポートを計画します。

>[!NOTE]
>
>カスタム名前空間にメタデータを読み込むには、まず、その名前空間を登録します。

メタデータを一括で読み込むには、次の手順に従います。

1. Assets ユーザーインターフェイスに移動して、ツールバーの「**[!UICONTROL 作成]**」をタップまたはクリックします。
1. メニューから「**[!UICONTROL メタデータ]**」を選択します。
1. On the **[!UICONTROL Metadata Import]** page, tap/click the **[!UICONTROL Select File]**.  メタデータが入った CSV ファイルを選択します。
1. CSVファイルに次のパラメーターが含まれていることを確認します。

   | メタデータの読み込みパラメーター | 説明 |
   |:---|:---|
   | [!UICONTROL バッチサイズ] | メタデータを読み込むバッチ内のアセット数。デフォルト値は 50 です。最大値は 100 です。 |
   | [!UICONTROL フィールドセパレーター] | Default value is `,` – a comma. 他の文字も指定できます. |
   | [!UICONTROL 複数の値の区切り文字] | メタデータ値のセパレーター。デフォルト値 `|` は — パイプです。 |
   | [!UICONTROL ワークフローを開始] | デフォルトでは false です。When set to true and default Launcher settings are in effect for the `DAM Metadata WriteBack Workflow` (that writes metadata to the binary XMP data). 起動ワークフローを有効にすると、システムのパフォーマンスに影響します。 |
   | [!UICONTROL アセットパス列名] | アセットが含まれている、CSV ファイルの列名を定義します。 |

1. ツールバーの「**[!UICONTROL 読み込み]**」をタップまたはクリックします。メタデータが読み込まれると、通知が通知インボックスに送信されます。アセットのプロパティページに移動し、メタデータ値がアセットに正常に読み込まれたかどうかを確認します。

## メタデータの書き出し {#export-metadata}

メタデータの一括書き出しの使用例は次のとおりです。

* アセットの移行時にサードパーティシステムにメタデータを読み込む。
* より広範なプロジェクトチームとアセットメタデータを共有する。
* メタデータをテストまたは監査してコンプライアンスを確保する。
* メタデータを外部化して個別にローカライズできるようにする。

複数のアセットのメタデータをCSV形式で書き出すことができます。 メタデータは非同期的に書き出され、システムのパフォーマンスに影響を及ぼしません。To export metadata, AEM traverses through the properties of the asset node `jcr:content/metadata` and its child nodes and exports the metadata properties in a CSV file.

複数のアセットのメタデータを一括で書き出すには、次の手順に従います。

1. メタデータを書き出すアセットを含んだアセットフォルダーを選択します。ツールバーの「**[!UICONTROL メタデータを書き出し]**」を選択します。

1. In the [!UICONTROL Metadata Export] dialog, specify a name for the CSV file. サブフォルダーのアセットのメタデータを書き出すには、「**[!UICONTROL サブフォルダーのアセットを含める]**」を選択します。

   ![export_metadata_page](assets/export_metadata_page.png)

1. 目的のオプションを選択します。ファイル名を指定し、必要に応じて日付を指定します。
1. In the **[!UICONTROL Properties to be exported]**, specify whether you want to export all or specific properties. If you choose **[!UICONTROL Selective]** properties to be exported, add the desired properties.

1. ツールバーの「**[!UICONTROL 書き出し]**」をタップまたはクリックします。メタデータが書き出されることを確認するメッセージが表示されます。メッセージを閉じます。

1. 書き出しジョブのインボックス通知を開きます。ジョブを選択し、ツールバーの「**[!UICONTROL 開く]**」をクリックします。メタデータが含まれている CSV ファイルをダウンロードするには、ツールバーの「**[!UICONTROL CSV ダウンロード]**」をタップまたはクリックします。「**[!UICONTROL 閉じる]**」をクリックします。

   ![csv_download](assets/csv_download.png)
