---
title: Brand Portal へのコレクションの公開
description: Brand Portal を対象としたコレクションの公開および非公開の方法を学びます。
contentOwner: VG
translation-type: tm+mt
source-git-commit: 0d70a672a2944e2c03b54beb3b5f734136792ab1

---


# Brand Portal へのコレクションの公開 {#publish-collections-to-brand-portal}

Adobe Experience Manager（AEM）Assets の管理者は、組織の AEM Assets Brand Portal のインスタンスにコレクションを公開できます。ただし、最初に AEM Assets を Brand Portal と統合する必要があります。For details, see [Configure AEM Assets integration with Brand Portal](brand-portal-configuring-integration.md).

AEM Assetsの元のコレクションに後で変更を加えた場合、そのコレクションを再度公開するまで、その変更はBrand Portalに反映されません。 この特性により、作業中の変更がBrand Portalで使用できなくなります。 Brand portalでは、管理者が発行した承認済みの変更のみを利用できます。

>[!NOTE]
>
>コンテンツフラグメントは Brand Portal に公開できません。Therefore, if you select content fragment(s) on AEM Author, then **[Publish to Brand Portal]** action is not available.
>
>コンテンツフラグメントを含むコレクションを AEM オーサーインスタンスから Brand Portal へ公開した場合は、そのフォルダー内のコンテンツフラグメントを除く全コンテンツが Brand Portal インターフェイスにレプリケートされます。

## Brand Portal へのコレクションの公開 {#publish-a-collection-to-brand-portal}

1. AEM Assets の UI で AEM のロゴをタップまたはクリックします。次に、**[!UICONTROL ナビゲーション]**&#x200B;ページで&#x200B;**[!UICONTROL アセット／コレクション]**&#x200B;に移動します。
2. コレクションコンソールから、ブランドポータルに公開するコレクションを選択します。

   ![select_collection](assets/select_collection.png)

3. ツールバーで「**[!UICONTROL Brand Portal に公開]**」をタップまたはクリックします。

   ![publish_to_bp_icon](assets/publish_to_bp_icon.png)

4. 確認ダイアログで「**[!UICONTROL 公開]**」をタップまたはクリックします。
5. 確認メッセージを閉じます。
6. 管理者として Brand Portal にログインします。公開したコレクションがコレクションインターフェイスで利用できます。

   ![published_collection](assets/published_collection.png)

## コレクションを非公開にする {#unpublish-collections}

AEM AssetsからBrand portalに公開するコレクションの公開を取り消すことができます。 元のコレクションの公開を取り消すと、そのコピーはBrand portalユーザーは使用できなくなります。

1. AEM Assets インスタンスのコレクションコンソールから、非公開にしたいコレクションを選択します。

   ![select_collection-1](assets/select_collection-1.png)

2. From the toolbar, tap/click the **[!UICONTROL Remove from Brand Portal]** icon.

   ![remove_from_bp_icon](assets/remove_from_bp_icon.png)

3. 確認ダイアログで「**[!UICONTROL 非公開]**」をタップまたはクリックします。
4. 確認メッセージを閉じます。コレクションがBrand portalインターフェイスから削除されます。
