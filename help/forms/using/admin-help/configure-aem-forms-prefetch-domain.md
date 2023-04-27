---
title: ドメイン情報をプリフェッチするためのAEM forms の設定
seo-title: Configure AEM forms to prefetchdomain information
description: 深くネストされたグループが原因で応答時間が遅くなった場合や、多くのグループのメンバーである場合は、AEM forms を設定してドメイン情報をプリフェッチします。
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
ht-degree: 40%

---

# ドメイン情報をプリフェッチするためのAEM forms の設定 {#configure-aem-forms-to-prefetchdomain-information}

多数のグループに属している場合（例：500 以上）や、グループが深くネストされている場合（例：30 レベル）は、応答時間が長くなる場合があります。 この問題が発生した場合は、特定のドメインから情報をプリフェッチするようにAEM forms を設定できます。

1. 管理コンソールで、**[!UICONTROL 設定／User Management／設定／既存の設定ファイルのインポートとエクスポート]**&#x200B;をクリックします。
1. ファイルに現在の設定をエクスポートするには、「**[!UICONTROL エクスポート]**」をクリックして別の場所に設定ファイルを保存します。
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

   この例では、プリフェッチ用に複数のドメインが設定されています。 ドメイン名は「/」で区切られます。 このことは、上の例において *Domain_Name1*、*Domain_Name2* および *Domain_Name3* として示されています。

1. 更新したファイルをインポートするには、User Management で、「**[!UICONTROL 設定ファイルのインポートとエクスポート]**」をクリックします。
1. 「**[!UICONTROL 参照]**」をクリックしてファイルを探し、「インポート」をクリックして「**[!UICONTROL OK]**」をクリックします。
