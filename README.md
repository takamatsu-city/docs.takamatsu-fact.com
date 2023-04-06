[高松市スマートマップ](https://maps.takamatsu-fact.com/)、およびデータAPIを使うと、営利・非営利を問わず、地図と位置情報を活用したウェブサイトやアプリケーションを作ることができます。

## クイックスタート

地図とデータを表示して、開発を始めましょう。

### 地図を表示する

**HTML**

```
<div id="map"></div>

<script type="text/javascript" src="https://city.geolonia.com/v1/kagawa/takamatsu/api.js"></script>
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
```

[Codepen で確認する](https://codepen.io/geolonia/pen/abaeMxg)

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

地図上に[高松市スマートマップ](https://maps.takamatsu-fact.com/)で公開されているポイントデータを表示できます。

まずは、[高松市オープンデータ一覧](https://github.com/takamatsu-city/opendata/#%E9%AB%98%E6%9D%BE%E5%B8%82%E3%82%AA%E3%83%BC%E3%83%97%E3%83%B3%E3%83%87%E3%83%BC%E3%82%BF) から表示したいデータを選びます。この例では、 `AED設置場所` を使います。

データ名列が「AED設置場所(0002)」の行、「GeoJSON」のリンク先をコピーします。

```
const myCity = new city.Takamatsu.Map();

myCity.on('load', () => {
  // まず、GeoJSONデータを読み込みます。
  fetch("https://opendata.takamatsu-fact.com/aed_location/data.geojson")
    .then((data) => data.json())
    .then((data) => {
      // GeoJSONのデータを地図に追加します。
      myCity.addSource('aed_location', {
        type: 'geojson',
        data: data,
      });

      // 次は、GeoJSONデータを表示させるための地図レイヤーを追加します。
      myCity.addLayer({
        id: 'aed_location_points',
        source: 'aed_location', // ←こちらは addSource の第一引数 'aed_location' と紐づけるための値です
        type: "circle",
        paint: {
          'circle-radius': 7,
          'circle-color': 'white',
          'circle-opacity': .8,
          'circle-stroke-width': 1,
          'circle-stroke-color': 'gray',
          'circle-stroke-opacity': 1,
        },
      });
    });
});
```

スタイルの設定は、 `addLayer` の `paint` 設定を使います。詳しくは、 [MapLibre GL JS のドキュメンテーション](https://maplibre.org/maplibre-gl-js-docs/style-spec/layers/#circle) を確認してください。


### 都市情報APIのデータを取得する

以下のように地図上に表示している地物（ポリゴンや点）のデータを取得できます。

```
const myCity = new city.Takamatsu.Map();

myCity.on("load", () => {
  myCity.loadData("商業地域");

  myCity.on("click", (e) => {
    const features = myCity.queryRenderedFeatures(e.point, {
      layers: ["商業地域"]
    });
    console.log(features.map(feature => feature.properties));
  });
});
```

![スクリーンショット 2023-04-05 16 00 56](https://user-images.githubusercontent.com/1124652/230005265-a76886d8-b38e-454a-89fb-461c4fa6560f.png)
[Codepen で触ってみる](https://codepen.io/geolonia/pen/yLxmwrx)

## カスタマイズする

高松市スマートマップは、Maplibre, Geolonia Maps と互換性があります。詳しいカスタマイズの方法は、[API Reference \| MapLibre GL JS Docs \| MapLibre](https://maplibre.org/maplibre-gl-js-docs/api/) を参照してください。

## 「高松市スマートマップ」と「高松都市情報API」 について

「高松市スマートマップ」と「高松都市情報API」 は、高松市が公開するサービスです。

市民、民間企業、学術団体が営利目的、非営利目的を問わず無料で利用し、地図と位置情報を活用したウェブサイトやアプリケーションを作ることができます。高松市もこの地図とAPIを利用して、市民向けサービスの開発や業務の合理化を進めています。

この地図で表示・配信されている情報は、国土地理院の「地理院地図」、香川県が公開する「ハザードマップデータ」、OpenStreetMapのデータ等、自由なライセンスで公開された情報をベースに、高松市が保有している地図、位置情報をオープンデータとして公開しているものです。

現在公開している情報は、都市計画にかかわる情報、市の設備施設情報、防災IoT情報などで、かんたんな記述でみなさんのウェブサイトやアプリの地図上に表示できる他、API
での取得もできます。利用方法は、「高松市スマートマップ 開発者向けドキュメンテーション」をお読みください。

## ご利用にあたって

本サイトで公開している情報は、地図の精度上誤差を含んでいます。また、地図の利用目的に応じて、表示項目の取捨選択や地図の見やすさ等を考慮した表現を行っています。都市計画情報のうち、都市施設においては、都市計画決定した一部を掲載しているため、詳細については担当課（都市計画課）までお問合せください。
システムの利用により発生した直接的又は間接的な損失、損害等についてもいかなる責任を負うものではありません。

ご利用にあたっては、「[高松市オープンデータ利用規約](https://opendata.smartcity-takamatsu.jp/odp/tos/)」に同意の上、ご利用ください。
