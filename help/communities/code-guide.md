---
title: コーディングのガイドライン
seo-title: Coding Guidelines
description: Communities 開発者向けガイドライン、ヒント、テクニック
seo-description: Communities developer guidelines, tips, and tricks
uuid: 311ef4f7-7f2c-44c3-bcf2-f68713752623
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.4/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 244cd43c-a573-495d-b80c-b97ba9d19b75
exl-id: 022043cd-35ed-49b1-b5b4-5cc92d29cef4
source-git-commit: c5b816d74c6f02f85476d16868844f39b4c47996
workflow-type: tm+mt
source-wordcount: '216'
ht-degree: 6%

---

# コーディングのガイドライン {#coding-guidelines}

>[!CAUTION]
>
>AEM 6.4 の拡張サポートは終了し、このドキュメントは更新されなくなりました。 詳細は、 [技術サポート期間](https://helpx.adobe.com/jp/support/programs/eol-matrix.html). サポートされているバージョンを見つける [ここ](https://experienceleague.adobe.com/docs/?lang=ja).

## ガイドライン、ヒントとテクニック {#guidelines-tips-and-tricks}

AEM Communitiesの使用は、Java Server Pages に大きく依存することから、ビジネスロジック、スタイル、ページコンテンツが互いに異なるテンプレートスクリプティング言語を柔軟に選択できるように進化しました。

ユーザー生成コンテンツ (UGC) を柔軟に操作できるのは、SocialResourceProvider API を使用することです。UGC では、どのコンテンツを認識する必要がなくなります [SRP](srp.md) オプションがデプロイメント用に選択されました。

AEM Communities開発者向けの様々なコーディングガイドラインおよびベストプラクティスを次に示します。

### コード {#code}

* [SRP を使用した UGC へのアクセス](accessing-ugc-with-srp.md) - UGC が JCR(JSRP) に格納されている場合にのみ機能するアプリケーションを記述しないようにする方法
* [SocialUtils リファクタリング](socialutils.md) - SocialUtils に代わる SRP のユーティリティメソッド。
* [命名規則](naming-conventions.md)  — カスタム Java クラスの命名規則。

### スクリプト {#scripts}

* [コミュニティコンポーネントのサイドロード](sideloading.md)  — ページの読み込み後に、コンポーネントを動的に追加する方法。
* [リッチテキストエディターの基本事項](rte.md)  — メンバーがコンテンツを投稿するために提供するリッチテキスト UI をカスタマイズする方法。

### IDE {#ide}

* [コミュニティでの Maven の使用](maven.md)  — コミュニティ API jar を含める方法。
* [SocialUtils リファクタリング](socialutils.md) - SocialUtils に代わる SRP のユーティリティメソッド。
