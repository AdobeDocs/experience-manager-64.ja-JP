---
title: フォントを使用可能にする
seo-title: Make fonts available
description: フォーム内で使用されるフォントが、AEM forms をホストする J2EE アプリケーションサーバーで使用できることを確認します。
seo-description: Ensure that the fonts used within a form are available for use on the J2EE application server hosting AEM forms.
uuid: 6588b4b6-f866-4253-91c8-3aa174340e8c
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_output
products: SG_EXPERIENCEMANAGER/6.4/FORMS
discoiquuid: 9f58a6c4-3190-49d4-800c-4a55dca7c296
exl-id: 33d63ec9-b100-48b4-b84d-a9de82c24f86
source-git-commit: c5b816d74c6f02f85476d16868844f39b4c47996
workflow-type: tm+mt
source-wordcount: '255'
ht-degree: 24%

---

# フォントを使用可能にする {#make-fonts-available}

>[!CAUTION]
>
>AEM 6.4 の拡張サポートは終了し、このドキュメントは更新されなくなりました。 詳細は、 [技術サポート期間](https://helpx.adobe.com/jp/support/programs/eol-matrix.html). サポートされているバージョンを見つける [ここ](https://experienceleague.adobe.com/docs/?lang=ja).

フォーム内で使用されるフォントが、AEM forms をホストする J2EE アプリケーションサーバーで使用できることを確認します。 例えば、次のシナリオについて考えてみます。 フォームデザイナーが、Designer が使用するフォントディレクトリにフォントを追加し、別のコンピューター上でそのフォントを使用するフォームを作成します。 Output サービスでこのフォントを使用するには、このフォントを Customer fonts ディレクトリに配置します。 カスタマーフォントディレクトリが存在しない場合は、AEM Forms をホストする J2EE アプリケーションサーバー上にディレクトリを作成します。

その他のフォント設定については、 [一般的なAEM forms の設定](/help/forms/using/admin-help/configure-general-aem-forms-settings.md#configure-general-aem-forms-settings).

**カスタマーフォントディレクトリの場所を指定します**

1. 管理コンソールで、設定/コアシステム設定/設定をクリックします。
1. 「システムフォントディレクトリの場所」ボックスに、カスタマーフォントディレクトリのパスを入力します。 複数のディレクトリを追加する場合は、セミコロン **;** で区切って指定します。
1. 「OK」をクリックしてください。
1. AEM forms がインストールされているシステムを再起動します。

>[!NOTE]
>
>フォントは Windows システムのフォントキャッシュから選択され、キャッシュを更新するにはシステムを再起動する必要があります。 カスタマーフォントディレクトリを指定した後、AEM Forms をインストールしているシステムを再起動してください。
