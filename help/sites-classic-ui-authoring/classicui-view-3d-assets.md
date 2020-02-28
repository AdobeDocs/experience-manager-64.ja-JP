---
title: 3D アセットの表示
seo-title: 3D アセットの表示
description: AEM のアセットの詳細ページから、インタラクティブ 3D ビューアを使用できます。このビューアには、3D アセットをオービット、ズームおよびパンできるインタラクティブなカメラコントロールのコレクションが含まれます。
seo-description: AEM のアセットの詳細ページから、インタラクティブ 3D ビューアを使用できます。このビューアには、3D アセットをオービット、ズームおよびパンできるインタラクティブなカメラコントロールのコレクションが含まれます。
uuid: 06dea4d6-c33a-45da-a9a7-7caae9d1717a
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.4/ASSETS
topic-tags: authoring
content-type: reference
discoiquuid: 5e1e0039-670e-4051-9f2a-e88162482467
translation-type: tm+mt
source-git-commit: cdec5b3c57ce1c80c0ed6b5cb7650b52cf9bc340

---


# 3D アセットの表示{#viewing-d-assets}

AEM のアセットの詳細ページから、インタラクティブ 3D ビューアを使用できます。このビューアには、3D アセットをオービット、ズームおよびパンできるインタラクティブなカメラコントロールのコレクションが含まれます。

![chlimage_1-16](assets/chlimage_1-16.png)

AEM 3D のデフォルトのステージを使用する他に、サードパーティ製アプリケーションで作成して AEM にアップロードしたステージも使用できます。

[AEM 3D でのステージの使用](/help/sites-classic-ui-authoring/classicui-stages-aem3d.md)を参照してください。

>[!NOTE]
>
>3D アセットを表示するには、デバイスまたはデスクトップのブラウザーが WebGL に対応している必要があります。また、基盤となるグラフィックハードウェアには、目的のサイズのモデルをレンダリングできるだけの性能とメモリが必要です。

## 3D アセットを表示する際のパフォーマンスに関する考慮事項 {#performance-considerations-when-you-view-d-assets}

アセットの詳細ページビューで 3D アセットを開くのにかかる時間は、いくつかの要因に依存します。以下の要因が含まれます。

* サーバーへの帯域幅と遅延。
* モデルサイズ（面の数）。
* マップの数とサイズ。
* ステージの複雑さ。例えば、IBL 画像のサイズなどです。

また、ワークステーション、ノートブック、モバイルタッチデバイスなどのクライアントコンピュータの機能も、カメラをインタラクティブに操作する際に考慮する必要があります。 グラフィック性能に優れ、ある程度パワフルなシステムなら、インタラクティブな 3D 表示をよりスムーズで満足なものにすることができます。

**3Dアセットを表示するには**:

1. 3D アセットが AEM にアップロードされていることを確認します。

   [AEM での 3D アセットのアップロードと処理](/help/sites-classic-ui-authoring/classicui-upload-proc-3d.md)を参照してください。
1. **[!UICONTROL Adobe Experience Manager]** の&#x200B;**[!UICONTROL ナビゲーション]**&#x200B;ページで「**[!UICONTROL アセット]**」をタップします。
1. Near the upper-right corner of the page, from the **[!UICONTROL View]** drop-down list, tap **[!UICONTROL Card View]**.

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
      <td><p>ズーム</p> <p>「」または「」</p> <p>パースペクティブ</p> </td> 
      <td><p>タップまたはクリックしてズームモードとパースペクティブモードを切り替えます。</p> <p>または、<code>ALT/OPTION</code> キーを押しながらアクションを実行して、一時的にパースペクティブモードに切り替えます。<br />キーを放すとズームモードに戻ります。</p> 
        <ul> 
        <li><strong>ズーム</strong>— ドリーインとドリーアウトの動作で、カメラを表示しているアセットの近くまたは遠くに<br /> 移動させます。 ズームは、マウスのスクロールホイール（利用可能な場合）、モバイルデバイスでの 2 本の指によるピンチ操作、あるいは Shift キーを押したまま左マウスボタンを使用して上または下にドラッグしたときのデフォルトの動作です。</li> 
        <li><strong>[パースペクティブ</strong>]：ビュー内のアセットの相対サイズを維持しながら、カメラの焦点距離（視野）を変更します。 パースペクティブは、スクロールホイール（利用可能な場合）、モバイルデバイスでの 2 本の指によるピンチ操作、あるいは Shift キーを押したまま左マウスボタンを使用して上または下にドラッグする動作の代替の動作です。</li> 
        </ul> </td> 
      </tr> 
      <tr> 
      <td><p>オービット</p> <p>「」または「」</p> <p>パン</p> </td> 
      <td><p>タップまたはクリックしてオービットモードとパンモードを切り替えます。</p> <p>または、<code>ALT/OPTION</code> キーを押しながらアクションを実行して、一時的にパンモードに切り替えます。キーを放すとオービットモードに戻ります。</p> 
        <ul> 
        <li><strong>[オービット</strong>]:3Dアセットの中心近くにあるターゲットポイントを中心に球上のビューカメラを既定値に移動します。 オービットは、モバイルデバイスでの左ボタンドラッグまたはシングルタッチドラッグのデフォルトの動作です。</li> 
        <li><strong>[パン</strong>]：ビュー平面内でカメラを移動します。 ターゲットポイントはカメラ対応して移動するので、以降のオービットアクションでは、カメラは新しいターゲットポイントを中心として移動します。パンは、左ボタンドラッグおよびシングルタッチドラッグの代替動作です。</li> 
        </ul> </td> 
      </tr> 
      <tr> 
      <td><p>調査</p> <p>「」または「」</p> <p>ターゲット</p> </td> 
      <td><p>タップまたはクリックして調査モードとターゲットモードを切り替えます。</p> 
        <ul> 
        <li><strong>Examine</strong>-Tapキーを押すか、をクリックしてTargetモードに入ります。</li> 
        <li><strong>Target</strong>- 3Dアセットの任意の場所をタップまたはクリックして、アセットのその部分のビューを中央に配置します。<br />オービットアクションでは、新しいターゲットポイントが使用されます。</li> 
        </ul> </td> 
      </tr> 
      <tr> 
      <td>リセット</td> 
      <td>タップまたはクリックして、視野のターゲットポイントをモデルの中心に戻します。リセットでも、アセット全体を表示したり、適切な表示サイズで表示するために、カメラを近づけたり遠ざけたりします。<br /></td> 
      </tr> 
    </tbody> 
    </table>

1. Near the upper-right corner of the asset details page, tap the **[!UICONTROL Stage Selector]** icon. 3D アセットに適用する背景とライティングを含むステージ名を選択します。

   ![](do-not-localize/chlimage_1-2.png)

   ステージは、3Dモデルが表示される環境背景、地表面、照明を提供します。

   [AEM 3D でのステージの使用](/help/sites-classic-ui-authoring/classicui-stages-aem3d.md)を参照してください。

1. Near the upper-right corner of the asset details page, tap the **[!UICONTROL Camera Selector]** icon, then select a camera view that you want to apply to the 3D asset.

   ![](do-not-localize/chlimage_1-3.png)

   多くの場合、ステージには事前定義済みのカメラが含まれています。現在のカメラを再選択して、事前定義済みの設定に戻すことができます。

   [AEM 3D でのステージの使用](/help/sites-classic-ui-authoring/classicui-stages-aem3d.md)を参照してください。

1. ページの右上隅にある「**[!UICONTROL 保存]**」をタップします。
1. 次のいずれかの操作をおこないます。

   * 3D アセットをレンダリングします。

      [3D アセットのレンダリング](/help/sites-classic-ui-authoring/classicui-rendering-3d.md)を参照してください。

   * ページの右上隅にある「**[!UICONTROL 閉じる]**」をタップして、アセットページに戻ります。

