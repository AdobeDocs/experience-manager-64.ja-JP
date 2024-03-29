---
title: メディアハンドラーとワークフローを使用したアセットの処理
description: 様々なハンドラーの概要と、ワークフローでハンドラーを使用してアセットに対してタスクを実行する方法について説明します。
contentOwner: AG
feature: Workflow,Renditions
role: User
exl-id: 7694c68d-0a17-4052-8fbe-9bf45b229e81
source-git-commit: c5b816d74c6f02f85476d16868844f39b4c47996
workflow-type: tm+mt
source-wordcount: '2261'
ht-degree: 43%

---

# アセットの処理メディアハンドラーとワークフローを使用する {#processing-assets-using-media-handlers-and-workflows}

>[!CAUTION]
>
>AEM 6.4 の拡張サポートは終了し、このドキュメントは更新されなくなりました。 詳細は、 [技術サポート期間](https://helpx.adobe.com/jp/support/programs/eol-matrix.html). サポートされているバージョンを見つける [ここ](https://experienceleague.adobe.com/docs/?lang=ja).

Adobe Experience Manager Assets には、アセットを処理するためのデフォルトのワークフローとメディアハンドラーのセットが用意されています。 ワークフローは、一般的なアセット管理および処理タスクを定義し、特定のタスクをメディアハンドラーに委任します。例えば、サムネールの生成やメタデータの抽出などです。

特定のタイプまたは形式のアセットがサーバーにアップロードされたときに自動的に実行されるワークフローを定義できます。 処理手順は、一連の Experience Manager Assets メディアハンドラーとして定義されます。 Adobe Experience Manager [組み込みのハンドラー](#default-media-handlers) また、 [カスタム開発](#creating-a-new-media-handler) または、 [コマンドラインツール](#command-line-based-media-handler).

メディアハンドラーは、アセットに対して特定のアクションを実行するExperience Manager Assets内のサービスです。 例えば、MP3 オーディオファイルがExperience Managerにアップロードされると、ワークフローは、メタデータを抽出してサムネールを生成する MP3 ハンドラーをトリガーします。 メディアハンドラーは、ワークフローで使用します。 最も一般的な MIME タイプは、Experience Manager内でサポートされます。 次のいずれかの操作を行うことで、アセットに対して特定のタスクを実行できます

* ワークフローの拡張または作成。
* メディアハンドラーの拡張または作成。
* メディアハンドラーの無効化または有効化

>[!NOTE]
>
>詳しくは、 [Assets でサポートされる形式](assets-formats.md) ページを参照してください。Experience Manager Assetsでサポートされるすべての形式と、各形式でサポートされる機能について説明します。

## デフォルトのメディアハンドラー {#default-media-handlers}

Experience Manager Assets内では次のメディアハンドラーを使用でき、最も一般的な MIME タイプを処理できます。

| ハンドラー名 | サービス名（システムコンソール内） | サポートされる MIME タイプ |
|---|---|---|
| [!UICONTROL TextHandler] | com.day.cq.dam.core.impl.handler.TextHandler | text/plain |
| [!UICONTROL PdfHandler] | com.day.cq.dam.handler.standard.pdf.PdfHandler | <ul><li>application/pdf</li><li>application/illustrator</li></ul> |
| [!UICONTROL JpegHandler] | com.day.cq.dam.core.impl.handler.JpegHandler | image/jpeg |
| [!UICONTROL Mp3Handler] | com.day.cq.dam.handler.standard.mp3.Mp3Handler | audio/mpeg<br><b>重要</b> - MP3 ファイルをアップロードすると、 [サードパーティのライブラリを使用して処理](https://www.zxdr.it/programmi/SistEvolBDD/LibJava/doc/de/vdheide/mp3/MP3File.html). MP3 に可変ビットレート（VBR）がある場合、ライブラリは不正確なおおよその長さを計算します。 |
| [!UICONTROL ZipHandler] | com.day.cq.dam.handler.standard.zip.ZipHandler | <ul><li>application/java-archive </li><li> application/zip</li></ul> |
| [!UICONTROL PictHandler] | com.day.cq.dam.handler.standard.pict.PictHandler | image/pict |
| [!UICONTROL StandardImageHandler] | com.day.cq.dam.core.impl.handler.StandardImageHandler | <ul><li>image/gif </li><li> image/png </li> <li>application/photoshop </li> <li>image/jpeg </li><li> image/tiff </li> <li>image/x-ms-bmp </li><li> image/bmp</li></ul> |
| [!UICONTROL MSOfficeHandler] | com.day.cq.dam.handler.standard.msoffice.MSOfficeHandler | application/msword |
| [!UICONTROL MSPowerPointHandler] | com.day.cq.dam.handler.standard.msoffice.MSPowerPointHandler | application/vnd.ms-powerpoint |
| [!UICONTROL OpenOfficeHandler] | com.day.cq.dam.handler.standard.ooxml.OpenOfficeHandler | <ul><li>application/vnd.openxmlformats-officedocument.wordprocessingml.document</li><li> application/vnd.openxmlformats-officedocument.spreadsheetml.sheet</li><li> application/vnd.openxmlformats-officedocument.presentationml.presentation</li></ul> |
| [!UICONTROL EPubHandler] | com.day.cq.dam.handler.standard.epub.EPubHandler | application/epub+zip |
| [!UICONTROL GenericAssetHandler] | com.day.cq.dam.core.impl.handler.GenericAssetHandler | アセットからデータを抽出する他のハンドラーが見つからなかった場合のフォールバック |

すべてのハンドラーは、次のタスクを実行します。

* アセットから使用可能なすべてのメタデータを抽出しています。
* アセットからサムネール画像を作成する

アクティブなメディアハンドラーを表示できます。

1. ブラウザーで、`http://localhost:4502/system/console/components` に移動します。
1. リンク `com.day.cq.dam.core.impl.store.AssetStoreImpl` をクリックします。
1. すべてのアクティブなメディアハンドラーリストが表示されます。次に例を示します。

![chlimage_1-437](assets/chlimage_1-437.png)

## ワークフローでメディアハンドラーを使用したアセットに対するタスクの実行 {#using-media-handlers-in-workflows-to-perform-tasks-on-assets}

メディアハンドラーは、ワークフローで使用されるサービスです。

Experience Managerには、アセットを処理するためのデフォルトのワークフローがいくつかあります。 ワークフローを表示するには、ワークフローコンソールを開き、 **[!UICONTROL モデル]** タブ：Experience Manager Assetsで始まるワークフロータイトルは、アセット固有のタイトルです。

特定の要件に従って、既存のワークフローを拡張し、新しいワークフローを作成してアセットを処理できます。

次の例は、 **[!UICONTROL AEM Assets Synchronization]** ワークフローでサブアセットを生成し、PDFドキュメント以外のすべてのアセットに対してサブアセットを生成する。

### メディアハンドラーの無効化／有効化 {#disabling-enabling-a-media-handler}

メディアハンドラーは、Apache Felix Web Management Console を使用して無効または有効にできます。 メディアハンドラーが無効になっている場合、アセットに対してタスクは実行されません。

メディアハンドラーを有効/無効にするには：

1. ブラウザーで、`https://<host>:<port>/system/console/components` に移動します。
1. メディアハンドラーの名前の横にある「**[!UICONTROL Disable]**」をクリックします。例：`com.day.cq.dam.handler.standard.mp3.Mp3Handler`
1. ページを更新します。メディアハンドラーの横に、無効であることを示すアイコンが表示されます。
1. メディアハンドラーを有効にするには、メディアハンドラーの名前の横にある「**[!UICONTROL Enable]**」をクリックします。

### メディアハンドラーの作成 {#creating-a-new-media-handler}

新しいメディアタイプをサポートしたり、アセットに対して特定のタスクを実行したりするには、メディアハンドラーを作成する必要があります。 この節では、手順を説明します。

#### 重要なクラスとインターフェイス {#important-classes-and-interfaces}

実装を開始するための最適な方法は、最も多くの点について対応し、適切なデフォルト動作を提供している付属の抽象実装から継承することです。それが `com.day.cq.dam.core.AbstractAssetHandler` クラスです。

このクラスには、抽象的なサービス記述子が用意されています。そのため、このクラスから継承し、maven-sling-plugin を使用する場合、inherit フラグを `true` に設定する必要があります。

次のメソッドを実装します。

* `extractMetadata()`：使用可能なすべてのメタデータを抽出します。
* `getThumbnailImage()`：渡されたアセットからサムネール画像を作成します。
* `getMimeTypes()`：アセットの MIME タイプを返します。

以下にテンプレートの例を示します。

`package my.own.stuff; /** * @scr.component inherit="true" * @scr.service */ public class MyMediaHandler extends com.day.cq.dam.core.AbstractAssetHandler { // implement the relevant parts } `

インターフェイスとクラスには以下が含まれます。

* `com.day.cq.dam.api.handler.AssetHandler` インターフェイス：特定の MIME タイプのサポートを追加するサービスを記述します。MIME タイプを追加するには、このインターフェイスを実装する必要があります。 このインターフェイスには、特定のドキュメントの読み込みと書き出し、サムネールの作成およびメタデータの抽出をおこなうメソッドがあります。
* `com.day.cq.dam.core.AbstractAssetHandler` クラス：その他すべてのアセットハンドラー実装の基礎として機能し、よく使用される機能を提供します。
* `com.day.cq.dam.core.AbstractSubAssetHandler` クラス：
   * その他すべてのアセットハンドラー実装の基礎として機能し、よく使用される機能を提供します。さらに、サブアセットの抽出についてよく使用される機能も提供します。
   * 実装を開始するための最適な方法は、最も多くの点について対応し、適切なデフォルト動作を提供している付属の抽象実装から継承することです。それが com.day.cq.dam.core.AbstractAssetHandler クラスです。
   * このクラスには、抽象的なサービス記述子が用意されています。したがって、このクラスから継承し、maven-sling-plugin を使用する場合、inherit フラグを true に設定する必要があります。

次のメソッドを実装する必要があります。

* `extractMetadata()`：使用できるすべてのメタデータを抽出します。
* `getThumbnailImage()`：渡されたアセットのサムネール画像を作成します。
* `getMimeTypes()`:このメソッドは、アセットの MIME タイプを返します。

以下にテンプレートの例を示します。

package my.own.stuff; /&amp;ast;&amp;ast; &amp;ast; @scr.component inherit=&quot;true&quot; &amp;ast; @scr.service &amp;ast;/ public class MyMediaHandler extends com.day.cq.dam.core.AbstractAssetHandler { // 関係する部分を実装 }

インターフェイスとクラスには以下が含まれます。

* `com.day.cq.dam.api.handler.AssetHandler` インターフェイス：特定の MIME タイプのサポートを追加するサービスを記述します。MIME タイプを追加するには、このインターフェイスを実装する必要があります。 このインターフェイスには、特定のドキュメントの読み込みと書き出し、サムネールの作成およびメタデータの抽出をおこなうメソッドがあります。
* `com.day.cq.dam.core.AbstractAssetHandler` クラス：その他すべてのアセットハンドラー実装の基礎として機能し、よく使用される機能を提供します。
* `com.day.cq.dam.core.AbstractSubAssetHandler` クラス：その他すべてのアセットハンドラー実装の基礎として機能し、よく使用される機能を提供します。さらに、サブアセットの抽出についてよく使用される機能も提供します。

#### 例：特定のテキストハンドラーを作成する {#example-create-a-specific-text-handler}

この節では、透かし付きのサムネールを生成する特定のテキストハンドラを作成します。

以下の手順を実行します。

参照： [開発ツール](../sites-developing/dev-tools.md) :Maven プラグインを使用して Eclipse をインストールして設定し、Maven プロジェクトに必要な依存関係を設定する場合。

次の手順を実行した後、txt ファイルをExperience Managerにアップロードすると、ファイルのメタデータが抽出され、透かしの付いた 2 つのサムネールが生成されます。

1. Eclipse で、 `myBundle` Maven プロジェクト：

   1. メニューバーで、**[!UICONTROL ファイル／新規／その他]**&#x200B;をクリックします。
   1. ダイアログボックスで、Maven フォルダーを展開し、「Maven プロジェクト」を選択して、 **[!UICONTROL 次へ]**.
   1. 次を確認します。 **[!UICONTROL 単純なプロジェクトの作成]** ボックスと **[!UICONTROL デフォルトの Workspace の場所を使用]** ボックスに移動し、 **[!UICONTROL 次へ]**.
   1. 次の値で Maven プロジェクトを定義します。

      * グループ ID :com.day.cq5.myhandler
      * アーティファクト Id：myBundle
      * 名前：マイExperience Managerバンドル
      * 説明：これは私のExperience Manager束です
   1. 「**[!UICONTROL 終了]**」をクリックします。


1. Java™コンパイラをバージョン 1.5 に設定します。

   1. `myBundle` プロジェクトを右クリックし、プロパティを選択してください。
   1. 「Java™ Compiler」を選択し、次のプロパティを 1.5 に設定します。

      * コンパイラのコンプライアンスレベル
      * 生成された.class ファイルの互換性
      * ソースの互換性
   1. 「**[!UICONTROL OK]**」をクリックします。ダイアログウィンドウで、「はい」をクリックします。


1. pom.xml ファイル内のコードを次のコードに置き換えます。

   ```xml
   <project xmlns="https://maven.apache.org/POM/4.0.0" xmlns:xsi="https://www.w3.org/2001/XMLSchema-instance"
    xsi:schemaLocation="https://maven.apache.org/POM/4.0.0 https://maven.apache.org/maven-v4_0_0.xsd">
    <modelVersion>4.0.0</modelVersion> 
    <!-- ====================================================================== --> 
    <!-- P A R E N T P R O J E C T D E S C R I P T I O N --> 
    <!-- ====================================================================== -->
    <parent>
     <groupId>com.day.cq.dam</groupId>
     <artifactId>dam</artifactId>
     <version>5.2.14</version>
     <relativePath>../parent</relativePath>
    </parent> 
    <!-- ====================================================================== --> 
    <!-- P R O J E C T D E S C R I P T I O N --> 
    <!-- ====================================================================== -->
    <groupId>com.day.cq5.myhandler</groupId>
    <artifactId>myBundle</artifactId>
    <name>My CQ5 bundle</name>
    <version>0.0.1-SNAPSHOT</version>
    <description>This is my CQ5 bundle</description>
    <packaging>bundle</packaging> 
    <!-- ====================================================================== --> 
    <!-- B U I L D D E F I N I T I O N --> 
    <!-- ====================================================================== -->
    <build>
     <plugins>
      <plugin>
       <groupId>org.apache.felix</groupId>
       <artifactId>maven-scr-plugin</artifactId>
      </plugin>
      <plugin>
       <groupId>org.apache.sling</groupId>
       <artifactId>maven-sling-plugin</artifactId>
       <configuration>
        <slingUrlSuffix>/libs/dam/install/</slingUrlSuffix>
       </configuration>
      </plugin>
      <plugin>
       <groupId>org.apache.felix</groupId>
       <artifactId>maven-bundle-plugin</artifactId>
       <extensions>true</extensions>
       <configuration>
        <instructions>
         <Bundle-Category>cq5</Bundle-Category>
         <Export-Package> com.day.cq5.myhandler </Export-Package>
        </instructions>
       </configuration>
      </plugin>
     </plugins>
    </build> 
    <!-- ====================================================================== --> 
    <!-- D E P E N D E N C I E S --> 
    <!-- ====================================================================== -->
    <dependencies>
     <dependency>
      <groupId>com.day.cq.dam</groupId>
      <artifactId>cq-dam-api</artifactId>
      <version>5.2.10</version>
      <scope>provided</scope>
     </dependency>
     <dependency>
      <groupId>com.day.cq.dam</groupId>
      <artifactId>cq-dam-core</artifactId>
      <version>5.2.10</version>
      <scope>provided</scope>
     </dependency>
     <dependency>
      <groupId>com.day.cq</groupId>
      <artifactId>cq-commons</artifactId>
     </dependency>
     <dependency>
      <groupId>javax.jcr</groupId>
      <artifactId>jcr</artifactId>
     </dependency>
     <dependency>
      <groupId>org.apache.felix</groupId>
      <artifactId>org.osgi.compendium</artifactId>
     </dependency>
     <dependency>
      <groupId>org.slf4j</groupId>
      <artifactId>slf4j-api</artifactId>
     </dependency>
     <dependency>
      <groupId>commons-lang</groupId>
      <artifactId>commons-lang</artifactId>
     </dependency>
     <dependency>
      <groupId>commons-collections</groupId>
      <artifactId>commons-collections</artifactId>
     </dependency>
     <dependency>
      <groupId>commons-io</groupId>
      <artifactId>commons-io</artifactId>
     </dependency>
     <dependency>
      <groupId>com.day.commons</groupId>
      <artifactId>day-commons-gfx</artifactId>
     </dependency>
     <dependency>
      <groupId>com.day.commons</groupId>
      <artifactId>day-commons-text</artifactId>
     </dependency>
     <dependency>
      <groupId>com.day.cq.workflow</groupId>
      <artifactId>cq-workflow-api</artifactId>
     </dependency>
     <dependency>
      <groupId>com.day.cq.wcm</groupId>
      <artifactId>cq-wcm-foundation</artifactId>
      <version>5.2.22</version>
     </dependency>
    </dependencies>
   ```

1. パッケージの作成 `com.day.cq5.myhandler` Java™クラスを含む `myBundle/src/main/java`:

   1. myBundle の下の `src/main/java` を右クリックし、「新規」、「パッケージ」の順に選択してください。
   1. `com.day.cq5.myhandler` という名前を付け、「終了」をクリックしてください。

1. Java™クラスの作成 `MyHandler`:

   1. Eclipse で、 `myBundle/src/main/java`、右クリック `com.day.cq5.myhandler` 「パッケージ」、「新規」、「クラス」の順に選択します。
   1. ダイアログウィンドウで、「Java™ Class MyHandler」という名前を付け、「完了」をクリックします。 Eclipse が MyHandler.java ファイルを作成して開きます。
   1. `MyHandler.java` で、既存のコードを以下のコードに置き換えてから、変更内容を保存してください。

   ```java
   package com.day.cq5.myhandler; 
   import java.awt.Color; 
   import java.awt.Rectangle; 
   import java.awt.image.BufferedImage; 
   import java.io.IOException; 
   import java.io.InputStream; 
   import java.io.InputStreamReader; 
   import javax.jcr.Node; 
   import javax.jcr.RepositoryException; 
   import javax.jcr.Session; 
   import org.apache.commons.io.IOUtils; 
   import org.slf4j.Logger; 
   import org.slf4j.LoggerFactory; 
   import com.day.cq.dam.api.metadata.ExtractedMetadata; 
   import com.day.cq.dam.core.AbstractAssetHandler; 
   import com.day.image.Font; 
   import com.day.image.Layer; 
   import com.day.cq.wcm.foundation.ImageHelper; 
   
   /** 
    * The <code>MyHandler</code> can extract text files 
    * @scr.component inherit="true" immediate="true" metatype="false" 
    * @scr.service 
    * 
    **/ 
   
   public class MyHandler extends AbstractAssetHandler { 
    /** * Logger instance for this class. */ 
    private static final Logger log = LoggerFactory.getLogger(MyHandler.class); 
    /** * Music icon margin */ 
    private static final int MARGIN = 10; 
    /** * @see com.day.cq.dam.api.handler.AssetHandler#getMimeTypes() */ 
    public String[] getMimeTypes() {
     return new String[] {"text/plain"}; 
    }
   
    public ExtractedMetadata extractMetadata(Node asset) { 
     ExtractedMetadata extractedMetadata = new ExtractedMetadata(); 
     InputStream data = getInputStream(asset); 
     try { 
      // read text data 
      InputStreamReader reader = new InputStreamReader(data); 
      char[] buffer = new char[4096]; 
      String text = ""; 
      while (reader.read(buffer) != -1) { 
       text += new String(buffer); 
      } 
      reader.close(); 
      long wordCount = this.wordCount(text); 
      extractedMetadata.setProperty("text", text); 
      extractedMetadata.setMetaDataProperty("Word Count",wordCount); 
      setMimetype(extractedMetadata, asset); 
     } catch (Throwable t) { 
      log.error("handling error: " + t.toString(), t); 
     } finally { 
      IOUtils.closeQuietly(data); 
     } 
     return extractedMetadata; } 
    // ----------------------< helpers >---------------------------------------- 
    protected BufferedImage getThumbnailImage(Node node) { 
     ExtractedMetadata metadata = extractMetadata(node); 
     final String text = (String) metadata.getProperty("text"); 
     // create text layer 
     final Layer layer = new Layer(500, 600, Color.WHITE); 
     layer.setPaint(Color.black); 
     Font font = new Font("Arial", 12); 
     String displayText = this.getDisplayText(text, 600, 12); 
     if(displayText!=null && displayText.length() > 0) {
      // commons-gfx Font class would throw IllegalArgumentException on empty or null text 
      layer.drawText(10, 10, 500, 600, displayText, font, Font.ALIGN_LEFT, 0, 0); 
     } 
     // create watermark and merge with text layer 
     Layer watermarkLayer; 
     try { 
      final Session session = node.getSession(); 
      watermarkLayer = ImageHelper.createLayer(session, "/content/dam/geometrixx/icons/certificate.png"); 
      watermarkLayer.setX(MARGIN); 
      watermarkLayer.setY(MARGIN); 
      layer.merge(watermarkLayer); 
     } catch (RepositoryException e) { 
      // TODO Auto-generated catch block 
      e.printStackTrace(); 
     } catch (IOException e) { 
      // TODO Auto-generated catch block 
      e.printStackTrace(); } 
     layer.crop(new Rectangle(510, 600)); 
     return layer.getImage(); } 
    // ---------------< private >----------------------------------------------- 
    /** 
     * This method cuts lines if the text file is too long..
     * * @param text
     * * text to check
     * * @param height
     * * text box height (px)
     * * @param fontheight
     * * font height (px) 
     * * @return the text which will fit into the box 
     */ 
    private String getDisplayText(String text, int height, int fontheight) { 
     String trimmedText = text.trim(); 
     int numOfLines = height / fontheight; 
     String lines[] = trimmedText.split("\n"); 
     if (lines.length <= numOfLines) { 
      return trimmedText; 
     } else { 
      String cuttetText = ""; 
      for (int i = 0; i < numOfLines; i++) { 
       cuttetText += lines[i] + "\n"; 
      } 
      return cuttetText; 
     } 
    } 
    /**
     * * This method counts the number of words in a string 
     * * @param text the String whose words would like to be counted
     * * @return the number of words in the string
     * */ 
    private long wordCount(String text) { 
     // We need to keep track of the last character, if we have two whitespace in a row we don't want to double count.
     // The starting of the document is always a whitespace.
     boolean prevWhiteSpace = true; 
     boolean currentWhiteSpace = true; 
     char c; long numwords = 0; 
     int j = text.length(); 
     int i = 0; 
     while (i < j) { 
      c = text.charAt(i++); 
      if (c == 0) { break; } 
      currentWhiteSpace = Character.isWhitespace(c); 
      if (currentWhiteSpace && !prevWhiteSpace) { numwords++; } 
      prevWhiteSpace = currentWhiteSpace; 
     } 
     // If we do not end with a whitespace then we need to add one extra word.
     if (!currentWhiteSpace) { numwords++; } 
     return numwords; 
    } 
   }
   ```

1. Java™クラスをコンパイルし、バンドルを作成します。

   1. myBundle プロジェクトを右クリックし、「 」を選択します。 **[!UICONTROL 実行ユーザー]**&#x200B;を、 **[!UICONTROL Maven インストール]**.
   1. バンドル `myBundle-0.0.1-SNAPSHOT.jar`（コンパイル済みのクラスが含まれる）が `myBundle/target` の下に作成されます。

1. CRX Explorer で、以下にノードを作成します。 `/apps/myApp`. 名前 = `install`、タイプ = `nt:folder`。
1. バンドル `myBundle-0.0.1-SNAPSHOT.jar` をコピーしてから、`/apps/myApp/install` の下に保存してください（WebDAV などを使用）。これで、新しいテキストハンドラがExperience Managerでアクティブになります。
1. ブラウザーで、Apache Felix Web Management Console を開きます。コンポーネントタブを選択し、デフォルトのテキストハンドラー `com.day.cq.dam.core.impl.handler.TextHandler` を無効にしてください。

## コマンドラインベースのメディアハンドラー {#command-line-based-media-handler}

Experience Managerを使用すると、ワークフロー内で任意のコマンドラインツールを実行して、アセットを変換し（ImageMagick など）、新しいレンディションをアセットに追加できます。 Experience Managerサーバーをホストするディスクにコマンドラインツールをインストールし、ワークフローにプロセスステップを追加して設定します。 呼び出されたプロセス ( `CommandLineProcess`、は、特定の MIME タイプに従ってフィルタリングし、新しいレンディションに基づいて複数のサムネールを作成します。

以下の変換を自動的に実行し、[!DNL Experience Manager Assets] 内に保存することができます。

* [ImageMagick](https://www.imagemagick.org/script/index.php) および [Ghostscript](https://www.ghostscript.com/) を使用した EPS および AI 変換
* [FFmpeg](https://ffmpeg.org/) を使用した FLV ビデオのトランスコーディング
* [LAME](https://lame.sourceforge.io) を使用した MP3 エンコーディング
* [SOX](https://sox.sourceforge.io) を使用したオーディオ処理

>[!NOTE]
>
>非 Windows システムでは、ファイル名に一重引用符（&#39;）を含むビデオアセットのレンディションの生成中に FFMpeg ツールがエラーを返します。ビデオファイル名に一重引用符が含まれている場合は、Experience Managerにアップロードする前に削除します。

`CommandLineProcess` プロセスは、リストに表示されている順序で以下の操作を実行します。

* MIME タイプを指定した場合、そのタイプに従ってファイルをフィルターします。
* Experience Manager・サーバをホストするディスク上に一時ディレクトリを作成します。
* 元のファイルを一時ディレクトリにストリーミングします。
* ステップの引数で定義されたコマンドを実行します。コマンドは、Experience Managerを実行するユーザーの権限を持つ一時ディレクトリ内で実行されます。
* 結果をストリーミングサーバーのレンディションフォルダーにExperience Managerします。
* 一時ディレクトリを削除します。
* 指定した場合、これらのレンディションに基づいてサムネールを作成します。 サムネールの数とサイズは、ステップの引数で定義します。

### ImageMagick の使用例 {#an-example-using-imagemagick}

次の例は、コマンドラインプロセスステップの設定方法を示しています。 MIME タイプ gif または tiff を持つアセットがに追加されるたびに `/content/dam` Experience Managerサーバーで、元の画像の反転画像が 3 つのサムネール (140 x 100、48 x 48、10 x 250) と共に作成されます。

この処理手順を実行するには、ImageMagick を使用します。 ImageMagick を、Experience Manager・サーバをホストするディスクにインストールします。

1. ImageMagick をインストールします。 詳しくは、 [ImageMagick のドキュメント](https://www.imagemagick.org/script/download.php) を参照してください。
1. ツールを設定して、 `convert` コマンドライン上で
1. ツールが適切にインストールされているかどうかを確認するには、コマンド `convert -h` をコマンドラインで実行します。

   コンバートツールの使用可能なすべてのオプションが記載されたヘルプ画面が表示されます。

   >[!NOTE]
   >
   >Windows®の一部のバージョン (Windows® SE など ) では、convert コマンドは、Windows®インストールに含まれるネイティブな変換ユーティリティと競合するので、実行に失敗します。 このような場合は、画像ファイルをサムネールに変換するために使用する ImageMagick ユーティリティの完全パスを指定します。例： `"C:\Program Files\ImageMagick-6.8.9-Q16\convert.exe" -define jpeg:size=319x319 ${filename} -thumbnail 319x319 cq5dam.thumbnail.319.319.png`

1. このツールが正しく実行されていることを確認するには、JPG 画像を作業ディレクトリに追加して、コマンド `convert <image-name>.jpg -flip <image-name>-flipped.jpg` をコマンドラインで実行します。

   反転画像がディレクトリに追加されます。

コマンドラインプロセスのステップを **[!UICONTROL DAM アセット更新]**&#x200B;ワークフローに追加します。

1. **[!UICONTROL ワークフロー]**&#x200B;コンソールを開きます。
1. 「**[!UICONTROL モデル]**」タブで、**[!UICONTROL DAM アセット更新]**&#x200B;モデルを編集します。
1. 以下のように、**[!UICONTROL Web enabled rendition]** ステップの設定を変更します。

   `mime:image/gif,mime:image/tiff,tn:140:100,tn:48:48,tn:10:250,cmd:convert ${directory}/${filename} -flip ${directory}/${basename}.flipped.jpg`

1. ワークフローを保存します。

変更したワークフローをテストするには、`/content/dam` にアセットを追加します。

1. ファイルシステムで、任意の TIFF 画像を取得します。名前を `myImage.tiff` に変更し、WebDAV などを使用して、`/content/dam` にコピーします。
1. **[!UICONTROL CQ5 DAM]** コンソール（例：`http://localhost:4502/libs/wcm/core/content/damadmin.html`）を開きます。
1. アセット `myImage.tiff` を開き、反転画像と 3 つのサムネールが作成されたことを確認します。

#### CommandLineProcess プロセスステップの設定 {#configuring-the-commandlineprocess-process-step}

この節では、**[!UICONTROL の]**&#x200B;プロセス引数`CommandLineProcess`を設定する方法について説明します。値を [!UICONTROL プロセスの引数] コンマを使用し、値を空白で始めないでください。

| 引数のフォーマット | 説明 |
|---|---|
| mime:&lt;mime-type> | オプション引数。アセットの MIME タイプが引数の MIME タイプと同じ場合にプロセスが適用されます。 <br>複数の MIME タイプを定義できます。 |
| tn:&lt;width>:&lt;height> | オプション引数。プロセスにより、引数で定義されたサイズのサムネールが作成されます。<br>複数のサムネールを定義できます。 |
| cmd: &lt;command> | 実行するコマンドを定義します。 この構文はコマンドラインツールによって異なります。1 つのコマンドのみを定義できます。<br>次の変数を使用して、コマンドを作成できます。<br>`${filename}`：入力ファイルの名前（例：original.jpg） <br> `${file}`:入力ファイルの完全パス名 ( 例： /tmp/cqdam0816.tmp/original.jpg ) <br> `${directory}`:入力ファイルのディレクトリ ( 例： /tmp/cqdam0816.tmp ) <br>`${basename}`:拡張子なしの入力ファイル名（例：original） <br>`${extension}`:入力ファイルの拡張子（例：jpg） |

例えば、ImageMagick がExperience Managerサーバーをホストするディスクにインストールされていて、 **CommandLineProcess** 実装として、次の値を **プロセスの引数**:

`mime:image/gif,mime:image/tiff,tn:140:100,tn:48:48,tn:10:250,cmd:convert ${directory}/${filename} -flip ${directory}/${basename}.flipped.jpg`

その場合、ワークフローが実行されると、このステップは `image/gif` または `mime:image/tiff` mime タイプとして。 元の画像の反転画像を作成し、.jpg に変換して、次の 3 つのサムネールを作成します。140 x 100、48 x 48、10 x 250。

ImageMagick を使用して 3 つの標準のサムネールを作成するには、以下の[!UICONTROL プロセス引数]を使用します。

`mime:image/tiff,mime:image/png,mime:image/bmp,mime:image/gif,mime:image/jpeg,cmd:convert ${filename} -define jpeg:size=319x319 -thumbnail "319x319>" -background transparent -gravity center -extent 319x319 -write png:cq5dam.thumbnail.319.319.png -thumbnail "140x100>" -background transparent -gravity center -extent 140x100 -write cq5dam.thumbnail.140.100.png -thumbnail "48x48>" -background transparent -gravity center -extent 48x48 cq5dam.thumbnail.48.48.png`

ImageMagick を使用して Web 対応レンディションを作成するには、以下の[!UICONTROL プロセス引数]を使用します。

`mime:image/tiff,mime:image/png,mime:image/bmp,mime:image/gif,mime:image/jpeg,cmd:convert ${filename} -define jpeg:size=1280x1280 -thumbnail "1280x1280>" cq5dam.web.1280.1280.jpeg`

>[!NOTE]
>
>この `CommandLineProcess` 手順は Assets（タイプのノード）にのみ適用されます `dam:Asset`) またはアセットの子孫。
