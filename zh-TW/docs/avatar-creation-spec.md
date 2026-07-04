# Avatar 規格與政策（v1）

語言：繁體中文 | [English](../../en/docs/avatar-creation-spec.md) | [简体中文](../../zh-CN/docs/avatar-creation-spec.md) | [日本語](../../ja/docs/avatar-creation-spec.md)

要發佈一個 Avatar，你需要兩樣東西：**一張圖片（avatar.png）** 與 **一份 metadata 檔（metadata.json）**。

---

## 重要：資料夾與 avatar_id 必須是英文

我們的系統**只認英文識別符**。即使你的角色名稱與描述是繁體中文、日文或其他語言，下列項目永遠必須是英文：

- `avatar_id` 欄位
- `creator` 欄位
- 你建立的 avatar 資料夾名稱（`avatars/<your_avatar_id>/`）
- 格式限制：**小寫英文字母 + 數字 + 底線（`_`）**——不能有空格、大寫字母、連字號（`-`）或任何非英文字元

**範例：**

| 正確 | 錯誤 |
|---------|---------|
| `avatar_id: pi_lang_001` | `avatar_id: 派狼_001` |
| `avatars/night_wolf_001/` | `avatars/Night-Wolf-001/` |
| `creator: shane_lin` | `creator: 林申` |

`metadata.json` 的 `traits` 物件內容、`collection` 名稱、角色相關的描述都可以使用任何語言，但 `avatar_id`、`creator`、資料夾名稱必須是英文。

**保留前綴**：這份 kit 內有兩種保留前綴，你的真實上架**都不可以**使用——Portal 會拒絕：

- **`EXAMPLE_`**：參考範例檔案，只供閱讀——不要複製這種資料夾。
- **`YOUR_`**：空白模板，設計來給你複製改名的——複製後**務必**把資料夾與 `avatar_id` 改成你自己的英文小寫 ID。

---

## 快速檢查清單

送出前，請確認以下項目都已完成：

- [ ] `avatar.png` 至少 512×512，建議 1024×1024
- [ ] `metadata.json` 包含所有必填欄位
- [ ] `avatar_id` 對應到你的 creator ID（不與其他 Avatar 重複）
- [ ] 圖片是你的原創作品，或你持有有效的授權文件
- [ ] `universe` 與 `realm` 欄位不包含受版權保護的 IP 名稱
- [ ] 圖片不含任何涉及未成年人的性化內容

---

## A) 圖片要求

| 項目 | 規格 |
|------|------|
| 檔名 | `avatar.png`（固定，不可變更） |
| 最小尺寸 | 512 × 512 px |
| 建議尺寸 | 1024 × 1024 px |
| 格式 | PNG（未來可能支援 APNG） |
| 比例 | 正方形（1:1） |

> **注意：** 如果你送的是動畫格式（APNG），某些 AI 介面可能只會顯示靜態的第一幀。建議同時準備一份靜態版本。

---

## B) metadata.json 規格

放在與 `avatar.png` 同一個資料夾內，檔名固定為 `metadata.json`。

> **這是 avatar schema——不是 listing manifest。** Avatar 的 `metadata.json`（`avatar_id`、`collection`、`traits`、`rights` 等）跟單品 Skill / Persona 用的 listing `metadata.json`（`title` / `name`、`cover`、`banner`、`listing.*`）無關，別互相貼錯。Avatar 也沒有另外的 cover/banner——方形 1:1 的 `avatar.png` 本身就是圖片。

### 完整範例

```json
{
  "avatar_id": "kai_001",
  "name": "周予衡",
  "collection": "weekday_workers",
  "listing_description": "一個專注的平日上班族，你可以把他選進自己的短篇故事——沉穩、有點疲憊、但很可靠。",
  "species": "human",
  "universe": "modern",
  "realm": "earth",
  "base": "original",
  "creation_method": "original",
  "traits": {
    "hair": "short_dark",
    "style": "smart_casual",
    "expression": "focused",
    "accessory": "glasses"
  },
  "rights": {
    "source": "original",
    "creator": "your_creator_id",
    "license": "llamppost_standard"
  }
}
```

### 欄位說明

**必填欄位：**

| 欄位 | 型別 | 說明 |
|-------|------|-------------|
| `avatar_id` | string | 唯一 ID，小寫英文 + 底線，命名後不可更改。這是資料夾代稱，不是顯示標題。 |
| `name` | string | 角色的真名／顯示名稱——這是買家看到的**上架標題**（例如 `周予衡`、`Signal`）。與 `avatar_id` 不同：`name` 可以是任何語言，`avatar_id` 必須維持小寫英文。 |
| `collection` | string | 這個 Avatar 所屬的系列（你自己命名） |
| `listing_description` | string | 2–3 句市集商品描述，說明買家會得到什麼＋角色調性。別留空，否則你的 Avatar 上架時會沒有描述。 |
| `species` | string | 角色物種，例如 `human`、`robot`、`animal`、`spirit` |
| `universe` | enum | 世界設定（見下方 Enum 清單） |
| `realm` | enum | 所屬領域（見下方 Enum 清單） |
| `base` | string | `original` 或授權 IP 名稱 |
| `creation_method` | enum | 作品是怎麼產出的——`original`、`original_ai_extended`、`ai_generated` 三者擇一。見下方〈E) 創作方式與真品標章〉。 |
| `traits` | object | 視覺特徵（自由 key-value，至少 1 組） |
| `rights` | object | 版權資訊（見下方） |

**Enum 清單：**

`universe`（世界設定）：

| 值 | 說明 |
|-------|-------------|
| `modern` | 現代世界（當代設定） |
| `ancient` | 古代世界（歷史或幻想古風） |
| `future` | 未來世界（科幻、賽博龐克等） |
| `alternate` | 平行世界（異世界、轉生等） |

`realm`（所屬領域）：

| 值 | 說明 |
|-------|-------------|
| `earth` | 地球／人間界 |
| `outer_space` | 外太空 |
| `heaven` | 天界／神界 |
| `hell` | 冥界／地獄 |

**`rights` 物件欄位：**

| 欄位 | 說明 |
|-------|-------------|
| `source` | `original` 或 `licensed` 或 `public_domain` |
| `creator` | 你的 creator ID |
| `license` | `llamppost_standard`（大多數情況下用這個） |

---

## C) 版權政策

### 原創作品

如果圖片是你的原創作品（包含你全權持有著作權的委託作品），請將 `base` 設為 `original`，並將 `rights.source` 設為 `original`。

### 使用受保護的 IP

如果你的 Avatar 是基於現有的 IP（漫畫角色、遊戲角色、電影角色等）：

1. 把 `base` 欄位設成該 IP 的名稱（例如 `"base": "my_licensed_ip"`）
2. 送出時必須附上授權文件
3. `universe` 與 `realm` 欄位**不可以直接寫 IP 名稱**

> 範例：如果你持有某個 IP 的授權，請把 `base` 設成該 IP 名稱，但 `universe` 仍應填 `modern` / `ancient` 等——不能寫成該 IP 的世界名。

### 公共領域

如果角色來自公共領域（例如歷史人物、經典神話），請把 `rights.source` 設為 `public_domain`，並在 `traits` 裡清楚註明角色的出處。

---

## D) 未成年人安全政策

**零容忍。**

任何包含涉及未成年人性化內容的 Avatar，都會立刻被下架，且創作者帳號將被終止，不論理由為何。

如果角色的年齡模糊，視覺呈現應以成年為預設。

---

## E) 創作方式與真品標章

`creation_method` 欄位告訴買家這張圖本身是怎麼做出來的。它與 `base` / `rights`（描述 IP 出處）互相獨立——`creation_method` 純粹講圖像的產出方式。請從以下三個值擇一（英文值原樣保留，不要翻譯）：

| 值 | 意義 |
|-------|-------------|
| `original`（原創） | 由創作者本人親手繪製／創作——在 iPad、傳統媒材、或任何非 AI 的方式上完成。實際作品是由人畫的，不是 AI 生成的。 |
| `original_ai_extended`（原創 AI 延伸） | 以創作者原創／最初的角色設計為基礎，再用 AI 來算圖或延伸。不是純粹由 AI 憑空生成——底下有一份人做的原創。 |
| `ai_generated`（AI 生成） | 圖像由 AI 生成。 |

**真品標章：** 標記為 `original` 或 `original_ai_extended` 的 Avatar 會在上架頁面取得真品標章，向買家標示這份作品**並非純 AI 生成**。標記為 `ai_generated` 的 Avatar 不會有標章。請誠實選擇——不實標示 `creation_method` 會被下架。

---

## 資料夾結構範例

```
avatars/
  kai_001/
    avatar.png
    metadata.json
```

每一個 Avatar 都使用自己的資料夾，資料夾名稱與 `avatar_id` 一致。
