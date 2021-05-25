---
title: 文字セットの変更
seo-title: 文字セットの変更
description: 出力ストリームをエンコードするための文字セットを指定できます。文字セットの変更方法について説明します。
seo-description: 出力ストリームをエンコードするための文字セットを指定できます。文字セットの変更方法について説明します。
uuid: ecb0c3ff-368c-4553-80e4-aa35fc15af62
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_output
products: SG_EXPERIENCEMANAGER/6.4/FORMS
discoiquuid: 811b31f8-5465-4fb2-b1f9-513936041771
exl-id: 7961efc6-4b11-423a-871d-7b37e3f36781
source-git-commit: bd94d3949f0117aa3e1c9f0e84f7293a5d6b03b4
workflow-type: tm+mt
source-wordcount: '154'
ht-degree: 96%

---

# 文字セットの変更 {#change-the-character-set}

出力ストリームをエンコードするための文字セットを指定できます。

1. 管理コンソールで、**[!UICONTROL サービス/output]**&#x200B;をクリックします。
1. 「国際化対応」の「文字セット」リストで、文字セットを選択します。この設定は、API 経由で指定される `TransformationFormat` と `PrintFormat` の値によって異なります。リストにない文字セットを指定するには、「カスタム」を選択し、表示されたボックスでエンコーディング値を指定します。

   `TransformationFormat` が PDF か PDF/A である場合、または `PrintFormat` が PCL、PostScript、Zebra Label、IPL、DPL、TPCL、GenericColorPCL または GenericPSLevel3 である場合、特定の文字セットのみがサポートされます。

   文字セットは、有効な正規名で指定する必要があります。デフォルト値は「ISO-8859-1」です。

1. 「**[!UICONTROL 保存]**」をクリックします。
