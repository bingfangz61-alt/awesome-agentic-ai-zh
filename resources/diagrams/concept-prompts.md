# Stage 7.5 概念圖 — ChatGPT image-gen prompts（3 圖 × 3 語言）

> 把下面的 prompt 整段複製貼到 ChatGPT（含 DALL-E / GPT-4o image gen），生成對應的概念圖 PNG。建議生成後存成 `resources/diagrams/<name>.{md,zh-Hans,en}.png` 跟既有命名一致。

## 圖 A — 12 進階概念 cluster map

### zh-TW prompt

```
生成一張清晰的技術示意圖，主題是「12 個進階 Agentic AI 概念分類地圖」。

版面設計：
- 2D 表格 / grid 結構
- X 軸（橫軸、由左至右）= 4 個 agent stack 層次：
  1. Service 層 / 2. Repo 層 / 3. Config 層 / 4. Types 層
- Y 軸（縱軸、由上至下）= 4 個問題類型：
  1. 編排類（agent 怎麼分工 / 協作）
  2. 反思類（agent 怎麼自我修正）
  3. 治理類（agent 自主權邊界）
  4. 韌性類（agent 預防失敗）

在對應的格子裡放概念名稱 + 編號：
- Service × 編排：1. Work Boundary（跨所有層、加 *）/ 3. Speculative Parallel / 10. Self-organizing Teams
- Service × 反思：5. Plan-Act-Reflect / 4. Agent-as-Judge
- Service × 治理：6. Hierarchical Task Decomposition
- Types × 編排：2. Contract Hand-offs
- Types × 反思：11. Spec-driven Development
- Config × 治理：7. Autonomy Gradients / 12. Graceful Degradation
- Config × 韌性：8. Cost-aware Budget Gates / 9. Failure Injection
- Repo × 反思：加註「memory 由 Stage 6 提供」（不放概念名稱）

視覺風格：
- 簡潔技術 blog 風（參考 Anthropic engineering blog）
- 2-3 個顏色（hover blue + neutral grey + 強調 orange、不要繽紛）
- Sans-serif 字體（如 Inter）、留白多
- Work Boundary（#1）標記為跨層 discipline（asterisk + 不同 color）
- 比例 16:9 適合 README banner

不要：3D 透視、漸層陰影、卡通插圖、emoji、過多裝飾。
```

### zh-Hans prompt

```
生成一张清晰的技术示意图，主题是「12 个进阶 Agentic AI 概念分类地图」。

版面设计：
- 2D 表格 / grid 结构
- X 轴（横轴、由左至右）= 4 个 agent stack 层次：
  1. Service 层 / 2. Repo 层 / 3. Config 层 / 4. Types 层
- Y 轴（纵轴、由上至下）= 4 个问题类型：
  1. 编排类（agent 怎么分工 / 协作）
  2. 反思类（agent 怎么自我修正）
  3. 治理类（agent 自主权边界）
  4. 韧性类（agent 预防失败）

在对应的格子里放概念名称 + 编号：
- Service × 编排：1. Work Boundary（跨所有层、加 *）/ 3. Speculative Parallel / 10. Self-organizing Teams
- Service × 反思：5. Plan-Act-Reflect / 4. Agent-as-Judge
- Service × 治理：6. Hierarchical Task Decomposition
- Types × 编排：2. Contract Hand-offs
- Types × 反思：11. Spec-driven Development
- Config × 治理：7. Autonomy Gradients / 12. Graceful Degradation
- Config × 韧性：8. Cost-aware Budget Gates / 9. Failure Injection
- Repo × 反思：加注「memory 由 Stage 6 提供」（不放概念名称）

视觉风格：
- 简洁技术 blog 风（参考 Anthropic engineering blog）
- 2-3 个颜色（hover blue + neutral grey + 强调 orange、不要缤纷）
- Sans-serif 字体（如 Inter）、留白多
- Work Boundary（#1）标记为跨层 discipline（asterisk + 不同 color）
- 比例 16:9 适合 README banner

不要：3D 透视、渐层阴影、卡通插图、emoji、过多装饰。
```

### English prompt

```
Generate a clean technical diagram titled "12 Advanced Agentic AI Concepts — Cluster Map".

Layout:
- 2D table / grid structure
- X-axis (left to right) = 4 agent stack layers:
  1. Service layer / 2. Repo layer / 3. Config layer / 4. Types layer
- Y-axis (top to bottom) = 4 problem categories:
  1. Orchestration (how agents divide work / coordinate)
  2. Reflection (how agents self-correct)
  3. Governance (agent autonomy boundaries)
  4. Resilience (preventing failure)

Place concept names + numbers in the matching cells:
- Service × Orchestration: 1. Work Boundary (cross-layer, mark with *) / 3. Speculative Parallel / 10. Self-organizing Teams
- Service × Reflection: 5. Plan-Act-Reflect / 4. Agent-as-Judge
- Service × Governance: 6. Hierarchical Task Decomposition
- Types × Orchestration: 2. Contract Hand-offs
- Types × Reflection: 11. Spec-driven Development
- Config × Governance: 7. Autonomy Gradients / 12. Graceful Degradation
- Config × Resilience: 8. Cost-aware Budget Gates / 9. Failure Injection
- Repo × Reflection: annotate "memory provided by Stage 6" (no concept name)

Visual style:
- Clean tech blog aesthetic (reference Anthropic engineering blog)
- 2-3 colors (hover blue + neutral grey + accent orange; not colorful)
- Sans-serif typography (e.g., Inter); generous whitespace
- Work Boundary (#1) marked as a cross-layer discipline (asterisk + distinct color)
- 16:9 aspect ratio, suitable as a README banner

Avoid: 3D perspective, gradient shadows, cartoon illustrations, emoji, excessive decoration.
```

---

## 圖 B — Reading path decision tree

### zh-TW prompt

```
生成一張清晰的技術示意圖，主題是「Agentic AI 進階閱讀決策樹」。

版面設計：
- 從頂端標題「你現在卡什麼問題？」往下分支出 5 條
- 5 條分支對應 5 個常見問題（橫向排列）：
  1. 不知道 agent 怎麼開始
  2. multi-agent 要不要用、怎麼開
  3. context 沒效率
  4. eval 怎麼寫 / 自動驗證
  5. 想跟上 frontier 現況
- 每個分支底下接一個方框、寫該分支「先讀」的文章 + 預估時間：
  1. → Anthropic Building Effective Agents (~20 min)
  2. → Cognition Don't Build Multi-Agents (~10 min)
  3. → Anthropic Skills + CLAUDE.md memory docs (~15 min)
  4. → Hamel Husain Evals blog (~15 min)
  5. → LangGraph Plan-Execute / Voyager / Self-Discover paper (~30 min/篇)
- 在底部加 1 行小字「規則：每分支最多挑 2 篇深讀，不要 broad-scan」

視覺風格：
- Top-down tree、方框 + 連線、不要圓角過多
- 「先讀」文章用粗體
- 5 條分支可上不同 color tag（紅 / 綠 / 黃 / 藍 / 紫）
- Sans-serif、比例 4:3 或正方形
- 簡潔技術風

不要：泛用 mind map（太繽紛）、Tree branches 加葉子或樹幹圖案、emoji、卡通元素。
```

### zh-Hans prompt

```
生成一张清晰的技术示意图，主题是「Agentic AI 进阶阅读决策树」。

版面设计：
- 从顶端标题「你现在卡什么问题？」往下分支出 5 条
- 5 条分支对应 5 个常见问题（横向排列）：
  1. 不知道 agent 怎么开始
  2. multi-agent 要不要用、怎么开
  3. context 没效率
  4. eval 怎么写 / 自动验证
  5. 想跟上 frontier 现况
- 每个分支底下接一个方框、写该分支「先读」的文章 + 预估时间：
  1. → Anthropic Building Effective Agents (~20 min)
  2. → Cognition Don't Build Multi-Agents (~10 min)
  3. → Anthropic Skills + CLAUDE.md memory docs (~15 min)
  4. → Hamel Husain Evals blog (~15 min)
  5. → LangGraph Plan-Execute / Voyager / Self-Discover paper (~30 min/篇)
- 在底部加 1 行小字「规则：每分支最多挑 2 篇深读，不要 broad-scan」

视觉风格：
- Top-down tree、方框 + 连线、不要圆角过多
- 「先读」文章用粗体
- 5 条分支可上不同 color tag（红 / 绿 / 黄 / 蓝 / 紫）
- Sans-serif、比例 4:3 或正方形
- 简洁技术风

不要：泛用 mind map（太缤纷）、Tree branches 加叶子或树干图案、emoji、卡通元素。
```

### English prompt

```
Generate a clean technical diagram titled "Agentic AI Advanced Reading Decision Tree".

Layout:
- Top heading: "What problem are you stuck on right now?"
- Branch down into 5 columns, each corresponding to a common problem (laid out horizontally):
  1. Don't know how to start with agents
  2. Should I use multi-agent / how
  3. Context is inefficient
  4. How to write evals / auto-verify
  5. Want to catch up on the frontier
- Under each branch, a box with the "read first" article + estimated time:
  1. → Anthropic Building Effective Agents (~20 min)
  2. → Cognition Don't Build Multi-Agents (~10 min)
  3. → Anthropic Skills + CLAUDE.md memory docs (~15 min)
  4. → Hamel Husain Evals blog (~15 min)
  5. → LangGraph Plan-Execute / Voyager / Self-Discover paper (~30 min each)
- Footnote at bottom: "Rule: pick at most 2 papers per branch — do not broad-scan."

Visual style:
- Top-down tree, rectangular boxes + lines, minimal rounded corners
- Bold the "read first" article names
- The 5 branches can have distinct color tags (red / green / yellow / blue / purple)
- Sans-serif, 4:3 or square aspect ratio
- Clean technical style

Avoid: generic mind-map look (too colorful), leaf/tree-trunk illustrations on the branches, emoji, cartoon elements.
```

---

## 圖 C — F11-F14 failure-mode lifecycle

### zh-TW prompt

```
生成一張清晰的技術示意圖，主題是「Agent failure mode 進化循環」（agent-collab-skills 的失敗模式 codify 機制）。

版面設計：
- 5 步驟的循環圖（cycle / loop，順時針或從上往下）
- 步驟：
  ① 發現 incident（dogfood 或 production fail）
  ② 在 docs/observed-failure-modes.md 文件化（命名為 F-N、如 F11 / F12 / F13 / F14）
  ③ 加進 acceptance-gate preset YAML check（codify 進規格）
  ④ 下次同樣情境自動被 catch
  ⑤ 累積夠多 → CLAUDE.md / SKILL.md mandatory invocation 規則
- 從 ⑤ 拉一條箭頭回到 ① 表示循環持續
- 中間或一側加文字註解：「不是寫死所有規則、而是每出一次包就 codify 一次」

右側放一個小框，舉 F14 具體例子（直線箭頭）：
  - F14 incident (2026-05-13、Phase D 操作者跳過 preset)
  - ↓
  - observed-failure-modes.md §F14（META-FAILURE）
  - ↓
  - multi-locale-mirror-sync.yml 新增 cross_document_link_text_parity check
  - ↓
  - retrospective test 抓到 9+ real drift（6 個 audit 漏的、3 個 audit 已知的）
  - ↓
  - CLAUDE.md mandatory preset 規則寫進去

視覺風格：
- 5-step loop 主圖 + F14 線性 example 右側
- 2-3 個顏色：incident 用紅、文件化用 blue、preset 用 green、CLAUDE.md 用 purple
- Sans-serif、比例 16:9 或 4:3
- 簡潔 tech blog 風、Anthropic engineering blog 質感

不要：齒輪 / 發條視覺 metaphor、過多 icon、emoji、3D 渲染。
```

### zh-Hans prompt

```
生成一张清晰的技术示意图，主题是「Agent failure mode 进化循环」（agent-collab-skills 的失败模式 codify 机制）。

版面设计：
- 5 步骤的循环图（cycle / loop，顺时针或从上往下）
- 步骤：
  ① 发现 incident（dogfood 或 production fail）
  ② 在 docs/observed-failure-modes.md 文件化（命名为 F-N、如 F11 / F12 / F13 / F14）
  ③ 加进 acceptance-gate preset YAML check（codify 进规格）
  ④ 下次同样情境自动被 catch
  ⑤ 累积够多 → CLAUDE.md / SKILL.md mandatory invocation 规则
- 从 ⑤ 拉一条箭头回到 ① 表示循环持续
- 中间或一侧加文字注解：「不是写死所有规则、而是每出一次包就 codify 一次」

右侧放一个小框，举 F14 具体例子（直线箭头）：
  - F14 incident (2026-05-13、Phase D 操作者跳过 preset)
  - ↓
  - observed-failure-modes.md §F14（META-FAILURE）
  - ↓
  - multi-locale-mirror-sync.yml 新增 cross_document_link_text_parity check
  - ↓
  - retrospective test 抓到 9+ real drift（6 个 audit 漏的、3 个 audit 已知的）
  - ↓
  - CLAUDE.md mandatory preset 规则写进去

视觉风格：
- 5-step loop 主图 + F14 线性 example 右侧
- 2-3 个颜色：incident 用红、文件化用 blue、preset 用 green、CLAUDE.md 用 purple
- Sans-serif、比例 16:9 或 4:3
- 简洁 tech blog 风、Anthropic engineering blog 质感

不要：齿轮 / 发条视觉 metaphor、过多 icon、emoji、3D 渲染。
```

### English prompt

```
Generate a clean technical diagram titled "Agent Failure-Mode Evolution Cycle" (the codification mechanism in agent-collab-skills).

Layout:
- A 5-step cycle / loop (clockwise or top-down):
  ① Incident detected (dogfood or production failure)
  ② Document in docs/observed-failure-modes.md (name it F-N, e.g. F11 / F12 / F13 / F14)
  ③ Add to acceptance-gate preset YAML check (codify into spec)
  ④ Next time the same situation occurs, it's auto-caught
  ⑤ After accumulating enough → write a mandatory invocation rule into CLAUDE.md / SKILL.md
- An arrow from ⑤ back to ① to show the cycle continues
- A side caption: "Don't hard-code every rule — codify each incident once"

On the right side, a small box with the F14 concrete example (linear arrows):
  - F14 incident (2026-05-13, Phase D operator skipped the preset)
  - ↓
  - observed-failure-modes.md §F14 (META-FAILURE)
  - ↓
  - multi-locale-mirror-sync.yml gains a cross_document_link_text_parity check
  - ↓
  - Retrospective test catches 9+ real drifts (6 audit-missed, 3 audit-known)
  - ↓
  - CLAUDE.md gains a mandatory-preset rule

Visual style:
- Main 5-step loop + linear F14 example on the right
- 2-3 colors: incident red, documentation blue, preset green, CLAUDE.md purple
- Sans-serif, 16:9 or 4:3 aspect ratio
- Clean tech blog aesthetic (reference Anthropic engineering blog)

Avoid: gear / clockwork visual metaphors, excessive icons, emoji, 3D rendering.
```

---

## 用法建議

1. 開 ChatGPT（GPT-4o 或 DALL-E、有 image gen 能力的 model）
2. 把對應語言的 prompt **整段**複製貼上
3. 生成後存成：
   - `resources/diagrams/concept-cluster.png`（zh-TW）
   - `resources/diagrams/concept-cluster.zh-Hans.png`
   - `resources/diagrams/concept-cluster.en.png`
   - 同理 `reading-decision-tree.{md,zh-Hans,en}.png` 跟 `failure-lifecycle.{md,zh-Hans,en}.png`
4. 嵌入 Stage 7.5 對應 section（取代或補充既有 ASCII 圖）

> 💡 **小撇步**：第一次生成不滿意、把 prompt 末尾「不要」list 加新項目（例如「不要在框內加 emoji」「不要紫色」）再 regenerate。通常 2-3 次調整能拿到可用版本。
