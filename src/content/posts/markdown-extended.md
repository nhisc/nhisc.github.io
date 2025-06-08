---
title: Markdown 擴展功能
published: 2025-06-08
updated: 2025-06-08
description: '了解更多 Fuwari 中的 Markdown 功能'
image: ''
tags: []
category: '範例'
draft: false 
---

## GitHub 儲存庫卡片
您可以新增連結到 GitHub 儲存庫的動態卡片，在頁面載入時，儲存庫資訊會從 GitHub API 取得。

::github{repo="Fabrizz/MMM-OnSpotify"}

使用程式碼 `::github{repo="<擁有者>/<儲存庫>"}` 建立 GitHub 儲存庫卡片。

```markdown
::github{repo="saicaca/fuwari"}
```

## 提示框

支援以下類型的提示框：`note` `tip` `important` `warning` `caution`

:::note
重點標示使用者應該注意的資訊，即使是快速瀏覽時也要注意。
:::

:::tip
幫助使用者更成功的可選資訊。
:::

:::important
使用者成功所需的重要資訊。
:::

:::warning
由於潛在風險而需要使用者立即注意的重要內容。
:::

:::caution
行動可能產生的負面後果。
:::

### 基本語法

```markdown
:::note
重點標示使用者應該注意的資訊，即使是快速瀏覽時也要注意。
:::

:::tip
幫助使用者更成功的可選資訊。
:::
```

### 自訂標題

提示框的標題可以自訂。

:::note[我的自訂標題]
這是一個有自訂標題的提示框。
:::

```markdown
:::note[我的自訂標題]
這是一個有自訂標題的提示框。
:::
```

### GitHub 語法

> [!TIP]
> 也支援 [GitHub 語法](https://github.com/orgs/community/discussions/16925)。

```
> [!NOTE]
> 也支援 GitHub 語法。

> [!TIP]
> 也支援 GitHub 語法。
```