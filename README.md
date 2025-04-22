# PDF 檔案檢視器

一個簡單易用的網頁式 PDF 檢視器，可以選擇資料夾並瀏覽其中的所有 PDF 檔案。

## 功能特點

- ✅ 選擇資料夾載入多個 PDF 檔案
- ✅ 下拉選單切換不同 PDF 檔案
- ✅ 即時預覽 PDF 內容
- ✅ 支援大型 PDF 檔案

## 安裝步驟

### 1. 複製專案
```bash
git clone <repository-url>
cd pdf-viewer
```

### 2. 安裝依賴
```bash
npm install
```

### 3. 安裝 PM2（生產環境）
```bash
npm install -g pm2
```

### 4. 啟動伺服器

#### 開發環境
```bash
node server.js
```

#### 生產環境（使用 PM2）
```bash
pm2 start server.js --name "pdf-viewer"
pm2 save
pm2 startup  # 設定開機自動啟動
```

## 專案結構
```
pdf-viewer/
├── node_modules/
├── public/
│   └── index.html
├── server.js
├── package.json
└── README.md
```

## 使用方法

1. 啟動伺服器後，開啟瀏覽器訪問 `http://localhost:3000`
2. 點擊「選擇資料夾」按鈕
3. 選擇包含 PDF 檔案的資料夾
4. 從下拉選單選擇要檢視的 PDF 檔案
5. PDF 將在下方區域顯示

## 技術架構

- **前端**: 純 HTML5 + CSS3 + JavaScript
- **後端**: Node.js + Express
- **PDF 處理**: 原生 HTML5 iframe 支援

## 系統需求

- Node.js 14.x 或更高版本
- 現代瀏覽器（Chrome、Firefox、Edge、Safari）

## 瀏覽器支援

| 瀏覽器 | 版本 |
|--------|------|
| Chrome | 60+ |
| Firefox | 60+ |
| Safari | 13+ |
| Edge | 79+ |

## 注意事項

- 由於瀏覽器安全限制，無法直接讀取本地檔案系統
- 使用者需要手動選擇資料夾
- 部分舊版瀏覽器可能不支援資料夾選擇功能
- 大型 PDF 檔案可能需要較長載入時間

## 開發指令

### 開發模式
```bash
npm run dev  # 需另外設定 nodemon
```

### 生產模式
```bash
npm start     # node server.js
npm run prod  # pm2 start server.js
```

## PM2 管理指令

### 基本操作
```bash
pm2 list              # 列出所有進程
pm2 show pdf-viewer   # 顯示詳細資訊
pm2 logs pdf-viewer   # 查看日誌
pm2 monit             # 監控資源使用
```

### 進程控制
```bash
pm2 restart pdf-viewer  # 重啟
pm2 stop pdf-viewer     # 停止
pm2 delete pdf-viewer   # 刪除進程
```

### 自動化配置
```javascript
// ecosystem.config.js
module.exports = {
  apps: [{
    name: 'pdf-viewer',
    script: 'server.js',
    instances: 1,
    exec_mode: 'fork',
    watch: false,
    max_memory_restart: '1G',
    env: {
      NODE_ENV: 'development'
    },
    env_production: {
      NODE_ENV: 'production'
    }
  }]
}
```

使用配置檔啟動：
```bash
pm2 start ecosystem.config.js
```

## 貢獻指南

歡迎提交 Pull Request 或開立 Issue 來改進本專案。

## 授權

MIT License
