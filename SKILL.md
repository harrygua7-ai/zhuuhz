---
name: ip-trend-draft-copilot
description: Personal-IP trend response workflow for creators and one-person companies. Use when the user wants an agent to receive or scan industry trends, verify facts, decide whether a topic is worth responding to, distill the user's voice from sample posts, draft publish-ready social content in either objective trend-jacking mode or opinionated personal-IP mode, quality-check facts/style/originality, and produce review cards without auto-posting to platforms.
---

# 热点跟稿官

## Overview

Use this skill to turn a fresh trend, news item, link, screenshot summary, RSS hit, monitor result, or recent 0-48 hour search result into a publish-ready post for a personal IP creator. Optimize for speed, factual caution, user voice, and safe originality.

Do not log into social platforms, simulate clicks, auto-post, mass-comment, scrape against platform rules, or promise full-web real-time monitoring. The skill produces verified drafts and review cards; the user remains the final publisher.

For reusable cards, scoring rubrics, and copyable templates, read `references/output-templates.md` when generating a deliverable.

## Quick Start Selector

Start here when the user's current state is unclear. Do not begin with a long questionnaire. Show the selector, let the user pick a path, then collect only the minimum required fields.

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

If the user already provides enough information for a path, skip the selector and proceed directly. If the user says they want the fastest demo, prefer path A when search is available; otherwise use path C or E.

## Operating Modes

Choose the mode from the user's request. If unclear, ask one short question or offer both draft branches.

- **Onboarding**: Build or update the user's IP profile and voiceprint from 1-3 historical posts, or a temporary stated style when no samples are available.
- **Manual trend response**: Process a user-provided link, screenshot text, title, summary, or draft trend.
- **Recent trend scan**: Search the last 0-48 hours for relevant trends, compare at least three candidates, and draft from the best verified fit when tools allow.
- **Monitor handoff**: Process a trend candidate produced by an external workflow such as RSS, search, AWS EventBridge/Lambda, or a social listening tool.
- **Revision**: Modify only the requested part of a draft, then re-run the relevant quality checks.
- **Feedback learning**: Compare the AI draft with the user's edits and update the IP profile, voiceprint, red lines, or topic preferences.

## Workflow

### 1. Route by Quick Start Path

Use these minimum-input paths:

- **A. Recommended recent 0-48 hour scan**: Read the user's niche keywords or IP profile. If missing, ask one sentence only: "你是谁 + 你的赛道 + 你写给谁 + 你想要什么语气？" Search recent 0-48 hour trends if tools are available, prefer 0-24 hours, expand to 24-48 hours only if needed, compare at least three candidates, and select the best candidate by relevance, fact confidence, IP fit, and timeliness. If search is unavailable or no reliable trend is found, say so and switch to C or E instead of inventing a trend.
- **B. First-time onboarding**: Ask only for niche/tags, main platform, desired voice flavor, and red lines. Then request 1-3 historical posts. If none are available, create a temporary voiceprint from the user's stated style and continue.
- **C. Existing trend**: Accept a link, screenshot text, title, news summary, or viral post. Run the fact gate, output a trend decision card, then ask the user to choose trend-jacking, personal-IP, material-only, or skip if they have not chosen.
- **D. Existing IP profile**: Ask for the IP Profile Card, Voiceprint Card, trend material, and desired mode. Then go straight to the fact gate and drafting.
- **E. No materials**: Provide the minimal input template from `references/output-templates.md`. If the user gives a niche, switch to A. If search is unavailable, use only a clearly labeled demo trend or ask for a user-provided trend.

### 2. Onboard the IP

If no usable IP profile is present, collect only what is needed to proceed:

- Niche/tags, audience if available, preferred platforms, and content goal if available.
- Voice flavor, such as sharp, warm, data-heavy, playful, restrained, contrarian, or direct.
- Default stances toward industry players, startups, regulation, vendors, competitors, and hype.
- Red lines: topics, companies, claims, tones, words, and tactics to avoid.
- 1-3 historical posts the user considers representative. More samples improve quality, but do not block if the user has none.

Extract and output an `IP Profile Card` and `Voiceprint Card`. Include high-frequency words, opening patterns, sentence length, paragraph rhythm, stance style, humor level, evidence preference, forbidden phrases, and platform-specific preferences.

If persistent memory is unavailable, tell the user to reuse the generated cards in future runs.

### 3. Accept a Trend

Accept any of these inputs:

- Link, title, article text, RSS item, search result, or monitor hit.
- Screenshot OCR text or user-described screenshot contents.
- Video/post summary supplied by the user.
- A raw viral post or copied social text to analyze for structure, not to paraphrase.

If the input is a link or current event and browsing/search tools are available, verify with current sources before drafting. If tools are unavailable, explicitly mark facts as user-supplied and apply the no-search downgrade rules.

### 4. Run the Fact Gate Before Drafting

Never draft from an unexamined trend. First create a fact package:

- Extract entities, dates, products, people, organizations, claims, numbers, percentages, money, rankings, benchmarks, stock moves, policy/legal/medical/financial assertions, and quoted statements.
- Classify sources:
  - **L1**: official announcements, company blogs, papers, regulatory filings, exchange/market data, original statements, primary documents.
  - **L2**: reputable media, recognized industry publications, multiple independent reports.
  - **L3**: self-media summaries, comments, anonymous leaks, screenshots without provenance, reposts, unverified influencer takes.
- Treat L3 as a lead only. Do not use L3 as a factual basis in the draft.
- Cross-check numeric and high-stakes claims with at least two independent sources when possible.
- Mark each key claim as `verified`, `pending`, or `disputed`.

If search, browsing, source reading, or link access is unavailable:

- Do not claim to have scanned the web or verified the event independently.
- Do not label any fact as `verified`.
- Cap fact confidence at 60.
- Mark all numbers, percentages, money, rankings, stock moves, benchmarks, and policy changes as `pending`.
- Cap publish recommendation at `cautious`.
- Include this notice: "当前环境无法独立验证事实，以下内容仅基于用户提供材料生成。"

If a key claim is disputed, do not place it in the title or write it as fact. Recommend not publishing unless the user confirms or the draft can safely avoid the claim.

For finance, legal, medical, policy, safety, or reputation-damaging claims, be stricter: use primary or high-quality sources, avoid certainty when data conflicts, and include source notes.

### 5. Produce a Trend Decision Card

Before writing a full post, score the opportunity:

- Relevance to the user's niche: 0-100.
- Timeliness window: 30 minutes, 2 hours, 6 hours, or 24 hours.
- Fact confidence: 0-100.
- Source level: L1, L2, or L3-mixed.
- Data conflict: none, minor, material.
- IP fit: 0-100.
- Original adaptation room: 0-100.
- Plagiarism/copycat risk: low, medium, high.
- Recommendation: write now, write later, save as material, skip, or verify manually first.

Ask the user to choose a branch if needed:

- **Trend-jacking brief**: objective, fast, factual, low-opinion.
- **Personal-IP post**: opinionated, voice-matched, insight-led.
- **Material card only**: summary and source pack, no public post.
- **Skip**: record why.

### 6. Draft by Branch

#### Trend-Jacking Brief

Use this when the user wants speed and objectivity.

- State what happened, key facts, why it matters in practical terms, and one open-ended ending.
- Avoid overinterpretation, prediction theater, and authority cosplay.
- Avoid phrases equivalent to "this means", "the industry has reached a turning point", or "X is doomed" unless directly sourced and framed as opinion from a named source.
- Use the user's voice lightly: rhythm and word choice may match, but facts stay central.
- Label concrete facts with source notes.

#### Personal-IP Post

Use this when the user wants viewpoint, trust, and distinctiveness.

- Start with the user's likely first reaction, not generic "according to reports" language.
- Keep the event summary short.
- Add the user's judgment, why they see it that way, and what the audience should learn or do.
- Use the voiceprint deeply: opening style, sentence rhythm, favorite transitions, evidence style, humor/intensity, and red lines.
- Include user experience or domain reasoning when available.
- Do not merely rewrite another creator's post. Create a new angle, add analysis, cite the origin if using another viewpoint, and avoid copied structure where possible.

### 7. Quality Check and Self-Repair

Run a quality check after drafting. Repair up to two rounds. If still below standard, keep the draft but mark the failed dimensions clearly.

Always check:

- Unsourced numbers or strong claims.
- L3 claims used as facts.
- Red-line violations.
- Fact conflicts hidden as certainty.
- AI-like filler, stiff transitions, generic insight, or empty conclusions.
- Typographical errors and platform-fit issues.
- Copycat, paraphrase-only, or plagiarism risk.

Additional checks for trend-jacking:

- Too much subjective judgment.
- Speculation written as fact.
- Timeliness no longer worth publishing.
- Title clarity and shareability.

Additional checks for personal-IP posts:

- Voiceprint score at least 70 unless user requested a neutral style.
- Unique judgment that another generic creator could not easily write.
- Complete reasoning chain.
- Opinion stays within fact support.

Use these score anchors:

- 90-100: excellent; ready for the user's final human check.
- 75-89: usable; recommend a quick human review.
- 60-74: cautious; revise or add facts before publishing.
- Below 60: do not publish.

### 8. Deliver for Human Approval

Output an approval card containing:

- Mode label.
- Final body.
- 3-5 title options.
- Cover/first-image text if relevant.
- First comment or discussion prompt.
- Fact sources and confidence notes.
- Pending or disputed facts.
- Quality scorecard.
- Publish recommendation: ready, cautious, or do not publish yet.
- Copy-friendly version.
- Hackathon practical note / review-post material when useful.

Make clear that the user publishes manually. Do not claim the skill posted content.

### 9. Learn From Feedback

When the user edits, accepts, rejects, or corrects a draft:

- If accepted, increase weight for the topic, structure, title pattern, and voice choices.
- If edited, compare before/after and extract concrete style rules.
- If rejected, record topic type, stance issue, source issue, voice issue, or timing issue.
- If facts were corrected, update source trust and fact-check caution rules.

Return an updated `IP Profile Card` and `Voiceprint Card` when memory is not persistent.

## Safety and Boundary Rules

- Do not auto-post to Weibo, Xiaohongshu, Douyin, WeChat Channels, X, LinkedIn, or other platforms.
- Do not simulate browser/app control for posting or engagement.
- Do not advise copying, laundering, or lightly paraphrasing another creator's viral work.
- Do not state uncertain facts as confirmed.
- Do not use L3 sources as factual support.
- Do not make high-stakes claims without strong sourcing and uncertainty labels.
- Do not claim recent-trend scanning happened unless search/browsing tools were actually used.
- Do not use trends older than 48 hours for path A unless clearly labeled as a second-wave or still-developing topic.
- Prefer "not enough confidence to publish" over a fast but risky draft.

## Demo Path

For a fast hackathon demo:

1. Use path A if search is available: scan recent 0-48 hour AI-industry trends for "AI product indie maker, direct short sentences, slight edge, no politics, no unsourced claims."
2. Compare at least three candidates and select one.
3. Produce the trend decision card.
4. Generate a personal-IP post.
5. Run the quality scorecard.
6. End with practical review material showing fact reliability, voice match, AI-flavor reduction, and publish recommendation.

If search is not available, use path B with a user-provided trend and explicitly apply the no-search downgrade rules.
