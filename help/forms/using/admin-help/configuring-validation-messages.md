---
title: 検証メッセージの設定
seo-title: Configuring validation messages
description: 検証メッセージの表示方法と、Web ブラウザーで返されるフォームを基準とした位置を指定する方法について説明します。
seo-description: Learn how to specify how validation messages are displayed and their location relative to the form returned in the web browser.
uuid: f6bff4fa-f90f-4135-ae40-7ab3d3613122
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_forms
products: SG_EXPERIENCEMANAGER/6.4/FORMS
discoiquuid: 5f2f8129-e45e-4f3f-ae30-c09330d0e152
exl-id: 2016ac85-12a1-42cb-bc03-fced94947010
source-git-commit: bd94d3949f0117aa3e1c9f0e84f7293a5d6b03b4
workflow-type: tm+mt
source-wordcount: '350'
ht-degree: 4%

---

# 検証メッセージの設定 {#configuring-validation-messages}

HTMLとしてレンダリングされるフォームの場合、発生したフォーム検証エラーがユーザーに対して表示されます。 検証メッセージの表示方法をカスタマイズできます。 検証メッセージが表示される場所に応じて、フォーム内のメッセージの位置とフレーム境界のサイズを制御することもできます。

## 検証メッセージの表示方法の指定 {#specify-how-validation-messages-are-displayed}

1. 管理コンソールで、サービス/Forms をクリックします。
1. 「検証出力」の「レポート」リストで、次のいずれかのオプションを選択します。

   **メッセージボックス：** 検証メッセージを別のダイアログボックスに表示するには

   **フレーム：** 同じウィンドウのフレーム内に検証メッセージを表示する。

   **フレームなし：** 検証メッセージを同じウィンドウに表示する。 この値がデフォルトです。

   **API 経由（データを含む）:** API を使用して（データと共に）検証メッセージを返す場合。 検証メッセージは、画面には表示されません。

   **API 経由（フォームを含む）:** 検証メッセージを API（フォームと共に）で返す場合。 検証メッセージは、画面には表示されません。

   **なし：** 検証メッセージを表示しない場合。

1. 「保存」をクリックします。

## Web ブラウザーで返されるフォームを基準とした検証メッセージの場所の指定 {#specify-the-location-of-validation-messages-relative-to-the-form-returned-in-the-web-browser}

[ レポート ] が [ フレーム ] または [ フレームなし ] に設定されている場合は、検証メッセージの場所を指定できます。

1. [ 検証出力 ] の [ 位置 ] リストで、次のいずれかのオプションを選択します。

   **左：** 検証メッセージを Web ブラウザーの左側に表示する。

   **右：** 検証メッセージを Web ブラウザーの右側に表示する。

   **上**:検証メッセージを Web ブラウザーの上部に表示する。 この値がデフォルトです。

   **下**:検証メッセージを Web ブラウザーの下部に表示する。

1. 「保存」をクリックします。

## フレーム境界のサイズを指定 {#specify-the-frame-border-size}

[ レポート ] が [ フレーム ] に設定されている場合は、フレーム枠のサイズを指定できます。

1. 「検証出力」の「境界線のサイズ」ボックスに、フレーム境界のサイズをピクセル単位で入力します。

   境界線のサイズは 0 以上にする必要があります。 デフォルト値は 1 です。

1. 「保存」をクリックします。
