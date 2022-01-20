---
title: ドメイン情報をプリフェッチするための AEM Forms の設定
seo-title: Configure AEM forms to prefetchdomain information
description: 'グループのネストが深いことによって応答時間が遅くなる場合や、多くのグループのメンバーである場合、ドメイン情報をプリフェッチするように AEM Forms を設定します。 '
seo-description: Configure AEM forms to prefetch domain information if you experience a slower response time due to deeply nested groups or if you are a member of many groups.
uuid: 53c8995e-3f9d-42e8-9f75-cee7debe6ce1
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_user_management
products: SG_EXPERIENCEMANAGER/6.4/FORMS
discoiquuid: f9a3f897-90c6-4942-8a86-aae510298f2a
exl-id: 6b431cbd-2cea-4ae2-ad26-587ba524d2f5
source-git-commit: bd94d3949f0117aa3e1c9f0e84f7293a5d6b03b4
workflow-type: tm+mt
source-wordcount: '181'
ht-degree: 67%

---

# ドメイン情報をプリフェッチするための AEM Forms の設定 {#configure-aem-forms-to-prefetchdomain-information}

ユーザーが多数のグループに属している場合（例えば、500 以上）や、グループのネストが深い場合（例えば、30 レベル）、応答時間が遅くなる可能性があります。この問題が発生している場合は、特定のドメインから情報をプリフェッチするように AEM Forms を設定できます。

1. 管理コンソールで、 **[!UICONTROL 設定/User Management /設定/設定ファイルの読み込みと書き出し]**.
1. 現在の設定をファイルに書き出すには、 **[!UICONTROL 書き出し]** 設定ファイルを別の場所に保存します。
1. 次のノード（太字でマーク）を追加します。

   ```as3
    <node name="UM"> 
    <map/>  
    <node name="PrincipalCache"> 
        <map> 
            <entry key="principalCacheSize" value="1000"/> 
            <entry key="principalCacheBatchFetchSize" value="10"/> 
            <entry key="rebuildCacheAfterSync" value="true /> 
            <entry key="enableFullPrefetch" value="false"/> 
            <entry key="principalCacheDomains" value="Domain_Name1/Domain_Name2/Domain_Name3"/> 
        <map> 
    </node> 
    <node name="APSAuditService">
   ```

   この例では、複数のドメインがプリフェッチ用に設定されています。ドメイン名は「/」によって区切られます。このことは、上の例において *Domain_Name1*、*Domain_Name2*&#x200B;および&#x200B;*Domain_Name3* として示されています。

1. 更新したファイルをインポートするには、User Management で、 **[!UICONTROL 設定/設定ファイルの読み込みと書き出し]**.
1. クリック **[!UICONTROL 参照]** ファイルを検索するには、[ インポート ] をクリックし、 **[!UICONTROL OK]**.
