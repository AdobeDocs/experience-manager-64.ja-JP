---
title: AEM Forms JEEパッチインストーラー
description: AEM Forms JEEパッチインストーラー
uuid: e709871b-c04c-43bb-a7d0-45e89fbd3d44
content-type: reference
discoiquuid: 83bace08-1d4f-4192-a634-c7c4879963d8
exl-id: ce5300ce-03f4-4e7b-bc5b-01a9968ebe06
source-git-commit: bd94d3949f0117aa3e1c9f0e84f7293a5d6b03b4
workflow-type: tm+mt
source-wordcount: '544'
ht-degree: 49%

---

# AEM Forms JEEパッチインストーラー{#aem-forms-jee-patch-installer}

>[!NOTE]
>
>[詳細情報](https://www.adobe.com/account/sign-in.supportportal.html) やパッチの入手方法については、サポートにお問い合わせください。

## パッチインストーラーについて{#about-the-patch-installer}

AEM 6.4 Forms JEEパッチインストーラーには、このパッチのリリースまでに利用可能なAEM 6.4 Forms JEEのすべてのコンポーネントに関する修正済みの問題がすべて含まれています。 修正された問題の完全なリストについては、最新の[累積修正パックリリースノート](cfp-release-notes.md)を参照してください。

## パッチ{#prerequisites-to-installing-the-patch}のインストールの前提条件

* AEM 6.4 Forms

## パッチ{#installing-and-configuring-the-patch}のインストールと設定

1. &lt;*AEM_forms_root*>/deploy フォルダーのバックアップを作成します。Quick Fix をアンインストールする場合は必須です。
1. アプリケーションサーバーを停止します。
1. パッチインストーラーアーカイブファイルをハードディスクに展開します。
1. 使用しているオペレーティングシステムに従って名前が付けられたディレクトリで、次の操作を実行します。

   * **Windows**
インストーラーをコピーしたハードディスク上の適切なディレクトリまたはフォルダーに移動し、 
`aemforms64_cfp_install.exe` file.

      * (Windows 32 ビット) `Windows\Disk1\InstData\VM`
      * (Windows 64 ビット) `Windows_64Bit`\ `Disk1\InstData\VM`
   * **Linux、Solaris、AIX** 適切なディレクトリに移動して、コマンドプロンプトで 
`./aem64_cfp_install.bin`

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
1. インストールが完了したら、「**[!UICONTROL 次へ]**」をクリックして、インストールしたファイルにQuick Fixの更新を適用します。
1. [Windowsの] み次の手順のいずれかを実行します。

   * 「完了」をクリックする前に、「Configuration Manager を起動」オプションの選択を解除します。`[aem-forms root]\configurationManager\bin`にある`ConfigurationManager.bat`ファイルを使用して、Configuration Managerを後で実行します。 `ConfigurationManager.bat`を使用すると、.laxファイル内のaxis.jar名を手動で更新するのを防ぐことができます
   * 「完了」をクリックする前に、「Configuration Manager を起動」オプションの選択を解除します。**ConfigurationManager.exe**&#x200B;または&#x200B;**ConfigurationManager_IPv6.exe**&#x200B;を使用してConfiguration Managerを実行する前に、*&lt;AEMorms_Install_Dir>\configurationManager\bin*&#x200B;ディレクトリに移動し、**axis.jar**&#x200B;を&#x200B;**に更新します —1.4.1.1.jar**（次のファイル）

      * ConfigurationManager.lax
      * ConfigurationManager_IPv6.lax

1. （UNIXベースのみ）「 Configuration Managerを起動」チェックボックスはデフォルトで選択されています。 「**[!UICONTROL 完了]**」をクリックして Configuration Manager を実行します。

   Configuration Manager を後で実行するには、「完了」をクリックする前に、「Configuration Manager を起動」オプションの選択を解除します。`[AEM_forms_root]/configurationManager/bin`ディレクトリ内の適切なスクリプトを使用して、後でConfiguration Managerを起動できます。

1. アプリケーションサーバーに応じて、以下のいずれかのドキュメントを選択し、「*AEM Forms の設定とデプロイ*」節の指示に従ってください。

   * [AEM Forms のインストールおよびデプロイ（JBoss 版）](http://www.adobe.com/go/learn_aemforms_installJBoss_64)
   * [AEM Forms のインストールおよびデプロイ（WebSphere 版）](http://www.adobe.com/go/learn_aemforms_installWebSphere_64)
   * [AEM Forms のインストールおよびデプロイ（WebLogic 版）](http://www.adobe.com/go/learn_aemforms_installWebLogic_64)

1. （JBossのみ）パッチをインストールしてサーバーを設定した後、JBossアプリケーションサーバーのtmpディレクトリとworkディレクトリを削除します。

## デプロイ後の設定{#post-deployment-configurations}

### SAML設定{#saml-configurations}

SAML認証を設定済みで、大きなIDPメタデータに関する問題が発生する場合は、パッチをインストールした後に次の手順を実行します。

1. アプリケーションサーバーで次のシステムプロパティを設定します。\
   `um.saml.enable.large.xml=true`

1. サーバーを再起動します。
1. 既存のSAML認証プロバイダーを削除し、SAML設定の説明に従って、既存のドメインに対して再度追加します。

## 影響を受けたモジュール{#impacted-modules}

* ドキュメントサービス
* Document Security
* Foundation JEE
* PDFG サービス

[サポートへのお問い合わせ](https://www.adobe.com/account/sign-in.supportportal.html)
