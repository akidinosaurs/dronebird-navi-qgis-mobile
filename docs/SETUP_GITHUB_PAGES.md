# GitHub Pages 公開手順

## 1. リポジトリを作成

GitHub で以下の名前の public repository を作成します。

```text
dronebird-navi-qgis-mobile
```

推奨 URL:

```text
https://github.com/akidinosaurs/dronebird-navi-qgis-mobile
```

## 2. ファイルをアップロード

このフォルダ内のファイルをすべて repository の root にアップロードします。

必要ファイル:

```text
index.html
README.md
.nojekyll
docs/CREATIVE_POINTS.md
docs/SETUP_GITHUB_PAGES.md
LICENSE
```

## 3. GitHub Pages を有効化

1. Repository の `Settings`
2. 左メニューの `Pages`
3. Source: `Deploy from a branch`
4. Branch: `main`
5. Folder: `/root`
6. Save

## 4. 公開 URL

数分後、以下で公開されます。

```text
https://akidinosaurs.github.io/dronebird-navi-qgis-mobile/
```

## 5. Git コマンドでアップロードする場合

```bash
git clone https://github.com/akidinosaurs/dronebird-navi-qgis-mobile.git
cd dronebird-navi-qgis-mobile

# このフォルダの中身をコピー
git add .
git commit -m "Add DroneBird Navi QGIS Mobile"
git push origin main
```
