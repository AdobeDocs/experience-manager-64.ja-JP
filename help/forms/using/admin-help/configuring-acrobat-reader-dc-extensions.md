---
title: データ取得のための Acrobat Reader DC Extensions の設定
seo-title: Configuring Acrobat Reader DC extensions for data capture
description: データキャプチャ用にAcrobat Reader DC拡張機能を設定する方法について説明します。
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
ht-degree: 5%

---

# データ取得のための Acrobat Reader DC Extensions の設定 {#configuring-acrobat-reader-dc-extensions-for-data-capture}

AEM forms インストール環境のユーザーが Content Services（非推奨）のデータ取得機能を使用している場合、これらのユーザーに対して読み取り専用アクセス権を持つロールを作成することをお勧めします。

***注意**:Adobe®LiveCycle® Content Services ES（非推奨）は、LiveCycleと共にインストールされるコンテンツ管理システムです。 これにより、ユーザーは人間中心のプロセスを設計、管理、監視、最適化できます。 Content Services（非推奨）のサポートは12/31/2014で終了します。

データ取得を行うには、SampleReaderExtensionsCredential にアクセスするためのユーザーロールを割り当てる必要があります。 標準の信頼管理者の役割を割り当てることもできますが、この役割は、一般の非管理者ユーザーに、PKI 信頼設定を制御し、PKI 資格情報を管理する強力な管理者権限を与えると考えてください。これにより、実稼働環境でのAEM forms のインストールのセキュリティが損なわれます。 AEM forms システム管理者は、Trust Store への読み取り専用アクセス権のみを付与するロールを作成し、この新しいロールを、データ取得を使用する管理者以外のユーザーに割り当てることをお勧めします。

## データ取得ユーザーのロールの作成 {#create-a-role-for-data-capture-users}

1. 管理コンソールで、設定/User Management/役割の管理をクリックし、「新しい役割」をクリックします。
1. ロール名（例：データ取得ユーザ）と説明を適切なフィールドに入力し、「次へ」をクリックします。
1. 役割の権限画面で、「権限を検索」をクリックし、使用可能な権限のリストから「Credential Read」を選択します。
1. 「OK」をクリックし、「完了」をクリックします。

## データキャプチャの役割を割り当てる {#assign-the-data-capture-role}

1. 管理コンソールで、設定/User Management/役割の管理をクリックし、「検索」をクリックします。
1. 作成したデータ取得ユーザーの役割をクリックします。
1. [ 役割のユーザー/グループ ] タブで、[ ユーザー/グループの検索 ] をクリックします。
1. 「ユーザーおよびグループの検索」画面で「検索」をクリックし、データ取得ユーザーの役割を必要とするユーザーを選択して、「OK」をクリックします。
1. 役割を編集画面で、「保存」をクリックします。
