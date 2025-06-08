---
title: 內湖高中資訊研究社官網設定與維護指南
published: 2025-06-08
description: 完整的網站設定、部署和維護交接指南，包含 GitHub 操作和日常維護流程。第34屆交接給第35屆使用。
tags: []
category: 技術文檔
draft: false
---

# 內湖高中資訊研究社官網設定與維護指南

本指南提供完整的網站設定、部署和維護流程，適用於**第34屆交接給第35屆**使用。

## 📋 目錄

1. [前置準備](#前置準備)
2. [環境設定](#環境設定)
3. [專案指令說明](#專案指令說明)
4. [網站結構說明](#網站結構說明)
5. [基本設定](#基本設定)
6. [內容管理](#內容管理)
7. [特殊功能設定](#特殊功能設定)
8. [GitHub 操作](#github-操作)
9. [部署流程](#部署流程)
10. [日常維護](#日常維護)
11. [常見問題](#常見問題)
12. [交接清單](#交接清單)

## 🚀 前置準備

### 系統需求
- **Node.js**：版本 ≤ 22
- **pnpm**：版本 ≤ 9（推薦使用，比 npm 更快）
- **Git**：版本控制工具
- **VS Code**：推薦的程式碼編輯器

### 需要的帳號
- **GitHub 帳號**：用於程式碼管理和部署
- **Vercel/Netlify 帳號**（可選）：用於自動部署

## 💻 環境設定

### 1. 安裝 Node.js
1. 前往 [Node.js 官網](https://nodejs.org/)
2. 下載並安裝 LTS 版本（確保版本 ≤ 22）
3. 驗證安裝：
```bash
node --version  # 應該顯示 v18.x.x 或 v20.x.x
```

### 2. 安裝 pnpm
```bash
# 全域安裝 pnpm
npm install -g pnpm

# 驗證安裝
pnpm --version  # 應該顯示版本號 ≤ 9
```

### 3. 複製並設定專案
```bash
# 複製專案
git clone https://github.com/你的帳號/NHISC._.35th.git
cd NHISC._.35th

# 安裝相依套件（必須執行兩個指令）
pnpm install
pnpm add sharp  # 圖片處理套件，必須額外安裝

# 啟動開發伺服器
pnpm dev
```

## 🧞 專案指令說明

以下所有指令都需要在專案根目錄執行：

| 指令 | 功能 |
|:--|:--|
| `pnpm install` 並 `pnpm add sharp` | 安裝相依套件 |
| `pnpm dev` | 在 `localhost:4321` 啟動本地開發伺服器 |
| `pnpm build` | 建構網站至 `./dist/` |
| `pnpm preview` | 本地預覽已建構的網站 |
| `pnpm new-post <檔名>` | 建立新文章 |
| `pnpm astro ...` | 執行 `astro add`, `astro check` 等指令 |
| `pnpm astro --help` | 顯示 Astro CLI 幫助 |

### 常用指令範例
```bash
# 建立新文章
pnpm new-post "2025-06-08-新生說明會"

# 檢查程式碼
pnpm astro check

# 建構並預覽
pnpm build
pnpm preview
```

## 📁 網站結構說明

```
NHISC._.35th/
├── src/
│   ├── config.ts              # 主要設定檔
│   ├── content/
│   │   ├── posts/             # 文章目錄
│   │   └── spec/              # 特殊頁面（關於我們等）
│   ├── components/            # 網站元件
│   ├── layouts/               # 頁面布局
│   └── assets/                # 靜態資源
├── public/
│   ├── favicon/               # 網站圖示
│   └── images/                # 公開圖片
├── astro.config.mjs           # Astro 設定檔
└── package.json               # 專案設定檔
```

## ⚙️ 基本設定

### 1. 修改網站基本資訊
編輯 `src/config.ts`：

```typescript
export const siteConfig: SiteConfig = {
    title: "NHISC._.35th", // 內湖高中資訊研究社第35屆
    subtitle: "內湖高中資訊研究社", // 網站副標題
    lang: "zh-TW",
    themeColor: {
        hue: 280, // 可調整主題色調（0-360）
        fixed: true, // 關閉主頁調色盤
    },
    banner: {
        enable: false, // 建議保持關閉
        src: "assets/images/demo-banner.png",
        position: "center",
        credit: {
            enable: false,
            text: "",
            url: "",
        },
    },
    toc: {
        enable: true, // 顯示文章目錄
        depth: 3, // 目錄深度
    },
    favicon: [
        {
            src: "/favicon/icon.png", // 社團 Logo
            theme: "light",
            sizes: "32x32",
        },
    ],
};

export const profileConfig: ProfileConfig = {
    avatar: "assets/images/club-logo.png", // 社團 Logo
    name: "NHISC._.35th", // 內湖高中資訊研究社第35屆
    bio: "內湖高中資訊研究社第35屆", // 社團簡介
    links: [
        {
            name: "GitHub",
            url: "https://github.com/你的組織",
            icon: "fa6-brands:github"
        },
        {
            name: "Instagram",
            url: "https://instagram.com/nhisc",
            icon: "fa6-brands:instagram"
        }
    ],
};

export const navBarConfig: NavBarConfig = {
    links: [
        LinkPreset.Home,      // 首頁
        LinkPreset.Archive,   // 文章列表
        LinkPreset.About,     // 關於我們
        // 可加入自訂連結
    ],
};
```

### 2. 更新網站圖示
1. 準備社團 Logo（建議 32x32 像素的 PNG 檔案）
2. 將檔案命名為 `icon.png`
3. 放置到 `public/favicon/` 目錄

### 3. 設定部署網址
編輯 `astro.config.mjs`：

```javascript
export default defineConfig({
  site: 'https://你的帳號.github.io',
  base: '/NHISC._.35th',
  // 其他設定...
});
```

## 📝 內容管理

### 1. 新增文章
使用指令建立新文章：

```bash
# 建立新文章（會自動產生檔案和基本 frontmatter）
pnpm new-post "2025-06-08-活動名稱"
```

或手動在 `src/content/posts/` 目錄建立新的 `.md` 檔案：

```markdown
---
title: 文章標題
published: 2025-06-08
description: 文章簡短描述
tags: [標籤1, 標籤2]
category: 分類名稱
draft: false
lang: zh-TW  # 僅當文章語言與 config.ts 中的網站語言不同時需要設置
---

# 文章內容

這裡寫文章內容...
```

### 2. 管理文章分類
建議的分類：
- `活動紀錄`：社團活動報告
- `技術教學`：程式設計教學
- `公告`：重要通知
- `心得分享`：成員心得
- `競賽成果`：比賽參與和成績

### 3. 更新關於我們頁面
編輯 `src/content/spec/about.md`：

```markdown
# 關於內湖高中資訊研究社

## 社團簡介
內湖高中資訊研究社（NHISC）成立於...，致力於推廣程式設計和資訊科技教育。

## 第35屆幹部介紹
- **社長**：XXX
- **副社長**：XXX（35th Vice President）
- **教學長**：XXX（35th Head of Education）
- **公關長**：XXX
- **美宣長**：XXX

## 相關連結
- [第34屆官網](https://nhisc34.pages.dev/)
- [GitHub 組織](https://github.com/你的組織)
- [Instagram](https://instagram.com/nhisc)

## 聯絡資訊
- Email: nhisc@example.com
- 社辦位置：XXX教室
```

## 🎨 特殊功能設定

### 1. GitHub 儲存庫卡片
在文章中插入 GitHub 專案卡片：

```markdown
::github{repo="你的組織/專案名稱"}
```

### 2. 提示框
支援多種類型的提示框：

```markdown
:::note
重要提醒內容
:::

:::tip
實用小技巧
:::

:::warning
注意事項
:::

:::important
重要資訊
:::

:::caution
警告內容
:::
```

### 3. 自訂提示框標題
```markdown
:::note[自訂標題]
自訂標題的提示框內容
:::
```

### 4. 數學公式
支援 LaTeX 數學公式：

```markdown
行內公式：$E = mc^2$

區塊公式：
$$
\sum_{i=1}^{n} x_i = x_1 + x_2 + \ldots + x_n
$$
```

## 🐙 GitHub 操作

### 1. 基本 Git 流程
```bash
# 查看目前狀態
git status

# 加入變更檔案
git add .

# 提交變更
git commit -m "更新：描述你做的變更"

# 推送到 GitHub
git push origin main
```

### 2. 常用 Git 指令
```bash
# 查看提交歷史
git log --oneline

# 查看變更內容
git diff

# 取得最新版本
git pull origin main

# 建立新分支
git checkout -b 新功能分支

# 切換分支
git checkout main
```

### 3. 協作流程
1. **更新前先拉取最新版本**
```bash
git pull origin main
```

2. **進行修改後提交**
```bash
git add .
git commit -m "新增：2025-06-08 新生說明會文章"
git push origin main
```

## 🚀 部署流程

### 方法一：GitHub Pages（推薦）
1. 進入 GitHub 專案設定頁面
2. 找到 "Pages" 選項
3. 選擇 "GitHub Actions" 作為來源
4. 網站會自動部署到 `https://你的帳號.github.io/NHISC._.35th`

### 方法二：Vercel 部署
1. 前往 [Vercel](https://vercel.com/)
2. 使用 GitHub 帳號登入
3. 匯入專案
4. 建構指令設定為 `pnpm build`
5. 輸出目錄設定為 `dist`

### 部署前檢查
確保 `astro.config.mjs` 設定正確：

```javascript
export default defineConfig({
  site: 'https://你的帳號.github.io',
  base: '/NHISC._.35th',
  integrations: [
    // ...其他設定
  ],
});
```

## 🔧 日常維護

### 1. 定期檢查事項
- **每週**：檢查網站是否正常運作
- **每月**：更新相依套件 `pnpm update`
- **每學期**：備份重要內容

### 2. 新增社團活動文章流程
```bash
# 1. 建立新文章
pnpm new-post "2025-06-08-新生入社說明會"

# 2. 編輯文章內容
# 檔案位置：src/content/posts/2025-06-08-新生入社說明會.md

# 3. 本地測試
pnpm dev

# 4. 提交和推送
git add .
git commit -m "新增：新生入社說明會活動紀錄"
git push origin main
```

### 3. 圖片管理最佳實務
- **小圖片**（<1MB）：放在 `src/assets/images/`
- **大圖片**（>1MB）：放在 `public/images/`
- **文章專用圖片**：與文章放在同一目錄
- **圖片檔名**：使用英文和數字，避免中文和特殊字元

### 4. 管理草稿文章
```markdown
---
title: 未完成的文章
draft: true  # 設為 true 隱藏文章
---
```

完成後改為 `draft: false` 發布。

## ❓ 常見問題

### Q1: 執行 `pnpm dev` 失敗
```bash
# 解決方案：重新安裝相依套件
rm -rf node_modules pnpm-lock.yaml
pnpm install
pnpm add sharp
pnpm dev
```

### Q2: 圖片無法顯示
- 檢查圖片路徑是否正確
- 確認圖片檔案存在
- 圖片名稱不要包含中文或特殊字元
- 檢查 `sharp` 套件是否已安裝

### Q3: `pnpm new-post` 指令無效
```bash
# 檢查是否在專案根目錄
pwd

# 重新安裝專案
pnpm install
```

### Q4: Git 推送失敗
```bash
# 如果遠端有新變更，先拉取
git pull origin main
# 解決衝突後重新推送
git push origin main
```

### Q5: 部署後網站內容沒更新
- 等待 5-10 分鐘讓部署完成
- 清除瀏覽器快取（Ctrl+F5）
- 檢查 GitHub Actions 是否成功執行
- 確認 `astro.config.mjs` 設定正確

### Q6: Node.js 版本問題
```bash
# 檢查 Node.js 版本
node --version

# 如果版本過高，建議使用 nvm 管理版本
# Windows: 下載 nvm-windows
# macOS/Linux: 安裝 nvm

# 安裝並使用 Node.js 20
nvm install 20
nvm use 20
```

## 📞 交接清單

### 第34屆移交給第35屆時需要提供：

#### 帳號權限
- [ ] GitHub 組織權限（Admin 或 Owner）
- [ ] Vercel/Netlify 部署平台帳號
- [ ] 網域管理權限（如有自訂網域）

#### 重要資料
- [ ] 這份完整的操作手冊
- [ ] 社團相關圖片和資源檔案
- [ ] 歷屆活動照片和文章
- [ ] 社團 Logo 和美術素材

#### 密碼和設定
- [ ] GitHub 組織帳號：`______`
- [ ] 部署平台帳號：`______`
- [ ] 網域管理帳號：`______`（如有）

#### 技術交接
- [ ] 確認新負責人已成功在本地運行專案
- [ ] 教學基本的 Git 操作和文章發布流程
- [ ] 說明特殊功能的使用方法
- [ ] 提供緊急聯絡方式

## 📚 進階資源

- [Astro 官方文檔](https://docs.astro.build/zh-cn/)
- [Fuwari 模板文檔](https://github.com/saicaca/fuwari)
- [Markdown 語法指南](https://markdown.tw/)
- [Git 教學](https://git-scm.com/book/zh-tw/v2)
- [GitHub 教學](https://docs.github.com/zh)
- [pnpm 文檔](https://pnpm.io/zh/)

## 🆘 緊急聯絡

**如果網站出現嚴重問題或需要技術支援，請立即聯絡：**

### 📧 第34屆副社長技術支援

#### 📝 Email 模板（手動複製使用）
如果上方連結無法使用，請複製以下模板手動發送 email 至 `zengcode0315@gmail.com`：

```
主旨：NHISC._.35th 官網技術支援請求

副社長，

我在維護內湖高中資訊研究社官網時遇到問題，需要您的協助。

【問題描述】
請詳細描述遇到的問題：


【錯誤訊息】
如有錯誤訊息，請複製貼上：


【執行環境】
- 作業系統：
- Node.js 版本：
- 瀏覽器：

【已嘗試的解決方法】
請列出已經嘗試過的解決方法：

謝謝協助！

內湖高中資訊研究社第35屆
```

### 🔧 備用方案
- 如果主要部署失敗，可以暫時使用 Vercel 部署
- 重要公告可以先透過社群媒體發布
- 保持定期備份，避免資料遺失

---

**最後更新**：2025年6月8日  
**版本**：v1.1 - 第34屆交接第35屆專用版（含技術支援聯絡）  
**維護者**：內湖高中資訊研究社第34屆  
**技術支援**：第34屆副社長 (zengcode0315@gmail.com)

> 💡 **提醒**：這份文檔應該定期更新，確保所有資訊都是最新的。建議每學期檢查一次，並根據實際使用情況調整內容。