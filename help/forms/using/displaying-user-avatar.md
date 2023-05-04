---
title: ユーザーアバターの表示
seo-title: Displaying the user avatar
description: AEM Forms Workspace をカスタマイズしてログインしているユーザーの画像を表示する方法。
seo-description: How to customize the AEM Forms workspace to display the image of a logged-in user.
uuid: 2961dc93-f0d0-4842-80f1-3c239a20e348
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.4/FORMS
topic-tags: forms-workspace
discoiquuid: aec03ea5-17a6-4775-92cb-2ad361895fdf
exl-id: 2bc70cd6-1ea6-4594-9b42-ab3d3000a0c5
source-git-commit: c5b816d74c6f02f85476d16868844f39b4c47996
workflow-type: tm+mt
source-wordcount: '228'
ht-degree: 39%

---

# ユーザーアバターの表示 {#displaying-the-user-avatar}

>[!CAUTION]
>
>AEM 6.4 の拡張サポートは終了し、このドキュメントは更新されなくなりました。 詳細は、 [技術サポート期間](https://helpx.adobe.com/jp/support/programs/eol-matrix.html). サポートされているバージョンを見つける [ここ](https://experienceleague.adobe.com/docs/?lang=ja).

ログインしているユーザーのアバターは、AEM Forms Workspace の右上隅に表示されます。 また、組織階層の直属のレポートのアバターは、マネージャビューに表示されます。 AEM Forms Workspace を設定して LDAP サーバーなどのデータベースからユーザー画像を選択できます。

>[!NOTE]
>
>サポートされているユーザー画像の縦横比は 1：1 です。

1. 次の手順に記載されている詳細説明を使用して DSC を作成してください。詳細については、[AEM Forms のプログラミング](https://www.adobe.com/go/learn_aemforms_programming_63_jp)ガイドの「AEM Forms のコンポーネントの開発」トピックを参照してください。
1. DSC で、getCurrentUserImageUrl および getUserImageUrl メソッドを公開する新しい SPI を定義して、AEM Formsユーザーの画像 URL を取得します。 Java™コードスニペットのサンプルを以下に示します。

   ```as3
   public class DemoUserImageURLProviderService { 
     public String getCurrentUserImageUrl() 
     { 
        // return the URL for profile Image of logged in user 
     } 
     public String getUserImageUrl(String principalOid) 
     { 
         // return the URL for profile Image for user represented by this principal Oid 
      } 
   }
   ```

1. component.xml ファイルを作成します。 spec-id が以下のコードスニペットのようになっていることを確認します。

   次のコードスニペットはサンプルです。 具体的な要件に合わせてカスタマイズします。

   ```as3
   <component xmlns="https://adobe.com/idp/dsc/component/document"> 
       <component-id>com.adobe.sample.DemoUsersComponent</component-id> 
       <version>1.1</version> 
       <supports-export>false</supports-export> 
       <descriptor-class>com.adobe.idp.dsc.component.impl.DefaultPOJODescriptorImpl</descriptor-class> 
       <services> 
           <service name="DemoUserImageURLProviderService" title="Demo User ImageURL provider service" orchestrateable="false"> 
           <auto-deploy service-id="DemoUserImageURLProviderService" category-id="Demo Users Component DSC" major-version="1" minor-version="0" /> 
           <description>Service for resolving user image url.</description> 
            <specifications> 
            <specification spec-id="com.adobe.idp.taskmanager.dsc.enterprise.UserImageUrlProvider"/> 
            </specifications> 
           <specification-version>1.0</specification-version> 
           <implementation-class>com.adobe.sample.demousers.DemoUserImageURLProviderService</implementation-class> 
           <request-processing-strategy>single_instance</request-processing-strategy> 
           <supported-connectors>default</supported-connectors> 
           <operation-config> 
               <operation-name>*</operation-name> 
               <transaction-type>Container</transaction-type> 
               <transaction-propagation>supports</transaction-propagation> 
               <!--transaction-timeout>3000</transaction-timeout--> 
           </operation-config> 
           <operations> 
               <operation anonymous-access="false" name="getCurrentUserImageUrl" method="getCurrentUserImageUrl"> 
                   <output-parameter name="result" type="java.lang.String"/> 
               </operation> 
               <operation anonymous-access="false" name="getUserImageUrl" 
   method="getUserImageUrl"> 
               <input-parameter name="principalOid" type="java.lang.String"/> 
               <output-parameter name="result" type="java.lang.String"/> 
               </operation> 
           </operations> 
           </service> 
       </services>
   </component>
   ```

1. Workbench を通じて DSC をデプロイします。 再起動 `ProcessManagementClientSessionService` サービス。
1. ブラウザーを更新するか、ユーザーでログアウトまたはログインをし直す必要があります。
