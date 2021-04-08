---
title: 高度な設定
seo-title: 高度な設定
description: Maya および Maya 以外のソフトウェアと AEM 3D の統合に適用する高度な設定について説明します。
seo-description: Maya および Maya 以外のソフトウェアと AEM 3D の統合に適用する高度な設定について説明します。
uuid: 016e7745-e3c3-4d77-b95a-c0e671d719e2
contentOwner: Rick Brough
topic-tags: 3D
content-type: reference
products: SG_EXPERIENCEMANAGER/6.4/ASSETS
discoiquuid: e43fd002-2954-4ef1-ac2b-e8d45afa75be
exl-id: fdc82bca-e676-4052-b3e9-a198c685df96
feature: 3D アセット
role: Administrator,Business Practitioner
translation-type: tm+mt
source-git-commit: 13eb1d64677f6940332a2eeb4d3aba2915ac7bba
workflow-type: tm+mt
source-wordcount: '1385'
ht-degree: 60%

---

# 高度な設定 {#advanced-configuration-settings}

一般的な使用例ではデフォルトの設定が適していますが、変更が必要になる場合もあります。

Maya および Maya 以外のソフトウェアと AEM 3D の統合に適用する高度な設定は、以下のとおりです。

AEMの&#x200B;**CRXDE Lite**&#x200B;を使用して、すべての設定にアクセスします(**[!UICONTROL ツール/一般/CRXDE Lite]**)。

>[!NOTE]
>
>パッケージを再インストールすると、すべての設定がデフォルト値にリセットされます。

>[!CAUTION]
>
>以下の表に記載されていない設定を編集すると、予期しないまたは望ましくないプログラムの動作が生じる可能性があります。

## アセットタイプの設定  {#asset-types-configuration}

AEMの&#x200B;**CRXDE Lite**(**[!UICONTROL ツール/一般/CRXDE Lite]**)で、次の設定にアクセスします。

| パス | 説明 |
|---|---|
| `/libs/settings/dam/v3D/assetTypes/*/Conversion` | 取り込み中に作成される中間 3D 形式のファイルタイプを指定します。「fbx」および「obj」ファイル形式の場合は空にし、Maya によって有効になる形式の場合は「fbx」を指定する必要があります。 |
| `/libs/settings/dam/v3D/assetTypes/*/Enabled` | **[!UICONTROL assetTypes]**&#x200B;リストーでこのエントリを有効または無効にするには、trueまたはfalseに設定します。 |
| `/libs/settings/dam/v3D/assetTypes/*/Extension` | このアセットタイプと関連付ける 1 つ以上のファイルサフィックスまたはファイル拡張子をコンマで区切って指定します。 |
| `/libs/settings/dam/v3D/assetTypes/*/IngestRegime` | FBXおよびOBJファイルフォーマットは`native`に、Mayaで有効なフォーマットは`maya`にする必要があります。 |
| `/libs/settings/dam/v3D/assetTypes/*/MimeType` | このアセットタイプの MIME タイプを指定します。Mayaで有効なフォーマットの場合は、`application/x-ext`を使用することをお勧めします。`ext`は`Extension`値として指定された文字列です。 |

## 取り込みの設定 {#ingestion-configuration}

AEMの&#x200B;**CRXDE Lite**(**[!UICONTROL ツール/一般/CRXDE Lite]**)で、次の設定にアクセスします。

<table> 
 <tbody> 
  <tr> 
   <td><strong>パス</strong></td> 
   <td><strong>説明</strong></td> 
  </tr> 
  <tr> 
   <td>/libs/settings/dam/v3D/settings/addGroundPlaneImageOnIngest</td> 
   <td>IBL ステージで表示またはレンダリングするときに、アンビエントオクルージョンドロップシャドウの生成を有効にします。Rapid Refine でのプレビューとレンダリングに適用されます。</td> 
  </tr> 
  <tr> 
   <td><p>/libs/settings/dam/v3D/settings/cleanupRenderWorkDir</p> </td> 
   <td>変換およびレンダリング後に MayaWork フォルダーに一時ファイルを保持する場合は、<strong>false</strong> に設定します。Maya での変換およびレンダリングでの問題をデバッグする場合に役立ちます。</td> 
  </tr> 
  <tr> 
   <td>/libs/settings/dam/v3D/settings/invokeAnimationOnIngest</td> 
   <td><p>有効にした場合、サーバーに ImageMagick がインストールされて、magickPath が設定されます。Rapid Refine を使用して、カード表示やその他の表示でサムネールとして使用される 3D オブジェクトのシンプルなアニメーションが作成されます。</p> <p>アニメーションを作成すると、取り込みプロセス中に CPU リソースを大量に消費します。</p> </td> 
  </tr> 
  <tr> 
   <td>/libs/settings/dam/v3D/settings/invokeLightMapsOnIngest</td> 
   <td>取り込み時にライトマップの自動作成を有効にします。<strong>false</strong> に設定すると、ライトマップの自動作成が無効になります。これにより、CPU リソースの消費が大幅に削減されますが、Rapid Refine でのプレビューおよびレンダリング時の画質が低下する場合があります。Maya でのレンダリングには影響しません。</td> 
  </tr> 
  <tr> 
   <td>/libs/settings/dam/v3D/settings/gPlaneZero</td> 
   <td><p><strong>true</strong>（デフォルト）に設定した場合、必要に応じて、オブジェクトのすべてのパーツが地表面の上(y=0)に来るように、オブジェクトは垂直方向に移動します。</p> <p><strong>false</strong>（デフォルト）に設定した場合、オブジェクトは再配置されず、ステージのグラウンド平面によって部分的に隠れる場合があります。 （Rapid Refine でのプレビューとレンダリングにのみ適用されます）。ただし、Maya でのレンダリングには影響しません。<strong>true</strong>に設定した場合、Mayaのオブジェクトの垂直位置は、プレビューの場合と、高速リファイン(Rapid Refine)を使用してレンダリングする場合とで異なる場合があります。</p> </td> 
  </tr> 
  <tr> 
   <td>/libs/settings/dam/v3D/Paths/magickPath</td> 
   <td>ImageMagick 変換ユーティリティのパスと名前です。アニメーションサムネールの作成が有効な場合は、絶対パスが必要です。</td> 
  </tr> 
  <tr> 
   <td>/libs/settings/dam/v3D/settings/MaxCpuPercentage</td> 
   <td><p>3D アセットの取り込み処理に最大でどの程度の CPU を使用するかを指定します。</p> <p>大きい値を設定すると、取り込み速度が上がりますが、AEM の反応が全体的に遅くなる場合があります。この設定は概算でかまいません。使用できる CPU コアの数が増えれば、精度も向上します。</p> </td> 
  </tr> 
 </tbody> 
</table>

## Cloud Services構成設定{#cloud-services-configuration-settings}

次の設定の値は、Adobeのアカウントマネージャー、プロビジョニングエキスパートまたはサポート担当者が提供します。

| **パス** | **説明** |
|---|---|
| `/libs/settings/dam/v3D/services/aws/accountId` | AdobeAWSアカウントのアカウントID。 |
| `/libs/settings/dam/v3D/services/aws/bucketName` | S3転送バケットの名前。通常は`aem3d`です。 |
| `/libs/settings/dam/v3D/services/aws/customerId` | Adobeが組織に割り当てる一意のID。 AWS CognitoユーザーIDとして使用されます。 |
| `/libs/settings/dam/v3D/services/aws/encryptedPassword` | このcustomerIdに関連付けられているパスワード。 AWS Cognitoパスワードとして使用されます。 |
| `/libs/settings/dam/v3D/services/aws/region` | クラウドサービスがデプロイされるAWSリージョン。 |
| `/libs/settings/dam/v3D/services/aws/userPoolId` | 適用可能なAWS CognitoユーザープールID。 |
| `/libs/settings/dam/v3D/services/dncr/clientId` | AWS CognitoクライアントID（dncrコンバージョンサービス用）。 |

## 共通の処理設定{#common-processing-settings}

AEMの&#x200B;**CRXDE Lite**(**[!UICONTROL ツール/一般/CRXDE Lite]**)で、次の設定にアクセスします。

| **パス** | **説明** |
|---|---|
| `/libs/settings/dam/v3D/Paths/mayaWorkPath` | Maya の変換およびレンダリングの作業フォルダーの名前と場所です。フォルダーが存在しない場合は自動的に作成されます。 |
| `/libs/settings/dam/v3D/Paths/maxWorkPath` | 3ds Max変換の作業フォルダの名前と場所。 フォルダーが存在しない場合は自動的に作成されます。 |
| `/libs/settings/dam/v3D/settings/debugNative` | **[!UICONTROL true]** に設定すると、Rapid Refine レンダラーでの形式変換およびレンダリング中にデバッグ情報を作成できます。 |

## レンダラーの設定 {#renderer-configuration}

AEMの&#x200B;**CRXDE Lite**(**[!UICONTROL ツール/一般/CRXDE Lite]**)で、次の設定にアクセスします。

| **パス** | **説明** |
|---|---|
| `/libs/settings/dam/v3D/settings/dynamicIBL` | **[!UICONTROL true]** に設定し、あらかじめ生成されたライトマップが利用できない場合（つまり、invokeLightMapsOnIngest=false の場合）、Rapid Refine レンダラーは、レンダリング中にライトマップを作成して、レンダリング画質を向上させます。この設定を有効にすると、レンダリング時間が大幅に長くなる場合があります。**[!UICONTROL false]**&#x200B;に設定すると、このような状況でのCPU使用量は最小限に抑えられますが、レンダリング品質は低下する場合があります。 |
| `/libs/settings/dam/v3D/renderers/*/Enabled` | **[!UICONTROL true]** に設定するとレンダラーが有効になり、**[!UICONTROL false]** に設定すると無効になります。 |
| `/libs/settings/dam/v3D/renderers/*/Display` | レンダリングパネルのレンダラーセレクターで表示される有効なレンダラーの文字列を変更できます。 |
| `/libs/settings/dam/v3D/renderers/*/MaxCpuPercentage` | 3D シーンのレンダリングに最大でどの程度の CPU を使用するかを指定します。大きい値を設定すると、レンダリング速度が上がりますが、AEM の反応が全体的に遅くなる場合があります。この設定は概算でかまいません。使用できる CPU コアの数が増えれば、精度も向上します。 |

## 3Dアセットプレビュー設定{#d-asset-preview-settings}

AEMの&#x200B;**CRXDE Lite**(**[!UICONTROL ツール/一般/CRXDE Lite]**)で、次の設定にアクセスします。

| パス | 説明 |
|---|---|
| `/libs/settings/dam/v3D/WebGLSites/autoSpin` | **[!UICONTROL true]**&#x200B;または&#x200B;**[!UICONTROL false]**&#x200B;に設定すると、ページ読み込み時の自動スピン（自動カメラオービット）を有効または無効にできます。 |
| `/libs/settings/dam/v3D/WebGLSites/autoSpinAfterReset` | **[!UICONTROL true]**&#x200B;に設定すると、**[!UICONTROL リセット]**&#x200B;が押された後に自動スピンが再開されます。 自動スピンが無効になっている場合は無視されます。 |
| `/libs/settings/dam/v3D/WebGLSites/autoSpinSpeed` | 自動スピンの速度（1 分あたりの回転数）と方向を指定します。右から左に回転する場合は負の値を、左から右に回転する場合は正の値を指定します。 |
| `/libs/settings/dam/v3D/WebGL/continueRotate` | タッチ操作とマウス操作に対するビューアの応答の段階的なフェードアウトで続行を無効にするには、**[!UICONTROL false]**&#x200B;に設定します。 |
| `/libs/settings/dam/v3D/WebGL/curtainColor` | 読み込みおよび初期化中に 3D アセットプレビューの表示域を任意で覆うことができる読み込みカーテンの色を指定します。R,G,B として値を指定します。それぞれの色成分の範囲は 0～255 です。 |
| `/libs/settings/dam/v3D/WebGL/fadeCurtains` | **[!UICONTROL true]**&#x200B;に設定した場合、ビューアの初期化の後半で、ロードカーテンが徐々にフェードアウトします。 **[!UICONTROL false]**&#x200B;に設定した場合、読み込みと初期化が完了するまで、カーテンは不透明のままです。 |
| `/libs/settings/dam/v3D/WebGL/showCurtains` | **[!UICONTROL true]**&#x200B;または&#x200B;**[!UICONTROL false]**&#x200B;に設定すると、3Dアセットプレビューのロードカーテンの有効/無効が切り替わります。 |
| `/libs/settings/dam/v3D/WebGL/spinHeight` | 自動スピンが有効でアクティブな場合、カメラの垂直方向の位置は、3D オブジェクトの高さを基準にして自動的に調整されます。0.5 に設定すると、カメラの垂直方向の位置はオブジェクトの高さの 1/2 の位置になり、水平線は表示域の垂直方向の中心になります。大きい値を設定すると、カメラはオブジェクトを見下ろすようになり、レンダリングされる水平線の高さは高くなります。小さい値を設定すると、カメラはオブジェクトを見上げるようになり、水平線は低くなります。 |

## 3Dサイトコンポーネントの設定{#d-sites-component-settings}

AEMの&#x200B;**CRXDE Lite**(**[!UICONTROL ツール/一般/CRXDE Lite]**)で、次の設定にアクセスします。

| パス | 説明 |
|---|---|
| `/libs/settings/dam/v3D/WebGLSites/autoSpinAfterReset` | ホームを押した後に自動スピン（自動カメラオービット）を再開するには、**[!UICONTROL true]**&#x200B;に設定します。 自動スピンが無効になっている場合は無視されます。 |
| `/libs/settings/dam/v3D/WebGLSites/continueRotate` | タッチ操作とマウス操作に対するビューアの応答の段階的なフェードアウトで続行を無効にするには、**[!UICONTROL false]**&#x200B;に設定します。 |
| `/libs/settings/dam/v3D/WebGLSites/curtainColor` | 読み込み中に 3D Sites コンポーネントの表示域をオプションで覆うことができる読み込みカーテンの色を指定します。R,G,B として値を指定します。それぞれの色成分の範囲は 0～255 です。 |
| `/libs/settings/dam/v3D/WebGLSites/fadeCurtains` | **[!UICONTROL true]**&#x200B;に設定すると、ロードカーテンは、ロードと初期化の後半の部分で徐々にフェードアウトします。 **[!UICONTROL false]**&#x200B;に設定した場合、読み込みと初期化が完了するまで、カーテンは不透明のままです。 |
| `/libs/settings/dam/v3D/WebGLSites/showCurtains` | **[!UICONTROL true]**&#x200B;または&#x200B;**[!UICONTROL false]**&#x200B;に設定すると、3Dサイトコンポーネントのロードカーテンが有効または無効になります。 |
| `/libs/settings/dam/v3D/WebGLSites/spinHeight` | 自動スピンが有効でアクティブな場合、カメラの垂直方向の位置は、3D オブジェクトの高さを基準にして自動的に調整されます。0.5 に設定すると、カメラの垂直方向の位置はオブジェクトの高さの 1/2 の位置になり、水平線は表示域の垂直方向の中心になります。大きい値を設定すると、カメラはオブジェクトを見下ろすようになり、レンダリングされる水平線の高さは高くなります。小さい値を設定すると、カメラはオブジェクトを見上げるようになり、水平線は低くなります。 |
