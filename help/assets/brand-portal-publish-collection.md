---
title: Brand Portal へのコレクションの公開
description: コレクションをBrand Portalに公開および非公開にする方法を説明します。
contentOwner: VG
feature: Brand Portal
role: User
exl-id: c2c6759e-f763-405e-9e45-5a90b9d32df2
source-git-commit: c5b816d74c6f02f85476d16868844f39b4c47996
workflow-type: tm+mt
source-wordcount: '359'
ht-degree: 47%

---

# Brand Portal へのコレクションの公開 {#publish-collections-to-brand-portal}

>[!CAUTION]
>
>AEM 6.4 の拡張サポートは終了し、このドキュメントは更新されなくなりました。 詳細は、 [技術サポート期間](https://helpx.adobe.com/jp/support/programs/eol-matrix.html). サポートされているバージョンを見つける [ここ](https://experienceleague.adobe.com/docs/?lang=ja).

Adobe Experience Manager Assets 管理者は、コレクションを [!DNL Experience Manager Assets Brand Portal] 組織のインスタンス。 ただし、最初に Assets を Brand Portal と統合する必要があります。詳しくは [ Assets と Brand Portal の連携の設定](configure-aem-assets-with-brand-portal.md)を参照してください。

その後、 Assets でオリジナルのコレクションに変更を加えても、そのコレクションを再び公開しない限り変更内容は Brand Portal に反映されません。このため、作業中の変更が Brand Portal に提供されることがありません。管理者が公開した承認済みの変更のみが Brand Portal で提供されます。

>[!NOTE]
>
>コンテンツフラグメントは Brand Portal に公開できません。したがって、 [!DNL Experience Manager] 作成者、その後 **[Brand Portalに公開]** アクションは使用できません。
>
>コンテンツフラグメントを含むコレクションをから公開する場合 [!DNL Experience Manager] Brand Portalにオーサリングした後、コンテンツフラグメントを除くフォルダーのすべてのコンテンツがBrand Portalインターフェイスにレプリケートされます。

## Brand Portal へのコレクションの公開 {#publish-a-collection-to-brand-portal}

1. Assets UI で、 [!DNL Experience Manager] ロゴ 次に、に移動します。 **[!UICONTROL アセット/コレクション]** から **[!UICONTROL ナビゲーション]** ページ。
2. コレクションコンソールで、Brand Portalに公開するコレクションを選択します。

   ![select_collection](assets/select_collection.png)

3. ツールバーのをタップまたはクリックします。 **[!UICONTROL Brand Portalに公開]**.

   ![publish_to_bp_icon](assets/publish_to_bp_icon.png)

4. 確認ダイアログで、をタップまたはクリックします。 **[!UICONTROL 公開]**.
5. 確認メッセージを閉じます。
6. 管理者として Brand Portal にログインします。公開したコレクションがコレクションインターフェイスで利用できます。

   ![published_collection](assets/published_collection.png)

## コレクションを非公開にする {#unpublish-collections}

 Assets から Brand Portal へ公開したコレクションを非公開にすることができます。元のコレクションを非公開にすると、Brand Portal のユーザーはそのコピーを使用できなくなります。

1. コレクションコンソールから、 [!DNL Assets] インスタンスを選択し、非公開にするコレクションを選択します。

   ![select_collection-1](assets/select_collection-1.png)

2. ツールバーの **[!UICONTROL Brand Portalから削除]** アイコン

   ![remove_from_bp_icon](assets/remove_from_bp_icon.png)

3. ダイアログで、「 」をタップまたはクリックします。 **[!UICONTROL 非公開]**.
4. 確認メッセージを閉じます。コレクションが Brand Portal インターフェイスから削除されます。
