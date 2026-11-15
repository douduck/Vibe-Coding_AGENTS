# HTML 簡報視覺風格規範（STYLE_GUIDE.md）

本文件定義本專案預設的 **「粉彩天藍 × 鼠尾草」溫暖水彩插畫風** 設計規範，供未來擴充其他寵物簡報時保持一致的視覺體驗。

---

## 1. 色彩系統與 CSS 變數

所有 HTML 簡報請於 `:root` 沿用以下低飽和莫蘭迪色票，確保長時間閱讀柔和不刺眼：

| CSS 變數 | 色碼 | 用途說明 |
| :--- | :--- | :--- |
| `--bg` | `#F6F8F9` | 簡報主畫布柔光白底色 |
| `--card` | `#FFFFFF` | 內容卡片與導覽列純白底色 |
| `--sky` | `#89AFC7` | **主色一：粉彩天藍**（插畫框線、重點強調、編號圓章） |
| `--sky-soft` | `#E6F0F5` | 粉彩天藍淺底（膠囊標籤、資訊卡、按鈕預設底色） |
| `--sage` | `#9CB7A0` | **主色二：鼠尾草綠**（進度條作用中圓點、檢核框、卡片底） |
| `--sage-soft` | `#E7F0E8` | 鼠尾草綠淺底（分類標籤、正向優點卡片） |
| `--warm` | `#E8D5C4` | **輔助點綴：暖杏米**（插畫暖色元素、平衡冷色調） |
| `--warm-soft` | `#F9F3EC` | 暖米淺底（注意事項、挑戰缺點卡片與醫療免責提醒） |
| `--ink` | `#2F3B44` | 深石板灰藍主文字（確保足夠對比度） |
| `--muted` | `#5F6E78` | 次要說明文字與頁碼資訊 |
| `--border` | `#DCE5EB` | 卡片與外框柔和邊線 |

---

## 2. 版面、圓角與排版規範

- **字體設定**：`"Noto Sans TC", "PingFang TC", "Microsoft JhengHei", sans-serif`
- **字級層級**：
  - 封面主標題（`h1`）：`36px`（行高 `1.3`）
  - 內頁標題（`h2`）：`28px`（行高 `1.35`）
  - 引言／重點摘要（`p.lead`）：`17px`（行高 `1.7`）
  - 卡片內文：至少 `14.5px`（行高 `1.65`）
- **圓角與邊框**：
  - 簡報外框（`.deck-shell`）：`border-radius: 28px; border: 3px solid var(--border);`
  - 插畫相框（`.illus-frame`）：`border-radius: 26px; border: 3px solid var(--sky);`
  - 內容卡片（`.card`）：`border-radius: 20px; border: 2px solid var(--border);`
  - 膠囊標籤與按鈕（`.tag` / `.nav-btn`）：`border-radius: 999px;`
- **互動操作**：須支援底部「上一頁／下一頁」按鈕、圓點快速跳頁，以及鍵盤 `←`、`→`、`Space` 翻頁。

---

## 3. 溫暖水彩插畫規範

- **視覺調性**：手繪水彩／水粉（watercolor and gouache）質感，筆觸柔和、留白充足，避免生硬的純幾何拼湊圖形。
- **配色呼應**：寵物主角可搭配鼠尾草綠小配件（如領巾、項圈或葉片），背景帶入淡天藍與暖米色居家元素。
- **圖檔產出提示詞模板**（新增其他寵物時可替換 `[動物品種]`）：
  > `Warm cozy flat storybook illustration of a [動物品種] wearing a tiny sage green bandana, soft pastel sky blue (#89AFC7) and sage green (#9CB7A0) background accents, gentle hand-drawn watercolor and gouache texture, clean composition, text-free, no labels, no watermarks`
- **離線封裝原則**：原始圖檔應存於 `slides_html/assets/`，並於 HTML 內以 Base64 Data URI 內嵌，確保使用者下載單一 `.html` 檔即可離線正常顯示圖片。
