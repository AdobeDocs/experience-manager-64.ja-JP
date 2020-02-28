---
title: Adobe Dimensionアセットの操作
seo-title: Adobe Dimensionアセットの操作
description: AEM 3DでのAdobe Dimensionアセットの操作
seo-description: AEM 3DでのAdobe Dimensionアセットの操作
uuid: 476e6758-b3a1-42ba-a18d-bfc407c6a72e
contentOwner: Rick Brough
topic-tags: 3D
products: SG_EXPERIENCEMANAGER/6.4/ASSETS
content-type: reference
discoiquuid: 4a601c2a-4ea1-4308-8ae8-704155f63c21
translation-type: tm+mt
source-git-commit: 5acb16b1734331767554261bbcf9640947f2e23f

---


# Adobe Dimensionアセットの操作 {#working-with-adobe-dimension-assets}

AEM 3D機能パックは、AEM Assets、AEM SitesおよびAEM ScreensのAdobe Dimensionアセット(`.dn` ファイル)をサポートしています。

glTFオープン標準に基づく新しい3Dビューアは、Adobe Dimensionアセットのプレビュー機能とサイトと画面の表示機能を提供します。

## クラウドベースのコンバージョンサービスについて {#about-the-cloud-based-conversion-service}

DimensionアセットがAEMにアップロードされると、ファイルのコピーがAmazon AWSでホストされるアドビが管理するクラウドベースのサービスに転送されます。 このサービスは、アドビ固有のDimensionファイル形式からオープン標準のglTF形式に変換します。 変換された3Dモデルは、バイナリglTF(`.glb`)としてパッケージ化される。 AEMは、変換されたモデルをプライマリディメンションアセットと共にレンディションとして保存します。

変換形式は、次の2つ `.glb` の方法のいずれかを使用して設定できます(手順につ [いては、「AEM 3Dのインストールと設定](install-config-3d.md) 」を参照)。

* Adobe glTF viewerを使用してAEM Assets、AEM SitesまたはAEM Screensでディメンションアセットを表示する場合、アドビ固有の拡張機能を含めて、画質を最大化します。 これにより、レンディショ `.glb` ンはほとんどのサードパーティアプリケーションと互換性がなくなります。
* レンディションとサードパーティアプリケーションとの互換性を維持す `.glb` るために、アドビ固有の拡張機能を除外します。 これにより、AEM Assets、AEM SitesまたはAEM Screens（例えば、IBL照明なし）での表示時の画質が、一般的なサードパーティアプリケーションの画質と同様に制限されます。

Amazon AWSとの間でのDimension/glTFファイルの転送、およびAWSでの一時的なストレージは、完全に保護されます。 これらのファイルはAmazon AWSで最小限の時間で保持されます。通常、通常の操作中は数分以内です。

ディメンションアセットのサポートを有効にするには、コンバージョンサービスにアクセスするための資格情報をアドビから取得する必要があります。 [AEM 3D のインストールと設定](install-config-3d.md)を参照してください。

>[!NOTE]
>
>提供された資格情報をインストールして使用する場合、お客様は、Amazon AWSでホストされるアドビが管理するクラウドベースのコンバージョンサービスにAdobe Dimension 3Dアセットが転送され、処理されることを理解し、同意します。

### AEM Assetsでの表示 {#viewing-on-aem-assets}

AEM 3D機能パックには、Adobe Dimensionアセットの表示に使用されるglTFオープン標準に基づく新しいビューアが含まれています。 このビューアは、ディメンションファイルまたは圧縮されたglTFをAEM Assetsの詳細ビューまたはAEMサイトの3Dコンポーネントで開くときに自動的に選択されます。

glTFビューアのユーザインターフェイスは、他のすべての3Dアセットタイプで使用される標準の3Dビューアとは多少異なることに注意してください。

#### See also the following: {#see-also-the-following}

* [AEM 3Dリリースノート](/help/release-notes/aem3d-release-notes.md) 。DNアセットおよびglTFビューアに適用される制限事項と制限事項について説明します。
* [Adobe Dimensionアセットに固有のコンポーネントプロパティに対する](using-the-3d-sites-component.md) 3Dサイトコンポーネントの操作
* [AEM 3Dのインストールと設定により](install-config-3d.md) 、クラウドベースの変換サービスを設定します。

