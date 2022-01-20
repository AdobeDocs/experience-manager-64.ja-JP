---
title: SPA への React コンポーネントの実装
seo-title: Implementing a React Component for SPA
description: この記事では、AEM SPA Editor で動作するように既存のシンプルな React コンポーネントを適応させる方法の例を示します。
seo-description: This article presents an example of how to adapt a simple, existing React component to work with the AEM SPA Editor.
uuid: aebca2ea-a020-45e1-8043-f8c21154c660
contentOwner: bohnert
products: SG_EXPERIENCEMANAGER/6.4/SITES
topic-tags: spa
content-type: reference
discoiquuid: 86a981fe-25f3-451a-b262-8c497619e0ac
exl-id: da0e076b-afb7-4ebe-8e5e-48c00750e453
source-git-commit: bd94d3949f0117aa3e1c9f0e84f7293a5d6b03b4
workflow-type: tm+mt
source-wordcount: '560'
ht-degree: 19%

---

# SPA への React コンポーネントの実装{#implementing-a-react-component-for-spa}

単一ページアプリケーション（SPA）により、Web サイトのユーザーに魅力的なエクスペリエンスを提供することができます。開発者は SPA フレームワークを使用してサイトを構築したいと考え、作成者はそうして構築されたサイトのコンテンツを AEM 内でシームレスに編集したいと考えています。

SPA オーサリング機能には、AEM 内で SPA をサポートするための包括的なソリューションが用意されています。この記事では、AEM SPA Editor で動作するように既存のシンプルな React コンポーネントを適応させる方法の例を示します。

>[!NOTE]
>シングルページアプリケーション (SPA) エディター機能には、AEM 6.4 Service Pack 2 以降が必要です。
>
>SPA Editor は、SPAフレームワークベースのクライアントサイドレンダリング (React やAngularなど ) が必要なプロジェクトで推奨されるソリューションです。

## はじめに {#introduction}

AEMとSPA Editor の間で確立された、シンプルで軽量な契約により、既存の JavaScript アプリケーションを使用してAEMでSPAと共に使用するように適応させることは、簡単なことです。

この記事では、We.Retail ジャーナルのサンプルSPAの天気コンポーネントの例を示します。

詳しくは、 [AEM用SPAアプリケーションの構造](/help/sites-developing/spa-getting-started-react.md) この記事を読む前に。

>[!CAUTION]
>このドキュメントでは、 [We.Retail ジャーナルアプリ](https://github.com/Adobe-Marketing-Cloud/aem-sample-we-retail-journal) デモ目的のみ。 どのプロジェクト作業にも使用しないでください。
>
>AEM プロジェクトでは、 [AEM プロジェクトアーキタイプ](https://docs.adobe.com/content/help/ja-JP/experience-manager-core-components/using/developing/archetype/overview.html)を活用します。このアーキタイプは、React または Angular を使用する SPA プロジェクトをサポートし、SPA SDK を活用します。

## 天気コンポーネント {#the-weather-component}

天気コンポーネントは、We.Retail ジャーナルアプリの左上にあります。 定義した場所の現在の天気が表示され、天候データが動的にプルされます。

### 気象ウィジェットの使用 {#using-the-weather-widget}

![screen_shot_2018-06-08at143224](assets/screen_shot_2018-06-08at143224.png)

SPAエディターでSPAのコンテンツをオーサリングする場合、天気コンポーネントは他のAEMコンポーネントと同様に表示され、ツールバーと共に完成し、編集可能です。

![screen_shot_2018-06-08at143304](assets/screen_shot_2018-06-08at143304.png)

市区町村は、他のAEMコンポーネントと同様に、ダイアログで更新できます。

![screen_shot_2018-06-08at143446](assets/screen_shot_2018-06-08at143446.png)

変更が保持され、コンポーネントは新しい天気データで自動的に更新されます。

![screen_shot_2018-06-08at143524](assets/screen_shot_2018-06-08at143524.png)

### 気象コンポーネントの実装 {#weather-component-implementation}

天候コンポーネントは、実際には、 [React オープンウェザー](https://www.npmjs.com/package/react-open-weather)。We.Retail ジャーナルサンプルSPAアプリケーション内でコンポーネントとして機能するように適応されています。

React Open Weather コンポーネントの使用に関する NPM ドキュメントのスニペットを以下に示します。

![screen_shot_2018-06-08at144723](assets/screen_shot_2018-06-08at144723.png) ![screen_shot_2018-06-08at144215](assets/screen_shot_2018-06-08at144215.png)

カスタマイズされた気象コンポーネントのコード ( `Weather.js`) を We.Retail ジャーナルアプリケーションに追加します。

* **行 16**:React Open Weather ウィジェットは、必要に応じて読み込まれます。
* **行 46**:この `MapTo` 関数は、この React コンポーネントをSPA Editor で編集できるように、対応するAEMコンポーネントに関連付けます。

* **行 22～29**:この `EditConfig` が定義され、市区町村が設定されているかどうかを確認し、空の場合は値を定義します。

* **行 31 ～ 44**:天気コンポーネントは、 `Component` クラスに含まれ、React Open Weather コンポーネントの NPM 使用に関するドキュメントで定義されている必要なデータを提供し、コンポーネントをレンダリングします。

```javascript
/*~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
 ~ Copyright 2018 Adobe Systems Incorporated
 ~
 ~ Licensed under the Apache License, Version 2.0 (the "License");
 ~ you may not use this file except in compliance with the License.
 ~ You may obtain a copy of the License at
 ~
 ~     https://www.apache.org/licenses/LICENSE-2.0
 ~
 ~ Unless required by applicable law or agreed to in writing, software
 ~ distributed under the License is distributed on an "AS IS" BASIS,
 ~ WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
 ~ See the License for the specific language governing permissions and
 ~ limitations under the License.
 ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~*/
import React, {Component} from 'react';
import ReactWeather from 'react-open-weather';
import {MapTo} from '@adobe/aem-react-editable-components';

require('./Weather.css');

const WeatherEditConfig = {

    emptyLabel: 'Weather',

    isEmpty: function() {
        return !this.props || !this.props.cq_model || !this.props.cq_model.city || this.props.cq_model.city.trim().length < 1;
    }
};

class Weather extends Component {

    render() {
        let apiKey = "12345678901234567890";
        let city;

        if (this.props.cq_model) {
            city = this.props.cq_model.city;
            return <ReactWeather key={'react-weather' + Date.now()} forecast="today" apikey={apiKey} type="city" city={city} />
        }

        return null;
    }
}

MapTo('we-retail-journal/global/components/weather')(Weather, WeatherEditConfig);
```

バックエンドコンポーネントが既に存在している必要がありますが、フロントエンド開発者は、コーディングをほとんどおこなわずに We.Retail ジャーナルSPAの React Open Weather コンポーネントを活用できます。

## 次のステップ {#next-step}

SPA for AEMの開発について詳しくは、この記事を参照してください。 [SPA for AEMの開発](/help/sites-developing/spa-architecture.md).
