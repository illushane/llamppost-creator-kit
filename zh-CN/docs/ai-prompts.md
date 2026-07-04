# AI 辅助撰写模板的 Prompt 集

语言：简体中文 | [English](../../en/docs/ai-prompts.md) | [繁體中文](../../zh-TW/docs/ai-prompts.md) | [日本語](../../ja/docs/ai-prompts.md)

这份文档提供**四支现成的 Prompt**，让你可以用 Claude、ChatGPT、Gemini 或任何 AI 助手辅助你填写 llamppost 模板。复制整段 Prompt，粘贴到你的 AI 对话里即可。

---

## 怎么用这份 Prompt 集

### 场景 A：你的 AI 可以读本地文件

例如 Claude Code、Cursor、Codex CLI、Codeium Chat——这类工具可以直接读取 repo 里的文件。

**做法**：
1. 把整个 `llamppost-creator-kit/` 文件夹开在编辑器里
2. 复制下面对应的 Prompt，粘贴到 AI 对话
3. AI 会自己去读 `docs/`、`personas/`、`skills/` 底下的文件

### 场景 B：你的 AI 只能读对话内容

例如 chat.openai.com、claude.ai 网页版、Gemini web、手机 App 等。

**做法**：
1. 先把**下列文件的完整内容**粘贴到对话开头：
   - Avatar → `docs/avatar-creation-spec.md`
   - Skill → `docs/skill-template.md` + `skills/YOUR_SKILL_NAME/SKILL.md` + `skills/YOUR_SKILL_NAME/metadata.json` + `skills/EXAMPLE_social_marketing_post_ideas/SKILL.md` + `skills/EXAMPLE_social_marketing_post_ideas/metadata.json`
   - Persona → `docs/persona-template.md` + `personas/YOUR_AGENT_NAME/persona.md` + `personas/YOUR_AGENT_NAME/metadata.json` + `personas/EXAMPLE_pi_lang/persona.md` + `personas/EXAMPLE_pi_lang/metadata.json`
   - Agent（全套）→ `agents/YOUR_AGENT_NAME/` 整包（README.md + persona.md + SKILL.md + avatar/metadata.json）+ 上面三组
2. 再复制对应的 Prompt 粘贴到对话
3. AI 会根据你贴的文件内容与规则对你发问

---

## Prompt A：只上架 Avatar

适用场景：你已经有一张角色图（或准备生成一张），需要产出 `metadata.json` 并确认版权合规。

### 已经有图了？两分钟搞定（不用跑 AI 问答）

如果你的角色图已经做好，只是需要 metadata，那你不需要下面的 Prompt——自己填这个文件就行：

1. 把你的图放进文件夹，命名为 `avatar.png`（PNG，正方形，至少 512×512）。
2. 打开 `metadata.json` 填这几项——就这些：
   - `avatar_id`——英文小写 + 下划线，例如 `night_wolf_001`（文件夹代称，不是标题）
   - `name`——角色的显示名称／上架标题，任何语言皆可，例如 `周予衡`、`Signal`
   - `collection`——你的系列名，例如 `weekday_workers`
   - `listing_description`——2–3 句：买家会得到什么 + 角色的调性（这是上架页会显示的内容——别留空）
   - `species` / `universe` / `realm`——从 `docs/avatar-creation-spec.md` 的枚举值里挑
   - `base`——`original`（你自己的作品）或授权 IP 名称
   - `creation_method`——作品怎么产出的：`original` / `original_ai_extended` / `ai_generated`（见规格；前两者会获得真品标识）
   - `traits`——几个视觉标签（头发／风格／表情）
   - `rights.creator`——你的 creator id
3. 上传文件夹。完成。

想让 AI 根据描述帮你填？那就改用下面整段。

### 完整辅助版

复制下面整段：

```
我要在 llamppost 平台上架一个 Avatar（角色图像）。请协助我产出 metadata.json 并确认版权合规。

请先读以下文件了解规则（如果你是本地 AI）：
- docs/avatar-creation-spec.md（完整规格与版权政策）
- README.md「重要：文件夹与 ID 必须是英文」区块

然后请依序问我以下问题，一次问一题，等我回答后再问下一题：

1. 你想上传的 Avatar 是什么样的角色？用 1–3 句描述外观、氛围、背景故事
2. 这个 Avatar 属于哪个系列（collection）？你打算在这个系列下放几个相关 Avatar？
3. 角色是什么物种（species）？（human / robot / animal / spirit / 其他）
4. 世界设定（universe）：modern / ancient / future / alternate？
5. 所属领域（realm）：earth / outer_space / heaven / hell？
6. 图片来源：原创、授权 IP、还是公共领域？
7. 如果是授权 IP：IP 名称是什么？你是否已经有授权文件？
8. 视觉特征（traits）：头发、服装、表情、配件、其他——至少 3 个
9. 你希望这个 Avatar 的 avatar_id 叫什么？
10. 市集商品描述：用 2–3 句讲买家会得到什么、以及角色的调性。这段会显示在商品页，并存进 metadata.json 的 `listing_description` 字段——必填，别留空。

问完之后，请输出：
- 完整的 metadata.json（符合 docs/avatar-creation-spec.md 的 schema）
- 建议的文件夹路径（例如 `avatars/night_wolf_001/`）
- 提交前的版权与内容合规检查清单

硬性规则（绝对不可违反）：
- avatar_id 与文件夹名称必须是**英文小写 + 数字 + 下划线**——不可有中文、大写、空格或连字符
- 不可使用 EXAMPLE_ 或 YOUR_ 前缀（这是 kit 保留字，Portal 会拒绝）
- universe 与 realm 字段不可直接写 IP 名称——要填 modern/ancient/future/alternate 这类枚举值
- 如果涉及授权 IP，请在输出里明确提醒我上传时必须附授权文件
- 如果图片可能涉及未成年人，请明确提醒我未成年人性化内容是零容忍政策
- 图片规格：至少 512×512，建议 1024×1024，PNG，1:1
```

---

## Prompt B：只上架 Skill

适用场景：你有一个清楚的 workflow 或服务，想单独上架一个 Skill（不绑定特定 Persona）。

复制下面整段：

```
我要在 llamppost 平台上架一个 Skill（技能）。请协助我填写完整的 SKILL.md。

请先读以下文件了解规则（如果你是本地 AI）：
- docs/skill-template.md（完整字段说明）
- skills/YOUR_SKILL_NAME/SKILL.md（空白模板）
- skills/EXAMPLE_social_marketing_post_ideas/SKILL.md（完整示例——看语气与结构）
- README.md「重要：文件夹与 ID 必须是英文」区块

然后请依序问我以下问题，一次问一题：

1. 这个 Skill 帮用户解决什么具体问题？用 1–2 句话告诉我核心用途
2. 最适合什么人用？（个人创业者、小团队、特定职业、特定场景）
3. 为什么要用这个 Skill，而不是自己直接问 AI？（独特价值是什么）
4. Workflow 大致有哪几步？（3–7 步，每步一个动作）
5. 用户需要提供什么东西才能开始？（列出所有必填 + 选填输入）
6. 用户最后会拿到什么具体的交付物？（请用数字与格式——「3 篇完整草稿」比「好几个想法」有说服力）
7. 这个 Skill 目前有哪些已知限制或不适用的场景？（诚实列出）
8. 你希望这个 Skill 的 skill_id 叫什么？（英文小写 + 下划线）
9. 主要分类（category）是什么？需要第二个次要分类吗？
10. title（显示名称）与 one_liner（搜索结果的第一句）你想怎么写？
11. base_price 想填 0（免费上架，Hatchling 试上架）还是付费（≥100 NT$）？

问完之后，请输出「两份文件」：
- `SKILL.md`——frontmatter 只放 `skill_id`，加上所有 body 区块
- `metadata.json`——上架字段：`skill_id`、`title`、`one_liner`、`version`、`base_price`、`languages`、`category`、`script_mode`、`listing_description`、`cover`、`banner`，以及嵌套的 `listing` 区块（`what_it_does` 字符串、`what_you_get` 字符串数组、`limitations` 字符串数组）
- 放进 `assets/` 的两张图规格：`cover-<skill_id>.png`（方形 1:1）+ `banner-<skill_id>.png`（宽 16:10），PNG 每张 2 MB 以内
- 建议的文件夹路径（例如 `skills/weekly_report_writer/`）
- 我还没想清楚但可以补强的地方（诚实指出）

硬性规则：
- 上架字段（title / one_liner / version / languages / category / script_mode / listing_description / listing.*）放进 `metadata.json`。`SKILL.md` frontmatter 只留 `skill_id`，不要把上架字段塞回 frontmatter。
- skill_id 与文件夹名称必须是**英文小写 + 数字 + 下划线**，且两者完全一致
- 不可使用 EXAMPLE_ 或 YOUR_ 前缀
- title、one_liner、body 内容可以使用任何语言（简中、繁中、英文、日文、任何语言）
- category 必须从 docs/skill-template.md 的清单挑，最多 2 个
- one_liner 不可用「AI」「智能型」「先进模型」这类模糊词——要讲用户能达成什么
- Known limitations 必须诚实列出（空白或假装没有问题是不行的）
- script_mode 默认用 workflow_only，除非你明确要附脚本
- 显示名称（title）可以有创意，但 skill_id 必须像 `weekly_report_writer` 这样的蛇形英文
- base_price 只允许 `0` 或 `≥100`（1–99 会被 Portal 拒绝）
- 单品 skill **不要**产出 compatible_personas 配对栏位——哪些 persona 跟它搭得好，推荐由平台依 category 自动处理（只有上架整组 Agent 时才需要双向绑定）
- 不要问我 tested_runtimes / tested_models / test_level——这些是 v1.5 后 deprecated，Portal 之后会自动测试填写
```

---

## Prompt C：只上架 Persona

适用场景：你有一个有辨识度的角色，想单独上架一个 Persona（不绑定特定 Skill）。

复制下面整段：

```
我要在 llamppost 平台上架一个 Persona（AI 人格）。请协助我填写完整的 persona.md。

请先读以下文件了解规则（如果你是本地 AI）：
- docs/persona-template.md（完整字段说明与 Voice Fingerprint schema）
- personas/YOUR_AGENT_NAME/persona.md（空白模板）
- personas/EXAMPLE_pi_lang/persona.md（完整示例——这是 Pi 狼，请看他的语气、5 段句子示例、3 段对话的写法）
- README.md「重要：文件夹与 ID 必须是英文」区块

然后请依序问我以下问题，一次问一题：

1. 这个角色的核心个性是什么？用 3–5 个形容词描述（例如：冷、嘲讽、行动优先、护短、坏嘴但温暖）
2. 这个角色是做什么的？（从 docs/persona-template.md 的 profession 清单挑 1 个——work 类或 companion/coach 类）
3. 这个角色最适合被召唤在什么场景？举 2–3 个具体例子
4. 这个角色**不适合**什么场景？（也要明讲——这能让用户更精准配对）
5. 角色的自称是什么？（例如「本狼」、「师傅」、「我」、「朕」）
6. 角色怎么称呼用户？（「你」、「老大」、「徒弟」）
7. 角色遇到用户反驳时会怎么处理？坚持、让步、还是绕路？
8. 角色遇到用户情绪低潮时会怎么处理？先共情、还是用行动处理情绪？
9. 对话示例的场景（1 段必填、2 段建议补上）：
    - 第一段（日常工作・必填）：角色在什么场景下被问问题？
    - 第二段（冲突／不同意・建议）：用户反驳什么？
    - 第三段（脆弱／情绪支持・建议）：用户分享了什么困难？
10. 靈魂素材（选填，但强烈建议——这是让角色有脊椎的东西）。请依序问我，每一段都接受「跳过」：
    - **核心信念**（这段会公开显示在上架页，买家安装前就会读到）：角色拿来衡量一切的 1 到 3 条信念是什么？
    - 它会替用户守住什么，就算没被要求？
    - 不管是谁来问，它都绝不帮的是什么？
    - 它在什么情况下会反对用户、而不是照办？
    - 形塑它判断的内在张力是什么？
    - 它怎么摆放自己对用户的位置（平辈、导师、直话直说的兄姐、安静的工具）？
11. 你希望这个 persona 的 persona_id 叫什么？（英文小写 + 下划线）
12. base_price 想填 0（免费上架，Hatchling 试上架）还是付费（≥100 NT$）？

问完之后，请依照 personas/EXAMPLE_pi_lang/ 的结构输出「两份文件」：
- `persona.md`——frontmatter 只放 `persona_id` + `profession`，加上完整 body
- `metadata.json`——上架字段：`persona_id`、`name`、`one_liner`、`version`、`base_price`、`languages`、`listing_description`、`cover`、`banner`（persona manifest 没有 title/category/script_mode/listing 区块）
- 放进 `assets/` 的两张图规格：`cover-<persona_id>.png`（1:1）+ `banner-<persona_id>.png`（16:10），PNG 每张 2 MB 以内
- Opening / During-work / Closing behavior 各 1–2 句
- 5 句 sentence examples（对应前面问的 5 个场景）
- 用户填写的灵魂素材段落：`## 核心信念`，再加上 `## 會保護什麼` / `## 絕不幫什麼` / `## 何時反對使用者` / `## 養成張力` / `## 與使用者的關係` 之中有回答的那几段。只放用户回答过的段落——没回答的就略过，不要自己编
- 至少 1 段必填对话（建议补满 3 段），每段都有 2–3 轮 User/Persona 交流
- 建议的文件夹路径（例如 `personas/night_wolf_strategist/`）

硬性规则：
- 上架字段（name / one_liner / languages / version / listing_description）放进 `metadata.json`。`persona.md` frontmatter 只留 `persona_id` + `profession`，不要把上架字段塞回 frontmatter。
- persona_id 与文件夹名称必须是**英文小写 + 数字 + 下划线**，且两者完全一致
- 不可使用 EXAMPLE_ 或 YOUR_ 前缀
- name（显示名称）、one_liner、所有 behavior 描述、对话、句子示例可以使用任何语言
- 若有补上多段对话，**语气必须一致**——这是 llamppost 跨模型一致性的核心卖点。如果读起来像不同的人，这个 persona 就废了
- 多段对话要涵盖**不同情绪 register**（routine / disagreement / vulnerability）——一段很长的单一场景对话不算多段
- 灵魂素材是选填。只写我实际回答的段落——不要编造我没给你的信念或拒绝
- 灵魂素材只能放**会改变角色判断**的东西，不是身世背景（不要写「喜欢咖啡、在海边长大」）
- `## 核心信念` 是**公开的**（安装前就显示在上架页）；其余五段灵魂是**私有的**（只到执行 prompt 与审核者）。不要在核心信念里放任何我不想让陌生人读到的东西
- base_price 只允许 `0` 或 `≥100`（1–99 会被 Portal 拒绝）
- 单品 persona **不要**产出 agent_skills / allowed_skill_categories 配对栏位——哪些 skill 跟它搭得好，推荐由平台依 profession 自动处理（只有上架整组 Agent 时才需要双向绑定）
- 不要问我 tested_runtimes / tested_models / test_level / model_fidelity / recommended_models / voice_fingerprint override——这些是 v1.5 后 deprecated 或由平台自动推导，Portal 之后会自动测试填写
```

---

## Prompt D：全套上架（Persona + Skill + Avatar）

适用场景：你要打造一个完整的角色商品——人格 + 技能 + 外观全都要，而且三者要相互呼应。

这个 Prompt 跟前面三支不同——它会先帮你定调整体设计，再分三阶段细化。

复制下面整段：

```
我要在 llamppost 平台上架一整套完整商品（Persona + Skill + Avatar），请协助我设计并填写全部三份文件。这三者必须相互呼应——不是三个不相关的东西。

请先读以下文件了解规则（如果你是本地 AI）：
- README.md（特别是「重要：文件夹与 ID 必须是英文」区块）
- docs/listing-ready-v1.md（上架指南全貌——特别是「发布 Agent」段落）
- docs/persona-template.md、docs/skill-template.md、docs/avatar-creation-spec.md
- agents/YOUR_AGENT_NAME/README.md（Agent 模板使用说明 + 双向绑定示例）
- agents/YOUR_AGENT_NAME/persona.md + SKILL.md + avatar/metadata.json（空白 Agent 模板）
- personas/EXAMPLE_pi_lang/persona.md（完整 Persona 示例）
- skills/EXAMPLE_social_marketing_post_ideas/SKILL.md（完整 Skill 示例）

这次不一次问完，请分四个阶段进行：

===== 阶段 1：先定调整体概念 =====

先不要问任何字段细节。请问我这三个问题：

1. 你想打造的角色是谁？用一句话讲（不超过 30 字）
2. 这个角色的核心价值：解决用户的什么问题？为什么是这个角色，而不是一般 AI？
3. 你预期的用户是谁？他们在什么场景下会召唤这个角色？

问完后，请输出一份 30 秒电梯简报（100 字内），让我确认方向对不对。
**等我说「方向 OK」后**，再进入阶段 2。

===== 阶段 2：填 Persona =====

用 Prompt C 的题目问我 Persona 细节（个性、三段对话场景，以及灵魂素材——尤其是**核心信念**，它会公开显示在上架页）。
写出完整的 persona.md 文件内容，包含 `## 核心信念` 段落，以及我有回答的其余灵魂段落。
输出后等我 review，我说 OK 再进阶段 3。

===== 阶段 3：填 Skill =====

基于刚才定好的 Persona 性格，帮我想：这个角色具体会提供什么 Skill？
（通常是 1 个最能展现角色独特价值的 skill——不是 10 个杂七杂八的）

然后用 Prompt B 的题目问我 Skill 细节。
写出完整的 SKILL.md 文件内容。

**重要（双向绑定）**：
- 这个 Skill 的 compatible_personas 字段必须包含刚才定义的 Persona 的 persona_id
- Persona 的 agent_skills 字段也必须包含这个 Skill 的 skill_id
- 两边必须同时更新，Portal 会验证对称性

输出后等我 review，我说 OK 再进阶段 4。

===== 阶段 4：填 Avatar =====

基于 Persona 的个性与氛围，帮我想 Avatar 的视觉方向：
- universe、realm、species 该怎么选才跟角色呼应？
- traits 应该强调哪些视觉元素？
- 这个 Avatar 跟 Persona 的语气是否一致？

然后用 Prompt A 的题目问我 Avatar 细节。
写出完整的 metadata.json 文件内容。

===== 最后：总览 =====

四个阶段都完成后，请输出一份上架前检查总览：
- 完整 Agent 文件夹结构（agents/<agent_name>/persona.md + SKILL.md + avatar/metadata.json）
- 建议的 agent 文件夹路径（例如 `agents/night_wolf_strategist/`）
- 双向绑定确认（Persona.agent_skills ↔ Skill.compatible_personas）
- 语气一致性检查（三份文件读起来像同一个角色吗？）
- 上架前的最终检查清单

硬性规则（前面三支 Prompt 的规则全部合并）：
- **Agent 不使用 listing `metadata.json`。** 这是跟单品 Skill / Persona 的关键差异：Agent 里所有上架字段（title、name、one_liner、category、languages、version、listing_description、script_mode）都留在 `persona.md` / `SKILL.md` 的 **frontmatter**。bundle 里唯一的 `metadata.json` 是 `avatar/metadata.json`（avatar schema）。不要在 Agent 根目录产生 listing `metadata.json` 或 `assets/` 的 cover/banner。
- persona_id、skill_id、avatar_id、文件夹名称都必须**英文小写 + 数字 + 下划线**
- 不可使用 EXAMPLE_ 或 YOUR_ 前缀
- 三个 ID 建议用共同前缀让它们看起来是一组（例如 `night_wolf_strategist` / `night_wolf_strategist_skill` / `night_wolf_strategist_001`）
- Persona ↔ Skill 的 agent_skills ↔ compatible_personas 必须双向绑定
- Agent 必须三者都齐（Persona + Skill + Avatar）。没有 Avatar 不能以 Agent 上架——告诉我要拆成单品还是先生成 Avatar
- 三个文件的语气、设定、世界观必须一致
- 灵魂素材是选填、且只在 persona 这一层——只写我回答的，绝不自己编。`## 核心信念` 公开显示在上架页；其余五段灵魂是私有的（只到执行 prompt 与审核者）
- persona **不绑它的 skill**——灵魂属于 persona，skill 是另一个可叠加的层；`agent_skills` ↔ `compatible_personas` 只标记搭配关系
- 每一阶段结束都要等我确认才进下一阶段——不要一口气全部生出来
- base_price 只允许 `0` 或 `≥100`（1–99 会被 Portal 拒绝）
- 不要问我 tested_models / test_level / model_fidelity / voice_fingerprint override——这些都已 deprecated 或由平台自动推导
```

---

## 通用提醒（所有 Prompt 都适用）

### 你的 AI 可能会犯的错

- **直接给你答案，不问问题** → 请回复：「请先按照 Prompt 的题目一题一题问我，不要自己假设」
- **给出 EXAMPLE_ 或 YOUR_ 前缀的 ID** → 请回复：「这是保留前缀，请重新命名为英文小写 + 下划线」
- **ID 里有中文、大写、空格或连字符** → 请回复：「ID 必须只有英文小写字母、数字、下划线」
- **跳过 known limitations** → 请回复：「请补上这个字段，就算只是空的也要明列」
- **多段对话写成类似的语气** → 请回复：「不同段要涵盖日常 / 冲突 / 脆弱不同 register，请重写」
- **塞 deprecated 字段（tested_models / model_fidelity / voice_fingerprint override 等）** → 请回复：「v1.5 后这些 deprecated，Portal 之后会自动填，现在不要塞」
- **base_price 填 1–99** → 请回复：「base_price 只允许 0 或 ≥100，请改」

### 你也应该检查的

在提交前，自己过一遍这个清单：
- [ ] 文件夹名称跟 `*_id` 字段**完全一致**
- [ ] ID 只有英文小写 + 数字 + 下划线
- [ ] 没有 `EXAMPLE_` 或 `YOUR_` 前缀
- [ ] 必填字段没有任何一个留空或留着模板默认值
- [ ] `base_price` 是 `0` 或 `≥100`
- [ ] 如果是 Persona + Skill 打包成一个 Agent，双向绑定都写好了
- [ ] Agent 上架时，`avatar/avatar.png` 已补上（不是只剩 placeholder）
- [ ] 语言切换区块（multi-language header）没有打到翻译的断层
- [ ] 没有 AI 硬塞进去的「希望这有帮助」这类客套话残留
