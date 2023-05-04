---
title: デバイスグループフィルターの作成
seo-title: Creating Device Group Filters
description: デバイスグループフィルターを作成して、一連のデバイス機能要件を定義する
seo-description: Create a device group filter to define a set of device capability requirements
uuid: 8db98b98-f26d-4924-930a-a682cd7df866
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.4/SITES
topic-tags: mobile-web
content-type: reference
discoiquuid: 4c4a7bc4-3fb1-44c1-823f-d789790f5e06
legacypath: /content/docs/en/aem/6-0/develop/mobile/groupfilters
exl-id: abbbf606-aff2-44b4-b16e-ceb54997115f
source-git-commit: c5b816d74c6f02f85476d16868844f39b4c47996
workflow-type: tm+mt
source-wordcount: '838'
ht-degree: 51%

---

# デバイスグループフィルターの作成{#creating-device-group-filters}

>[!CAUTION]
>
>AEM 6.4 の拡張サポートは終了し、このドキュメントは更新されなくなりました。 詳細は、 [技術サポート期間](https://helpx.adobe.com/jp/support/programs/eol-matrix.html). サポートされているバージョンを見つける [ここ](https://experienceleague.adobe.com/docs/?lang=ja).

>[!NOTE]
>
>Adobeは、単一ページアプリケーションのフレームワークベースのクライアントサイドレンダリング（React など）を必要とするプロジェクトでは、SPA Editor を使用することをお勧めします。 [詳細情報](/help/sites-developing/spa-overview.md)を参照してください。

デバイスグループフィルターを作成して、一連のデバイス機能要件を定義します。 必要なデバイス機能のグループをターゲットにするために必要な数のフィルターを作成します。

組み合わせを使用して機能のグループを定義できるようにフィルターをデザインします。 通常、異なるデバイスグループの機能が重複します。 したがって、複数のデバイスグループ定義で一部のフィルターを使用する場合があります。

作成したフィルターは、 [グループ設定。](/help/sites-developing/mobile.md#creating-a-device-group)

## フィルター Java クラス {#the-filter-java-class}

デバイスグループフィルターは、 [com.day.cq.wcm.mobile.api.device.DeviceGroupFilter](https://helpx.adobe.com/experience-manager/6-4/sites/developing/using/reference-materials/javadoc/index.html?com/day/cq/wcm/mobile/api/device/DeviceGroupFilter.html) インターフェイス。 デプロイすると、実装クラスは、デバイスグループの設定で使用できるフィルターサービスを提供します。

この記事で説明するソリューションでは、Apache Felix Maven SCR Plugin を使用して、コンポーネントとサービスの開発を容易にします。 そのため、サンプルの Java クラスでは `@Component` と `@Service` のアノテーションを使用します。クラスは次の構造を持ちます。

```java
package com.adobe.example.myapp;

import java.util.Map;

import com.day.cq.wcm.mobile.api.device.DeviceGroup;
import com.day.cq.wcm.mobile.api.device.DeviceGroupFilter;

import org.apache.felix.scr.annotations.Component;
import org.apache.felix.scr.annotations.Service;

@Component(metatype = false)
@Service 
public class myDeviceGroupFilter implements DeviceGroupFilter {
 
       public String getDescription() {
  return null;
 }

 public String getTitle() { 
  return null;
 }

 public boolean matches(DeviceGroup arg0, String arg1, Map arg2) { 
  return false;
 }

}
```

次のメソッドのコードを指定する必要があります。

* getDescription:フィルターの説明を返します。 この説明はデバイスグループ設定ダイアログに表示されます。
* getTitle:フィルターの名前を返します。 この名前は、デバイスグループ用のフィルターを選択した場合に表示されます。
* 一致：デバイスに必要な機能があるかどうかを判断します。

### フィルターの名前と説明の指定 {#providing-the-filter-name-and-description}

`getTitle` メソッドと `getDescription` メソッドは、それぞれフィルター名と説明を返します。次のコードは、最も簡単な実装を示しています。

```java
public String getDescription() {
    return "An example device group filter";
}

public String getTitle() { 
 return "myFilter";
}
```

言語を 1 つにするオーサリング環境では、名前と説明のテキストをハードコーディングすれば十分です。 複数言語で使用する場合は、文字列を外部化すること、またはソースコードを再コンパイルせずに文字列を変更できるようにすることを検討します。

### フィルター条件に対する評価 {#evaluating-against-filter-criteria}

デバイスの機能がすべてのフィルター条件を満たす場合、`matches` 関数は `true` を返します。デバイスがグループに属しているかどうかを判断するには、メソッドの引数に指定された情報を評価します。次の値が引数として指定されます。

* DeviceGroup オブジェクト
* ユーザーエージェントの名前
* デバイスの機能を格納する Map オブジェクト。Map のキーは WURFL™ の機能名であり、値は WURFL™ データベースの対応する値です。

[com.day.cq.wcm.mobile.api.devicespecs.DeviceSpecsConstants](https://helpx.adobe.com/experience-manager/6-4/sites/developing/using/reference-materials/javadoc/index.html?com/day/cq/wcm/mobile/api/device/DeviceGroupFilter.html) インターフェイスの静的なフィールドには WURFL™ の機能名のサブセットが含まれます。デバイスの機能の Map から値を取得する場合は、これらのフィールドの定数をキーとして使用します。

例えば、次のコード例では、デバイスが CSS をサポートするかどうかを指定します。

```xml
boolean cssSupport = true;
cssSupport = NumberUtils.toInt(capabilities.get(DeviceSpecsConstants.DSPEC_XHTML_SUPPORT_LEVEL)) > 1;
```

`org.apache.commons.lang.math` パッケージは `NumberUtils` クラスを提供します。

>[!NOTE]
>
>AEM にデプロイされる WURFL™ データベースには、フィルター条件として使用する機能が含まれます（[デバイスの検出](/help/sites-developing/mobile.md#server-side-device-detection)を参照）。

### 画面サイズのフィルターの例 {#example-filter-for-screen-size}

次に示す DeviceGroupFilter の実装例では、デバイスの物理サイズが最小要件を満たしているかどうかを判断します。 このフィルターは、タッチデバイスグループに精度を追加するためのものです。 アプリケーション UI のボタンのサイズは、物理的な画面のサイズに関係なく同じにする必要があります。 他の項目（テキストなど）のサイズは変わる場合があります。 フィルターを使用すると、UI 要素のサイズを制御する特定の CSS を動的に選択できます。

このフィルターは、`physical_screen_height` と `physical_screen_width` の WURFL™ プロパティ名に対してサイズ基準を適用します。

```java
package com.adobe.example.myapp;

import java.util.Map;

import com.day.cq.wcm.mobile.api.device.DeviceGroup;
import com.day.cq.wcm.mobile.api.device.DeviceGroupFilter;

import org.apache.commons.lang.math.NumberUtils;
import org.apache.felix.scr.annotations.Component;
import org.apache.felix.scr.annotations.Service;

@Component(metatype = false)
@Service
@SuppressWarnings("unused")
public class ScreenSizeLarge implements DeviceGroupFilter {
    private int len=400;
    private int wid=200;
    public String getDescription() {

        return "Requires the physical size of the screen to have minimum dimensions " + len + "x" + wid+".";
    }

    public String getTitle() {
        return "Screen Size Large ("+len + "x" + wid+")";
    }

    public boolean matches(DeviceGroup deviceGroup, String userAgent,
            Map<String, String> deviceCapabilities) {

        boolean longEnough=true;
        boolean wideEnough=false;
        int dimension1=NumberUtils.toInt(deviceCapabilities.get("physical_screen_height"));
        int dimension2=NumberUtils.toInt(deviceCapabilities.get("physical_screen_width"));
        if(dimension1>dimension2){
            longEnough=dimension1>=len;
            wideEnough=dimension2>=wid;
        }else{
            longEnough=dimension2>=len;
            wideEnough=dimension1>=wid;
        }

        return longEnough && wideEnough;
    }
}
```

getTitle メソッドが返す文字列値は、デバイスグループのプロパティのドロップダウンリストに表示されます。

![filteraddtogroup](assets/filteraddtogroup.png)

getTitle メソッドと getDescription メソッドが返す文字列値は、デバイスグループの概要ページの下部に表示されます。

![filterdescription](assets/filterdescription.png)

### Maven POM ファイル {#the-maven-pom-file}

次の POM コードは、Maven を使用してアプリケーションをビルドする場合に役立ちます。POM は、必要な複数のプラグインおよび依存関係を参照します。

**プラグイン:**

* Apache Maven Compiler プラグイン：ソースコードから Java クラスをコンパイルします。
* Apache Felix Maven Bundle プラグイン：バンドルとマニフェストを作成します
* Apache Felix Maven SCR プラグイン：コンポーネント記述子ファイルを作成し、service-component マニフェストヘッダーを設定します。

**依存関係：**

* `cq-wcm-mobile-api-5.5.2.jar`：DeviceGroup インターフェイスと DeviceGroupFilter インターフェイスを提供します。

* `org.apache.felix.scr.annotations.jar`：Component アノテーションと Service アノテーションを提供します。

DeviceGroup インターフェイスと DeviceGroupFilter インターフェイスは Day Communique 5 WCM Mobile API バンドルに含まれています。Felix アノテーションは Apache Felix Declarative Services バンドルに含まれています。この JAR ファイルはアドビの公開リポジトリから入手できます。

この記事の作成時点では、最新リリースの AEM に含まれている WCM Mobile API バンドルのバージョンは 5.5.2 です。AdobeWeb コンソール ([http://localhost:4502/system/console/bundles](http://localhost:4502/system/console/bundles)) を使用して、これがお使いの環境にデプロイされるバンドルのバージョンであることを確認します。

**POM：**（ユーザーの POM では別の groupId と version が使用されます。）

```xml
<project xmlns="https://maven.apache.org/POM/4.0.0"
        xmlns:xsi="https://www.w3.org/2001/XMLSchema-instance"
        xsi:schemaLocation="https://maven.apache.org/POM/4.0.0 https://maven.apache.org/xsd/maven-4.0.0.xsd">
      <modelVersion>4.0.0</modelVersion>
      <groupId>com.adobe.example.myapp</groupId>
      <artifactId>devicefilter</artifactId>
      <version>0.0.1-SNAPSHOT</version>
      <name>my app device filter</name>
      <url>https://dev.day.com/docs/en/cq/current.html</url>
  <packaging>bundle</packaging>
<build>
    <plugins>
        <plugin>
            <groupId>org.apache.maven.plugins</groupId>
            <artifactId>maven-compiler-plugin</artifactId>
            <configuration>
                <source>1.5</source>
                <target>1.5</target>
            </configuration>
        </plugin>
        <plugin>
            <groupId>org.apache.felix</groupId>
            <artifactId>maven-scr-plugin</artifactId>
            <executions>
                  <execution>
                    <id>generate-scr-scrdescriptor</id>
                    <goals>
                          <goal>scr</goal>
                    </goals>
                  </execution>
            </executions>
          </plugin>
        <plugin>
            <groupId>org.apache.felix</groupId>
            <artifactId>maven-bundle-plugin</artifactId>
            <version>1.4.3</version>
            <extensions>true</extensions>
            <configuration>
                <instructions>
                    <Export-Package>com.adobe.example.myapp.*;version=${project.version}</Export-Package>
                </instructions>
            </configuration>
        </plugin>
    </plugins>
</build>
<dependencies>
     <dependency>
         <groupId>com.day.cq.wcm</groupId>
         <artifactId>cq-wcm-mobile-api</artifactId>
         <version>5.5.2</version>
         <scope>provided</scope>
     </dependency>
     <dependency>
        <groupId>org.apache.felix</groupId>
        <artifactId>org.apache.felix.scr.annotations</artifactId>
        <version>1.6.0</version>
        <scope>compile</scope>
    </dependency>
</dependencies>
</project>
```

アドビの公開リポジトリを使用するには、[Content Package Maven Plugin の入手](/help/sites-developing/vlt-mavenplugin.md)の節で指定されているプロファイルを Maven 設定ファイルに追加してください。
