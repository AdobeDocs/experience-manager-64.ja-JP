---
title: AEM Forms JEE パッチインストーラー
description: AEM Forms JEE パッチインストーラー
uuid: e709871b-c04c-43bb-a7d0-45e89fbd3d44
content-type: reference
discoiquuid: 83bace08-1d4f-4192-a634-c7c4879963d8
exl-id: ce5300ce-03f4-4e7b-bc5b-01a9968ebe06
source-git-commit: bd94d3949f0117aa3e1c9f0e84f7293a5d6b03b4
workflow-type: tm+mt
source-wordcount: '544'
ht-degree: 76%

---

# AEM Forms JEE パッチインストーラー {#aem-forms-jee-patch-installer}

>[!NOTE]
>
>詳細情報またはパッチの入手については、[サポートにお問い合わせ](https://www.adobe.com/jp/account/sign-in.supportportal.html)ください。

## パッチインストーラーについて {#about-the-patch-installer}

AEM 6.4 Forms JEE パッチインストーラーには、このパッチのリリースまで使用可能であった、AEM 6.4 Forms JEE のすべてのコンポーネントに関するすべての問題の修正が含まれています。最新の  [累積修正パックリリースノート](cfp-release-notes.md) 修正された問題の完全なリストを参照してください。

## パッチをインストールするための前提条件 {#prerequisites-to-installing-the-patch}

* AEM 6.4 Forms

## パッチのインストールと設定 {#installing-and-configuring-the-patch}

1. &lt;*AEM_forms_root*>/deploy フォルダーのバックアップを作成します。Quick Fix をアンインストールする場合は必須です。
1. アプリケーションサーバーを停止します。
1. パッチインストーラーアーカイブファイルをハードディスクに展開します。
1. 使用しているオペレーティングシステムに従って名前が付けられたディレクトリで、次の操作を実行します。

   * **Windows**

インストーラをコピーしたハードディスク上のインストールメディアまたはフォルダの適切なディレクトリに移動し、 
`aemforms64_cfp_install.exe` ファイル.

      * （Windows 32 ビット） `Windows\Disk1\InstData\VM`
      * （Windows 64 ビット） `Windows_64Bit`\ `Disk1\InstData\VM`
   * **Linux、Solaris、AIX** 適切なディレクトリに移動して、コマンドプロンプトで 
`./aem64_cfp_install.bin` を入力します。

      * （Linux）`Linux/Disk1/InstData/NoVM`
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
1. インストールが完了したら、「**」をクリックします[!UICONTROL 次へ]**をクリックして、インストールされているファイルにクイックフィックスの更新を適用します。
1. [Windows のみ] 次のいずれかの手順を実行します。

   * 「Configuration Manager を起動」オプションの選択を解除してから、「完了」をクリックます。後で、 `ConfigurationManager.bat` 次の場所にあるファイル： `[aem-forms root]\configurationManager\bin`. 使用 `ConfigurationManager.bat` .lax ファイル内の axis.jar 名を手動で更新するのを回避できます。
   * 「Configuration Manager を起動」オプションの選択を解除してから、「完了」をクリックます。を使用して Configuration Manager を実行する前に **ConfigurationManager.exe** または **ConfigurationManager_IPv6.exe**&#x200B;に移動します。 *&lt;aemforms_install_dir>\configurationManager\bin* ディレクトリと更新 **axis.jar** から **axis-1.4.1.1.jar** を次のファイルに置きます。

      * ConfigurationManager.lax
      * ConfigurationManager_IPv6.lax

1. （UNIX ベースのみ）「 Start Configuration Manager 」チェックボックスはデフォルトで選択されています。 「**[!UICONTROL 完了]**」をクリックして Configuration Manager を実行します。

   Configuration Manager を後で実行するには、「完了」をクリックする前に、「Configuration Manager を起動」オプションの選択を解除します。`[AEM_forms_root]/configurationManager/bin` ディレクトリにある該当スクリプトを使用して、Configuration Manager を後で起動することができます。

1. アプリケーションサーバーに応じて、以下のいずれかのドキュメントを選択し、*AEM Forms の設定とデプロイ*&#x200B;節の指示に従ってください。

   * [AEM Forms のインストールおよびデプロイ（JBoss 版）](http://www.adobe.com/go/learn_aemforms_installJBoss_64_jp)
   * [AEM Forms のインストールおよびデプロイ（WebSphere 版）](http://www.adobe.com/go/learn_aemforms_installWebSphere_64_jp)
   * [AEM Forms のインストールおよびデプロイ（WebLogic 版）](http://www.adobe.com/go/learn_aemforms_installWebLogic_64_jp)

1. （JBoss のみ）パッチをインストールしてサーバーを設定した後、JBoss Application Server の tmp および work ディレクトリを削除します。

## デプロイメント後の設定 {#post-deployment-configurations}

### SAML の設定 {#saml-configurations}

SAML 認証を設定済みで、大きな IDP メタデータに関する問題が発生した場合は、パッチをインストールした後に次の手順を実行します。

1. アプリケーションサーバーで次のシステムプロパティを設定します。\
   `um.saml.enable.large.xml=true`

1. サーバーを再起動します。
1. 既存の SAML 認証プロバイダーを削除し、SAML 設定の説明に従って、既存のドメインに対してそれらのプロバイダーを再度追加します。

## 影響を受けるモジュール {#impacted-modules}

* Document Services
* Document Security
* Foundation JEE
* PDFG サービス

[サポートへのお問い合わせ](https://www.adobe.com/account/sign-in.supportportal.html)
