# AGENTS.md — 各式寵物介紹與資料集建置專案規範

> **⚡ AI 代理必讀：當收到「新的寵物 PDF」或「生成 XX 資料」請求時（強制執行規則）**
>
> **⛔ 禁止只在聊天室回覆純文字摘要！**
> 當使用者上傳本資料夾（或專案）與新的寵物 PDF（例如 `賓士貓.pdf`），並要求 "生成 XX 的資料" 或 "整理 XX" 時，**絕對不可只在對話框列出文字重點就結束**。AI 代理必須**實際建立所有對應檔案並重新打包為 `寵物介紹.zip` 提供下載**（因為 AI 無法直接修改使用者電腦本機資料夾，必須透過產出新 `.zip` 讓使用者下載更新）。
>
> 請立即依序執行以下 5 個步驟（不需等待使用者二次確認）：
>
> 1. **歸檔至 `raw/`**：若新上傳的 PDF（如 `賓士貓.pdf`）尚未在 `raw/` 內，立刻將其存入 `raw/<原始檔名>.pdf`。
> 2. **讀取全文並建立介紹文章與資料集**：完整讀取該 PDF（圖片／掃描型 PDF 須逐頁視覺判讀），並實際寫入檔案：
>    - 新增品種介紹文章至 `content/<物種>/<物種>_<英文代碼>.md`（犬類存於 `content/dogs/`、貓類存於 `content/cats/`，例如 `content/cats/cat_tuxedo.md`）。
>    - 更新根目錄的 `pets_master.json` 與 `pets_master.csv`（`utf-8-sig` 含 BOM）。
>    - 更新 `index.md` 的物種統計與分類表；並更新專案資料夾外層、與 `寵物介紹/` 同一層的 `index.html` 簡報導覽連結。
> 3. **實際建立問答筆記檔案（`notes/`）**：嚴格依據該 PDF 與資料夾現有資料，建立 `notes/YYYYMMDD_<品種>_beginner_pros_cons.md`（不混入未收錄的外部知識；缺漏項目僅於末段附參考連結）。
> 4. **實際建立簡報大綱、HTML 簡報檔案與首頁導覽**：
>    - 建立 `slides_outline/YYYYMMDD_<品種>_beginner_pros_cons_outline.md`。
>    - 依 `slides_html/STYLE_GUIDE.md`（粉彩天藍 × 鼠尾草溫暖水彩插畫風）生成對應寵物插畫存於 `slides_html/assets/`，並建立內嵌 Base64 圖片的離線單檔簡報 `slides_html/YYYYMMDD_<品種>_beginner_pros_cons_slides.html`。
>    - **同步更新 `index.md` 與專案資料夾外層的 `index.html`**：確保外層首頁卡片與超連結正確指向 `寵物介紹/slides_html/YYYYMMDD_<品種>_beginner_pros_cons_slides.html`，無 404 連結錯誤。
> 5. **驗證並打包提供下載**：確認 JSON 無重複 `id`、數值皆符合 `min <= max`、無 `TBD` 佔位符且網頁超連結皆有效後，**將整份 `寵物介紹/` 重新打包為 `寵物介紹.zip` 交給使用者下載**。

---


## 專案外層首頁與簡報導覽（強制規則）

- **`index.html` 必須放在 `寵物介紹/` 資料夾的外層，與 `寵物介紹/` 資料夾同一層**；不得放在 `寵物介紹/index.html`，也不可只把首頁放在 `slides_html/` 或其他子資料夾。解壓縮後的結構必須是：`index.html` 與 `寵物介紹/` 並列。
- 每次新增、刪除、改名或重新生成任何 `寵物介紹/slides_html/*.html` 簡報時，**同一輪作業必須同步更新外層的 `index.html`**，讓首頁能連到目前專案內的每一份正式簡報；不可只新增最新簡報的連結而漏掉既有簡報。
- 外層首頁依物種分類呈現簡報卡片，連結一律使用相對路徑，例如 `寵物介紹/slides_html/檔名.html`，不得使用本機絕對路徑或暫存路徑。
- 若簡報檔案被移除或改名，必須同步修正／移除外層首頁對應連結；若簡報新增，必須新增對應卡片與連結。
- **打包前必須自動或人工比對**：`寵物介紹/slides_html/` 中每一份正式簡報 HTML 都有且只有一個可用的外層首頁入口；首頁每個簡報連結都必須指向實際存在的檔案，不得有 404。`STYLE_GUIDE.md` 不屬於簡報，不需建立卡片。
- 外層首頁更新後，重新檢查解壓縮後可直接以瀏覽器開啟 `index.html`，並可由首頁開啟所有簡報。

## 專案目標與語言規範

- **專案目標**：建立涵蓋犬, 貓, 小型哺乳類, 鳥類, 爬蟲與觀賞魚等各式寵物的知識庫與結構化資料集（`pets_master.json`、`pets_master.csv`），並支援基於知識庫的問答筆記、簡報大綱與 HTML 簡報產出及 `index.html` 首頁導覽。使用者不需撰寫或執行程式碼，所有作業皆由 AI 代理依本文件規範完成。
- **語言與地區慣例**：一律使用**繁體中文（台灣用語）**，例如：飼料、結紮、晶片登記、狂犬病疫苗、寵物美容、新台幣（TWD）。
- **寫作語氣**：兼顧科學準確性與親切易讀性；避免過度擬人化或誇大行銷詞彙，飼養難度與缺點須客觀呈現。

## 目錄結構與存檔位置規範

請 AI 代理在建立、移動或更新檔案時，嚴格遵守以下目錄分工：

- `raw/`：存放所有原始參考 PDF、公開飼養指南與未整理筆記（如 `比熊.pdf`、`哈士奇.pdf`、`賓士貓.pdf`）。
- `content/`：依物種分類存放**所有寵物介紹 Markdown 文章**：
  - `content/dogs/`：犬類介紹文章（如 `dog_bichon_frise.md`、`dog_siberian_husky.md`）
  - `content/cats/`：貓類介紹文章（如 `cat_tuxedo.md`）
  - `content/small_mammals/`、`content/birds/`、`content/reptiles/`、`content/fish/`：其他物種待擴充。
- `notes/`：嚴格依據專案現有資料回答使用者問題或彙整所產出的 `.md` 問答筆記。
- `slides_outline/`：依據 `notes/` 內容拆分產出的簡報逐頁大綱（Markdown）。
- `slides_html/`：依據簡報大綱與風格規範（`slides_html/STYLE_GUIDE.md`）製作的離線 HTML 簡報檔案，插畫原圖備份於 `slides_html/assets/`。
- `index.html`：專案導覽首頁，提供美觀的圖卡與正確相對路徑（`slides_html/...`），供點擊瀏覽各品種簡報。
- `pets_master.json` & `pets_master.csv`：位於專案根目錄的主要結構化資料集（CSV 須為 `utf-8-sig` 含 BOM 編碼）。
- `index.md`：知識庫總索引 Markdown 版本。

## 結構化資料集欄位規範

每筆寵物紀錄須包含核心欄位（`id`、`species`、`breed_zh`、`breed_en`、`size_tier`、`adult_weight_kg`、`lifespan_years`、`beginner_friendly`、`exercise_need`、`grooming_need`、`temperament_tags`、`climate_suitability_tw`、`common_health_issues`、`initial_cost_twd`、`monthly_cost_twd`、`adoption_notes`、`sources`、`last_updated`）。
