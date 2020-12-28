---
title: AEM 6.4の既知の問題
seo-title: AEM 6.4の既知の問題
description: Adobe Experience Manager6.4の既知の問題
seo-description: Adobe Experience Manager6.4の既知の問題
uuid: 1733f15e-9c4f-4db3-98ee-25c2ea606f0d
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.4
topic-tags: release-notes
content-type: reference
discoiquuid: 266634ab-21d3-4aac-acfa-b799a7485507
translation-type: tm+mt
source-git-commit: f8ba597c62379ba413309303c2ad066ab7afce1e
workflow-type: tm+mt
source-wordcount: '1040'
ht-degree: 44%

---


# 既知の問題 {#known-issues}

このページは、2018年4月にリリースされた既知の問題のリストをAdobe Experience Manager6.4に掲載しています。 既知の問題の詳細については、[サポート](https://helpx.adobe.com/jp/support/experience-manager.html)にお問い合わせください。

## ハイブリッドデバイス {#hybrid-devices}

ハイブリッドデバイスはサポートされません。こうしたデバイスを使用するときは多様な問題が発生する恐れがあります。次の推奨手順は、多くの問題の解決に役立ちます。

Google Chromeをブラウザーとして使用している場合：

* アドレスバーに「`chrome://flags/`」と入力し、Enterキーを押します。
* タッチイベントを有効にする/無効をクリックします。
* ブラウザーを再起動します（すべてのタブとウィンドウ）。

Mozilla Firefoxをブラウザーとして使用している場合：

* アドレスバーに「`about:config`」と入力し、Enterキーを押します。
* 設定を`dom.w3c`にフィルターします。
* 設定が`0`と`false`であることを確認します。
* ブラウザーを再起動します。

Microsoft Edgeをブラウザーとして使用する場合：

* アドレスバーに「`about:flags`」と入力し、Returnキーを押します。
* 「Experimental features（試験的な機能）」までスクロールし、**[!UICONTROL Touch]**&#x200B;を選択します。
* 「**[!UICONTROL タッチイベントを有効にする]**」をクリックします。
* 「**[!UICONTROL 常にオフ]**」を選択します。
* ブラウザーを再起動します。

## プラットフォーム {#platform}

* **操作ダッシュボード：**&#x200B;バックアップファイルに .zip 拡張子がない場合、プログレスバーが表示されない。（GRANITE-10713）
* **HTL:** Java Useオブジェクトのパッケージ宣言の末尾に空白文字が含まれていると、SightlyJavaCompilerService(GRANITE-20836)がフリーズする
* **Apache Felix/Sling:** Configファイルは、configuration.delete()の後でもリポジトリ内に存在します(GRANITE-20618)
* **Cloud Settings：設定** コンテナの編集後、コンソールが壊れる(GRANITE-20726)
* **セキュリティ：** IMS統合がカスタムコンテキストパスで失敗する(GRANITE-20639)
* **セキュリティ：SSO、外部およびデフォルトのLoginModulesのデフォルトのJAASランクの** 向上(GRANITE-20590)
* **ツール — CRX DE Lite:** Ridge of properties表示が上に移動し続ける(GRANITE-12040)
* **ツール — CRX DE Lite：プロパティ名(GRANITE-12351)を重複** クリックしない限り、「Long」値タイプに対する変更を保存できません。

* **ツール — CRX DE Lite:** ctrl+Fで、開いているテキストファイルの検索がRegExp検索で停止する(GRANITE-5996)

* **ツール — CRX DE Lite:** Nodeプロパティがノード名の変更後に表示されない(GRANITE-7160)
* **UI:** プルダウン「more...」 IEおよびFirefoxのPover要素で開いた場合に、すべての要素が表示されない(GRANITE-16326)
* **UI:** 情報ツールチップが、2列の並び方を持つ固定列レイアウトを使用する場合に非表示になる(GRANITE-16869)
* **UI：**&#x200B;存在しない別のユーザーとして実行している場合に未処理のエラーが発生する（GRANITE-23228）。[エラーハンドラーを実装して](/help/sites-developing/customizing-errorhandler-pages.md)エラーメッセージをカスタマイズすることで回避します。

* **Omnisearch：バックスラッシュを使用した** 検索は例外を引き起こします(GRANITE-11769)
* **Omnisearch:リスト表示で「表示設定」を** 開くと、検索フィルタが変更されます(GRANITE-16524)
* **Omnisearch:SitesからAssets検索を実行すると、列の設定の** 誤ったリストが表示される(GRANITE-16527)

* **オムニサーチ：**&#x200B;左レールの述語がオムニサーチサーバーの要求に影響されてしまう（GRANITE-20524）
* **Omnisearch:** Omnisearchはコンテキストパスをサポートしていません(GRANITE-16044)

## Assets {#assets}

* **検索**:検索文字列開始に空白 [OAK-4786が含まれる場合、検索で結果が返されません。](https://issues.apache.org/jira/browse/OAK-4786)

* **検索**:クラシックUIでは、タグは検索に表示されません(CQ-4235239)

* **UI**:Copy-PasteとSelect-Allの後にアセットUIが応答しなくなる(CQ-4236142)

* **UI**:遅延読み込み後にアセットを移動できない(CQ-4236134)

* **レポート**:アセット変更レポートの作成でエラーが発生しました。(CQ-4239744)

* **レポート**:定期的な通常のアセットレポートの生成に一貫性がなく失敗する（一部のレポートはキューに登録されたままになる）(CQ-4239089)

* **メタデータ**:複数値のテキストフィールドをアセットスキーマに追加すると、必須フィールドのカスケードルールが機能しない(CQ-4239333)

* **BrandPortal**:Brand Portalへの公開がコレクションで機能しない(CQ-4238731)

* **アップロード**：ファイル名に特殊文字を含むアセットをアップロードする場合、許可されていない文字に関する検証エラーメッセージは、すべてのアセットに対して表示されるわけではありません。この検証エラーメッセージは、最初のアセットに対してのみ表示され、提供されたアセットのファイル名が許可されないということがユーザーに明確に示されます。（CQ-4256876）

## Communities {#communities}

* **モデレート**：一括モデレート UI から 1 回の削除操作で親投稿を削除できない（CQ-4236797）

* **コンソール** - [ユーザ名を忘れた場合]または[パスワードを忘れた場合]のリンクが、対応するパスワード取得フォームではなく、ログインページにリダイレクトされる(CQ-4237682)

## フォーム {#forms}

### インストールとデプロイメント

* （AEM Forms JEE の場合のみ）設定マネージャーの実行中に JBoss アプリケーションサーバーをブートストラップすると、EJB 呼び出しおよびブートストラップの失敗エラーが返される。ただし、それらは無視できます（参照 # CQ-4229793）。
* AEM Formsが起動すると、`SAX Security Manager could not be setup`警告が表示されます。 （CQ-4297403）

### インタラクティブコミュニケーション

* グラフ要素や画像要素を含んだインタラクティブコミュニケーションをエージェント UI で読み込むのに時間がかかる（CQ-4236630）
* 印刷プレビューのデータ表示形式はdd-mm-yyyyですが、Webプレビューーのデータ表示形式は`dd-mmm-yy`です(CQ-4237045)
* インタラクティブコミュニケーション Web チャネルが順序付きおよび順序なしリストしかサポートしない。リストドキュメントフラグメントで、インタラクティブコミュニケーションの Web チャネルについて複雑なリストとインデントがサポートされない（CQ-4233672）
* Web チャネルを印刷チャネルに同期させる場合、以下の問題が発生します。

   * 印刷チャネルから Web チャネルに初めて切り替えるときに同期に時間がかかる。
   * 印刷チャネルに未設定のグラフコンポーネントが含まれている場合、Web チャネルが同期しない。この問題を解決するには、グラフコンポーネントを削除して同期し直す必要があります。
   * 「ライブコピーの同期中にエラーが発生しました」というエラーが発生して同期に失敗する場合があります。 この問題を解決するには、ページを更新する必要があります。
   * 印刷チャネルテンプレートでテーブルの第 1 列がヘッダー列になっている場合、レイアウトフラグメント内の静的テキストがテーブルのセル名に置き換わる。
   * Web チャネルコミュニケーションの下部以外の場所にコンポーネントまたはアセットを追加できない。別の場所に配置するには、Web チャネルの下部にパネルを追加し、コンテンツツリーを使用して順序を変更する必要があります。
   * ライブコピーの継承を削除せずに、Web チャネルの継承されたターゲット領域にコンテンツを移動できる

（CQ-4239780）

### データ統合

* SOAP ベース Web サービスの認証設定が表示されないので、クラウドサービスで設定できない。この問題を解決するには、以下の手順を実行する必要があります。

   1. CRXDE Liteコンソールで、次のノードに移動します。\
      /libs/fd/fdm/gui/components/admin/fdmcloudservice/createcloudconfigwizard/cloudservices/\
      wsdlauthenticationsettings/items/fixedcolumns/items/items/items/items/wsdl/items/\
      selectAuthentication/items/custom.
   1. valueプロパティの値をtextプロパティの値と同じに更新します。
   1. 「すべて保存」をクリックして設定を保存します。

（CQ-4238462）

### Adobe Sign との統合

* Adobe Sign スケジューラーが断続的に機能しなくなるので、署名中のフォームが送信に移動しない。この問題を解決するには、AEM Webコンソール(https://[*server*]:[*port*]/system/console/bundles)から&#x200B;**Apache Slingスケジューラーサポート**&#x200B;バンドルを再起動します。

### アダプティブフォームの作成

* アダプティブフォームのグラフコンポーネントが通常より多くの領域を占有する。
* アダプティブフォーム、アダプティブフォームフラグメント、またはインタラクティブ通信のプロパティをFormsマネージャーUIに保存すると、例外が返されます。
* Samsung の Android 6.0 デバイスでは、アダプティブフォームのテキストボックスに指定された最大文字数が適用されない（参照 # CQ-4235205）。
