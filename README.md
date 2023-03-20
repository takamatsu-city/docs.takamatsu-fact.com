# 高松市 スマートシティー地図 & API ドキュメント

高松市が公開するスマートシティー地図は、どなたでも無料でご利用いただけます。

## クイックスタート

以下のソースをコピーして、開発を始めましょう。

### 地図の表示

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

### データの表示

高松市が公開する200種類以上のデータを、地図上に表示します。
データの一覧は、[高松スマートシティ地図](https://map.takamatsu-fact.com/)で確認できます。

**都市計画区分の表示**

`loadData` メソッドを使って、地図上にデータを表示できます。

```
const myCity = new city.Takamatsu.Map();

myCity.on('load', () => {  
  
  myCity.loadData("商業地域")
  
  myCity.loadData('第一種低層住居専用地域', {
    'fill-color': 'purple',
  })
    
})
```

### データの取得

`hogehoge` メソッドを使って、地図上に表示しているデータが取得できます。

```
空間ID SDK か高松市のSDKを利用してデータを取得する簡単な方法を記入する
イメージはオンクリックで情報を alert 表示か、console に出すか？
```

## SDK と API 

SDK のメソッドを並べる

## カスタムデータの追加

独自のデータをGeoJSON、ベクトルタイル形式で表示する方法を並べる。

パイプラインとかにリンクを貼る





---

以下は大きく変更予定

## レスポンス

PBF フォーマットで返却されます。
以下のライブラリ等を使うことでデータは GeoJSON フォーマットに変換できます。

https://github.com/spatial-id/javascript-sdk

### レイヤー

データは GeoJSON の FeatureCollection としてパースされます。
各レイヤーのジオメトリと properties は以下のデータ型を持ちます。

```typescript
// 下水
{
  $geometry: Polygon,
  番号: number,
  処理区名: string,
  決定区域: number,
  計画区域: number,
  計画区域計: number,
  計画人口: number,
  事業区域: number,
  事業人口: number,
  処理面積: number,
  排除方式: string,
  市町名: string | undefined,
  計画面積: number | undefined,
  計画汚水量: number | undefined,
  認可面積: number | undefined,
  認可人口: number | undefined,
  認可汚水量: number | undefined
}
```

```typescript
// 公共施設
{
  $geometry: Point,
  番号: number,
  名称: string,
  所在地: string,
  面積: number,
  決定年月日: string,
  備考: string | null,
  種別: string | undefined,
  計画面積: number | string | undefined,
  供用面積: string | undefined,
  墓園名: string | undefined,
  位置: string | undefined,
  緑地名: string | undefined,
  開設: string | undefined,
  駅名: string | undefined,
  鉄道名: string | undefined,
  路線名: string | undefined,
  駐車場名: string | undefined,
  構造: string | null | undefined,
  収容台数: number | undefined,
  供用年月日: string | undefined
}
```

```typescript
// 土地区画整理事業
{
  $geometry: Polygon,
  番号: number,
  施行主体: string,
  地区名: string,
  施行者: string,
  施行面積: string,
  総事業費: number,
  決定年月日: string,
  告示年月日: string,
  施行期間: string,
  公告年月日: string,
  減歩率公共: string,
  用地率: string
}
```

```typescript
// 地区計画
{
  $geometry: Polygon,
  番号: number,
  名称: string,
  区域面積: number,
  地区施設: string,
  決定年月日: string,
  備考: string
}
```

```typescript
// 地番図
{
  $geometry: Polygon,
  照合キー: string,
  市町村CD: string,
  大字CD: string,
  小字CD: null | undefined,
  市町村名: string,
  大字名: string | null,
  小字名: null | undefined,
  地番1: string,
  地番2: string | null,
  地番3: string | null | undefined,
  地番4: null | undefined,
  地番X: null | undefined,
  表示文字列: string
}
```

```typescript
// 地籍図
{
  $geometry: Polygon,
  照合キー: string,
  市町村CD: string,
  大字CD: string,
  小字CD: null | undefined,
  市町村名: string,
  大字名: string | null,
  小字名: null | undefined,
  地番1: string,
  地番2: string | null,
  地番3: null | undefined,
  地番4: null | undefined,
  地番X: null | undefined,
  表示文字列: string
}
```

```typescript
// 市街地再開発事業
{
  $geometry: Polygon,
  番号: number,
  名称: string,
  施行区域: number,
  建築敷地: number,
  建ぺい率: string,
  容積率: string,
  主要用途: string,
  公共施設: string,
  決定年月日: string
}
```

```typescript
// 河川
{
  $geometry: Polygon,
  番号: number,
  管理番号: number,
  河川名称: string
}
```

```typescript
// 特別用途地区
{
  $geometry: Polygon,
  番号: number,
  地区名: string,
  備考: string
}
```

```typescript
// 緑地
{
  $geometry: Polygon,
  番号: number,
  緑地名: string,
  位置: string,
  計画面積: string,
  供用面積: string,
  決定年月日: string
}
```

```typescript
// 臨港地区
{
  $geometry: Polygon,
  番号: number,
  区域名: string,
  地区名: string,
  面積: string,
  商: string,
  工業: string,
  鉄道連絡: string,
  保安: string,
  特殊貨物: string,
  マリーナ: string,
  指定なし: string,
  決定年月日: string
}
```

```typescript
// 都市公園
{
  $geometry: Polygon,
  番号: number,
  種別: string,
  名称: string,
  位置: string | null,
  供用面積: string | null,
  区分コード: number | null | undefined,
  規模コード: number | null | undefined,
  公園番号: string | null | undefined,
  公園名称: string | undefined,
  計画面積: string | null | undefined,
  決定年月日: string | null | undefined,
  備考: string | null | undefined
}
```

```typescript
// 都市再生特別地区
{
  $geometry: Polygon,
  番号: number,
  種類: string,
  容積率最高: string,
  容積率最低: string,
  建ぺい最高: string,
  高さ最高: string,
  壁面制限: string,
  注意事項１: string,
  注意事項２: string,
  注意事項３: string | null,
  注意事項４: string
}
```

```typescript
// 都市計画
{
  $geometry: Polygon,
  番号: number,
  種類名: string,
  建ぺい率: string | number,
  容積率: string | number,
  高さ制限: string,
  用途の概要: string | undefined,
  許可面積: string | undefined,
  敷地規模: number | undefined,
  屋根不燃等: string | undefined,
  日影規制: string | undefined,
  備考: string | undefined,
  LAYER: number | undefined,
  LINETYPE: number | undefined,
  用途名: string | undefined,
  種類: string | undefined,
  面積: number | undefined,
  容積最高A: string | undefined,
  建最高A: string | undefined,
  容積最低A: string | undefined,
  建最低A: string | undefined,
  容積最高B: null | undefined,
  建最高B: null | undefined,
  容積最低B: null | undefined,
  建最低B: null | undefined,
  決定年月日: string | undefined,
  注意事項１: string | undefined,
  注意事項２: null | undefined
}
```

```typescript
// 都市計画・防火
{
  $geometry: Polygon,
  番号: number,
  地区名: string,
  防火地域: number,
  準防火地域: number,
  合計: number,
  決定年月日: string,
  備考: string
}
```

```typescript
// 都市計画道路
{
  $geometry: Polygon,
  番号: number,
  区分コード: number | null,
  規模コード: number | null,
  路線番号: string | null,
  路線名称: string | null,
  起点: string | null,
  終点: string | null,
  車線の数: number | null,
  代表幅員: string | null,
  延長: number | null,
  決定年月日: string | null
}
```

```typescript
// 都市高速鉄道
{
  $geometry: Polygon,
  番号: number,
  名称: string,
  位置・起点: string,
  位置・終点: string,
  主な経過地: string,
  区域延長: number,
  構造: string,
  起点(1): string,
  終点(1): string,
  経過地(1): string,
  延長(1): number,
  構造(1): string,
  延長(2): number,
  備考(2): string,
  含まれる駅: string,
  決定年月日: string
}
```

```typescript
// 風致地区
{
  $geometry: Polygon,
  番号: number,
  名称: string,
  面積: number,
  決定年月日: string,
  位置: string
}
```

```typescript
// 駐車場・駐輪場整備地区
{
  $geometry: Polygon,
  番号: number,
  区域名: string,
  面積(当初): string,
  面積(変更): string,
  決定年月日: string | null,
  備考: string | null,
  名称: string | undefined
}
```

