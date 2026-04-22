# Student Grade Proxy Server

代理服務器用於存取 SharePoint Excel 檔案，過濾並返回學生成績資料。

## 🚀 Railway 快速部署

### 步驟 1：準備專案

1. 確保所有檔案都在 `railway-proxy-server` 目錄中
2. 推送到 GitHub（如果還沒有）

```bash
cd railway-proxy-server
git init
git add .
git commit -m "Initial commit: Railway proxy server"
git remote add origin https://github.com/lkw0102/railway-proxy-server.git
git push -u origin main
```

### 步驟 2：部署到 Railway

1. 前往 [Railway](https://railway.app)
2. 使用 GitHub 帳號登入
3. 點擊「New Project」
4. 選擇「Deploy from GitHub repo」
5. 選擇您的儲存庫
6. Railway 會自動偵測 Node.js 專案

### 步驟 3：設定環境變數

在 Railway 專案設定中，前往「Variables」標籤，新增：

```
TENANT_ID=d1a86d43-9bb5-40b7-ab52-754d8d6d7bf1
CLIENT_ID=your-client-id
PROXY_USERNAME=s54748@esp.edu.mo
PROXY_PASSWORD=your-password
NODE_ENV=production
ALLOWED_ORIGINS=https://groupespauloedu.sharepoint.com
```

### 步驟 4：設定建置和啟動命令

Railway 通常會自動偵測，但可以手動設定：

- **Build Command**: `npm install && npm run build`
- **Start Command**: `node dist/server.js`

### 步驟 5：取得服務 URL

部署完成後，Railway 會提供一個 URL，例如：
```
https://your-app-name.up.railway.app
```

## 📝 本地開發

```bash
# 安裝依賴
npm install

# 開發模式
npm run dev

# 建置
npm run build

# 生產模式
npm start
```

## 🔗 API 端點

### POST /api/getStudentGrade

**請求：**
```json
{
  "studentId": "s12345",
  "excelFilePath": "https://groupespauloedu.sharepoint.com/:x:/r/sites/Classrooms/Shared%20Documents/test.xlsx"
}
```

**回應：**
```json
{
  "success": true,
  "data": [
    {
      "學生帳號": "s12345",
      "科目1": 85,
      "科目2": 90
    }
  ],
  "studentId": "s12345"
}
```

### GET /health

健康檢查端點，返回服務狀態。

## 🔐 環境變數

| 變數名稱 | 說明 | 必填 |
|---------|------|------|
| `TENANT_ID` | Azure AD 租戶 ID | ✅ |
| `CLIENT_ID` | Azure AD 應用程式 ID | ✅ |
| `PROXY_USERNAME` | 代理人帳號 | ✅ |
| `PROXY_PASSWORD` | 代理人帳號密碼 | ✅ |
| `PORT` | 伺服器端口（Railway 會自動設定） | ❌ |
| `NODE_ENV` | 環境模式 | ❌ |
| `ALLOWED_ORIGINS` | 允許的來源（CORS） | ❌ |

## 📋 檢查清單

- [ ] 專案已推送到 GitHub
- [ ] Railway 專案已建立
- [ ] 環境變數已設定
- [ ] 部署成功
- [ ] 健康檢查端點可訪問
- [ ] API 端點測試通過
- [ ] SPFx 已更新為使用新的服務 URL
