# PDF 檔案檢視器

因為期中考很多slides與題目要看而生的repo

## 功能特點

- 選擇資料夾載入多個 PDF 檔案
- 下拉選單切換不同 PDF 檔案
- 即時預覽 PDF 內容

## 安裝步驟

### 1. 複製專案
```bash
git clone https://github.com/Kazmaku/PDF-viewer.git
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

### 4. 新增server.js
```
const express = require('express');
const path = require('path');
const app = express();
const port = 3000;

app.use(express.static('public'));

app.listen(port, () => {
    console.log(`伺服器運行於 http://localhost:${port}`);
});
```

### 5. 啟動伺服器

#### 開發環境
```bash
node server.js
```

#### 生產環境（使用 PM2）
```bash
pm2 start server.js --name "pdf-viewer"
pm2 save
pm2 startup  # 設定開機自動啟動(非必要
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


## 注意事項

- 由於瀏覽器安全限制，無法直接讀取本地檔案系統
- 使用者需要手動選擇資料夾
- 部分舊版瀏覽器可能不支援資料夾選擇功能
- 大型 PDF 檔案可能需要較長載入時間



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
