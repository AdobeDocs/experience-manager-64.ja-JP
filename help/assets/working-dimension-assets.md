---
title: Adobe Dimensionアセットの操作
description: AEM 3DでのAdobe Dimensionアセットの操作
contentOwner: Rick Brough
topic-tags: 3D
products: SG_EXPERIENCEMANAGER/6.4/ASSETS
content-type: reference
exl-id: be8f6361-607d-4529-aef0-e8978dfd04b4
feature: 3D Assets
role: Business Practitioner
translation-type: tm+mt
source-git-commit: f9faa357f8de92d205f1a297767ba4176cfd1e10
workflow-type: tm+mt
source-wordcount: '498'
ht-degree: 1%

---

# Adobe Dimension資産の操作{#working-with-adobe-dimension-assets}

>[!IMPORTANT]
>
>AEM 6.4のAEM 3D機能パックは、サポートされなくなりました。 Adobeでは、[AEMの3Dアセット機能をCloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/assets/dynamicmedia/assets-3d.html#dynamicmedia)または[AEM 6.5.3以降として使用することをお勧めします。](https://experienceleague.adobe.com/docs/experience-manager-65/assets/dynamic/assets-3d.html#dynamic) Adobe Dimensionアセットを使用する場合

AEM 3D機能パックは、AEM Assets、AEM Sites、AEM ScreensのAdobe Dimensionアセット（`.dn`ファイル）をサポートしています。

glTFオープン規格に基づく新しい3Dビューアは、Adobe Dimensionアセットのプレビューおよびサイトと画面の表示機能を提供します。

## クラウドベースのコンバージョンサービスについて{#about-the-cloud-based-conversion-service}

DimensionアセットがAEMにアップロードされると、ファイルのコピーが、AmazonAWSでホストされるAdobe管理のクラウドベースのサービスに転送されます。 このサービスは、Adobe固有のDimensionファイル形式からオープン標準のglTF形式に変換します。 変換された3Dモデルは、バイナリglTF(`.glb`)としてパッケージ化されます。 AEMは、変換されたモデルをプライマリDimensionアセットと共にレンディションとして保存します。

`.glb`変換形式は、次の2つの方法のいずれかを使用して設定できます(手順については、[AEM 3Dのインストールと設定](install-config-3d.md)を参照)。

* AEM Assets、AEM Sites、AEM Screensの表示Dimensionアセットに対してAdobeglTFビューアを使用する場合、視覚的な画質を最大限に高めるために、Adobe固有の拡張機能を含めます。 これにより、`.glb`レンディションは、ほとんどのサードパーティアプリケーションと互換性がなくなります。
* Adobe固有の拡張子を除外して、`.glb`レンディションとサードパーティのアプリケーションとの互換性を維持します。 これにより、AEM Assets、AEM Sites、AEM Screensでの表示時の画質が制限され（例えば、IBL照明がない場合）、一般的なサードパーティアプリケーションの画質をシミュレートできます。

Dimension/glTFファイルのAmazonAWSとの間またはAWSとの間での転送、およびAWSでのそれらの一時的なストレージは完全に保護されます。 これらのファイルは、AmazonAWSでは最小限の時間で保持されます。通常、通常の操作中は数分以内です。

Dimensionアセットのサポートを有効にするには、Adobeから変換サービスにアクセスするための資格情報を取得する必要があります。 [AEM 3D のインストールと設定](install-config-3d.md)を参照してください。

>[!NOTE]
>
>提供された資格情報をインストールして使用する場合、お客様は、AmazonAWSでホストされるAdobe管理のクラウドベースの変換サービスに、お客様のAdobe Dimension3Dアセットが転送され、処理されることを理解し、同意します。

### AEM Assetsでの表示{#viewing-on-aem-assets}

AEM 3D機能パックには、Adobe Dimensionアセットの表示に使用するglTFオープン規格に基づく新しいビューアが含まれています。 このビューアは、Dimensionファイルまたは圧縮されたglTFをAEM Assetsの詳細表示に開くか、AEM Sitesの3Dコンポーネントで開くときに自動的に選択されます。

glTFビューアのユーザインターフェイスは、他のすべての3Dアセットタイプで使用される標準の3Dビューアとは少し異なることに注意してください。

#### 次も参照してください。{#see-also-the-following}

* [AEM 3Dリリース](/help/release-notes/aem3d-release-notes.md) ノート（DNアセットおよびglTFビューアに適用される制限および制限に関するもの）。
* [3Dサイトコンポー](using-the-3d-sites-component.md) ネントの操作(Adobe Dimensionアセット固有のコンポーネントプロパティ用)
* [AEMのインストールと設定3](install-config-3d.md) Dクラウドベースの変換サービスを設定します。
