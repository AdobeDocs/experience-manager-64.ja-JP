---
title: Brand Portal へのコレクションの公開
description: Brand Portal を対象としたコレクションの公開および非公開の方法を学びます。
contentOwner: VG
feature: Brand Portal
role: User
exl-id: c2c6759e-f763-405e-9e45-5a90b9d32df2
source-git-commit: de5632ff0ee87a4ded88e792b57e818baf4c01a3
workflow-type: tm+mt
source-wordcount: '323'
ht-degree: 41%

---

# Brand Portal へのコレクションの公開 {#publish-collections-to-brand-portal}

Adobe Experience Manager Assets 管理者は、コレクションを [!DNL Experience Manager Assets Brand Portal] 組織のインスタンス。 ただし、最初に Assets を Brand Portal と統合する必要があります。詳しくは [ Assets と Brand Portal の連携の設定](configure-aem-assets-with-brand-portal.md)を参照してください。

その後、Assets 内の元のコレクションに変更を加えても、そのコレクションを再度公開するまで、変更はBrand Portalに反映されません。 この特性により、作業中の変更がBrand Portalでは利用できなくなります。 管理者が公開した承認済みの変更のみが Brand Portal で提供されます。

>[!NOTE]
>
>コンテンツフラグメントは Brand Portal に公開できません。したがって、 [!DNL Experience Manager] 作成者、その後 **[Brand Portalに公開]** アクションは使用できません。
>
>コンテンツフラグメントを含むコレクションをから公開する場合 [!DNL Experience Manager] Brand Portalにオーサリングした後、コンテンツフラグメントを除くフォルダーのすべてのコンテンツがBrand Portalインターフェイスにレプリケートされます。

## Brand Portal へのコレクションの公開 {#publish-a-collection-to-brand-portal}

1. Assets UI で、 [!DNL Experience Manager] ロゴ 次に、**[!UICONTROL ナビゲーション]**&#x200B;ページで&#x200B;**[!UICONTROL アセット／コレクション]**&#x200B;に移動します。
2. コレクションコンソールで、Brand Portalに公開するコレクションを選択します。

   ![select_collection](assets/select_collection.png)

3. ツールバーで「**[!UICONTROL Brand Portal に公開]**」をタップまたはクリックします。

   ![publish_to_bp_icon](assets/publish_to_bp_icon.png)

4. 確認ダイアログで「**[!UICONTROL 公開]**」をタップまたはクリックします。
5. 確認メッセージを閉じます。
6. 管理者として Brand Portal にログインします。公開したコレクションがコレクションインターフェイスで利用できます。

   ![published_collection](assets/published_collection.png)

## コレクションを非公開にする {#unpublish-collections}

Assets からBrand Portalに公開したコレクションを非公開にできます。 元のコレクションを非公開にすると、そのコピーはBrand Portalのユーザーは使用できなくなります。

1. コレクションコンソールから、 [!DNL Assets] インスタンスを選択し、非公開にするコレクションを選択します。

   ![select_collection-1](assets/select_collection-1.png)

2. ツールバーの **[!UICONTROL Brand Portalから削除]** アイコン

   ![remove_from_bp_icon](assets/remove_from_bp_icon.png)

3. 確認ダイアログで「**[!UICONTROL 非公開]**」をタップまたはクリックします。
4. 確認メッセージを閉じます。コレクションが Brand Portal インターフェイスから削除されます。
