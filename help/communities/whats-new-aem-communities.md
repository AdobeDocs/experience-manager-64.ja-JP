---
title: AEM 6.4 Communities の新機能
description: AEM Communitiesは、企業がパートナー、顧客、従業員間で共同作業するためのフレームワークを提供します。
uuid: e4bf343c-59cd-48ac-bee4-85db109e4c65
contentOwner: mgulati
discoiquuid: 3e3c867f-afb0-4402-94f4-16e1a556ddee
exl-id: fcdc65c9-929d-4a87-8ff7-5e3cf5711fd9
source-git-commit: c5b816d74c6f02f85476d16868844f39b4c47996
workflow-type: tm+mt
source-wordcount: '1076'
ht-degree: 0%

---

# AEM 6.4 Communities の新機能 {#what-s-new-in-aem-communities}

>[!CAUTION]
>
>AEM 6.4 の拡張サポートは終了し、このドキュメントは更新されなくなりました。 詳細は、 [技術サポート期間](https://helpx.adobe.com/jp/support/programs/eol-matrix.html). サポートされているバージョンを見つける [ここ](https://experienceleague.adobe.com/docs/?lang=ja).

AEM Communitiesは、企業がパートナー、顧客、従業員間で共同作業するためのフレームワークを提供します。 Web サイトの構造にソーシャル機能を提供し、企業がステークホルダーに知識を提供し、ブランド価値の向上に役立てるのを支援します。

AEM 6.4 Communities は、コミュニティユーザーのエクスペリエンスを強化し、コミュニティ管理者、モデレーターおよびマネージャーの日常業務を容易にする機能を提供します。

新機能と機能強化の概要については、こちらを参照してください。 また、 AEM 6.4 Communities も参照してください。 [リリースノート](../release-notes/communities-release-notes.md). AEM 6.4 Communities ドキュメントについては、 [AEM 6.4 Communities ユーザーガイド](home.md).

## サブコミュニティまたはコミュニティグループの管理 {#managing-sub-communities-or-community-groups}

AEM Communitiesを使用すると、コミュニティ管理者は、事前に定義されたテンプレートを使用して、オーサー環境でコミュニティサイト内にグループとサブグループを作成できます。 これらのグループはサブコミュニティとして機能し、親サイトからテーマやスタイルなど、多くの設定を継承できます。 ただし、これらのグループは親サイトとは異なる場合があります。例えば、異なるグループモデレーターのセットを持つ場合や、セキュリティレベルが異なる場合があります。 これらのグループは、独立した完全なミニコミュニティとして機能し、以下の機能強化によりさらに活用されます。

### 複数ロケールのグループを 1 つの手順で作成 {#create-multi-locale-groups-in-single-step}

コミュニティサイトの一部として、複数言語のグループを 1 回の操作で作成できます。 **[!UICONTROL 追加の利用可能なコミュニティグループの言語]** ～に入る **[!UICONTROL コミュニティグループテンプレート]** ページ（作成時に使用可能） [新しいコミュニティグループ](groups.md) コミュニティサイト内では、がこれを可能にします。

![multilingualgroup-1](assets/multilingualgroup-1.png)

このようなグループを作成するには、サイトコンソールから目的のコミュニティサイトのグループコレクションに簡単に移動します。 グループを作成し、 **[!UICONTROL 追加の利用可能なコミュニティグループの言語]** ～の分野 **[!UICONTROL コミュニティグループテンプレート]** ページ。

### グループコンソールからコミュニティグループを削除 {#delete-community-groups-from-groups-console}

AEM 6.4 Communities では、コミュニティサイトコンソール内のコミュニティグループコレクションに、既存のコミュニティグループに対してグループを削除アイコンが表示されます。 これにより、 [グループの削除](groups.md#deleting-the-group) 1 回のクリックで、グループに関連付けられたすべての項目（コンテンツやユーザーのメンバーシップなど）の削除に加えて、

![deletegrp](assets/deletegrp.png)

### グループ内でイネーブルメントリソースを作成し、割り当てます {#create-and-assign-enablement-resources-within-groups}

ターゲットコミュニティメンバーの特定のセットに対して、学習コンテンツを作成、管理、公開できるようになりました。 コミュニティグループ（コミュニティサイト全体だけでなく）のカタログ機能や割り当て機能が利用できるため、イネーブルメントマネージャは次のことが可能です。 [イネーブルメントリソースの割り当て](resource.md) 小さな人々の集まりへの道を学ぶのも

![assignmentcatalog](assets/assignmentcatalog.png)

## ユーザー生成コンテンツのモデレート {#moderating-user-generated-content}

AEM 6.4 Communities ではモデレーションに対していくつかの改善が行われています。モデレーターは、コミュニティモデレーターの日常生活を緩和するのに役立ちます。

### 自動スパム検出  {#automatic-spam-detection}

新しいスパム検出エンジンにより、コミュニティサイトやグループ上で望ましくない、迷惑なユーザー生成コンテンツを除外することができます。 有効にすると、この機能は、事前に定義された一連のスパムワードに基づいて、ユーザー生成コンテンツの一部をスパムまたは非スパムとしてマークできます。 モデレーターは、コンテンツに対してさらに操作して、パブリッシュインスタンスでの表示を拒否または許可できます。 これらのモデレート操作は、インラインまたは一括モデレートコンソールを通じて実行できます。

![spamdetection-1](assets/spamdetection-1.png)

[スパム検出](moderate-ugc.md#spam-detection) 90%の精度で特定のユーザー生成コンテンツを検索し、フラグを設定します。 ただし、この機能はデフォルトでは有効になっていません。 この機能を有効にするには、コミュニティ管理者が system/console の configMgr に移動し、スパムプロセスを追加する必要があります。

![spamprocess-1](assets/spamprocess-1.png)

### Q&amp;A 用の新しい（回答済み/未回答）フィルター {#new-answered-unanswered-filters-for-qna}

AEM 6.4 では、2 つの [新しいフィルター](moderation.md#filter-rail)Q&amp;A の質問に対して「回答済み」および「未回答」という名前が付けられ、一括モデレートコンソールに追加されました。 これらのフィルターは、フィルターレールの「ステータス」の下に表示されます。

![ステータス](assets/statuses.png)

「回答済み」ステータスを選択すると、回答済みのすべての質問がコンテンツ領域のモデレーターに表示されます。 一方、「未回答」ステータスのみが選択されている場合は、回答済みの質問以外のすべてのコンテンツ（すべてのコンテンツタイプ）がモデレーターに表示されます。未回答の質問やフォーラムトピック、ブログ記事、コメントなどのコンテンツは回答済みの質問には存在しません。

### ブックマークモデレートフィルター {#bookmark-moderation-filters}

AEM Communitiesは [事前定義済みのモデレートフィルターをブックマークに追加する](moderation.md#filter-rail) モデレートコンソールで これらの保存済みのブックマークは、後で再訪問したり、他のユーザーと共有したりできます。

ユーザーは、モデレートコンソールのフィルターレールから目的のフィルターを選択して、フィルターされた UGC を表示し、ブラウザーでフィルターをブックマークするだけです。 これらのフィルターは URL 文字列の末尾に追加されるので、後で共有、再利用、再訪問できます。

## コミュニティサイトの管理 {#managing-community-sites}

AEM 6.4 Communities ではサイト管理機能が強化され、異なる言語の多数のコミュニティサイトをサイト管理者が簡単に作成、管理、削除できるようになりました。

### 1 つの手順で複数のロケールのコミュニティサイトを作成 {#create-multi-locale-community-sites-in-one-step}

AEM Communitiesでは [多言語コミュニティサイト](create-site.md) 単一の操作で これは、で複数の言語から選択できるので可能です **[!UICONTROL コミュニティサイトの基本言語]** ～に入る **[!UICONTROL サイトテンプレート]** ページを開きます。

![multilocalesite](assets/multilocalesite.png)

ユーザーは、これらのすべてのサイトに対して、設定フォルダー、ブランディング、その他多数の設定を一度に選択できます。

### サイトコンソールからコミュニティサイトを削除 {#delete-community-sites-from-sites-console}

AEM 6.4 Communities では、コミュニティサイトコンソールの既存のコミュニティサイトにサイトを削除アイコンが表示されます。 これにより、 [サイトの削除](create-site.md) 関連する項目をワンクリックで表示できます。

![siteactions](assets/siteactions.png)

## UGC とユーザープロファイルの管理 {#managing-ugc-and-user-profiles}

コミュニティエクスペリエンスの中心にユーザーデータ保護を維持するため、AEM Communitiesは [標準搭載の API](user-ugc-management-service.md) および [サンプルサーブレット](https://github.com/Adobe-Marketing-Cloud/aem-communities-ugc-migration/tree/main/bundles/communities-ugc-management-servlet). これらの API は、ユーザー生成コンテンツの一括管理（一括削除および一括書き出し）やユーザープロファイルの削除に役立ち、EU の GDPR 準拠リクエストの処理に役立ちます。

## 変更内容 {#what-s-changed}

* 新しいコミュニティサイトを作成する際に、Captcha の検証がAEM 6.4 Communities で標準で使用できなくなりました。 ただし、コミュニティサイトをカスタマイズして、 [Googleコンポーネント reCAPTCHA](https://helpx.adobe.com/experience-manager/using/aem_recaptcha.html) セキュリティの向上
* カスタム CSS をアップロードするオプションが、コミュニティサイトとグループのテーマから削除されました。
* 一括モデレート UI のフィルターレールにコンテンツのみおよび検索アイコンが追加されました。
* コンテンツパスフィルターが、一括モデレート UI のフィルターレールに追加されました。
* 一括モデレート UI から、一括モードに切り替え、一括モードを終了する機能が削除されました。 複数選択モードに入るには、選択 ( ![selecticon](assets/selecticon.png)) アイコンを投稿に表示します。投稿の上にマウスを置く（デスクトップ）か、投稿の上に指を押しながら（モバイル）表示します。
