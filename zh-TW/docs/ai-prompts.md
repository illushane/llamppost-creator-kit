# AI 輔助撰寫模板的 Prompt 集

語言：繁體中文 | [English](../../en/docs/ai-prompts.md) | [简体中文](../../zh-CN/docs/ai-prompts.md) | [日本語](../../ja/docs/ai-prompts.md)

這份文件提供**四支現成的 Prompt**，讓你可以用 Claude、ChatGPT、Gemini 或任何 AI 助手輔助你填寫 llamppost 模板。複製整段 Prompt，貼到你的 AI 對話裡即可。

---

## 怎麼用這份 Prompt 集

### 情境 A：你的 AI 可以讀本地檔案

例如 Claude Code、Cursor、Codex CLI、Codeium Chat——這類工具可以直接讀取 repo 裡的檔案。

**做法**：
1. 把整個 `llamppost-creator-kit/` 資料夾開在編輯器裡
2. 複製下面對應的 Prompt，貼到 AI 對話
3. AI 會自己去讀 `docs/`、`personas/`、`skills/` 底下的檔案

### 情境 B：你的 AI 只能讀對話內容

例如 chat.openai.com、claude.ai 網頁版、Gemini web、手機 App 等。

**做法**：
1. 先把**下列檔案的完整內容**貼到對話開頭：
   - Avatar → `docs/avatar-creation-spec.md`
   - Skill → `docs/skill-template.md` + `skills/YOUR_SKILL_NAME/SKILL.md` + `skills/YOUR_SKILL_NAME/metadata.json` + `skills/EXAMPLE_social_marketing_post_ideas/SKILL.md` + `skills/EXAMPLE_social_marketing_post_ideas/metadata.json`
   - Persona → `docs/persona-template.md` + `personas/YOUR_AGENT_NAME/persona.md` + `personas/YOUR_AGENT_NAME/metadata.json` + `personas/EXAMPLE_pi_lang/persona.md` + `personas/EXAMPLE_pi_lang/metadata.json`
   - Agent（全套）→ `agents/YOUR_AGENT_NAME/` 整包（README.md + persona.md + SKILL.md + avatar/metadata.json）+ 上面三組
2. 再複製對應的 Prompt 貼到對話
3. AI 會根據你貼的檔案內容與規則對你發問

---

## Prompt A：只上架 Avatar

適用情境：你已經有一張角色圖（或準備生成一張），需要產出 `metadata.json` 並確認版權合規。

### 已經有圖了？兩分鐘搞定（不必跑 AI 問答）

如果你的角色圖已經完成、只差 metadata，那你根本不需要下面那段 Prompt——自己填一下檔案就好：

1. 把你的圖放進資料夾，命名為 `avatar.png`（PNG、正方形、至少 512×512）。
2. 打開 `metadata.json`，填這幾項——就這些：
   - `avatar_id`——英文小寫 + 底線，例如 `night_wolf_001`（資料夾代稱，不是標題）
   - `name`——角色的顯示名稱／上架標題，任何語言皆可，例如 `周予衡`、`Signal`
   - `collection`——你的系列名稱，例如 `weekday_workers`
   - `listing_description`——2–3 句：買家會得到什麼 + 角色的調性（這就是顯示在上架頁的描述，別留空）
   - `species` / `universe` / `realm`——從 `docs/avatar-creation-spec.md` 的枚舉值挑
   - `base`——`original`（你自己的作品）或授權 IP 名稱
   - `creation_method`——作品怎麼產出的：`original` / `original_ai_extended` / `ai_generated`（見規格；前兩者會取得真品標章）
   - `traits`——幾個視覺標籤（頭髮 / 風格 / 表情）
   - `rights.creator`——你的 creator id
3. 上傳資料夾。完成。

想讓 AI 從一段描述幫你填？那就改複製下面整段。

### 完整 AI 輔助版

複製下面整段：

```
我要在 llamppost 平台上架一個 Avatar（角色圖像）。請協助我產出 metadata.json 並確認版權合規。

請先讀以下檔案了解規則（如果你是本地 AI）：
- docs/avatar-creation-spec.md（完整規格與版權政策）
- README.md「重要：資料夾與 ID 必須是英文」區塊

然後請依序問我以下問題，一次問一題，等我回答後再問下一題：

1. 你想上傳的 Avatar 是什麼樣的角色？用 1–3 句描述外觀、氛圍、背景故事
2. 這個 Avatar 屬於哪個系列（collection）？你打算在這個系列下放幾個相關 Avatar？
3. 角色是什麼物種（species）？（human / robot / animal / spirit / 其他）
4. 世界設定（universe）：modern / ancient / future / alternate？
5. 所屬領域（realm）：earth / outer_space / heaven / hell？
6. 圖片來源：原創、授權 IP、還是公共領域？
7. 如果是授權 IP：IP 名稱是什麼？你是否已經有授權文件？
8. 視覺特徵（traits）：頭髮、服裝、表情、配件、其他——至少 3 個
9. 你希望這個 Avatar 的 avatar_id 叫什麼？
10. 市集上架描述：用 2–3 句講買家會得到什麼、以及角色的調性。這段會顯示在商品頁，會存進 metadata.json 的 `listing_description` 欄位——必填，別留空。

問完之後，請輸出：
- 完整的 metadata.json（符合 docs/avatar-creation-spec.md 的 schema）
- 建議的資料夾路徑（例如 `avatars/night_wolf_001/`）
- 送出前的版權與內容合規檢查清單

硬性規則（絕對不可違反）：
- avatar_id 與資料夾名稱必須是**英文小寫 + 數字 + 底線**——不可有中文、大寫、空格或連字號
- 不可使用 EXAMPLE_ 或 YOUR_ 前綴（這是 kit 保留字，Portal 會拒絕）
- universe 與 realm 欄位不可直接寫 IP 名稱——要填 modern/ancient/future/alternate 這類枚舉值
- 如果涉及授權 IP，請在輸出裡明確提醒我上傳時必須附授權文件
- 如果圖片可能涉及未成年人，請明確提醒我未成年人性化內容是零容忍政策
- 圖片規格：至少 512×512，建議 1024×1024，PNG，1:1
```

---

## Prompt B：只上架 Skill

適用情境：你有一個清楚的 workflow 或服務，想單獨上架一個 Skill（不綁定特定 Persona）。

複製下面整段：

```
我要在 llamppost 平台上架一個 Skill（技能）。請協助我填寫完整的 SKILL.md。

請先讀以下檔案了解規則（如果你是本地 AI）：
- docs/skill-template.md（完整欄位說明）
- skills/YOUR_SKILL_NAME/SKILL.md（空白模板）
- skills/EXAMPLE_social_marketing_post_ideas/SKILL.md（完整範例——看語氣與結構）
- README.md「重要：資料夾與 ID 必須是英文」區塊

然後請依序問我以下問題，一次問一題：

1. 這個 Skill 幫使用者解決什麼具體問題？用 1–2 句話告訴我核心用途
2. 最適合什麼人用？（個人創業者、小團隊、特定職業、特定情境）
3. 為什麼要用這個 Skill，而不是自己直接問 AI？（獨特價值是什麼）
4. Workflow 大致有哪幾步？（3–7 步，每步一個動作）
5. 使用者需要提供什麼東西才能開始？（列出所有必填 + 選填輸入）
6. 使用者最後會拿到什麼具體的交付物？（請用數字與格式——「3 篇完整草稿」比「好幾個想法」有說服力）
7. 這個 Skill 目前有哪些已知限制或不適用的情境？（誠實列出）
8. 你希望這個 Skill 的 skill_id 叫什麼？（英文小寫 + 底線）
9. 主要分類（category）是什麼？需要第二個次要分類嗎？
10. title（顯示名稱）與 one_liner（搜尋結果的第一句）你想怎麼寫？
11. base_price 想填 0（免費上架，Hatchling 試上架）還是付費（≥100 NT$）？

問完之後，請輸出「兩份檔案」：
- `SKILL.md`——frontmatter 只放 `skill_id`，加上所有 body 區塊
- `metadata.json`——上架欄位：`skill_id`、`title`、`one_liner`、`version`、`base_price`、`languages`、`category`、`script_mode`、`listing_description`、`cover`、`banner`，以及巢狀的 `listing` 區塊（`what_it_does` 字串、`what_you_get` 字串陣列、`limitations` 字串陣列）
- 放進 `assets/` 的兩張圖規格：`cover-<skill_id>.png`（方形 1:1）+ `banner-<skill_id>.png`（寬 16:10），PNG 每張 2 MB 以內
- 建議的資料夾路徑（例如 `skills/weekly_report_writer/`）
- 我還沒想清楚但可以補強的地方（誠實指出）

硬性規則：
- 上架欄位（title / one_liner / version / languages / category / script_mode / listing_description / listing.*）放進 `metadata.json`。`SKILL.md` frontmatter 只留 `skill_id`，不要把上架欄位塞回 frontmatter。
- skill_id 與資料夾名稱必須是**英文小寫 + 數字 + 底線**，且兩者完全一致
- 不可使用 EXAMPLE_ 或 YOUR_ 前綴
- title、one_liner、body 內容可以使用任何語言（繁中、英文、日文、任何語言）
- category 必須從 docs/skill-template.md 的清單挑，最多 2 個
- one_liner 不可用「AI」「智慧型」「先進模型」這類模糊詞——要講使用者能達成什麼
- Known limitations 必須誠實列出（空白或假裝沒有問題是不行的）
- script_mode 預設用 workflow_only，除非你明確要附腳本
- 顯示名稱（title）可以有創意，但 skill_id 必須像 `weekly_report_writer` 這樣的蛇形英文
- base_price 只允許 `0` 或 `≥100`（1–99 會被 Portal 拒絕）
- 不要問我 tested_runtimes / tested_models / test_level——這些是 v1.5 後 deprecated，Portal 之後會自動測試填寫
```

---

## Prompt C：只上架 Persona

適用情境：你有一個有辨識度的角色，想單獨上架一個 Persona（不綁定特定 Skill）。

複製下面整段：

```
我要在 llamppost 平台上架一個 Persona（AI 人格）。請協助我填寫完整的 persona.md。

請先讀以下檔案了解規則（如果你是本地 AI）：
- docs/persona-template.md（完整欄位說明與 Voice Fingerprint schema）
- personas/YOUR_AGENT_NAME/persona.md（空白模板）
- personas/EXAMPLE_pi_lang/persona.md（完整範例——這是 Pi 狼，請看他的語氣、5 段句子範例、3 段對話的寫法）
- README.md「重要：資料夾與 ID 必須是英文」區塊

然後請依序問我以下問題，一次問一題：

1. 這個角色的核心個性是什麼？用 3–5 個形容詞描述（例如：冷、嘲諷、行動優先、護短、壞嘴但溫暖）
2. 這個角色是做什麼的？（從 docs/persona-template.md 的 profession 清單挑 1 個——work 類或 companion/coach 類）
3. 這個角色最適合被召喚在什麼情境？舉 2–3 個具體例子
4. 這個角色**不適合**什麼情境？（也要明講——這能讓使用者更精準配對）
5. 角色的自稱是什麼？（例如「本狼」、「師傅」、「我」、「朕」）
6. 角色怎麼稱呼使用者？（「你」、「老大」、「徒弟」）
7. 角色遇到使用者反駁時會怎麼處理？堅持、讓步、還是繞路？
8. 角色遇到使用者情緒低潮時會怎麼處理？先共情、還是用行動處理情緒？
9. 對話範例的情境（1 段必填、2 段建議補上）：
    - 第一段（日常工作・必填）：角色在什麼情境下被問問題？
    - 第二段（衝突／不同意・建議）：使用者反駁什麼？
    - 第三段（脆弱／情緒支持・建議）：使用者分享了什麼困難？
10. 靈魂素材（選填，但強烈建議——這是讓角色有脊椎的東西）。請依序問我，每一段都接受「跳過」：
    - **核心信念**（這段會公開顯示在上架頁，買家安裝前就會讀到）：角色拿來衡量一切的 1 到 3 條信念是什麼？
    - 它會替使用者守住什麼，就算沒被要求？
    - 不管是誰來問，它都絕不幫的是什麼？
    - 它在什麼情況下會反對使用者、而不是照辦？
    - 形塑它判斷的內在張力是什麼？
    - 它怎麼擺放自己對使用者的位置（平輩、導師、直話直說的兄姐、安靜的工具）？
11. 你希望這個 persona 的 persona_id 叫什麼？（英文小寫 + 底線）
12. base_price 想填 0（免費上架，Hatchling 試上架）還是付費（≥100 NT$）？

問完之後，請依照 personas/EXAMPLE_pi_lang/ 的結構輸出「兩份檔案」：
- `persona.md`——frontmatter 只放 `persona_id` + `profession`，加上完整 body
- `metadata.json`——上架欄位：`persona_id`、`name`、`one_liner`、`version`、`base_price`、`languages`、`listing_description`、`cover`、`banner`（persona manifest 沒有 title/category/script_mode/listing 區塊）
- 放進 `assets/` 的兩張圖規格：`cover-<persona_id>.png`（1:1）+ `banner-<persona_id>.png`（16:10），PNG 每張 2 MB 以內
- Opening / During-work / Closing behavior 各 1–2 句
- 5 句 sentence examples（對應前面問的 5 個情境）
- 使用者填寫的靈魂素材段落：`## 核心信念`，再加上 `## 會保護什麼` / `## 絕不幫什麼` / `## 何時反對使用者` / `## 養成張力` / `## 與使用者的關係` 之中有回答的那幾段。只放使用者回答過的段落——沒回答的就略過，不要自己編
- 至少 1 段必填對話（建議補滿 3 段），每段都有 2–3 輪 User/Persona 交流
- 建議的資料夾路徑（例如 `personas/night_wolf_strategist/`）

硬性規則：
- 上架欄位（name / one_liner / languages / version / listing_description）放進 `metadata.json`。`persona.md` frontmatter 只留 `persona_id` + `profession`，不要把上架欄位塞回 frontmatter。
- persona_id 與資料夾名稱必須是**英文小寫 + 數字 + 底線**，且兩者完全一致
- 不可使用 EXAMPLE_ 或 YOUR_ 前綴
- name（顯示名稱）、one_liner、所有 behavior 描述、對話、句子範例可以使用任何語言
- 若有補上多段對話，**語氣必須一致**——這是 llamppost 跨模型一致性的核心賣點。如果讀起來像不同的人，這個 persona 就廢了
- 多段對話要涵蓋**不同情緒 register**（routine / disagreement / vulnerability）——一段很長的單一情境對話不算多段
- 靈魂素材是選填。只寫我實際回答的段落——不要編造我沒給你的信念或拒絕
- 靈魂素材只能放**會改變角色判斷**的東西，不是身家背景（不要寫「喜歡咖啡、在海邊長大」）
- `## 核心信念` 是**公開的**（安裝前就顯示在上架頁）；其餘五段靈魂是**私有的**（只到執行 prompt 與審核者）。不要在核心信念裡放任何我不想讓陌生人讀到的東西
- base_price 只允許 `0` 或 `≥100`（1–99 會被 Portal 拒絕）
- 不要問我 tested_runtimes / tested_models / test_level / model_fidelity / recommended_models / voice_fingerprint override——這些是 v1.5 後 deprecated 或由平台自動推導，Portal 之後會自動測試填寫
```

---

## Prompt D：全套上架（Persona + Skill + Avatar）

適用情境：你要打造一個完整的角色商品——人格 + 技能 + 外觀全都要，而且三者要相互呼應。

這個 Prompt 跟前面三支不同——它會先幫你定調整體設計，再分三階段細化。

複製下面整段：

```
我要在 llamppost 平台上架一整套完整商品（Persona + Skill + Avatar），請協助我設計並填寫全部三份檔案。這三者必須相互呼應——不是三個不相關的東西。

請先讀以下檔案了解規則（如果你是本地 AI）：
- README.md（特別是「重要：資料夾與 ID 必須是英文」區塊）
- docs/listing-ready-v1.md（上架指南全貌——特別是「發佈 Agent」段落）
- docs/persona-template.md、docs/skill-template.md、docs/avatar-creation-spec.md
- agents/YOUR_AGENT_NAME/README.md（Agent 模板使用說明 + 雙向綁定範例）
- agents/YOUR_AGENT_NAME/persona.md + SKILL.md + avatar/metadata.json（空白 Agent 模板）
- personas/EXAMPLE_pi_lang/persona.md（完整 Persona 範例）
- skills/EXAMPLE_social_marketing_post_ideas/SKILL.md（完整 Skill 範例）

這次不一次問完，請分四個階段進行：

===== 階段 1：先定調整體概念 =====

先不要問任何欄位細節。請問我這三個問題：

1. 你想打造的角色是誰？用一句話講（不超過 30 字）
2. 這個角色的核心價值：解決使用者的什麼問題？為什麼是這個角色，而不是一般 AI？
3. 你預期的使用者是誰？他們在什麼情境下會召喚這個角色？

問完後，請輸出一份 30 秒電梯簡報（100 字內），讓我確認方向對不對。
**等我說「方向 OK」後**，再進入階段 2。

===== 階段 2：填 Persona =====

用 Prompt C 的題目問我 Persona 細節（個性、三段對話情境，以及靈魂素材——尤其是**核心信念**，它會公開顯示在上架頁）。
寫出完整的 persona.md 檔案內容，包含 `## 核心信念` 段落，以及我有回答的其餘靈魂段落。
輸出後等我 review，我說 OK 再進階段 3。

===== 階段 3：填 Skill =====

基於剛才定好的 Persona 性格，幫我想：這個角色具體會提供什麼 Skill？
（通常是 1 個最能展現角色獨特價值的 skill——不是 10 個雜七雜八的）

然後用 Prompt B 的題目問我 Skill 細節。
寫出完整的 SKILL.md 檔案內容。

**重要（雙向綁定）**：
- 這個 Skill 的 compatible_personas 欄位必須包含剛才定義的 Persona 的 persona_id
- Persona 的 agent_skills 欄位也必須包含這個 Skill 的 skill_id
- 兩邊必須同時更新，Portal 會驗證對稱性

輸出後等我 review，我說 OK 再進階段 4。

===== 階段 4：填 Avatar =====

基於 Persona 的個性與氛圍，幫我想 Avatar 的視覺方向：
- universe、realm、species 該怎麼選才跟角色呼應？
- traits 應該強調哪些視覺元素？
- 這個 Avatar 跟 Persona 的語氣是否一致？

然後用 Prompt A 的題目問我 Avatar 細節。
寫出完整的 metadata.json 檔案內容。

===== 最後：總覽 =====

四個階段都完成後，請輸出一份上架前檢查總覽：
- 完整 Agent 資料夾結構（agents/<agent_name>/persona.md + SKILL.md + avatar/metadata.json）
- 建議的 agent 資料夾路徑（例如 `agents/night_wolf_strategist/`）
- 雙向綁定確認（Persona.agent_skills ↔ Skill.compatible_personas）
- 語氣一致性檢查（三份檔案讀起來像同一個角色嗎？）
- 上架前的最終檢查清單

硬性規則（前面三支 Prompt 的規則全部合併）：
- **Agent 不使用 listing `metadata.json`。** 這是跟單品 Skill / Persona 的關鍵差異：Agent 裡所有上架欄位（title、name、one_liner、category、languages、version、listing_description、script_mode）都留在 `persona.md` / `SKILL.md` 的 **frontmatter**。bundle 裡唯一的 `metadata.json` 是 `avatar/metadata.json`（avatar schema）。不要在 Agent 根目錄產生 listing `metadata.json` 或 `assets/` 的 cover/banner。
- persona_id、skill_id、avatar_id、資料夾名稱都必須**英文小寫 + 數字 + 底線**
- 不可使用 EXAMPLE_ 或 YOUR_ 前綴
- 三個 ID 建議用共同前綴讓它們看起來是一組（例如 `night_wolf_strategist` / `night_wolf_strategist_skill` / `night_wolf_strategist_001`）
- Persona ↔ Skill 的 agent_skills ↔ compatible_personas 必須雙向綁定
- Agent 必須三者都齊（Persona + Skill + Avatar）。沒有 Avatar 不能以 Agent 上架——告訴我要拆成單品還是先生成 Avatar
- 三個檔案的語氣、設定、世界觀必須一致
- 靈魂素材是選填、且只在 persona 這一層——只寫我回答的，絕不自己編。`## 核心信念` 公開顯示在上架頁；其餘五段靈魂是私有的（只到執行 prompt 與審核者）
- persona **不綁它的 skill**——靈魂屬於 persona，skill 是另一個可疊加的層；`agent_skills` ↔ `compatible_personas` 只標記搭配關係
- 每一階段結束都要等我確認才進下一階段——不要一口氣全部生出來
- base_price 只允許 `0` 或 `≥100`（1–99 會被 Portal 拒絕）
- 不要問我 tested_models / test_level / model_fidelity / voice_fingerprint override——這些都已 deprecated 或由平台自動推導
```

---

## 通用提醒（所有 Prompt 都適用）

### 你的 AI 可能會犯的錯

- **直接給你答案，不問問題** → 請回覆：「請先按照 Prompt 的題目一題一題問我，不要自己假設」
- **給出 EXAMPLE_ 或 YOUR_ 前綴的 ID** → 請回覆：「這是保留前綴，請重新命名為英文小寫 + 底線」
- **ID 裡有中文、大寫、空格或連字號** → 請回覆：「ID 必須只有英文小寫字母、數字、底線」
- **跳過 known limitations** → 請回覆：「請補上這個欄位，就算只是空的也要明列」
- **多段對話寫成類似的語氣** → 請回覆：「不同段要涵蓋日常 / 衝突 / 脆弱不同 register，請重寫」
- **塞 deprecated 欄位（tested_models / model_fidelity / voice_fingerprint override 等）** → 請回覆：「v1.5 後這些 deprecated，Portal 之後會自動填，現在不要塞」
- **base_price 填 1–99** → 請回覆：「base_price 只允許 0 或 ≥100，請改」

### 你也應該檢查的

在送出前，自己過一遍這個清單：
- [ ] 資料夾名稱跟 `*_id` 欄位**完全一致**
- [ ] ID 只有英文小寫 + 數字 + 底線
- [ ] 沒有 `EXAMPLE_` 或 `YOUR_` 前綴
- [ ] 必填欄位沒有任何一個留空或留著模板預設值
- [ ] `base_price` 是 `0` 或 `≥100`
- [ ] 如果是 Persona + Skill 綁定組合（Agent），雙向綁定都寫好了
- [ ] Agent 上架時，`avatar/avatar.png` 已補上（不是只剩 placeholder）
- [ ] 語言切換區塊（multi-language header）沒有打到翻譯的斷層
- [ ] 沒有 AI 硬塞進去的「希望這有幫助」這類客套話殘留
