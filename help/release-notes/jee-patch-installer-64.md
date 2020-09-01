---
title: AEM FormsJEEパッチインストーラー
description: 'null'
uuid: e709871b-c04c-43bb-a7d0-45e89fbd3d44
content-type: reference
discoiquuid: 83bace08-1d4f-4192-a634-c7c4879963d8
translation-type: tm+mt
source-git-commit: 610e9a54adad3abdfecb8b2c4da67d677f75175e
workflow-type: tm+mt
source-wordcount: '540'
ht-degree: 46%

---


# AEM FormsJEEパッチインストーラー {#aem-forms-jee-patch-installer}

>[!NOTE]
>
>[詳細やパッチの入手方法については、サポート](https://www.adobe.com/jp/account/sign-in.supportportal.html) にお問い合わせください。

## パッチインストーラについて {#about-the-patch-installer}

AEM 6.4FormsJEEパッチインストーラーには、このパッチのリリースまで使用可能なAEM 6.4FormsJEEのすべてのコンポーネントに関するすべての修正済みの問題が含まれています。 修正された問題の完全なリストについては、 [累積Fix Packの最新リリースノート](cfp-release-notes.md) を参照してください。

## パッチのインストールに必要な前提条件 {#prerequisites-to-installing-the-patch}

* AEM 6.4 Forms

## パッチのインストールと設定 {#installing-and-configuring-the-patch}

1. &lt;*AEM_forms_root*>/deploy フォルダーのバックアップを作成します。Quick Fix をアンインストールする場合は必須です。
1. アプリケーションサーバーを停止します。
1. パッチインストーラーのアーカイブファイルをハードドライブに展開します。
1. 使用しているオペレーティングシステムに従って名前が付けられたディレクトリで、次の操作を実行します。

   * **Windows**&#x200B;インストールメディアまたはハードディスク上のインストーラーのコピー先フォルダーにある適切なディレクトリに移動し、重複クリックして、 
`aemforms64_cfp_install.exe` file.

      * (Windows 32-bit) `Windows\Disk1\InstData\VM`
      * (Windows 64-bit) `Windows_64Bit`\ `Disk1\InstData\VM`
   * **Linux、Solaris、AIX** 適切なディレクトリに移動して、コマンドプロンプトで 
`./aem64_cfp_install.bin`。

      * (Linux) `Linux/Disk1/InstData/NoVM`
      * (Solaris) `Solaris/Disk1/InstData/NoVM`
      * (AIX)

         ```
         AIX/Disk1/InstData/VM
         ```
   インストールの手順を示すインストールウィザードが起動します。

1. 概要パネルで「**[!UICONTROL 次へ]**」をクリックします。
1. インストールフォルダーを選択画面で、表示されるデフォルトの場所が既存のインストール場所であることを確認するか、または「**[!UICONTROL 参照]**」をクリックして AEM Forms がインストールされている別のフォルダーを選択してから、「**[!UICONTROL 次へ]**」をクリックします。

1. Quick Fix パッチの概要の情報を読み、「**[!UICONTROL 次へ]**」をクリックします。
1. プリインストールの概要情報を読み、「**[!UICONTROL インストール]**」をクリックします。
1. When the installation is complete, click **[!UICONTROL Next]**to apply the quick fix updates to your installed files.
1. [Windowsのみ] ：次のいずれかの手順を実行します。

   * 「完了」をクリックする前に、「Configuration Manager を起動」オプションの選択を解除します。後で、にある `ConfigurationManager.bat` ファイルを使用してConfiguration Managerを実行し `[aem-forms root]\configurationManager\bin`ます。 を使用す `ConfigurationManager.bat` ると、.laxファイル内のaxis.jar名を手動で更新しないようにできます。
   * 「完了」をクリックする前に、「Configuration Manager を起動」オプションの選択を解除します。ConfigurationManager.exe **またはConfigurationManager_IPv6.exeを使用してConfiguration Manager** を実行する前に **、**&lt;AEMForms_Install_Dir \configurationManager\bin ********** directoryに移動し、&lt;AEMForms_Install_Dir>dirディレクトリに移動し、.1.jarを更新してください。

      * ConfigurationManager.lax
      * ConfigurationManager_IPv6.lax

1. （UNIXベースのみ）デフォルトでは、「開始のConfiguration Manager」チェックボックスが選択されています。 「**[!UICONTROL 完了]**」をクリックして Configuration Manager を実行します。

   Configuration Manager を後で実行するには、「完了」をクリックする前に、「Configuration Manager を起動」オプションの選択を解除します。You can start Configuration Manager later using the appropriate script in the `[AEM_forms_root]/configurationManager/bin` directory.

1. アプリケーションサーバーに応じて、以下のいずれかのドキュメントを選択し、「*AEM Forms の設定とデプロイ*」節の指示に従ってください。

   * [AEM Forms のインストールおよびデプロイ（JBoss 版）](http://www.adobe.com/go/learn_aemforms_installJBoss_64_jp)
   * [AEM Forms のインストールおよびデプロイ（WebSphere 版）](http://www.adobe.com/go/learn_aemforms_installWebSphere_64_jp)
   * [AEM Forms のインストールおよびデプロイ（WebLogic 版）](http://www.adobe.com/go/learn_aemforms_installWebLogic_64_jp)

1. （JBossのみ）パッチをインストールしてサーバーを設定した後、JBoss Application Serverのtmpおよびworkディレクトリを削除します。

## Post-deployment configurations {#post-deployment-configurations}

### SAML設定 {#saml-configurations}

SAML認証を設定済みで、大きいIDPメタデータに関する問題が発生する場合は、パッチのインストール後に次の手順を実行します。

1. アプリケーションサーバーで次のシステムプロパティを設定します。\
   `um.saml.enable.large.xml=true`

1. サーバーを再起動します。
1. SAML設定の説明に従って、既存のSAML認証プロバイダーを削除し、既存のドメインに対して再度追加します。

## 影響を受けたモジュール {#impacted-modules}

* ドキュメントサービス
* ドキュメントのセキュリティ
* Foundation JEE
* PDFG サービス

[サポートへのお問い合わせ](https://www.adobe.com/jp/account/sign-in.supportportal.html)
