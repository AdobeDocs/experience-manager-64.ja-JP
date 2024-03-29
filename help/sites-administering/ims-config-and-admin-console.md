---
title: AEM Managed Services に対する Adobe IMS 認証およびアドミンコンソールのサポート
seo-title: Adobe IMS Authentication and Admin Console Support for AEM Managed Services
description: AEMでのAdmin Consoleの使用方法を説明します。
seo-description: Learn how to use the Admin Console in AEM.
uuid: 3f5b32c7-cf62-41a4-be34-3f71bbf224eb
contentOwner: sarchiz
products: SG_EXPERIENCEMANAGER/6.4/SITES
topic-tags: Security
content-type: reference
discoiquuid: f6112dea-a1eb-4fd6-84fb-f098476deab7
exl-id: 38bbad03-aead-43d3-a28c-cc716955ddfb
source-git-commit: c5b816d74c6f02f85476d16868844f39b4c47996
workflow-type: tm+mt
source-wordcount: '1785'
ht-degree: 49%

---

# AEM Managed Services に対する Adobe IMS 認証およびアドミンコンソールのサポート {#adobe-ims-authentication-and-admin-console-support-for-aem-managed-services}

>[!CAUTION]
>
>AEM 6.4 の拡張サポートは終了し、このドキュメントは更新されなくなりました。 詳細は、 [技術サポート期間](https://helpx.adobe.com/jp/support/programs/eol-matrix.html). サポートされているバージョンを見つける [ここ](https://experienceleague.adobe.com/docs/?lang=ja).

>[!NOTE]
>
>この機能は、Adobe Managed Services のお客様にのみご利用いただけます。

## はじめに {#introduction}

AEM 6.4.3.0 では、AEMインスタンスと、Adobe IMS(Identity Management System) ベースの認証に対するAdmin Consoleサポートが、 **AEM Managed Services** 顧客。

Admin ConsoleのAEMオンボーディングにより、AEM Managed Servicesのお客様は、1 つのコンソールですべてのExperience Cloudユーザーを管理できます。 ユーザーとグループは AEM インスタンスに関連付けられている製品プロファイルに割り当てることができ、特定のインスタンスにログインできます。

## 主なハイライト {#key-highlights}

* AEM IMS 認証のサポートは、AEM 作成者、管理者または開発者に対してのみ有効で、サイト訪問者などの顧客サイトの外部エンドユーザーに対しては無効です
* このAdmin Consoleは、AEM Managed Servicesのお客様を IMS 組織として、およびそのインスタンスを製品コンテキストとして表します。 顧客システムおよび製品管理者は、インスタンスへのアクセスを管理できるようになります。
* AEM Managed Servicesは顧客トポロジをAdmin Consoleと同期します。 Admin Consoleには、インスタンスごとにAEM Managed Services製品コンテキストのインスタンスが 1 つ存在します。
* Admin Console内の製品プロファイルは、ユーザーがアクセスできるインスタンスを決定します
* お客様独自の SAML 2 準拠 ID プロバイダーを使用したフェデレーテッド認証がサポートされます
* 個人のAdobeID ではなく、Enterprise ID または Federated ID のみ（お客様のシングルサインオン用）がサポートされます。
* ユーザー管理 (Adobe Admin Console) は、引き続き顧客管理者が所有します。

## アーキテクチャ {#architecture}

IMS 認証は、AEMとAdobe IMSエンドポイントの間で OAuth プロトコルを使用して機能します。 ユーザーが IMS に追加され、Adobe ID を持つようになると、IMS 資格情報を使用して AEM Managed Services インスタンスにログインできます。

ユーザーログインフローを以下に示します。ユーザーは IMS にリダイレクトされ、必要に応じて SSO 検証のために顧客 IDP にリダイレクトされてから、AEMにリダイレクトされます。

![image2018-9-23_23-55-8](assets/image2018-9-23_23-55-8.png)

## 設定方法 {#how-to-set-up}

###  Admin Console への組織のオンボーディング {#onboarding-organizations-to-admin-console}

お客様がAdmin Consoleをオンボーディングすることは、AEM認証にAdobe IMSを使用するための前提条件です。

最初のステップとして、Adobe IMS に組織をプロビジョニングする必要があります。Adobeの企業のお客様は、 [Adobe Admin Console](https://helpx.adobe.com/jp/enterprise/using/admin-console.html).

AEM Managed Servicesのお客様は、既に組織がプロビジョニングされている必要があります。また、IMS プロビジョニングの一環として、Admin Consoleでカスタマーインスタンスを使用して、ユーザーの使用権限とアクセスを管理できます。

ユーザー認証のための IMS への移行は、AMS とお客様の共同作業となり、それぞれがワークフローを完了させます。

顧客が IMS 組織として存在し、AMS が顧客の IMS へのプロビジョニングを完了したら、次のような設定ワークフローを実行する必要があります。

![image2018-9-23_23-33-25](assets/image2018-9-23_23-33-25.png)

1. 指定されたシステム管理者が、Admin Consoleへのログインの招待を受け取ります
1. システム管理者がドメインを要求して、ドメイン（この例では acme.com）の所有権を確認します。
1. システム管理者はユーザーディレクトリを設定します
1. システム管理者は、SSO 設定用にAdmin Consoleで ID プロバイダ (IDP) を設定します。
1. AEM 管理者は、通常どおりローカルグループ、権限および特権を管理します。ユーザーとグループの同期を参照してください。

>[!NOTE]
>
>IDP 設定を含む、Adobe Identity Management Basics の詳細については、[このページ](https://helpx.adobe.com/jp/enterprise/using/set-up-identity.html)の記事を参照してください。
>
>エンタープライズ管理とAdmin Consoleの詳細については、この記事を参照してください [このページ](https://helpx.adobe.com/jp/enterprise/managing/user-guide.html).

### ユーザーのAdmin Consoleへのオンボーディング {#onboarding-users-to-the-admin-console}

ユーザーをオンボードする方法は、お客様の規模と好みに応じて 3 つあります。

1. Admin Console内でユーザーとグループを手動で作成
1. ユーザーを含む CSV ファイルのアップロード
1. お客様のエンタープライズ Active Directory からユーザーとグループを同期します。

#### Admin Console UI による手動追加 {#manual-addition-through-admin-console-ui}

ユーザーとグループは、Admin Console の UI で手動で作成できます。この方法は、管理するユーザー数が多くない場合に使用できます。 例えば、AEMユーザーが 50 人未満の場合、

また、Analytics、Target、Creative Cloudアプリケーションなど、他のAdobe製品の管理に既にこの方法を使用している場合は、手動でユーザーを作成することもできます。

![image2018-9-23_20-39-9](assets/image2018-9-23_20-39-9.png)

#### Admin ConsoleUI でのファイルアップロード {#file-upload-in-the-admin-console-ui}

CSV ファイルをアップロードしてユーザーをまとめて登録すると、ユーザーの作成を簡単に処理できます。

![image2018-9-23_18-59-57](assets/image2018-9-23_18-59-57.png)

#### ユーザー同期ツール {#user-sync-tool}

Adobe同期ツール (UST) を使用すると、企業のお客様は、Active Directory や他のテスト済みの OpenLDAP ディレクトリサービスを利用して、ユーザーを作成または管理できます。 対象ユーザーは、ツールをインストールおよび設定できる IT ID 管理者（Enterprise Directory および System Admin）です。 オープンソースツールはカスタマイズ可能なので、顧客は独自の要件に合わせて開発者に変更してもらうことができます。

ユーザー同期が実行されると、組織の Active Directory（または互換性のあるその他のデータソース）からユーザーのリストを取得し、Admin Console内のユーザーのリストと比較します。 その後、Admin Console を組織のディレクトリと同期するために、Adobe User Management API を呼び出します。変更フローは完全に一方向です。Admin Consoleでおこなった編集は、ディレクトリにはプッシュされません。

このツールを使用すると、お客様のディレクトリ内のAdmin Consoleグループを製品設定とAdmin Console内のユーザーグループにマッピングできます。新しい UST バージョンでは、ユーザーグループを製品内に動的に作成することもできます。

ユーザー同期を設定するには、[User Management API](https://www.adobe.io/apis/cloudplatform/usermanagement/docs/setup.html) を使用する場合と同様に、組織が一連の資格情報を作成する必要があります。

![image2018-9-23_13-36-56](assets/image2018-9-23_13-36-56.png)

ユーザー同期は、次の場所にある Adobe Github リポジトリを介して配布されます。

[https://github.com/adobe-apiplatform/user-sync.py/releases/latest](https://github.com/adobe-apiplatform/user-sync.py/releases/latest)

次の場所にあるプレリリースバージョンの 2.4RC1 は、動的グループの作成をサポートしています。[https://github.com/adobe-apiplatform/user-sync.py/releases/tag/v2.4rc1](https://github.com/adobe-apiplatform/user-sync.py/releases/tag/v2.4rc1)

このリリースの主な機能は、Admin Console でユーザーのメンバーシップに合わせて新しい LDAP グループを動的にマッピングする機能と、動的なユーザーグループ作成です。

新しいグループ機能の詳細については、こちらを参照してください。

[https://github.com/adobe-apiplatform/user-sync.py/blob/v2/docs/en/user-manual/advanced_configuration](https://github.com/adobe-apiplatform/user-sync.py/blob/v2/docs/en/user-manual/advanced_configuration.md#additional-group-options)

>[!NOTE]
>
>ユーザー同期ツールについて詳しくは、[ドキュメントページ](https://adobe-apiplatform.github.io/user-sync.py/en/)を参照してください。
>
>
>ユーザー同期ツールでは、[ここ](https://adobe-apiplatform.github.io/umapi-documentation/en/UM_Authentication.html)に説明されている手順を使用して、Adobe I/O クライアント UMAPI として登録する必要があります。
>
>Adobe I/O コンソールのドキュメントは[ここ](https://www.adobe.io/apis/cloudplatform/console.html)を参照してください。
>
>
>ユーザー同期ツールで使用される User Management API については、こちらを参照してください [場所](https://www.adobe.io/apis/cloudplatform/umapi-new.html).

>[!NOTE]
>
>AEM IMS の設定は、Adobe Managed Services チームによって処理されます。 ただし、顧客管理者は要件（自動グループメンバーシップやグループマッピングなど）に従って変更できます。 IMS クライアントもManaged Servicesチームによって登録されます。

## 使用方法 {#how-to-use}

### Admin Console での製品とユーザーアクセスの管理 {#managing-products-and-user-access-in-admin-console}

お客様の製品管理者がAdmin Consoleにログインすると、次に示すように、AEM Managed Services製品コンテキストの複数のインスタンスが表示されます。

![screen_shot_2018-09-17at105804pm](assets/screen_shot_2018-09-17at105804pm.png)

この例では、*AEM-MS-Onboard* 組織には、ステージング、実稼働など、さまざまなトポロジと環境にまたがる 32 のインスタンスがあります。

![screen_shot_2018-09-17at105517pm](assets/screen_shot_2018-09-17at105517pm.png)

詳細を確認するとインスタンスを識別できます。

![screen_shot_2018-09-17at105601pm](assets/screen_shot_2018-09-17at105601pm.png)

各製品コンテキストのインスタンスの下に、関連する製品プロファイルがあります。この製品プロファイルは、ユーザーおよびグループにアクセス権を割り当てるために使用されます。

![image2018-9-18_7-48-50](assets/image2018-9-18_7-48-50.png)

この製品プロファイルの下に追加されたすべてのユーザーおよびグループは、次の例に示すように、そのインスタンスにログインできます。

![screen_shot_2018-09-17at105623pm](assets/screen_shot_2018-09-17at105623pm.png)

### AEMへのログイン {#logging-into-aem}

#### ローカル管理者ログイン {#local-admin-login}

ログイン画面にはローカルでログインするオプションがあるので、AEMは引き続き管理者ユーザーのローカルログインをサポートできます。

![screen_shot_2018-09-18at121056am](assets/screen_shot_2018-09-18at121056am.png)

#### IMS ベースのログイン {#ims-based-login}

他のユーザーの場合は、IMS がインスタンスに設定された後に、IMS ベースのログインを使用できます。ユーザーが最初に **Adobe** ボタンをクリックします。

![image2018-9-18_0-10-32](assets/image2018-9-18_0-10-32.png)

その後、ユーザーは IMS ログイン画面にリダイレクトされ、資格情報を入力します。

![screen_shot_2018-09-17at115629pm](assets/screen_shot_2018-09-17at115629pm.png)

初回Admin Console設定時にフェデレーテッド IDP が設定される場合、ユーザーは SSO 用にカスタマー IDP にリダイレクトされます。

次の例では、IDP は Okta です。

![screen_shot_2018-09-17at115734pm](assets/screen_shot_2018-09-17at115734pm.png)

認証が完了すると、ユーザーは AEM にリダイレクトされてログインします。

![screen_shot_2018-09-18at120124am](assets/screen_shot_2018-09-18at120124am.png)

### 既存のユーザーの移行 {#migrating-existing-users}

別の認証方法を使用しており、現在 IMS に移行中の既存のAEMインスタンスの場合は、移行手順が必要です。

AEM リポジトリ内の既存ユーザー（LDAP または SAML を介してローカルに提供される）は、IDP がユーザー移行ユーティリティを使用しているため、IMS を指すように移行できます。

このユーティリティは、IMS プロビジョニングの一環として AMS チームによって実行されます。

### AEMでの権限と ACL の管理 {#managing-permissions-and-acls-in-aem}

アクセス制御とアクセス許可は引き続き AEM で管理されます。これは、IMS からのユーザーグループ（以下の例では AEM-GRP-008）と、アクセス許可とアクセス制御が定義されているローカルグループの分離を使用して実現できます。IMS から同期されたユーザーグループは、ローカルグループに割り当てられ、権限を継承することができます。

以下の例では、同期グループをローカル *Dam_Users* グループに追加しています。

ここでは、ユーザーはAdmin Console内のいくつかのグループに割り当てられています。 ( ユーザーとグループは、ユーザー同期ツールを使用して LDAP から同期することも、ローカルで作成することもできます。 **ユーザーのAdmin Consoleへのオンボーディング** 上 )。

>[!NOTE]
>
>ユーザーグループは、ユーザーがインスタンスにログインした場合にのみ同期されます。

![screen_shot_2018-09-17at94207pm](assets/screen_shot_2018-09-17at94207pm.png)

ユーザーは、IMS の以下のグループの一部です。

![screen_shot_2018-09-17at94237pm](assets/screen_shot_2018-09-17at94237pm.png)

ユーザーがログインすると、以下に示すように、グループメンバーシップが同期されます。

![screen_shot_2018-09-17at94033pm](assets/screen_shot_2018-09-17at94033pm.png)

AEM では、IMS から同期されたユーザーグループを既存のローカルグループ（DAM ユーザーなど）にメンバーとして追加できます。

![screen_shot_2018-09-17at95804pm](assets/screen_shot_2018-09-17at95804pm.png)

以下に示すように、グループは *AEM-GRP_008* は、DAM ユーザーの権限と権限を継承します。 これは、同期されたグループの権限を効果的に管理する方法で、LDAP ベースの認証方法でも一般的に使用されます。

![screen_shot_2018-09-17at110505pm](assets/screen_shot_2018-09-17at110505pm.png)
