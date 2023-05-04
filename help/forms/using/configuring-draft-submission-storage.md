---
title: ドラフトと送信に使用するストレージサービスの設定
seo-title: Configuring storage services for drafts and submissions
description: ドラフトと送信用のストレージを設定する方法を説明します
seo-description: Learn how to configure storage for drafts and submissions
uuid: 2f4efc07-312c-4908-8c91-84f4e6c5ad25
topic-tags: publish
content-type: reference
products: SG_EXPERIENCEMANAGER/6.4/FORMS
discoiquuid: 6ebb6420-68b6-4abc-b298-c252db038416
exl-id: c73fd1c5-6f3f-4c62-a8d6-fcd22f02c0ca
source-git-commit: c5b816d74c6f02f85476d16868844f39b4c47996
workflow-type: tm+mt
source-wordcount: '567'
ht-degree: 33%

---

# ドラフトと送信に使用するストレージサービスの設定 {#configuring-storage-services-for-drafts-and-submissions}

>[!CAUTION]
>
>AEM 6.4 の拡張サポートは終了し、このドキュメントは更新されなくなりました。 詳細は、 [技術サポート期間](https://helpx.adobe.com/jp/support/programs/eol-matrix.html). サポートされているバージョンを見つける [ここ](https://experienceleague.adobe.com/docs/?lang=ja).

## 概要 {#overview}

AEM Formsでは、以下を保存できます。

* **ドラフト**：後で送信するためエンドユーザーが入力して保存した作業中のフォーム。

* **送信**：ユーザーが入力したデータが含まれている送信済みフォーム。

AEM Forms Portal のデータサービスとメタデータサービスは、ドラフトと送信のサポートを提供します。 デフォルトでは、データはパブリッシュインスタンスに格納されます。その後、設定済みのオーサーインスタンスに逆複製され、他のパブリッシュインスタンスで使用できるようになります。

既存の標準アプローチでは、個人識別情報 (PII) を含むすべてのデータをパブリッシュインスタンスに保存する点が問題になります。

上記のデフォルトの方法に加えて、フォームデータをローカルに保存する代わりに、直接フォームデータを処理にプッシュする代わりに、別の実装も使用できます。 パブリッシュインスタンス上に機密データを格納することを懸念するお客様は、データを処理サーバーに送信する代替実装を選択できます。 処理はオーサーインスタンスでおこなわれるので、通常、安全なゾーンに保たれます。

>[!NOTE]
>
>「フォームポータル」送信アクションを使用したり、アダプティブフォームでフォームポータルにデータを保存するオプションを有効にしたりすると、フォームデータは AEM リポジトリーに保存されます。実稼働環境では、ドラフトまたは送信されたフォームデータを AEM リポジトリーに保存しないことをお勧めします。代わりに、ドラフトと送信コンポーネントをエンタープライズデータベースなどの安全なストレージと統合して、ドラフトと送信済みフォームデータを格納する必要があります。
>
>詳しくは、「[ドラフト&amp;送信コンポーネントとデータベースの統合](/help/forms/using/integrate-draft-submission-database.md)」を参照してください。

## Forms Portal のドラフトと送信サービスの設定 {#configuring-forms-portal-drafts-and-submissions-services}

AEM Web Console Configuration（`https://[*host*]:[*port*]/system/console/configMgr`）で、「**Forms Portal Draft and Submission Configuration**」をクリックし、編集モードで開きます。

次に示すように、必要に応じてプロパティの値を指定します。

### パブリッシュインスタンスにデータを保存するための標準提供サービス {#out-of-the-box-services-to-store-data-on-publish-instance}

データは、設定されたオーサーインスタンスにリバースレプリケートされます。

<table> 
 <tbody>
  <tr>
   <th>プロパティ</th> 
   <th>値</th> 
  </tr>
  <tr>
   <td>Forms Portal ドラフトデータサービス ( ドラフトデータサービスの識別子 (<strong>draft.data.service</strong>))</td> 
   <td>com.adobe.fd.fp.service.impl.DraftDataServiceImpl<br /> </td> 
  </tr>
  <tr>
   <td>Forms Portal Draft Metadata Service( ドラフトメタデータサービスの識別子 (<strong>draft.metadata.service</strong>))</td> 
   <td>com.adobe.fd.fp.service.impl.DraftMetadataServiceImpl<br /> </td> 
  </tr>
  <tr>
   <td>Formsポータル送信データサービス ( 送信データサービスの識別子 (<strong>submit.data.service</strong>))</td> 
   <td>com.adobe.fd.fp.service.impl.SubmitDataServiceImpl<br /> </td> 
  </tr>
  <tr>
   <td>Forms Portal 送信メタデータサービス ( 送信メタデータサービス (<strong>submit.metadata.service</strong>))</td> 
   <td>com.adobe.fd.fp.service.impl.SubmitMetadataServiceImpl<br /> </td> 
  </tr>
 </tbody>
</table>

### リモート処理インスタンスにデータを保存する標準のサービス {#out-of-the-box-services-to-store-data-on-remote-processing-instance}

データは設定されたリモートインスタンスに直接プッシュされます

<table> 
 <tbody>
  <tr>
   <th>プロパティ</th> 
   <th>値</th> 
  </tr>
  <tr>
   <td>Forms Portal ドラフトデータサービス ( ドラフトデータサービスの識別子 (<strong>draft.data.service</strong>))</td> 
   <td>com.adobe.fd.fp.service.impl.DraftDataServiceRemoteImpl<br /> </td> 
  </tr>
  <tr>
   <td>Forms Portal Draft Metadata Service( ドラフトメタデータサービスの識別子 (<strong>draft.metadata.service</strong>))</td> 
   <td>com.adobe.fd.fp.service.impl.DraftMetadataServiceRemoteImpl<br /> </td> 
  </tr>
  <tr>
   <td>Formsポータル送信データサービス ( 送信データサービスの識別子 (<strong>submit.data.service</strong>))</td> 
   <td>com.adobe.fd.fp.service.impl.SubmitDataServiceRemoteImpl<br /> </td> 
  </tr>
  <tr>
   <td>Forms Portal 送信メタデータサービス ( 送信メタデータサービス (<strong>submit.metadata.service</strong>))</td> 
   <td>com.adobe.fd.fp.service.impl.SubmitMetadataServiceRemoteImpl<br /> </td> 
  </tr>
 </tbody>
</table>

上記の設定以外に、設定済みのリモート処理インスタンスに関する情報を提供します。

AEM Web Console Configuration（`https://[*host*]:[*port*]/system/console/configMgr`）で、「**AEM DS Settings Service**」をクリックし、編集モードで開きます。AEM DS Settings Service ダイアログで、処理サーバーの URL、処理サーバーのユーザー名、およびパスワードに関する情報を入力します。

>[!NOTE]
>
>また、ユーザーデータをデータベースに格納するためのサンプル実装も提供されます。 ユーザーデータを既存のデータベースに格納するデータサービスとメタデータサービスを設定する方法を理解するには、「[サンプル：ドラフトと送信コンポーネントのデータベースへの統合](/help/forms/using/integrate-draft-submission-database.md)」を参照してください。
