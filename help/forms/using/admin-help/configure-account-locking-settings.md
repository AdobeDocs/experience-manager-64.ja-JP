---
title: アカウントロックの設定
seo-title: Configure account-locking settings
description: 指定された回数の連続した認証エラーが発生した後にユーザーアカウントをロックするには、「アカウントロックを有効にする」オプションを使用します。
seo-description: Use the Enable Account Locking option to lock user accounts after a specified number of consecutive authentication failures.
uuid: 5ff3fb76-8b11-4818-9a75-40ed8e121da5
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/setting_up_and_managing_domains
products: SG_EXPERIENCEMANAGER/6.4/FORMS
discoiquuid: d4409c6b-f4ef-499c-8daa-e93a163ff8ab
exl-id: e407c643-5753-447e-ad4e-deb7b9eb2b55
source-git-commit: bd94d3949f0117aa3e1c9f0e84f7293a5d6b03b4
workflow-type: tm+mt
source-wordcount: '194'
ht-degree: 12%

---

# アカウントロックの設定 {#configure-account-locking-settings}

ドメインを追加する際に、アカウントのロックを有効にするかどうかを指定します。 「アカウントロックを有効にする」オプションが選択されている場合、ユーザーアカウントは、指定された回数連続した認証エラーの後でロックされます。 指定された時間が経過すると、ユーザーは再度認証を試みることができます。 この機能を使用すると、ユーザーが様々な資格情報の組み合わせを試みてシステムにアクセスするのを防ぐことができます。

ドメインの管理ページの設定を使用して、認証失敗の最大数と、アカウントがロックされる時間を指定します。 これらの設定は、アカウントロックが有効になっているすべてのドメインに適用されます。

1. 管理コンソールで、**[!UICONTROL 設定／User Management／ドメインの管理]**&#x200B;をクリックします。
1. 「連続する認証失敗の最大回数」ボックスに、ユーザーが連続してログインを失敗してからアカウントがロックされる回数を入力します。 デフォルト値は 20 です。
1. 「次の時間後にアカウントをロック解除する（分） 」ボックスに、ユーザーアカウントがロックされる時間（分）を入力します。 指定した分数が経過すると、ユーザーは再度ログインを試みることができます。 デフォルト値は 30 です。
1. 「**[!UICONTROL 保存]**」をクリックします。
