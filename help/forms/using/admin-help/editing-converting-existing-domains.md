---
title: 既存のドメインの編集と変換
seo-title: Editing and converting existing domains
description: ドメインの管理ページで既存のドメインの設定を変更する方法を説明します。 既存のエンタープライズドメインをハイブリッドドメインに（またはその逆に）変換する。
seo-description: Learn how to change the settings for existing domains from the Domain Management page. Convert an existing enterprise domain to a hybrid domain or vice versa.
uuid: 4cc9547e-b4ec-4588-b1cf-18720f06149a
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/setting_up_and_managing_domains
products: SG_EXPERIENCEMANAGER/6.4/FORMS
discoiquuid: 44dec184-3ef7-4ba6-a87f-ad171d3cb188
exl-id: 07ca7715-f7b3-40e0-95bc-e05f0662ed08
source-git-commit: c5b816d74c6f02f85476d16868844f39b4c47996
workflow-type: tm+mt
source-wordcount: '346'
ht-degree: 13%

---

# 既存のドメインの編集と変換{#editing-and-converting-existing-domains}

>[!CAUTION]
>
>AEM 6.4 の拡張サポートは終了し、このドキュメントは更新されなくなりました。 詳細は、 [技術サポート期間](https://helpx.adobe.com/jp/support/programs/eol-matrix.html). サポートされているバージョンを見つける [ここ](https://experienceleague.adobe.com/docs/?lang=ja).

ドメインの管理ページで、既存のドメインの設定を変更できます。 既存のエンタープライズドメインをハイブリッドドメインに変換することもできます。

## 既存のドメインの編集 {#edit-an-existing-domain}

1. 管理コンソールで、設定／User Management／ドメインの管理をクリックします。
1. 編集するドメインの名前をクリックします。
1. ドメイン名を変更するには、[ 名前 ] ボックスのテキストを変更します。
1. エンタープライズドメインまたはハイブリッドドメインの認証情報を変更するには、ページの下部にある適切な認証名をクリックします。 認証を編集ページで、必要に応じて設定を変更します。 ( [認証設定](/help/forms/using/admin-help/configuring-authentication-providers.md#authentication-settings).)
1. エンタープライズドメインのディレクトリ情報を変更するには、ページの下部にある適切なディレクトリ名をクリックします。 ディレクトリを編集ページで、必要に応じて設定を変更します。 ( [ディレクトリまたはカスタム SPI の追加](/help/forms/using/admin-help/configuring-directories.md#adding-directories-or-custom-spis).)
1. 変更が完了したら、[OK] をクリックします。

## エンタープライズドメインのハイブリッドドメインへの変換 {#convert-an-enterprise-domain-to-a-hybrid-domain}

1. 管理コンソールで、設定／User Management／ドメインの管理をクリックします。
1. 変換するエンタープライズドメインの名前をクリックします。
1. 「ハイブリッドドメインに変換」をクリックします。
1. ユーザーおよびグループのデータとユーザーの認証に関して表示される情報を確認し、「OK」をクリックします。
1. ハイブリッドドメインの設定を編集し、「OK」をクリックします。

>[!NOTE]
>
>変換するエンタープライズドメインにディレクトリ設定が含まれていない場合、LDAP 認証設定は失われます。

## ハイブリッドドメインのエンタープライズドメインへの変換 {#convert-a-hybrid-domain-to-an-enterprise-domain}

1. 管理コンソールで、設定／User Management／ドメインの管理をクリックします。
1. 変換するハイブリッドドメインの名前をクリックします。
1. 「エンタープライズドメインに変換」をクリックします。
1. ユーザーおよびグループのデータとユーザーの認証に関して表示される情報を確認し、「OK」をクリックします。
1. 「ディレクトリを追加」をクリックし、必要なディレクトリ情報を設定します。 ( [ディレクトリまたはカスタム SPI の追加](/help/forms/using/admin-help/configuring-directories.md#adding-directories-or-custom-spis).)
