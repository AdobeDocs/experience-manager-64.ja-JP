---
title: メタデータのスキーマに関する参照情報
description: Dublin Core、IPTC などのメタデータのスキーマを含め、アセットメタデータを記述する際の標準規則を学習します。
contentOwner: AG
feature: Metadata
role: User,Admin
exl-id: 883bebc6-8bbc-43b1-91e5-9e2bf2470b6e
source-git-commit: c5b816d74c6f02f85476d16868844f39b4c47996
workflow-type: tm+mt
source-wordcount: '428'
ht-degree: 25%

---

# メタデータのスキーマに関する参照情報 {#metadata-schemata-reference}

>[!CAUTION]
>
>AEM 6.4 の拡張サポートは終了し、このドキュメントは更新されなくなりました。 詳細は、 [技術サポート期間](https://helpx.adobe.com/jp/support/programs/eol-matrix.html). サポートされているバージョンを見つける [ここ](https://experienceleague.adobe.com/docs/?lang=ja).

次のリファレンスでは、一部のメタデータスキーマに関する情報（アルファベット順）と、プロパティおよびその定義のリストを示します。

## Dublin Core {#dublin-core}

Dublin Core メタデータは、アセットをより検索しやすい形で記述できるように、標準化された規則のセットを提供します。In [!DNL Experience Manager] Assets(Dublin Core) は、ビデオ、サウンド、画像、ドキュメントなどのデジタルアセットを記述します。

シンプルな DCMES(Dublin Core Metadata Element Set) には、次の表に示す 15 個のメタデータ要素が含まれています。 各 Dublin Core 要素はオプションで、繰り返し使用できます。 Dublin Core メタデータ情報は、メディアタイプ固有のメタデータと同様に追加または削除できます。

DCMES 以外にも、Dublin Core Metadata Initiative によって作成された他のメタデータ要素があります。詳しくは、[Dublin Core Initiative](https://dublincore.org/) を参照してください。

| プロパティ | 説明 |
|---|---|
| 投稿者 | コンテンツに貢献する責任を負う人または会社。 |
| 範囲 | アセットの対象となる地理的な場所または期間。 |
| 作成者 | コンテンツの作成を担当する人または会社。 |
| date | アセットに関連付けられた日付または期間。 |
| description | アセットに関する詳細情報。 |
| format | アセットのファイル形式、物理メディア、またはサイズ。 [!DNL Experience Manager] では、dc:format を使用してアセットの mime タイプを示します。 |
| 識別子 | アセットへの一意の参照。 |
| language | アセットの言語（英語の場合は en など）。 |
| 媒体社 | アセットを使用可能にする人または会社。 |
| relation | 関連するアセット。 |
| 権限 | このアセットに対する権限を持つユーザーに関する情報。 |
| source | アセットの派生元となる関連アセット。 |
| 件名 | アセットのトピック。 |
| title | アセットの名前。 |
| type | アセットの特性またはジャンル。 |

## IPTC {#iptc}

IPTC は、世界中の通信機関のコンソーシアムで、技術基準の開発と維持を目標の 1 つとしています。 IPTC は、写真家の間でほぼ一般的に受け入れられる画像に対する一連の写真メタデータ規格を定義しました。 これらのメタデータ規格は、1990 年代に作成された IPTC Information Interchange Model(IIM) と呼ばれるより広範な規格の一部でした。

IPTC ヘッダー情報はほとんどXMPに置き換えられましたが、XMPでは IPTC コアスキーマと拡張スキーマを使用できます。 イメージプログラムでは、XMPと IPTC の両方のプロパティが同期されます。
