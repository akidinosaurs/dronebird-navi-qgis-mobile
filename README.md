# DroneBird Navi QGIS Mobile

**DroneBird Navi QGIS Mobile** は、OpenAerialMap に公開されたドローンオルソ画像を、スマホ上で追加・重ね合わせ・確認できる現場向けミニ GIS です。

QGIS の「レイヤー追加」「表示 ON/OFF」「透明度調整」「順序変更」「ズーム」「削除」といった基本操作を、iOS Safari でも使いやすい Web アプリとして再設計しました。

## Demo

GitHub Pages 公開後の URL をここに記載します。

```text
https://akidinosaurs.github.io/dronebird-navi-qgis-mobile/
```

## 背景

ドローンで撮影した画像は、OpenDroneMap / WebODM などでオルソ画像化し、OpenAerialMap に公開できます。  
しかし、公開後に現場や自治体、学生が実際に使うには、XYZ タイル URL の取得、GIS への追加、レイヤー管理、ハザード情報との重ね合わせが必要になります。

既存の WebGIS は便利ですが、ドローン現場で使うには操作が重く、特にスマホでは外部タイル追加やレイヤー管理が難しい場面があります。

そこで本アプリでは、**OpenAerialMap の公開オルソ画像をスマホで扱える現場用ミニ GIS** として設計しました。

1. 問題点はなにか
OAMに公開しても現場で即使えるわけではない
既存GISは高機能だが、ドローン現場では操作が重い
防災訓練ではオルソ単体ではなく、ハザード・地形・避難所との重ね合わせが必要
2. それをどのように解決したか
QGIS風のレイヤー管理をスマホWebに移植
OAM URL / ID からオルソ画像を追加
XYZ / TMS タイルを直接追加可能
洪水、傾斜、陰影、避難所サンプルをプリセット化
GeoJSON追加に対応
iOS Safariでも使える静的Webアプリとして設計
3. これが足りなかった
OAM API連携の安定化
DIPSやNOTAMなど公式な飛行可否判定
地域別ハザードマップとの本格連携
オフライン対応
レイヤー検索、凡例、サムネイル、履歴管理などのUI強化

## 主な機能

### OpenAerialMap 連携

- OAM URL / Image ID からオルソ画像を追加
- OAM API 取得を試行
- 横瀬小学校データはフォールバック XYZ タイルを内蔵
- OAM の XYZ / TMS タイルを直接追加可能

### QGIS 風レイヤーパネル

- レイヤー表示 ON/OFF
- 透明度調整
- レイヤー順序の上下移動
- レイヤー範囲へズーム
- レイヤー情報表示
- URL / 情報コピー
- レイヤー削除

### レイヤー追加

- OpenAerialMap URL / ID
- XYZ / TMS タイル URL
- GeoJSON URL
- GeoJSON 直接貼り付け
- GeoJSON ファイル読み込み

### 防災・地形レイヤー

- GSI 標準地図
- GSI 淡色地図
- 洪水浸水想定区域
- 傾斜量図
- 陰影起伏図
- 避難所サンプル GeoJSON

### 現場向け機能

- 現在地表示
- 地図クリックによる座標表示
- 座標コピー
- 距離計測
- 全レイヤー範囲表示
- プロジェクト保存 / 復元
- JSON エクスポート / インポート

## 使い方

### 1. OpenAerialMap の URL を貼る

例：

```text
https://map.openaerialmap.org/#/-18.632,18.47900000000001,3/latest/6a374d65339a46ab3a85936f
```

「OAMから追加」を押すと、OAM API からタイル URL と bbox の取得を試します。  
取得に失敗した場合でも、登録済みの横瀬データは内蔵フォールバックで表示できます。

### 2. XYZ タイルを追加する

```text
https://tiles.openaerialmap.org/.../{z}/{x}/{y}
```

QGIS の XYZ タイル追加と同じ考え方で、`{z}/{x}/{y}` を含む URL を追加できます。

### 3. GeoJSON を追加する

避難所、被害箇所、調査メモ、現地確認ポイントなどを GeoJSON として追加できます。

## 創意工夫のポイント

詳しくは [`docs/CREATIVE_POINTS.md`](docs/CREATIVE_POINTS.md) を参照してください。

要点は次の通りです。

1. **QGIS の基本機能をスマホ Web に移植**  
   単なる地図ビューアではなく、レイヤー追加・管理・透明度・順序変更を実装しました。

2. **OpenAerialMap 公開後の“使いにくさ”を解消**  
   OAM に公開したドローンオルソを、URL から直接現場で扱えるようにしました。

3. **防災現場を想定したレイヤー構成**  
   オルソ画像、洪水、傾斜、陰影、避難所を重ねて、現場判断に使える構成にしました。

4. **iOS Safari の制約内で最大限実装**  
   アプリインストール不要、静的 HTML、localStorage 保存、ファイル読み込み対応にしました。

5. **ひなたGISやQGISの代替ではなく、現場補助に特化**  
   汎用 GIS ではなく、ドローン現場で「今見る・重ねる・判断する」ことに絞りました。

## 技術構成

- MapLibre GL JS
- OpenAerialMap API / XYZ Tile
- GSI Tiles
- GeoJSON
- HTML / CSS / JavaScript
- GitHub Pages

## ファイル構成

```text
.
├── index.html
├── README.md
├── .nojekyll
├── docs
│   ├── CREATIVE_POINTS.md
│   └── SETUP_GITHUB_PAGES.md
└── LICENSE
```

## GitHub Pages 公開方法

1. GitHub で `dronebird-navi-qgis-mobile` という public repository を作成
2. このリポジトリ一式をアップロード
3. `Settings > Pages`
4. Source を `Deploy from a branch`
5. Branch を `main` / `/root` に設定
6. 数分後に以下で公開

```text
https://akidinosaurs.github.io/dronebird-navi-qgis-mobile/
```

詳細は [`docs/SETUP_GITHUB_PAGES.md`](docs/SETUP_GITHUB_PAGES.md) を参照してください。

## 注意事項

- 本アプリは公式な飛行可否判定ツールではありません。
- 実飛行では DIPS2.0、NOTAM、土地管理者、自治体資料を必ず確認してください。
- iOS Safari では、現在地取得、ローカル保存、ファイル入出力、ダウンロード挙動が端末設定や HTTPS 環境に依存します。
- OAM API はレスポンス形式や CORS 状況により取得できない場合があるため、XYZ タイルの直接追加も併用できる設計にしています。

## License

MIT
