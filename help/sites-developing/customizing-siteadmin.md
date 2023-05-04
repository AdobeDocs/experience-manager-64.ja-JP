---
title: Web サイトコンソールのカスタマイズ（クラシック UI）
seo-title: Customizing the Websites Console (Classic UI)
description: Web サイト管理コンソールを拡張して、カスタム列を表示できます
seo-description: The Websites Administration console can be extended to display custom columns
uuid: 7587d026-f974-46fe-bac3-3872d3a083ab
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.4/SITES
topic-tags: extending-aem
content-type: reference
discoiquuid: 73e57f20-4022-46ab-aa5c-ec866298b645
exl-id: c7e37599-0712-44cf-8191-d444d12f95c4
source-git-commit: c5b816d74c6f02f85476d16868844f39b4c47996
workflow-type: tm+mt
source-wordcount: '817'
ht-degree: 63%

---

# Web サイトコンソールのカスタマイズ（クラシック UI）{#customizing-the-websites-console-classic-ui}

>[!CAUTION]
>
>AEM 6.4 の拡張サポートは終了し、このドキュメントは更新されなくなりました。 詳細は、 [技術サポート期間](https://helpx.adobe.com/jp/support/programs/eol-matrix.html). サポートされているバージョンを見つける [ここ](https://experienceleague.adobe.com/docs/?lang=ja).

## Web サイト (siteadmin) コンソールへのカスタム列の追加 {#adding-a-custom-column-to-the-websites-siteadmin-console}

Web サイト管理コンソールを拡張して、カスタム列を表示できます。 このコンソールは JSON オブジェクトをベースに構築されており、これを拡張するには `ListInfoProvider` インターフェイスを実装する OSGI サービスを作成します。こうしたサービスが、コンソール構築のためにクライアントに送信される JSON オブジェクトを修正します。

このステップバイステップのチュートリアルでは、`ListInfoProvider` インターフェイスを実装して web サイト管理コンソールに新しい列を表示する方法について説明します。次の手順で構成されます。

1. [OSGi サービスの作成](#creating-the-osgi-service) をクリックし、それを含むバンドルをAEMサーバーにデプロイします。
1. （オプション） [新しいサービスのテスト](#testing-the-new-service) コンソールの構築に使用される JSON オブジェクトをリクエストする JSON 呼び出しを発行する。
1. リポジトリー内のコンソールのノード構造を拡張して、[新しい列を表示](#displaying-the-new-column)します。

>[!NOTE]
>
>このチュートリアルは、次の管理コンソールを拡張する場合にも使用できます。
>
>* デジタルアセットコンソール
>* コミュニティコンソール
>


### OSGI サービスの作成 {#creating-the-osgi-service}

`ListInfoProvider` インターフェイスは、次の 2 つのメソッドを定義します。

* リストのグローバルプロパティを更新する `updateListGlobalInfo`
* 単一のリスト項目を更新する `updateListItemInfo`

どちらのメソッドにも次の引数があります。

* `request`：関連付けられた Sling HTTP リクエストオブジェクト
* `info`：更新する JSON オブジェクト。グローバルリストまたは現在のリスト項目に 1 つずつ
* `resource`：Sling リソース

次の実装例では、

* 各項目に *starred* プロパティを追加します。これは、ページ名が「*e*」で始まる場合は `true` で、それ以外は `false` です。

* を追加します。 *starredCount* プロパティ。リスト用にグローバルで、開始リスト項目の数を含みます。

OSGi サービスを作成するには：

1. CRXDE Lite [バンドルを作成](/help/sites-developing/developing-with-crxde-lite.md#managing-a-bundle).
1. 以下のサンプルコードを追加します。
1. バンドルをビルドします。

新しいサービスが起動し、実行されます。

```java
package com.test;

import com.day.cq.commons.ListInfoProvider;
import com.day.cq.i18n.I18n;
import com.day.cq.wcm.api.Page;
import org.apache.felix.scr.annotations.Component;
import org.apache.felix.scr.annotations.Service;
import org.apache.sling.api.SlingHttpServletRequest;
import org.apache.sling.api.resource.Resource;
import org.apache.sling.commons.json.JSONException;
import org.apache.sling.commons.json.JSONObject;

@Component(metatype = false)
@Service(value = ListInfoProvider.class)
public class StarredListInfoProvider implements ListInfoProvider {

    private int count = 0;

    public void updateListGlobalInfo(SlingHttpServletRequest request, JSONObject info, Resource resource) throws JSONException {
        info.put("starredCount", count);
        count = 0; // reset for next execution
    }

    public void updateListItemInfo(SlingHttpServletRequest request, JSONObject info, Resource resource) throws JSONException {
        Page page = resource.adaptTo(Page.class);
        if (page != null) {
            // Consider starred if page name starts with 'e'
            boolean starred = page.getName().startsWith("e");
            if (starred) {
                count++;
            }
            I18n i18n = new I18n(request);
            info.put("starred", starred ? i18n.get("Yes") : i18n.get("No"));
        }
    }

}
```

>[!CAUTION]
>
>* 指定されたリクエストやリソースに基づいて、情報を JSON オブジェクトに追加すべきかどうかを実装環境に応じて判断する必要があります。
>* `ListInfoProvider` の実装が、応答オブジェクト内に既に存在するプロパティを定義している場合、そのプロパティの値は、指定した値で上書きされます。\
   >  [サービスランキング](https://www.osgi.org/javadoc/r2/org/osgi/framework/Constants.html#SERVICE_RANKING)を使用して、複数の `ListInfoProvider` 実装の実行順序を管理できます。
>


### 新しいサービスのテスト {#testing-the-new-service}

Web サイト管理コンソールを開き、サイトを閲覧すると、ブラウザーは、コンソールの構築に使用される JSON オブジェクトを取得するための ajax 呼び出しを発行します。 例えば、`/content/geometrixx` フォルダーを閲覧すると、コンソールを構築するために、次のリクエストが AEM サーバーに送信されます。

[http://localhost:4502/content/geometrixx.pages.json?start=0&amp;limit=30&amp;predicate=siteadmin](http://localhost:4502/content/geometrixx.pages.json?start=0&amp;limit=30&amp;predicate=siteadmin)

新しいサービスを含むバンドルのデプロイ後に、そのサービスが実行されていることを確認するには、以下を行います。

1. ブラウザーで次の URL を参照します。

   [http://localhost:4502/content/geometrixx.pages.json?start=0&amp;limit=30&amp;predicate=siteadmin](http://localhost:4502/content/geometrixx.pages.json?start=0&amp;limit=30&amp;predicate=siteadmin)

1. 応答があり、新しいプロパティが次のように表示されます。

![screen_shot_2012-02-13at163046](assets/screen_shot_2012-02-13at163046.png)

### 新しい列の表示 {#displaying-the-new-column}

最後の手順では、`/libs/wcm/core/content/siteadmin` のオーバーレイによってすべての Geometrixx ページで新しいプロパティを表示するよう、web サイト管理コンソールのノード構造を適応させます。以下の手順を実行します。

1. CRXDE Lite で、タイプ `sling:Folder` のノードを使用してノード構造 `/apps/wcm/core/content` を作成し、構造 `/libs/wcm/core/content` を反映します。

1. ノード `/libs/wcm/core/content/siteadmin` をコピーし、以下 `/apps/wcm/core/content` に貼り付けます。

1. ノード `/apps/wcm/core/content/siteadmin/grid/assets` から `/apps/wcm/core/content/siteadmin/grid/geometrixx` にコピーし、プロパティを変更します。

   * **pageText** を削除
   * 設定 **pathRegex** から `/content/geometrixx(/.*)?`

      これにより、すべての geometrixx Web サイトでグリッド設定がアクティブになります。

   * **storeProxySuffix** を `.pages.json` に設定
   * 複数値プロパティ **storeReaderFields** を編集し、`starred` 値を追加します。
   * MSM 機能をアクティベートするには、次の MSM パラメーターを複数文字列プロパティ **storeReaderFields** に追加します。

      * **msm:isSource**
      * **msm:isInBlueprint**
      * **msm:isLiveCopy**

1. （タイプ **nt:unstructured** の）`starred` ノードを、次のプロパティを設定して `/apps/wcm/core/content/siteadmin/grid/geometrixx/columns` の下に追加します。

   * **dataIndex**：文字列タイプの `starred`
   * **ヘッダー**：文字列タイプの `Starred`
   * **xtype**：文字列タイプの `gridcolumn`

1. （オプション）表示したくない列を `/apps/wcm/core/content/siteadmin/grid/geometrixx/columns` でドロップします。

1. `/siteadmin` は、デフォルトとして `/libs/wcm/core/content/siteadmin` を指すバニティーパスです。

   このパスを `/apps/wcm/core/content/siteadmin` のサイト管理のバージョンにリダイレクトするには、プロパティ `sling:vanityOrder` が `/libs/wcm/core/content/siteadmin` で定義されているより大きい値を持つように定義します。デフォルト値は 300 なので、それより大きい値が適しています。

1. Web サイト管理コンソールに移動し、次の Geometrixx サイトに移動します。 

   [http://localhost:4502/siteadmin#/content/geometrixx](http://localhost:4502/siteadmin#/content/geometrixx).

1. **Starred** という新しい列が使用可能になり、次のようにカスタム情報が表示されます。

![screen_shot_2012-02-14at104602](assets/screen_shot_2012-02-14at104602.png)

>[!CAUTION]
>
>複数のグリッド設定が、 **pathRegex** プロパティの先頭にあるプロパティが使用され、最も具体的なプロパティではありません。つまり、設定の順序が重要です。

### サンプルパッケージ {#sample-package}

このチュートリアルの結果は、Package Share の [Web サイト管理コンソールのカスタマイズ](http://localhost:4502/crx/packageshare/index.html/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/helper/customizing-siteadmin)で入手できます。
