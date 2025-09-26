## 物件標記 APP

使用手機相機拍攝、偵測、裁切與標記物件，並將結果上傳至雲端保存與後續應用。

<p float="left">
  <img src="../../blob/main/2.jpg?raw=true" width="250" alt="偵測結果畫面" />
  <img src="../../blob/main/5.jpg?raw=true" width="250" alt="裁切特寫" /> 
  <img src="../../blob/main/3.jpg?raw=true" width="250" alt="標記輸入" />
  <img src="../../blob/main/1.jpg?raw=true" width="250" alt="相機拍攝" />
  <img src="../../blob/main/4.jpg?raw=true" width="250" alt="上傳完成" />
</p>

### 功能特色

- **拍攝與偵測**: 使用手機相機拍攝，內建模型自動偵測照片中的物件並框選。
- **自動裁切**: 依每個偵測到的物件自動裁切產生特寫影像。
- **標籤管理**: 每個物件可輸入 1–3 個自訂標籤。
- **雲端儲存**: 影像與標記一鍵上傳至雲端，便於管理與後續使用。

### 技術與套件

- [ML Kit](https://developers.google.com/ml-kit): 物件偵測與框選
- [Firebase Storage](https://firebase.google.com/docs/storage): 圖片儲存
- [Firebase Realtime Database](https://firebase.google.com/docs/database): 標記資料儲存與同步

### 運作流程

1. 拍攝照片
2. 模型偵測並產生邊界框
3. 依物件自動裁切出特寫
4. 使用者輸入 1–3 個標籤
5. 上傳至雲端（圖片存入 Storage、標記寫入 Realtime Database）

### 資料結構

- **圖片**: 以 JPEG 格式儲存於 Firebase Storage，檔名格式為 `JPEG_日期_時間`，例如 `JPEG_20201009_141200`。
- **標記**: 以 JSON 格式儲存於 Firebase Realtime Database，結構如下。

欄位說明:

```json
"<物件隨機ID(英數混合)>": {
  "bottom": "物件框底部 y 軸數值 (int)",
  "label1": "標籤 1 (string)",
  "label2": "標籤 2 (string)",
  "label3": "標籤 3 (string)",
  "left": "物件框左側 x 軸數值 (int)",
  "right": "物件框右側 x 軸數值 (int)",
  "top": "物件框頂部 y 軸數值 (int)",
  "uid": "該物件對應照片檔名 (string)"
}
```

儲存範例:

```json
"-MlJ27Vsisfl9O9TcNfY": {
  "bottom": "2990",
  "label1": "鍵盤",
  "label2": "",
  "label3": "",
  "left": "213",
  "right": "1159",
  "top": "2040",
  "uid": "0"
}
```

### 安裝與執行（簡述）

- 需求: Android Studio、具備網路的 Android 裝置
- Firebase 設定: 建立專案並啟用 Storage 與 Realtime Database，下載 `google-services.json` 放置於 `app/`
- 專案: 匯入專案後同步 Gradle，連接實機即可執行

> 註: 以上為概要步驟；實際設定請依專案中的 Firebase/ML Kit 設定檔與程式碼為準。

### 展示影片

- [YouTube 連結](https://youtu.be/3dlyRlCIImk)

### 待辦與規劃

- [ ] 螢幕手動框選（含縮放）
- [ ] 標記格式遵循標準（COCO 格式）
- [ ] 同步帳號接續標記（同步照片並套用歷史標記）
- [ ] 可手動增加標記項目數量
- [ ] beta 版上架 Google Play 商店
