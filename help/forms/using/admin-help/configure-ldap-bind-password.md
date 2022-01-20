---
title: LDAP バインドパスワードの設定
seo-title: Configure the LDAP bind password
description: '設定ファイルを別のシステムに読み込む前にバインドパスワードを設定する方法について説明します。 '
seo-description: Learn how to configure the bind password field before you import the configuration file into another system.
uuid: 1ab1907c-8b55-4b6f-bd5b-49f22d78b8a8
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_user_management
products: SG_EXPERIENCEMANAGER/6.4/FORMS
discoiquuid: 165b3950-b03f-4848-8361-ffb0a26d2658
exl-id: eaa2c889-d116-4209-9063-0c0b32dd8849
source-git-commit: bd94d3949f0117aa3e1c9f0e84f7293a5d6b03b4
workflow-type: tm+mt
source-wordcount: '183'
ht-degree: 90%

---

# LDAP バインドパスワードの設定{#configure-the-ldap-bind-password}

セキュリティ上の問題を防ぐため、書き出された設定ファイル（config.xml）のバインドパスワードフィールドは設定されていません。設定ファイルを別のシステムに読み込む前に、このパスワードを設定してください。このパスワードは、データベースに格納されている既存のパスワードよりも優先されます。パスワードが null の場合は、既存の null 以外のパスワード値が優先されます。

1. 管理コンソールで、設定／User Management／設定／既存の設定ファイルの読み込みと書き出しをクリックします。
1. 現在の設定をファイルに書き出すには、「書き出し」をクリックして設定ファイルを別の場所に保存します。
1. ファイル内で、 `Domains` > *[ドメイン名]* > `DirectoryConfigs` > `LDAPGroupConfig` ノード。 以下に例を示します。

   ```as3
    <node name="LDAPGroupConfig"> 
        <map> 
            <entry key="bindanonymously" value="false" />  
            <entry key="basedn" value="dc=corp,dc=adobe,dc=com" />  
            <entry key="batchSize" value="200" />  
            <entry key="binduser" value="cn=Directory Manager" />  
            <entry key="bindpassword" value="" /> 
        </map>
   ```

   `bindpassword` の値部分に値を入力して変更を保存します。

1. ファイル内で、 `Domains` > *[ドメイン名]* > `DirectoryConfigs` > `LDAPGroupConfig` > `LDAPUserConfig` ノード。 以下に例を示します。

   ```as3
    <node name="LDAPUserConfig"> 
        <map> 
            <entry key="bindanonymously" value="false" />  
            <entry key="batchSize" value="200" />  
            <entry key="basedn" value="dc=corp,dc=adobe,dc=com" />  
            <entry key="bindpassword" value="" /> 
            <entry key="binduser" value="cn=Directory Manager" />  
        </map>
   ```

   `bindpassword` の値部分に値を入力して変更を保存します。

1. 更新したファイルを読み込むには、User Management で、設定／既存の設定ファイルの読み込みと書き出しをクリックします。
1. 「参照」をクリックしてファイルを探し、「読み込み」をクリックして「OK」をクリックします。
