---
title: セキュリティ
seo-title: Security
description: 開発フェーズ中にアプリケーションのセキュリティが開始
seo-description: Application Security starts during the development phase
exl-id: 22c48f8c-38df-4c9b-88cf-67f6ae46e7e1
source-git-commit: c5b816d74c6f02f85476d16868844f39b4c47996
workflow-type: tm+mt
source-wordcount: '462'
ht-degree: 58%

---

# セキュリティ{#security}

>[!CAUTION]
>
>AEM 6.4 の拡張サポートは終了し、このドキュメントは更新されなくなりました。 詳細は、 [技術サポート期間](https://helpx.adobe.com/jp/support/programs/eol-matrix.html). サポートされているバージョンを見つける [ここ](https://experienceleague.adobe.com/docs/?lang=ja).

アプリケーションのセキュリティは、開発フェーズで開始します。 Adobeでは、次のセキュリティのベストプラクティスを適用することをお勧めします。

## リクエストセッションを使用 {#use-request-session}

最小権限の原則に従って、アドビでは、リポジトリへのすべてのアクセスを、ユーザー要求と適切なアクセス制御にバインドされたセッションを使用して行うことをお勧めします。

## クロスサイトスクリプティング (XSS) に対するProtect {#protect-against-cross-site-scripting-xss}

クロスサイトスクリプティング (XSS) を使用すると、攻撃者は他のユーザーが閲覧した Web ページにコードを挿入できます。 このセキュリティ脆弱性は、悪意のある Web ユーザーによって悪用され、アクセス制御をバイパスする可能性があります。

AEMは、ユーザーが指定したすべてのコンテンツを出力時にフィルタリングする原則を適用します。 開発とテストの両方で、XSS の防止が最も優先されます。

AEM が提供する XSS 保護メカニズムは、[OWASP（The Open Web Application Security Project）](https://www.owasp.org/)が提供する [AntiSamy Java ライブラリ](https://www.owasp.org/index.php/Category:OWASP_AntiSamy_Project)に基づいています。デフォルトの AntiSamy 構成は、次の場所にあります。

`/libs/cq/xssprotection/config.xml`

設定ファイルをオーバーレイすることで、この設定を独自のセキュリティ要件に適合させることが重要です。公式の [AntiSamy ドキュメント](https://www.owasp.org/index.php/Category:OWASP_AntiSamy_Project)では、セキュリティ要件を実装するために必要なすべての情報が提供されています。

>[!NOTE]
>
>[AEM が提供する XSSAPI](https://helpx.adobe.com/experience-manager/6-4/sites/developing/using/reference-materials/javadoc/com/adobe/granite/xss/XSSAPI.html) を使用して、常に XSS 対策 API にアクセスすることを強くお勧めします。

また、[Apache 対応の mod_security](https://www.modsecurity.org) などの web アプリケーションファイアウォールを使用すると、デプロイメント環境のセキュリティを高い信頼性で一元的に制御でき、以前は検出されなかったクロスサイトスクリプティング攻撃に対する保護も可能になります。

## Cloud Service情報へのアクセス {#access-to-cloud-service-information}

>[!NOTE]
>
>インスタンスの保護に必要なクラウドサービス情報用の ACL と OSGi 設定は、[実稼動準備モード](/help/sites-administering/production-ready.md)の一部として自動化されます。つまり、設定の変更を手動で行う必要はありませんが、設定されていることをデプロイメントの運用を開始する前に確認しておくことをお勧めします。

次の場合： [AEMインスタンスとAdobe Marketing Cloudの統合](/help/sites-administering/marketing-cloud.md) 次を使用 [Cloud Service設定](/help/sites-developing/extending-cloud-config.md). これらの設定に関する情報は、収集された統計と共にリポジトリに保存されます。 この機能を使用する場合は、この情報に対するデフォルトのセキュリティが要件に一致するかどうかを確認することをお勧めします。

webservicesupport モジュールは、次の場所に統計情報と設定情報を書き込みます。

`/etc/cloudservices`

デフォルトの権限は、次のとおりです。

* オーサー環境：`contributors` に対する `read` 権限

* パブリッシュ環境：`everyone` に対する `read` 権限

## クロスサイトリクエストフォージェリ攻撃からの保護 {#protect-against-cross-site-request-forgery-attacks}

CSRF 攻撃を軽減するために AEM で採用されているセキュリティメカニズムについて詳しくは、セキュリティチェックリストの [Sling リファラーフィルター](/help/sites-administering/security-checklist.md#protect-against-cross-site-request-forgery)の節と、[CSRF 対策フレームワークのドキュメント](/help/sites-developing/csrf-protection.md)を参照してください。
