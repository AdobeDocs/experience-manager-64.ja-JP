---
title: マネージャービューを使用した組織階層でのタスクの管理
seo-title: Managing tasks in an organizational hierarchy using Manager View
description: 管理者や組織の責任者がAEM Forms Workspace の「TODO」タブで直属および直属の部下のタスクにアクセスし、作業する方法。
seo-description: How managers and organization heads can access and work on the tasks of their direct and indirect reports in the To-do tab in AEM Forms workspace.
uuid: a44d5a64-c03a-4337-8577-b121e6202449
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.4/FORMS
topic-tags: forms-workspace
discoiquuid: c7cf28bf-2806-47bc-a803-8bc0e803fc4d
exl-id: 28877528-2f91-4ee0-b9d8-c7df364ed803
source-git-commit: c5b816d74c6f02f85476d16868844f39b4c47996
workflow-type: tm+mt
source-wordcount: '380'
ht-degree: 38%

---

# マネージャービューを使用した組織階層でのタスクの管理 {#managing-tasks-in-an-organizational-hierarchy-using-manager-view}

>[!CAUTION]
>
>AEM 6.4 の拡張サポートは終了し、このドキュメントは更新されなくなりました。 詳細は、 [技術サポート期間](https://helpx.adobe.com/jp/support/programs/eol-matrix.html). サポートされているバージョンを見つける [ここ](https://experienceleague.adobe.com/docs/?lang=ja).

AEM Forms Workspace で、管理者は、階層内の任意のユーザーに割り当てられたタスク（直属または直属の部下）にアクセスし、様々なアクションを実行できるようになりました。 タスクは、AEM Forms Workspace の「TODO」タブで使用できます。 ダイレクトレポートのタスクでサポートされるアクションは次のとおりです。

**転送** 直属のタスクを任意のユーザーに転送します。

**要求**&#x200B;直属のタスクを要求します。

**要求して開く**&#x200B;直属のタスクを要求してマネージャーの TODO リストに自動的に開きます。

**拒否**&#x200B;他のユーザーによって直属に転送されたタスクを拒否します。このオプションは、他のユーザーによって直属のユーザーに転送されたタスクで使用できます。

AEM Formsは、ユーザーのアクセスを、ユーザーがアクセス制御 (ACL) を持つタスクのみに制限します。 このようなチェックを行うと、ユーザーはアクセス権限を持つタスクのみを取得できます。 サードパーティの Web サービスと実装を使用して階層を定義する場合、組織は、ニーズに合わせてマネージャーとダイレクトレポートの定義をカスタマイズできます。

1. DSC を作成します。詳細については、「[AEM Forms によるプログラミング](https://www.adobe.com/go/learn_aemforms_programming_63_jp)」ガイドの「AEM Forms のコンポーネントの開発」トピックを参照してください。
1. DSC で、階層管理の新しい SPI を定義して、AEM Formsユーザー内の直接レポートおよび階層を定義します。 Java™コードスニペットのサンプルを以下に示します。

   ```as3
   public class MyHierarchyMgmtService 
   { 
        /*
       Input : Principal Oid for a livecycle user
       Output : Returns true when the user is either the service invoker OR his direct/indirect report.
       */
       boolean isInHierarchy(String principalOid) {
   
       }
   
       /* 
       Input : Principal Oid for a livecycle user
       Output : List of principal Oids for direct reports of the livecycle user
       A user may get direct reports only for himself OR his direct/indirect reports.
       So the API is functionally equivalent to - 
       isInHierarchy(principalOid) ? <return direct reports> : <return empty list>
       */
       List<String> getDirectReports(String principalOid) {
   
       }
   
       /* 
       Returns whether a livecycle user has direct reports or not.
       It's functionally equivalent to -
       getDirectReports(principalOid).size()>0
       */
       boolean isManager(String principalOid) {
   
       }  
   }
   ```

1. component.xml ファイルを作成します。 spec-id が以下のコードスニペットと同じである必要があります。 再利用可能なサンプルコードスニペットを以下に示します。

   ```as3
   <component xmlns="https://adobe.com/idp/dsc/component/document"> 
       <component-id>com.adobe.sample.SampleDSC</component-id> 
       <version>1.1</version> 
       <supports-export>false</supports-export> 
         <descriptor-class>com.adobe.idp.dsc.component.impl.DefaultPOJODescriptorImpl</descriptor-class> 
         <services> 
           <service name="MyHierarchyMgmtService" title="My hierarchy management service" orchestrateable="false"> 
           <auto-deploy service-id="MyHierarchyMgmtService" category-id="Sample DSC" major-version="1" minor-version="0" /> 
           <description>Service for resolving hierarchy management.</description> 
            <specifications> 
            <specification spec-id="com.adobe.idp.taskmanager.dsc.enterprise.HierarchyManagementProvider"/> 
            </specifications> 
           <specification-version>1.0</specification-version> 
           <implementation-class>com.adobe.sample.hierarchymanagement.MyHierarchyMgmtService</implementation-class> 
           <request-processing-strategy>single_instance</request-processing-strategy> 
           <supported-connectors>default</supported-connectors> 
           <operation-config> 
               <operation-name>*</operation-name> 
               <transaction-type>Container</transaction-type> 
               <transaction-propagation>supports</transaction-propagation> 
               <!--transaction-timeout>3000</transaction-timeout--> 
           </operation-config> 
           <operations> 
               <operation anonymous-access="true" name="isInHierarchy" method="isInHierarchy"> 
                   <input-parameter name="principalOid" type="java.lang.String" /> 
                   <output-parameter name="result" type="java.lang.Boolean"/> 
               </operation> 
               <operation anonymous-access="true" name="getDirectReports" method="getDirectReports"> 
                   <input-parameter name="principalOid" type="java.lang.String" /> 
                   <output-parameter name="result" type="java.util.List"/> 
               </operation> 
               <operation anonymous-access="true" name="isManager" method="isManager"> 
                   <input-parameter name="principalOid" type="java.lang.String" /> 
                   <output-parameter name="result" type="java.lang.Boolean"/> 
               </operation> 
               </operations> 
               </service> 
         </services>
   </component>
   ```

1. Workbench を通じて DSC をデプロイします。 再起動 `ProcessManagementTeamTasksService` サービス。
1. ブラウザーを更新するか、ユーザーでログアウトまたはログインをし直す必要があります。

次の画面は、直属の部下のタスクへのアクセスと使用可能なアクションを示しています。

![cu_manager_view](assets/cu_manager_view.png)

直属のタスクへのアクセスとタスクで実行するアクション
