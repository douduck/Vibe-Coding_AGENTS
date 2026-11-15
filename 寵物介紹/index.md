# 寵物知識庫總索引（Pet Wiki Index）

本索引依據 `AGENTS.md`（`AGENTS.md`）規範維護，彙整本專案已建立的寵物介紹文章、問答筆記、簡報檔案、視覺風格規範與結構化資料集，方便檢視、擴充與下載使用。

## 專案檔案與資料集總覽

| 檔案／資料夾 | 類型 | 說明 |
| :--- | :--- | :--- |
| `AGENTS.md` | 專案規範 | 定義目錄架構、單一 PDF 自動入庫流程、JSON/CSV 欄位標準與無程式碼 AI 協作規範 |
| `index.md` | 知識庫索引 | 本文件，記錄各物種收錄進度、檔案路徑與更新日誌 |
| `pets_master.json` | 結構化資料集 | 所有已收錄寵物的標準化 JSON 資料 |
| `pets_master.csv` | 表格資料集 | 由 `pets_master.json` 匯出之 `utf-8-sig` 編碼 CSV（可用 Excel 直接開啟） |
| `raw/` | 原始資料夾 | 存放所有上傳的原始 PDF（`比熊.pdf`、`哈士奇.pdf`、`賓士貓.pdf`） |
| `content/` | 品種介紹資料夾 | **所有寵物介紹文章一律存於此資料夾下依物種分類的子目錄**（如 `content/dogs/`、`content/cats/`） |
| `notes/` | 問答筆記夾 | 嚴格依據資料夾現有資料撰寫之問答 `.md` 筆記 |
| `slides_outline/` | 簡報大綱夾 | 依據 `notes/` 內容拆分之簡報逐頁 Markdown 大綱 |
| `slides_html/` | HTML 簡報夾 | 依據大綱與 `slides_html/STYLE_GUIDE.md` 風格生成之單檔離線 HTML 簡報 |
| `slides_html/STYLE_GUIDE.md` | 視覺風格規範 | 粉彩天藍 × 鼠尾草溫暖水彩插畫風色票、字體、圓角與插畫提示詞規範 |

## 目前收錄統計

- **已收錄物種總數**：4 筆
- **犬類（`content/dogs/`）**：2 筆
- **貓類（`content/cats/`）**：1 筆
- **小型哺乳類（`content/small_mammals/`）**：0 筆（待擴充）
- **鳥類（`content/birds/`）**：0 筆（待擴充）
- **爬蟲類（`content/reptiles/`）**：0 筆（待擴充）
- **觀賞魚（`content/fish/`）**：0 筆（待擴充）
- **問答筆記（`notes/`）**：4 份
- **簡報大綱（`slides_outline/`）**：3 份
- **HTML 簡報（`slides_html/`）**：3 份

## 物種分類目錄

### 犬類（`content/dogs/`）

| ID | 中文名稱 | 英文名稱 | 體型 | 新手友善度 | 檔案路徑 | 最後更新 |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| `dog_bichon_frise` | 比熊犬 | Bichon Frise | 中小型（`small`） | 4 / 5 | `content/dogs/dog_bichon_frise.md` | 2026-11-15 |
| `dog_siberian_husky` | 哈士奇 | Siberian Husky | 中型（`medium`） | 2 / 5 | `content/dogs/dog_siberian_husky.md` | 2026-11-15 |

### 貓類（`content/cats/`）

| ID | 中文名稱 | 英文名稱 | 體型 | 新手友善度 | 檔案路徑 | 最後更新 |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| `cat_tuxedo` | 賓士貓 | Tuxedo Cat | 中型（`medium`） | 4 / 5 | `content/cats/cat_tuxedo.md` | 2026-11-15 |

### 其他物種

目前尚無條目。之後新增任何寵物介紹文章，一律依物種存入 `content/<species>/` 資料夾並同步更新本表與 `pets_master.json`。

## 問答筆記與簡報索引

| 類型 | 檔案路徑 | 對應主題／來源 | 最後更新 |
| :--- | :--- | :--- | :--- |
| 問答筆記 | `notes/20261115_bichon_beginner_pros_cons.md` | 新手適不適合養比熊犬與優缺點（依 `raw/比熊.pdf`） | 2026-11-15 |
| 簡報大綱 | `slides_outline/20261115_bichon_beginner_pros_cons_outline.md` | 新手比熊犬飼養評估 8 頁大綱 | 2026-11-15 |
| HTML 簡報 | `slides_html/20261115_bichon_beginner_pros_cons_slides.html` | 粉彩天藍 × 鼠尾草溫暖水彩插畫風簡報（比熊犬） | 2026-11-15 |
| 問答筆記 | `notes/20261115_husky_beginner_pros_cons.md` | 新手適不適合養哈士奇與優缺點（依 `raw/哈士奇.pdf`） | 2026-11-15 |
| 簡報大綱 | `slides_outline/20261115_husky_beginner_pros_cons_outline.md` | 新手哈士奇飼養評估 8 頁大綱 | 2026-11-15 |
| HTML 簡報 | `slides_html/20261115_husky_beginner_pros_cons_slides.html` | 粉彩天藍 × 鼠尾草溫暖水彩插畫風簡報（哈士奇） | 2026-11-15 |
| 問答筆記 | `notes/20261115_tuxedo_beginner_pros_cons.md` | 新手適不適合養賓士貓與優缺點（依 `raw/賓士貓.pdf`） | 2026-11-15 |
| 簡報大綱 | `slides_outline/20261115_tuxedo_beginner_pros_cons_outline.md` | 新手賓士貓飼養評估 8 頁大綱 | 2026-11-15 |
| HTML 簡報 | `slides_html/20261115_tuxedo_beginner_pros_cons_slides.html` | 粉彩天藍 × 鼠尾草溫暖水彩插畫風簡報（賓士貓） | 2026-11-15 |
| 風格規範 | `slides_html/STYLE_GUIDE.md` | 粉彩天藍 × 鼠尾草溫暖水彩插畫風設計規範 | 2026-11-15 |

## 更新日誌（Changelog）

- **2026-11-15（新增賓士貓品種資料、問答筆記與 HTML 簡報）**
  - 歸檔 `raw/賓士貓.pdf`，並建立貓類介紹文章 `content/cats/cat_tuxedo.md`。
  - 同步更新 `pets_master.json`、`pets_master.csv` 與 `index.md`（收錄總數更新為 3 筆）。
  - 產出問答筆記 `notes/20261115_tuxedo_beginner_pros_cons.md`、簡報大綱 `slides_outline/20261115_tuxedo_beginner_pros_cons_outline.md`、封面水彩插畫 `slides_html/assets/tuxedo_cover.jpg` 與離線 HTML 簡報 `slides_html/20261115_tuxedo_beginner_pros_cons_slides.html`。
- **2026-11-15（整理資料夾歸檔架構並補齊哈士奇筆記與簡報）**
  - 移除程式碼腳本依賴，更新 `AGENTS.md` 為純 AI 協作規範。
  - 將 `dog_bichon_frise.md` 與 `dog_siberian_husky.md` 統一歸檔至 `content/dogs/`，並標註後續所有品種介紹文章皆存於 `content/<species>/`。
  - 補齊哈士奇問答筆記 `notes/20261115_husky_beginner_pros_cons.md`、簡報大綱 `slides_outline/20261115_husky_beginner_pros_cons_outline.md` 與 HTML 簡報 `slides_html/20261115_husky_beginner_pros_cons_slides.html`。
- **2026-11-15（新增哈士奇品種資料與介紹）**
  - 依據 `raw/哈士奇.pdf` 新增哈士奇介紹文章，並同步更新 `pets_master.json`、`pets_master.csv` 與 `index.md`。
- **2026-11-15（初始化知識庫與比熊犬示範資料）**
  - 建立 `AGENTS.md`、`index.md`、`pets_master.json`、`pets_master.csv` 與比熊犬完整介紹、筆記與簡報。
