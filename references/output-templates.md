# Output Templates

Use these templates when delivering work with `ip-trend-draft-copilot`. Keep outputs compact enough for a creator to review quickly.

## Quick Start Selector

```text
你想怎么开始？

A. 立即扫描最近 0-48 小时相关热点并生成稿子（推荐）
适合：你现在没有具体热点，但想让 Agent 根据你的赛道主动找一个最近仍有时效性的热点，核查事实后生成发布就绪稿。

B. 第一次使用，先建立我的个人 IP 档案
适合：还没配置过身份、风格、红线、历史内容的人。建立后，后续生成会更像你。

C. 我手上已有热点，帮我判断值不值得写
适合：你已经有链接、截图、标题、新闻摘要或爆款文案，想快速判断能不能跟。

D. 我已有 IP 档案，直接生成跟稿
适合：你之前保存过 IP 档案卡和语言指纹卡，现在只想快速产出一篇稿。

E. 我目前什么材料都没有
适合：不知道怎么开始，让 Agent 用最小问题帮你临时建档并跑一个轻量版本。
```

## Minimal Input Templates

### A. Recent 0-48 Hour Scan

```text
你是谁 + 你的赛道 + 你写给谁 + 你想要什么语气：

优先平台（可选）：
红线（可选）：
```

### B. First-Time Setup

```text
你的赛道/标签：
你主要发的平台：
你希望别人感受到的语言味道：
你的红线：

历史内容（1-3 条，可空）：
1.
2.
3.
```

### C. Existing Trend

```text
热点材料（链接 / 截图文字 / 标题 / 摘要 / 爆款文案）：

我想要：
蹭热度稿 / 个人 IP 稿 / 只做素材 / 先判断
```

### D. Existing Profile

```text
IP 档案卡：

语言指纹卡：

热点材料：

想要模式：蹭热度 / 个人 IP
```

### E. No Materials

```text
你可以这样填：

我是：
我发的平台：
我的风格：
我的红线：
我想跟的热点/赛道：
```

## IP Profile Card

```markdown
## IP 档案卡
- 赛道/标签：
- 目标受众：
- 平台偏好：
- 内容目标：涨粉 / 建信任 / 带线索 / 表达观点
- 默认立场：
- 绝对红线：
- 优先关注：
- 少推/不推：
```

## Voiceprint Card

```markdown
## 语言指纹卡
- 语气基调：
- 高频词/口头禅：
- 开头习惯：
- 句长和节奏：
- 段落留白：
- 证据偏好：数据 / 案例 / 经验 / 类比 / 反问
- 幽默和锋利度：
- 常用结尾：
- 禁用表达：
- 平台差异：
```

## Fact Package

```markdown
## 事实包
- 事件一句话：
- 关键实体：
- 时间线：
- 已验证事实：
- 待确认事实：
- 存在争议：
- 不采用的信息：
- 来源清单：
- 验证限制：
```

Source notation:

```text
[L1 已验证] 官方公告：...
[L2 待确认] 媒体报道：...
[L3 不采用] 自媒体/评论/截图：...
```

## Trend Decision Card

```markdown
## 热点判断卡
- 热点标题：
- 一句话摘要：
- 相关度：__/100
- 时效窗口：30分钟 / 2小时 / 6小时 / 24小时
- 事实可信度：__/100
- 信源等级：L1 / L2 / L3混杂
- 数据冲突：无 / 轻微 / 关键冲突
- 适合我的 IP：__/100
- 原创改编空间：__/100
- 抄袭/撞稿风险：低 / 中 / 高
- 建议动作：立即写 / 稍后写 / 只收藏 / 跳过 / 先人工确认
```

## Recent Scan Candidate Table

Use this for path A before selecting one trend.

```markdown
## 最近 0-48 小时候选热点
| 候选 | 时间窗 | 相关度 | 事实可信度 | IP 适配 | 时效 | 风险 | 建议 |
|---|---|---:|---:|---:|---|---|---|
| 1 | 0-24h / 24-48h | __ | __ | __ | 强/中/弱 | 低/中/高 | 写/跳过/待确认 |
| 2 | 0-24h / 24-48h | __ | __ | __ | 强/中/弱 | 低/中/高 | 写/跳过/待确认 |
| 3 | 0-24h / 24-48h | __ | __ | __ | 强/中/弱 | 低/中/高 | 写/跳过/待确认 |
```

## Draft Approval Card

```markdown
## 审核卡
- 模式：蹭热度 / 个人 IP / 素材卡
- 发布建议：可发 / 谨慎发 / 不建议发
- 待确认事项：

### 标题备选
1.
2.
3.

### 正文
...

### 首图/封面文案
...

### 评论区引导
...

### 事实来源
...

### 质检评分
| 维度 | 分数/状态 |
|---|---:|
| 事实可靠性 | __/100 |
| 语言像我 | __/100 |
| AI 味浓度 | __/100 |
| 原创增量 | __/100 |
| 传播钩子 | __/100 |
| 红线检查 | 通过/未通过 |
```

## Scoring Rubric

- **事实可靠性**: Base on source level, cross-check status, and whether numbers/quotes are sourced. Penalize disputed or single-source high-stakes claims.
- **语言像我**: Compare against voiceprint: opening, rhythm, vocabulary, stance, paragraph shape, and forbidden expressions.
- **AI 味浓度**: Penalize generic transitions, sweeping claims, "值得关注的是", "不难看出", empty summaries, and over-balanced tone.
- **原创增量**: Reward user-specific judgment, experience, counterintuitive angle, and useful implication. Penalize mere paraphrase.
- **传播钩子**: Reward clear stakes, timeliness, contrast, specificity, and audience relevance. Penalize clickbait unsupported by facts.

Score anchors:

```text
90-100：表现优秀，可直接进入人工最终确认
75-89：可用，建议人工快速检查
60-74：谨慎，需要修改或补充事实
低于 60：不建议发布
```

No-search downgrade:

```text
当前环境无法独立验证事实，以下内容仅基于用户提供材料生成。
```

When search, browsing, or source reading is unavailable:

- Fact reliability may not exceed 60.
- Do not mark facts as verified.
- Mark numbers, percentages, money, rankings, stock moves, benchmarks, and policy changes as pending.
- Publish recommendation may not exceed "谨慎发".

## Rewrite Commands

When the user asks for a modification, preserve all unaffected parts.

```text
只改标题，不动正文。
第三段加一个我的个人经历。
语气再尖一点，但不要攻击具体个人。
删掉所有待确认数字。
改成客观蹭热度稿。
改成更像我平时发朋友圈的口吻。
```

## Hackathon Review Material

```markdown
## 实战笔记素材
我用这个 Skill 处理了一个赛道热点。它先做事实闸门，区分 L1/L2/L3 来源，再判断这个热点是否适合我的个人 IP。

结果：
- 事实可靠性：__/100
- 语言像我：__/100
- AI 味浓度：__/100
- 原创增量：__/100
- 发布建议：

最有用的是：它没有直接乱写热点，而是把待确认事实和不建议采用的信息标了出来，最后生成的是一篇可以由我确认后发布的观点稿。
```
