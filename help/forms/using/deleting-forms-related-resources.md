---
title: フォームと関連リソースの削除
seo-title: Deleting forms and related resources
description: AEM Formsでフォームやアセットを削除する方法、および参照元および参照元のアセットと XFA フォームに対する影響。
seo-description: How to delete a form or an asset in AEM Forms and the impact on referenced and referring assets and XFA forms.
uuid: df522b87-59d8-4678-922d-c9aab82b1381
content-type: reference
products: SG_EXPERIENCEMANAGER/6.4/FORMS
topic-tags: forms-manager
discoiquuid: c8519eec-f841-4867-baa9-a9e03042755e
role: Admin
exl-id: 94a66d83-b359-4be6-b668-4b4ba024b1e7
source-git-commit: c5b816d74c6f02f85476d16868844f39b4c47996
workflow-type: tm+mt
source-wordcount: '407'
ht-degree: 24%

---

# フォームと関連リソースの削除 {#deleting-forms-and-related-resources}

>[!CAUTION]
>
>AEM 6.4 の拡張サポートは終了し、このドキュメントは更新されなくなりました。 詳細は、 [技術サポート期間](https://helpx.adobe.com/jp/support/programs/eol-matrix.html). サポートされているバージョンを見つける [ここ](https://experienceleague.adobe.com/docs/?lang=ja).

フォームとアセットを削除して、これらのアセットをリポジトリから削除できます。 削除操作は、すべてのアセットタイプおよびフォルダーで機能します。

オーサーインスタンスからアセットを削除すると、そのアセットもパブリッシュインスタンスから削除されます。 AEM Formsサーバーは、オーサーインスタンスとパブリッシュインスタンスで構成されます。 オーサーインスタンスは、フォームのアセットとリソースを作成し、管理するためのものです。 発行インスタンスには、エンドユーザーが使用できる発行済みフォームのアセットと関連リソースが含まれています。

## フォームの削除方法 {#how-to-delete-a-form}

1. `https://[hostname]:[portport]/aem/forms.html.` にアクセスして AEM Forms ユーザーインターフェイスにログインします。
1. 削除するフォームを探して移動します。ツールバーで ![aem6forms_delete2](assets/aem6forms_delete2.png) 削除をクリックし、削除操作を確定します。

   >[!NOTE]
   >
   >一度に削除できるフォームは 1 つだけです。 複数のフォームを個別に削除するか、親フォルダーを削除します。

1. アセットを削除する前に、AEM Formsは参照を確認し、明示的な確認を求めます。 関係ステータスに関係なくアセットを削除する場合は、「削除を強制」をクリックします。

   >[!NOTE]
   >
   >他のアセットによって参照されているアセットを削除すると、機能に問題を起こす可能性があります。

   >[!NOTE]
   >
   >選択したアセットがフォルダーで、その階層にそのようなアセットが含まれている場合は、他のアセットを個別に削除するか、フォルダー全体を削除します。

## 参照先 XFA フォームを削除した場合の影響 {#impact-of-deleting-a-referenced-xfa-form}

AEM Formsでは、XFA フォームテンプレートは、アダプティブフォームまたは別の XFA フォームテンプレートによって参照することができます。 また、テンプレートは、リソースまたは別の XFA テンプレートを参照することもできます。

アダプティブフォームが参照している XFA フォームは、アダプティブフォームを破損する可能性があるので、削除しないことをお勧めします。 アダプティブフォームが XFA フォームを参照する場合、そのフィールドは連結されます。 XFA の削除後、アダプティブフォームはそのフィールドを XFA フィールドと同期できず、そのようなフィールドに関するエラーメッセージを表示します。 参照先 XFA の削除の影響と dirty アダプティブフォームの詳細については、[参照先 XFA フォームの更新](/help/forms/using/get-xdp-pdf-documents-aem.md#p-updating-referenced-xfa-forms-p)を参照してください。

このような XFA フォームを削除するには、アダプティブフォームを更新し、XFA フィールドとの連結を削除します。
