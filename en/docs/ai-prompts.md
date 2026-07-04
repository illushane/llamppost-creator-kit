# AI Prompts for Writing Templates

Language: English | [繁體中文](../../zh-TW/docs/ai-prompts.md) | [简体中文](../../zh-CN/docs/ai-prompts.md) | [日本語](../../ja/docs/ai-prompts.md)

This doc gives you **four ready-to-use prompts** for using Claude, ChatGPT, Gemini, or any AI assistant to help you fill out llamppost templates. Copy the whole prompt block and paste it into your AI chat.

---

## How to use these prompts

### Case A: your AI can read local files

For example, Claude Code, Cursor, Codex CLI, Codeium Chat — tools that can read files directly from a repo.

**What to do:**
1. Open the whole `llamppost-creator-kit/` folder in your editor
2. Copy the matching prompt below and paste it into your AI chat
3. The AI will go read `docs/`, `personas/`, `skills/` on its own

### Case B: your AI can only read the chat

For example, chat.openai.com, claude.ai web, Gemini web, mobile apps.

**What to do:**
1. First, paste the **full content of these files** at the start of the chat:
   - Avatar → `docs/avatar-creation-spec.md`
   - Skill → `docs/skill-template.md` + `skills/YOUR_SKILL_NAME/SKILL.md` + `skills/YOUR_SKILL_NAME/metadata.json` + `skills/EXAMPLE_social_marketing_post_ideas/SKILL.md` + `skills/EXAMPLE_social_marketing_post_ideas/metadata.json`
   - Persona → `docs/persona-template.md` + `personas/YOUR_AGENT_NAME/persona.md` + `personas/YOUR_AGENT_NAME/metadata.json` + `personas/EXAMPLE_pi_lang/persona.md` + `personas/EXAMPLE_pi_lang/metadata.json`
   - Agent (full set) → the whole `agents/YOUR_AGENT_NAME/` (README.md + persona.md + SKILL.md + avatar/metadata.json) plus the three sets above
2. Then paste the matching prompt
3. The AI will ask you questions based on the files and rules you pasted

---

## Prompt A: Avatar only

When to use: you already have a character image (or are about to generate one) and need to produce `metadata.json` and confirm rights compliance.

### Already have the image? The 2-minute path (no AI interview needed)

If your character image is done and you just need the metadata, you don't need the prompt below — just fill the file yourself:

1. Put your image in the folder as `avatar.png` (PNG, square, at least 512×512).
2. Open `metadata.json` and fill these — that's all there is:
   - `avatar_id` — lowercase English + underscores, e.g. `night_wolf_001` (folder slug, not the title)
   - `name` — the character's display name / listing title, any language, e.g. `Signal`, `周予衡`
   - `collection` — your series name, e.g. `weekday_workers`
   - `listing_description` — 2–3 sentences: what the buyer gets + the character's vibe (this is what shows on the listing — don't leave it blank)
   - `species` / `universe` / `realm` — pick from the enums in `docs/avatar-creation-spec.md`
   - `base` — `original` (your own art) or the licensed IP name
   - `creation_method` — how the art was made: `original` / `original_ai_extended` / `ai_generated` (see spec; the first two get an authenticity badge)
   - `traits` — a few visual tags (hair / style / expression)
   - `rights.creator` — your creator id
3. Upload the folder. Done.

Prefer to have an AI fill it from a description? Copy the whole block below instead.

### Full assisted version

Copy the whole block:

```
I want to publish an Avatar (character image) on the llamppost platform. Help me produce metadata.json and confirm rights compliance.

First read these files for the rules (if you're a local AI):
- docs/avatar-creation-spec.md (full spec and rights policy)
- README.md "Important: folder and ID names must be English" section

Then ask me the following questions in order, one at a time, waiting for my answer before moving to the next:

1. What kind of character is the Avatar you want to upload? Describe in 1–3 sentences: look, vibe, backstory
2. Which collection does this Avatar belong to? How many related Avatars do you plan to place under this collection?
3. What species is the character? (human / robot / animal / spirit / other)
4. Universe: modern / ancient / future / alternate?
5. Realm: earth / outer_space / heaven / hell?
6. Image source: original, licensed IP, or public domain?
7. If licensed IP: what's the IP name? Do you already have the license documents?
8. Visual traits: hair, outfit, expression, accessories, other — at least 3
9. What avatar_id do you want for this Avatar?
10. Marketplace listing description: 2–3 sentences on what the buyer gets and the character's vibe. This shows on the product page and is saved as `listing_description` in metadata.json — required, don't leave it blank.

After the questions, output:
- The complete metadata.json (matching the schema in docs/avatar-creation-spec.md)
- A suggested folder path (e.g., `avatars/night_wolf_001/`)
- A pre-submission rights + content compliance checklist

Hard rules (never violate):
- avatar_id and folder name must be **lowercase English + digits + underscores** — no Chinese, no uppercase, no spaces, no hyphens
- Do not use EXAMPLE_ or YOUR_ prefixes (kit-reserved; Portal will reject)
- universe and realm fields cannot directly contain an IP name — they must be enums like modern/ancient/future/alternate
- If licensed IP is involved, explicitly remind me to attach the license docs at upload
- If the image might involve minors, explicitly remind me that minor sexualization is a zero-tolerance policy
- Image spec: at least 512×512, 1024×1024 recommended, PNG, 1:1
```

---

## Prompt B: Skill only

When to use: you have a clear workflow or service and want to publish a Skill on its own (not bound to a specific Persona).

Copy the whole block:

```
I want to publish a Skill on the llamppost platform. Help me fill out the complete SKILL.md.

First read these files for the rules (if you're a local AI):
- docs/skill-template.md (full field reference)
- skills/YOUR_SKILL_NAME/SKILL.md (blank template)
- skills/EXAMPLE_social_marketing_post_ideas/SKILL.md (full example — look at the tone and structure)
- README.md "Important: folder and ID names must be English" section

Then ask me the following questions in order, one at a time:

1. What concrete problem does this Skill solve for the user? Tell me the core use in 1–2 sentences
2. Who's it best for? (solo founders, small teams, specific roles, specific situations)
3. Why use this Skill instead of just asking AI directly? (what's the unique value)
4. What are the main workflow steps? (3–7 steps, one action per step)
5. What does the user need to provide to get started? (list all required + optional inputs)
6. What concrete deliverable does the user end up with? (use numbers and formats — "3 full drafts" is more convincing than "some ideas")
7. What are this Skill's current known limits or non-applicable situations? (list honestly)
8. What skill_id do you want for this Skill? (lowercase English + underscores)
9. What's the primary category? Do you want a secondary?
10. How do you want to write the title (display name) and one_liner (first line in search results)?
11. Do you want base_price to be 0 (free Hatchling trial) or paid (≥100 NT$)?

After the questions, output BOTH files:
- `SKILL.md` — frontmatter with ONLY `skill_id`, plus all body sections
- `metadata.json` — the listing fields: `skill_id`, `title`, `one_liner`, `version`, `base_price`, `languages`, `category`, `script_mode`, `listing_description`, `cover`, `banner`, and the nested `listing` block (`what_it_does` string, `what_you_get` string[], `limitations` string[])
- A spec for the two images to drop into `assets/`: `cover-<skill_id>.png` (square 1:1) + `banner-<skill_id>.png` (wide 16:10), PNG under 2 MB
- Suggested folder path (e.g., `skills/weekly_report_writer/`)
- Things I haven't thought through that could be reinforced (be honest)

Hard rules:
- Listing fields (title / one_liner / version / languages / category / script_mode / listing_description / listing.*) go in `metadata.json`. `SKILL.md` frontmatter keeps ONLY `skill_id`. Don't put listing fields back in the frontmatter.
- skill_id and folder name must be **lowercase English + digits + underscores**, and the two must match exactly
- Do not use EXAMPLE_ or YOUR_ prefixes
- title, one_liner, body content can be in any language (Traditional Chinese, English, Japanese, anything)
- category must be picked from the list in docs/skill-template.md, up to 2
- one_liner must not use vague words like "AI" / "smart" / "advanced model" — say what the user can achieve
- Known limitations must be listed honestly (blank or pretending there's no issue is not allowed)
- script_mode defaults to workflow_only unless you're explicitly shipping a script
- Display name (title) can be creative, but skill_id must be snake_case English like `weekly_report_writer`
- base_price only allows `0` or `≥100` (1–99 will be rejected by Portal)
- Don't ask me about tested_runtimes / tested_models / test_level — these are deprecated in v1.5, Portal will auto-fill via testing later
```

---

## Prompt C: Persona only

When to use: you have a distinctive character and want to publish a Persona on its own (not bound to a specific Skill).

Copy the whole block:

```
I want to publish a Persona (AI character) on the llamppost platform. Help me fill out the complete persona.md.

First read these files for the rules (if you're a local AI):
- docs/persona-template.md (full field reference and Voice Fingerprint schema)
- personas/YOUR_AGENT_NAME/persona.md (blank template)
- personas/EXAMPLE_pi_lang/persona.md (full example — this is Pi Lang; look at his tone, 5 sentence examples, 3 dialogues)
- README.md "Important: folder and ID names must be English" section

Then ask me the following questions in order, one at a time:

1. What's the character's core personality? Describe in 3–5 adjectives (e.g., cool, sarcastic, action-first, protective, sharp-tongued but warm)
2. What does this character do? (Pick 1 from the profession list in docs/persona-template.md — work type or companion/coach type)
3. What situations is this character best summoned for? Give 2–3 concrete examples
4. What situations is this character **not** suited for? (Be explicit — this helps users match better)
5. How does the character refer to itself? (e.g., "本狼", "師傅", "I", "we")
6. How does the character address the user? ("you", "boss", "kid")
7. How does the character handle pushback from the user? Hold the line, yield, or pivot?
8. How does the character handle user emotional lows? Empathize first, or handle emotion through action?
9. Dialogue example scenarios (1 required, 2 recommended):
    - First (routine work, required): what situation is the character asked about?
    - Second (conflict / disagreement, recommended): what does the user push back on?
    - Third (vulnerability / emotional support, recommended): what hard thing does the user share?
10. Soul material (optional but strongly recommended — this is what gives the character a spine). Ask me in order, and accept "skip" for any:
    - **Core beliefs** (this becomes PUBLIC on the listing page — buyers read it before installing): what 1–3 convictions does the character measure everything against?
    - What does it protect for the user, even unasked?
    - What will it never help with, no matter who asks?
    - When does it push back on the user instead of complying?
    - What internal tension shapes its judgment?
    - How does it position itself toward the user (peer, mentor, blunt older sibling, quiet tool)?
11. What persona_id do you want for this persona? (lowercase English + underscores)
12. Do you want base_price to be 0 (free Hatchling trial) or paid (≥100 NT$)?

After the questions, output BOTH files, following the structure of personas/EXAMPLE_pi_lang/:
- `persona.md` — frontmatter with ONLY `persona_id` + `profession`, plus the full body
- `metadata.json` — the listing fields: `persona_id`, `name`, `one_liner`, `version`, `base_price`, `languages`, `listing_description`, `cover`, `banner` (persona manifests have NO title/category/script_mode/listing block)
- A spec for the two images for `assets/`: `cover-<persona_id>.png` (1:1) + `banner-<persona_id>.png` (16:10), PNG under 2 MB
- Opening / During-work / Closing behavior, 1–2 sentences each
- 5 sentence examples (matching the 5 situations from earlier)
- The Soul material sections the user filled in: `## 核心信念` (Core beliefs) plus any of `## 會保護什麼` / `## 絕不幫什麼` / `## 何時反對使用者` / `## 養成張力` / `## 與使用者的關係`. Only include sections the user answered — skip the rest, don't invent.
- At least 1 required dialogue (3 recommended), each with 2–3 turns of User/Persona exchange
- Suggested folder path (e.g., `personas/night_wolf_strategist/`)

Hard rules:
- Listing fields (name / one_liner / languages / version / listing_description) go in `metadata.json`. `persona.md` frontmatter keeps ONLY `persona_id` + `profession`. Don't put listing fields back in the frontmatter.
- persona_id and folder name must be **lowercase English + digits + underscores**, and the two must match exactly
- Do not use EXAMPLE_ or YOUR_ prefixes
- name (display name), one_liner, all behavior descriptions, dialogues, sentence examples can be in any language
- If you write multiple dialogues, **the tone must be consistent** — this is llamppost's core selling point for cross-model consistency. If they read like different people, the persona is broken
- Multiple dialogues must cover **different emotional registers** (routine / disagreement / vulnerability) — one long single-situation dialogue does not count as multiple
- Soul material is optional. Only write the sections I actually answer — don't invent beliefs or refusals I didn't give you
- Soul material must contain only things that **change the character's judgment**, not background trivia (no "loves coffee, grew up by the sea")
- `## 核心信念` (Core beliefs) is **public** (shows on the listing page before install); the other five soul sections are **private** (runtime + reviewer only). Don't put anything in 核心信念 that I wouldn't want a stranger to read
- base_price only allows `0` or `≥100` (1–99 will be rejected by Portal)
- Don't ask me about tested_runtimes / tested_models / test_level / model_fidelity / recommended_models / voice_fingerprint override — these are deprecated in v1.5 or auto-derived by the platform, Portal will fill them via testing later
```

---

## Prompt D: Full Agent (Persona + Skill + Avatar)

When to use: you want to build a complete character product — personality + skill + look, all three, and the three need to resonate.

This prompt is different from the previous three — it first helps you lock in the overall design, then refines in three stages.

Copy the whole block:

```
I want to publish a complete Agent on the llamppost platform (Persona + Skill + Avatar). Help me design and fill out all three files. The three must resonate — not three unrelated things.

First read these files for the rules (if you're a local AI):
- README.md (especially "Important: folder and ID names must be English")
- docs/listing-ready-v1.md (full listing guide — especially the "Publishing an Agent" section)
- docs/persona-template.md, docs/skill-template.md, docs/avatar-creation-spec.md
- agents/YOUR_AGENT_NAME/README.md (Agent template usage + bidirectional binding example)
- agents/YOUR_AGENT_NAME/persona.md + SKILL.md + avatar/metadata.json (blank Agent template)
- personas/EXAMPLE_pi_lang/persona.md (full Persona example)
- skills/EXAMPLE_social_marketing_post_ideas/SKILL.md (full Skill example)

Don't ask everything at once. Run this in four stages:

===== Stage 1: lock the overall concept =====

Don't ask about any field details yet. Ask me these three questions:

1. Who's the character you want to build? In one sentence (under 30 chars)
2. The character's core value: what user problem does it solve? Why this character, not a generic AI?
3. Who are your expected users? In what situation would they summon this character?

After my answers, output a 30-second elevator pitch (under 100 chars) to confirm we're aligned.
**Wait until I say "direction's good"** before moving to Stage 2.

===== Stage 2: fill the Persona =====

Use Prompt C's questions to ask me about Persona details (personality, the three dialogue scenarios, and the Soul material — especially **Core beliefs**, which becomes public on the listing page).
Write the complete persona.md content, including the `## 核心信念` (Core beliefs) section and any other soul sections I answered.
After output, wait for my review, then move to Stage 3 once I say OK.

===== Stage 3: fill the Skill =====

Based on the Persona we just defined, help me think: what Skill would this character specifically offer?
(Usually 1 skill that best showcases the character's unique value — not 10 scattered ones)

Then use Prompt B's questions to ask me about Skill details.
Write the complete SKILL.md content.

**Important (bidirectional binding)**:
- This Skill's compatible_personas field must include the persona_id we just defined
- The Persona's agent_skills field must include this Skill's skill_id
- Both sides must be updated together — Portal verifies the symmetry

After output, wait for my review, then move to Stage 4 once I say OK.

===== Stage 4: fill the Avatar =====

Based on the Persona's personality and vibe, help me think about the Avatar's visual direction:
- How should universe, realm, species be chosen to resonate with the character?
- What visual elements should traits emphasize?
- Does this Avatar match the Persona's tone?

Then use Prompt A's questions to ask me about Avatar details.
Write the complete metadata.json content.

===== Finally: overview =====

After all four stages, output a pre-launch checklist overview:
- Complete Agent folder structure (agents/<agent_name>/persona.md + SKILL.md + avatar/metadata.json)
- Suggested Agent folder path (e.g., `agents/night_wolf_strategist/`)
- Bidirectional binding confirmation (Persona.agent_skills ↔ Skill.compatible_personas)
- Tone consistency check (do all three files read like the same character?)
- Final pre-launch checklist

Hard rules (combining all three previous prompts):
- **Agents do NOT use a listing `metadata.json`.** This is the key difference from standalone Skills/Personas: in an Agent, keep ALL listing fields (title, name, one_liner, category, languages, version, listing_description, script_mode) in the `persona.md` / `SKILL.md` **frontmatter**. The only `metadata.json` in the bundle is `avatar/metadata.json` (avatar schema). Do NOT emit a listing `metadata.json` or an `assets/` cover/banner pair at the Agent root.
- persona_id, skill_id, avatar_id, folder names must all be **lowercase English + digits + underscores**
- Do not use EXAMPLE_ or YOUR_ prefixes
- All three IDs should share a common prefix to look like one set (e.g., `night_wolf_strategist` / `night_wolf_strategist_skill` / `night_wolf_strategist_001`)
- Persona ↔ Skill's agent_skills ↔ compatible_personas must be bidirectionally bound
- An Agent requires all three (Persona + Skill + Avatar). Without an Avatar, you can't ship as an Agent — tell me to either split into standalones or generate an Avatar first
- The three files' tone, setting, worldview must be consistent
- Soul material is optional and persona-level only — only write what I answer, never invent it. `## 核心信念` (Core beliefs) is public on the listing page; the other five soul sections are private (runtime + reviewer only)
- A persona is **not bound to its skill** — the soul belongs to the persona, the skill is a separate stackable layer; `agent_skills` ↔ `compatible_personas` only marks the pairing
- Wait for my confirmation after each stage — don't generate everything in one shot
- base_price only allows `0` or `≥100` (1–99 will be rejected by Portal)
- Don't ask me about tested_models / test_level / model_fidelity / voice_fingerprint override — these are all deprecated or auto-derived by the platform
```

---

## General reminders (apply to all prompts)

### Mistakes your AI might make

- **Gives you answers without asking questions** → Reply: "Please follow the prompt questions one at a time, don't assume on your own"
- **Gives an ID with the EXAMPLE_ or YOUR_ prefix** → Reply: "That's a reserved prefix, rename to lowercase English + underscores"
- **ID contains Chinese, uppercase, spaces, or hyphens** → Reply: "ID must be only lowercase English letters, digits, and underscores"
- **Skips known limitations** → Reply: "Please fill in this field — even if blank, list it explicitly"
- **Writes multiple dialogues in a similar tone** → Reply: "Different dialogues must cover routine / conflict / vulnerability registers, please rewrite"
- **Stuffs deprecated fields (tested_models / model_fidelity / voice_fingerprint override, etc.)** → Reply: "These are deprecated in v1.5, Portal will auto-fill later — don't stuff them in"
- **Fills base_price as 1–99** → Reply: "base_price only allows 0 or ≥100, please fix"

### Things you should also check

Before submitting, run yourself through this list:
- [ ] Folder name and `*_id` field **match exactly**
- [ ] ID is only lowercase English + digits + underscores
- [ ] No `EXAMPLE_` or `YOUR_` prefix
- [ ] No required field left blank or with template defaults
- [ ] `base_price` is `0` or `≥100`
- [ ] If it's a Persona + Skill Agent, bidirectional binding is set on both sides
- [ ] For Agent listings, `avatar/avatar.png` is in place (not just placeholder)
- [ ] Multi-language header section isn't broken by translation drift
- [ ] No AI-inserted "hope this helps" politeness leftovers
