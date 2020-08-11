---
title: 3D アセットの表示
seo-title: 3D アセットの表示
description: AEM のアセットの詳細ページから利用できるインタラクティブ 3D ビューア、およびインタラクティブ 3D ビューアを使用した 3D アセットの表示方法について学習します。
seo-description: AEM のアセットの詳細ページから利用できるインタラクティブ 3D ビューア、およびインタラクティブ 3D ビューアを使用した 3D アセットの表示方法について学習します。
uuid: 7d8133ac-3110-4979-8e19-e65090e791be
contentOwner: Rick Brough
topic-tags: 3D
content-type: reference
products: SG_EXPERIENCEMANAGER/6.4/ASSETS
discoiquuid: 65040923-a8a8-4e27-82c0-67a04348e238
translation-type: tm+mt
source-git-commit: 11b65cf2d180f04168d4c5d0929957c95a372e3c
workflow-type: tm+mt
source-wordcount: '1806'
ht-degree: 70%

---


# 3D アセットの表示 {#viewing-d-assets}

>[!IMPORTANT]
>
>AEM 6.4でのAEM 3Dのサポートは終了しました。 Adobeでは、 [AEMの3Dアセット機能をCloud Service](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/assets/dynamicmedia/assets-3d.html)[またはAEM 6.5.3以降として使用することをお勧めします。](https://docs.adobe.com/content/help/en/experience-manager-65/assets/dynamic/assets-3d.html) を表示3Dアセットに追加します。

このドキュメントでは、3D アセットをアセットの詳細で表示する方法と 3D コンポーネント内のアセットをサイトで表示する方法の両方について説明します。

## アセットの詳細ページでの 3D アセットの表示 {#viewing-d-assets-in-the-asset-details-page}

AEM のアセットの詳細ページから、インタラクティブ 3D ビューアを使用できます。このビューアには、3D アセットをオービット、ズームおよびパンできるインタラクティブなカメラコントロールのコレクションが含まれます。

![chlimage_1-139](assets/chlimage_1-139.png)

AEM 3D のデフォルトのステージを使用する他に、サードパーティ製アプリケーションで作成して AEM にアップロードしたステージも使用できます。

[AEM 3D でのステージの使用](about-the-use-of-stages-in-aem-3d.md)を参照してください。

>[!NOTE]
>
>3D アセットを表示するには、デバイスまたはデスクトップのブラウザーが WebGL に対応している必要があります。また、基盤となるグラフィックハードウェアには、目的のサイズと複雑度のモデルをレンダリングできるだけの性能とメモリが必要です。シャドウの表示などの特定のプレビュー機能は、すべてのブラウザーで利用できません。

### 3D アセットを表示する際のパフォーマンスに関する考慮事項 {#performance-considerations-when-you-view-d-assets}

アセットの詳細ページビューで 3D アセットを開くのにかかる時間は、いくつかの要因に依存します。以下の要因が含まれます。

* サーバーへの帯域幅と遅延。
* モデルサイズ（面の数）。
* マップの数とサイズ。
* ステージの複雑さ。例えば、IBL 画像のサイズなどです。

さらに、カメラをインタラクティブに操作する際に、ワークステーション、ノートパソコン、モバイルタッチデバイスなどのクライアントコンピューターの性能を考慮することも重要です。グラフィック性能に優れ、ある程度パワフルなシステムなら、インタラクティブな 3D 表示をよりスムーズで満足なものにすることができます。

**表示3Dアセット**:

1. 3D アセットが AEM にアップロードされていることを確認します。

   [AEM での 3D アセットのアップロードと処理](upload-processing-3d-assets.md)を参照してください。

1. From AEM, on the **[!UICONTROL Navigation]** page, tap **[!UICONTROL Assets]**.
1. ページの右上隅付近にある「**[!UICONTROL 表示]**」ドロップダウンリストで「**[!UICONTROL カード表示]**」をタップします。
1. 表示する 3D アセットに移動します。
1. 3D アセットのカードをタップして、アセットの詳細ページで開きます。
1. 次のいずれかの操作をおこないます。

   * アセットの詳細ページの右下隅にあるカメラコントロールパレットを使用して、アセットの様々な表示を変更します。

      従来の Apple のシングルボタンマウスなど、スクロールホイールのない非接触型入力デバイスを使用している場合は、ズームモードまたはパースペクティブモードでも 3D アセットのズームまたはパースペクティブを変更できます。このアクションは、`SHIFT` キーを押しながらマウスボタンを押して上または下方向にドラッグすることによって、実行します。

      一般的なノートコンピューターのタッチパッドを使用していると、多くの場合、2 本指を使用したジェスチャでズーム動作またはパースペクティブ動作をコントロールすることは困難です。そのような場合は、`SHIFT` キーを押しながらアクションを実行します。そうすると、ピンチジェスチャの速度が低下し、必要とする正確なズームレベルまたはパースペクティブを実現しやすくなります。Alternately, you can use a one finger drag up or down while the `SHIFT`key is pressed to affect zoom or perspective behaviors.
   <table> 
    <tbody> 
      <tr> 
      <td><strong>カメラコントロール名</strong><br /> </td> 
      <td><strong>説明</strong></td> 
      </tr> 
      <tr> 
      <td><p>ズーム</p> <p>または</p> <p>パースペクティブ</p> </td> 
      <td><p>タップまたはクリックしてズームモードとパースペクティブモードを切り替えます。</p> <p>または、<code>ALT/OPTION</code> キーを押しながらアクションを実行して、一時的にパースペクティブモードに切り替えます。<br />キーを放すとズームモードに戻ります。</p> 
      <ul> 
      <li><strong>ズーム</strong>— ドリーインとドリーアウトの動作で、カメラを表示しているアセットに近づくか遠ざけます<br /> 。 ズームは、マウスのスクロールホイール（利用可能な場合）、モバイルデバイスでの 2 本の指によるピンチ操作、あるいは Shift キーを押したまま左マウスボタンを使用して上または下にドラッグしたときのデフォルトの動作です。</li> 
      <li><strong>パースペクティブ</strong>-表示内のアセットの相対サイズを維持しながら、表示の焦点距離（の場とも呼ばれます）を変更します。 パースペクティブは、スクロールホイール（利用可能な場合）、モバイルデバイスでの 2 本の指によるピンチ操作、あるいは Shift キーを押したまま左マウスボタンを使用して上または下にドラッグする動作の代替の動作です。</li> 
      </ul> </td> 
      </tr> 
      <tr> 
      <td><p>オービット</p> <p>または</p> <p>パン</p> </td> 
      <td><p>タップまたはクリックしてオービットモードとパンモードを切り替えます。</p> <p>または、<code>ALT/OPTION</code> キーを押しながらアクションを実行して、一時的にパンモードに切り替えます。キーを放すとオービットモードに戻ります。</p> 
      <ul> 
      <li><strong>[軌道</strong>]:3Dアセットの中心付近にあるターゲット点を中心とする球上のビューカメラを既定値に移動します。 オービットは、モバイルデバイスでの左ボタンドラッグまたはシングルタッチドラッグのデフォルトの動作です。</li> 
      <li><strong>[パン</strong>]：ビュー平面内のカメラを移動します。 ターゲットポイントはカメラ対応して移動するので、以降のオービットアクションでは、カメラは新しいターゲットポイントを中心として移動します。パンは、左ボタンドラッグおよびシングルタッチドラッグの代替動作です。</li> 
      </ul> </td> 
      </tr> 
      <tr> 
      <td><p>調査</p> <p>または</p> <p>ターゲット</p> </td> 
      <td><p>タップまたはクリックして調査モードとターゲットモードを切り替えます。</p> 
      <ul> 
      <li><strong>Examine</strong>-Tapキーを押すか、クリックしてターゲットモードに入ります。</li> 
      <li><strong>ターゲット</strong>- 3Dアセットの任意の場所をタップまたはクリックして、アセットのその部分の表示を中央に配置します。<br />オービットアクションでは、新しいターゲットポイントが使用されます。</li> 
      </ul> </td> 
      </tr> 
      <tr> 
      <td>リセット</td> 
      <td>タップまたはクリックして、視野のターゲットポイントをモデルの中心に戻します。リセットでも、アセット全体を表示したり、適切な表示サイズで表示するために、カメラを近づけたり遠ざけたりします。<br /></td> 
      </tr> 
    </tbody> 
    </table>

   * Near the upper-right corner of the asset details page, tap the **[!UICONTROL Stage Selector]** icon. 3D アセットに適用する背景とライティングを含むステージ名を選択します。

   ![chlimage_1-140](assets/chlimage_1-140.png)

   ステージは、3Dモデルが表示される環境 — 背景、接地面、照明を提供します。

   [AEM 3D でのステージの使用](about-the-use-of-stages-in-aem-3d.md)を参照してください。

   * Near the upper-right corner of the asset details page, tap the **[!UICONTROL Camera Selector]** icon, then select a camera view that you want to apply to the 3D asset.

   ![chlimage_1-141](assets/chlimage_1-141.png)

   多くの場合、ステージには事前定義済みのカメラが含まれています。現在のカメラを再選択して、事前定義済みの設定に戻すことができます。

   [AEM 3D でのステージの使用](about-the-use-of-stages-in-aem-3d.md)を参照してください。

1. ページの右上隅にある「**[!UICONTROL 保存]**」をタップします。
1. 次のいずれかの操作をおこないます。

   * 3D アセットをレンダリングします。

      [3D アセットのレンダリング](rendering-3d-assets.md)を参照してください。

   * ページの右上隅にある「**[!UICONTROL 閉じる]**」をタップして、アセットページに戻ります。

## Sites 3D コンポーネント内の 3D アセットの表示 {#viewing-d-assets-in-the-sites-d-component}

>[!NOTE]
>
>この節は、Adobe Dimension以外の3Dアセットタイプで使用される従来のwebGLビューアにのみ適用されます。

デバイスのタイプに応じて、様々な方法で 3D コンポーネント機能にアクセスします。

詳しくは、次のトピックを参照してください。

* [タッチスクリーンデバイス](#touchscreen-devices)
* [タッチパッドデバイス](#touchpad-devices)
* [マウスおよびトラックボールデバイス](#mouse-and-trackball-devices)

詳しくは、3Dコンポーネントを含むWebページの [プレビューも参照してください](using-the-3d-sites-component.md#previewing-a-web-page-that-has-a-d-component)。

![screen_shot_2017-12-11at145654](assets/screen_shot_2017-12-11at145654.png)

### タッチスクリーンデバイス {#touchscreen-devices}

タッチスクリーンデバイスで 3D コンポーネントを操作するには：

1. 1 本の指でドラッグまたはスワイプして、オブジェクトの周囲で視点（「カメラ」）を移動（「オービット」）します。あらゆる方向からオブジェクトを表示できます。

1. 2 本の指でピンチして、カメラをオブジェクトに近づけたり、オブジェクトから遠ざけたりします。このアクションはズームインまたはズームアウトと同様です。このアクションを使用して、オブジェクトを詳しく調べることができます。また、「+」ボタンを押したままにしてカメラをオブジェクトに近づけたり、「-」ボタンを押したままにしてカメラをオブジェクトから遠ざけたりすることもできます。

1. 2 本の指でドラッグして、カメラをパンします。このアクションではカメラを横方向に移動して、ズームインしたままオブジェクトの様々な部分を見ることができます。Alternatively, tap the **[!UICONTROL Orbit/Pan Toggle]** button to toggle to Pan mode, then use a one-finger drag to pan the camera. Tap the **[!UICONTROL Orbit/Pan Toggle]** button to revert to **[!UICONTROL Orbit]** mode.

1. **[!UICONTROL ビューアをリセット]**&#x200B;をタップして、カメラをリセットします。このアクションにより、オブジェクト全体の表示に戻り、自動スピンが有効になっている場合は自動スピンが再開されます。

1. **[!UICONTROL 全画面表示]**&#x200B;をタップして、全画面表示モードに切り替えます（デバイスでサポートされている場合）。**[!UICONTROL 全画面表示]**&#x200B;を再度タップすると、3D ビューアはページ埋め込みモードに戻ります。

### タッチパッドデバイス {#touchpad-devices}

タッチパッドデバイスで 3D コンポーネントを操作するには：

1. （左）タッチパッドボタンを押しながら 1 本の指でドラッグして、オブジェクトの周囲で視点（「カメラ」）を移動（「オービット」）します。あらゆる方向からオブジェクトを表示できます。

1. タッチパッドボタンを押し込まずに 2 本の指で下方向または上方向にドラッグして、カメラをオブジェクトに近づけたり、オブジェクトから遠ざけたりします。このアクションはズームインまたはズームアウトと同様です。このアクションを使用して、オブジェクトを詳しく調べることができます。Alternatively, click and hold the **[!UICONTROL Zoom In]** or **[!UICONTROL Zoom Out]** buttons to move the camera closer or farther away from the object.

1. Use a one-finger drag while holding the **ALT/option** key and the (left) touchpad button to pan the camera. このアクションではカメラを横方向に移動して、ズームインしたままオブジェクトの様々な部分を見ることができます。Alternatively, click the **[!UICONTROL Orbit/Pan Toggle]** button to toggle to **[!UICONTROL Pan]** mode, then use a one-finger drag while holding the (left) button to pan the camera. Click the **[!UICONTROL Orbit/Pan Toggle]** button again to revert to **[!UICONTROL Orbit]** mode.

1. Click **[!UICONTROL Reset Viewer]** to reset the camera. このアクションにより、オブジェクト全体の表示に戻り、自動スピンが有効になっている場合は自動スピンが再開されます。

1. Click **[!UICONTROL Full Screen]** to enter full-screen mode. Use the **Escape** key on your keyboard or click **[!UICONTROL Full Screen]** again to restore the 3D viewer to page-embedded mode.

### マウスおよびトラックボールデバイス {#mouse-and-trackball-devices}

マウスおよびトラックボールデバイスで 3D コンポーネントを操作するには：

1. 左マウスボタンを押しながらドラッグして、オブジェクトの周囲で視点（「カメラ」）を移動（「オービット」）します。あらゆる方向からオブジェクトを表示できます。

1. スクロールホイールを使用して、カメラをオブジェクトに近づけたり、オブジェクトから遠ざけたりします。このアクションはズームインまたはズームアウトと同様です。このアクションを使用して、オブジェクトを詳しく調べることができます。Alternatively, click and hold the **[!UICONTROL Zoom In]** or **[!UICONTROL Zoom Out]** buttons to move the camera closer or farther away from the object.

1. Drag while holding the **ALT/option** key and the left mouse button to pan the camera. このアクションではカメラを横方向に移動して、ズームインしたままオブジェクトの様々な部分を見ることができます。Alternatively, click the **[!UICONTROL Orbit/Pan Toggle]** button to toggle to **[!UICONTROL Pan]** mode, then drag while holding the left mouse button to pan the camera. Click the **[!UICONTROL Orbit/Pan Toggle]** again to revert to **[!UICONTROL Orbit]** mode.
1. Click **[!UICONTROL Reset Viewer]** to reset the camera. このアクションにより、オブジェクト全体の表示に戻り、自動スピンが有効になっている場合は自動スピンが再開されます。
1. Click **[!UICONTROL Full Screen]** to enter full-screen mode. Use the **[!UICONTROL Escape]** key on your keyboard or click **[!UICONTROL Full Screen]** again to restore the 3D viewer to page-embedded mode.

