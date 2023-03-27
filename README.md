# 高松市スマートマップ & API ドキュメント

高松市スマートマップは、どなたでも無料でご利用いただけます。

## クイックスタート

以下のソースをコピーして、開発を始めましょう。

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

[Codepen で触ってみよう！](https://codepen.io/shinichin/pen/VwGGZyq)

### 高松市のデータを表示する

高松市が公開する200種類以上のデータを、地図上に表示します。
データの一覧は、[高松スマートシティ地図](https://map.takamatsu-fact.com/)で確認できます。

**都市計画情報を表示する**

`loadData` メソッドを使って、地図上に[高松市スマートマップ](https://maps.takamatsu-fact.com/)で公開されているポリゴンデータを表示できます。

```
const myCity = new city.Takamatsu.Map();

myCity.on('load', () => {  
  
  myCity.loadData("商業地域")
  
  myCity.loadData('第一種低層住居専用地域', {
    'fill-color': 'purple',
  })
    
})
```

**施設情報を表示する**

`loadData` メソッドを使って、地図上に[高松市スマートマップ](https://maps.takamatsu-fact.com/)で公開されているポイントデータを表示できます。

```
const myCity = new city.Takamatsu.Map();

myCity.on('load', () => {  
  
  myCity.loadGeoJSON("AED設置場所")
    
})
```


### 都市情報APIのデータを取得する

`hogehoge` メソッドを使って、地図上に表示しているデータが取得できます。

```
空間ID SDK か高松市のSDKを利用してデータを取得する簡単な方法を記入する
イメージはオンクリックで情報を alert 表示か、console に出すか？
```

### カスタムデータを表示する

```
myCity.loadData("GeoJSON/vectortile のURL")
```

CSV から GeoJSON を作成し、GitHub Pages にホストするためには、[geoloniamaps/geojson\-api: CSV フォーマットのデータを GitHub Actions で GeoJSON に変換し API として公開するためのテンプレートリポジトリです。](https://github.com/geoloniamaps/geojson-api)をご利用いただけます。

## SDK の詳細

基本的なメソッドをいくつか並べる

## カスタマイズ

Maplibre, Geolonia いずれかのドキュメンテーションサイトにリンクを貼る
