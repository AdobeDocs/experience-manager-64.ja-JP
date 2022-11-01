---
title: アダプティブフォームでのAcrobat Signの使用
seo-title: Using Acrobat Sign in an adaptive form
description: アダプティブフォームの電子署名 (Acrobat Sign) ワークフローを有効にして、署名ワークフローを自動化し、単一および複数の署名プロセスを簡素化し、モバイルデバイスからフォームに電子署名を行います。
seo-description: Enable e-signature (Acrobat Sign) workflows for an adaptive form to automate signing workflows, simplify single and multi-signature processes, and to electronically sign forms from mobile devices.
uuid: 9c65dc44-c1a5-44df-8659-6efbe347575b
contentOwner: khsingh
products: SG_EXPERIENCEMANAGER/6.4/FORMS
topic-tags: develop
discoiquuid: 29fc297e-0a95-4d2a-bfe6-5676d53624db
noindex: true
feature: Adaptive Forms, Acrobat Sign
exl-id: 5922ea6e-8be9-4e65-89a6-67b6cc12c4ee
source-git-commit: f8b19b6723d333e76fed111b9fde376b3bb13a1d
workflow-type: tm+mt
source-wordcount: '3562'
ht-degree: 53%

---

# アダプティブフォームでのAcrobat Signの使用 {#using-adobe-sign-in-an-adaptive-form}

アダプティブフォームの電子署名 (Acrobat Sign) ワークフローを有効にして、署名ワークフローを自動化し、単一および複数の署名プロセスを簡素化し、モバイルデバイスからフォームに電子署名を行います。

Acrobat Signを使用すると、アダプティブフォームの電子署名ワークフローが有効になります。 電子署名を利用すると、法務、販売、給与、人事管理など分野でドキュメントを処理するワークフローを改善できます。

一般的なAcrobat Signおよびアダプティブフォームのシナリオでは、ユーザーはアダプティブフォームに入力してサービスを申し込みます。 例えば、住宅ローンやクレジットカードの申請では、すべての借り手や共同申請者から、法的に有効な署名を取得する必要があります。同様のシナリオで電子署名ワークフローを有効にするには、Acrobat SignとAEM Formsを統合します。 その他の例として、 Acrobat Signを使用して次のことができます。

* 完全に自動化された提案プロセス、見積りプロセス、契約プロセスを使用して、任意のデバイスで契約を締結する。
* 人事プロセスを短時間で完了し、従業員に対してデジタルエクスペリエンスを提供する。
* 契約のサイクルタイムを短縮し、ベンダーとの取引を早期に開始する。
* 共通するプロセスを自動化するためのデジタルワークフローを作成する。

Acrobat SignとAEM Formsの統合では、次のことがサポートされます。

* 単一ユーザーと複数ユーザーの署名ワークフローを処理する機能
* 複数の署名ワークフローを並列的に順次処理する機能
* フォーム内とフォーム外での署名機能
* 匿名ユーザーまたはログインユーザーとしてフォームを署名する機能
* 動的な署名プロセスを処理する機能（AEM Forms のワークフローと統合）
* ナレッジベース、電話、ソーシャルプロファイルによる認証機能

詳しくは、 [アダプティブフォームでのAcrobat Signの使用に関するベストプラクティス](https://medium.com/adobetech/using-adobe-sign-to-e-sign-an-adaptive-form-heres-the-best-way-to-do-it-dc3e15f9b684) より優れた署名エクスペリエンスを作成するため。

## 前提条件 {#prerequisites}

アダプティブフォームでAcrobat Signを使用する前に、以下の手順を実行します。

* AEM Forms Cloud Service がAcrobat Signを使用するように設定されていることを確認します。 詳しくは、 [Acrobat SignとAEM Formsの統合](/help/forms/using/adobe-sign-integration-adaptive-forms.md).
* 署名者のリストが準備されていること。少なくとも、各署名者の電子メールアドレスが必要になります。

## アダプティブフォーム用のAcrobat Signの設定 {#configure-adobe-sign-for-an-adaptive-form}

アダプティブフォーム用にAcrobat Signを設定するには、以下の手順を実行します。

1. [Acrobat Signのアダプティブフォームプロパティの編集](#enableadobesign)
1. [Acrobat Signフィールドをアダプティブフォームに追加する](#addadobesignfieldstoanadaptiveform)
1. [アダプティブフォームのAcrobat Signの有効化](#enableadobsignforanadaptiveform)
1. [アダプティブフォームのAcrobat SignCloud Serviceを選択](#selectadobesigncloudserviceforanadaptiveform)

1. [Acrobat Sign署名者をアダプティブフォームに追加する](#addsignerstoanadaptiveform)
1. [アダプティブフォームに対して送信アクションを選択する](#selectsubmitactionforanadaptiveform)

![signer-details](assets/signer-details.png)

### Acrobat Signのアダプティブフォームプロパティの編集 {#enableadobesign}

既存のアダプティブフォームまたは新しいアダプティブフォームに対して、Acrobat Signのアダプティブフォームプロパティを設定します。

[Acrobat Sign用アダプティブフォームの作成](/help/forms/using/working-with-adobe-sign.md#create-an-adaptive-form-for-adobe-sign) 基本的なアダプティブフォームを作成する手順を説明します。 詳しくは、 [アダプティブフォームの作成](/help/forms/using/creating-adaptive-form.md) アダプティブフォームの作成時に使用できるその他のオプションについては、を参照してください。

#### Acrobat Sign用アダプティブフォームの作成 {#create-an-adaptive-form-for-adobe-sign}

Acrobat Sign用のアダプティブフォームを作成するには、以下の手順を実行します。

1. **[!UICONTROL Adobe Experience Manager]**／**[!UICONTROL Forms]**／**[!UICONTROL フォームとドキュメント]**&#x200B;に移動します。
1. 「**[!UICONTROL 作成]**」をタップして、「**[!UICONTROL アダプティブフォーム]**」を選択します。テンプレートのリストが表示されます。テンプレートを選択して、「**[!UICONTROL 次へ]**」をタップします。
1. 「**[!UICONTROL 基本]**」タブで次の操作を行います。

   1. アダプティブフォームの&#x200B;**名前**&#x200B;と&#x200B;**タイトル**&#x200B;を指定します。
   1. を選択します。 [設定コンテナ](/help/forms/using/adobe-sign-integration-adaptive-forms.md#configure-adobe-sign-with-aem-forms) AEM Formsと連携するAcrobat Signの設定時に作成されました。

      >[!NOTE]
      >
      >この **[!UICONTROL Acrobat SignCloud Service]** ドロップダウンリストには、このフィールドで選択した設定コンテナで設定されたクラウドサービスが表示されます。 この **[!UICONTROL Acrobat SignCloud Service]** ドロップダウンリストは **[!UICONTROL 電子署名]** 」セクションを使用して、 **[!UICONTROL Acrobat Signを有効にする]** オプション。

1. 「**[!UICONTROL フォームモデル]**」タブで、次のいずれかのオプションを選択します。

   * 「**[!UICONTROL フォームテンプレートをレコードのドキュメントテンプレートとして関連付ける]**」オプションを選択し、「レコードのドキュメント」テンプレートを選択します。フォームテンプレートベースのアダプティブフォームを使用する場合、署名用として送信されたドキュメントには、関連するフォームテンプレートに基づくフィールドだけが表示されます。表示されないアダプティブフォームのフィールドもあります。
   * 「**[!UICONTROL レコードのドキュメントを生成]**」オプションを選択します。「レコードのドキュメント」オプションが有効なアダプティブフォームを使用すると、署名用に送信されたドキュメントにアダプティブフォームのすべてのフィールドが表示されます。

1. 「**[!UICONTROL 作成」をタップします。]** 署名が有効なアダプティブフォームが作成され、Acrobat Signフィールドを追加する際に使用できます。

#### Acrobat Sign用アダプティブフォームの編集 {#editafsign}

既存のアダプティブフォームでAcrobat Signを使用するには、以下の手順を実行します。

1. **[!UICONTROL Adobe Experience Manager]**／**[!UICONTROL Forms]**／**[!UICONTROL フォームとドキュメント]**&#x200B;に移動します。
1. アダプティブフォームを選択し、**[!UICONTROL プロパティ]**&#x200B;をタップします。
1. 内 **[!UICONTROL 基本]** タブで、 [設定コンテナ](/help/forms/using/adobe-sign-integration-adaptive-forms.md#configure-adobe-sign-with-aem-forms) AEM Formsと連携するAcrobat Signの設定時に作成されました。
1. 「**[!UICONTROL フォームモデル]**」タブで、次のいずれかのオプションを選択します。

   * 「**[!UICONTROL フォームテンプレートをレコードのドキュメントテンプレートとして関連付ける]**」オプションを選択し、「レコードのドキュメント」テンプレートを選択します。フォームテンプレートベースのアダプティブフォームを使用する場合、署名用として送信されたドキュメントには、関連するフォームテンプレートに基づくフィールドだけが表示されます。表示されないアダプティブフォームのフィールドもあります。
   * 「**[!UICONTROL レコードのドキュメントを生成]**」オプションを選択します。「レコードのドキュメント」オプションが有効なアダプティブフォームを使用すると、署名用に送信されたドキュメントにアダプティブフォームのすべてのフィールドが表示されます。

1. 「**[!UICONTROL 保存して閉じる]**」をタップします。アダプティブフォームがAcrobat Signに対して有効になっている。

### Acrobat Signフィールドをアダプティブフォームに追加する {#addadobesignfieldstoanadaptiveform}

Acrobat Signは、アダプティブフォームに配置できる様々なフィールドを備えています。 これらのフィールドには、署名、イニシャル、会社名、タイトルなど、様々なタイプのデータを入力することができます。このため、署名が行われる際に署名だけでなく追加情報を収集できます。Acrobat Signブロックコンポーネントを使用すると、Acrobat Signフィールドをアダプティブフォーム内の様々な場所に配置できます。

アダプティブフォームにフィールドを追加し、それらのフィールドに関する各種のオプションをカスタマイズするには、以下の手順を実行します。

1. ドラッグ&amp;ドロップ **Acrobat Sign Block** コンポーネントを、コンポーネントブラウザーからアダプティブフォームに切り替えます。 Acrobat Signブロックコンポーネントには、サポートされるすべてのAcrobat Signフィールドが含まれています。 デフォルトでは、**署名**&#x200B;フィールドがアダプティブフォームに追加されます。

   ![署名ブロック](assets/sign-block.png)

   デフォルトでは、Acrobat Signブロックは公開済みのアダプティブフォームには表示されません。 Adobe Sign ブロックが表示されるのは、署名ドキュメントだけです。Acrobat Signブロックの表示は、Acrobat Signブロックコンポーネントのプロパティから変更できます。

   >[!NOTE]
   >
   >* Acrobat Signブロックの使用は、アダプティブフォームでAcrobat Signを使用する場合に必須ではありません。 Acrobat Signブロックを使用せずに署名者用のフィールドを追加した場合は、署名ドキュメントの下部にデフォルトの署名フィールドが表示されます。
   >* Acrobat Signブロックは、レコードのドキュメントを自動的に生成するアダプティブフォームに対してのみ使用してください。 レコードのドキュメントまたはフォームテンプレートベースのアダプティブフォームの生成にカスタム XDP を使用している場合、Acrobat Signブロックは不要です。


1. を選択します。 **Acrobat Sign Block** コンポーネントをタップし、 **編集** ![aem_6_3_edit](assets/aem_6_3_edit.png) アイコン フィールドを追加するためのオプションと、フィールドの外観を設定するためのオプションが表示されます。

   ![adobe-sign-block-select-fields](assets/adobe-sign-block-select-fields.png)

   **A.** Acrobat Signフィールドを選択して追加します。 **B.** Acrobat Signブロックを全画面表示に展開します。

1. 次をタップします。 **Acrobat Sign Field** ![aem_6_3_adobesign](assets/aem_6_3_adobesign.png) アイコン Acrobat Signフィールドを選択および追加するオプションが表示されます。

   を展開します。 **タイプ** ドロップダウンフィールドでAcrobat Signフィールドを選択し、「完了」をタップします。 ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png) アイコンをクリックして、選択したフィールドをAcrobat Signブロックに追加します。 「**タイプ**」ドロップダウンフィールドには、「署名」タイプ、「署名者の情報」タイプ、「データフィールド」タイプが表示されます。Acrobat SignとAEM Formsの統合は、タイプドロップダウンボックスに表示される唯一のサポートフィールドです。 Acrobat Signフィールドについて詳しくは、 [Acrobat Signドキュメント](https://helpx.adobe.com/jp/sign/using/field-types.html).

   ![adobe-sign-block-fields-options](assets/adobe-sign-block-fields-options.png)

   フィールドには、必ず一意の名前を指定する必要があります。フィールドを必須フィールドとしてマークするための必須オプションを選択することもできます。また、 **名前** および **必須** オプションを選択すると、一部のAcrobat Signフィールドには、さらに多くのオプションがあります。 例えば、マスクや複数行のオプションなどです。また、各Acrobat Signフィールドには、同じAcrobat Signブロック内に存在するか異なるブロック内に存在するかに関わらず、一意の名前を指定します。

### アダプティブフォームのAcrobat Signの有効化 {#enableadobsignforanadaptiveform}

デフォルトでは、Acrobat Signはアダプティブフォームに対して有効になっていません。 Adobe Sign を有効にするには、以下の手順を実行します。

1. コンテンツブラウザーで「**フォームコンテナ**」をタップし、**設定**&#x200B;アイコン（![設定](assets/configure.png)）をタップします。この操作により、アダプティブフォームのコンテナプロパティを表示するプロパティブラウザーが開きます。
1. プロパティブラウザーで、を展開します。 **電子署名** アコーディオンで、 **Acrobat Signを有効にする** オプション。 これにより、アダプティブフォームでAcrobat Signが有効になります。

### Acrobat SignCloud Serviceと署名順序を選択 {#selectadobesigncloudserviceforanadaptiveform}

AEM Formsの 1 つのインスタンスに対して複数のAcrobat Signサービスを設定できます。 人事や財務などの部門ごとに個別のサービスセットを設定することをお勧めします。こうすることにより、署名済みドキュメントの追跡とレポート処理が容易になります。例えば、銀行には複数の部署があります。これらの部署ごとに個別の設定を指定することで、ドキュメントを正しくトラッキングできるようになります。

また、1 つのドキュメントに対して複数の署名者を設定できます。例えば、複数のユーザーがクレジットカードを申し込む場合があります。銀行は、これらの申し込みの処理を開始する前に、すべての申請者の署名を取得する必要があります。このように複数の署名者を処理するシナリオの場合、各ドキュメントを順に署名することも、順不同で同時に署名することもできます。

クラウドサービスと署名順を選択するには、以下の手順を実行します。

![クラウドサービス](assets/cloud-service.png)

1. コンテンツブラウザーで「**フォームコンテナ**」をタップし、**設定**&#x200B;アイコン（![設定](assets/configure.png)）をタップします。この操作により、アダプティブフォームのコンテナプロパティを表示するプロパティブラウザーが開きます。
1. プロパティブラウザーで、を展開します。 **電子署名** アコーディオンで、 **Acrobat Signを有効にする** オプション。 これにより、アダプティブフォームでAcrobat Signが有効になります。
1. 既に設定済みのAcrobat SignCloud Servicesのリストからクラウドサービスを選択します。

   この **Acrobat SignCloud Service** リストが空です。 [AEM FormsとのAcrobat Signの設定](/help/forms/using/adobe-sign-integration-adaptive-forms.md) サービスを設定する記事です。

   ドロップダウンには、 `global` ツール/のフォルダー **[!UICONTROL Cloud Services]** > **[!UICONTROL Acrobat Sign]**. また、このドロップダウンには、アダプティブフォームの作成時に「**[!UICONTROL 設定コンテナ]**」フィールドで選択したフォルダーに存在するクラウドサービスも表示されます。

1. 「**署名者は署名できます**」ダイアログボックスで、署名順序を選択します。Acrobat Signの歌手はアダプティブフォームに署名できます **連続**  — 別の署名者の後に続く、または **同時**  — 順不同。

   順に署名する場合は、1 人の署名者が、署名用のフォームを一度に 1 つずつ受け取ります。最初の署名者によるフォームの署名が完了すると、フォームが次の署名者に送信され、最後の署名者になるまでこの手順が繰り返されます。

   同時に署名する場合は、複数の署名者がフォームを同時に署名することができます。

1. [アダプティブフォームに署名者を追加する](#addsignerstoanadaptiveform) 「完了」アイコンをタップして、変更を保存します。

### アダプティブフォームに署名者を追加する {#addsignerstoanadaptiveform}

1 つのアダプティブフォームに対して、署名者を 1 人だけ設定することも、複数の署名者を設定することもできます。署名者を追加する際に、その署名者の詳細な認証情報を設定することもできます。また、フォームの入力者と署名者を同じユーザーにするかどうかを選択することもできます。署名者に関する各種の詳細情報の追加と指定を行うには、以下の手順を実行します。

1. コンテンツブラウザーで「**フォームコンテナ**」をタップし、**設定** ![設定](assets/configure.png) アイコンをタップします。この操作により、アダプティブフォームのコンテナプロパティを表示するプロパティブラウザーが開きます。
1. プロパティブラウザーで、を展開します。 **電子署名** アコーディオンで、 **Acrobat Signを有効にする** オプション。 これにより、アダプティブフォームでAcrobat Signが有効になります。
1. 「**署名者設定」で「**&#x200B;署名者を追加&#x200B;**」をタップします。**&#x200B;アダプティブフォームに署名者が追加されます。1 つのアダプティブフォームに複数のAcrobat Sign署名者を追加することができます。
1. ![phone-details](assets/phone-details.png)

   「**編集** ![aem_6_3_edit](assets/aem_6_3_edit.png)」アイコンをクリックして、署名者に関する以下の情報を指定します。

   * **タイトル：** 署名者を一意に識別するタイトルを指定します。
   * **署名者とフォームの入力者は同じですか？:** 選択 **はい**&#x200B;フォームの入力者と最初の署名者が同じ人物の場合は、 このオプションを「**いいえ**」に設定した場合は、アダプティブフォームの署名ステップコンポーネントは使用しないでください。フォームに署名ステップコンポーネントが含まれている場合は、このフィールドの値が自動的に「はい」に設定されます。
   * **署名者の電子メールアドレス：**&#x200B;署名者の電子メールアドレスを指定します。署名者は、ここで指定した電子メールアドレスで、署名する必要があるドキュメントやフォームを受信します。フォームフィールドで指定した電子メールアドレスを使用することも、ログインユーザーの AEM ユーザープロファイルで指定した電子メールアドレスを使用することも、電子メールアドレスを手動で入力することもできます。このステップは、必ず実行する必要があります。また、署名者を 1 人だけ設定した場合は、署名者の電子メールアドレスが、AEM クラウドサービスの設定に使用するAcrobat Signアカウントと同一でないことを確認してください。
   * **署名者の認証方法：**&#x200B;署名するフォームを開く前にユーザーを認証する方法を指定します。電話による認証、ナレッジベースによる認証、ソーシャル ID に基づく認証のいずれかを選択することができます。

   >[!NOTE]
   >
   >* ソーシャル ID に基づく認証の場合、Facebook、Google、LinkedIn を使用した認証オプションがデフォルトで用意されています。Acrobat Signサポートに連絡して、他のソーシャル認証プロバイダーを有効にすることができます。


   * **入力または署名するAcrobat Signフィールド：** 署名者用のAcrobat Signフィールドを選択します。 アダプティブフォームには複数のAcrobat Signフィールドを含めることができます。 署名者用に特定のフィールドを有効にできます。「 」フィールドに、使用可能なすべてのAcrobat Signブロックが表示されます。 いずれかのブロックを選択すると、そのブロックのすべてのフィールドが選択されます。フィールドの選択を解除するには、「X」アイコンを使用します。

   ![signer-details-1](assets/signer-details-1.png)

   上記の画像には、2 つのAcrobat Signブロックの例が含まれています。個人情報とオフィスの詳細

   「完了 ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png)」アイコンをタップします。署名者が追加され、設定が完了します。

### アダプティブフォームに対して送信アクションを選択する {#selectsubmitactionforanadaptiveform}

次に、Acrobat Signフィールドをアダプティブフォームに追加し、フォームコンテナからAcrobat Signを有効にして、「Acrobat SignCloud Service」を選択し、Acrobat Sign署名者を追加して、アダプティブフォームに適した送信アクションを選択します。 アダプティブフォームの送信アクションについて詳しくは、[送信アクションの設定](/help/forms/using/configuring-submit-actions.md)を参照してください。

また、Acrobat Sign対応のアダプティブフォームは、すべての署名者がフォームに署名した後でのみ送信されます。 一部の署名者しか署名していないフォームは、フォームポータルの「保留中の署名」セクションで表示されます。Acrobat Sign Configuration Service は、次の場所でAcrobat Signサーバーのポーリングを続けます： [一定の間隔](/help/forms/using/adobe-sign-integration-adaptive-forms.md) 署名のステータスを検証する場合。 すべての署名者がフォームの署名を完了すると、送信アクションサービスが起動してフォームが送信されます。カスタムの送信アクションを使用していて、フォームでAcrobat Signを使用している場合は、送信アクションサービスを使用するようにカスタムの送信アクションを更新します。

>[!NOTE]
>
>アダプティブフォームのデータは、一時的にフォームポータルに保存されます。次を使用することをお勧めします。 [Forms Portal のカスタムストレージ](/help/forms/using/configuring-draft-submission-storage.md). これにより、PII（Personally Identifiable Information：個人を特定できる情報）データが AEM サーバーに保存されるのを防ぐことができます。

これで、フォームに署名するための準備が整いました。フォームのプレビューを表示して、署名の方法を確認することができます。発行されたフォームでは、署名者が電子メールで署名用のフォームを受け取ると、Acrobat Signブロックフィールドが表示されます。 この動作を、フォーム外署名機能といいます。最初の署名者に対して、フォーム内署名機能を設定することもできます。詳しい手順については、「[フォーム内署名機能の設定](/help/forms/using/working-with-adobe-sign.md#create-in-form-signing-experience)」を参照してください。

## アダプティブフォームのクラウド署名の設定 {#configure-cloud-signatures-for-an-adaptive-form}

クラウドベースのデジタル署名（リモート署名）は、デスクトップ、モバイル、web 上で機能する新世代のデジタル署名で、署名者の認証に関する最高レベルのコンプライアンスと保証を満たします。クラウドベースのデジタル署名を使用してアダプティブフォームに署名できます。

後 [Acrobat Signのアダプティブフォームプロパティの編集](#enableadobesign)アダプティブフォームにクラウド署名フィールドを追加するには、以下の手順を実行します。

1. ドラッグ&amp;ドロップ **Acrobat Sign Block** コンポーネントを、コンポーネントブラウザーからアダプティブフォームに切り替えます。 Acrobat Signブロックコンポーネントには、サポートされるすべてのAcrobat Signフィールドが含まれています。 デフォルトでは、**署名**&#x200B;フィールドがアダプティブフォームに追加されます。

   ![署名ブロック](assets/sign-block.png)

1. を選択します。 **Acrobat Sign Block** コンポーネントをタップし、 **編集** ![aem_6_3_edit](assets/aem_6_3_edit.png) アイコン フィールドを追加するためのオプションと、フィールドの外観を設定するためのオプションが表示されます。

   ![adobe-sign-block-select-fields](assets/adobe-sign-block-select-fields.png)

   **A.** Acrobat Signフィールドを選択して追加します。 **B.** Acrobat Signブロックを全画面表示に展開します。

1. 次をタップします。 **Acrobat Sign Field** ![aem_6_3_adobesign](assets/aem_6_3_adobesign.png) アイコン Acrobat Signフィールドを選択および追加するオプションが表示されます。

   を展開します。 **タイプ** 選択するドロップダウンフィールド **電子署名** 「完了」をタップします。 ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png) アイコンをクリックして、選択したフィールドをAcrobat Signブロックに追加します。

   ![digital_signatures](assets/digital_signatures.png)

   フィールドには、必ず一意の名前を指定する必要があります。

   次を使用して、アダプティブフォームにデジタル署名を適用します。

   * クラウド署名：トラストサービスプロバイダーがホストする[デジタル ID](https://helpx.adobe.com/jp/sign/kb/digital-certificate-providers.html) を使用して署名します。
   * Adobe Acrobat または Reader：ドキュメントをダウンロードして Adobe Acrobat または Reader で開き、スマートカード、USB トークン、ファイルベースのデジタル ID を使用して署名します。

   クラウド署名フィールドをアダプティブフォームに追加した後、次の手順を実行して設定プロセスを完了します。

   * [アダプティブフォームのAcrobat Signの有効化](#enableadobsignforanadaptiveform)
   * [アダプティブフォームのAcrobat SignCloud Serviceを選択](#selectadobesigncloudserviceforanadaptiveform)
   * [Acrobat Sign署名者をアダプティブフォームに追加する](#addsignerstoanadaptiveform)
   * [アダプティブフォームに対して送信アクションを選択する](#selectsubmitactionforanadaptiveform)


## フォーム内署名機能の設定 {#create-in-form-signing-experience}

フォームの入力時に、アダプティブフォームに署名することもできます。この動作を、フォーム内署名機能といいます。フォーム内署名機能は、複数の署名者が存在する場合に、最初の署名者のみ使用することができます。アダプティブフォームに対してフォーム内署名機能を設定するには、以下の手順を実行します。

1. [署名ステップコンポーネントの追加と設定](#add-and-configure-the-signature-step-component)を行います。
1. [概要ステップコンポーネントを追加](#configure-the-thank-you-page-or-summary-step-component)します。

![in-form-signing-experience](assets/in-form-signing-experience.png)

### 署名ステップコンポーネントの追加と設定 {#add-and-configure-the-signature-step-component}

署名ステップコンポーネントを使用して、入力済みのフォームに電子的に署名するための領域を指定します。署名ステップコンポーネントが含まれているセクションをレンダリングすると、入力済みフォームの署名可能な PDF バージョンが表示されます。署名ステップコンポーネントは、フォームの幅いっぱいに表示されます。そのため、署名ステップコンポーネントが含まれているセクションに他のコンポーネントを配置しないようにすることをお勧めします。

署名ステップコンポーネントを設定するには、以下の手順を実行します。

1. **署名ステップ**&#x200B;コンポーネントを、コンポーネントブラウザーからフォームにドラッグアンドドロップします。
1. 新しく追加された署名ステップコンポーネントを選択し、「**設定** ![configure](assets/configure.png)」アイコンをタップします。この操作により、署名ステップのプロパティを表示するプロパティブラウザーが開きます。以下のプロパティを設定します。

   * **要素名：**&#x200B;コンポーネントの名前を指定します。
   * **タイトル：**&#x200B;コンポーネントの一意のタイトルを指定します。
   * **テンプレートメッセージ：** 署名 PDF の読み込み中に表示するメッセージを指定します。Acrobat Signサービスでは、署名PDFの準備と読み込みに時間がかかります。
   * **署名サービス：** を選択します。 **Acrobat Sign** オプション。
   * **レガシーの E-Sign コンポーネントを使用**：[AEM Forms Workspace](/help/forms/using/introduction-html-workspace.md) または AEM Forms アプリケーションで個別のアダプティブフォームを使用する場合や、ベースとなるアダプティブフォームにレガシーの E-Sign コンポーネントが含まれている場合は、「**レガシーの E-Sign コンポーネントを使用**」オプションを選択します。
   * **設定**:設定を選択します (Acrobat SignCloud Service)。 このドロップダウンボックスを使用できるのは、「**レガシーの E-Sign コンポーネントを使用**」オプションが有効になっている場合だけです。

   完了（![aem_6_3_forms_save](assets/aem_6_3_forms_save.png)）アイコンをタップして、変更を保存します。

   ![signature-step](assets/signature-step.png)

   >[!NOTE]
   >
   >* **[!UICONTROL 署名者ステップ]**&#x200B;コンポーネントをフォームにドラッグアンドドロップすると、「**[!UICONTROL 署名者とフォーム記入者は同一ですか？]**」オプションが自動的に「**はい**」に設定されます。フォームを正しく機能させるには、このオプションが設定されている必要があります。
   >* Acrobat Sign対応のアダプティブフォームでは、署名ステップコンポーネントを使用したセクションまたはパネルの「送信」ボタンの使用はサポートされていません。 手動送信の署名ステップの後、または [Acrobat Sign Configuration Service](/help/forms/using/adobe-sign-integration-adaptive-forms.md#configure-adobe-sign-scheduler-to-sync-the-signing-status).


### 「ありがとうございます」ページまたは概要ステップコンポーネントの設定  {#configure-the-thank-you-page-or-summary-step-component}

**概要ステップ**&#x200B;コンポーネントにより、フォームが自動的に送信され、カスタマイズ後の概要ページに情報が取り込まれ、送信されたフォームの概要情報が表示されます。また、リターンマップ内の必須情報も取得されます。概要ステップコンポーネントは、フォームの幅いっぱいに表示されます。そのため、概要ステップコンポーネントが含まれているセクションに他のコンポーネントを配置しないようにすることをお勧めします。

これで、フォーム内署名機能を使用するための準備が整いました。フォームのプレビューを表示して、署名の方法を確認することができます。

## よくある質問  {#frequently-asked-questions}

**Q：特定のアダプティブフォームを別のアダプティブフォームに埋め込むことができますが、埋め込まれたアダプティブフォームでAcrobat Signを有効にできますか？**

**回答：** いいえ。AEM Formsは、Acrobat Sign対応のアダプティブフォームを埋め込んだアダプティブフォームの署名に使用することはできません。

**Q:高度なテンプレートを使用してアダプティブフォームを作成し、編集用に開くと、「電子署名または署名者が正しく設定されていません」というエラーメッセージが表示されます。 表示されます。このエラーメッセージを解決するにはどうすればよいですか？**

**回答：** 高度なテンプレートを使用して作成されたアダプティブフォームは、Acrobat Signを使用するように設定されます。 このエラーを解決するには、Acrobat Signクラウド設定を作成して選択し、アダプティブフォームのAcrobat Sign署名者を設定します。

**Q:アダプティブフォームの静的テキストコンポーネントでAcrobat Signのテキストタグを使用することはできますか？**

**回答：** はい、テキストコンポーネントでテキストタグを使用して、Acrobat Signフィールドを [レコードのドキュメント](/help/forms/using/generate-document-of-record-for-non-xfa-based-adaptive-forms.md) （「レコードのドキュメントの自動生成」オプションのみ）アダプティブフォームが有効になっています。 テキストタグを作成する手順とルールについては、 [Acrobat Sign Documentation](https://experienceleague.adobe.com/docs/document-cloud-learn/sign-learning-hub/admin-set-up/advanced-tasks-admins/adobe-sign-text-tagging.html). アダプティブフォームでは、テキストタグを使用する場合に制限があることにも注意してください。テキストタグを使用して、Acrobat Sign Block がサポートするフィールドのみを作成できます。

**Q:AEM Formsには、Acrobat Signブロックと署名ステップの両方のコンポーネントが用意されています。 アダプティブフォームで両方を同時に使用することはできますか？**

**A：**&#x200B;はい。フォーム内で両方のコンポーネントを同時に使用することができます。これらのコンポーネントを使用する場合は、以下の推奨事項を参照してください。

**Acrobat Signブロック：** Acrobat Signブロックを使用すると、アダプティブフォームの任意の場所にAcrobat Signフィールドを追加できます。 また、特定のフィールドを署名者に割り当てることもできます。アダプティブフォームがプレビューまたはパブリッシュされたAcrobat Signブロックがデフォルトで表示されていない場合。 これらのブロックは、署名ドキュメント内でのみ使用することができます。署名ドキュメント内では、署名者に割り当てられているフィールド以外は使用できません。Acrobat Signブロックは、最初の署名者および後続の署名者と共に使用できます。

**署名ステップコンポーネント：**&#x200B;署名ステップコンポーネントを使用すると、フォーム内署名機能を設定することができます。この機能では、最初の署名者のみ、フォームの入力時に署名を行うことができます。署名ステップコンポーネントが含まれているセクションをレンダリングすると、フォームの署名可能な PDF バージョンが表示されます。これは通常、最後のセクションか、最後から 2 番目のセクションになります。このセクションの後に、フォームの概要コンポーネントが表示されます。
