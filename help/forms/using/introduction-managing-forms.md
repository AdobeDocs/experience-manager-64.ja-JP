---
title: フォーム管理の概要
seo-title: フォーム管理の概要
description: AEM Forms は、アダプティブフォームおよび関連アセットを管理するためのツールを提供します。本記事では、主なフォーム管理機能およびユーザーインターフェイス要素を紹介します。
seo-description: AEM Forms は、アダプティブフォームおよび関連アセットを管理するためのツールを提供します。本記事では、主なフォーム管理機能およびユーザーインターフェイス要素を紹介します。
uuid: 8a9fe83a-e9dc-410e-9bae-eca936c6eb8a
content-type: reference
products: SG_EXPERIENCEMANAGER/6.4/FORMS
topic-tags: introduction
discoiquuid: 6f9cb26a-ac7f-4218-827f-9d4d55b859b4
translation-type: tm+mt
source-git-commit: 1a671421c208d8b1b446765b9302877506dbddc2

---


# フォームの管理の概要 {#introduction-to-managing-forms}

AEM Forms は、フォーム、ドキュメント、テーマ、レター、ドキュメントフラグメント、データディクショナリおよび関連アセットを作成および管理するためのシンプルかつパワフルなユーザーインターフェイスを提供します。開発者のデスクトップから製品に至るまで、フォーム、ドキュメント、および関連アセットのライフサイクル全体を管理できます。\
エンドユーザー向けのポータルサーバー上にあります。 AEM Forms のユーザーインターフェイスを使用して次の操作を実行できます。

* AEM Forms コンポーネントへのアクセス
* AEM Forms 設定へのアクセス

>[!NOTE]
>
>For detailed information about other AEM tools and options, see [Working with the Author Environment](/help/sites-authoring/home.md).

## AEM Forms コンポーネントへのアクセス {#access-aem-forms-components}

AEM には、フォーム、ドキュメントおよび関連アセットを作成するためのオプションに加えて、サイトの作成、アセットの作成、AEM インスタンスの管理などのオプションが用意されています。You can click the ![adobeexperiencemanager](assets/adobeexperiencemanager.png) Experience Manager logo to navigate to all the available tools. 他のコンポーネントのコンソールへのリンクに加えて、AEM Forms のリンクもあります。To navigate to AEM Forms, click the **Experience Manager logo** ![adobeexperiencemanager](assets/adobeexperiencemanager.png) > **navigation** ![compass](assets/compass.png) > **Forms**. 以下のコンソールのリンクが表示されます。

* フォームとドキュメント
* テーマ
* レター
* ドキュメントフラグメント
* データディクショナリ

![aem-forms-console](assets/aem-forms-console.png)

### フォームとドキュメント  {#forms-documents}

フォームとドキュメントには、インタラクティブ通信、アダプティブフォーム、アダプティブフォームフラグメント、フォームセットを作成するためのオプションが用意されています。JEE 上の AEM Forms の場合のみ、ローカルストレージからファイルを読み込むオプションと AEM Forms アセットを Workbench と同期するオプションが「フォームとドキュメント」に表示されます。

作成ボタンは、AEM Forms アセットを作成またはアップロードする処理の開始点になります。次のオプションを作成できます。

* **Interactive Communication**:インタラクティブ通信は、HTMLベースのデジタル通信、ステートメント、ドキュメントをパーソナライズし、インタラクティブで、デバイスに対応した形式のドキュメントです。 インタラクティブ通信はレスポンシブな特性を持っているため、使用するデバイスや設定に応じて、レイアウトとデザインが自動的に変わります。詳しくは、「[インタラクティブ通信の概要](/help/forms/using/interactive-communications-overview.md)」を参照してください。

* **アダプティブフォーム：**&#x200B;アダプティブフォームは、魅力的でレスポンシブなフォームです。アダプティブフォームを作成し、ユーザーの応答、デバイス、または作業環境に基づいてフォームセクションを追加または削除することで、ユーザーの入力に動的に対応することができます。 アダプティブフォームについて詳しくは、「[アダプティブフォームの作成について](/help/forms/using/introduction-forms-authoring.md)」を参照してください。

* **アダプティブフォームフラグメント：**&#x200B;すべてのフォームは特定の目的のためにデザインされますが、ほとんどのフォームにはいくつかの共通するセグメントがあります。例えば、名前と住所、家族の詳細、収入の詳細などの個人の詳細を入力するためのものなどです。このようなセクションに対して個別のアセットを作成できます。これらの再利用可能なスタンドアロンセグメントは、アダプティブフォームフラグメントと呼ばれます。 詳しくは、「[アダプティブフォームフラグメント](/help/forms/using/adaptive-form-fragments.md)」を参照してください。

* **フォームセット：**&#x200B;フォームセットは HTML5 フォームの集まりであり、エンドユーザーには 1 つのフォームのセットとして提供されます。エンドユーザーがフォームセットへの入力を始めると、フォームはシームレスにその内容を別のフォームにも写します。最後に、ユーザーは1回のクリックですべてのフォームを単一のエンティティとして送信できます。 詳しくは、「[AEM Forms におけるフォームセット](/help/forms/using/formset-in-aem-forms.md)」を参照してください。

* **フォルダー：** AEM forms ユーザーインターフェイスは、フォルダーを利用してアセットを整理します。サポートされているフォルダーは 2 種類あります。

   * **一般フォルダー：**&#x200B;これらのフォルダーは、AEM forms ユーザーインターフェイスで作成されたアセットに対して使用されます。これらのフォルダーには、厳密なフォルダー構造はありません。これらのフォルダーでは、フォルダー名の変更とサブフォルダーの作成を行うことができます。また、アダプティブフォーム、インタラクティブ通信、アダプティブフォームフラグメント、フォームテンプレート（XDP）、PDF フォーム、ドキュメント、関連アセットを、これらのフォルダーに保存することができます。
   * **フォームワークフローフォルダー：**&#x200B;フォームワークフローフォルダーは、AEM Forms ユーザーインターフェイスで Workbench プロセス（LiveCycle アーカイブ）が移行および同期されるときに作成されます。このフォルダーの名前を変更することはできません。また、このフォルダー内に、サブフォルダー、インタラクティブ通信、アダプティブフォームフラグメントを作成することはできません。また、バージョンフォルダーの削除、アダプティブフォーム、アダプティブフォームフラグメント、またはインタラクティブ通信の作成とアップロードを、バージョンフォルダーと並行して行うこともできません。

![フォルダ](assets/folders.png)

******A.一般フォルダ**&#x200B;ーB。フォームワークフローフォルダー

フォームとドキュメントパネルには、以下のオプションも用意されています。

* **ローカルストレージからのファイルの読み込み：** PDF フォームとドキュメント、フォームテンプレート（XFA フォーム）およびその他のリソース（画像や XSD の XML スキーマ）を読み込むことができます。詳しい手順については、「[AEM Forms におけるアセットの読み込みと書き出し](/help/forms/using/import-export-forms-templates.md)」を参照してください。

* **AEM Forms アセットの Workbench との同期：**「Workbench のファイル」オプションを使用して、AEM Forms ユーザーインターフェイスと Workbench の間でアセットを同期することができます。これにより、AEM FormsユーザーインターフェイスとWorkbenchのcrx-repositoryアセット選択で、すべてのアセットが使用可能になります。

### テーマ  {#themes}

テーマには、コンポーネントやパネルのスタイル設定の詳細が含まれています。テーマには個別の ID があります。このため、1 つのテーマを複数のアダプティブフォームで再利用できます。コンポーネントに対してスタイルを指定したり、複数のフォームで使用されている様々なコンポーネントの CSS プロパティを変更したりできます。スタイルには、背景色、状態色、透明度、およびサイズなどのプロパティが含まれます。テーマのカスタマイズを保存し、プリセットとしてフォームのコンポーネントにそれらを移植することができます。テーマをフォームに追加すると、指定されたスタイルがフォームの対応コンポーネントに反映されます。AEM 6.2 Forms では、テーマを作成してフォームに適用できます。

テーマの作成と使用について詳しくは、「[AEM Forms のテーマ](/help/forms/using/themes.md)」を参照してください。

### レター  {#letters}

AEM Forms のレターは、安全でパーソナライズされたインタラクティブな通信です。AEM Forms を使用すると、合理化されたプロセスで承認済みコンテンツとカスタム作成コンテンツの両方からレター（通信とも呼ばれます）を簡単に作成できます。

レターの作成と使用について詳しくは、「[レターの作成](/help/forms/using/create-letter.md)」を参照してください。

### ドキュメントフラグメント {#document-fragments}

ドキュメントフラグメントは、レターの作成時に使用する再利用可能な通信のパーツやコンポーネントです。ドキュメントフラグメントのタイプとして、テキスト、リスト、条件およびレイアウトフラグメントがあります。ドキュメントフラグメントの作成と使用について詳しくは、「[ドキュメントフラグメントの作成](/help/forms/using/document-fragments.md)」を参照してください。

### データディクショナリ {#data-dictionaries}

一般のビジネスユーザーにとって、XSD（xml スキーマ）や Java クラスといった、メタデータ表現に関する知識は必要ありません。しかし、通常はソリューションを構築するために、これらのデータ構造や属性の利用が必要となります。AEM Forms でデータディクショナリを使用することにより、ビジネスユーザーはバックエンドデータソースの情報を使用できます。基礎となるデータモデルの技術的な詳細情報を把握する必要はありません。

データディクショナリの作成と使用について詳しくは、[データディクショナリに関する記事](/help/forms/using/data-dictionary.md)を参照してください。

## AEM Forms 設定へのアクセス {#accessing-aem-forms-configurations}

AEM ツールパネルには、様々なコンポーネント用のツールが含まれています。To navigate to AEM Forms-specific tools, click the **Experience Manager logo** ![adobeexperiencemanager](assets/adobeexperiencemanager.png) > **tools** ![hammer](assets/hammer.png) > **Forms**. 以下の機能を実行するためのツールが表示されます。

* **監視フォルダーを設定：**&#x200B;管理者は、監視フォルダーと呼ばれるネットワークフォルダーを設定できます。ユーザーがファイル（PDF ファイルなど）を監視フォルダーに配置すると、設定済みの操作が開始され、ファイルが操作されます。<!-- Fix broken link For detailed information, see Create and Configure a watched folder. -->

* **** Forms App Offline Serviceの設定：AEM Formsアプリケーションのオフラインサービスは、フォームで使用されるリソースのパスまたはURLをキャッシュします。 フォームで使用されるリソースのパスや URL をキャッシュに保存することで、サーバー側のパフォーマンスが向上します。To configure the server-side offline component of AEM Forms app, see [Working in the offline mode](/help/forms/using/work-offline-mode.md).

![aem-forms-tools](assets/aem-forms-tools.png)

* **PDF Generator を設定：**&#x200B;管理者は、AEM Forms PDF Generator の設定、ユーザーアカウントの追加、PDF Generator 設定の読み込みまたは書き出しを行うことができます。
* **Correspondence Management アセットを発行：** AEM Forms では、作成者インスタンスからすべてのレター、ドキュメントフラグメント、データディクショナリおよび関連する依存関係を同時に発行できます。発行済みのアセットには、すべての Correspondence Management アセットと関連する依存性が含まれます。For detailed information, see [Publishing and unpublishing forms &amp; documents](/help/forms/using/publishing-unpublishing-forms.md#publishallthecorrespondencemanagementassets).
* **Correspondence Management アセットを書き出し：**&#x200B;すべての Correspondence Management アセットおよび関連する依存関係を、AEM Forms インスタンスからパッケージとしてダウンロードできます。手順について詳しくは、「[AEM Forms におけるアセットの読み込みと書き出し](/help/forms/using/import-export-forms-templates.md#importandexportassetsincorrespondencemanagement)」を参照してください。

## 共通のユーザーインターフェイス要素 {#commonelements}

* **** 左側のレール：左側のレールアイコンのレールをクリッ ![クすると](assets/railleftpng.png) 、AEM Formsのタイムライン機能とリファレンス機能が表示されます。

   * **タイムライン：**&#x200B;アセットに対するコメントをタイムラインに追加して表示し、レビューとして使用できます。手順について詳しくは、「[フォームのアセットのレビューの作成と管理](/help/forms/using/create-reviews-forms.md)」を参照してください。
   * **参照：** 1 つの AEM Forms アセットを複数の AEM Forms アセットで使用できます。例えば、1 つのドキュメントフラグメントを複数のレターで使用できます。「参照」は、選択したアセットが使用されるアセット（他のフォームまたはリソース）のリストで、選択したアセットが使用している他のアセットのリストです。

* **パンくず：**&#x200B;パンくずは、現在のコンソールまたはフォルダーのタイトルを表します。「パンくず」オプションをクリックすると、フォルダー階層の上位のフォルダーに移動することができます。
* **** 表示切り替え：表示切り替えアイコンviewlistまたはviewcardをクリッ ![クすると](assets/viewlist.png) 、リスト表示と ![](assets/viewcard.png) カード表示をすばやく切り替えることができます。 共通のユーザーインターフェイスコンポーネントについて詳しくは、「[作成者環境の操作](/help/sites-authoring/basic-handling.md)」を参照してください。
* **** 検索：検索オプション検索 ![を使用すると](assets/search.png) 、必要なコンテンツやツールをすばやく検索して表示できます。 コンテンツまたは製品機能の名前を入力し、提案から選択します。例えば、「ドキュメント」と入力すると、フォームとドキュメントコンソールやドキュメントフラグメントコンソールをすばやく見つけて移動できます。検索について詳しくは、AEM 6.2 の[検索](/help/sites-authoring/search.md)に関する記事を参照してください。
* **アクションツールバー**：アセットを選択すると、アセット一覧の上にアクションツールバーが表示されます。このツールバーには、選択したアセットに対応するすべての管理ツールが表示されます。ツールアイコンの上にマウスを移動すると、その機能を説明するツールヒントが表示されます。

>[!NOTE]
>
>ユーザーがフォームとドキュメントのコンソールを検索すると、「**フィルターおよびオプション**」のみがレールに表示されます。「フィルターおよびオプション」を使用して、高度な検索を実行できます。

* **アクションツールバー**：アセットを選択すると、アセット一覧の上にアクションツールバーが表示されます。このツールバーには、選択したアセットに対応するすべての管理ツールが表示されます。ツールアイコンの上にマウスを移動すると、その機能を説明するツールヒントが表示されます。

![アダプティブフォームのアクションツールバー](assets/action-tool-bar.png)