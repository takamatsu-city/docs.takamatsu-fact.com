[高松市スマートマップ](https://maps.takamatsu-fact.com/)、およびデータAPIを使うと、営利・非営利を問わず、地図と位置情報を活用したウェブサイトやアプリケーションを作ることができます。

## クイックスタート

さっそく地図とデータを表示して、開発を始めましょう。

### 地図を表示する

**HTML**

```
<div id="map"></div>

<script type="text/javascript" src="https://geolonia.github.io/takamatsu-maps-sdk/index.js"></script>
```

**CSS**

```
html, body, #map
{
  width: 100vw;
  height: 100vh;
  margin: 0;
  padding: 0;
}
```

**Javascript**

```
const myCity = new city.Takamatsu.Map();

myCity.on('load', () => {})
```

[Codepen で確認する](https://codepen.io/shinichin/pen/VwGGZyq)

### 高松市のデータを表示する

高松市が[高松市スマートマップ](https://maps.takamatsu-fact.com/)公開しているデータを、地図上に表示できます。

**都市計画情報を表示する**

`loadData` メソッドを使って、地図上に[高松市スマートマップ](https://maps.takamatsu-fact.com/)で公開されているポリゴンデータを表示できます。

```
const myCity = new city.Takamatsu.Map();

myCity.on('load', () => {  
  
  myCity.loadData("商業地域")
    
})
```

* 第一引数には、高松市スマートマップに表示されているデータの `class` 文字列を入れてください。

**施設情報を表示する**

`loadGeoJSON` メソッドを使って、地図上に[高松市スマートマップ](https://maps.takamatsu-fact.com/)で公開されているポイントデータを表示できます。

```
const myCity = new city.Takamatsu.Map();

myCity.on('load', () => {  
  
  myCity.loadGeoJSON("AED設置場所")
    
})
```

### 都市情報APIのデータを取得する

`hogehoge` メソッドを使って、地図上に表示している地物（ポリゴンや点）のデータを取得できます。

```
空間ID SDK か高松市のSDKを利用してデータを取得する簡単な方法を記入する
オンクリックで情報を alert 表示か、console に出すか
```

## カスタマイズする

高松市スマートマップは、Maplibre, Geolonia Maps と互換性があります。詳しいカスタマイズの方法は、[API Reference \| MapLibre GL JS Docs \| MapLibre](https://maplibre.org/maplibre-gl-js-docs/api/) を参照してください。

## ご利用にあたって

「高松スマートマップ」と「高松都市情報API」 は、高松市が公開するサービスです。

市民、民間企業、学術団体が営利目的、非営利目的を問わず無料で利用し、地図と位置情報を活用したウェブサイトやアプリケーションを作ることができます。高松市もこの地図とAPIを利用して、市民向けサービスの開発や業務の合理化を進めています。

この地図で表示・配信されている情報は、国土地理院の「地理院地図」、香川県が公開する「ハザードマップデータ」、OpenStreetMap のデータ等、自由なライセンスで公開された情報をベースに、高松市が保有している地図、位置情報をオープンデータとして公開しているものです。

現在公開している情報は、都市計画にかかわる情報、市の設備情報、防災IoT情報などで、かんたんな記述でみなさんのウェブサイトやアプリの地図上に表示できる他、API での取得もできます。利用方法は、「[高松市スマートマップ 開発者向けドキュメンテーション](https://docs.takamatsu-fact.com)」をお読みください。

本サイトで公開している情報は、地図の精度上誤差や、データの過不足を含んでいます。また、地図の利用目的に応じて、表示項目の取捨選択や地図の見やすさ等を考慮した表現を行っています。地図、及び各種オープンデータにはすべての都市施設が含まれているわけではありません。
システムの利用により発生した直接的又は間接的な損失、損害等についてもいかなる責任を負うものではありません。

ご利用にあたっては、「[高松市オープンデータ利用規約](https://opendata.smartcity-takamatsu.jp/odp/tos/)」に同意の上、ご利用ください。


