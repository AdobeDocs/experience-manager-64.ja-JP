---
title: Forms のキャッシュの構成
seo-title: Configuring caching for Forms
description: キャッシュ設定の構成方法と、キャッシュの考慮事項のクラスター化方法について説明します。
seo-description: Learn how to configure cache settings and how to cluster considerations for caches.
uuid: 70f36191-4163-410b-991a-e1481488aea0
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_forms
products: SG_EXPERIENCEMANAGER/6.4/FORMS
discoiquuid: 8a07dddf-1281-45ac-a55e-4333b860a261
exl-id: 12ba2a8a-1260-4645-87c4-28f268e9d0ba
source-git-commit: c5b816d74c6f02f85476d16868844f39b4c47996
workflow-type: tm+mt
source-wordcount: '1644'
ht-degree: 25%

---

# Forms のキャッシュの構成 {#configuring-caching-for-forms}

>[!CAUTION]
>
>AEM 6.4 の拡張サポートは終了し、このドキュメントは更新されなくなりました。 詳細は、 [技術サポート期間](https://helpx.adobe.com/jp/support/programs/eol-matrix.html). サポートされているバージョンを見つける [ここ](https://experienceleague.adobe.com/docs/?lang=ja).

Formsサービスは、Designer で作成されたフォームデザインを使用し、様々な形式でレンダリングします。

管理コンソールのFormsページには、Formsサービスによる項目のキャッシュ方法を制御する設定が含まれています。 これらの設定を調整して、Formsサービスのパフォーマンスを最適化できます。

Formsサービスは、次の項目をキャッシュします。

* **フォームデザイン：** Forms サービスは、リポジトリまたは HTTP ソースから取得したフォームデザインをキャッシュします。このキャッシュにより、以降のレンダリング要求では、Forms サービスがリポジトリではなくキャッシュからフォームデザインを取得するようになるため、パフォーマンスが向上します。
* **フラグメントと画像：** Forms サービスでは、フォームデザインで使用されるフラグメントと画像をキャッシュできます。Forms サービスがこれらのオブジェクトをキャッシュすると、フラグメントと画像がリポジトリから読み取られるのは初回要求時のみになるので、パフォーマンスが向上します。
* **フォーム：** Forms サービスでは、レンダリング対象のフォームをキャッシュします。Formsサービスは、以降の要求で同じフォームを解決してレンダリングする必要がないので、このタイプのキャッシュではパフォーマンスが向上します。

Formsでは、次の 2 つの場所にキャッシュを保存します。

* **メモリ内：** アイテムは、すばやくアクセスできるようにメモリに保存されます。 メモリ内キャッシュのサイズは制限されており、サーバーを再起動すると削除されます。
* **ディスク上：** アイテムは、サーバーのファイルシステムに保存されます。 ディスクキャッシュは、メモリ内キャッシュよりも大きな容量を持ち、サーバーを再起動しても保持されます。 ディスクキャッシュの場所は、アプリケーションサーバーによって異なります。 ディスクキャッシュの場所の変更については、 [Formsの場所の設定](/help/forms/using/admin-help/configuring-locations-forms.md#configuring-locations-for-forms).

## キャッシュモードの指定 {#specifying-the-cache-mode}

Formsは、次の 2 つのキャッシュモードをサポートしています。

* 無条件
* キャッシュチェックポイントの使用

キャッシュモードを切り替えた場合、変更を有効にするには、Formsサービスを再起動します。 このサービスを再起動するには、Workbench を使用するか、 [AEM forms モジュールに関連付けられたサービスを開始または停止します](/help/forms/using/admin-help/starting-stopping-services.md#start-or-stop-the-services-associated-with-aem-forms-modules) 」を参照してください。

モードを切り替えると、キャッシュのチェックポイント時間が自動的にリセットされます。

### 無条件キャッシュの使用 {#using-unconditional-caching}

このモードでは、Formsサービスは要求を受け取ると、必要なリソース（フォームデザインと、フラグメントや画像などの関連アセット）を検証します。 Formsサービスは、リポジトリ内のリソースのタイムスタンプと、キャッシュ内のリソースのタイムスタンプを比較します。 キャッシュ内のリソースが古い場合は、Formsサービスによって更新されます。

このキャッシュモードでは、最新のリソースが確実に使用されます。 ただし、Formsサービスはキャッシュされた項目をリクエストごとにリポジトリと照らし合わせて検証するので、パフォーマンスが影響を受けます。 このキャッシュモードは、リソースが頻繁に更新され、パフォーマンスが主な問題とならない開発環境やステージング環境に適しています。

**無条件キャッシュの指定**

1. 管理コンソールで、サービス／Forms をクリックします。
1. 「 Forms Cache Control Settings 」で、「 Unconditional 」を選択し、「 Save 」をクリックします。

### キャッシュチェックポイントを使用 {#use-the-cache-check-point}

このモードでは、Formsサービスは、キャッシュされたリソースのタイムスタンプがキャッシュのチェックポイント時間よりも古い場合にのみ、リポジトリーで新しいバージョンのリソースを確認します。 最後のキャッシュのチェックポイント時間は、管理コンソールのFormsページに表示されます。

パフォーマンスが問題となり、リソースの変更が頻繁でない、高パフォーマンスの実稼動環境で、このキャッシュモードを使用します。 リポジトリリソースに加えた変更をデプロイする場合は、キャッシュのチェックポイント時間をリセットできます。

**キャッシュチェックポイントの使用を指定する**

1. 管理コンソールで、サービス/Formsをクリックします。
1. 「 Forms Cache Control Settings 」で、最後の検証がキャッシュのチェックポイント時間より前に実行された場合にのみ選択し、「 Save 」をクリックします。

**キャッシュのチェックポイントをリセット**

1. 管理コンソールで、サービス／Forms をクリックします。
1. 「 Forms Cache Control Settings 」で、「 Cache Check Point 」をクリックします。

**キャッシュの内容をリセット**

キャッシュの内容は、いつでもクリアできます。 キャッシュがリセットされると、Formsサービスは完全なレンダリングを実行して新しいキャッシュコンテンツを作成するので、各フォームの最初のリクエストは遅くなります。

1. 管理コンソールで、サービス／Forms をクリックします。
1. 「 Forms Cache Control Settings 」で、「 Reset Cache 」をクリックします。

## キャッシュ設定の指定 {#configuring-cache-settings}

Formsがキャッシュに使用する設定を指定できます。この設定により、AEM forms 環境のパフォーマンスを最適化できます。

これらの設定にアクセスするには、管理コンソールで、サービス/Formsをクリックします。

>[!NOTE]
>
>キャッシュのディスク要件は、リポジトリと同じである必要があります。

### グローバルキャッシュ設定の指定 {#specifying-global-cache-settings}

設定 **グローバルキャッシュ設定** 領域は、すべてのタイプのキャッシュに影響を与えます。 これらの設定のいずれかを変更した場合、変更を有効にするには、Formsサービスを再起動します。 このサービスを再起動するには、Workbench を使用するか、 [AEM forms モジュールに関連付けられたサービスを開始または停止します](/help/forms/using/admin-help/starting-stopping-services.md#start-or-stop-the-services-associated-with-aem-forms-modules) 」を参照してください。

**最大キャッシュドキュメントサイズ（KB）：**&#x200B;任意のメモリ内キャッシュに保存できるフォームデザインまたはその他のリソースの最大サイズ（キロバイト単位）です。これは、すべてのインメモリキャッシュに適用されるグローバル設定です。 リソースがこの値より大きい場合、そのリソースはメモリにキャッシュされません。 デフォルト値は 1024 キロバイトです。この設定は、ディスクキャッシュには影響しません。

**フォームレンダリングキャッシュの有効化：**&#x200B;デフォルトでは、このオプションが選択されており、レンダリングされたフォームがその後の取得のためにキャッシュされます。Formsサービスは特定のフォームを 1 回だけレンダリングし、キャッシュされたバージョンを使用するので、この設定によりパフォーマンスが向上します。 このオプションは、フォームデザインの caching プロパティと連携します。 フォームデザインでのこの値の設定について詳しくは、Designer ヘルプを参照してください。

### フォームデザインのキャッシュ {#caching-form-designs}

Formsサービスは、レンダリング要求を受け取ると、リポジトリからフォームデザインを取得してキャッシュします。 このキャッシュにより、以降のレンダリング要求では、Forms サービスがリポジトリではなくキャッシュからフォームデザインを取得するようになるため、パフォーマンスが向上します。

Formsサービスは、常にフォームデザインをディスクにキャッシュします。 フォームデザインがサーバー上に保存されている場合、これらのファイルはディスクキャッシュと見なされます。 また、Formsサービスは、 **メモリ内テンプレートキャッシュ** 領域 これらの設定のいずれかを変更した場合、変更を有効にするには、Formsサービスを再起動します。 このサービスを再起動するには、Workbench を使用するか、 [AEM forms モジュールに関連付けられたサービスを開始または停止します](/help/forms/using/admin-help/starting-stopping-services.md#start-or-stop-the-services-associated-with-aem-forms-modules) 」を参照してください。

**テンプレート設定キャッシュサイズ：**&#x200B;メモリに保持するテンプレート設定オブジェクトの最大数です。デフォルト値は 100 です。この値は、「テンプレートキャッシュサイズ」の値以上に設定することをお勧めします。 この設定は、ディスクキャッシュには影響しません。

**テンプレートキャッシュサイズ：**&#x200B;メモリ内に保持するテンプレートコンテンツオブジェクトの最大数です。デフォルト値は 100 です。この設定は、ディスクキャッシュには影響しません。

**有効：**&#x200B;デフォルトでは、このチェックボックスが選択されており、フォームテンプレートがメモリ内にキャッシュされます。このオプションを選択しない場合、フォームテンプレートはディスク上にのみキャッシュされます。

### レンダリングされたフォームのキャッシュ {#caching-rendered-forms}

Formsサービスは、レンダリングされたフォームをキャッシュし、以降の要求で同じフォームを解決してレンダリングする必要がないようにします。 レンダリングされたフォームは、ディスクとメモリの両方にキャッシュされます。

これらの設定は、 **メモリ内フォームレンダリングキャッシュ** 領域 これらの設定のいずれかを変更した場合、変更を有効にするには、Formsサービスを再起動します。 このサービスを再起動するには、Workbench を使用するか、 [AEM forms モジュールに関連付けられたサービスを開始または停止します](/help/forms/using/admin-help/starting-stopping-services.md#start-or-stop-the-services-associated-with-aem-forms-modules) 」を参照してください。

**キャッシュサイズ：**&#x200B;メモリ内キャッシュに格納できるレンダリングされたフォームの最大数を指定します。デフォルト値は 100 です。この設定は、ディスクキャッシュには影響しません。

**有効：**&#x200B;デフォルトでは、このオプションが選択されており、レンダリングされたフォームがメモリ内にキャッシュされます。このオプションを選択しない場合、レンダリングされたフォームはディスク上にのみキャッシュされます。

### フラグメントと画像のキャッシュ {#caching-fragments-and-images}

Formsサービスは、フォームデザインで使用されるフラグメントと画像をディスクにキャッシュします。 これにより、フラグメントと画像は最初の要求時にリポジトリから読み取られるだけになるので、パフォーマンスが向上します。 その後のリクエストでは、Formsサービスはディスクキャッシュからフラグメントと画像を読み取ります。 フラグメントと画像はディスク上にのみキャッシュされ、メモリ内にはキャッシュされません。

次の設定を使用して、フラグメントと画像のディスク上のキャッシュを制御できます。 これらの設定は、 **テンプレートリソースキャッシュ設定** 領域：

**リソースキャッシュ：**&#x200B;リストから次のいずれかのオプションを選択します。

**フラグメントと画像に対して有効：** Forms サービスはフラグメントと画像をキャッシュします。これはデフォルトのオプションです。

**フラグメントに対して有効：** Forms サービスはフラグメントをキャッシュしますが、画像はキャッシュしません。

**無効：** Forms サービスは、フラグメントも画像もキャッシュしません。

**クリーンアップ間隔（秒）：** Forms サービスが無効な古いキャッシュファイルを削除する頻度を指定します。Formsサービスは、有効なキャッシュファイルを削除しません。 クリーンアップ間隔を変更した場合、変更を有効にするには、Formsサービスを再起動します。 このサービスを再起動するには、Workbench を使用するか、AEM Forms モジュール関連サービスの開始と停止の説明を参照してください。デフォルト値は 600 秒です。

## キャッシュのクラスタリングに関する考慮事項 {#clustering-considerations-for-caches}

クラスタ環境では、各ノードは独自のメモリ内キャッシュとディスクキャッシュを維持します。 各ノードのキャッシュの内容は、そのノードでレンダリングされたフォームに応じて異なります。

キャッシュの場所は、クラスターの各ノードで同じ（同じディスクとパス）である必要があります。 共有ストレージにキャッシュを配置しないでください。

管理コンソールのFormsページを使用して特定のノードのキャッシュ設定を変更すると、リクエストがそのノードに送信されると、他のノードのキャッシュ設定が更新されます。 この動作は、「キャッシュをリセット」ボタンにも当てはまります。 あるノードの [ キャッシュをリセット ] ボタンをクリックすると、そのノードからキャッシュが直ちに削除されます。 リクエストがそのノードに送信されると、他のノードのキャッシュはクリアされます。
