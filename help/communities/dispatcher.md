---
title: Communities 用の Dispatcher の設定
seo-title: Configuring Dispatcher for Communities
description: AEM Communities用の Dispatcher の設定
seo-description: Configure the dispatcher for AEM Communities
uuid: c17daca9-3244-4b10-9d4e-2e95df633dd9
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.4/COMMUNITIES
content-type: reference
topic-tags: deploying
discoiquuid: 23745dd3-1424-4d22-8456-d2dbd42467f4
exl-id: dc4e27dd-fb2e-485d-8c7f-ab830bde1d3d
source-git-commit: c5b816d74c6f02f85476d16868844f39b4c47996
workflow-type: tm+mt
source-wordcount: '663'
ht-degree: 13%

---

# Communities 用の Dispatcher の設定 {#configuring-dispatcher-for-communities}

>[!CAUTION]
>
>AEM 6.4 の拡張サポートは終了し、このドキュメントは更新されなくなりました。 詳細は、 [技術サポート期間](https://helpx.adobe.com/jp/support/programs/eol-matrix.html). サポートされているバージョンを見つける [ここ](https://experienceleague.adobe.com/docs/?lang=ja).

## AEM Communities {#aem-communities}

AEM Communitiesの場合、の適切な機能を確保するために、Dispatcher を設定する必要があります。 [コミュニティサイト](overview.md#community-sites). コミュニティイネーブルメントやソーシャルログインなどの機能を含める場合は、追加の設定が必要です。

お客様の特定の導入およびサイト設計に必要な事項を学ぶには

* [カスタマーケア](https://helpx.adobe.com/jp/marketing-cloud/contact-support.html)に問い合わせる

メイン [Dispatcher のドキュメント](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/dispatcher.html?lang=ja).

## Dispatcher のキャッシュ {#dispatcher-caching}

### 概要 {#overview}

AEM Communitiesの Dispatcher キャッシュは、Dispatcher がコミュニティサイトのページの完全にキャッシュされたバージョンを提供する機能です。

現在、コミュニティサイトを閲覧したユーザー、検索の結果コミュニティページにアクセスしたユーザー、ページをインデックス化した検索エンジンなど、匿名のサイト訪問者に対してのみサポートされています。 メリットは、匿名のユーザーと検索エンジンのパフォーマンスが向上することです。

サインインしたメンバーの場合、Dispatcher はキャッシュをバイパスし、要求をパブリッシャーに直接リレーして、すべてのページが動的に生成および配信されるようにします。

Dispatcher のキャッシュをサポートするように設定した場合、Dispatcher がキャッシュしたページを最新の状態に保つために、TTL ベースの「max age」の有効期限がヘッダーに追加されます。

### 要件 {#requirements}

* Dispatcher バージョン 4.1.2 以降 ( [Dispatcher のインストール](https://helpx.adobe.com/jp/experience-manager/dispatcher/using/dispatcher-install.html) （最新バージョンの場合）
* [ACS AEM Commons パッケージ](https://adobe-consulting-services.github.io/acs-aem-commons/)

   * バージョン 3.3.2 以降
   * `ACS AEM Commons - Dispatcher Cache Control Header - Max Age` OSGi 設定

### 設定 {#configuration}

OSGi 設定 **ACS AEM Commons - Dispatcher キャッシュ制御ヘッダー — 最大経過時間** 指定されたパスの下に表示される、キャッシュされたページの有効期限を設定します。

* 次の [Web コンソール](../../help/sites-deploying/configuring-osgi.md)

   * 例： [http://localhost:4503/system/console/configMgr](http://localhost:4503/system/console/configMgr)

* 場所 `ACS AEM Commons - Dispatcher Cache Control Header - Max Age`
* 「+」アイコンを選択して新しい接続設定を作成

![chlimage_1-339](assets/chlimage_1-339.png)

* **フィルターパターン**

   *（必須）* コミュニティページへの 1 つ以上のパス。 例：`/content/sites/engage/(.*)`

* **Cache-Control の最大経過時間**

   *（必須）* キャッシュ制御ヘッダーに追加する最大経過時間（秒）。 0 より大きい値を指定する必要があります。

## Dispatcher クライアントヘッダー {#dispatcher-client-headers}

/clientheaders セクション ( `dispatcher.any`特定のヘッダーセットをリストする場合は、 `"CSRF-Token"` ～のために [イネーブルメント機能](enablement.md) 正しく動作させる。

## Dispatcher フィルター {#dispatcher-filters}

の/filter セクション `dispatcher.any` ファイルは、 [コンテンツへのアクセスの設定 — /filter](https://helpx.adobe.com/jp/experience-manager/dispatcher/using/dispatcher-configuration.html#filter).

この節では、コミュニティ機能を適切に機能させるために必要なエントリについて説明します。

フィルタープロパティ名は、フィルターパターンを適用する順序を示す 4 桁の数字を使用する規則に従います。 複数のフィルターパターンを 1 つの要求に適用した場合は、最後に適用されたフィルターパターンが有効になります。したがって、最初のフィルターパターンは、多くの場合、すべてを拒否するために使用され、次のパターンは、制御された方法でアクセスを復元するために役立ちます。

以下のサンプルでは、任意の特定の dispatcher.any ファイルに合わせて変更する必要がある可能性のあるプロパティ名を使用します。

関連トピック

* [Dispatcher のセキュリティチェックリスト](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/getting-started/security-checklist.html?lang=ja#getting-started)

>[!NOTE]
>
>**プロパティ名の例**
>表示されるすべてのプロパティ名（例： ） **/0050** および **/0170**&#x200B;を使用する場合は、既存の dispatcher.any 設定ファイル内に収まるように調整する必要があります。

次のエントリは、特にすべての deny エントリの後に/filter セクションの末尾に追加する必要があります。

```shell
# design and template assets

>[!CAUTION]
>
>AEM 6.4 has reached the end of extended support and this documentation is no longer updated. For further details, see our [technical support periods](https://helpx.adobe.com/support/programs/eol-matrix.html). Find the supported versions [here](https://experienceleague.adobe.com/docs/).
/0050 { /type "allow" /glob "GET /etc/designs/*" }

# collected JS/CSS from the components and design

>[!CAUTION]
>
>AEM 6.4 has reached the end of extended support and this documentation is no longer updated. For further details, see our [technical support periods](https://helpx.adobe.com/support/programs/eol-matrix.html). Find the supported versions [here](https://experienceleague.adobe.com/docs/).
/0051 { /type "allow" /glob "GET /etc/clientlibs/*" }

# foundation search component - write stats

>[!CAUTION]
>
>AEM 6.4 has reached the end of extended support and this documentation is no longer updated. For further details, see our [technical support periods](https://helpx.adobe.com/support/programs/eol-matrix.html). Find the supported versions [here](https://experienceleague.adobe.com/docs/).
/0052 { /type "allow" /glob "GET /bin/statistics/tracker/*" }

# allow users to edit profile page

>[!CAUTION]
>
>AEM 6.4 has reached the end of extended support and this documentation is no longer updated. For further details, see our [technical support periods](https://helpx.adobe.com/support/programs/eol-matrix.html). Find the supported versions [here](https://experienceleague.adobe.com/docs/).
/0054 { /type "allow" /glob "* /home/users/*/*/profile.form.html*" }

# all profile data

>[!CAUTION]
>
>AEM 6.4 has reached the end of extended support and this documentation is no longer updated. For further details, see our [technical support periods](https://helpx.adobe.com/support/programs/eol-matrix.html). Find the supported versions [here](https://experienceleague.adobe.com/docs/).
/0057 { /type "allow" /glob "GET /home/users/*/profile/*" }

# required for social "Sign In" link.

>[!CAUTION]
>
>AEM 6.4 has reached the end of extended support and this documentation is no longer updated. For further details, see our [technical support periods](https://helpx.adobe.com/support/programs/eol-matrix.html). Find the supported versions [here](https://experienceleague.adobe.com/docs/).
/0059 { /type "allow" /glob "GET /etc/clientcontext/*" }

# required for "Sign Out" operation

>[!CAUTION]
>
>AEM 6.4 has reached the end of extended support and this documentation is no longer updated. For further details, see our [technical support periods](https://helpx.adobe.com/support/programs/eol-matrix.html). Find the supported versions [here](https://experienceleague.adobe.com/docs/).
/0063 { /type "allow" /glob "* /system/sling/logout*" }

# enable Facebook and Twitter signin

>[!CAUTION]
>
>AEM 6.4 has reached the end of extended support and this documentation is no longer updated. For further details, see our [technical support periods](https://helpx.adobe.com/support/programs/eol-matrix.html). Find the supported versions [here](https://experienceleague.adobe.com/docs/).
/0064 { /type "allow" /glob "GET /etc/cloudservices/*" }

# enable personalization

>[!CAUTION]
>
>AEM 6.4 has reached the end of extended support and this documentation is no longer updated. For further details, see our [technical support periods](https://helpx.adobe.com/support/programs/eol-matrix.html). Find the supported versions [here](https://experienceleague.adobe.com/docs/).
/0062 { /type "allow" /url "/libs/cq/personalization/*" }

# for Enablement features

>[!CAUTION]
>
>AEM 6.4 has reached the end of extended support and this documentation is no longer updated. For further details, see our [technical support periods](https://helpx.adobe.com/support/programs/eol-matrix.html). Find the supported versions [here](https://experienceleague.adobe.com/docs/).
/0170 { /type "allow" /url "/libs/granite/csrf/token.json*" }
/0171 { /type "allow" /glob "POST /content/sites/*/resources/en/*" }
/0172 { /type "allow" /glob "GET /content/communities/enablement/reports/*" }
/0173 { /type "allow" /glob "GET /content/sites/*" }
/0174 { /type "allow" /glob "GET /content/communities/scorm/*" }
/0175 { /type "allow" /url "GET /content/sites/*" }
/0176 { /type "allow" /url "GET /libs/granite/security/userinfo.json"}
/0177 { /type "allow" /url "GET /libs/granite/security/currentuser.json" }

# Enable CSRF token otherwise nothings works.

>[!CAUTION]
>
>AEM 6.4 has reached the end of extended support and this documentation is no longer updated. For further details, see our [technical support periods](https://helpx.adobe.com/support/programs/eol-matrix.html). Find the supported versions [here](https://experienceleague.adobe.com/docs/).
/5001 { /type "allow" /glob "GET /libs/granite/csrf/token.json *"}        
# Allow SCF User Model to bootstrap as it depends on the granite user

>[!CAUTION]
>
>AEM 6.4 has reached the end of extended support and this documentation is no longer updated. For further details, see our [technical support periods](https://helpx.adobe.com/support/programs/eol-matrix.html). Find the supported versions [here](https://experienceleague.adobe.com/docs/).
/5002 { /type "allow" /glob "GET /libs/granite/security/currentuser.json*" }
   
# Allow Communities Site Logout button work

>[!CAUTION]
>
>AEM 6.4 has reached the end of extended support and this documentation is no longer updated. For further details, see our [technical support periods](https://helpx.adobe.com/support/programs/eol-matrix.html). Find the supported versions [here](https://experienceleague.adobe.com/docs/).
/5003 { /type "allow" /glob "GET /system/sling/logout.html*" }
   
# Allow i18n to load correctly

>[!CAUTION]
>
>AEM 6.4 has reached the end of extended support and this documentation is no longer updated. For further details, see our [technical support periods](https://helpx.adobe.com/support/programs/eol-matrix.html). Find the supported versions [here](https://experienceleague.adobe.com/docs/).
/5004 { /type "allow" /glob "GET /libs/cq/i18n/dict.en.json *" }

# Allow social json get pattern.

>[!CAUTION]
>
>AEM 6.4 has reached the end of extended support and this documentation is no longer updated. For further details, see our [technical support periods](https://helpx.adobe.com/support/programs/eol-matrix.html). Find the supported versions [here](https://experienceleague.adobe.com/docs/).
/6002 { /type "allow" /glob "GET *.social.*.json*" }
   
# Allow loading of templates

>[!CAUTION]
>
>AEM 6.4 has reached the end of extended support and this documentation is no longer updated. For further details, see our [technical support periods](https://helpx.adobe.com/support/programs/eol-matrix.html). Find the supported versions [here](https://experienceleague.adobe.com/docs/).
/6003 { /type "allow" /glob "GET /services/social/templates*" }
   
# Allow SCF User model to check moderator rules

>[!CAUTION]
>
>AEM 6.4 has reached the end of extended support and this documentation is no longer updated. For further details, see our [technical support periods](https://helpx.adobe.com/support/programs/eol-matrix.html). Find the supported versions [here](https://experienceleague.adobe.com/docs/).
/6005 { /type "allow" /glob "GET /services/social/getLoggedInUser?moderatorCheck=*" }
   
# Allow CKEditor to load which uses a query pattern not sufficed by regular glob above.

>[!CAUTION]
>
>AEM 6.4 has reached the end of extended support and this documentation is no longer updated. For further details, see our [technical support periods](https://helpx.adobe.com/support/programs/eol-matrix.html). Find the supported versions [here](https://experienceleague.adobe.com/docs/).
/6006 { /type "allow" /glob "GET /etc/clientlibs/social/thirdparty/ckeditor/*.js?t=*" }
/6007 { /type "allow" /glob "GET /etc/clientlibs/social/thirdparty/ckeditor/*.css?t=*" }
   
# Allow Fonts from Communities to load

>[!CAUTION]
>
>AEM 6.4 has reached the end of extended support and this documentation is no longer updated. For further details, see our [technical support periods](https://helpx.adobe.com/support/programs/eol-matrix.html). Find the supported versions [here](https://experienceleague.adobe.com/docs/).
/6050 { /type "allow" /glob "GET *.woff *" }
/6051 { /type "allow" /glob "GET *.ttf *" }

# Enable CQ Security checkpoint for component guide.

>[!CAUTION]
>
>AEM 6.4 has reached the end of extended support and this documentation is no longer updated. For further details, see our [technical support periods](https://helpx.adobe.com/support/programs/eol-matrix.html). Find the supported versions [here](https://experienceleague.adobe.com/docs/).
/7001 { /type "allow" /glob "GET /libs/cq/security/userinfo.json?cq_ck=*"
```

## Dispatcher ルール {#dispatcher-rules}

のルールセクション `dispatcher.any` は、要求された URL に基づいてキャッシュする応答を定義します。 Communities の場合、ルールセクションを使用して、キャッシュしないものを定義します。

```shell
# Never cache the client-side .social.json calls

>[!CAUTION]
>
>AEM 6.4 has reached the end of extended support and this documentation is no longer updated. For further details, see our [technical support periods](https://helpx.adobe.com/support/programs/eol-matrix.html). Find the supported versions [here](https://experienceleague.adobe.com/docs/).
/0001 { /type "deny" /glob "*.social.json*" }

# Never cache the user-specific .json requests

>[!CAUTION]
>
>AEM 6.4 has reached the end of extended support and this documentation is no longer updated. For further details, see our [technical support periods](https://helpx.adobe.com/support/programs/eol-matrix.html). Find the supported versions [here](https://experienceleague.adobe.com/docs/).
/0002 { /type "deny" /glob "/libs/granite/csrf/token.json*" }
/0003 { /type "deny" /glob "/libs/granite/security/currentuser.json*" }
/0004 { /type "deny" /glob "/libs/granite/security/userinfo.json*" }

# Never cache the private community groups pages in case - add your own deny rules in there

>[!CAUTION]
>
>AEM 6.4 has reached the end of extended support and this documentation is no longer updated. For further details, see our [technical support periods](https://helpx.adobe.com/support/programs/eol-matrix.html). Find the supported versions [here](https://experienceleague.adobe.com/docs/).
/0005 { /type "deny" /glob "/content/*/groups/*" }

# Never cache the assignments page in case the Enablement feature is in use - add your own deny rules in there

>[!CAUTION]
>
>AEM 6.4 has reached the end of extended support and this documentation is no longer updated. For further details, see our [technical support periods](https://helpx.adobe.com/support/programs/eol-matrix.html). Find the supported versions [here](https://experienceleague.adobe.com/docs/).
/0006 { /type "deny" /glob "/content/*/assignments/*" }

# Never cache user generated content

>[!CAUTION]
>
>AEM 6.4 has reached the end of extended support and this documentation is no longer updated. For further details, see our [technical support periods](https://helpx.adobe.com/support/programs/eol-matrix.html). Find the supported versions [here](https://experienceleague.adobe.com/docs/).
/0208 { /type "deny" /glob "/content/usergenerated/*" }
```

## トラブルシューティング {#troubleshooting}

主な問題の原因は、以前のルールへの影響に注意を払わずにフィルタールールを挿入することです。特に、アクセスを拒否するルールを追加する場合に問題が発生します。

最初のフィルターパターンは、多くの場合、次のフィルターが制御された方法でアクセスを復元するように、すべてを拒否するために使用されます。 1 つのリクエストに複数のフィルターが適用される場合、最後に適用されるフィルターが有効になります。

## サンプルの dispatcher.any {#sample-dispatcher-any}

以下はサンプルです `dispatcher.any` Communities /filters と/rules を含むファイル。

```shell
# Each farm configures a set of load balanced renders (i.e. remote servers)

>[!CAUTION]
>
>AEM 6.4 has reached the end of extended support and this documentation is no longer updated. For further details, see our [technical support periods](https://helpx.adobe.com/support/programs/eol-matrix.html). Find the supported versions [here](https://experienceleague.adobe.com/docs/).
/farms
  {
  # First farm entry
  /website 
    {  
    # Request headers that should be forwarded to the remote server.
    /clientheaders
      {
      # Forward all request headers that are end-to-end. If you want
      # to forward a specific set of headers, you'll have to list
      # them here.
      "*"
      }
      
    # Hostname globbing for farm selection (virtual domain addressing)
    /virtualhosts
      {
      # Entries will be compared against the "Host" request header
      # and an optional request URL prefix.
      #
      # Examples:
      #
      #   www.company.com
      #   intranet.*
      #   myhost:8888/mysite
      "*"
      }
      
    # The load will be balanced among these render instances
    /renders
      {
      /rend01
        {
        # Hostname or IP of the render
        /hostname "127.0.0.1"
        # Port of the render
        /port "4503"
        # Connect timeout in milliseconds, 0 to wait indefinitely
        # /timeout "0"
        }
      }
      
    # The filter section defines the requests that should be handled by the dispatcher.
    #
    # Entries can be either specified using globs, or elements of the request line:
    #
    # (1) globs will be compared against the entire request line, e.g.:
    #
    #     /0001 { /type "deny" /glob "* /index.html *" }
    #
    #   matches request "GET /index.html HTTP/1.1" but not "GET /index.html?a=b HTTP/1.1".
    #
    # (2) method/url/query/protocol will be compared againts the respective elements of
    #   the request line, e.g.:
    #
    #     /0001 { /type "deny" /method "GET" /url "/index.html" }
    #
    #   matches both "GET /index.html" and "GET /index.html?a=b HTTP/1.1".
    #
    # Note: specifying elements of the request line is the preferred method.
    /filter
      {
      # Deny everything first and then allow specific entries
      /0001 { /type "deny" /glob "*" }
      
      # Open consoles
#     /0011 { /type "allow" /url "/admin/*"  }  # allow servlet engine admin

>[!CAUTION]
>
>AEM 6.4 has reached the end of extended support and this documentation is no longer updated. For further details, see our [technical support periods](https://helpx.adobe.com/support/programs/eol-matrix.html). Find the supported versions [here](https://experienceleague.adobe.com/docs/).
#     /0012 { /type "allow" /url "/crx/*"    }  # allow content repository

>[!CAUTION]
>
>AEM 6.4 has reached the end of extended support and this documentation is no longer updated. For further details, see our [technical support periods](https://helpx.adobe.com/support/programs/eol-matrix.html). Find the supported versions [here](https://experienceleague.adobe.com/docs/).
#     /0013 { /type "allow" /url "/system/*" }  # allow OSGi console

>[!CAUTION]
>
>AEM 6.4 has reached the end of extended support and this documentation is no longer updated. For further details, see our [technical support periods](https://helpx.adobe.com/support/programs/eol-matrix.html). Find the supported versions [here](https://experienceleague.adobe.com/docs/).
        
      # Allow non-public content directories
#     /0021 { /type "allow" /url "/apps/*"   }  # allow apps access

>[!CAUTION]
>
>AEM 6.4 has reached the end of extended support and this documentation is no longer updated. For further details, see our [technical support periods](https://helpx.adobe.com/support/programs/eol-matrix.html). Find the supported versions [here](https://experienceleague.adobe.com/docs/).
#     /0022 { /type "allow" /url "/bin/*"    }

>[!CAUTION]
>
>AEM 6.4 has reached the end of extended support and this documentation is no longer updated. For further details, see our [technical support periods](https://helpx.adobe.com/support/programs/eol-matrix.html). Find the supported versions [here](https://experienceleague.adobe.com/docs/).
      /0023 { /type "allow" /url "/content*" }  # disable this rule to allow mapped content only
      
#     /0024 { /type "allow" /url "/libs/*"   }

>[!CAUTION]
>
>AEM 6.4 has reached the end of extended support and this documentation is no longer updated. For further details, see our [technical support periods](https://helpx.adobe.com/support/programs/eol-matrix.html). Find the supported versions [here](https://experienceleague.adobe.com/docs/).
#     /0025 { /type "deny"  /url "/libs/shindig/proxy*" } # if you enable /libs close access to proxy

>[!CAUTION]
>
>AEM 6.4 has reached the end of extended support and this documentation is no longer updated. For further details, see our [technical support periods](https://helpx.adobe.com/support/programs/eol-matrix.html). Find the supported versions [here](https://experienceleague.adobe.com/docs/).

#     /0026 { /type "allow" /url "/home/*"   }

>[!CAUTION]
>
>AEM 6.4 has reached the end of extended support and this documentation is no longer updated. For further details, see our [technical support periods](https://helpx.adobe.com/support/programs/eol-matrix.html). Find the supported versions [here](https://experienceleague.adobe.com/docs/).
#     /0027 { /type "allow" /url "/tmp/*"    }

>[!CAUTION]
>
>AEM 6.4 has reached the end of extended support and this documentation is no longer updated. For further details, see our [technical support periods](https://helpx.adobe.com/support/programs/eol-matrix.html). Find the supported versions [here](https://experienceleague.adobe.com/docs/).
#     /0028 { /type "allow" /url "/var/*"    }

>[!CAUTION]
>
>AEM 6.4 has reached the end of extended support and this documentation is no longer updated. For further details, see our [technical support periods](https://helpx.adobe.com/support/programs/eol-matrix.html). Find the supported versions [here](https://experienceleague.adobe.com/docs/).

      # Enable specific mime types in non-public content directories 
      /0041 { /type "allow" /url "*.css"   }  # enable css
      /0042 { /type "allow" /url "*.gif"   }  # enable gifs
      /0043 { /type "allow" /url "*.ico"   }  # enable icos
      /0044 { /type "allow" /url "*.js"    }  # enable javascript
      /0045 { /type "allow" /url "*.png"   }  # enable png
      /0046 { /type "allow" /url "*.swf"   }  # enable flash
      /0047 { /type "allow" /url "*.jpg"   }  # enable jpg
      /0048 { /type "allow" /url "*.jpeg"  }  # enable jpeg

      # Deny content grabbing
      /0081 { /type "deny"  /url "*.infinity.json" }
      /0082 { /type "deny"  /url "*.tidy.json"     }
      /0083 { /type "deny"  /url "*.sysview.xml"   }
      /0084 { /type "deny"  /url "*.docview.json"  }
      /0085 { /type "deny"  /url "*.docview.xml"  }
      
      /0086 { /type "deny"  /url "*.*[0-9].json" }
#     /0087 { /type "allow" /method "GET" /url "*.1.json" }  # allow one-level json requests

>[!CAUTION]
>
>AEM 6.4 has reached the end of extended support and this documentation is no longer updated. For further details, see our [technical support periods](https://helpx.adobe.com/support/programs/eol-matrix.html). Find the supported versions [here](https://experienceleague.adobe.com/docs/).

      # Deny query
   /0090 { /type "deny"  /url "*.query.json" }
   
      #######################################
      ## BEGIN: AEM COMMUNITITES ADDITIONS
   #######################################
   /0050 { /type "allow" /glob "GET /etc/designs/*" }  
   /0051 { /type "allow" /glob "GET /etc/clientlibs/*" }  
   /0052 { /type "allow" /glob "GET /bin/statistics/tracker/*" } 
   /0054 { /type "allow" /glob "* /home/users/*/*/profile.form.html*" } 
   /0057 { /type "allow" /glob "GET /home/users/*/profile/*" } 
   /0059 { /type "allow" /glob "GET /etc/clientcontext/*" }
   /0063 { /type "allow" /glob "* /system/sling/logout*" } 
   /0064 { /type "allow" /glob "GET /etc/cloudservices/*" } 
   /0062 { /type "allow" /url "/libs/cq/personalization/*"  }  # enable personalization

   # For Enablement features
   /0170 { /type "allow" /url "/libs/granite/csrf/token.json*" }
   /0171 { /type "allow" /glob "POST /content/sites/*/resources/en/*" }
   /0172 { /type "allow" /glob "GET /content/communities/enablement/reports/*" }
   /0173 { /type "allow" /glob "GET /content/sites/*" }
   /0174 { /type "allow" /glob "GET /content/communities/scorm/*" }
   /0175 { /type "allow" /url "GET /content/sites/*" }
   /0176 { /type "allow" /url "GET /libs/granite/security/userinfo.json"}
   /0177 { /type "allow" /url "GET /libs/granite/security/currentuser.json" }
 
      # Enable CSRF token otherwise nothings works.
   /5001 { /type "allow" /glob "GET /libs/granite/csrf/token.json *"}        
    
   # Allow SCF User Model to bootstrap as it depends on the granite user
   /5002 { /type "allow" /glob "GET /libs/granite/security/currentuser.json*" }
   
      # Allow Communities Site Logout button work
      /5003 { /type "allow" /glob "GET /system/sling/logout.html*" }
   
   # Allow i18n to load correctly
   /5004 { /type "allow" /glob "GET /libs/cq/i18n/dict.en.json *" }

   # Allow social json get pattern.
   /6002 { /type "allow" /glob "GET *.social.*.json*" }
   
   # Allow loading of templates
   /6003 { /type "allow" /glob "GET /services/social/templates*" }
   
   # Allow SCF User model to check moderator rules
   /6005 { /type "allow" /glob "GET /services/social/getLoggedInUser?moderatorCheck=*" }
   
   # Allow CKEditor to load which uses a query pattern not sufficed by regular glob above.
   /6006 { /type "allow" /glob "GET /etc/clientlibs/social/thirdparty/ckeditor/*.js?t=*" }
   /6007 { /type "allow" /glob "GET /etc/clientlibs/social/thirdparty/ckeditor/*.css?t=*" }
   
   # Allow Fonts from Communities to load
   /6050 { /type "allow" /glob "GET *.woff *" }
   /6051 { /type "allow" /glob "GET *.ttf *" }

      # Enable CQ Security checkpoint for component guide.
   /7001 { /type "allow" /glob "GET /libs/cq/security/userinfo.json?cq_ck=*"}

      #######################################
      ## END: AEM COMMUNITITES ADDITIONS
   #######################################
      
      }

    # The cache section regulates what responses will be cached and where.
    /cache
      {
      # The docroot must be equal to the document root of the webserver. The
      # dispatcher will store files relative to this directory and subsequent
      # requests may be "declined" by the dispatcher, allowing the webserver
      # to deliver them just like static files.
      /docroot "/opt/dispatcher"

      # Sets the level upto which files named ".stat" will be created in the 
      # document root of the webserver. When an activation request for some 
      # page is received, only files within the same subtree are affected 
      # by the invalidation.
      #/statfileslevel "0"
      
      # Flag indicating whether to cache responses to requests that contain
      # authorization information.
      /allowAuthorized "1"
      
      # Flag indicating whether the dispatcher should serve stale content if
      # no remote server is available.
      #/serveStaleOnError "0"
      
      # The rules section defines what responses should be cached based on
      # the requested URL. Please note that only the following requests can
      # lead to cacheable responses:
      #
      # - HTTP method is GET
      # - URL has an extension
      # - Request has no query string
      # - Request has no "Authorization" header (unless allowAuthorized is 1)
      /rules
        {
        /0000
          {
          # the globbing pattern to be compared against the url
          # example: * -> everything
          #        : /foo/bar.* -> only the /foo/bar documents
          #        : /foo/bar/* -> all pages below /foo/bar
          #        : /foo/bar[./]* -> all pages below and /foo/bar itself
          #        : *.html        -> all .html files
          /glob "*"
          /type "allow"
          }

      #######################################
      ## BEGIN: AEM COMMUNITITES ADDITIONS
     #######################################   
    
   # Never cache the client-side .social.json calls
   /0001 { /type "deny" /glob "*.social.json*" }

   # Never cache the user-specific .json requests
   /0002 { /type "deny" /glob "/libs/granite/csrf/token.json*" }
   /0003 { /type "deny" /glob "/libs/granite/security/currentuser.json*" }
   /0004 { /type "deny" /glob "/libs/granite/security/userinfo.json*" }

   # Never cache the private community groups pages in case - add your own deny rules in there
   /0005 { /type "deny" /glob "/content/*/groups/*" }

   # Never cache the assignments page in case the enablement feature is in use - add your own deny rules in there
   /0006 { /type "deny" /glob "/content/*/assignments/*" }
     
      #######################################
      ## END: AEM COMMUNITITES ADDITIONS
      #######################################   
    
        }
        
      # The invalidate section defines the pages that are "invalidated" after
      # any activation. Please note that the activated page itself and all 
      # related documents are flushed on an modification. For example: if the 
      # page /foo/bar is activated, all /foo/bar.* files are removed from the
      # cache.
      /invalidate
        {
        /0000
          {
          /glob "*"
          /type "deny"
          }
        /0001
          {
          # Consider all HTML files stale after an activation.
          /glob "*.html"
          /type "allow"
          }
        /0002
          {
          /glob "/etc/segmentation.segment.js"
          /type "allow"
          }
        /0003
          {
          /glob "*/analytics.sitecatalyst.js"
          /type "allow"
          }
        }

      # The allowedClients section restricts the client IP addresses that are
      # allowed to issue activation requests.
      /allowedClients
        {
        # Uncomment the following to restrict activation requests to originate
        # from "localhost" only.
        #
        #/0000
        #  {
        #  /glob "*"
        #  /type "deny"
        #  }
        #/0001
        #  {
        #  /glob "127.0.0.1"
        #  /type "allow"
        #  }
        }
        
      # The ignoreUrlParams section contains query string parameter names that
      # should be ignored when determining whether some request's output can be
      # cached or delivered from cache.
      #
      # In this example configuration, the "q" parameter will be ignored. 
      #/ignoreUrlParams
      #  {
      #  /0001 { /glob "*" /type "deny" }
      #  /0002 { /glob "q" /type "allow" }
      #  }
      
    /enableTTL "1"

      }
      
    # The statistics sections dictates how the load should be balanced among the
    # renders according to the media-type. 
    /statistics
      {
      /categories
        {
        /html
          {
          /glob "*.html"
          }
        /others
          {
          /glob "*"
          }
        }
      }
    }
  }
```
