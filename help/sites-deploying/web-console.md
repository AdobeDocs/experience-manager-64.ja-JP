---
title: Web コンソール
seo-title: Web Console
description: AEM Web コンソールの使用方法について学習します。
seo-description: Learn how to use the AEM web console.
uuid: 7856b2b3-4216-421d-a315-cd9a55936362
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.4/SITES
content-type: reference
topic-tags: configuring
discoiquuid: 4a33fddd-0399-40e4-8687-564fb6765b76
feature: Configuring
exl-id: a8a3267d-2af5-4cca-b76d-66de62d93f69
source-git-commit: bd94d3949f0117aa3e1c9f0e84f7293a5d6b03b4
workflow-type: tm+mt
source-wordcount: '718'
ht-degree: 73%

---

# Web コンソール{#web-console}

AEM の Web コンソールは、[Apache Felix Web Management Console](https://felix.apache.org/documentation/subprojects/apache-felix-web-console.html) に基づいています。Apache Felix は、OSGi R4 サービスプラットフォームを実装するためのコミュニティによる取り組みです。このプラットフォームには、OSGi フレームワークと標準のサービスが含まれています。

>[!NOTE]
>
>Web コンソールでは、デフォルト設定に言及している説明はすべて、Sling のデフォルトに関連しています。
>
>AEM には独自のデフォルト値があるので、設定されるデフォルト値は、コンソールに表示される値と異なる場合があります。

Web コンソールには、OSGi バンドルを保守するための次のような一連のタブがあります。

* [Configuration](#configuration)：OSGi バンドルの設定に使用します。AEM システムパラメーターを設定するための基盤となるメカニズムです。
* [Bundles](#bundles)：バンドルのインストールに使用します。
* [Components](#components)：AEM で必要なコンポーネントのステータスの制御に使用します。

おこなわれた変更は、実行中のシステムにすぐに適用されます。再起動は不要です。

コンソールには、からアクセスできます。 `../system/console`;例：

`http://localhost:4502/system/console/components`

## 設定 {#configuration}

「**Configuration**」タブは、OSGi バンドルの設定に使用します。AEM システムパラメーターを設定するための基盤となるメカニズムです。

>[!NOTE]
>
>詳しくは、[Web コンソールでの OSGi 設定](/help/sites-deploying/configuring-osgi.md)を参照してください。

「**Configuration**」タブにアクセスするには、次のいずれかを使用します。

* ドロップダウンメニュー：

   **OSGi >**

* URL例：

   `http://localhost:4502/system/console/configMgr`

設定のリストは次のように表示されます。

![screen_shot_2012-02-15at52308pm](assets/screen_shot_2012-02-15at52308pm.png)

この画面のドロップダウンリストから、次の 2 種類の設定を使用できます。

* **Configurations**
既存の設定を更新できます。設定には永続識別子（PID）が割り当てられています。設定は次のいずれかになります。

   * 標準かつ AEM に不可欠な設定。これらの設定は必須であり、削除すると値がデフォルト設定に戻ります。
   * 「Factory Configurations」から作成されたインスタンス。これらのインスタンスはユーザーによって作成され、削除するとインスタンスが削除されます。

* **Factory Configurations**
必要な機能オブジェクトのインスタンスを作成できます。

   このインスタンスには永続識別子が割り当てられます。また、「Configurations」ドロップダウンリストに表示されます。

リストからエントリを選択すると、その設定に関連するパラメーターが表示されます。

![chlimage_1-21](assets/chlimage_1-21.png)

必要に応じて、パラメーターを更新し、次の処理をすることができます。

* **保存**

   変更を保存します。

   ファクトリ設定の場合は、永続識別子を持つ新しいインスタンスが作成されます。新しいインスタンスは「Configurations」に表示されます。

* **リセット**

   画面に表示されるパラメータを、最後に保存されたパラメータにリセットします。

* **削除**

   現在の設定を削除します。 標準の場合は、パラメーターがデフォルト設定に戻ります。ファクトリ設定から作成された場合は、特定のインスタンスが削除されます。

* **Unbind**

   現在の設定をバンドルからバインド解除します。

* **キャンセル**

   現在の変更をキャンセルします。

## バンドル {#bundles}

この **バンドル** 「 」タブは、AEMに必要な OSGi バンドルをインストールするためのメカニズムです。タブにアクセスするには、次のいずれかの方法を使用します。

* ドロップダウンメニュー：

   **OSGi >**

* URL例：

   `http://localhost:4502/system/console/bundles`

バンドルのリストは次のように表示されます。

![screen_shot_2012-02-15at44740pm](assets/screen_shot_2012-02-15at44740pm.png)

このタブでは、次のことができます。

* **インストールまたは更新**

   以下が可能です。 **参照** をクリックして、バンドルを含むファイルを検索し、 **開始** すぐに **開始レベル**.

* **再読み込み**

   表示されているリストを更新します。

* **パッケージを更新**

   これにより、すべてのパッケージの参照がチェックされ、必要に応じて更新されます。

   例えば、更新後に、以前の参照が原因で古いバージョンと新しいバージョンの両方が引き続き実行される場合などです。このオプションでは、新しいバージョンへの参照をすべて確認して移動します。これにより、古いバージョンを停止できます。

* **開始**

   指定した開始レベルに従って、バンドルを開始します。

* **停止**

   バンドルを停止します。

* **アンインストール**

   システムからバンドルをアンインストールします。

* **ステータスの確認**

   このリストは、バンドルの現在のステータスを示します。特定のバンドルの名前をクリックすると、詳細情報が表示されます。

>[!NOTE]
>
>**更新**&#x200B;後に、**パッケージの更新**&#x200B;を実行することをお勧めします。

## コンポーネント {#components}

この **コンポーネント** 「 」タブを使用すると、様々なコンポーネントを有効または無効にできます。次のいずれかの方法でアクセスできます。

* ドロップダウンメニュー：

   **メイン >**

* URL例：

   `http://localhost:4502/system/console/components`

コンポーネントのリストは次のように表示されます。特定のコンポーネントを有効または無効にしたり、（必要に応じて）コンポーネントの設定の詳細を開いたりするための様々なアイコンがあります。

![screen_shot_2012-02-15at52144pm](assets/screen_shot_2012-02-15at52144pm.png)

特定のコンポーネントの名前をクリックすると、そのステータスに関する詳細情報が表示されます。ここで、コンポーネントを有効または無効にしたり、再読み込みしたりすることもできます。

![chlimage_1-22](assets/chlimage_1-22.png)

>[!NOTE]
>
>コンポーネントの有効化または無効化が適用されるのは、AEM／CRX が再起動されるまでです。
>
>開始状態はコンポーネントの記述子内で定義されます。この記述子は開発時に生成され、バンドルの作成時にバンドルに格納されます。
