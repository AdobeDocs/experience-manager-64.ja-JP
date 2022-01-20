---
title: Eclipse を使用して AEM プロジェクトを開発する方法
seo-title: How to Develop AEM Projects Using Eclipse
description: このガイドでは、Eclipse を使用して AEM ベースのプロジェクトを開発する方法について説明します
seo-description: This guide describes how to use Eclipse for developing AEM based projects
uuid: 79fee76f-6bcc-498f-af46-530816b41bbe
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.4/SITES
topic-tags: development-tools
content-type: reference
discoiquuid: aa58cfb8-ec15-4698-a8f0-97683b0de51c
exl-id: 5fae4a4c-c97a-4541-bdc5-63ef4ca0172c
source-git-commit: bd94d3949f0117aa3e1c9f0e84f7293a5d6b03b4
workflow-type: tm+mt
source-wordcount: '435'
ht-degree: 65%

---

# Eclipse を使用して AEM プロジェクトを開発する方法{#how-to-develop-aem-projects-using-eclipse}

このガイドでは、Eclipse を使用して AEM ベースのプロジェクトを開発する方法について説明します。

>[!NOTE]
>
>アドビでは、Eclipse による AEM ソリューションの開発を支援する [AEM Developer Tools for Eclipse](/help/sites-developing/aem-eclipse.md) を提供しています。

## 概要 {#overview}

Eclipse で AEM の開発を開始するには、次の手順を実行する必要があります。

各手順の詳細については、このページで後述します。

* Eclipse 4.3（Kepler）のインストール
* Maven に基づく AEM プロジェクトの設定
* Maven POM での Eclipse 用の JSP サポートの準備
* Eclipse への Maven プロジェクトの読み込み

>[!NOTE]
>
>このガイドは Eclipse 4.3（Kepler）と AEM 5.6.1 を基に作成されています。

## Eclipse のインストール {#install-eclipse}

[Eclipse のダウンロードページ](https://www.eclipse.org/downloads/)から「Eclipse IDE for Java EE Developers」をダウンロードします。

[インストール手順](https://wiki.eclipse.org/Eclipse/Installation)に従って Eclipse をインストールします。

## Maven に基づく AEM プロジェクトの設定 {#set-up-your-aem-project-based-on-maven}

次に、 [Apache Maven を使用したAEMプロジェクトの構築方法](/help/sites-developing/ht-projects-maven.md).

## Eclipse 用の JSP サポートの準備 {#prepare-jsp-support-for-eclipse}

Eclipse では JSP との連携もサポートされます。サポートされる項目の例を次に示します。

* タグライブラリのオートコンプリート
* &lt;cq:defineObjects /> と &lt;sling:defineObjects /> で定義されたオブジェクトの Eclipse での認識

サポートを有効にするには、次の手順を実行します。

1. 次の手順に従います。 [JSP の使用方法](/help/sites-developing/ht-projects-maven.md#how-to-work-with-jsps) in [Apache Maven を使用したAEMプロジェクトの構築方法](/help/sites-developing/ht-projects-maven.md).
1. コンテンツモジュールの POM 内の &lt;build /> セクションに次の項目を追加します。

   Eclipse の Maven サポートプラグインである m2e は maven-jspc-plugin のサポートを提供しません。この設定は、プラグインおよび一時的なコンパイルの結果のクリーンアップの関連タスクを無視するように m2e に通知します。

   これは問題ではありません。～で述べたように [JSP の使用方法](/help/sites-developing/ht-projects-maven.md#how-to-work-with-jsps)の場合、この設定では、maven-jspc-plugin は、ビルドプロセスの一部として JSP コンパイルを検証するためにのみ使用されます。Eclipse は、JSP で既に問題を報告しています。これを実行する際に、この Maven プラグインに依存しません。

   **myproject/content/pom.xml**

   ```xml
   <build>
     <!-- ... -->
     <pluginManagement>
       <plugins>
         <!--This plugin's configuration is used to store Eclipse m2e settings only. It has no influence on the Maven build itself.-->
         <plugin>
           <groupId>org.eclipse.m2e</groupId>
           <artifactId>lifecycle-mapping</artifactId>
           <version>1.0.0</version>
           <configuration>
             <lifecycleMappingMetadata>
               <pluginExecutions>
                 <pluginExecution>
                   <pluginExecutionFilter>
                     <groupId>org.apache.sling</groupId>
                     <artifactId>maven-jspc-plugin</artifactId>
                     <versionRange>[2.0.6,)</versionRange>
                     <goals>
                       <goal>jspc</goal>
                     </goals>
                   </pluginExecutionFilter>
                   <action>
                     <ignore/>
                   </action>
                 </pluginExecution>
                 <pluginExecution>
                   <pluginExecutionFilter>
                     <groupId>org.apache.maven.plugins</groupId>
                     <artifactId>maven-clean-plugin</artifactId>
                     <versionRange>[2.4.1,)</versionRange>
                     <goals>
                       <goal>clean</goal>
                     </goals>
                   </pluginExecutionFilter>
                   <action>
                     <ignore/>
                   </action>
                 </pluginExecution>
               </pluginExecutions>
             </lifecycleMappingMetadata>
           </configuration>
         </plugin>
       </plugins>
     </pluginManagement>
   </build>
   ```

### Eclipse への Maven プロジェクトの読み込み {#import-the-maven-project-into-eclipse}

1. Eclipse で、File／Import を選択します。
1. Import ダイアログで、Maven／Existing Maven Projects を選択し、「Next」をクリックします。

   ![chlimage_1-41](assets/chlimage_1-41.png)

1. プロジェクトの最上位のフォルダーのパスを入力して、「Select All」、「Finish」の順にクリックします。

   ![chlimage_1-42](assets/chlimage_1-42.png)

1. これで、Eclipse を使用して AEM プロジェクトを開発するための設定（JSP のオートコンプリートを含む）がすべて完了しました。

   ![chlimage_1-43](assets/chlimage_1-43.png)

   >[!NOTE]
   >
   >次を含める場合： `/libs/foundation/global.jsp` または内の他の JSP `/libs`を使用する場合は、Eclipse がインクルージョンを解決できるように、プロジェクトにコピーする必要があります。 同時に、Maven によってコンテンツパッケージにバンドルされていないことを確認する必要があります。 これをおこなう方法については、 [Apache Maven を使用してAEMプロジェクトを構築する方法](/help/sites-developing/ht-projects-maven.md).
