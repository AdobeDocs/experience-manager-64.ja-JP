---
title: アセットを効率的に翻訳するためのベストプラクティス
description: 翻訳された各バージョンを同期し、翻訳ワークフローを合理化するための、アセットの効率的な管理に関するベストプラクティス。
contentOwner: AG
feature: Translation
role: User,Admin
exl-id: 15162b80-ddef-4ec0-9db6-36695c93ebb1
source-git-commit: de5632ff0ee87a4ded88e792b57e818baf4c01a3
workflow-type: tm+mt
source-wordcount: '498'
ht-degree: 94%

---

# アセットの翻訳のベストプラクティス 効率的に {#best-practices-for-translating-assets-efficiently}

Adobe Experience Manager Assets は、デジタルアセットのバイナリ、メタデータ、タグを複数のロケールに翻訳し、翻訳済みアセットを管理する多言語ワークフローをサポートしています。 詳しくは、[多言語のアセット](multilingual-assets.md)を参照してください。

アセットの管理を効率化して、翻訳された各バージョンが確実に同期されるようにするには、翻訳ワークフローを実行する前にアセットの[言語コピー](preparing-assets-for-translation.md)を作成します。

アセットやアセットのグループの言語コピーは、類似のコンテンツ階層を持つ言語の兄弟（または同系言語のアセットのバージョン）です。

各言語コピーは独立したアセットです。このため、アセットを複数のロケールに翻訳すると、CRX リポジトリのサイズが大幅に大きくなります。例えば、合計サイズが 10 GB のアセットを 2 言語に翻訳すると、リポジトリのサイズが約 20 GB（各言語 10 GB）大きくなります。

アセットのバイナリはメタデータやタグと比較して、大量のストレージ領域を占有します。このため、メタデータやタグを翻訳するだけで済む場合は、バイナリの翻訳は省略してください。別のロケールに翻訳されたメタデータとタグとの関連付けのために、バイナリの元のコピーをリポジトリで保持することができます。バイナリは、複数の翻訳されたバージョンではなく単一のコピーを管理することで、リポジトリのサイズへの影響を最小限に抑えることができます。

ファイルデータストアや Amazon S3 データストアはこれらのシナリオに最適なストレージインフラストラクチャを提供します。これらのストレージリポジトリは、複数のロケールのメタデータやタグで共有できる、アセットバイナリの単一のコピー（レンディションを含む）を保存します。このため、アセットの言語コピーを作成してメタデータやタグを翻訳しても、リポジトリのサイズには影響を及ぼしません。

いくつかのワークフローや翻訳統合フレームワークの設定を少し変更して、処理の効率を上げることもできます。

1. 次のいずれかの操作を行います。

   * [ファイルデータストアの設定](/help/sites-deploying/data-store-config.md)
   * [Amazon S3 データストアの設定](/help/sites-deploying/data-store-config.md)

1. [DAM メタデータの書き戻し](/help/sites-administering/workflow-offloader.md#disable-offloading)ワークフローを無効化します。

   名前が示すとおり、**「DAM メタデータの書き戻し」ワークフローはメタデータをバイナリファイルに書き直します。メタデータは翻訳後に変更になるので、バイナリファイルに書き戻すと言語コピーに別のバイナリが生成されます。

   >[!NOTE]
   >
   >**「DAM メタデータの書き戻し」ワークフローを無効化すると、アセットバイナリで XMP メタデータの書き戻しがオフになります。結果として、将来メタデータに加えられる変更はアセット内に保存されなくなります。このワークフローを無効にする前に、結果を評価してください。

1. 「*最終変更日を設定*」ワークフローを有効化します。

   アセットの最終変更日は、「*DAM メタデータの書き戻し*」ワークフローが設定します。このワークフローは手順 2 で無効にするので、[!DNL Experience Manager Assets] は今後アセットの最終変更日を最新の状態に保つことができなくなります。このため、「*最終変更日を設定*」ワークフローを有効化して、アセットの最終変更日が最新の状態に保たれるようにします。最終変更日が最新でないアセットはエラーの原因となる場合があります。

1. アセットのバイナリを翻訳しないように、[翻訳統合フレームワークを設定](/help/sites-administering/tc-tic.md)します。「アセット」タブの「アセットを翻訳」の選択を解除して、アセットのバイナリの翻訳を停止します。
1. [多言語のアセットのワークフロー](multilingual-assets.md)を使用して、アセットのメタデータやタグを翻訳します。
