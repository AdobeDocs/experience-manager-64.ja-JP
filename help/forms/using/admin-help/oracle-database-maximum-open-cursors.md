---
title: Oracle データベースの最大オープンカーソル数のしきい値
seo-title: Oracle database maximum open cursors threshold
description: 「Oracle」でオープンカーソルの最大値を設定する方法について説明します。
seo-description: Learn about configuring a maximum value for open cursors in Oracle.
uuid: c1d20997-f853-4772-b1c6-8cea73221d0a
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_the_aem_forms_database
products: SG_EXPERIENCEMANAGER/6.4/FORMS
discoiquuid: d3565776-1b7d-498c-9840-b17f80170d9b
exl-id: ad14ff27-964f-481f-a8ef-052d9cfb7734
source-git-commit: bd94d3949f0117aa3e1c9f0e84f7293a5d6b03b4
workflow-type: tm+mt
source-wordcount: '84'
ht-degree: 27%

---

# Oracle データベースの最大オープンカーソル数のしきい値 {#oracle-database-maximum-open-cursors-threshold}

oracleのオープンカーソルの最大値を設定するには、アプリケーションに適した数値にこの値を調整する必要がある場合があります。 中程度の負荷では、開いている平均カーソル数は 2700 であることが明らかです。 上限は 3000 にすることをお勧めします。 詳しくは、[https://www.orafaq.com/node/758](https://www.orafaq.com/node/758) を参照してください。
