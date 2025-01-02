# 海洋生物互動網站  

## 介紹  
本網站透過互動式展示介紹各種海洋生物，結合最新技術提供生動有趣的學習體驗。係於逢甲大學就讀時與組員共同開發之專案，因此命為「逢甲海洋生物博物館網站」，故僅供教學參考用。


## 功能特色  
- **付款系統**  
  - 支援 **LINEPAY**（沙盒模式）進行付款流程測試與模擬。  
- **生物辨識功能**  
  - 整合 **Google Cloud Vision** 提供圖片辨識與分析服務，用於識別海洋生物。  
- **互動式展示**  
  - 提供圖片與影片，生動呈現海洋生物資訊。  
- **響應式設計**  
  - 支援手機、平板與電腦裝置，提供一致的使用體驗。  


## 技術架構  
| 種類      | 技術名稱                   | 說明                                                                      |
|-----------|----------------------------|---------------------------------------------------------------------------|
| 前端      | Vue.js、CSS、Bootstrap     | 網站介面展示與互動設計，響應式適配各種裝置與螢幕尺寸。                     |
| 後端      | Node.js、Express           | 提供伺服器邏輯與 API 開發。                                               |
| 資料庫    | MongoDB                    | 儲存與管理網站資料，支援快速查詢與操作功能。                              |

---

## 簡報(Canva)  
[逢甲海生館](https://www.canva.com/design/DAGZ5yLzd6s/zfIzUUiJ_EHXlqoGw9Xw3g/edit?utm_content=DAGZ5yLzd6s&utm_campaign=designshare&utm_medium=link2&utm_source=sharebutton)



# 環境設定與安裝
### Project Setup

```sh
npm install
```

### Compile and Hot-Reload for Development

```sh
npm run dev
```

### Compile and Minify for Production

```sh
npm run build
```
