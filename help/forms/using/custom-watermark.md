---
title: レター PDF プレビューのカスタム透かし
seo-title: Custom watermark in letter PDF preview
description: レター PDF プレビューのカスタム透かしの作成方法について説明します。
seo-description: Learn how to create custom watermark in letter PDF preview.
uuid: f406de81-af94-40dd-97ec-9ca95620f961
content-type: reference
products: SG_EXPERIENCEMANAGER/6.4/FORMS
topic-tags: correspondence-management
discoiquuid: a09e2c83-083d-427a-8336-0567e00c5712
feature: Correspondence Management
exl-id: 8aeabd95-948d-4a54-b593-1eda8ddd731b
source-git-commit: bd94d3949f0117aa3e1c9f0e84f7293a5d6b03b4
workflow-type: tm+mt
source-wordcount: '335'
ht-degree: 57%

---

# レター PDF プレビューのカスタム透かし {#custom-watermark-in-letter-pdf-preview}

## 概要 {#overview}

Create Correspondence UI を使用するエージェントユーザーは、電子メールや印刷などを後処理に送信する最終的形態で表示します。

PDF データの不正使用を防ぐため、プレビューの PDF に透かしを付けることができます。デフォルトのウォーターマークは「プレビュー」で、PDF 全体に表示されます。

プレビューの透かしを有効にするには、「PDF」で **[!UICONTROL 透かしを適用]** の「プレビュー中」オプション **[!UICONTROL Correspondence Management 設定]** 時刻 `https://[server]:[port]/system/console/configMgr`.

![default-watermark](assets/default-watermark.png)

透かしのテキストと外観をカスタマイズするには、次の手順を実行します。

## Create Correspondence UI で PDF プレビュー内の透かしをカスタマイズする {#customizewatermark-}

1. に移動します。 `https://[server]:[port]/[ContextPath]/crx/de` 管理者としてログインします。
1. apps フォルダーに、 **[!UICONTROL previewwatermark]** libs フォルダー内の previewwatermark フォルダーに似たパス/構造を持つ

   1. 次のパスにある**previewwatermark **フォルダを右クリックし、「 **ノードをオーバーレイ**:

      `/libs/fd/cm/configFiles/previewwatermark`

   1. ノードをオーバーレイダイアログに次の値が表示されていることを確認します。

      **パス：** /libs/fd/cm/configFiles/previewwatermark

      **オーバーレイの場所：** /apps/

      **ノードタイプを一致させる：** 確認済み

      >[!NOTE]
      >
      >/libs ブランチでは変更を加えないでください。 次の操作を行った場合はこのブランチが変更されるため、各自で加えた変更はすべて失われます。
      >
      >* インスタンス上でのアップグレード
      >* ホットフィックスの適用
      >* 機能パックのインストール


   1. 「**OK**」をクリックし、「**すべて保存**」をクリックします。この **[!UICONTROL previewwatermark]** 指定されたパスにフォルダーが作成されます。

1. ddx ファイルを「/libs/fd/cm/configFiles/previewwatermark」フォルダから「/apps/fd/cm/configFiles/previewwatermark」フォルダにコピー&amp;ペーストし、をクリックします。 **[!UICONTROL すべて保存]**.
1. ddx ファイルは /apps/fd/cm/configFiles/previewwatermark/ から必要に応じて変更します。

   ```
   <DDX xmlns="https://ns.adobe.com/DDX/1.0/">
    <PDF result="output.pdf">
     <PDF source="input.pdf"/>
           <Watermark opacity="15%" rotation="45">
            <StyledText>
                     <p font-family="Georgia" font-size="70pt" color="black" font-weight="bold">
                         PREVIEW
                    </p>
            </StyledText>
           </Watermark>
    </PDF>
   </DDX>
   ```

   透かしの外観、テキスト、配置のカスタマイズについては、「透かしや背景の追加と削除」を参照してください。 [Assembler サービスと DDX リファレンス](https://help.adobe.com/en_US/livecycle/11.0/ddxRef.pdf) 文書。

   >[!NOTE]
   >
   >ddx ファイルでは、結果と入力への参照を output.pdf および input.pdf から変化させません。ddx ファイルの名前も変更しません。

1. 「**すべて保存**」をクリックします。
