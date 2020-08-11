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
source-git-commit: 11b65cf2d180f04168d4c5d0929957c95a372e3c
workflow-type: tm+mt
source-wordcount: '511'
ht-degree: 1%

---


# Adobe Dimensionアセットの操作 {#working-with-adobe-dimension-assets}

>[!IMPORTANT]
>
>AEM 6.4のAEM 3D機能パックは、サポートされなくなりました。 Adobeでは、 [AEMの3Dアセット機能をCloud Service](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/assets/dynamicmedia/assets-3d.html)[またはAEM 6.5.3以降として使用することをお勧めします。](https://docs.adobe.com/content/help/en/experience-manager-65/assets/dynamic/assets-3d.html) adobe dimensionアセットを使用する場合

AEM 3D機能パックは、AEM Assets、AEM Sites、AEM ScreensのAdobe Dimensionアセット(`.dn` ファイル)をサポートしています。

glTFオープン規格に基づく新しい3Dビューアは、Adobe Dimensionアセットのプレビューおよびサイトと画面の表示機能を提供します。

## クラウドベースのコンバージョンサービスについて {#about-the-cloud-based-conversion-service}

DimensionアセットがAEMにアップロードされると、ファイルのコピーが、AmazonAWSでホストされるAdobe管理のクラウドベースのサービスに転送されます。 このサービスは、Adobe固有のDimensionファイル形式からオープン標準のglTF形式に変換します。 変換された3Dモデルは、バイナリglTF (`.glb`)としてパッケージ化されます。 AEMは、変換されたモデルをプライマリDimensionアセットと共にレンディションとして保存します。

変換形式は、次の2つの方法のいずれかを使用して設定できます(手順については、AEM 3Dの `.glb` インストールと設定を参照 [](install-config-3d.md) )。

* AEM Assets、AEM Sites、AEM Screensの表示Dimensionアセットに対してAdobeglTFビューアを使用する場合、視覚的な画質を最大限に高めるために、Adobe固有の拡張機能を含めます。 これにより、レンディションはほとんどのサードパーティアプリケーションと互換性がなくなります。 `.glb`
* Adobe固有の拡張子を除外して、レンディションとサードパーティのアプリケーションとの互換性を維持します。 `.glb` これにより、AEM Assets、AEM Sites、AEM Screensでの表示時の画質が制限され（例えば、IBL照明がない場合）、一般的なサードパーティアプリケーションの画質をシミュレートできます。

Dimension/glTFファイルのAmazonAWSとの間またはAWSとの間での転送、およびAWSでのそれらの一時的なストレージは完全に保護されます。 これらのファイルは、AmazonAWSでは最小限の時間で保持されます。通常、通常の操作中は数分以内です。

Dimensionアセットのサポートを有効にするには、Adobeから変換サービスにアクセスするための資格情報を取得する必要があります。 [AEM 3D のインストールと設定](install-config-3d.md)を参照してください。

>[!NOTE]
>
>提供された資格情報をインストールして使用する場合、お客様は、AmazonAWSでホストされるAdobe管理のクラウドベースの変換サービスに、お客様のAdobe Dimension3Dアセットが転送され、処理されることを理解し、同意します。

### AEM Assetsでの閲覧 {#viewing-on-aem-assets}

AEM 3D機能パックには、Adobe Dimensionアセットの表示に使用するglTFオープン規格に基づく新しいビューアが含まれています。 このビューアは、Dimensionファイルまたは圧縮されたglTFをAEM Assetsの詳細表示に開くか、AEM Sitesの3Dコンポーネントで開くときに自動的に選択されます。

glTFビューアのユーザインターフェイスは、他のすべての3Dアセットタイプで使用される標準の3Dビューアとは少し異なることに注意してください。

#### See also the following: {#see-also-the-following}

* [DNアセットとglTFビューアに適用される制限および制限に関するAEM 3Dリリースノート](/help/release-notes/aem3d-release-notes.md) 。
* [3Dサイトコンポーネントの操作](using-the-3d-sites-component.md) (Adobe Dimensionアセット固有のコンポーネントプロパティ用)
* [AEM 3Dのインストールと設定により、クラウドベースの変換サービスを設定します。](install-config-3d.md)

