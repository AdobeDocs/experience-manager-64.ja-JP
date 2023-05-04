---
title: 設定ファイルの読み込みと書き出し
seo-title: Importing and exporting the configuration file
description: サーバーの環境設定を編集したり、別のAEM forms 製品インスタンスを設定したりするために、設定ファイルを読み込んで書き出す方法について説明します。
seo-description: Learn how to import and export the configuration file in order to edit server preferences or configure another AEM forms product instance.
uuid: 32e8a709-2d7c-4740-9533-d53aa751bc58
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_user_management
products: SG_EXPERIENCEMANAGER/6.4/FORMS
discoiquuid: c1636537-f7dc-48d8-a3f0-9052bcd28b62
exl-id: dbad776a-60fd-4fcc-ba2a-a2f379f5462c
source-git-commit: c5b816d74c6f02f85476d16868844f39b4c47996
workflow-type: tm+mt
source-wordcount: '290'
ht-degree: 6%

---

# 設定ファイルの読み込みと書き出し {#importing-and-exporting-the-configuration-file}

>[!CAUTION]
>
>AEM 6.4 の拡張サポートは終了し、このドキュメントは更新されなくなりました。 詳細は、 [技術サポート期間](https://helpx.adobe.com/jp/support/programs/eol-matrix.html). サポートされているバージョンを見つける [ここ](https://experienceleague.adobe.com/docs/?lang=ja).

手動設定ページを使用して、設定のコピーを XML 形式でダウンロードします。 このファイルの設定は、すべてのサーバの環境設定を制御します。 その後、ファイルを編集し、サーバーにアップロードし直すことができます。 また、このファイルを使用して、別のAEM forms 製品インスタンスを設定することもできます。

セキュリティ上の問題を回避するために、ディレクトリサーバーのバインドパスワード値は、書き出された設定ファイルに含まれません。 ファイルを新しいシステムに読み込む前に、XML ファイル内のパスワードを更新します。

>[!NOTE]
>
>設定ファイルを読み込むと、ファイル内の情報に基づいてAEM forms が再設定されます。 設定ファイルの変更を検討するのは、AEM forms 製品および XML に詳しいシステム管理者またはプロフェッショナルサービスコンサルタントのみです。 例えば、破損した設定を再構成する場合に、設定ファイルを編集する必要が生じる場合があります。

**設定情報の書き出し**

1. 管理コンソールで、設定/User Management/設定/設定ファイルの読み込みと書き出しをクリックします。
1. 「書き出し」をクリックします。 Microsoft Internet Explorer を使用している場合は、ファイルを保存する場所を指定するよう求められます。 Firefox を使用している場合、ファイルはデスクトップに保存されます。

**設定情報の読み込み**

1. 管理コンソールで、設定/User Management/設定/設定ファイルの読み込みと書き出しをクリックします。
1. 「参照」をクリックして設定ファイルを探し、「読み込み」をクリックして、「OK」をクリックします。
