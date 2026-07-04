# AI 補助でテンプレートを書くためのプロンプト集

言語：日本語 | [English](../../en/docs/ai-prompts.md) | [繁體中文](../../zh-TW/docs/ai-prompts.md) | [简体中文](../../zh-CN/docs/ai-prompts.md)

このドキュメントは**すぐに使える 4 つのプロンプト**を提供し、Claude、ChatGPT、Gemini、または任意の AI アシスタントを使って llamppost テンプレートの記入を手伝ってもらえます。プロンプト全体をコピーして、AI チャットに貼り付けてください。

---

## プロンプト集の使い方

### シチュエーション A：あなたの AI がローカルファイルを読める

例：Claude Code、Cursor、Codex CLI、Codeium Chat——この種のツールは repo 内のファイルを直接読み取れます。

**やり方**：
1. `llamppost-creator-kit/` フォルダ全体をエディタで開く
2. 下の対応するプロンプトをコピーして AI チャットに貼り付け
3. AI が自分で `docs/`、`personas/`、`skills/` 配下のファイルを読みに行きます

### シチュエーション B：あなたの AI は会話内容しか読めない

例：chat.openai.com、claude.ai web 版、Gemini web、スマホアプリなど。

**やり方**：
1. まず**以下のファイルの完全な内容**を会話の冒頭に貼り付け：
   - Avatar → `docs/avatar-creation-spec.md`
   - Skill → `docs/skill-template.md` + `skills/YOUR_SKILL_NAME/SKILL.md` + `skills/YOUR_SKILL_NAME/metadata.json` + `skills/EXAMPLE_social_marketing_post_ideas/SKILL.md` + `skills/EXAMPLE_social_marketing_post_ideas/metadata.json`
   - Persona → `docs/persona-template.md` + `personas/YOUR_AGENT_NAME/persona.md` + `personas/YOUR_AGENT_NAME/metadata.json` + `personas/EXAMPLE_pi_lang/persona.md` + `personas/EXAMPLE_pi_lang/metadata.json`
   - Agent（全部）→ `agents/YOUR_AGENT_NAME/` 全体（README.md + persona.md + SKILL.md + avatar/metadata.json）+ 上記の 3 セット
2. 次に対応するプロンプトをコピーして会話に貼り付け
3. AI があなたが貼ったファイル内容とルールに基づいて質問してきます

---

## プロンプト A：Avatar のみ上架

適用シチュエーション：すでにキャラクターの画像がある（または生成する予定）、`metadata.json` を出力し著作権コンプライアンスを確認する必要がある。

### すでに画像がある？2分で完了（AIインタビュー不要）

キャラクターの画像が完成していて metadata だけ必要なら、下のプロンプトは不要です——自分でファイルを記入すればそれで終わりです：

1. 画像をフォルダに `avatar.png` として置く（PNG、正方形、最低 512×512）。
2. `metadata.json` を開いて以下を記入する——必要なのはこれだけ：
   - `avatar_id` — 英小文字 + アンダースコア、例：`night_wolf_001`（フォルダのスラッグで、タイトルではない）
   - `name` — キャラクターの表示名／リスティングのタイトル、任意の言語、例：`ハル`、`周予衡`、`Signal`
   - `collection` — あなたのシリーズ名、例：`weekday_workers`
   - `listing_description` — 2〜3 文：購入者が得られるもの + キャラクターの雰囲気（これがリスティングに表示される——空欄にしないこと）
   - `species` / `universe` / `realm` — `docs/avatar-creation-spec.md` の enum から選ぶ
   - `base` — `original`（自作）またはライセンス IP 名
   - `creation_method` — 作品の制作方法：`original` / `original_ai_extended` / `ai_generated`（仕様参照；最初の 2 つは真正性バッジが付く）
   - `traits` — ビジュアルタグをいくつか（髪 / スタイル / 表情）
   - `rights.creator` — あなたの creator id
3. フォルダをアップロード。完了。

説明文から AI に記入してもらいたい？代わりに下の全体をコピーしてください。

### 補助あり完全版

下の全体をコピー：

```
私は llamppost プラットフォームで Avatar（キャラクター画像）を上架したい。metadata.json の出力と著作権コンプライアンスの確認を手伝ってください。

まず以下のファイルを読んでルールを理解してください（ローカル AI の場合）：
- docs/avatar-creation-spec.md（完全な仕様と著作権ポリシー）
- README.md「重要：フォルダと ID は必ず英語」セクション

次に、以下の質問を順番に 1 つずつ訊いてください、私が答えてから次の質問へ：

1. アップロードしたい Avatar はどんなキャラクターですか？1–3 文で外見、雰囲気、背景ストーリーを描写してください
2. この Avatar はどのコレクション（collection）に属しますか？このコレクション配下に関連 Avatar をいくつ置く予定？
3. キャラクターは何の種族（species）ですか？（human / robot / animal / spirit / その他）
4. 世界設定（universe）：modern / ancient / future / alternate？
5. 所属領域（realm）：earth / outer_space / heaven / hell？
6. 画像ソース：オリジナル、ライセンス IP、それともパブリックドメイン？
7. ライセンス IP の場合：IP 名は何？ライセンス書類は既にお持ち？
8. ビジュアル特徴（traits）：髪、衣装、表情、アクセサリー、その他——最低 3 つ
9. この Avatar の avatar_id を何にしたい？
10. マーケットの商品説明：購入者が得られるものとキャラクターの雰囲気を 2〜3 文で。これは商品ページに表示され、metadata.json の `listing_description` として保存されます——必須、空欄にしないこと。

すべて訊き終わったら、以下を出力してください：
- 完全な metadata.json（docs/avatar-creation-spec.md の schema に準拠）
- 推奨フォルダパス（例：`avatars/night_wolf_001/`）
- 送信前の著作権とコンテンツコンプライアンスのチェックリスト

ハードルール（絶対に違反不可）：
- avatar_id とフォルダ名は**英小文字 + 数字 + アンダースコア**——中国語、大文字、スペース、ハイフン不可
- EXAMPLE_ や YOUR_ プレフィックスは使用不可（これはキットの予約語、Portal が拒否）
- universe と realm フィールドに直接 IP 名を書くのは不可——modern/ancient/future/alternate のような enum 値を入れる
- ライセンス IP が絡む場合、出力で明確に「アップロード時にライセンス書類を添付すること」を私にリマインドしてください
- 画像に未成年者が含まれる可能性がある場合、未成年者の性的化コンテンツはゼロトレランスポリシーであることを明確にリマインドしてください
- 画像仕様：最低 512×512、推奨 1024×1024、PNG、1:1
```

---

## プロンプト B：Skill のみ上架

適用シチュエーション：はっきりした workflow やサービスがあり、Skill だけ単独で上架したい（特定 Persona にバインドしない）。

下の全体をコピー：

```
私は llamppost プラットフォームで Skill（技能）を上架したい。完全な SKILL.md の記入を手伝ってください。

まず以下のファイルを読んでルールを理解してください（ローカル AI の場合）：
- docs/skill-template.md（完全なフィールド説明）
- skills/YOUR_SKILL_NAME/SKILL.md（空白テンプレート）
- skills/EXAMPLE_social_marketing_post_ideas/SKILL.md（完全な例——口調と構造を見る）
- README.md「重要：フォルダと ID は必ず英語」セクション

次に、以下の質問を順番に 1 つずつ訊いてください：

1. この Skill はユーザーのどんな具体的な問題を解決しますか？1–2 文でコアな用途を教えてください
2. どんな人に最適？（個人起業家、小規模チーム、特定職業、特定シチュエーション）
3. なぜこの Skill を使うのか、自分で直接 AI に訊くのではなく？（ユニークな価値は何）
4. Workflow は大体どんなステップ？（3–7 ステップ、各ステップ 1 アクション）
5. ユーザーは何を提供する必要があれば開始できる？（必須 + 任意のインプット全てをリスト）
6. ユーザーは最終的にどんな具体的な納品物を受け取る？（数字とフォーマットを使ってください——「3 本の完全ドラフト」は「いくつかのアイデア」より説得力がある）
7. この Skill には現時点でどんな既知の制限や適用外シチュエーションがある？（正直にリスト）
8. この Skill の skill_id を何にしたい？（英小文字 + アンダースコア）
9. メインカテゴリ（category）は何？2 つ目のサブカテゴリも必要？
10. title（表示名）と one_liner（検索結果の最初の一文）をどう書きたい？
11. base_price は 0（無料上架、Hatchling お試し上架）と有料（≥100 NT$）どっちを入れたい？

すべて訊き終わったら、「2 つのファイル」を出力してください：
- `SKILL.md`——frontmatter には `skill_id` のみ、加えてすべての本文セクション
- `metadata.json`——リスティングフィールド：`skill_id`、`title`、`one_liner`、`version`、`base_price`、`languages`、`category`、`script_mode`、`listing_description`、`cover`、`banner`、およびネストされた `listing` ブロック（`what_it_does` 文字列、`what_you_get` 文字列配列、`limitations` 文字列配列）
- `assets/` に配置する 2 枚の画像仕様：`cover-<skill_id>.png`（正方形 1:1）+ `banner-<skill_id>.png`（横長 16:10）、PNG 各 2 MB 以内
- 推奨フォルダパス（例：`skills/weekly_report_writer/`）
- まだ考えがまとまっていないが補強できる部分（正直に指摘）

ハードルール：
- リスティングフィールド（title / one_liner / version / languages / category / script_mode / listing_description / listing.*）は `metadata.json` に入れます。`SKILL.md` frontmatter には `skill_id` のみを残し、リスティングフィールドを frontmatter に戻さないでください。
- skill_id とフォルダ名は**英小文字 + 数字 + アンダースコア**、両者は完全一致
- EXAMPLE_ や YOUR_ プレフィックスは使用不可
- title、one_liner、本文はどの言語でも使用可（繁体字中国語、英語、日本語、何でも）
- category は docs/skill-template.md のリストから選ぶ、最大 2 つ
- one_liner には「AI」「スマート」「先進的なモデル」のような曖昧な言葉を使わない——ユーザーが何を達成できるかを書く
- Known limitations は正直にリストアップ必須（空白や問題なしのフリは不可）
- script_mode はデフォルトで workflow_only、明確にスクリプト付属でない限り
- 表示名（title）はクリエイティブで OK、ただし skill_id は `weekly_report_writer` のような snake_case 英語必須
- base_price は `0` または `≥100` のみ許可（1–99 は Portal が拒否）
- 単品 Skill に `compatible_personas` を出力しないでください——単品上架にペアリング欄はなく、プラットフォームが `category` をもとに相性のよい Persona を扱います（バインディングが必要な場合は Agent テンプレートを使う）
- tested_runtimes / tested_models / test_level を私に訊かないでください——v1.5 以降 deprecated、Portal が今後自動テストして記入します
```

---

## プロンプト C：Persona のみ上架

適用シチュエーション：識別性のあるキャラクターがあり、Persona だけ単独で上架したい（特定 Skill にバインドしない）。

下の全体をコピー：

```
私は llamppost プラットフォームで Persona（AI 人格）を上架したい。完全な persona.md の記入を手伝ってください。

まず以下のファイルを読んでルールを理解してください（ローカル AI の場合）：
- docs/persona-template.md（完全なフィールド説明と Voice Fingerprint schema）
- personas/YOUR_AGENT_NAME/persona.md（空白テンプレート）
- personas/EXAMPLE_pi_lang/persona.md（完全な例——これは Pi 狼、彼の口調、5 段の例文、3 段の対話の書き方を見てください）
- README.md「重要：フォルダと ID は必ず英語」セクション

次に、以下の質問を順番に 1 つずつ訊いてください：

1. このキャラクターのコアな個性は何？3–5 個の形容詞で描写（例：クール、皮肉屋、行動優先、仲間思い、毒舌だけど温かい）
2. このキャラクターは何をする人？（docs/persona-template.md の profession リストから 1 つ選ぶ——work 系または companion/coach 系）
3. このキャラクターは最もどんなシチュエーションで召喚されるのに向いてる？具体例を 2–3 つ
4. このキャラクターは**どんなシチュエーションに向かない**？（明確に言ってください——これでユーザーがより精密にマッチング可能）
5. キャラクターの一人称は？（例：「オレ」、「師匠」、「私」、「朕」）
6. キャラクターはユーザーをどう呼ぶ？（「あなた」、「お前」、「ボス」、「弟子」）
7. キャラクターはユーザーに反論されたときどう対応？貫く、譲歩、それとも遠回し？
8. キャラクターはユーザーが感情の落ち込みに遭ったときどう対応？まず共感、それとも行動で感情を処理？
9. 対話例のシチュエーション（1 段必須、2 段は補うことを推奨）：
    - 1 段目（日常業務・必須）：キャラクターはどんなシチュエーションで質問される？
    - 2 段目（対立／不同意・推奨）：ユーザーは何に反論する？
    - 3 段目（脆弱／感情サポート・推奨）：ユーザーはどんな困難をシェアした？
10. ソウル素材（任意、ただし強く推奨——これがキャラクターに背骨を通すもの）。順番に訊いてください、各段とも「スキップ」を受け入れること：
    - **核心信念**（この段は上架ページに公開表示され、購入者がインストールする前に読む）：キャラクターがすべてを測る物差しにする 1〜3 個の信念は何？
    - 頼まれなくても、ユーザーのために守るものは何？
    - 誰が頼んでも絶対に手伝わないことは何？
    - どんな状況で、従うのではなくユーザーに反対する？
    - その判断を形づくる内なる葛藤は何？
    - ユーザーに対して自分をどう位置づける（対等、メンター、はっきり物を言う兄／姉、静かな道具）？
11. この persona の persona_id を何にしたい？（英小文字 + アンダースコア）
12. base_price は 0（無料上架、Hatchling お試し上架）と有料（≥100 NT$）どっちを入れたい？

すべて訊き終わったら、personas/EXAMPLE_pi_lang/ の構造に従って「2 つのファイル」を出力してください：
- `persona.md`——frontmatter には `persona_id` + `profession` のみ、加えて完全な body
- `metadata.json`——リスティングフィールド：`persona_id`、`name`、`one_liner`、`version`、`base_price`、`languages`、`listing_description`、`cover`、`banner`（persona manifest には title/category/script_mode/listing ブロックはない）
- `assets/` に配置する 2 枚の画像仕様：`cover-<persona_id>.png`（1:1）+ `banner-<persona_id>.png`（16:10）、PNG 各 2 MB 以内
- Opening / During-work / Closing behavior 各 1–2 文
- 5 つの sentence examples（前に訊いた 5 つのシチュエーションに対応）
- ユーザーが記入したソウル素材の段落：`## 核心信念`、加えて `## 會保護什麼` / `## 絕不幫什麼` / `## 何時反對使用者` / `## 養成張力` / `## 與使用者的關係` のうち回答があった段だけ。ユーザーが答えた段だけを置き、答えなかった段は省く、自分で創作しないこと
- 最低 1 段の必須対話（3 段補うことを推奨）、各段に 2–3 ラウンドの User/Persona やり取り
- 推奨フォルダパス（例：`personas/night_wolf_strategist/`）

ハードルール：
- リスティングフィールド（name / one_liner / languages / version / listing_description）は `metadata.json` に入れます。`persona.md` frontmatter には `persona_id` + `profession` のみを残し、リスティングフィールドを frontmatter に戻さないでください。
- persona_id とフォルダ名は**英小文字 + 数字 + アンダースコア**、両者は完全一致
- EXAMPLE_ や YOUR_ プレフィックスは使用不可
- name（表示名）、one_liner、すべての behavior 描写、対話、例文はどの言語でも使用可
- 複数段の対話を補う場合、**口調は必ず一貫**——これが llamppost の cross-model 一貫性のコアセールスポイント。別人のように読めたら、この persona は廃品同然
- 複数段の対話は**異なる感情 register**（routine / disagreement / vulnerability）をカバー必須——長い単一シチュエーションの対話 1 段は複数段にカウントしない
- ソウル素材は任意。私が実際に答えた段だけを書く——私が渡していない信念や拒否を創作しないこと
- ソウル素材には**キャラクターの判断を変えるもの**だけを置く、生い立ちではない（「コーヒーが好き、海辺で育った」は書かない）
- `## 核心信念` は**公開**（インストール前に上架ページに表示）；残りの 5 段のソウルは**私有**（実行プロンプトと審査者にのみ届く）。核心信念には、見知らぬ人に読まれたくないものを一切入れない
- base_price は `0` または `≥100` のみ許可（1–99 は Portal が拒否）
- 単品 Persona に `agent_skills` / `allowed_skill_categories` を出力しないでください——単品上架にペアリング欄はなく、プラットフォームが `profession` をもとに相性のよい skill を扱います（バインディングが必要な場合は Agent テンプレートを使う）
- tested_runtimes / tested_models / test_level / model_fidelity / recommended_models / voice_fingerprint override を私に訊かないでください——これらは v1.5 以降 deprecated またはプラットフォームが自動推論、Portal が今後自動テストして記入します
```

---

## プロンプト D：Agent 上架（Persona + Skill + Avatar）

適用シチュエーション：完全なキャラクター商品を作りたい——人格 + 技能 + 外見すべて欲しい、3 つが互いに呼応する必要がある。

このプロンプトは前の 3 つと違います——まず全体デザインを決めてから、3 段階で細部を詰めます。

下の全体をコピー：

```
私は llamppost プラットフォームで完全な商品セット（Persona + Skill + Avatar）を上架したい、3 ファイルすべてのデザインと記入を手伝ってください。この 3 つは互いに呼応する必要がある——3 つの無関係なものではない。

まず以下のファイルを読んでルールを理解してください（ローカル AI の場合）：
- README.md（特に「重要：フォルダと ID は必ず英語」セクション）
- docs/listing-ready-v1.md（上架ガイド全体——特に「Agent を公開する」セクション）
- docs/persona-template.md、docs/skill-template.md、docs/avatar-creation-spec.md
- agents/YOUR_AGENT_NAME/README.md（Agent テンプレートの使い方 + 双方向バインディング例）
- agents/YOUR_AGENT_NAME/persona.md + SKILL.md + avatar/metadata.json（空白 Agent テンプレート）
- personas/EXAMPLE_pi_lang/persona.md（完全な Persona 例）
- skills/EXAMPLE_social_marketing_post_ideas/SKILL.md（完全な Skill 例）

今回は一気に訊かず、4 段階に分けて進めてください：

===== 段階 1：まず全体コンセプトを決める =====

まずフィールドの詳細は訊かないでください。この 3 つを訊いてください：

1. 作りたいキャラクターは誰？一文で（30 文字以内）
2. このキャラクターのコア価値：ユーザーのどんな問題を解決する？なぜ一般 AI ではなく、このキャラクターなのか？
3. 想定ユーザーは誰？どんなシチュエーションでこのキャラクターを召喚する？

訊き終わったら、30 秒エレベーターピッチ（100 文字以内）を出力して、方向性が合っているか私に確認させてください。
**私が「方向 OK」と言ってから**、段階 2 に進んでください。

===== 段階 2：Persona を記入 =====

プロンプト C の質問で Persona の詳細を訊いてください（個性、3 段の対話シチュエーション、そしてソウル素材——とくに**核心信念**、これは上架ページに公開表示される）。
`## 核心信念` 段落と、私が回答したその他のソウル段落を含む、完全な persona.md ファイル内容を書き出してください。
出力後、私のレビューを待って、OK と言ったら段階 3 へ。

===== 段階 3：Skill を記入 =====

さっき決めた Persona の性格をベースに、このキャラクターが具体的にどんな Skill を提供するか考えてください。
（通常はキャラクターのユニーク価値を最も発揮できる 1 つの skill——雑多な 10 個ではない）

それからプロンプト B の質問で Skill の詳細を訊いてください。
完全な SKILL.md ファイル内容を書き出してください。

**重要（双方向バインディング）**：
- この Skill の compatible_personas フィールドはさっき定義した Persona の persona_id を必ず含む
- Persona の agent_skills フィールドもこの Skill の skill_id を必ず含む
- 両側を同時に更新、Portal が対称性を検証

出力後、私のレビューを待って、OK と言ったら段階 4 へ。

===== 段階 4：Avatar を記入 =====

Persona の個性と雰囲気をベースに、Avatar のビジュアル方向を考えてください：
- universe、realm、species をどう選べばキャラクターと呼応する？
- traits はどんなビジュアル要素を強調すべき？
- この Avatar は Persona の口調と一致してる？

それからプロンプト A の質問で Avatar の詳細を訊いてください。
完全な metadata.json ファイル内容を書き出してください。

===== 最後：オーバービュー =====

4 段階すべて完了したら、上架前チェックオーバービューを出力してください：
- 完全な Agent フォルダ構造（agents/<agent_name>/persona.md + SKILL.md + avatar/metadata.json）
- 推奨 agent フォルダパス（例：`agents/night_wolf_strategist/`）
- 双方向バインディング確認（Persona.agent_skills ↔ Skill.compatible_personas）
- 口調一貫性チェック（3 ファイルが同じキャラクターのように読める？）
- 上架前の最終チェックリスト

ハードルール（前の 3 プロンプトのルールすべてマージ）：
- **Agent はリスティング `metadata.json` を使いません。** これが単品の Skill / Persona との重要な違いです：Agent ではすべてのリスティングフィールド（title、name、one_liner、category、languages、version、listing_description、script_mode）を `persona.md` / `SKILL.md` の **frontmatter** に残します。バンドル内で唯一の `metadata.json` は `avatar/metadata.json`（avatar schema）です。Agent のルートにリスティング `metadata.json` や `assets/` の cover/banner を生成しないでください。
- persona_id、skill_id、avatar_id、フォルダ名はすべて**英小文字 + 数字 + アンダースコア**必須
- EXAMPLE_ や YOUR_ プレフィックスは使用不可
- 3 つの ID は共通プレフィックスを使ってセットに見せるのを推奨（例：`night_wolf_strategist` / `night_wolf_strategist_skill` / `night_wolf_strategist_001`）
- Persona ↔ Skill の agent_skills ↔ compatible_personas は必ず双方向バインディング
- Agent は 3 つすべて必須（Persona + Skill + Avatar）。Avatar なしでは Agent 上架不可——単品に分解するか先に Avatar 生成するか教えてください
- 3 ファイルの口調、設定、世界観は必ず一致
- ソウル素材は任意、かつ persona の層にのみある——私が答えたものだけを書き、絶対に自分で創作しない。`## 核心信念` は上架ページに公開表示；残りの 5 段のソウルは私有（実行プロンプトと審査者にのみ届く）
- persona は**その skill にバインドしない**——ソウルは persona に属し、skill は別の重ねられる層；`agent_skills` ↔ `compatible_personas` は組み合わせ関係を記すだけ
- 各段階終了時に私の確認を待つこと——一気に全部生成しないでください
- base_price は `0` または `≥100` のみ許可（1–99 は Portal が拒否）
- tested_models / test_level / model_fidelity / voice_fingerprint override を私に訊かないでください——これらは全部 deprecated またはプラットフォームが自動推論
```

---

## 汎用リマインダー（すべてのプロンプトに適用）

### あなたの AI がやらかすかもしれないこと

- **質問せず直接答えを出す** → 返事：「プロンプトの質問通りに 1 つずつ訊いてください、自分で仮定しないで」
- **EXAMPLE_ や YOUR_ プレフィックス付きの ID を出す** → 返事：「これは予約プレフィックス、英小文字 + アンダースコアで命名し直してください」
- **ID に中国語、大文字、スペース、ハイフンが入ってる** → 返事：「ID は英小文字、数字、アンダースコアのみ」
- **known limitations をスキップ** → 返事：「このフィールドを補ってください、空でも明示必須」
- **複数段の対話が似た口調で書かれる** → 返事：「異なる段は日常 / 対立 / 脆弱の異なる register をカバーする必要、書き直してください」
- **deprecated フィールドを詰め込む（tested_models / model_fidelity / voice_fingerprint override など）** → 返事：「v1.5 以降これらは deprecated、Portal が今後自動記入、今は詰めないで」
- **base_price に 1–99 を入れる** → 返事：「base_price は 0 または ≥100 のみ許可、修正してください」

### あなた自身もチェックすべきこと

送信前に、自分でこのチェックリストを通してください：
- [ ] フォルダ名と `*_id` フィールドが**完全一致**
- [ ] ID は英小文字 + 数字 + アンダースコアのみ
- [ ] `EXAMPLE_` や `YOUR_` プレフィックスがない
- [ ] 必須フィールドに空白やテンプレートのデフォルト値が残っていない
- [ ] `base_price` が `0` または `≥100`
- [ ] Persona + Skill バインディングの組み合わせ（Agent）なら、双方向バインディングが両側書けている
- [ ] Agent 上架時、`avatar/avatar.png` を補ってある（placeholder だけではない）
- [ ] 言語切り替えセクション（multi-language header）が翻訳の分断にぶつかっていない
- [ ] AI が無理やり押し込んだ「お役に立てれば幸いです」のような社交辞令が残っていない
