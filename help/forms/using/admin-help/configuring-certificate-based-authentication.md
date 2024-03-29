---
title: 証明書ベースの認証の設定
seo-title: Configuring certificate-based authentication
description: 認証局 (CA) 証明書を Trust Store に読み込み、証明書ベースの認証用の証明書のマッピングを作成します。
seo-description: Import a Certificate Authority (CA) certificate into the Trust Store and create a certificate mapping for certificate-based authentication.
uuid: 9802a969-6d29-4b80-a4ed-06eb6e66e046
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_user_management
products: SG_EXPERIENCEMANAGER/6.4/FORMS
discoiquuid: d958ae65-3008-4d68-9e11-4346e149827f
exl-id: 88932b5b-2acc-4f21-8ce3-b819a990ad30
source-git-commit: c5b816d74c6f02f85476d16868844f39b4c47996
workflow-type: tm+mt
source-wordcount: '762'
ht-degree: 7%

---

# 証明書ベースの認証の設定 {#configuring-certificate-based-authentication}

>[!CAUTION]
>
>AEM 6.4 の拡張サポートは終了し、このドキュメントは更新されなくなりました。 詳細は、 [技術サポート期間](https://helpx.adobe.com/jp/support/programs/eol-matrix.html). サポートされているバージョンを見つける [ここ](https://experienceleague.adobe.com/docs/?lang=ja).

User Management は、通常、ユーザー名とパスワードを使用して認証を実行します。 User Management は、証明書ベースの認証もサポートしています。証明書ベースの認証は、Acrobatを通じてユーザーを認証する場合や、プログラムを通じてユーザーを認証する場合に使用できます。 プログラムによるユーザーの認証について詳しくは、 [AEM forms によるプログラミング](https://www.adobe.com/go/learn_aemforms_programming_63_jp).

証明書ベースの認証を使用するには、信頼する認証局 (CA) 証明書を Trust Store に読み込み、証明書のマッピングを作成します。

## CA 証明書を読み込む {#import-the-ca-certificate}

証明書を読み込む際に、「証明書の認証で信頼」および「 ID で信頼」オプションと、必要なその他のオプションを選択します。 証明書のインポートについて詳しくは、 [証明書の管理](/help/forms/using/admin-help/certificates.md#managing-certificates).

## 証明書のマッピングの設定 {#configuring-certificate-mapping}

ユーザーに対して証明書ベースの認証を有効にするには、証明書のマッピングを作成します。 A *証明書のマッピング* 証明書の属性とドメイン内のユーザーの属性とのマップを定義します。 複数の証明書を同じドメインにマッピングできます。

証明書をテストする際に、User Management は証明書チェックをアップロードし、次の要件を満たしていることを確認します。

* 証明書が有効です。
* 指定した発行者が証明書を検証できます。
* 証明書には、マッピングに必要な属性が含まれています。
* 指定したマッピングにより、証明書がAEM forms データベース内の 1 人のユーザーにのみマッピングされます。 現在のユーザーと古い（削除された）ユーザーの両方が、マッピング条件に一致するかどうかを確認します。 したがって、古いユーザーを含む複数のユーザーが属性値を考慮している場合、証明書テストは失敗します。

>[!NOTE]
>
>既存の証明書のマッピングは編集できません。

**証明書のマッピングの追加**

1. 管理コンソールで、設定/User Management/設定/証明書のマッピングをクリックします。
1. 「新しい証明書のマッピング」をクリックし、「発行者用」リストで、Trust Store の管理で設定した証明書エイリアスを選択します。
1. 証明書の属性の 1 つをユーザーの属性にマッピングします。 例えば、証明書の共通名をユーザーのログイン ID にマッピングできます。

   証明書の属性の内容が User Management データベースのユーザーの属性の内容と異なる場合、Java 正規表現 (regex) を使用して 2 つの属性を照合できます。 例えば、証明書の共通名が *Alex Pink （認証）* および *Alex Pink （署名）* User Management データベースの共通名は、 *Alex Pink*&#x200B;の場合は、正規表現を使用して、証明書属性の必要な部分 ( この例では *Alex Pink*.) 指定する正規表現は、Java 正規表現の仕様に準拠している必要があります。

   「カスタムの順序」ボックスでグループの順序を指定すると、式を変換できます。 カスタムオーダーは、`java.util.regex.Matcher.replaceAll()` メソッドで使用します。表示される動作はそのメソッドの動作に対応し、それに応じて入力文字列（カスタム順序）を指定する必要があります。

   正規表現をテストするには、「テストパラメーター」ボックスに値を入力し、「テスト」をクリックします。

   正規表現では、次の文字を使用できます。

   * 。（任意の文字）
   * &amp;ast;（0 回または何回かの出現）
   * ()（グループを角括弧で囲んで指定）
   * \ （正規表現文字を正規表現文字にエスケープするために使用）
   * $n （n 番目のグループを参照するために使用）

   正規表現の例：

   * 「Alex Pink (Authentication)」から「Alex Pink」を抽出するには

      **正規表現：** (.&amp;ast;) \(認証\)

   * 「Alex (Authentication) Pink」から「Alex Pink」を抽出するには

      **正規表現：** (.&amp;ast;)\(認証\) (.&amp;ast;)

   * 「Alex (Authentication) Pink」から「Pink Alex」を抽出するには

      **正規表現：** (.&amp;ast;)\(認証\) (.&amp;ast;)

      カスタム注文：$2 $1 （2 番目のグループを返し、最初のグループに連結、空白文字でキャプチャ）

   * 「smtp:apink@sampleorg.com」から「apink@sampleorg.com」を抽出するには

      **Regex:** smtp:(.&amp;ast;)
   正規表現の使用について詳しくは、 [正規表現に関する Java チュートリアル](https://java.sun.com/docs/books/tutorial/essential/regex/).

1. 「ドメイン用」リストで、ユーザーのドメインを選択します。
1. この設定をテストするには、「参照」をクリックしてサンプルのユーザー証明書をアップロードし、「証明書をテスト」をクリックします。設定が正しい場合は、「OK」をクリックします。

**既存の証明書のマッピングの編集**

1. 管理コンソールで、設定/User Management/設定をクリックします。
1. 「証明書のマッピング」をクリックします。
1. 編集する証明書のマッピングを選択し、設定を編集します。 正規表現とカスタムの順序を更新できます。
1. 変更をテストするには、[ 参照 ] をクリックしてサンプルの証明書をアップロードし、[ 証明書のテスト ] をクリックして、[OK] をクリックします。

**証明書のマッピングの削除**

1. 管理コンソールで、設定/User Management/設定/証明書のマッピングをクリックします。
1. 削除する証明書のマッピングのチェックボックスをオンにして、[ 削除 ] をクリックし、[OK] をクリックします。
