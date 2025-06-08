---
title: Fuwari 簡單使用指南
published: 2025-06-08
description: "如何使用這個部落格模板。"
image: "./cover.jpeg"
tags: []
category: 指南
draft: false
---

> 封面圖片來源：[來源](https://image.civitai.com/xG1nkqKTMzGDvpLrqFT7WA/208fc754-890d-4adb-9753-2c963332675d/width=2048/01651-1456859105-(colour_1.5),girl,_Blue,yellow,green,cyan,purple,red,pink,_best,8k,UHD,masterpiece,male%20focus,%201boy,gloves,%20ponytail,%20long%20hair,.jpeg)

這個部落格模板是使用 [Astro](https://astro.build/) 建立的。對於本指南中未提及的事項，您可以在 [Astro 文檔](https://docs.astro.build/) 中找到答案。

## 文章的 Front-matter

```yaml
---
title: 我的第一篇部落格文章
published: 2023-09-09
description: 這是我新 Astro 部落格的第一篇文章。
image: ./cover.jpg
tags: [Foo, Bar]
category: 前端
draft: false
---
```

| 屬性          | 描述                                                                                                                                                                                                     |
|---------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `title`       | 文章標題。                                                                                                                                                                                               |
| `published`   | 文章發布日期。                                                                                                                                                                                           |
| `description` | 文章的簡短描述。顯示在首頁上。                                                                                                                                                                           |
| `image`       | 文章的封面圖片路徑。<br/>1. 以 `http://` 或 `https://` 開頭：使用網路圖片<br/>2. 以 `/` 開頭：使用 `public` 目錄中的圖片<br/>3. 不使用上述前綴：相對於 markdown 檔案的路徑                        |
| `tags`        | 文章標籤。                                                                                                                                                                                               |
| `category`    | 文章分類。                                                                                                                                                                                               |
| `draft`       | 如果這篇文章仍是草稿，則不會顯示。                                                                                                                                                                       |

## 文章檔案放置位置

您的文章檔案應該放在 `src/content/posts/` 目錄中。您也可以建立子目錄來更好地組織您的文章和資源。

```
src/content/posts/
├── post-1.md
└── post-2/
    ├── cover.png
    └── index.md
```
