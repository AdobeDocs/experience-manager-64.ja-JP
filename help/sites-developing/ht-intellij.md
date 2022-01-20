---
title: IntelliJ IDEA を使用して AEM プロジェクトを開発する方法
seo-title: How to Develop AEM Projects using IntelliJ IDEA
description: IntelliJ IDEA を使用した AEM プロジェクトの開発
seo-description: Using IntelliJ IDEA to develop AEM projects
uuid: 382b5008-2aed-4e08-95be-03c48f2b549e
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.4/SITES
topic-tags: development-tools
content-type: reference
discoiquuid: df6410a2-794e-4fa2-ae8d-37271274d537
exl-id: 274b3a33-3267-41ee-bdcd-351787152570
source-git-commit: bd94d3949f0117aa3e1c9f0e84f7293a5d6b03b4
workflow-type: tm+mt
source-wordcount: '642'
ht-degree: 63%

---

# IntelliJ IDEA を使用して AEM プロジェクトを開発する方法{#how-to-develop-aem-projects-using-intellij-idea}

## 概要 {#overview}

IntelliJ で AEM の開発を開始するには、次の手順を実行する必要があります。

各手順の詳細については、このページで後述します。

* IntelliJ のインストール
* Maven に基づく AEM プロジェクトの設定
* Maven POM での IntelliJ 用の JSP サポートの準備
* IntelliJ への Maven プロジェクトの読み込み

>[!NOTE]
>
>このガイドは IntelliJ IDEA Ultimate Edition 12.1.4 と AEM 5.6.1 を基に作成されています。

### IntelliJ IDEA のインストール {#install-intellij-idea}

[JetBrains のダウンロードページ](https://www.jetbrains.com/idea/download/index.html)から IntelliJ IDEA をダウンロードします。

そのページのインストール手順に従ってください。

### Maven に基づく AEM プロジェクトの設定 {#set-up-your-aem-project-based-on-maven}

次に、 [Apache Maven を使用したAEMプロジェクトの構築方法](/help/sites-developing/ht-projects-maven.md).

IntelliJ IDEA でAEMプロジェクトの操作を開始するには、 [5 分ではじめに](https://maven.apache.org/guides/getting-started/maven-in-five-minutes.html) で十分です。

### IntelliJ IDEA 用の JSP サポートの準備 {#prepare-jsp-support-for-intellij-idea}

IntelliJ IDEA では JSP との連携もサポートされます。サポートされる項目の例を次に示します。

* タグライブラリのオートコンプリート
* ～によって定義された物体への意識 `<cq:defineObjects />` および `<sling:defineObjects />`

これが機能するには、 [JSP の使用方法](/help/sites-developing/ht-projects-maven.md#how-to-work-with-jsps) in [Apache Maven を使用したAEMプロジェクトの構築方法](/help/sites-developing/ht-projects-maven.md).

### Maven プロジェクトの読み込み {#import-the-maven-project}

1. を開きます。 **インポート** IntelliJ IDEA のダイアログ

   * 選択 **プロジェクトを読み込み** まだプロジェクトを開いていない場合は、ようこそ画面で
   * 選択 **ファイル —> プロジェクトを読み込み** メインメニューから

1. Import ダイアログで、プロジェクトの POM ファイルを選択します。

   ![chlimage_1-45](assets/chlimage_1-45.png)

1. 次のダイアログに示すデフォルト設定を使用して続行します。

   ![chlimage_1-46](assets/chlimage_1-46.png)

1. 次のダイアログで、 **次へ** および **完了**.
1. これで、IntelliJ IDEA を使用した AEM 開発用の設定は完了です。

   ![chlimage_1-47](assets/chlimage_1-47.png)

### IntelliJ IDEA による JSP のデバッグ {#debugging-jsps-with-intellij-idea}

IntelliJ IDEA を使用して JSP をデバッグするには、次の手順をおこなう必要があります。

* プロジェクトでの Web ファセットの設定
* JSR45 サポートプラグインのインストール
* デバッグプロファイルの設定
* デバッグモード用の AEM の設定

#### プロジェクトでの Web ファセットの設定 {#set-up-a-web-facet-in-the-project}

デバッグ用の JSP を検索する場所を IntelliJ IDEA で認識する必要があります。IDEA では `content-package-maven-plugin` 設定を解釈できないので、これを手動で設定する必要があります。

1. に移動します。 **ファイル —> プロジェクト構造**
1. を選択します。 **コンテンツ** モジュール
1. クリック **+** モジュールのリストの上にあるを選択し、 **Web**
1. 「Web リソースディレクトリ」として、 `content/src/main/content/jcr_root subdirectory` の名前を指定します。

![chlimage_1-48](assets/chlimage_1-48.png)

#### JSR45 サポートプラグインのインストール {#install-the-jsr-support-plugin}

1. 次に移動： **プラグイン** IntelliJ IDEA 設定のウィンドウ
1. 次に移動： **JSR45 統合** プラグインを使用し、横のチェックボックスをオンにします。
1. クリック **適用**
1. 再起動するよう要求されたら、IntelliJ IDEA を再起動します。

![chlimage_1-49](assets/chlimage_1-49.png)

#### デバッグプロファイルの設定 {#configure-a-debug-profile}

1. に移動します。 **実行/設定を編集**
1. ヒット **+** を選択し、 **JSR45 リモート**
1. 設定ダイアログで、「 」を選択します。 **設定** 次の **アプリケーションサーバー** 汎用サーバーの設定
1. デバッグの開始時にブラウザーを開く場合は、開始ページを適切な URL に設定します。
1. すべてを削除 **起動前** vlt 自動同期を使用する場合はタスク、使用しない場合は適切な Maven タスクを設定します
1. の **起動/接続** パネル、必要に応じてポートを調整
1. IntelliJ IDEA が処理するコマンドライン引数をコピーします。

![chlimage_1-50](assets/chlimage_1-50.png) ![chlimage_1-51](assets/chlimage_1-51.png)

#### デバッグモード用の AEM の設定 {#configure-aem-for-debug-mode}

必要な最後の手順は、IntelliJ IDEA が推奨する JVM オプションを指定して AEM を起動することです。

そのためには、AEM jar ファイルを直接起動して、これらのオプションを追加します。例えば、次のコマンドラインを使用します。

`java -Xdebug -Xrunjdwp:transport=dt_socket,address=58242,suspend=n,server=y -Xmx1024m -XX:MaxPermSize=256M -jar cq-quickstart-5.6.1.jar`

また、次に示すように、`crx-quickstart/bin/start` の起動スクリプトにこれらのオプションを追加することもできます。

```shell
# ...

# default JVM options
if [ -z "$CQ_JVM_OPTS" ]; then
 CQ_JVM_OPTS='-server -Xmx1024m -XX:MaxPermSize=256M -Djava.awt.headless=true'
fi

CQ_JVM_OPTS="$CQ_JVM_OPTS -Xdebug -Xrunjdwp:transport=dt_socket,address=58242,suspend=n,server=y"

# ...
```

#### デバッグの開始 {#start-debugging}

これで、AEM における JSP のデバッグ用の設定はすべて完了です。

1. 選択 **Run -> Debug -> Your Debug Profile**
1. コンポーネントのコードにブレークポイントを設定します。
1. ブラウザーでページにアクセスします。

![chlimage_1-52](assets/chlimage_1-52.png)

### IntelliJ IDEA によるバンドルのデバッグ {#debugging-bundles-with-intellij-idea}

標準の汎用リモートデバッグ接続を使用して、バンドル内のコードをデバッグできます。[リモートデバッグに関する Jetbrain のドキュメント](https://www.jetbrains.com/idea/webhelp/run-debug-configuration-remote.html)の手順に従ってください。
