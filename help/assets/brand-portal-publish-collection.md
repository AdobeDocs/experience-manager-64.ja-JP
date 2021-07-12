---
title: Brand Portal へのコレクションの公開
description: Brand Portal を対象としたコレクションの公開および非公開の方法を学びます。
contentOwner: VG
feature: Brand Portal
role: User
exl-id: c2c6759e-f763-405e-9e45-5a90b9d32df2
source-git-commit: 3c050c33a384d586d74bd641f7622989dc1d6b22
workflow-type: tm+mt
source-wordcount: '340'
ht-degree: 63%

---

# Brand Portal へのコレクションの公開 {#publish-collections-to-brand-portal}

Adobe Experience Manager（AEM）Assets の管理者は、組織の AEM Assets Brand Portal のインスタンスにコレクションを公開できます。ただし、最初に AEM Assets を Brand Portal と統合する必要があります。詳しくは [AEM Assets と Brand Portal の連携の設定](configure-aem-assets-with-brand-portal.md)を参照してください。

その後、AEM Assetsで元のコレクションに変更を加えても、そのコレクションを再度公開するまで、変更はBrand Portalに反映されません。 この特性により、作業中の変更がBrand Portalでは利用できなくなります。 管理者が公開した承認済みの変更のみが Brand Portal で提供されます。

>[!NOTE]
>
>コンテンツフラグメントは Brand Portal に公開できません。したがって、AEMオーサー上でコンテンツフラグメントを選択した場合、「**[Brand Portalに公開]**」アクションは使用できません。
>
>コンテンツフラグメントを含むコレクションを AEM オーサーインスタンスから Brand Portal へ公開した場合は、そのフォルダー内のコンテンツフラグメントを除く全コンテンツが Brand Portal インターフェイスにレプリケートされます。

## Brand Portal へのコレクションの公開 {#publish-a-collection-to-brand-portal}

1. AEM Assets の UI で AEM のロゴをタップまたはクリックします。次に、**[!UICONTROL ナビゲーション]**&#x200B;ページで&#x200B;**[!UICONTROL アセット／コレクション]**&#x200B;に移動します。
2. コレクションコンソールで、Brand Portalに公開するコレクションを選択します。

   ![select_collection](assets/select_collection.png)

3. ツールバーで「**[!UICONTROL Brand Portal に公開]**」をタップまたはクリックします。

   ![publish_to_bp_icon](assets/publish_to_bp_icon.png)

4. 確認ダイアログで「**[!UICONTROL 公開]**」をタップまたはクリックします。
5. 確認メッセージを閉じます。
6. 管理者として Brand Portal にログインします。公開したコレクションがコレクションインターフェイスで利用できます。

   ![published_collection](assets/published_collection.png)

## コレクションを非公開にする {#unpublish-collections}

AEM AssetsからBrand Portalに公開したコレクションを非公開にできます。 元のコレクションを非公開にすると、そのコレクションのコピーはBrand Portalユーザーには使用できなくなります。

1. AEM Assets インスタンスのコレクションコンソールから、非公開にしたいコレクションを選択します。

   ![select_collection-1](assets/select_collection-1.png)

2. ツールバーの「**[!UICONTROL Brand Portalから削除]**」アイコンをタップまたはクリックします。

   ![remove_from_bp_icon](assets/remove_from_bp_icon.png)

3. 確認ダイアログで「**[!UICONTROL 非公開]**」をタップまたはクリックします。
4. 確認メッセージを閉じます。コレクションが Brand Portal インターフェイスから削除されます。
