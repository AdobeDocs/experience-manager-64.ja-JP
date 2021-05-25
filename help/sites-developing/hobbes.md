---
title: UI のテスト
seo-title: UI のテスト
description: AEM には、AEM UI のテストを自動化するためのフレームワークが用意されています
seo-description: AEM には、AEM UI のテストを自動化するためのフレームワークが用意されています
uuid: b0280a70-643e-4455-82ea-fa7a90823b53
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.4/SITES
content-type: reference
topic-tags: components, testing
discoiquuid: bc0130c3-826e-47dd-b18b-85e1a7bb9936
exl-id: 16b4088d-13b4-47b9-b89d-0c4a13676f12
source-git-commit: bd94d3949f0117aa3e1c9f0e84f7293a5d6b03b4
workflow-type: tm+mt
source-wordcount: '717'
ht-degree: 76%

---

# UI のテスト{#testing-your-ui}

AEM には、AEM UI のテストを自動化するためのフレームワークが用意されています。このフレームワークを使用して、Web ブラウザーで直接 UI テストを記述して実行します。このフレームワークは、テストを作成するためのJavaScript APIを提供します。

AEMテストフレームワークは、JavaScriptで記述されたテストライブラリであるHobbes.jsを使用します。 Hobbes.js フレームワークは、開発プロセスの一環として AEM のテスト用に開発されたものです。このフレームワークは現在、独自の AEM アプリケーションのテスト用に一般に利用できます。

>[!NOTE]
>
>APIの詳細については、Hobbes.jsの[ドキュメント](https://helpx.adobe.com/experience-manager/6-4/sites/developing/using/reference-materials/test-api/index.html)を参照してください。

## テストの構造 {#structure-of-tests}

自動化されたテストを AEM 内で使用する場合は、以下の用語を理解しておくことが重要です。

|  |  |
|---|---|
| 動作 | **アクション**&#x200B;は、リンクやボタンのクリックなど、Webページ上の特定のアクティビティです。 |
| テストケース | **テストケース**&#x200B;は、1つ以上の&#x200B;**アクション**&#x200B;で構成できる特定の状況です。 |
| テストスイート | **テストスイート**&#x200B;は、関連する&#x200B;**テストケース**&#x200B;のグループで、一緒に特定の使用例をテストします。 |

## テストの実行 {#executing-tests}

### テストスイートの表示 {#viewing-test-suites}

テストコンソールを開くと、登録されているテストスイートが表示されます。テストパネルには、テストスイートとそのテストケースのリストが表示されます。

ツールコンソールに移動するには、**グローバルナビゲーション／ツール／運営／テスト**&#x200B;の順に移動します。

![chlimage_1-26](assets/chlimage_1-26.png)

コンソールを開くと、左側には、テストスイートのリストと共に、すべてのテストスイートを順番に実行するためのオプションが表示されます。右側に表示される背景が格子柄のスペースは、テストの実行時にページコンテンツを表示するためのプレースホルダーです。

![chlimage_1-27](assets/chlimage_1-27.png)

### 1 つのテストスイートの実行 {#running-a-single-test-suite}

テストスイートは個別に実行できます。1 つのテストスイートを実行すると、テストケースとそのアクションの実行に応じてページが変化し、テストの完了後に結果が表示されます。アイコンによって結果が示されます。

チェックマークアイコンは、成功したテストを示します。

![](do-not-localize/chlimage_1-5.png)

「X」アイコンは、失敗したテストを示します。

![](do-not-localize/chlimage_1-6.png)

1 つのテストスイートを実行するには：

1. テストパネルで、実行するテストケースの名前をクリックまたはタップして、アクションの詳細を展開します。

   ![chlimage_1-28](assets/chlimage_1-28.png)

1. 「**Run tests**」ボタンをクリックまたはタップします。

   ![](do-not-localize/chlimage_1-7.png)

1. テストが実行されると、プレースホルダーはページコンテンツに置き換えられます。

   ![chlimage_1-29](assets/chlimage_1-29.png)

1. 説明をタップまたはクリックして&#x200B;**結果**&#x200B;パネルを開いて、テストケースの結果を確認します。**結果**&#x200B;パネルでテストケースの名前をタップまたはクリックすると、すべての詳細が表示されます。

   ![chlimage_1-30](assets/chlimage_1-30.png)

### 複数のテストの実行 {#running-multiple-tests}

テストスイートは、コンソールに表示された順番で実行されます。テストをドリルダウンして、詳細な結果を確認できます。

![chlimage_1-31](assets/chlimage_1-31.png)

1. テストパネルで、実行するテストスイートのタイトルの下にある「**Run all tests**」ボタンまたは「**Run tests**」ボタンをタップまたはクリックします。

   ![](do-not-localize/chlimage_1-8.png)

1. 各テストケースの結果を表示するには、そのテストケースのタイトルをタップまたはクリックします。**結果**&#x200B;パネルでテストの名前をタップまたはクリックすると、すべての詳細が表示されます。

   ![chlimage_1-32](assets/chlimage_1-32.png)

## シンプルなテストスイートの作成と使用 {#creating-and-using-a-simple-test-suite}

以下の手順では、[We.Retailコンテンツ](/help/sites-developing/we-retail.md)を使用してテストスイートを作成および実行する手順を説明しますが、別のWebページを使用するようにテストを簡単に変更できます。

独自のテストスイートの作成について詳しくは、[Hobbes.js API のドキュメント](https://helpx.adobe.com/experience-manager/6-4/sites/developing/using/reference-materials/test-api/index.html)を参照してください。

1. CRXDE Lite を開きます。([http://localhost:4502/crx/de](http://localhost:4502/crx/de))
1. `/etc/clientlibs`フォルダーを右クリックし、**作成/フォルダーを作成**&#x200B;をクリックします。 名前に`myTests`と入力して、「**OK**」をクリックします。
1. `/etc/clientlibs/myTests`フォルダーを右クリックし、**作成/ノードを作成**&#x200B;をクリックします。 以下のプロパティ値を使用して「**OK**」をクリックします。

   * 名前：`myFirstTest`
   * 型：`cq:ClientLibraryFolder`

1. myFirstTest ノードに次のプロパティを追加します。

   | 名前 | タイプ | 値 |
   |---|---|---|
   | `categories` | `String[]` | `granite.testing.hobbes.tests` |
   | `dependencies` | `String[]` | `granite.testing.hobbes.testrunner` |

   >[!NOTE]
   >
   >**AEM Forms のみ**
   >
   >アダプティブフォームをテストするには、categories と dependencies に次の値を追加してください。次に例を示します。
   >
   >**カテゴリ**:  `granite.testing.hobbes.tests, granite.testing.hobbes.af.commons`
   >
   >**依存関係**:  `granite.testing.hobbes.testrunner, granite.testing.hobbes.af`

1. 「**すべて保存**」をクリックします。
1. `myFirstTest` ノードを右クリックして、**作成／ファイルを作成**&#x200B;をクリックします。ファイル名に`js.txt`と入力して、「**OK**」をクリックします。
1. `js.txt` ファイルに次のテキストを入力します。

   ```
   #base=.
   myTestSuite.js
   ```

1. 「**すべて保存**」をクリックして、`js.txt` ファイルを閉じます。
1. `myFirstTest` ノードを右クリックして、**作成／ファイルを作成**&#x200B;をクリックします。ファイル名に`myTestSuite.js`と入力して、「**OK**」をクリックします。
1. `myTestSuite.js` ファイルに次のコードをコピーして、ファイルを保存します。

   ```
   new hobs.TestSuite("Experience Content Test Suite", {path:"/etc/clientlibs/myTests/myFirstTest/myTestSuite.js"})
      .addTestCase(new hobs.TestCase("Navigate to Experience Content")
         .navigateTo("/content/we-retail/us/en/experience/arctic-surfing-in-lofoten.html")
      )
      .addTestCase(new hobs.TestCase("Hover Over Topnav")
         .mouseover("li.visible-xs")
      )
      .addTestCase(new hobs.TestCase("Click Topnav Link")
         .click("li.active a")
   );
   ```

1. **テスト**&#x200B;コンソールに移動して、テストスイートを実行します。
