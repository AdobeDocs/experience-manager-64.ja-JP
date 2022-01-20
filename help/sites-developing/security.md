---
title: セキュリティ
seo-title: Security
description: アプリケーションのセキュリティは、開発フェーズから始まります
seo-description: Application Security starts during the development phase
uuid: efd5f3bc-da07-4fc8-a6ce-f1e6f5084c9e
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.4/SITES
topic-tags: introduction
content-type: reference
discoiquuid: d2267663-6c1d-413c-9862-e82e21ae6906
exl-id: 22c48f8c-38df-4c9b-88cf-67f6ae46e7e1
source-git-commit: bd94d3949f0117aa3e1c9f0e84f7293a5d6b03b4
workflow-type: tm+mt
source-wordcount: '426'
ht-degree: 65%

---

# セキュリティ{#security}

アプリケーションのセキュリティは、開発フェーズから始まります。アドビでは、次のセキュリティベストプラクティスを実施することをお勧めします。

## リクエストセッションの使用 {#use-request-session}

leas 権限の原則に従い、Adobeでは、すべてのリポジトリアクセスを、ユーザーリクエストにバインドされたセッションと適切なアクセス制御を使用しておこなうことをお勧めします。

## クロスサイトスクリプティング（XSS）に対する保護 {#protect-against-cross-site-scripting-xss}

クロスサイトスクリプティング（XSS）を利用することにより、攻撃者は他のユーザーが表示する Web ページにコードを埋め込むことができます。このセキュリティ脆弱性が悪意のある Web ユーザーに悪用され、アクセス制御が擦り抜けられる可能性があります。

AEM では、ユーザーが提供するコンテンツをすべて出力時にフィルタリングする原則を適用しています。XSS を回避することは、開発時にもテスト時にも第一優先となります。

AEMが提供する XSS 保護メカニズムは、 [AntiSamy Java ライブラリ](https://www.owasp.org/index.php/Category:OWASP_AntiSamy_Project) 提供： [OWASP(Open Web Application Security Project)](https://www.owasp.org/).デフォルトの AntiSamy 設定は、次の場所にあります。

`/libs/cq/xssprotection/config.xml`

設定ファイルをオーバーレイすることで、この設定を独自のセキュリティニーズに合わせて調整することが重要です。 役人は [AntiSamy ドキュメント](https://www.owasp.org/index.php/Category:OWASP_AntiSamy_Project) は、セキュリティ要件を実装するために必要なすべての情報を提供します。

>[!NOTE]
>
>XSS 対策 API にアクセスする場合は、[AEM が提供する XSSAPI](https://helpx.adobe.com/experience-manager/6-4/sites/developing/using/reference-materials/javadoc/com/adobe/granite/xss/XSSAPI.html) を常に使用することを強くお勧めします。

さらに、次のような Web アプリケーションファイアウォールが存在します。 [Apache 向け mod_security](https://www.modsecurity.org)を使用すると、デプロイメント環境のセキュリティを一元的に確実に制御し、未検出のクロスサイトスクリプティング攻撃から保護できます。

## クラウドサービス情報へのアクセス {#access-to-cloud-service-information}

>[!NOTE]
>
>インスタンスの保護に必要なクラウドサービス情報用の ACL と OSGi 設定は、[実稼動準備モード](/help/sites-administering/production-ready.md)の一部として自動化されます。つまり、設定の変更を手動で行う必要はありませんが、デプロイメントの運用を開始する前に変更を確認しておくことをお勧めします。

[AEM インスタンスを Adobe Marketing Cloud と統合する](/help/sites-administering/marketing-cloud.md)場合は、[クラウドサービス設定](/help/sites-developing/extending-cloud-config.md)を使用します。これらの設定に関する情報は、収集された統計と共にリポジトリに格納されます。この機能を使用する場合は、この情報に適用されるデフォルトのセキュリティが要件に対応しているかどうかを確認することをお勧めします。

webservicesupport モジュールは、統計と設定情報を次の場所に書き込みます。

`/etc/cloudservices`

デフォルトの権限では、次の処理が可能です。

* オーサー環境： `read` 対象 `contributors`

* パブリッシュ環境： `read` 対象 `everyone`

## クロスサイトリクエストフォージェリ攻撃からの保護 {#protect-against-cross-site-request-forgery-attacks}

CSRF 攻撃を軽減するために AEM で採用されているセキュリティメカニズムについて詳しくは、セキュリティチェックリストの [Sling Referrer Filter](/help/sites-administering/security-checklist.md#protect-against-cross-site-request-forgery) および [CSRF 対策フレームワークのドキュメント](/help/sites-developing/csrf-protection.md)を参照してください。
