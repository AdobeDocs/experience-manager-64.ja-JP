---
title: ドラフトおよび送信データサービスのカスタマイズ
seo-title: Customizing Draft and Submission data services
description: AEM Formsはデフォルトで、ドラフトと送信済みのアダプティブフォームをパブリッシュインスタンスのデフォルトのノードに保存します。 ただし、AEM Formsのドラフトと送信データサービスを設定して、ドラフトと送信済みのアダプティブフォームのストレージをカスタマイズすることはできます。
seo-description: AEM Forms, by default, stores draft and submitted adaptive forms in a default node on the Publish instance. However, you can configure the draft and submission data services of AEM Forms to customize the storage of draft and submitted adaptive forms.
uuid: c3ec1708-3b11-4142-93f0-1cffb6643f34
content-type: reference
products: SG_EXPERIENCEMANAGER/6.4/FORMS
topic-tags: customization
discoiquuid: 602fd6a9-9a65-411c-8475-a4082a3fdee0
exl-id: c6243a1f-8f8f-48dc-af3b-b165f451ce73
source-git-commit: c5b816d74c6f02f85476d16868844f39b4c47996
workflow-type: tm+mt
source-wordcount: '312'
ht-degree: 51%

---

# ドラフトおよび送信データサービスのカスタマイズ {#customizing-draft-and-submission-data-services}

>[!CAUTION]
>
>AEM 6.4 の拡張サポートは終了し、このドキュメントは更新されなくなりました。 詳細は、 [技術サポート期間](https://helpx.adobe.com/jp/support/programs/eol-matrix.html). サポートされているバージョンを見つける [ここ](https://experienceleague.adobe.com/docs/?lang=ja).

## 概要 {#overview}

AEM Formsを使用すると、アダプティブフォームをドラフトとして保存できます。 ドラフト機能を使用すると、ユーザーは作業中のフォームを維持できます。 その後、ユーザーは任意のデバイスからいつでもフォームに入力して送信できます。

デフォルトでは、AEM Forms はドラフトと送信に関連付けられたユーザーデータを `/content/forms/fp` ノードのパブリッシュインスタンスに保存します。

ただし、AEM Formsポータルコンポーネントは、ドラフトと送信用のユーザーデータの保存の実装をカスタマイズできるデータサービスを提供します。 例えば、組織に現在実装されているデータストアにデータを保存することができます。

ユーザーデータのストレージをカスタマイズするには、 [下書きデータ](/help/forms/using/custom-draft-submission-data-services.md#p-draft-data-service-p) および [送信データ](/help/forms/using/custom-draft-submission-data-services.md#p-submission-data-service-p) サービス。

## 前提条件 {#prerequisites}

* [フォームポータルコンポーネント](/help/forms/using/enabling-forms-portal-components.md)を有効にする
* [フォームポータルページ](/help/forms/using/creating-form-portal-page.md)の作成
* [フォームポータル用アダプティブフォーム](/help/forms/using/draft-submission-component.md)を有効にする
* [カスタムストレージの実装の詳細](/help/forms/using/draft-submission-component.md#customizing-the-storage)を学ぶ

## ドラフトデータサービス {#draft-data-service}

ユーザーのドラフトデータのストレージをカスタマイズするには、`DraftAFDataService` インターフェイスのすべてのメソッドに対して実装を指定する必要があります。

メソッドとその引数の説明を、次のインターフェイスのコードサンプルに示します。

```java
public interface DraftAFDataService {
 
 /**
  * Deletes the user data stored against the ID passed as the argument
  * 
  * @param draftDataID
  * @return status for the just occurred delete draft UserData operation 
  * @throws FormsPortalException
  */
 public Boolean deleteAFDraftUserData (String draftDataID) throws FormsPortalException;
 
 /**
  * Saves user data provided in the argument map
  * 
  * @param draftUserDataMap contains Form Data (key - "guideState"), Adaptive Form Name (Key - "guideName"), and Draft DataID (Key - "userDataID") in case of update
  * @return userData ID would be returned which needs to be saved in metadata node 
  * @throws FormsPortalException
  */
 public String saveAFUserData (Map<String, Object> draftUserDataMap) throws FormsPortalException;
 
 /**
  * Gets the user data stored against the ID passed as the argument
  * 
  * @param Draft DataID
  * @return guideState (which would then be populated in adaptive form to reload the draft) which is stored against draftDataID
  * @throws FormsPortalException
  */
 public byte[] getAFDraftUserData(String draftDataID) throws FormsPortalException;
 
 /**
  * Saves the attachments for current adaptive form instance 
  * 
  * @param attachmentsBytes would expect byte array of the attachment to be saved
  * @return id for the attachment just saved (so that it could be retrieved later)
  * @throws FormsPortalException
  */
 public String saveAttachments(byte[] attachmentBytes) throws FormsPortalException;
}
```

## 送信データサービス {#submission-data-service}

ユーザーの送信データのストレージをカスタマイズするには、`SubmittedAFDataService` インターフェイスのすべてのメソッドに対して実装を指定する必要があります。

メソッドとその引数の説明を、次のインターフェイスのコードサンプルに示します。

```java
public interface SubmittedAFDataService {
 
 /**
  * Submits the user data passed in argument map
  * 
  * @param submittedAFUserdataMap contains Form Data (key - "guideState"), Adaptive Form Name (Key - "guideName"), and Draft DataID (Key - "userDataID")
  * @return userData ID is returned that needs to be saved in the metadata node
  * @throws FormsPortalException
  */
 public String submitAFUserData (Map<String, Object> submittedAFUserdataMap) throws FormsPortalException;
 
 /**
  * Gets the user data stored against the ID passed as argument
  * 
  * @param submitDataID
  * @return guideState which would be used to open DOR
  * @throws FormsPortalException
  */
 public byte[] getSubmittedAFUSerData(String submitDataID) throws FormsPortalException;
 
 /**
  * Deletes user data stored against the ID passed as argument
  * 
  * @param Submit DataID
  * @return status of the delete operation on Submitted User data
  * @throws FormsPortalException
  */
 
 public Boolean deleteSubmittedAFUserData(String submitDataID) throws FormsPortalException;
 
 /**
  * Submits the attachment bytes passed as argument
  * 
  * @param attachmentsBytes would expect byte array of the attachment to be saved
  * @return id for the attachment just saved (so that it could be retrieved later) 
  * @throws FormsPortalException
  */
 public String submitAttachments(Object attachmentBytes) throws FormsPortalException;

}
```
