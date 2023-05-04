---
title: OSGi バンドル
seo-title: OSGI Bundles
description: OSGi バンドルの管理に関するヒント
seo-description: Tips for managing your OSGi bundles
uuid: 07af7089-a233-4e5b-928c-76ddc0af8839
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.4/SITES
content-type: reference
topic-tags: best-practices
discoiquuid: 8d3374ac-51dd-4ff5-84c9-495c937ade12
exl-id: 19df20a9-7c89-4dfa-8eca-81c4a14c21ff
source-git-commit: c5b816d74c6f02f85476d16868844f39b4c47996
workflow-type: tm+mt
source-wordcount: '387'
ht-degree: 57%

---

# OSGi バンドル{#osgi-bundles}

>[!CAUTION]
>
>AEM 6.4 の拡張サポートは終了し、このドキュメントは更新されなくなりました。 詳細は、 [技術サポート期間](https://helpx.adobe.com/jp/support/programs/eol-matrix.html). サポートされているバージョンを見つける [ここ](https://experienceleague.adobe.com/docs/?lang=ja).

## セマンティックバージョン管理を使用 {#use-semantic-versioning}

セマンティックバージョニング番号付けに関する合意に基づいたベストプラクティスについては、[https://semver.org/](https://semver.org/) を参照してください。

## OSGi バンドルで厳密に必要とされる以上のクラスや jar を埋め込まないでください。 {#do-not-embed-more-classes-and-jars-than-strictly-needed-in-osgi-bundles}

共通のライブラリは、別々のバンドルにファクタリングする必要があります。 これにより、バンドル間で再利用できます。 をラッピングする場合 *JAR* OSGi バンドルで、オンラインソースで、既にこの操作を実行しているかどうかを確認します。 既存のバンドルラッパーを見つける一般的な場所は次のとおりです。Apache Felix、Apache Sling、Apache Geronimo、Apache ServiceMix、Eclipse バンドルレシピおよび SpringSource Enterprise バンドルリポジトリ。

## 最低限必要なバンドルバージョンに依存 {#depend-on-the-lowest-needed-bundle-versions}

POM ファイルのコンパイル時依存関係の場合、常に、必要な API を公開するために最低限必要なバージョンに依存するようにします。このようにすると、下位互換性を高め、以前のリリースに対するバックポート修正が容易になります。

## OSGi バンドルから最小限のパッケージセットをエクスポートする {#export-a-minimal-set-of-packages-from-osgi-bundles}

パッケージのエクスポートが完了したら、すぐに他のユーザーが依存する API を作成しておきます。エクスポート対象を可能な限り少なくし、エクスポートされているものが API であることを確認してください。以前にエクスポートしたものを取得してプライベートにするよりも、プライベートメソッドまたはクラスを取得してパブリックにする方がはるかに簡単です。

実装は常に別の *impl* パッケージ。 デフォルトでは、 *maven-bundle-plugin* は、 *impl* 名前に。

## エクスポートするパッケージごとに、常にセマンティックバージョンを明示的に定義する {#always-explicitly-define-a-semantic-version-for-each-package-exported}

このようにすることで、API の利用者も新しいバージョンに取り組むことができます。定義の際には、必ずセマンティックバージョニングのベストプラクティスに従ってください。これにより、API の利用者は、新しいバージョンでの変更点がどのようなタイプのものかを知ることができます。

## 公開場所に関するメタタイプ情報を含める {#include-metatype-information-where-exposed}

意味のあるメタタイプ情報を指定することで、Felix コンソールでのサービスおよびコンポーネントが理解しやすくなります。SCR 注釈および属性のリストについては、[https://felix.apache.org/documentation/subprojects/apache-felix-maven-scr-plugin/scr-annotations.html](https://felix.apache.org/documentation/subprojects/apache-felix-maven-scr-plugin/scr-annotations.html) を参照してください。
