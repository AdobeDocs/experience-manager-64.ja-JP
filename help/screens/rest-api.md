---
title: REST API
seo-title: REST API
description: AEM Screens には、Siren の仕様に準拠するシンプルな RESTful API が用意されています。このページの説明に従って、コンテンツ構造内を移動する方法と環境内のデバイスにコマンドを送信する方法を学習します。
seo-description: AEM Screens には、Siren の仕様に準拠するシンプルな RESTful API が用意されています。このページの説明に従って、コンテンツ構造内を移動する方法と環境内のデバイスにコマンドを送信する方法を学習します。
uuid: 5988fdcb-cda5-4d3e-a2ab-f9ee4179e568
contentOwner: Jyotika Syal
content-type: reference
products: SG_EXPERIENCEMANAGER/6.4/SCREENS
topic-tags: developing
discoiquuid: c07b6e4f-c0a4-4151-a543-76dabd6d5146
translation-type: tm+mt
source-git-commit: 95c719ef7f2b4a803b1796f323924cf1a731bf99

---


# REST API{#rest-apis}

AEM Screens には、[Siren](https://github.com/kevinswiber/siren) の仕様に準拠するシンプルな RESTful API が用意されています。この API により、コンテンツ構造内を移動したり、環境内のデバイスにコマンドを送信したりできるようになります。

この API には、[*http://localhost:4502/api/screens.json *](http://localhost:4502/api/screens.json)からアクセスできます。

## コンテンツ構造内での移動 {#navigating-content-structure}

API 呼び出しから返される JSON コードには、現在のリソースに関連するエンティティのリストが記述されています。リストに含まれている自己リンクをたどると、各エンティティに REST リソースとして再びアクセスできます。

例えば、重要なデモロケーションのディスプレイにアクセスするには、次の呼び出しをおこないます。

```xml
GET /api/screens/content/screens/we-retail/locations/demo/flagship.json HTTP/1.1
Host: http://localhost:4502
```

または、次のように curl を使用します。

```xml
curl -u admin:admin http://localhost:4502/api/screens/content/screens/we-retail/locations/demo/flagship.json
```

結果は以下のようになります。

```xml
{
  "class": [
    "aem-io/screens/location"
  ],
  "links": [
    {
      "rel": [
        "self"
      ],
      "href": "http://localhost:4502/api/screens/content/screens/we-retail/locations/demo/flagship.json"
    },
    {
      "rel": [
        "parent"
      ],
      "href": "http://localhost:4502/api/screens/content/screens/we-retail/locations/demo.json"
    }
  ],
  "properties": {…},
  "entities": [
    {
      "class": [
        "aem-io/screens/display"
      ],
      "links": [
        {
          "rel": [
            "self"
          ],
          "href": "http://localhost:4502/api/screens/content/screens/we-retail/locations/demo/flagship/single.json"
        }
      ],
      "rel": [
        "child"
      ],
      "properties": {
        "title": "Single Screen Display",
        "height": 1440,
        "description": "Demo location of a single screen display.",
        "name": "single",
        "width": 2560,
        "idletimeout": 300,
        "layoutrows": 1,
        "layoutcols": 1
      }
    },
    …
  ]
}
```

その後、単一のスクリーンディスプレイにアクセスするには、次の呼び出しをおこないます。

```xml
GET /api/screens/content/screens/we-retail/locations/demo/flagship/single.json HTTP/1.1
Host: http://localhost:4502
```

## リソースに対するアクションの実行 {#executing-actions-on-the-resource}

API 呼び出しで返される JSON コードには、リソースに対して使用可能なアクションのリストを含めることができます。

例えば、このディスプレイでは、割り当てられているすべてのデバイスへのコマンド送信を許可する *broadcast-command* アクションがリストされています。

```xml
GET /api/screens/content/screens/we-retail/locations/demo/flagship/single.json HTTP/1.1
Host: http://localhost:4502
```

または、次のように curl を使用します。

```xml
curl -u admin:admin http://localhost:4502/api/screens/content/screens/we-retail/locations/demo/flagship/single.json
```

***結果:***

```xml
{
  "class": [
    "aem-io/screens/display"
  ],
  "links": […],
  "properties": {…},
  "entities": […],
  "actions": [
    {
      "method": "POST",
      "name": "broadcast-command",
      "href": "/api/screens/content/screens/we-retail/locations/demo/flagship/single",
      "title": "",
      "fields": [
        {
          "name": ":operation",
          "type": "hidden",
          "value": "broadcast-command"
        },
        {
          "name": "command",
          "type": "text"
        },
        {
          "name": "command_payload",
          "optional": true,
          "type": "text"
        }
      ]
    }
  ]
}
```

このアクションを呼び出すには、次の呼び出しをおこないます。

```xml
POST /api/screens/content/screens/we-retail/locations/demo/flagship/single.json HTTP/1.1
Host: http://localhost:4502

:operation=broadcast-command&command=reboot
```

または、次のように curl を使用します。

```xml
curl -u admin:admin -X POST -d ':operation=broadcast-command&command=reboot' http://localhost:4502/api/screens/content/screens/we-retail/locations/demo/flagship/single.json
```

その他のリソースには、異なるアクションが表示されます。 その中には、
- Channels: `boardcast-command`, `broadcast-command-with-ack`, `unassign`
- ディスプレイ: `boardcast-command`, `broadcast-command-with-ack`
- デバイス: `boardcast-command`, `broadcast-command-with-ack`