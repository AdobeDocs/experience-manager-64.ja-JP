---
title: Forms の場所の設定
seo-title: Configuring locations for Forms
description: Forms の場所の設定方法について説明します。
seo-description: Learn how to configure location for Forms.
uuid: ba35888b-492c-4678-890b-160b53e7d659
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_forms
products: SG_EXPERIENCEMANAGER/6.4/FORMS
discoiquuid: 3d2b7cfb-228c-4cc2-8fcd-d500f0010010
exl-id: 283ef073-b71d-4b48-882f-15f05581c1de
source-git-commit: bd94d3949f0117aa3e1c9f0e84f7293a5d6b03b4
workflow-type: tm+mt
source-wordcount: '804'
ht-degree: 77%

---

# Forms の場所の設定 {#configuring-locations-for-forms}

Web ルート、検索対象フォームの場所、PDFForm 変換で使用するシード PDF ファイル、キャッシュの場所などの属性の URL、URI およびファイルの場所を指定できます。

1. 管理コンソールで、サービス／Forms をクリックします。
1. 「場所」で、適切なオプションを指定します。オプションについては後述します。
1. 「保存」をクリックします。

## 場所の設定 {#locations-settings}

**ベース URL :** 画像やスクリプトなどのフォームリソースが配置されるベース URL。 HTML 変換に画像やスクリプトなどの外部依存の HREF 参照が含まれている場合は、この値が必須となります。このようなスクリプトの 1 つに xfasubset.js があります。xfasubset.js は HTML フォームで XFA インテリジェンスを実行するのに必要です。この値は HTTP 形式のコンテンツルート URI である必要があります。

>[!NOTE]
>
>Base URL では HTTP プロトコルまたはリポジトリプロトコルのみがサポートされています。file:/// のようなプロトコルはサポートされていません。カスタム CSS またはデジタル署名 URI などのリソースにアクセスする必要がある場合は、適切な API パラメーターの値を使用して絶対位置を指定します。

依存パスが絶対パスのとき、ベース URL 値は無視されます。それ以外の場合、依存パスはベース URL と連結されます。

デフォルト値は空の文字列です。

次の例は、（コンテンツルート URI とベース URL を使用して）同じコンテンツを指しています。

`(ContentRootURI)/subdir/image1.jpg`

`(BaseURL)/subdir/image1.jpg`

**FS Web ルート URI:** Forms Web アプリケーションの URL。 Forms Web アプリケーションとクライアントアプリケーションを同じアプリケーションサーバーにデプロイする場合は、このボックスを空白のままにしておくことができます。その場合は Forms API Web ルート URL が使用されます。

Forms Web アプリケーションとクライアントアプリケーションを同じアプリケーションサーバーにデプロイしない場合は、次の例に示すように、このボックスに Forms Web アプリケーションの URL を入力する必要があります。

`https://<host name>:<port>/FormServer`

`host name` と `port` には、それぞれ Forms Web アプリケーションをホストするサーバーのサーバー名とポート番号を入力します。

デフォルト値は空の文字列です。

**Web ルート URI:** アプリケーションの Web ルート。 この値と、AEM Forms SDK を介して指定された sTargetURL パラメーターを連結して（sTargetURL が相対 URL の場合）、アプリケーション固有の Web コンテンツにアクセスするための絶対 URL が作成されます。

デフォルト値は空の文字列です。

**コンテンツルート URI:** フォームの取得元の URI または絶対位置です。 この値と、API 経由で指定された sFormQuery パラメーターを連結して、フォームの取得先である絶対パスが作られます。この値で参照できるのは、特定のディレクトリか、HTTP でアクセス可能な Web 上の場所です。

デフォルト値は空の文字列です。

**XCI 設定 URI:** レンダリングに使用される XCI ファイルが見つかる相対的または絶対的な場所です。 相対パスの場合は、デプロイ可能な AEM Forms EAR ファイル内に XCI ファイルが保存されていることが前提となります。

デフォルト値は `com/adobe/formServer/PA/pa.xci` です。

**フォントマップ URI:** フォントマッピングファイルの相対位置または絶対位置です。 相対パスの場合は、デプロイ可能な AEM Forms EAR ファイル内にこのファイルが保存されていることが前提となります。

フォントマップファイルによってフォーム内に HTML 変換のためのカスタムフォントマップが作成されます。こうすると、クライアントコンピューターに存在しないフォントを別のフォントに置き換えるように指定することができます。

デフォルト値は `com/adobe/formServer/client-font-map.properties` です。

次のエントリは、フォントマップファイル内のエントリの例です。

`Arial=Arial,Helvetica,sans-serif`

**シードPDFファイル：** 配信を最適化するために PDFForm 変換で使用される最初のPDFファイルです。 シード PDF ファイルで指定する特別な PDF ファイル（XFA ストリーム、画像およびフォントリソースのみを含む）にフォームのデザインとデータが付加されます。このフォームは Acrobat バージョン 7 以降でレンダリングされ、PDFForm 変換に適用されます。

デフォルト値は空の文字列です。

**キャッシュの場所：** Formsディスクキャッシュの場所を指定します。 この設定を変更すると、現在の場所の既存のキャッシュ情報すべてがリセットされ、新しいキャッシュが新しい場所に作成されます。次のいずれかのオプションを選択します。

**デフォルトの場所：** これはデフォルトの選択です。 このオプションを選択すると、次のように使用しているアプリケーションサーバーによって決まる場所にキャッシュが作成されます。

* **JBoss:** [JBoss ホーム]\server\[install type]\svcdata\FormServer\Cache
* **WebLogic:** [WebLogic ホーム]\user_projects\domains\[aem-forms ドメイン名 ]\adobe\[forms サーバー名 ]\FormServer\Cache
* **WebSphere:** [IBMホーム]\WebSphere\AppServer\installedApps\adobe\server1\FormServer\Cache

**LC 一時ディレクトリ：** キャッシュは、AEM forms 一時ディレクトリのサブディレクトリに作成されます。このサブディレクトリは、管理コンソールの設定/コアシステム設定/設定/一時ディレクトリの場所で指定されます。 サブディレクトリの名前は adobeform_です。[servername].

>[!NOTE]
>
>一時クリーニングユーティリティを使用している場合、これらのディレクトリを削除しても機能に影響を与えませんが、新しいキャッシュが作成されるまで、短期間パフォーマンスが大きく低下する可能性があります。このような問題を回避するには、AEM Forms 一時ディレクトリの消去中、これらのディレクトリを削除しないでください。
