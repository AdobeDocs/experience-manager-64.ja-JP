---
title: OWASP Top 10
seo-title: OWASP Top 10
description: AEMが OWASP のセキュリティリスク上位 10 件をどのように扱うかを説明します。
seo-description: Learn how AEM deals with the top 10 OWASP security risks.
uuid: a5a7e130-e15b-47ae-ba21-448f9ac76074
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.4/SITES
topic-tags: Security
content-type: reference
discoiquuid: e5323ae8-bc37-4bc6-bca6-9763e18c8e76
exl-id: c29472c8-9a93-4cb1-9cb1-05fc155ba736
source-git-commit: 31d6111a82a3cbfef22970d05280b0d3fd1c0de7
workflow-type: tm+mt
source-wordcount: '496'
ht-degree: 44%

---

# OWASP Top 10{#owasp-top}

この [Web アプリケーションセキュリティプロジェクトを開く](https://www.owasp.org) (OWASP) は、これらが [Web アプリケーションのセキュリティリスク上位 10 件](https://www.owasp.org/index.php/OWASP_Top_Ten_Project).

以下に、CRX での処理方法の説明と共に、これらを示します。

## 1.射出 {#injection}

* SQL — デザインによって回避：デフォルトのリポジトリ設定には、従来のデータベースも必要もありません。すべてのデータはコンテンツリポジトリに保存されます。 すべてのアクセスは認証済みユーザーに制限され、JCR API を介してのみ実行できます。 SQL は、検索クエリ (SELECT) でのみサポートされます。 さらに、SQL は値バインディングをサポートします。
* LDAP — 認証モジュールは入力をフィルタリングし、バインド方法を使用してユーザーインポートを実行するので、LDAP インジェクションはできません。
* OS — アプリケーション内から実行されたシェル実行はありません。

## 2.クロスサイトスクリプティング (XSS) {#cross-site-scripting-xss}

このリスクを軽減する一般的な方法は、[OWASP Encoder](https://www.owasp.org/index.php/OWASP_Java_Encoder_Project) と [AntiSamy](https://www.owasp.org/index.php/Category:OWASP_AntiSamy_Project) に基づくサーバー側の XSS 保護ライブラリを使用して、ユーザーが生成したコンテンツのすべての出力をエンコードすることです。

XSS はテスト時および開発時における最優先事項であり、検出された問題は（通常）すぐに解決されます。

## 3. 認証とセッション管理の不備 {#broken-authentication-and-session-management}

AEM では、[Apache Jackrabbit](https://jackrabbit.apache.org/) と [Apache Sling](https://sling.apache.org/) に基づく、堅実で実績のある認証手法を利用しています。ブラウザー／HTTP セッションは AEM では使用されません。

## 4.安全でない直接オブジェクト参照 {#insecure-direct-object-references}

データオブジェクトへのすべてのアクセスはリポジトリーによって仲介されるので、役割に基づくアクセス制御によって制限されます。

## 5.クロスサイトリクエストフォージェリ (CSRF) {#cross-site-request-forgery-csrf}

クロスサイトリクエストフォージェリ（CSRF）は、暗号トークンをあらゆる形式および AJAX リクエストに自動的に注入し、すべての POST についてこのトークンをサーバー上で検証することで軽減されます。

さらに、AEM に搭載されているリファラーヘッダーベースのフィルターを設定して、特定のホスト（リストで定義）からの POST リクエスト&#x200B;*のみ*&#x200B;を許可することができます。

## 6.セキュリティの設定ミス {#security-misconfiguration}

すべてのソフトウェアが常に正しく設定されていることを保証することは不可能です。 しかし、できるだけ多くのガイダンスを提供し、設定をできるだけ簡単にするよう努めています。 さらに、AEMは [統合セキュリティヘルスチェック](/help/sites-administering/operations-dashboard.md) セキュリティ構成を一目で監視するのに役立つ情報です。

詳しくは、[セキュリティチェックリスト](/help/sites-administering/security-checklist.md)を参照してください。セキュリティ強化の手順を段階的に説明しています。

## 7.安全でない暗号化ストレージ {#insecure-cryptographic-storage}

パスワードは暗号化ハッシュとしてユーザーノードに保存されます。デフォルトでは、このようなノードは、管理者とユーザー自身が読み取り可能です。

サードパーティの資格情報などの機密データは、FIPS 140-2 認定暗号化ライブラリを使用して暗号化された形式で保存されます。

## 8. URL アクセスの制限の失敗 {#failure-to-restrict-url-access}

リポジトリでは、アクセス制御エントリを使用して、特定のパスの特定のユーザーまたはグループに対して[（JCR で指定された）詳細な権限](https://www.adobe.io/experience-manager/reference-materials/spec/jcr/2.0/16_Access_Control_Management.html)を設定できます。アクセス制限はリポジトリによって適用されます。

## 9. 不十分なトランスポート層の保護 {#insufficient-transport-layer-protection}

サーバー設定（例：HTTPS のみの使用）によって軽減されます。

## 10. 未検証のリダイレクトとフォワード {#unvalidated-redirects-and-forwards}

ユーザーが指定した宛先へのすべてのリダイレクトを内部の場所に制限することで軽減されます。
