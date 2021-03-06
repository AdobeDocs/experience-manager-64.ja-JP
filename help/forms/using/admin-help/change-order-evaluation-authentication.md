---
title: 認証評価の順序の変更
seo-title: Change the order of evaluation for authentication
description: 'AEM Forms が複数の認証プロバイダーを評価する順序を変更できます。 '
seo-description: You can change the order in which AEM forms evaluates multiple authentication providers.
uuid: c2693e5b-cf09-4bb8-815a-2b20ebf6eea0
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_user_management
products: SG_EXPERIENCEMANAGER/6.4/FORMS
discoiquuid: 5434df9c-ecf6-450a-aa7e-d9ab69b66fe6
exl-id: cac16c50-a85d-4e40-a590-8a0a52be893c
source-git-commit: bd94d3949f0117aa3e1c9f0e84f7293a5d6b03b4
workflow-type: tm+mt
source-wordcount: '147'
ht-degree: 89%

---

# 認証評価の順序の変更 {#change-the-order-of-evaluation-for-authentication}

複数の認証プロバイダーを設定した場合、AEM forms による認証評価の順序を変更できます。認証評価の順序は、config.xml ファイルに一覧表示される認証プロバイダーの順序によって決まります。

1. 管理コンソールで、設定／User Management／設定／既存の設定ファイルの読み込みと書き出しをクリックします。
1. 現在の設定をファイルに書き出すには、「書き出し」をクリックして設定ファイルを別の場所に保存します。
1. ファイルから、以下のノードを検索します。

   ```as3
    <node name="AuthSchemes"> 
        <map />  
            <node name="CertificateAuth"> 
                <map> 
                    <entry key="order" value="3" />  
                    <entry key="name" value="edc.server.auth.scheme.certificate" />  
                </map> 
        </node> 
        <node name="Kerberos"> 
            <map> 
                <entry key="kerberosSPN" value="defaultSPN" />  
                <entry key="order" value="1" />  
                <entry key="name" value="edc.server.auth.scheme.kerberos" />  
            </map> 
    </node>
   ```

   In `<entry key="order" value="3" />`、各ノードの値を編集して、認証評価の順序を設定します。

1. 更新したファイルを読み込むには、User Management で、設定／既存の設定ファイルの読み込みと書き出しをクリックします。
1. 「参照」をクリックしてファイルを探し、「読み込み」をクリックして「OK」をクリックします。
