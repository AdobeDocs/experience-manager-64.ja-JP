---
title: Cookie の使用法の設定
seo-title: Configuring Cookie Usage
description: AEM では、Web ページでの Cookie の使用方法を設定および制御できるサービスを提供しています
seo-description: AEM provides a service that enables you to configure and control how cookies are used with your web pages
uuid: 10d95176-0a56-41f1-9d36-01dbdac757d4
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.4/SITES
topic-tags: platform
content-type: reference
discoiquuid: 5773ec1a-f15b-462d-8f9f-54ee1d7ead44
exl-id: 7f604d89-c6ad-405d-98cd-80f057466e61
source-git-commit: bd94d3949f0117aa3e1c9f0e84f7293a5d6b03b4
workflow-type: tm+mt
source-wordcount: '554'
ht-degree: 100%

---

# Cookie の使用法の設定{#configuring-cookie-usage}

AEM では、Web ページでの Cookie の使用方法を設定および制御できるサービスを提供しています:

* 設定可能なサーバー側のサービスによって、使用可能な Cookie のリストを管理します。
* JavaScript API によって、Cookie が使用可能であることを検証する JavaScript コードを作成できます。

この機能を使用して、ページが Cookie の使用方法に関するユーザーの同意に従って動作するようにします。

## 許可された Cookie の設定 {#configuring-allowed-cookies}

Adobe Granite Opt-Out Service の設定によって、Web ページでの Cookie の使用方法を指定します。次の表に、設定可能なプロパティについて説明します。

 サービスを設定するには、[Web コンソール](/help/sites-deploying/configuring-osgi.md#osgi-configuration-with-the-web-console)を使用するか、[リポジトリに OSGi 設定を追加](/help/sites-deploying/configuring-osgi.md#adding-a-new-configuration-to-the-repository)します。次の表では、どちらの方法でも必要になるプロパティについて説明しています。OSGi 設定の場合、サービス PID は `com.adobe.granite.optout` です。

| プロパティ名（Web コンソール） | OSGi のプロパティ名 | 説明 |
|---|---|---|
| Opt-Out Cookies | optout.cookies | ユーザーのデバイス上に存在する場合、そのユーザーが Cookie の使用に同意していないことを示す Cookie の名前。 |
| Opt-Out HTTP Headers | optout.headers | 存在する場合、ユーザーが Cookie の使用に同意していないことを示す HTTP ヘッダーの名前。 |
| White-List Cookies | optout.whitelist.cookies | Web サイトの正常動作にとって不可欠であり、ユーザーの同意なしに使用可能な Cookie のリスト。 |

## Cookie の使用に関する検証 {#validating-cookie-usage}

クライアント側の JavaScript を使用して Adobe Granite Opt-Out Service を呼び出し、Cookie を使用できることを確認します。次のタスクを実行するには、Granite.OptOutUtil という JavaScript オブジェクトを使用します。

* 追跡の目的で Cookie を使用することをユーザーが同意していないことを示す Cookie 名のリストを取得します。
* 使用可能な Cookie のリストを取得します。
* 追跡の目的で Cookie を使用することをユーザーが同意していないことを示す Cookie が、Web ブラウザーに含まれているかを判断します。
* 特定の Cookie が使用可能であるかを判断します。

granite.utils [クライアントライブラリフォルダー](/help/sites-developing/clientlibs.md#referencing-client-side-libraries)に、Granite.OptOutUtil オブジェクトが存在します。ページの JSP ヘッド部に次のコードを追加して、JavaScript ライブラリにリンクをインクルードするようにします。

`<ui:includeClientLib categories="granite.utils" />`

例えば、次の JavaScript 関数は、COOKIE_NAME Cookie の使用が許可されているかを判断し、その後その Cookie に書き込みます。

```
function writeCookie(value){
   if (!Granite.OptOutUtil.maySetCookie("COOKIE_NAME")) 
      return;
   if (value) {
      value = encodeURIComponent(value);
      document.cookie = "COOKIE_NAME=" + value; 
   }
}
```

## Granite.OptOutUtil JavaScript オブジェクト {#the-granite-optoututil-javascript-object}

Granite.OptOutUtil を使用して、Cookie の使用が許可されているかを判断できます。

### getCookieNames() 関数 {#getcookienames-function}

存在する場合に、ユーザーが Cookie の使用に同意していないことを示す Cookie の名前を返します。

**パラメーター**

なし。

**戻り値**

Cookie 名の配列。

#### getWhitelistCookieNames() 関数 {#getwhitelistcookienames-function}

ユーザーの同意に関係なく使用可能な Cookie の名前を返します。

**パラメーター**

なし。

**戻り値**

Cookie 名の配列。

#### isOptedOut() 関数 {#isoptedout-function}

Cookie の使用の同意が得られていないことを示す Cookie がユーザーのブラウザーに保存されていないかを判断します。

**パラメーター**

なし。

**戻り値**

同意がないことを示す Cookie が見つかった場合はブール値 `true`、同意がないことを示す Cookie が存在しない場合は値 `false`。

### maySetCookie(cookieName) 関数 {#maysetcookie-cookiename-function}

ユーザーのブラウザー上で特定の Cookie を使用できるかを判断します。この関数は、`isOptedOut` 関数と、`getWhitelistCookieNames` が返すリスト内に特定の特定の Cookie が含まれているかの判断を連結して使用する処理と同等です。

**パラメーター**

* cookieName：文字列。 Cookie の名前。

**戻り値**

`cookieName` を使用できる場合はブール値 `true`、`cookieName` が使用できない場合は値 `false`。
