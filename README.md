# 目力練功房

給遠視／弱視孩子的近距離精細目力訓練小遊戲。純靜態網頁，沒有相依套件、沒有後端、沒有任何資料上傳。

**線上版：https://graylightai.github.io/eye-gym/**

手機用 Safari 或 Chrome 開，「分享 → 加入主畫面」就會變成全螢幕、鎖直板的 app，沒有網址列。

## 檔案

```
index.html      整個 app（HTML + CSS + JS 都在裡面）
img/            53 張遊戲圖案 + eyes.png（app 圖示）
manifest.json   PWA 設定，已鎖直板 portrait
```

## 本機打開

直接用瀏覽器開 `index.html` 就能玩。唯一差別：`file://` 下 canvas 會被瀏覽器視為跨來源，讀不到圖案的透明遮罩，「三個一組」的點擊判定會退回方框判定（點起來比較不精準）。要完整效果就起一個本機伺服器：

```
cd 目力練功房 && python3 -m http.server 8000
# 開 http://localhost:8000
```

## 做成 app

這個資料夾可以直接丟進 Capacitor（`npx cap add ios` / `android`）或當 PWA 掛到任何靜態主機。`manifest.json` 已經設好 `"orientation": "portrait"`；用 Capacitor 的話 iOS 要在 Xcode 的 Deployment Info 取消勾選橫向，Android 在 `AndroidManifest.xml` 的 activity 加 `android:screenOrientation="portrait"`。

## 圖案授權

`img/` 裡的圖案來自 Google [Noto Emoji](https://github.com/googlefonts/noto-emoji)，採 **Apache License 2.0**，可以商用。上架前把 Apache-2.0 的 NOTICE 放進 app 的授權聲明頁即可。

要換圖：把 PNG（建議 128×128、去背）丟進 `img/`，然後在 `index.html` 的 `SPRITES` 陣列加一筆 `['檔名', '中文名']`。陣列是由易到難排序的——前面放輪廓差很多的，後面放容易看錯的，因為精細度越高才會用到越後面的圖案。

## 醫療上的定位

這是輔助練習，不是治療，不能取代回診。**一定要戴著矯正眼鏡做**；遮眼側別與每日時間請照眼科醫師指示。
