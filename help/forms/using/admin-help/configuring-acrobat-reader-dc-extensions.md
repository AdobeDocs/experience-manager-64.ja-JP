---
title: データ取得のための Acrobat Reader DC Extensions の設定
seo-title: Configuring Acrobat Reader DC extensions for data capture
description: データ取得のための Acrobat Reader DC Extensions の設定方法について説明します。
seo-description: Learn how to configure Acrobat Reader DC extensions for data capture.
uuid: af6b3c72-601e-4f54-8343-a323eeee5906
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_acrobat_reader_dc_extensions
products: SG_EXPERIENCEMANAGER/6.4/FORMS
discoiquuid: 8f8367fe-a8e9-46ee-a980-1633be02932d
exl-id: 3609ad29-f5b4-4426-8bbc-7c2e38f9b140
source-git-commit: e608249c3f95f44fdc14b100910fa11ffff5ee32
workflow-type: tm+mt
source-wordcount: '307'
ht-degree: 95%

---

# データ取得のための Acrobat Reader DC Extensions の設定 {#configuring-acrobat-reader-dc-extensions-for-data-capture}

AEM forms インストール環境のユーザーが Content Services（非推奨）のデータ取得機能を使用する場合、このユーザー用に、読み取り専用アクセス権を持つロールを作成することをお勧めします。

***注意**:Adobe®LiveCycle® Content Services ES（非推奨）は、LiveCycleと共にインストールされるコンテンツ管理システムです。 Content Services では、ユーザーは人間中心のプロセスを設計、管理、監視および最適化することができます。Content Services（非推奨）のサポートは 2014 年 12 月 31 日をもって終了しています。

データを取得するには、SampleReaderExtensionsCredential にアクセスするために、ユーザーロールをアサインする必要があります。標準的な Trust 管理者ロールをアサインすることはできますが、これにより管理者以外の一般的なユーザーに対して、PKI Trust 設定や PKI 秘密鍵証明書の管理を行うことができる、強力な管理者権限を付与することになるので、AEM Forms がインストールされた実稼働環境のセキュリティを危険にさらす可能性があります。AEM Forms システム管理者が、Trust Store への読み取り専用アクセス権のみを含む新規ロールを作成して、データ取得機能を使用する管理者以外のユーザーにこのロールをアサインすることをお勧めします。

## データ取得を行うユーザー用のロールの作成 {#create-a-role-for-data-capture-users}

1. 管理コンソールで、設定／User Management／ロールの管理をクリックし、「新規ロール」をクリックします。
1. 該当するフィールドにロール名（Data Capture User など）および説明を入力して、「次へ」をクリックします。
1. 「ロールの権限」画面で「権限を検索」をクリックし、使用可能な権限のリストから「Credential Read」を選択します。
1. 「OK」をクリックし、「完了」をクリックします。

## データ取得ロールをアサインするには： {#assign-the-data-capture-role}

1. 管理コンソールで、設定／User Management／ロールの管理をクリックし、「検索」をクリックします。
1. 作成したデータ取得ユーザーロールをクリックします。
1. 「ユーザー／グループのロール」タブで、「ユーザーまたはグループを検索」をクリックします。
1. 「ユーザーおよびグループを検索」画面で「検索」をクリックし、データ取得ユーザーロールを必要とするユーザーを選択して、「OK」をクリックします。
1. ロールを編集画面で、「保存」をクリックします。
