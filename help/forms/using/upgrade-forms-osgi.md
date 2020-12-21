---
title: AEM 6.4 Forms へのアップグレード
seo-title: AEM 6.4 Forms へのアップグレード
description: 'AEM 6.1 Forms、AEM 6.2 Forms、LiveCycle ES4 SP1 を、AEM 6.3 Forms に直接アップグレードすることができます。 '
seo-description: 'AEM 6.1 Forms、AEM 6.2 Forms、LiveCycle ES4 SP1 を、AEM 6.3 Forms に直接アップグレードすることができます。 '
uuid: 1435246a-9215-4d88-b52c-59a5c329bb77
content-type: reference
products: SG_EXPERIENCEMANAGER/6.3/FORMS
topic-tags: installing
geptopics: SG_AEMFORMS/categories/jee
discoiquuid: e745033f-8015-4fae-9d82-99d35802c0a6
translation-type: tm+mt
source-git-commit: 6a8fa45ec61014acebe09048066972ecb1284641
workflow-type: tm+mt
source-wordcount: '849'
ht-degree: 82%

---


# OSGi 上の AEM 6.4 Forms へのアップグレード {#upgrade-to-aem-forms-osgi}

ご使用の環境に合わせて、次のアップグレードパスのいずれかを使用します。

## AEM 6.2 Forms または AEM 6.3 Forms から AEM 6.4 Forms へのアップグレード {#upgrade-aem-forms-62-63-to-64}

AEM 6.2 Forms と AEM 6.3 Forms の場合、AEM 6.4 Forms へ直接アップグレードすることができます。以下の操作を実行してください。

1. 既存の AEM インスタンスを AEM 6.4 にアップグレードします。手順は次のとおりです。

   1. AEM 6.2 Forms または AEM 6.3 Forms の最新のサービスパックおよびパッチをインストールします。詳しくは、次を参照してください。

      * [AEM 6.2 リリースノート](https://helpx.adobe.com/jp/experience-manager/6-2/release-notes.html)
      * [AEM 6.3 リリースノート](https://helpx.adobe.com/jp/experience-manager/6-3/release-notes.html)
      * [AEM Sustenance Hub](https://helpx.adobe.com/jp/experience-manager/aem-releases-updates.html)
   1. アップグレードのソースインスタンスを準備します。詳しくは、「[AEM 6.4 へのアップグレード](/help/sites-deploying/upgrade.md#preparing%20the%20source%20instance)」を参照してください。
   1. [AEM 6.4 QuickStart](/help/sites-deploying/deploy.md#getting%20the%20software) をダウンロードします。
   1. **（Unix/Linux ベースのインストールのみ）** 基盤のオペレーティングシステムとして UNIX または Linux を使用している場合は、ターミナルウィンドウを開いて crx-quickstart が含まれているフォルダーに移動し、次のコマンドを実行します。

      `chmod -R 755 ../crx-quickstart`

   1. AEMインスタンスをAEM 6.3にアップグレードします。詳しい手順については、[AEM 6.4](/help/sites-deploying/upgrade.md)へのアップグレードを参照してください。

      次の手順に進む前に、ServiceEvent REGISTERED および ServiceEvent UNREGISTERED メッセージが &lt;crx-repository>/error.log ファイルに出現しなくなるまで待ちます。

      >[!NOTE]
      >
      >サーバーが起動して実行した後、いくつかの AEM Forms バンドルはインストール状態のままです。バンドルの数はインストールごとに異なる可能性があります。これらのバンドルの状態は無視しても問題はありません。バンドルは`https://[server]:[port]/system/console/`に一覧表示されます。


1. AEM Forms アドオンパッケージのインストール. 手順は次のとおりです。

   1. [ソフトウェア配布](https://experience.adobe.com/downloads)を開きます。 ソフトウェアディストリビューションにログインするには、Adobe ID が必要です。
   1. ヘッダーメニューにある&#x200B;**[!UICONTROL Adobe Experience Manager]**&#x200B;をタップします。
   1. 「**[!UICONTROL フィルター]**」セクションで、
      1. 「**[!UICONTROL ソリューション]**」ドロップダウンリストから「**[!UICONTROL Forms]**」を選択します。
      1. パッケージのバージョンとタイプを選択します。 また、「**[!UICONTROL ダウンロードを検索]**」オプションを使用して、結果をフィルターすることもできます。
   1. お使いのオペレーティングシステムに対応するパッケージ名をタップし、「**[!UICONTROL EULA条項に同意]**」を選択して、「**[!UICONTROL ダウンロード]**」をタップします。
   1. [Package Manager](https://docs.adobe.com/content/help/ja-JP/experience-manager-65/administering/contentmanagement/package-manager.html)を開き、「**[!UICONTROL パッケージをアップロード]**」をクリックして、パッケージをアップロードします。
   1. パッケージを選択し、「**[!UICONTROL インストール]**」をクリックします。

      [AEM Formsリリース](https://helpx.adobe.com/jp/aem-forms/kb/aem-forms-releases.html)の記事に記載されている直接リンクを使って、パッケージをダウンロードすることもできます。

      >[!NOTE]
      >
      >パッケージのインストールが完了したら、AEM インスタンスを再起動するよう指示されます。**その際、すぐにサーバーを停止しないでください。** AEM Forms サーバーを停止する前に、ServiceEvent REGISTERED メッセージと ServiceEvent UNREGISTERED メッセージが &lt;crx-repository>/error.log ファイルに表示されなくなり、このログファイルが安定した状態になるまで待ちます。また、いくつかのパッケージについては、インストールされたままの状態になる場合があることに注意してください。これらのパッケージは、無視してかまいません。

   1. AEM インスタンスを停止して、次のファイルを削除します。

      * `[AEM_Installation_Directory]\[crx-quickstart]\launchpad\ext\bcmail-jdk15-1.35`
      * `[AEM_Installation_Directory]\[crx-quickstart]\launchpad\ext\bcprov-jdk15-1.35`
   1. AEM インスタンスを起動します。


1. インストールの事後処理を実行します。

   * **移行ユーティリティの実行**

      移行ユーティリティにより、以前のバージョンのアダプティブフォームや対応する管理アセットが AEM 6.4 Forms で使用できるようになります。このユーティリティは、AEM Software Distributionからダウンロードできます。 移行ユーティリティの詳しい設定方法と使用方法については、[移行ユーティリティ](/help/forms/using/migration-utility.md)に関する説明を参照してください。

      [ドラフト統合とコンポーネント送信のサンプル](integrate-draft-submission-database.md)をデータベースで使用して旧バージョンのアップグレードを行う場合は、アップグレードの実行後に、以下の SQL クエリを実行してください。

      ```
      UPDATE metadata m, additionalmetadatatable am
      SET m.dataType = am.value
      WHERE m.id = am.id
      AND am.key = 'dataType'
      ```

      ```
      DELETE from additionalmetadatatable
      WHERE `key` = 'dataType'
      ```

   * **(AEM 6.2Formsまたは以前のバージョンからアップグレードした場合のみ)Adobe Signの再設定**

      Adobe Sign を以前のバージョンの AEM Forms で設定してある場合は、AEM Cloud サービスから Adobe Sign を再設定します。詳細については、「[Adobe Sign を AEM Forms に統合する](/help/forms/using/adobe-sign-integration-adaptive-forms.md)」を参照してください。

   * **分析機能とレポートの再設定（バージョン 6.2 以前の AEM Forms をアップグレードする場合のみ）** 

      AEM 6.4 Forms では、ソースのトラフィック変数とインプレッションの成功イベントは利用できません。そのため、バージョン 6.2 以前の AEM Forms をアップグレードすると、AEM Forms から Adobe Analytics サーバーにデータが送信されなくなり、アダプティブフォームの分析レポートが使用できなくなります。また、AEM 6.4 Forms には、フォームバージョン分析用のトラフィック変数と、フィールドの処理時間に関する成功イベントが導入されています。このため、AEM Forms 環境で分析とレポートを再設定してください。詳しい手順については、「[分析とレポートの設定](/help/forms/using/configure-analytics-forms-documents.md)」を参照してください。

1. サーバーのアップグレードが成功し、すべてのデータが正常に移行され、問題なく動作することを確認してください。

   * **バンドルのステータスを確認：**&#x200B;すべてのバンドルがアクティブ状態になっていることを確認します。
   * **複製と逆複製を確認：**&#x200B;移行されたフォームをいくつか発行、記入、送信します。送信済みデータも確認します。
   * **管理者および開発者のユーザーインターフェースへのアクセスを確認：**&#x200B;管理者アカウントで AEM インスタンスにログインし、次の URL にアクセスできるか確認します。

      * `https://[server]:[port]/crx/packmgr`
      * `https://[server]:[port]/crx/de`
      * `https://[server]:[port]/aem/forms.html/content/dam/formsanddocuments`

   >[!NOTE]
   AEM 6.4 Forms では crx-repository の構造が変更されています。AEM 6.4 Forms にアップグレードしたあと、新規作成するカスタマイズについては、変更後のパスを使用してください。変更後のパスの一覧については、「[AEM 6.4 Forms におけるリポジトリの再構築](/help/sites-deploying/forms-repository-restructuring-in-aem-6-4.md)」を参照してください。

## AEM 6.0 Forms または AEM 6.1 Forms から AEM 6.4 Forms へのアップグレード {#upgrade-aem-forms-60-61-to-64}

**AEM 6.0 Forms** と **AEM 6.1 Forms** の場合、AEM 6.4 Forms に直接アップグレードすることはできません。AEM 6.2Forms](/help/forms/using/upgrade.md)への中間的な[アップグレードまたは[AEM 6.3Forms](/help/forms/using/upgrade.md)へのアップグレードを実行し、AEM 6.2FormsまたはAEM 6.3FormsからAEM6.4Formsにアップグレードします。
