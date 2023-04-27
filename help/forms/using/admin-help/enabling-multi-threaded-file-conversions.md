---
title: マルチスレッドファイル変換の有効化
seo-title: Enabling multi-threaded file conversions
description: マルチスレッドファイル変換を有効にする方法を説明します。
seo-description: Learn how to enable multi-threaded file conversions.
uuid: 830c78aa-4f68-4e01-8b24-69a0275689c7
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/working_with_pdf_generator
products: SG_EXPERIENCEMANAGER/6.4/FORMS
discoiquuid: 85d655bb-1b6b-4b4d-ae39-eca3ef9b7fd7
feature: PDF Generator
exl-id: f0441588-7c16-40ab-841f-e89576a0d292
source-git-commit: bd94d3949f0117aa3e1c9f0e84f7293a5d6b03b4
workflow-type: tm+mt
source-wordcount: '869'
ht-degree: 6%

---

# マルチスレッドファイル変換の有効化 {#enabling-multi-threaded-file-conversions}

PDFジェネレーターを使用すると、特定の種類のファイルに対してマルチスレッドファイル変換を有効にすることができます。 マルチスレッドファイル変換を使用すると、PDFジェネレーターで同時に複数の変換を実行できるので、パフォーマンスが向上します。

## OpenOffice、Word、PowerPoint ドキュメントのマルチスレッドファイル変換の有効化 {#enabling-multi-threaded-file-conversions-for-openoffice-word-and-powerpoint-documents}

デフォルトでは、PDFジェネレーターは一度に 1 つの OpenOffice、Microsoft Word または PowerPoint ドキュメントのみを変換できます。 マルチスレッド変換を有効にすると、PDFジェネレーターは複数のドキュメントを同時に変換できます。 PDFジェネレーターは、OpenOffice または PDFMaker の複数のインスタンスを起動します（Word および PowerPoint の変換を実行するために使用されます）。

>[!NOTE]
>
>マルチスレッドファイル変換は、Microsoft Word 2003 および PowerPoint 2003 ではサポートされていません。 マルチスレッドファイル変換を有効にするには、Microsoft Word 2007、PowerPoint 2007、またはMicrosoft Word 2010、PowerPoint 2010 にアップグレードします。

>[!NOTE]
>
>マルチスレッドファイル変換は、Microsoft Excel、Microsoft Visio、Microsoft Project、Microsoft Publisher ではサポートされていません。

OpenOffice または PDFMaker の各インスタンスは、別々のユーザーアカウントを使用して起動されます。 追加する各ユーザーアカウントは、forms サーバーコンピューター上での管理者権限を持つ有効なユーザーである必要があります。 クラスター環境では、同じユーザーセットがクラスターのすべてのノードで有効である必要があります。

管理コンソールのユーザーアカウントページで、マルチスレッドファイル変換に使用するユーザーアカウントを指定できます。 アカウントの追加、削除、またはアカウントのパスワードの変更を行うことができます。 Windows Server 2003 または Windows Server 2008 でPDFジェネレーターを実行している場合は、管理者権限を持つユーザーアカウントを少なくとも 3 つ追加します。

Windows Server 2003、2008、または OpenOffice(Linux または Sun™ Solaris™) で OpenOffice、Microsoft Word またはMicrosoft PowerPoint のユーザーを追加する場合は、すべてのユーザーの初期アクティベーションダイアログを閉じます。

### プロセスレベルのトークンを置き換える権限を追加 {#add-the-right-to-replace-the-process-level-token}

Windows オペレーティングシステムでは、PDF変換に使用される管理者ユーザーアカウント（PDFG ユーザー）に、プロセスレベルトークンの置き換え権限が必要です。 この権限は、グループポリシーエディタを使用して追加できます。

1. Windows の [ スタート ] メニューで、[ ファイル名を指定して実行 ] をクリックし、「 gpedit.msc 」と入力します。
1. [ ローカルコンピュータポリシー ] > [ コンピュータの構成 ] > [Windows の設定 ] > [ セキュリティの設定 ] > [ ローカルポリシー ] > [ ユーザー権限の割り当て ] の順にクリックします。 を編集します。 *プロセスレベルトークンの置き換え* 管理者グループを含めるポリシーです。
1. 「プロセスレベルトークンの置き換え」エントリにユーザーを追加します。

### Windows Server 2008 上の OpenOffice、Microsoft Word およびMicrosoft PowerPoint に必要な追加設定 {#additional-configuration-required-for-openoffice-microsoft-word-and-microsoft-powerpoint-on-windows-server-2008}

Windows Server 2008 で OpenOffice、Microsoft Word またはMicrosoft PowerPoint を実行している場合は、追加した各ユーザーの UAC を無効にします。

1. 「Campaign コントロールパネル」>「ユーザーアカウント」>「ユーザーアカウント制御を有効にする」をクリックします。
1. 「ユーザーアカウント制御 (UAC) を使用してコンピューターを保護する」チェックボックスをオフにし、「OK」をクリックします。
1. 設定を有効にするには、コンピュータを再起動します。

### Linux または Solaris 上の OpenOffice に必要な追加設定 {#additional-configuration-required-for-openoffice-on-linux-or-solaris}

1. ユーザーアカウントを追加します。 ( [ユーザーアカウントの追加](enabling-multi-threaded-file-conversions.md#add-a-user-account).)
1. 次に、/etc/sudoers ファイルに変更を加えます。 このファイルのデフォルトの権限は 440 です。 このファイルの権限を書き込み可能に変更します。
1. /etc/sudoers ファイルに、追加のユーザー（forms サーバーを実行する管理者以外）のエントリを追加します。 例えば、lcadm というユーザーおよび myhost という名前のサーバーとしてAEM forms を実行していて、user1 および user2 として動作させる場合は、/etc/sudoers に次のエントリを追加します。

   ```as3
    lcadm myhost=(user1) NOPASSWD: ALL 
    lcadm myhost=(user2) NOPASSWD: ALL
   ```

   この設定により、lcadm は、ホスト「myhost」上で、「user1」または「user2」として、パスワードの入力を求めることなく、任意のコマンドを実行できます。

   >[!NOTE]
   >
   >システムユーザーと PDFG ユーザーの役割を「user1」と「user2」に割り当てていることを確認します。 PDFG ロールをユーザーに割り当てるには、 [ユーザーアカウントの追加](enabling-multi-threaded-file-conversions.md#add-a-user-account)

1. また、/etc/sudoers ファイルで、行の先頭に番号記号 (#) を付けて、この行を見つけてコメントアウトします。

   ```as3
   Defaults requiretty
   ```

   これにより、Linux ユーザを追加できます。

1. etc/sudoers ファイルの権限を 440 に変更します。
1. [ユーザーアカウントの追加](enabling-multi-threaded-file-conversions.md#add-a-user-account)で追加したすべてのユーザーが forms サーバーに接続できるようにします。例えば、user1 というローカルユーザーに forms サーバーに接続する権限を許可するには、次のコマンドを使用します。

   `xhost +local:user1@`

   詳しくは、 xhost コマンドのドキュメントを参照してください。

1. サーバーを再起動します。

>[!NOTE]
>
>OpenOffice は、すべての PDFG ユーザーがアクセスできるディレクトリの場所にインストールする必要があります。 これを確認するには、PDFG ユーザーとしてログインし、問題なく OpenOffice を起動できるかどうかを確認します。

### ユーザーアカウントの追加 {#add-a-user-account}

1. 管理コンソールで、サービス/PDFジェネレーター/ユーザーアカウントをクリックします。
1. 「追加」をクリックし、forms サーバー上での管理者権限を持つユーザーのユーザー名とパスワードを入力します。 OpenOffice のユーザーを設定する場合は、最初の OpenOffice アクティベーションダイアログを閉じます。

   >[!NOTE]
   >
   >OpenOffice 用にユーザーを設定する場合、OpenOffice のインスタンス数を、この手順で指定したユーザーアカウント数より多くすることはできません。

1. forms サーバーを再起動します。

### マルチスレッドファイル変換に使用されるリストからユーザーを削除します {#remove-a-user-from-the-list-used-for-multi-threaded-file-conversions}

1. 管理コンソールで、サービス/PDFジェネレーター/ユーザーアカウントをクリックします。
1. 削除するユーザーの横のチェックボックスをクリックし、「削除」をクリックします。
1. 確認ページで、「削除」をクリックします。
1. forms サーバーを再起動します。

### アカウントのパスワードの変更 {#change-the-password-for-an-account}

1. 管理コンソールで、サービス/PDFジェネレーター/ユーザーアカウントをクリックします。
1. ユーザー名をクリックし、新しいパスワードを入力して確定します。 このパスワードは、ユーザーのシステムパスワードと一致する必要があります。
