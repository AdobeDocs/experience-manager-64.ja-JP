---
title: AEM の閉じられたユーザーグループ
seo-title: Closed User Groups in AEM
description: AEMでの閉じられたユーザーグループについて説明します。
seo-description: Learn about Closed User Groups in AEM.
uuid: a65ed163-fdec-45f3-adf9-984d36f4eb73
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.4/SITES
topic-tags: Security
content-type: reference
discoiquuid: a2bd7045-970f-4245-ad5d-a272a654df0a
exl-id: 71dfaea7-2fae-4feb-bb1d-ad0da573f910
source-git-commit: c5b816d74c6f02f85476d16868844f39b4c47996
workflow-type: tm+mt
source-wordcount: '6907'
ht-degree: 48%

---

# AEM の閉じられたユーザーグループ{#closed-user-groups-in-aem}

>[!CAUTION]
>
>AEM 6.4 の拡張サポートは終了し、このドキュメントは更新されなくなりました。 詳細は、 [技術サポート期間](https://helpx.adobe.com/jp/support/programs/eol-matrix.html). サポートされているバージョンを見つける [ここ](https://experienceleague.adobe.com/docs/?lang=ja).

## はじめに {#introduction}

AEM 6.3 以降には、新しい閉じられたユーザーグループ実装があり、既存の実装に存在するパフォーマンス、拡張性、セキュリティの問題に対処することを目的としています。

>[!NOTE]
>
>このドキュメントでは、説明を簡略にするために、閉じられたユーザーグループ（Closed User Group）を「CUG」という略語で表記します。

この新しい実装の目的は、必要に応じて既存の機能をカバーすると同時に、旧バージョンからの問題や設計上の制限に対応することです。その結果、次の特性を持つ新しい CUG デザインが作成されます。

* 認証要素と承認要素を明確に分離し、個別に使用することも、組み合わせて使用することもできます。
* 他のアクセス制御の設定や権限要件に干渉することなく、設定された CUG ツリーでの制限付き読み取りアクセスを反映する専用の認証モデル。
* （通常、オーサリングインスタンスで必要となる）制限付き読み取りアクセスのアクセス制御設定と、（通常、公開時にのみ要求される）権限評価の切り離し。
* 権限のエスカレーションなしでの制限付き読み取りアクセスの編集
* 認証要件をマークする専用のノードタイプ拡張。
* 認証要件に関連付けられたオプションのログインパス。

### 新しいカスタムユーザーグループの実装 {#the-new-custom-user-group-implementation}

CUG は、AEMのコンテキストで知られているもので、次の手順で構成されます。

* 保護する必要があるツリーの読み取りアクセスを制限し、特定の CUG インスタンスと共にリストされるプリンシパル、または CUG 評価から完全に除外されるプリンシパルに対しての読み取りのみを許可します。 これは、 **認証** 要素。
* 特定のツリーに対する認証を強制し、オプションで、そのツリーに対して専用のログインページを指定して、その後除外します。 これは、 **認証** 要素。

新しい実装は、認証要素と承認要素の間に線を引くように設計されています。 AEM 6.3 以降では、認証要件を明示的に追加することなく、読み取りアクセスを制限できます。 例えば、特定のインスタンス全体で認証が必要な場合や、特定のツリーが既に認証が必要なサブツリー内に存在する場合などです。

同様に、有効な権限設定を変更しなくても、特定のツリーに認証要件をマークできます。組み合わせと結果は、 [CUG ポリシーと認証要件の組み合わせ](/help/sites-administering/closed-user-groups.md#combining-cug-policies-and-the-authentication-requirement) 」セクションに入力します。

## 概要 {#overview}

### 認証：読み取りアクセスの制限 {#authorization-restricting-read-access}

CUG の主な機能は、選択したプリンシパル以外のすべてのユーザーに対して、コンテンツリポジトリ内の特定のツリーに対する読み取りアクセスを制限することです。 デフォルトのアクセス制御コンテンツをその場で操作する代わりに、CUG を表す専用のアクセス制御ポリシーを定義することで、新しい実装では異なるアプローチを取ります。

#### CUG のアクセス制御ポリシー {#access-control-policy-for-cug}

この新しいタイプのポリシーには、次の特徴があります。

* （Apache Jackrabbit API によって定義される）タイプ org.apache.jackrabbit.api.security.authorization.PrincipalSetPolicy のアクセス制御ポリシー。
* PrincipalSetPolicy は、変更可能なプリンシパルのセットに対する権限を付与します。
* 付与される権限とポリシーの有効範囲は、実装の詳細です。

CUG の表現に使用される PrincipalSetPolicy の実装は、さらに次も定義します。

* CUG ポリシーは、通常の JCR 項目に対する読み取りアクセスのみを許可します（例えば、アクセス制御コンテンツは除外されます）。
* スコープは、CUG ポリシーを保持するアクセス制御ノードによって定義されます。
* CUG ポリシーはネストでき、ネストされた CUG は「親」CUG のプリンシパルセットを継承せずに新しい CUG を開始します。
* 評価が有効な場合、ポリシーの効果はサブツリー全体に継承され、次にネストされた CUG が継承されます。

これらの CUG ポリシーは、oak-authorization-cug と呼ばれる別の認証モジュールを介して、AEM インスタンスに導入されます。このモジュールは、独自のアクセス制御管理および権限評価に付属しています。つまり、デフォルトのAEM設定には、複数の認証メカニズムを組み合わせた Oak コンテンツリポジトリ設定が付属しています。 詳しくは、[この Apache Oak ドキュメントページ](https://jackrabbit.apache.org/oak/docs/security/authorization/composite.html)を参照してください。

この複合セットアップでは、新しい CUG は、ターゲットノードに適用されている既存のアクセス制御コンテンツを置き換えません。ただし、この CUG は、元のアクセス制御に影響を与えずに後で削除可能な補助的要素として設計されており、AEM ではデフォルトでアクセス制御リストになります。

以前の実装とは異なり、新しい CUG ポリシーは常にアクセス制御コンテンツとして認識され、扱われます。 これは、JCR アクセス制御管理 API を使用して作成および編集されることを意味します。 詳しくは、[CUG ポリシーの管理](#managing-cug-policies)の節を参照してください。

#### CUG ポリシーの権限評価 {#permission-evaluation-of-cug-policies}

CUG 専用のアクセス制御管理に加え、新しい承認モデルでは、ポリシーの権限評価を条件付きで有効にできます。 これにより、ステージング環境で CUG ポリシーを設定し、実稼動環境にレプリケートされた後にのみ有効な権限の評価を有効にすることができます。

CUG ポリシーの権限評価と、デフォルトまたは追加の承認モデルとの連携は、Apache Jackrabbit Oak の複数の承認メカニズム用に設計されたパターンに従います。つまり、すべてのモデルがアクセスを付与する場合にのみ、特定の権限セットが付与されます。詳しくは、[このページ](https://jackrabbit.apache.org/oak/docs/security/authorization/composite.html)を参照してください。

CUG ポリシーの処理と評価を目的とした認証モデルに関連する権限評価には、次の特性が適用されます。

* 通常のノードおよびプロパティの読み取り権限のみを処理し、アクセス制御コンテンツの読み取りは処理しません
* 保護された JCR コンテンツの変更に必要な書き込み権限や種類の権限（アクセス制御、ノードタイプ情報、バージョン管理、ロック、ユーザー管理など）は処理されません。これらの権限は CUG ポリシーに影響を受けず、関連する認証モデルでは評価されません。 これらの権限が付与されるかどうかは、セキュリティ設定に設定された他のモデルに応じます。

1 つの CUG ポリシーが権限評価に与える影響は、次のように要約できます。

* 読み取りアクセスは拒否されます（除外されたプリンシパルやポリシーにリストされたプリンシパルを含むサブジェクトを除く）。
* このポリシーは、ポリシーとプロパティを保持する、アクセス制御されたノードで有効になります。
* この影響は、階層の下まで、つまり、アクセス制御されたノードによって定義されるアイテムツリーまで継承されます。
* ただし、アクセス制御されたノードの兄弟や祖先には影響しません。
* 特定の CUG の継承は、ネストされた CUG で停止します。

#### ベストプラクティス {#best-practices}

CUG を介した制限付き読み取りアクセスを定義する際には、次のベストプラクティスを考慮する必要があります。

* CUG は、読み取りアクセスの制限のために必要なのか、認証要件のために必要なのかを判断します。認証要件のために必要な場合、または両方のために必要な場合は、ベストプラクティスに関する節で「認証要件の詳細」を確認してください。
* 脅威の境界を特定し、データの機密性と、許可されたアクセスに関連する役割を明確に把握するために、保護する必要のあるデータまたはコンテンツの脅威モデルを作成します
* 一般的な認証に関する側面とベストプラクティスを念頭に置いたリポジトリコンテンツと CUG をモデル化します。

   * 読み取り権限は、特定の CUG と、設定でデプロイされた他のモジュールの評価権限が、特定のサブジェクトが特定のリポジトリ項目を読み取ることを許可する場合にのみ付与されることに注意してください
   * 読み取りアクセスが既に他の認証モジュールによって制限されている冗長 CUG の作成を避けます
   * ネストされた CUG の過剰な必要性は、コンテンツデザインの問題を強調する可能性があります
   * CUG の非常に過度な必要性（例えば、すべてのページ）は、アプリケーションやコンテンツの特定のセキュリティニーズに合わせて、潜在的により適したカスタム認証モデルの必要性を示している可能性があります。

* CUG ポリシーでサポートされるパスをリポジトリ内のいくつかのツリーに制限して、パフォーマンスを最適化します。 例えば、AEM 6.3 よりデフォルト値として付属している /content ノード下にのみ CUG を許可します。
* CUG ポリシーは、小さなプリンシパルのセットに対して読み取りアクセスを許可するように設計されています。 多数のプリンシパルが必要な場合は、コンテンツやアプリケーションのデザインの問題を強調表示する可能性があるので、再度検討する必要があります。

### 認証：認証要件の定義 {#authentication-defining-the-auth-requirement}

CUG 機能の認証関連の部分を使用すると、認証が必要なツリーをマークし、必要に応じて専用のログインページを指定できます。 旧バージョンに準じて、新しい実装では、コンテンツリポジトリ内で認証を必要とするツリーをマークできます。また、条件によっては、`Sling org.apache.sling.api.auth.Authenticator` との同期を有効にして、強制的に要件を適用し、ログインリソースにリダイレクトすることも可能です。

これらの要件は、`sling.auth.requirements` 登録プロパティを提供する OSGi サービスによって Authenticator に登録されます。次に、これらのプロパティを使用して、認証要件を動的に拡張します。 詳しくは、 [Sling ドキュメント](https://sling.apache.org/apidocs/sling7/org/apache/sling/auth/core/AuthConstants.html#AUTH_REQUIREMENTS).

#### 専用の Mixin タイプを使用した認証要件の定義 {#defining-the-authentication-requirement-with-a-dedicated-mixin-type}

セキュリティ上の理由から、新しい実装では、残存している JCR プロパティを、`granite:AuthenticationRequired` という名前の専用の mixin タイプで置き換えます。この mixin タイプは、ログインパス `granite:loginPath` に、STRING タイプの単一のオプションプロパティを定義します。この mixin タイプに関連するコンテンツが変更された場合にのみ、Apache Sling Authenticator に登録される要件が更新されます。この変更は、一時的な変更を永続化する際に追跡されるので、有効にするには `javax.jcr.Session.save()` を呼び出す必要があります。

同じことが `granite:loginPath` プロパティにも当てはまります。認証要件関連の mixin タイプで定義されている場合にのみ考慮されます。 残存しているプロパティをこの名前で非構造化 JCR ノードに追加しても、期待した効果は得られず、OSGi 登録を更新するハンドラーはこのプロパティを無視します。

>[!NOTE]
>
>ログインパスプロパティの設定はオプションで、認証が必要なツリーがデフォルトのログインページや継承されたログインページにフォールバックできない場合にのみ必要です。 詳しくは、 [ログインパスの評価](/help/sites-administering/closed-user-groups.md#evaluation-of-login-path) 下

#### Sling Authenticator を使用した認証要件およびログインパスの登録 {#registering-the-authentication-requirement-and-login-path-with-the-sling-authenticator}

このタイプの認証要件は、特定の実行モードと、コンテンツリポジトリにあるツリーの小さいサブセットに限定されることが想定されるため、認証要件の mixin タイプおよびログインパスプロパティの追跡すると結果は条件次第となり、サポートパスが定義された該当する設定に関連付けられます（詳しくは、後述の「設定オプション」を参照してください）。したがって、サポートパスの有効範囲内で変更があった場合にのみ、OSGi 登録の更新が実行され、それ以外の場所では、mixin タイプもログインパスプロパティも無視されます。

デフォルトの AEM セットアップでは、この設定を利用できるようにするために、mixin を author 実行モードで設定し、その設定をパブリッシュインスタンスへのレプリケーション時にのみ有効にできるようになりました。Sling での認証要件の強制方法について詳しくは、[このページ](https://sling.apache.org/documentation/the-sling-engine/authentication/authenticationframework.html)を参照してください。

`granite:AuthenticationRequired` mixin タイプを設定済みのサポートパス内に追加すると、関係するハンドラーの OSGi 登録が更新され、`sling.auth.requirements` プロパティを含む新しいエントリが追加されます。特定の認証要件がオプション `granite:loginPath` プロパティの値は、認証要件から除外するために、Authenticator に「 — 」プレフィックスと共に登録されます。

#### 認証要件の評価と継承 {#evaluation-and-inheritance-of-the-authentication-requirement}

Apache Sling 認証の要件は、ページまたはノード階層を通じて継承されると想定されます。 継承の詳細と、順序や優先順位などの認証要件の評価は実装の詳細と見なされ、この記事には記載されません。

#### ログインパスの評価 {#evaluation-of-login-path}

認証時の対応リソースへのログインパスとリダイレクトの評価は、現在、Adobe Granite Login Selector Authentication Handler（`com.day.cq.auth.impl.LoginSelectorHandler`）の詳細で実装されています。このハンドラーは、AEM にデフォルトで設定されている Apache Sling AuthenticationHandler です。

`AuthenticationHandler.requestCredentials` を呼び出すと、このハンドラーは、ユーザーのリダイレクト先となるマッピングログインページの特定を試みます。これには、次の手順が含まれます。

* リダイレクトの理由として、期限切れのパスワードと通常のログインの必要性を区別します。
* 通常のログインの場合、は、次の順序でログインパスを取得できるかどうかをテストします。

   * 新しい `com.adobe.granite.auth.requirement.impl.RequirementService` で実装される LoginPathProvider から
   * 廃止された古い CUG 実装から
   * `LoginSelectorHandler` で定義したログインページマッピングから
   * 最後に、`LoginSelectorHandler` で定義したデフォルトログインページへのフォールバック

* 前述の呼び出しから有効なログインパスが取得されると、ユーザーのリクエストはすぐに、そのページにリダイレクトされます。

このドキュメントの目的は、内部の `LoginPathProvider` インターフェイスによって公開されるログインパスの評価です。AEM 6.3 以降に出荷された実装は、次のように動作します。

* ログインパスの登録は、リダイレクトの理由として、期限切れのパスワードと通常のログインの必要性を区別することによって異なります
* 通常のログインの場合、ログインパスが次の順序で取得できるかどうかをテストします。

   * 新しい `com.adobe.granite.auth.requirement.impl.RequirementService` で実装される `LoginPathProvider` から
   * 廃止された古い CUG 実装から
   * `LoginSelectorHandler` で定義したログインページマッピングから
   * 最後に、`LoginSelectorHandler` で定義したデフォルトログインページへのフォールバック

* 前述の呼び出しから有効なログインパスが取得されると、ユーザーのリクエストはすぐに、そのページにリダイレクトされます。

Granite の新しい認証要件のサポートで実装される `LoginPathProvider` は、`granite:loginPath` プロパティで定義したログインパスを公開します。また、これらのプロパティは、前述の mixin タイプによって定義されます。ログインパスとプロパティ値自体を保持するリソースパスのマッピングはメモリに保持され、階層内の他のノードに適したログインパスを見つけるために評価されます。

>[!NOTE]
>
>評価は、設定済みのサポート対象パス内のに配置されているリソースに関連付けられたリクエストに対してのみ実行されます。 その他のリクエストの場合は、ログインパスを決定する別の方法が評価されます。

#### ベストプラクティス {#best-practices-1}

認証要件を定義する際は、次のベストプラクティスを考慮する必要があります。

* 認証要件のネストを避ける：ツリーの最初に 1 つの auth 要件マーカーを配置すれば十分で、ターゲットノードで定義されたサブツリー全体に継承されます。 そのツリー内の追加の認証要件は冗長と見なす必要があり、Apache Sling 内の認証要件を評価する際に、パフォーマンスの問題が発生する可能性があります。 認証と認証に関連する CUG 領域を分離することで、CUG または他の種類のポリシーを使用して読み取りアクセスを制限し、同時にツリー全体に対して認証を実行できます。
* 再びネストされたサブツリーを要件から除外する必要なく、認証要件がツリー全体に適用されるように、リポジトリのコンテンツをモデル化します。
* 余分なログインパスの指定を回避するには、次のようにします。

   * 継承に依存し、ネストされたログインパスを定義しないようにする
   * オプションのログインパスを、デフォルト値または継承された値に対応する値に設定しないでください。
   * アプリケーション開発者は、`LoginSelectorHandler` に関連付けられるグローバルなログインパス設定（デフォルトとマッピングの両方）に設定する必要があるログインパスを識別してください。

## リポジトリでの表現 {#representation-in-the-repository}

### リポジトリ内の CUG ポリシー表現 {#cug-policy-representation-in-the-repository}

新しい CUG ポリシーがリポジトリコンテンツにどのように反映されるかについては、Oak のドキュメントに記載されています。詳しくは、 [このページ](https://jackrabbit.apache.org/oak/docs/security/authorization/cug.html#Representation_in_the_Repository).

### リポジトリの認証要件 {#authentication-requirement-in-the-repository}

個別の認証要件の必要性は、ターゲットノードに配置された専用の mixin ノードタイプでリポジトリコンテンツに反映されます。mixin タイプは、ターゲットノードで定義されるツリーの専用のログインページを指定するオプションのプロパティを定義します。

ログインパスに関連付けられたページは、そのツリーの内部または外部に配置される場合があります。 認証要件から除外されます。

```java
[granite:AuthenticationRequired]
      mixin
      - granite:loginPath (STRING)
```

## CUG ポリシーと認証要件の管理 {#managing-cug-policies-and-authentication-requirement}

### CUG ポリシーの管理 {#managing-cug-policies}

CUG の読み取りアクセスを制限する新しいタイプのアクセス制御ポリシーは、JCR アクセス制御管理 API を使用して管理され、[JCR 2.0 仕様](https://www.adobe.io/experience-manager/reference-materials/spec/jcr/2.0/16_Access_Control_Management.html) に記載されるメカニズムに従います。

#### 新しい CUG ポリシーを設定 {#set-a-new-cug-policy}

以前に CUG が設定されていないノードに新しい CUG ポリシーを適用するコード。 `getApplicablePolicies` は、まだ一度も設定されていない新しいポリシーのみを返すことに注意が必要です。最後に、ポリシーを書き戻し、変更を保持する必要があります。

```java
String path = [...] // needs to be a supported, absolute path

Principal toAdd1 = [...]
Principal toAdd2 = [...]
Principal toRemove = [...]

AccessControlManager acMgr = session.getAccessControlManager();
PrincipalSetPolicy cugPolicy = null;

AccessControlPolicyIterator it = acMgr.getApplicablePolicies(path);
while (it.hasNext()) {
        AccessControlPolicy policy = it.nextAccessControlPolicy();
        if (policy instanceof PrincipalSetPolicy) {
           cugPolicy = (PrincipalSetPolicy) policy;
           break;
        }
}

if (cugPolicy == null) {
   log.debug("no applicable policy"); // path not supported or no applicable policy (e.g.
                                                   // the policy was set before)
   return;
}

cugPolicy.addPrincipals(toAdd1, toAdd2);
cugPolicy.removePrincipals(toRemove));

acMgr.setPolicy(path, cugPolicy); // as of this step the policy can be edited/removed
session.save();
```

#### 既存の CUG ポリシーの編集 {#edit-an-existing-cug-policy}

既存の CUG ポリシーを編集するには、次の手順が必要です。 変更したポリシーを書き戻す必要があり、変更は `javax.jcr.Session.save()`.

```java
String path = [...] // needs to be a supported, absolute path

Principal toAdd1 = [...]
Principal toAdd2 = [...]
Principal toRemove = [...]

AccessControlManager acMgr = session.getAccessControlManager();
PrincipalSetPolicy cugPolicy = null;

for (AccessControlPolicy policy : acMgr.getPolicies(path)) {
     if (policy instanceof PrincipalSetPolicy) {
        cugPolicy = (PrincipalSetPolicy) policy;
        break;
     }
}

if (cugPolicy == null) {
   log.debug("no policy to edit"); // path not supported or policy not set before
   return;
}

if (cugPolicy.addPrincipals(toAdd1, toAdd2) || cugPolicy.removePrincipals(toRemove)) {
   acMgr.setPolicy(path, cugPolicy);
   session.save();
} else {
     log.debug("cug policy not modified");
}
```

### 有効な CUG ポリシーの取得 {#retrieve-effective-cug-policies}

JCR アクセス制御管理では、特定のパスで有効なポリシーを取得するためのベストエフォート方式を定義します。 CUG ポリシーの評価は、対応する設定が有効になっているかどうかが条件となるので、特定の CUG ポリシーが特定のインストールで有効かどうかを調べるには、`getEffectivePolicies`を呼び出すと簡単です。

>[!NOTE]
>
>～間の違いにご注意ください `getEffectivePolicies` と、特定のパスが既に既存の CUG に含まれているかどうかを調べるために階層を上に向かう後続のコード例です。

```java
String path = [...] // needs to be a supported, absolute path

AccessControlManager acMgr = session.getAccessControlManager();
PrincipalSetPolicy cugPolicy = null;

// log an debug message of all CUG policies that take effect at the given path
// there could be zero, one or many (creating nested CUGs is possible)
for (AccessControlPolicy policy : acMgr.getEffectivePolicies(path) {
     if (policy instanceof PrincipalSetPolicy) {
        String policyPath = "-";
        if (policy instanceof JackrabbitAccessControlPolicy) {
           policyPath = ((JackrabbitAccessControlPolicy) policy).getPath();
        }
        log.debug("Found effective CUG for path '{}' at '{}', path, policyPath);
     }
}
```

#### 継承された CUG ポリシーの取得 {#retrieve-inherited-cug-policies}

特定のパスで定義されたネストされた CUG を、それらが有効かどうかに関係なく検索する。 詳しくは、 [設定オプション](/help/sites-administering/closed-user-groups.md#configuration-options) 」セクションに入力します。

```java
String path = [...]

List<AccessControlPolicy> cugPolicies = new ArrayList<AccessControlPolicy>();
while (isSupportedPath(path)) {
     for (AccessControlPolicy policy : acMgr.getPolicies(path)) {
         if (policy instanceof PrincipalSetPolicy) {
            cugPolicies.add(policy);
         }
      }
      path = (PathUtils.denotesRoot(path)) ? null : PathUtils.getAncestorPath(path, 1);
}
```

#### Pincipal による CUG ポリシーの管理 {#managing-cug-policies-by-pincipal}

で定義される拡張機能 `JackrabbitAccessControlManager` CUG ポリシーは常にすべてのプリンシパルに影響するので、プリンシパルによるアクセス制御ポリシーの編集を許可するのは CUG アクセス制御管理では実装されません。次に示す `PrincipalSetPolicy` は読み取りアクセス権を付与されますが、他のすべてのプリンシパルはターゲットノードで定義されたツリー内のコンテンツを読み取ることができません。

対応するメソッドは常に空のポリシー配列を返しますが、例外はスローしません。

### 認証要件の管理 {#managing-the-authentication-requirement}

新しい認証要件の作成、変更または削除は、ターゲットノードの有効なノードタイプを変更することで達成されます。その後、オプションのログインパスプロパティへの書き込みには、通常の JCR API を使用できます。

>[!NOTE]
>
>上記の特定のターゲットノードに対する変更は、Apache Sling Authenticator に反映されます ( `RequirementHandler` が設定され、ターゲットは、サポートされるパスで定義されるツリーに含まれます（設定オプションの節を参照）。
>
>詳しくは、「[Mixin ノードタイプの割り当て]」（https://docs.adobe.com/docs/en/spec/jcr/2.0/10_Writing.html#10.10.3 Mixin ノードタイプの割り当て）および 「[ノードの追加とプロパティの設定]」（https://docs.adobe.com/docs/en/spec/jcr/2.0/10_Writing.html#10.4 ノードの追加とプロパティの設定）を参照してください。

#### 新しい認証要件の追加 {#adding-a-new-auth-requirement}

新しい認証要件を作成する手順を以下に示します。 新しい認証要件は、ターゲットノードを含むツリーに `RequirementHandler` が設定済みの場合にのみ、Apache Sling Authenticator に登録されます。

```java
Node targetNode = [...]

targetNode.addMixin("granite:AuthenticationRequired");
session.save();
```

#### ログインパスを使用した新しい認証要件の追加 {#add-a-new-auth-requirement-with-login-path}

ログインパスを含む新しい認証要件を作成する手順です。 ログインパスの要件と除外は、Apache Sling Authenticator に登録されるのは、 `RequirementHandler` は、ターゲットノードを含むツリー用に設定されています。

```java
Node targetNode = [...]
String loginPath = [...] // STRING property

Node targetNode = session.getNode(path);
targetNode.addMixin("granite:AuthenticationRequired");

targetNode.setProperty("granite:loginPath", loginPath);
session.save();
```

#### 既存のログインパスの変更 {#modify-an-existing-login-path}

既存のログインパスを変更する手順については、以下で詳しく説明します。 変更結果は、ターゲットノードを含むツリーに `RequirementHandler` が設定済みの場合にのみ、Apache Sling Authenticator に登録されます。以前のログインパスの値は登録から削除されます。 ターゲットノードに関連付けられている認証要件は、この変更の影響を受けません。

```java
Node targetNode = [...]
String newLoginPath = [...] // STRING property

if (targetNode.isNodeType("granite:AuthenticationRequired")) {
   targetNode.setProperty("granite:loginPath", newLoginPath);
   session.save();
} else {
     log.debug("cannot modify login path property; mixin type missing");
}
```

#### 既存のログインパスの削除 {#remove-an-existing-login-path}

既存のログインパスを削除する手順です。 ログインパスのエントリは、ターゲットノードを含むツリーに `RequirementHandler` が設定済みの場合にのみ、Apache Sling Authenticator から登録が解除されます。ターゲットノードに関連付けられている認証要件は影響を受けません。

```java
Node targetNode = [...]

if (targetNode.hasProperty("granite:loginPath") &&
   targetNode.isNodeType("granite:AuthenticationRequired")) {
   targetNode.setProperty("granite:loginPath", null);
   session.save();
} else {
     log.debug("cannot remove login path property; mixin type missing");
}
```

または、次の方法を使用して、同じ目的を達成することもできます。

```java
String path = [...] // absolute path to target node

String propertyPath = PathUtils.concat(path, "granite:loginPath");
if (session.propertyExists(propertyPath)) {
    session.getProperty(propertyPath).remove();
    // or: session.removeItem(propertyPath);
    session.save();
}
```

#### 認証要件の削除 {#remove-an-auth-requirement}

既存の認証要件を削除する手順です。 この要件は、Apache Sling Authenticator からの登録が解除されるのは、 `RequirementHandler` は、ターゲットノードを含むツリー用に設定されています。

```java
Node targetNode = [...]
targetNode.removeMixin("granite:AuthenticationRequired");

session.save();
```

#### 有効な認証要件の取得 {#retrieve-effective-auth-requirements}

Apache Sling Authenticator に登録されている有効なすべての認証要件を読み取る専用のパブリック API はありません。ただし、リストは、`https://<serveraddress>:<serverport>/system/console/slingauth` のシステムコンソール、「**認証要件の設定**」セクションで公開されています。

次の画像は、デモコンテンツを含むAEMパブリッシュインスタンスの認証要件を示しています。 強調表示されているコミュニティページのパスは、このドキュメントで説明する実装によって追加された要件が Apache Sling Authenticator にどのように反映されるかを示しています。

>[!NOTE]
>
>この例では、オプションのログインパスプロパティは設定されていませんでした。 その結果、2 番目のエントリは認証子に登録されていません。

![chlimage_1-62](assets/chlimage_1-62.jpeg)

#### 有効なログインパスの取得 {#retrieve-the-effective-login-path}

現時点では、認証が必要なリソースに匿名アクセスするときに有効になるログインパスを取得できるパブリック API はありません。ログインパスの取得方法に関する実装の詳細については、「ログインパスの評価」の節を参照してください。

ただし、この機能で定義されたログインパス以外に、ログインへのリダイレクトを指定する別の方法があります。この方法は、コンテンツモデルを設計する際や、特定のAEMインストールの認証要件を考慮に入れる必要があります。

#### 継承された認証要件の取得 {#retrieve-the-inherited-auth-requirement}

ログインパスと同様に、コンテンツに定義されている継承された認証要件を取得するパブリック API はありません。 以下のサンプルに、特定の階層に定義されるすべての認証要件を（有効になっているかどうかに関係なく）リストする方法を示します。詳しくは、[設定オプション](/help/sites-administering/closed-user-groups.md#configuration-options)を参照してください。

>[!NOTE]
>
>認証要件とログインパスのどちらについても継承メカニズムを利用するようにし、ネストされた認証要件を作成しないことが推奨されます。
>
>詳しくは、[認証要件の評価と継承](#evaluation-and-inheritance-of-the-authentication-requirement)、[ログインパスの評価](#evaluation-of-login-path)、および[ベストプラクティス](#best-practices)を参照してください。

```java
String path = [...]
Node node = session.getNode(path);

Map<String, String> authRequirements = new ArrayList<String, String>();
while (isSupported(node)) {
     if (node.isNodeType("granite:AuthenticationRequired")) {
         String loginPath = (node.hasProperty("granite:loginPath") ?
                                     node.getProperty("granite:loginPath").getString() :
                                     "";
        authRequirements.put(node.getPath(), loginPath);
        node = node.getParent();
     }
}
```

### CUG ポリシーと認証要件の組み合わせ {#combining-cug-policies-and-the-authentication-requirement}

次の表に、CUG ポリシーの有効な組み合わせと、両方のモジュールが設定を通じて有効になっているAEMインスタンスの認証要件を示します。

| **認証が必要** | **ログインパス** | **制限付き読み取りアクセス** | **予想される効果** |
|---|---|---|---|
| はい | はい | はい | 有効な権限評価によってアクセス権が付与されている場合、ユーザーによっては CUG ポリシーのマークが付いたサブツリー以外、表示できなくなる場合があります。未認証ユーザーは、指定されたログインページにリダイレクトされます。 |
| はい | いいえ | はい | 有効な権限評価によってアクセス権が付与されている場合、ユーザーによっては CUG ポリシーのマークが付いたサブツリー以外、表示できなくなる場合があります。認証されていないユーザーは、継承されたデフォルトのログインページにリダイレクトされます。 |
| はい | はい | いいえ | 認証されていないユーザーは、指定のログインページにリダイレクトされます。認証要件でマークされたツリーの表示が許可されているかどうかは、そのサブツリーに含まれる個々の項目の有効な権限によって異なります。 読み取りアクセスを制限する専用の CUG が存在しない。 |
| はい | いいえ | 不可 | 認証されていないユーザーは、継承されたデフォルトのログインページにリダイレクトされます。認証要件でマークされたツリーの表示が許可されるかどうかは、そのサブツリーに含まれる個々の項目の有効な権限によって異なります。 読み取りアクセスを制限する専用の CUG が存在しない。 |
| いいえ | いいえ | はい | 有効な権限評価によってアクセス権が付与されている場合、認証されたユーザー、認証されていないユーザーはいずれも CUG ポリシーのマークが付いたサブツリー以外、表示できなくなる場合があります。認証されていないユーザーも同じように処理され、ログインにリダイレクトされません。 |

>[!NOTE]
>
>「ログインパス」は、認証要件に関連するオプションの属性なので、「認証要件」 = なし、「ログインパス」 = ありの組み合わせは存在しません。mixin タイプの定義を追加せずに JCR プロパティを名前で指定するだけでは、そのプロパティは有効にならず、対応するハンドラーによって無視されます。

## OSGi コンポーネントと設定 {#osgi-components-and-configuration}

この節では、OSGi コンポーネントと、新しい CUG 実装で導入された個々の設定オプションの概要を説明します。

また、CUG マッピングに関するドキュメントを参照して、新旧の実装間での設定オプションの全体的な対応関係を確認してください。

### 承認：セットアップと設定 {#authorization-setup-and-configuration}

新しい承認関連のパーツは、AEM のデフォルトインストールの一部である **Oak CUG Authorization** バンドル（`org.apache.jackrabbit.oak-authorization-cug`）に含まれています。このバンドルは、読み取りアクセスを管理する追加の方法としてデプロイすることを目的とした、個別の認証モデルを定義します。

#### CUG 認証の設定 {#setting-up-cug-authorization}

CUG 承認のセットアップについては、[関連する Apache ドキュメント](https://jackrabbit.apache.org/oak/docs/security/authorization/cug.html#pluggability)に詳しく記載されています。デフォルトでは、AEMにはすべての実行モードで CUG 認証がデプロイされています。 別の認証設定が必要なインストールでは、CUG 認証を無効にする手順も使用できます。

#### リファラーフィルタの設定 {#configuring-the-referrer-filter}

また、CDN やロードバランサーなどを介した AEM へのアクセスに使用できるすべてのホスト名を含む [Sling Referrer Filter](/help/sites-administering/security-checklist.md#the-sling-referrer-filter) を設定する必要もあります。

リファラーフィルターが設定されていない場合、ユーザーが CUG サイトにログインしようとすると、次のようなエラーが表示されます。

```shell
31.01.2017 13:49:42.321 *INFO* [qtp1263731568-346] org.apache.sling.security.impl.ReferrerFilter Rejected referrer header for POST request to /libs/granite/core/content/login.html/j_security_check : https://hostname/libs/granite/core/content/login.html?resource=%2Fcontent%2Fgeometrixx%2Fen%2Ftest-site%2Ftest-page.html&$$login$$=%24%24login%24%24&j_reason=unknown&j_reason_code=unknown
```

#### OSGi コンポーネントの特性 {#characteristics-of-osgi-components}

認証要件を定義し、専用のログインパスを指定するために、次の 2 つの OSGi コンポーネントが導入されました。

* `org.apache.jackrabbit.oak.spi.security.authorization.cug.impl.CugConfiguration`
* `org.apache.jackrabbit.oak.spi.security.authorization.cug.impl.CugExcludeImpl`

**org.apache.jackrabbit.oak.spi.security.authorization.cug.impl.CugConfiguration**

<table> 
 <tbody> 
  <tr> 
   <td>ラベル</td> 
   <td>Apache Jackrabbit Oak CUG 設定</td> 
  </tr> 
  <tr> 
   <td>説明</td> 
   <td>CUG 権限の設定と評価に関する認証設定。</td> 
  </tr> 
  <tr> 
   <td>設定プロパティ</td> 
   <td> 
    <ul> 
     <li><code>cugSupportedPaths</code></li> 
     <li><code>cugEnabled</code></li> 
     <li><code>configurationRanking</code></li> 
    </ul> <p>また、以下の<a href="/help/sites-administering/closed-user-groups.md#configuration-options" target="_blank">設定オプション</a>を参照してください。</p> </td> 
  </tr> 
  <tr> 
   <td>設定ポリシー</td> 
   <td><code>ConfigurationPolicy.REQUIRE</code></td> 
  </tr> 
  <tr> 
   <td>参照</td> 
   <td><code>CugExclude (ReferenceCardinality.OPTIONAL_UNARY)</code></td> 
  </tr> 
 </tbody> 
</table>

**org.apache.jackrabbit.oak.spi.security.authorization.cug.impl.CugExcludeImpl**

<table> 
 <tbody> 
  <tr> 
   <td>ラベル</td> 
   <td>Apache Jackrabbit Oak CUG 除外リスト</td> 
  </tr> 
  <tr> 
   <td>説明</td> 
   <td>設定された名前を持つプリンシパルを CUG 評価から除外できます。</td> 
  </tr> 
  <tr> 
   <td>設定プロパティ</td> 
   <td> 
    <ul> 
     <li><code>principalNames</code></li> 
    </ul> <p>後述の「設定オプション」の節も参照してください。</p> </td> 
  </tr> 
  <tr> 
   <td>設定ポリシー</td> 
   <td><code>ConfigurationPolicy.REQUIRE</code></td> 
  </tr> 
  <tr> 
   <td>参照</td> 
   <td>該当なし</td> 
  </tr> 
 </tbody> 
</table>

#### 設定オプション {#configuration-options}

重要な設定オプションは次の通りです。

* `cugSupportedPaths`：CUG を含むことができるサブツリーを指定します。デフォルト値は設定されません。
* `cugEnabled`：現在の CUG ポリシーに対して権限評価を有効にする設定オプション。

CUG-authorization モジュールに関連する使用可能な設定オプションが次の場所にリストされ、詳しく説明されています： [Apache Oak ドキュメント](https://jackrabbit.apache.org/oak/docs/security/authorization/cug.html#configuration).

#### CUG 評価からのプリンシパルの除外 {#excluding-principals-from-cug-evaluation}

CUG 評価の個々のプリンシパルの除外は、前の実装から適用されています。 新しい CUG 認承では、CugExclude という名前の専用インターフェイスを使用してこれを説明します。Apache Jackrabbit Oak 1.4 には、プリンシパルの固定セットを除外するデフォルト実装と、個々のプリンシパル名を設定できる拡張実装が付属しています。後者は、AEMパブリッシュインスタンスで設定されます。

AEM 6.3 以降のデフォルトでは、次のプリンシパルは CUG ポリシーの影響を受けません。

* 管理プリンシパル（管理者ユーザー、管理者グループ）
* サービスユーザープリンシパル
* リポジトリの内部システムプリンシパル

詳しくは、 [AEM 6.3 以降のデフォルト設定](#default-configuration-since-aem) 」の節を参照してください。

除外する「管理者」グループは、システムコンソールの **Apache Jackrabbit Oak CUG Exclude List**&#x200B;の設定セクションで変更または拡張できます。

また、特殊なニーズがある場合は、CugExclude インターフェイスのカスタム実装を提供、導入して、除外するプリンシパルのセットを調整することもできます。詳しい説明と実装例については、[プラグの可／不可](https://jackrabbit.apache.org/oak/docs/security/authorization/cug.html#pluggability)に関するドキュメントを参照してください。

### 認証：セットアップと設定 {#authentication-setup-and-configuration}

新しい認証関連のパーツは、**Adobe Granite Authentication Handler** バンドル（`com.adobe.granite.auth.authhandler` バージョン 5.6.48）に含まれています。このバンドルはAEMのデフォルトインストールの一部です。

非推奨の CUG サポートに代わる認証要件を設定するには、一部の OSGi コンポーネントが、特定のAEMインストールに存在し、アクティブである必要があります。 詳しくは、 **OSGi コンポーネントの特性** 下

>[!NOTE]
>
>RequirementHandler の必須設定オプションにより、認証関連のパーツは、サポートされる一連のパスを指定して機能が有効になっている場合にのみアクティブになります。 標準のAEMインストールでは、この機能はオーサー実行モードでは無効になり、パブリッシュ実行モードでは/content に対して有効になります。

**OSGi コンポーネントの特性**

認証要件を定義し、専用のログインパスを指定するために、次の 2 つの OSGi コンポーネントが導入されました。

* `com.adobe.granite.auth.requirement.impl.RequirementService`
* `com.adobe.granite.auth.requirement.impl.DefaultRequirementHandler`

**com.adobe.granite.auth.requirement.impl.RequirementService**

<table> 
 <tbody> 
  <tr> 
   <td>ラベル</td> 
   <td>-</td> 
  </tr> 
  <tr> 
   <td>説明</td> 
   <td><code>LoginSelectorHandler</code>に公開される、認証要件（<code>granite:AuthenticationRequirement</code>Mixin タイプを通して）に影響を与えるコンテンツの変更の監視者、およびログインパスを登録する認証要件専用の OSGi サービス。 </td> 
  </tr> 
  <tr> 
   <td>設定プロパティ</td> 
   <td>-</td> 
  </tr> 
  <tr> 
   <td>設定ポリシー</td> 
   <td><code>ConfigurationPolicy.OPTIONAL</code></td> 
  </tr> 
  <tr> 
   <td>参照</td> 
   <td> 
    <ul> 
     <li><code>RequirementHandler (ReferenceCardinality.MANDATORY_UNARY)</code></li> 
     <li><code>Executor (ReferenceCardinality.MANDATORY_UNARY)</code></li> 
    </ul> </td> 
  </tr> 
 </tbody> 
</table>

**com.adobe.granite.auth.requirement.impl.DefaultRequirementHandler**

| ラベル | Adobe Granite 認証要件とログインパスハンドラー |
|---|---|
| 説明 | Apache Sling 認証の要件と、関連するログインパスに対応する除外を更新する`RequirementHandler`実装。 |
| 設定プロパティ | `supportedPaths` |
| 設定ポリシー | `ConfigurationPolicy.REQUIRE` |
| 参照 | 該当なし |

#### 設定オプション {#configuration-options-1}

CUG 書き換えの認証関連部分には、AdobeGranite Authentication Requirement および Login Path Handler に関連付けられた 1 つの設定オプションのみが付属しています。

**認証要件およびログイン・パス・ハンドラ**

<table> 
 <tbody> 
  <tr> 
   <td>プロパティ</td> 
   <td>タイプ</td> 
   <td>デフォルト値</td> 
   <td>説明</td> 
  </tr> 
  <tr> 
   <td><p>ラベル = サポートされているパス</p> <p>名前 = 「supportedPaths」</p> </td> 
   <td>Set&lt;String&gt;</td> 
   <td>-</td> 
   <td>このハンドラーにより認証要件が適用されるパス。<code>granite:AuthenticationRequirement</code>Mixin タイプをノードに適用せずに追加する場合は（例えばオーサーインスタンスで）、この設定を未設定のままにしてください。未設定にしておくと、この機能は無効になります。 </td> 
  </tr> 
 </tbody> 
</table>

## AEM 6.3 以降のデフォルト設定 {#default-configuration-since-aem}

AEMの新規インストールでは、デフォルトで、CUG 機能の認証関連部分と認証関連部分の両方に新しい実装が使用されます。 古い実装「AdobeGranite 閉じられたユーザーグループ (CUG) のサポート」は廃止され、すべてのAEMインストールでデフォルトで無効になります。 代わりに、新しい実装は次のように有効になります。

### オーサーインスタンス {#author-instances}

| **「Apache Jackrabbit Oak CUG 設定」** | **説明** |
|---|---|
| サポートされているパス `/content` | CUGpolicies のアクセス制御管理が有効になっています。 |
| CUG 評価が有効の FALSE | 権限の評価は無効になっています。CUG ポリシーは無効です。 |
| ランキング | 200 | Oak のドキュメントを参照してください。 |

>[!NOTE]
>
>設定なし **Apache Jackrabbit Oak CUG 除外リスト** および **AdobeGranite 認証要件およびログインパスハンドラー** は、デフォルトのオーサリングインスタンスに存在します。

### パブリッシュインスタンス {#publish-instances}

| **「Apache Jackrabbit Oak CUG の設定」** | **説明** |
|---|---|
| サポートされているパス `/content` | CUG ポリシーのアクセス制御管理は、設定されたパスの下で有効になります。 |
| CUG 評価が有効の TRUE | 権限の評価は、設定されたパスの下で有効になります。CUG ポリシーは `Session.save()` で有効になります。 |
| ランキング | 200 | Oak のドキュメントを参照してください。 |

| **「Apache Jackrabbit Oak CUG 除外リスト」** | **説明** |
|---|---|
| プリンシパル名の管理者 | CUG 評価から管理者プリンシパルを除外します。 |

| **「Adobe Granite 認証要件とログインパスハンドラー」** | **説明** |
|---|---|
| サポートされているパス `/content` | `granite:AuthenticationRequired` Mixin タイプを使用してリポジトリで定義された認証要件は、`Session.save()` で `/content` の下で有効になります。Sling Authenticator が更新されます。 サポートされているパスの外側に mixin タイプを追加することは無視されます。 |

## CUG 認証および認証要件の無効化 {#disabling-cug-authorization-and-authentication-requirement}

特定のインストールで CUG を使用しなかったり、認証と承認に別の手段を使用したりした場合に、新しい実装を完全に無効にすることができます。

### CUG 認証を無効にする {#disable-cug-authorization}

詳しくは、 [CUG プラグ可能](https://jackrabbit.apache.org/oak/docs/security/authorization/cug.html#pluggability) 複合承認設定から CUG 承認モデルを削除する方法の詳細に関するドキュメント。

### 認証要件の無効化 {#disable-the-authentication-requirement}

`granite.auth.authhandler` モジュールが提供する認証要件のサポートを無効にするには、**Adobe Granite Authentication Requirement and Login Path Handler** に関連する設定を削除するだけで十分です。

>[!NOTE]
>
>ただし、設定を削除しても、mixin タイプの登録は解除されません。mixin タイプは有効にならなくてもノードに適用できます。

## 他のモジュールとのインタラクション {#interaction-with-other-modules}

### Apache Jackrabbit API {#apache-jackrabbit-api}

CUG 承認モデルで使用される新しいタイプのアクセス制御ポリシーを反映するために、Apache Jackrabbit で定義される API が拡張されました。 `jackrabbit-api` モジュールのバージョン 2.11.0 では、`javax.jcr.security.AccessControlPolicy` から拡張される、`org.apache.jackrabbit.api.security.authorization.PrincipalSetPolicy` という名前の新しいインターフェイスが定義されています。

### Apache Jackrabbit FileVault {#apache-jackrabbit-filevault}

Apache Jackrabbit FileVault の読み込みメカニズムは、タイプ `PrincipalSetPolicy` のアクセス制御ポリシーに対応するように調整されています。

### Apache Sling コンテンツ配布 {#apache-sling-content-distribution}

上記を参照 [Apache Jackrabbit FileVault](/help/sites-administering/closed-user-groups.md#apache-jackrabbit-filevault) 」セクションに入力します。

### AdobeGranite レプリケーション {#adobe-granite-replication}

複数のAEMインスタンス間で CUG ポリシーをレプリケートできるように、レプリケーションモジュールが若干調整されました。

* `DurboImportConfiguration.isImportAcl()` は、文字どおりに解釈され、`javax.jcr.security.AccessControlList` を実装するアクセス制御ポリシーにのみ影響します。

* `DurboImportTransformer` は、真の ACL に対してのみこの設定を考慮します。
* CUG 承認モデルによって作成される `org.apache.jackrabbit.api.security.authorization.PrincipalSetPolicy` インスタンスなどの他のポリシーは常にレプリケーションされ、設定オプション `DurboImportConfiguration.isImportAcl` () は無視されます。

CUG ポリシーのレプリケーションには 1 つ制約があります。対応する Mixin ノードタイプ `rep:CugMixin,` を削除せずに、特定の CUG ポリシーを削除した場合、レプリケーション時に CUG ポリシーの削除が反映されません。これに対処するには、ポリシーの削除時に常に mixin を削除する必要があります。 ただし、mixin タイプを手動で追加すると、この制限が表示される場合があります。

### AdobeGranite 認証ハンドラー {#adobe-granite-authentication-handler}

**バンドルに付属する認証ハンドラー** Adobe Granite HTTP Header Authentication Handler`com.adobe.granite.auth.authhandler` は、同じモジュールによって定義される `CugSupport` インターフェイスへの参照を保持します。これは、特定の環境内での「領域」の計算に使用され、このハンドラーによって設定される領域にフォールバックします。

このモジュールは、`CugSupport` への参照をオプションとして使用できるように調整されました。この調整により、既に廃止されている実装を特定のセットアップで再度有効にしても、最大限の後方互換性を確保できます。その実装を使用するインストールでは、CUG 実装から領域が抽出されることはありませんが、**Adobe Granite HTTP Header Authentication Handler** によって定義される領域が常に表示されます。

>[!NOTE]
>
>デフォルトでは、**Adobe Granite HTTP Header Authentication Handler** は、「Disable Login Page」（`auth.http.nologin`）オプションが有効になっているパブリッシュ実行モードでのみ設定されます。

### AEM ライブコピー {#aem-livecopy}

ライブコピーに関連した CUG の設定は、以下のようにノードとプロパティーを 1 つずつ追加することによってリポジトリーに表示されます。

* `/content/we-retail/us/en/blueprint/rep:cugPolicy`
* `/content/we-retail/us/en/LiveCopy@granite:loginPath`

これらの要素は両方とも、`cq:Page` に作成されます。現在の設計では、MSM は `cq:PageContent`（`jcr:content`）ノードの下にあるノードとプロパティのみを処理します。

そのため、CUG グループをブループリントからライブコピーにロールアウトすることはできません。ライブコピーを設定する際には、この点を考慮してください。

## 新しい CUG 実装に伴う変更 {#changes-with-the-new-cug-implementation}

この節の目的は、CUG 機能に加えられた変更の概要と、古い実装と新しい実装の比較を示すことです。 CUG サポートの設定方法に影響する変更をリストし、リポジトリコンテンツで CUG を管理する方法と方法を説明します。

### CUG の設定と設定の違い {#diferences-in-cug-setup-and-configuration}

廃止された OSGi コンポーネント **Adobe Granite Closed User Group (CUG) Support**（`com.day.cq.auth.impl.cug.CugSupportImpl`）は、新しいコンポーネントに置き換えられ、前の CUG 機能の承認関連のパーツと認証関連のパーツを分けて扱えるようになりました。

## リポジトリコンテンツにおける CUG の管理の違い {#differences-in-managing-cugs-in-the-repository-content}

以下の節では、実装とセキュリティの観点から、古い実装と新しい実装の違いを説明します。 新しい実装は同じ機能を提供することを目的としていますが、新しい CUG を使用する際に知っておくべき微妙な変更点があります。

### 認可に関する違い {#diferences-with-regards-to-authorization}

認証の観点からの主な違いを次のリストにまとめます。

**CUG 専用のアクセス制御コンテンツ**

古い実装では、デフォルトの承認モデルを使用して、公開時にアクセス制御リストポリシーを操作し、CUG が要求する設定で既存の ACE を置き換えていました。 これは、公開時に解釈された通常の残存 JCR プロパティを書き込むことでトリガーされました。

新しい実装では、デフォルトの承認モデルのアクセス制御設定は、作成、変更、または削除される CUG に影響されません。 代わりに、`PrincipalSetPolicy` という名前の新しいタイプのポリシーが、追加のアクセス制御コンテンツとして、ターゲットノードに適用されます。この追加ポリシーは、ターゲットノードの子として配置され、デフォルトのポリシーノードがある場合はその兄弟になります。

**アクセス制御管理での CUG ポリシーの編集**

この変更は、残りの JCR プロパティから専用のアクセス制御ポリシーに移行した場合、CUG 機能の承認部分を作成または変更するために必要な権限に影響を与えます。 この移行はアクセス制御コンテンツに対する変更と見なされるので、リポジトリに書き込むためには `jcr:readAccessControl` 権限と `jcr:modifyAccessControl` 権限が必要です。したがって、このコンテンツを設定または変更できるのは、ページのアクセス制御コンテンツを変更する権限を持つコンテンツ作成者のみです。 これは、通常の JCR プロパティを書き込む機能で十分だった古い実装とは対照的で、結果として権限のエスカレーションが発生します。

**ポリシーで定義されたターゲットノード**

CUG ポリシーは、読み取りアクセスの制限を受けるサブツリーを定義する JCR ノードで作成される必要があります。 CUG がツリー全体に影響すると想定される場合、これはAEMページになる可能性があります。

CUG ポリシーを指定のページの下にある jcr:content ノードにのみ配置すると、指定のページのコンテンツへのアクセスは制限されますが、兄弟ページや子ページには影響しません。 場合によってはこうしたケースも有効で、きめ細かなアクセスコンテンツを適用可能なリポジトリエディターによって達成できます。ただし、cq:cugEnabled プロパティを jcr:content ノードに配置することが、内部でページノードに再マッピングされた以前の実装とは対照的です。このマッピングは実行されなくなりました。

**CUG ポリシーによる権限評価**

古い CUG サポートから追加の承認モデルに移行したことで、有効な読み取り権限の評価方法が変更されています。詳しくは、 [Jackrabbit ドキュメント](https://jackrabbit.apache.org/oak/docs/security/authorization/composite.html): `CUGcontent` は、Oak リポジトリで設定されたすべてのモデルの権限評価で読み取りアクセス権が付与された場合にのみ、読み取りアクセス権が付与されます。

つまり、有効な権限の評価では、`CUGPolicy` とデフォルトのアクセス制御エントリの両方が考慮され、CUG コンテンツに対する読み取りアクセスは、両方のタイプのポリシーによって付与される場合にのみ付与されます。`/content` ツリー全体への読み取りアクセスが全員に付与されるデフォルトの AEM パブリッシュインストールでは、CUG ポリシーの効果は、古い実装のものと同じです。

**オンデマンド評価**

CUG 承認モデルを使用すると、アクセス制御管理と権限評価を個別にオンにできます。

* CUG を作成できる 1 つ以上のサポート対象パスがモジュールにある場合、アクセス制御管理は有効になります。
* 権限の評価は、オプションの場合にのみ有効です **CUG 評価が有効** が追加でオンになっています。

CUG ポリシーの新しいAEMのデフォルト設定評価では、「publish」実行モードでのみ有効になります。 詳細は、 [AEM 6.3 以降のデフォルト設定](#default-configuration-since-aem) を参照してください。 これは、特定のパスに対する有効なポリシーと、コンテンツに保存されているポリシーを比較することで検証できます。 有効なポリシーは、CUG の権限評価が有効になっている場合にのみ表示されます。

前述のように、CUG アクセス制御ポリシーは現在、コンテンツに保存されるようになりましたが、これらのポリシーの結果である有効な権限の評価は、「**CUG Evaluation Enabled**」が、システムコンソールの Apache Jackrabbit Oak **CUG Configuration のシステムコンソールでオンになっている場合のみ適用されます。** デフォルトでは、「パブリッシュ」実行モードでのみ有効になります。

### 認証に関する相違点 {#differences-with-regards-to-authentication}

認証に関する違いについては、以下で説明します。

#### 認証要件用の専用 Mixin タイプ {#dedicated-mixin-type-for-authentication-requirement}

前の実装では、CUG の承認と認証に関連するパーツは、単一の JCR プロパティ（`cq:cugEnabled`）によって呼び出されました。認証に関する限り、これによって、Apache Sling Authenticator 実装で保存される認証要件の更新リストが得られました。新しい実装では、これと同じことが、専用の mixin タイプ（`granite:AuthenticationRequired`）でターゲットノードをマークすることで達成されます。

#### ログインパスを除外するためのプロパティ {#property-for-excluding-login-path}

Mixin タイプは、基本的に `cq:cugLoginPage` プロパティに対応する、`granite:loginPath` という名前の単一のオプションプロパティを定義します。以前の実装とは異なり、ログインパスプロパティは、宣言するノードタイプが前述の mixin の場合にのみ考慮されます。 mixin タイプを設定せずにその名前のプロパティを追加しても、効果がなく、新しい要件もログインパスの除外もオーセンティケーターに報告されません。

#### 認証要件の権限 {#privilege-for-authentication-requirement}

mixin タイプを追加または削除するには、`jcr:nodeTypeManagement` 権限が付与されている必要があります。前の実装では、残余プロパティの編集には `jcr:modifyProperties` 権限が使用されました。

`granite:loginPath` に関する限り、残余プロパティを追加、変更または削除するには同じ権限が必要です。

#### Mixin タイプで定義されたターゲットノード {#target-node-defined-by-mixin-type}

認証要件は、強制的なログインの対象となるサブツリーを定義する JCR ノードで作成される必要があります。 CUG がツリー全体に影響を与え、新しい実装の UI が結果としてページノードに auth-requirement mixin タイプを追加する場合、これはAEMページの可能性が高くなります。

CUG ポリシーを特定のページ下の jcr:content ノードにのみ配置すると、コンテンツへのアクセスのみが制限され、そのページノード自体や子ページには影響しません。

場合によってはこうしたケースも有効で、任意のノードに mixin を配置できるリポジトリエディターによって達成できます。ただし、この動作は、cq:cugEnabled プロパティや cq:cugLoginPage プロパティを jcr:content ノードに配置することが、内部でページノードに再マッピングされた前の実装とは対照的です。このマッピングは実行されなくなりました。

#### 設定済みのサポート対象パス {#configured-supported-paths}

`granite:AuthenticationRequired` mixin タイプと granite:loginPath プロパティは、**Adobe Granite Authentication Requirement and Login Path Handler** で提供される「**サポートされているパス**」設定オプションによって定義される適用範囲内でのみ考慮されます。これらのパスが指定されていないと、認証要件機能は全体で無効になります。その場合、Mixin タイプやプロパティを追加しても、特定の JCR ノードに設定しても、どちらも有効になりません。

### JCR コンテンツ、OSGi サービスおよび設定のマッピング {#mapping-of-jcr-content-osgi-services-and-configurations}

次のドキュメントでは、新旧の実装間での OSGi サービス、設定およびリポジトリコンテンツの包括的な対応関係について説明します。

AEM 6.3 以降の CUG の対応関係

[ファイルを入手](assets/cug-mapping.pdf)

## CUG をアップグレード {#upgrade-cug}

### 非推奨の CUG を使用した既存のインストール {#existing-installations-using-the-deprecated-cug}

古い CUG サポート実装は廃止され、今後のバージョンでは削除される予定です。 AEM 6.3 より前のバージョンからアップグレードする場合は、新しい実装に移行することをお勧めします。

アップグレードされたAEMのインストールでは、1 つの CUG 実装のみが有効になっていることを確認することが重要です。 新しい CUG サポートと廃止された古い CUG サポートの組み合わせはテストされておらず、望ましくない動作を引き起こす可能性が高くなります。

* 認証要件に関する Sling Authenticator の競合
* 古い CUG に関連付けられた ACL 設定が新しい CUG ポリシーと衝突した場合、読み取りアクセスが拒否されました。

### 既存の CUG コンテンツの移行 {#migrating-existing-cug-content}

Adobeは、新しい CUG 実装に移行するためのツールを提供します。 この機能を使用するには、次の手順に従います。

1. `https://<serveraddress>:<serverport>/system/console/cug-migration` に移動して、ツールにアクセスします。
1. CUG を調べるルートパスを入力し、「**Perform dry run**」ボタンを押します。これにより、選択した場所で変換可能な CUG がスキャンされます。
1. 結果を確認した後、「**Perform migration**」ボタンを押して、新しい実装に移行します。

>[!NOTE]
>
>問題が発生した場合は、移行ツールの出力を取得するために`com.day.cq.auth.impl.cug`にある特定のロガーを&#x200B;**デバッグ**&#x200B;レベルに設定することが可能です。詳細については、[ロギング](/help/sites-deploying/configure-logging.md)を参照してください。
