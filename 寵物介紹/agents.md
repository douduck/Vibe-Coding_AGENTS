# AGENTS.md — 各式寵物介紹與資料集建置專案規範

> **⚡ AI 代理必讀：當收到「新的寵物 PDF」或「生成 XX 資料」請求時（強制執行規則）**
>
> **⛔ 禁止只在聊天室回覆純文字摘要！**
> 當使用者上傳本資料夾（或專案）與新的寵物 PDF（例如 `賓士貓.pdf`），並要求「生成 XX 的資料」或「整理 XX」時，**絕對不可只在對話框列出文字重點就結束**。AI 代理必須**實際建立所有對應檔案並重新打包為 `寵物介紹.zip` 提供下載**（因為 AI 無法直接修改使用者電腦本機資料夾，必須透過產出新 `.zip` 讓使用者下載更新）。
>
> 請立即依序執行以下 5 個步驟（不需等待使用者二次確認）：
>
> 1. **歸檔至 `raw/`**：若新上傳的 PDF（如 `賓士貓.pdf`）尚未在 `raw/` 內，立刻將其存入 `raw/<原始檔名>.pdf`。
> 2. **讀取全文並建立介紹文章與資料集**：完整讀取該 PDF（圖片／掃描型 PDF 須逐頁視覺判讀），並實際寫入檔案：
>    - 新增品種介紹文章至 `content/<物種>/<物種>_<英文代碼>.md`（犬類存於 `content/dogs/`、貓類存於 `content/cats/`，例如 `content/cats/cat_tuxedo.md`）。
>    - 更新根目錄的 `pets_master.json` 與 `pets_master.csv`（`utf-8-sig` 含 BOM）。
>    - 更新 `index.md` 的物種統計、分類表與更新日誌。
> 3. **實際建立問答筆記檔案（`notes/`）**：嚴格依據該 PDF 與資料夾現有資料，建立 `notes/YYYYMMDD_<品種>_beginner_pros_cons.md`（不混入未收錄的外部知識；缺漏項目僅於末段附參考連結）。
> 4. **實際建立簡報大綱與 HTML 簡報檔案**：
>    - 建立 `slides_outline/YYYYMMDD_<品種>_beginner_pros_cons_outline.md`。
>    - 依 `slides_html/STYLE_GUIDE.md`（「粉彩天藍 × 鼠尾草」溫暖水彩插畫風）生成對應寵物插畫存於 `slides_html/assets/`，並建立內嵌 Base64 圖片的離線單檔簡報 `slides_html/YYYYMMDD_<品種>_beginner_pros_cons_slides.html`。
> 5. **驗證並打包提供下載**：確認 JSON 無重複 `id`、數值皆符合 `min <= max`、無 `TBD` 佔位符後，**將整份 `寵物介紹/` 重新打包為 `寵物介紹.zip` 交給使用者下載**，並預覽新生成的簡報或 `.md` 檔案。

---

## 專案目標與語言規範

- **專案目標**：建立涵蓋犬、貓、小型哺乳類、鳥類、爬蟲與觀賞魚等各式寵物的知識庫與結構化資料集（`pets_master.json`、`pets_master.csv`），並支援基於知識庫的問答筆記、簡報大綱與 HTML 簡報產出。使用者不需撰寫或執行程式碼，所有作業皆由 AI 代理依本文件規範完成。
- **語言與地區慣例**：一律使用**繁體中文（台灣用語）**，例如：飼料、結紮、晶片登記、狂犬病疫苗、寵物美容、新台幣（TWD）。
- **寫作語氣**：兼顧科學準確性與親切易讀性；避免過度擬人化或誇大行銷詞彙，飼養難度與缺點須客觀呈現。

## 目錄結構與存檔位置規範

請 AI 代理在建立、移動或更新檔案時，嚴格遵守以下目錄分工：

- `raw/`：存放所有原始參考 PDF、公開飼養指南與未整理筆記（如 `比熊.pdf`、`哈士奇.pdf`）。
- `content/`：依物種分類存放**所有寵物介紹 Markdown 文章**，**之後新增或更新的所有相關品種介紹文章一律存進對應子資料夾中**：
  - `content/dogs/`：犬類介紹文章（如 `dog_bichon_frise.md`、`dog_siberian_husky.md`）
  - `content/cats/`：貓類介紹文章（如 `cat_tuxedo.md`，待擴充）
  - `content/small_mammals/`：小型哺乳類介紹文章（待擴充）
  - `content/birds/`：鳥類介紹文章（待擴充）
  - `content/reptiles/`：爬蟲類介紹文章（待擴充）
  - `content/fish/`：觀賞魚介紹文章（待擴充）
- `notes/`：嚴格依據專案現有資料回答使用者問題或彙整所產出的 `.md` 問答筆記。
- `slides_outline/`：依據 `notes/` 內容拆分產出的簡報逐頁大綱（Markdown）。
- `slides_html/`：依據簡報大綱與風格規範（`slides_html/STYLE_GUIDE.md`）製作的離線 HTML 簡報檔案，插畫原圖備份於 `slides_html/assets/`。
- `pets_master.json` & `pets_master.csv`：位於專案根目錄的主要結構化資料集（CSV 須為 `utf-8-sig` 含 BOM 編碼，方便 Excel 直接開啟）。
- `index.md`：知識庫總索引，記錄各物種收錄進度、檔案路徑與更新日誌。

## 結構化資料集欄位規範

每筆寵物紀錄須包含以下核心欄位，並同時維護於 `pets_master.json` 與 `pets_master.csv`：

| 欄位名稱 | 資料型態 | 必填 | 說明與格式規範 |
| :--- | :--- | :--- | :--- |
| `id` | string | 是 | 唯一識別碼，格式為 `<物種>_<品種>`（例：`dog_bichon_frise`、`dog_siberian_husky`、`cat_tuxedo`） |
| `species` | string | 是 | 物種分類：`dog`、`cat`、`small_mammal`、`bird`、`reptile`、`fish` |
| `breed_zh` | string | 是 | 繁體中文常見名稱（例：比熊犬、哈士奇、賓士貓） |
| `breed_en` | string | 是 | 英文標準名稱（例：Bichon Frise、Siberian Husky、Tuxedo Cat） |
| `size_tier` | string | 是 | 體型分級：`mini`、`small`、`medium`、`large`、`giant` |
| `adult_weight_kg` | object | 是 | 成體體重範圍，含 `min` 與 `max` 數值（公斤） |
| `lifespan_years` | object | 是 | 平均壽命範圍，含 `min` 與 `max` 整數（年） |
| `beginner_friendly` | integer | 是 | 新手友善度評分（`1` 到 `5` 的整數，`5` 為最適合新手） |
| `exercise_need` | string | 是 | 活動量需求：`low`、`medium`、`high` |
| `grooming_need` | string | 是 | 清潔與美容頻率：`low`、`medium`、`high` |
| `temperament_tags` | array | 是 | 3 至 6 個性格關鍵字陣列 |
| `climate_suitability_tw` | string | 是 | 台灣濕熱氣候適應評估與環境建議 |
| `common_health_issues` | array | 是 | 常見好發或遺傳疾病列表，須附簡短預防重點 |
| `initial_cost_twd` | object | 是 | 初期建置或市場參考價估算，`min` / `max` 整數（新台幣） |
| `monthly_cost_twd` | object | 是 | 每月固定開銷估算，`min` / `max` 整數（新台幣；若來源未明列金額須設 `0` 並附 `note` 說明） |
| `adoption_notes` | string | 否 | 台灣領養管道、晶片登記或法規備註 |
| `sources` | array | 是 | 參考資料來源網址、專欄標題或 `raw/` 檔名列表 |
| `last_updated` | string | 是 | 最後更新日期，格式為 `YYYY-MM-DD` |

## 寵物介紹文章撰寫模板

在 `content/<species>/<id>.md` 建立介紹文章時，請依下列 8 個章節順序撰寫：

1. **基本檔案摘要**
2. **外觀與生理特徵**
3. **性格與日常互動**
4. **台灣飼養環境建議**
5. **飲食、清潔與醫療照護**（含醫療免責聲明）
6. **預算與時間投入評估**
7. **適合族群與飼養前檢核表**
8. **參考來源**

## 問答筆記（`notes/`）與簡報（`slides_outline/`、`slides_html/`）規範

1. **嚴格接地資料夾現有內容**：筆記正文與簡報內容必須**完全依照專案資料夾內現有資料**整理撰寫，不得混入未收錄於資料夾內的外部知識，並明確標註引用來源檔名。
2. **資料缺口處理原則（只給連結、不寫入內容）**：若資料夾內沒有足夠資料回答部分子題，可於筆記末段列出「待補查之外部參考連結」，供使用者審閱後決定是否正式收錄至 `raw/`。
3. **HTML 簡報視覺風格**：預設套用 `slides_html/STYLE_GUIDE.md` 的「粉彩天藍 × 鼠尾草」溫暖水彩插畫風，支援鍵盤與按鈕翻頁，並將圖片以 Base64 內嵌於單檔 HTML 中。

## 品質護欄與禁止事項

- **醫療免責原則**：禁止提供具體處方藥劑量或診斷結論；遇異常症狀說明時，一律提醒應由合格獸醫師診斷。
- **編碼與檔名規範**：CSV 一律採用 `utf-8-sig`（含 BOM）；Markdown 與 JSON 採用 UTF-8；檔名與識別碼僅使用小寫英數字與底線（`_`）。
- **禁止虛構來源**：只能放入實際查證過的有效來源，不可編造網址或不存在的機構名稱。