# Technical Blog Writing Framework

A structured framework for writing engaging, SEO-optimized technical blog posts for **dev.to** and **Medium** — written in a storytelling voice, with full checklist review whether the post is a fresh draft or an existing one.

This file contains two formats — choose the one that fits your post:

| Format | Use when |
|--------|----------|
| [Format A: Tutorial / How-To](#format-a-tutorial--how-to) | Teaching a concept or walking through a technical process |
| [Format B: Engineering Narrative](#format-b-engineering-narrative) | Sharing a real decision, migration, or architectural tradeoff from experience |

All posts go through these shared protocols regardless of format:

| Protocol | Purpose |
|----------|---------|
| [Clarifying Questions](#agent-protocol-clarifying-questions) | Run before writing any draft or reviewing any existing post |
| [Sensitive Information Guard](#agent-protocol-sensitive-information-guard) | Run before any draft is written or shared |
| [Draft Review Mode](#agent-protocol-draft-review-mode) | Run when the input is an existing draft rather than raw notes |
| [Storytelling Voice](#agent-protocol-storytelling-voice) | Apply to every sentence of every post, both formats |
| [Platform Optimisation](#agent-protocol-platform-optimisation) | Apply after the post is complete, before publishing |

---

# Agent Protocol: Clarifying Questions

## When to ask vs. when to proceed

Before writing any draft, the agent must assess whether the input — text, notes, code, or a rough outline — contains enough information to fill each required section without fabricating details.

**Proceed without asking if:**
- The input clearly answers the required fields for that section (even if phrased loosely)
- A reasonable inference can be made from context and code alone
- The missing detail is cosmetic (e.g., an exact word count, a CTA preference)

**Ask before writing if:**
- A required section depends on first-person experience or decisions that cannot be inferred (e.g., "why did you choose X over Y?")
- Numbers are needed (latency, error rates, team size, timeline) and none are present in the input
- The format itself is ambiguous — it's unclear whether this is a tutorial or a narrative

**Never fabricate:**
- Benchmark numbers or metrics
- Architectural decisions or the reasoning behind them
- Mistakes, incidents, or rollback events
- Quotes or team attributions

If any of these are missing and cannot be inferred, stop and ask. A placeholder like `[INSERT METRIC]` is acceptable only as a last resort when the user has explicitly asked for a draft skeleton.

---

## Step 0 — Format Detection

Before applying any framework, determine which format applies.

**If the user provides enough signal** (e.g., "write a tutorial on X" or "here's our migration story"), proceed to the appropriate format.

**If the format is ambiguous**, ask:

> "Before I start — is this post meant to **teach someone how to do something** (tutorial), or to **share a real decision or migration your team went through** (engineering narrative)? The structure is quite different for each."

Only ask this once. If the user's follow-up still doesn't clarify, default to **narrative** if the input contains first-person experience, decisions, or outcomes — and **tutorial** if it contains steps, code, or a process to explain.

---

## Step 1 — Input Assessment

After format is determined, scan the input and identify which required fields are **present**, **inferable**, or **missing**.

### Required fields — Format A (Tutorial)

| Field | Status |
|-------|--------|
| Primary keyword / topic | |
| Target audience and assumed skill level | |
| The core problem the post solves | |
| Step-by-step content or code to explain | |
| At least one original insight, pitfall, or benchmark | |
| Preferred CTA | |

### Required fields — Format B (Narrative)

| Field | Status |
|-------|--------|
| What the "before" system or approach was | |
| The specific trigger that forced a change | |
| Alternatives that were considered (and ruled out) | |
| Why the chosen approach was selected | |
| What broke or surprised you during execution | |
| Concrete before/after metrics or outcomes | |
| The one lesson you'd pass on to another team | |
| Preferred CTA | |

---

## Step 2 — Clarifying Questions

If any required field is missing and cannot be inferred, ask about it before drafting. Group all questions into a single message — do not ask one at a time across multiple turns.

### Rules for asking:
- Ask only about fields that are genuinely missing — do not ask about things already answered in the input
- Maximum 5 questions per check-in — prioritize the ones that affect the most sections
- Frame questions around what the reader needs, not what the framework requires (e.g., "What was the tipping point that made the old system unworkable?" not "Please fill in the 'trigger' field")
- If a question has a sensible default the agent can assume, state the assumption and ask the user to correct it rather than leaving it open-ended

### Question bank — Format A (Tutorial)

Use these when the relevant field is missing:

**Topic / keyword:**
> "What's the specific problem this post should help someone solve? One sentence is fine — I'll build the keyword angle from there."

**Audience:**
> "Who's the target reader — someone just getting started with [X], or someone who already knows the basics and wants to go deeper?"

**Original insight:**
> "Is there something you discovered about [topic] that surprised you, or a mistake you see people commonly make? Even one concrete observation will make the post stand out."

**Code or steps:**
> "Do you have code, commands, or a process outline I can work from? Or should I draft the technical steps and you'll review for accuracy?"

**CTA:**
> "What do you want the reader to do at the end — subscribe, share, try a demo, or read a related post?"

---

### Question bank — Format B (Narrative)

Use these when the relevant field is missing:

**Before state:**
> "Can you describe what the old system looked like — roughly what it was, how long you'd been running it, and what started going wrong?"

**Trigger:**
> "What was the specific moment or event that made the status quo unacceptable? An incident, a growth inflection point, a failed deploy?"

**Alternatives considered:**
> "What other approaches did you seriously consider before landing on [chosen solution]? Even a quick 'we looked at X but ruled it out because Y' is enough."

**Decision reasoning:**
> "What ultimately tipped the decision toward [chosen approach]? And what was the main tradeoff you accepted by going that route?"

**What broke:**
> "What surprised you most during the migration — something that didn't go to plan, or a problem you hadn't anticipated?"

**Metrics:**
> "Do you have any before/after numbers you can share — latency, error rates, deploy frequency, incidents, cost? Even rough figures are better than none."

**The lesson:**
> "If a team came to you today about to do the same migration, what's the one thing you'd make sure they knew going in?"

**CTA:**
> "How do you want to close — invite comments, link to a related post, or point to the repo/RFC if it's public?"

---

## Step 3 — Confirm Before Drafting

Once all required fields are either present, inferred, or answered:

1. Briefly summarize what you're about to write (2–3 sentences: format, main angle, target reader) — this gives the user a chance to correct the direction before a full draft is written
2. State any assumptions made for fields that were inferred rather than explicitly provided
3. Ask for a go-ahead, or proceed directly if the user has already said "write it"

**Example confirmation:**

> "I have enough to start. I'll write this as a Format B narrative — the story of migrating from a monolithic deploy to per-service CI pipelines, aimed at senior engineers at scaling startups. I'm assuming the before-state p99 latency was around 800ms based on your notes; correct me if that's off. Writing now unless you want to change anything."

---

# Agent Protocol: Sensitive Information Guard

## Run this before writing or sharing any draft

This protocol runs before the clarifying questions and before any content is generated. Its purpose is to ensure that nothing in the post — names, metrics, architecture details, incident descriptions — exposes the author, teammates, employers, or third-party vendors to reputational, legal, or professional risk.

**The default position is: protect first, ask second.** If in doubt about whether something is sensitive, treat it as sensitive until told otherwise.

---

## What counts as sensitive

### People
- Full names of teammates, managers, or colleagues involved in decisions or incidents — unless they have publicly written about the same event themselves
- Attribution of specific mistakes or failures to named individuals
- Quotes or paraphrased opinions from internal discussions (Slack, meetings, RFCs)

### Company and employer
- Unreleased product details, roadmap items, or internal architecture not publicly documented
- Internal cost figures, revenue numbers, or business metrics not in public filings or press releases
- Incident details that could reflect badly on the company's reliability or engineering culture if read by customers or press
- Details about ongoing security vulnerabilities, even if already patched

### Vendors and third parties
- Criticism of a specific vendor by name where the claim isn't publicly documented or verifiable
- SLA failures or support quality issues tied to a named vendor
- Pricing or contract terms shared under NDA

### Code and systems
- Internal service names, internal domain names, or internal endpoint paths that reveal infrastructure topology
- API keys, tokens, credentials, or anything that looks like one — even example placeholders that follow a real pattern
- Internal tool names that combined with architecture details could fingerprint the company's stack to a competitor

---

## What to do when sensitive content is detected

### Step 1 — Flag before writing
Before generating any draft, if sensitive content is present in the input, list what was found and ask:

> "I noticed a few things in your notes that might be worth anonymising before this goes public. I'd like to flag them before I write anything:
>
> - [Item 1 — e.g., teammate's full name tied to a specific mistake]
> - [Item 2 — e.g., internal service name that reveals infrastructure]
> - [Item 3 — e.g., exact cost figure from an internal dashboard]
>
> For each one: should I anonymise it, remove it, or keep it as-is because it's already public? I won't proceed until I know."

### Step 2 — Anonymisation strategies (apply only after confirmation)

| Sensitive element | Safe replacement |
|------------------|-----------------|
| Teammate's name | Role only ("a senior engineer on the team", "our infrastructure lead") |
| Company-internal system name | Generic descriptor ("our primary data pipeline", "the monolith") |
| Exact internal cost figure | Order-of-magnitude range ("roughly $X0k/month") or omit |
| Vendor name (negative context) | Category ("our previous cloud provider", "the SaaS tool we were using") |
| Incident specifics tied to a named customer | Fully anonymised ("a high-traffic customer segment") |
| Internal repo or service path | Placeholder (`[internal-service]`) |
| Specific headcount or team size | Range ("a team of 5–8 engineers") |

### Step 3 — Never silently remove
Do not quietly drop sensitive information without telling the author. Always flag what was removed or changed and why, so the author can decide if the omission affects the story in a way they want to address differently.

---

## Sensitive information checklist (run before publishing)

- [ ] No teammate named in connection with a mistake or failure without their explicit consent
- [ ] No internal system names, paths, or endpoints that reveal infrastructure topology
- [ ] No exact cost, revenue, or business metrics not already in public sources
- [ ] No vendor criticism by name without a publicly verifiable source
- [ ] No incident details that read as a customer-facing reliability issue
- [ ] No credentials, tokens, or key-shaped strings anywhere in code examples
- [ ] All quotes are either your own words or from publicly attributed sources

---

# Agent Protocol: Draft Review Mode

## When the input is an existing draft (not raw notes)

If the user shares a draft that already exists — whether a rough outline, a near-complete post, or anything in between — the agent does **not** start rewriting from scratch. Instead it runs a full structured review against the applicable format checklist and flags every gap, weakness, and violation before touching a word.

---

## How to detect draft input

The input is a draft (not raw notes) if it:
- Contains prose paragraphs with headings
- Has a recognisable post structure (intro, sections, conclusion)
- Is explicitly described as "a draft", "something I wrote", or "can you review this"

If the input is ambiguous (e.g., a mix of bullet notes and partial paragraphs), ask:

> "Is this a draft you'd like reviewed and improved, or raw notes you'd like me to build a post from? The approach is quite different."

---

## Draft review process

### Step 1 — Identify the format
Determine whether it's Format A (Tutorial) or Format B (Narrative) and state this at the start of the review.

### Step 2 — Run the full checklist
Go through every item in the applicable format checklist. For each item, mark it as one of:
- ✅ Present and strong
- ⚠️ Present but weak — explain specifically what's missing or could be stronger
- ❌ Missing entirely — explain what needs to be added and why it matters

Present the review as a structured checklist output, not a wall of prose feedback.

### Step 3 — Run the sensitive information checklist
Regardless of how polished the draft is, run the full sensitive information checklist from the protocol above. Flag anything that needs to be addressed before publishing.

### Step 4 — Run the storytelling voice check
Check the draft against the storytelling voice guidelines. Flag:
- Sections that read like documentation rather than a story
- Passive constructions that distance the author from the decision
- Places where the emotional reality of the situation is absent (the stress, the uncertainty, the relief)
- Transitions between sections that feel abrupt or mechanical

### Step 5 — Prioritise feedback
After the full review, summarise:
- The top 3 things to fix before this post is ready to publish
- Any quick wins that would improve the post significantly with minimal rewriting

### Step 6 — Ask before rewriting
Do not rewrite sections without asking. After delivering the review, ask:

> "Would you like me to rewrite any of these sections, or would you prefer to revise them yourself based on this feedback?"

If the user says "just fix it", rewrite only the flagged sections — do not rewrite sections that were marked ✅.

---

# Agent Protocol: Storytelling Voice

## Apply to every sentence of every post, both formats

Technical writing defaults to documentation mode: passive voice, third-person distance, flat declarative sentences. This framework requires a different register — one that puts the reader inside the situation as it unfolds, not looking at it from outside after the fact.

The goal is not to make technical content "casual" or "fun". It is to make the reader feel the weight of the decision, the texture of the problem, and the humanity of the people involved — while remaining technically precise.

---

## Core principles

### Write from inside the moment, not above it
Documentation: *"A decision was made to migrate to a microservices architecture."*
Storytelling: *"We spent three weeks arguing about it in design docs before anyone admitted the monolith was the problem."*

The storytelling version puts the reader in the room. They feel the friction, the delay, the reluctance to name the real issue.

### Name the emotion without over-explaining it
You don't need to say "we were stressed". You need to describe the situation that produced the stress.

Documentation: *"The incident caused significant concern across the team."*
Storytelling: *"By the third page in two weeks, the on-call rotation had become something people were actively trying to trade away."*

### Use specific details instead of general statements
General: *"The old system didn't scale well."*
Specific: *"At 40,000 requests per minute, the queue would back up and the whole pipeline would stall. We'd watch the dashboards, wait, and hope it cleared before a customer noticed."*

Specificity is what makes a reader trust you. Anyone can say "it didn't scale". Only someone who was there can describe watching the dashboards.

### Vary sentence length deliberately
Long sentences carry accumulating complexity — they work for building context, listing what you tried, describing a situation getting worse. Short sentences land hard. They work for conclusions, reversals, moments of decision.

*"We tried rate limiting. We tried caching at the edge. We rewrote the hot path twice. None of it was enough. The problem wasn't the code — it was the architecture."*

### Let transitions carry the story forward
Avoid mechanical transitions ("Now we will discuss...", "In this section..."). Use transitions that carry momentum:
- *"That's when we realised..."*
- *"The fix seemed obvious — until we tried it."*
- *"Three months later, we were back in the same room with the same problem."*

---

## Voice checklist (run on every draft)

- [ ] No passive constructions where an active voice would be more direct ("a decision was made" → "we decided")
- [ ] No section that reads like documentation — every section should have a human subject doing something
- [ ] At least one specific, concrete detail per major section (a number, a scene, a reaction, a quote)
- [ ] Sentence length varied — no three consecutive sentences of the same length
- [ ] Transitions between sections feel like story momentum, not chapter headings
- [ ] The reader can feel what was at stake — not just what was done

---

## What storytelling voice is NOT

- It is not informal or sloppy — technical precision is non-negotiable
- It is not self-congratulatory — the story serves the reader's understanding, not the author's ego
- It is not dramatised beyond what actually happened — no invented tension, no exaggerated stakes
- It does not replace structure — the framework sections still exist; the voice is how you fill them

---

# Agent Protocol: Platform Optimisation

## Apply after the post is complete, before publishing

This protocol runs once the post is written and reviewed. Its purpose is to produce two publish-ready versions — one optimised for **dev.to** and one for **Medium** — since each platform has a different audience, discovery mechanism, and formatting expectation.

Do not apply both sets of optimisations to the same file. Produce separate outputs or clearly marked sections for each platform.

---

## dev.to optimisation

### Audience
Practising developers, mostly mid-level to senior. Skew toward open-source, tooling, and hands-on technical content. Community is conversational and values directness over polish.

### Discovery mechanism
dev.to uses **tags** as the primary discovery mechanism. Posts surface in tag feeds and on the homepage "Top" and "Latest" lists. Engagement (reactions, comments, saves) within the first few hours drives homepage placement.

### Formatting rules
- Use the standard Markdown front matter block at the top of every post:
```
---
title: [Post title]
published: true
description: [One sentence — this appears in the feed card, keep it under 160 chars]
tags: [tag1, tag2, tag3, tag4]
cover_image: [URL to cover image if available]
canonical_url: [Leave blank if dev.to is the primary; set to your blog URL if cross-posting]
---
```
- Use `##` and `###` headings — `#` renders too large on dev.to
- Code blocks must use triple backticks with a language identifier: ` ```javascript ` not ` ``` `
- Images: use direct URLs or uploaded images — dev.to CDN handles resizing
- Callout boxes: use the dev.to liquid tag `{% note %}` for tips and warnings — they render as styled cards

### Tags — rules and strategy
- Maximum 4 tags per post
- Use the highest-traffic relevant tags — check dev.to tag pages for follower count before choosing
- Always include one broad tag (`webdev`, `programming`, `javascript`) and one specific tag (`postgres`, `kubernetes`, `rust`)
- Avoid tags with under 1,000 followers — they get no traffic
- Tag selection checklist:
  - [ ] 1 broad, high-traffic tag
  - [ ] 1–2 technology-specific tags matching the post content
  - [ ] 1 format or intent tag if applicable (`tutorial`, `discuss`, `showdev`)

### CTA for dev.to
- End with a question to the community — dev.to comments are active and a good comment thread surfaces the post further
- Example: *"Have you run into this same problem? What did your team do differently — I'd genuinely like to know."*
- Do not end with a newsletter signup CTA — dev.to readers respond poorly to it

### Timing
- Post Tuesday–Thursday, 9–11am UTC — peak dev.to traffic window
- Engage with early comments within the first 2 hours — it signals activity and boosts placement

---

## Medium optimisation

### Audience
Broader technical audience — includes non-engineers (PMs, founders, tech leads). Skew toward engineering culture, career, and architecture posts more than hands-on tutorials. Readers expect more polished prose.

### Discovery mechanism
Medium uses **publications** and the **Medium Partner Program** for distribution. Posts submitted to publications (e.g., Better Programming, Towards Data Science, The Startup) get editorial distribution to their subscriber base. The algorithm also surfaces posts based on reading history and tags.

### Formatting rules
- Medium does not use Markdown — it uses a rich text editor. When preparing the post, note which elements need manual formatting:
  - Headings: use Medium's H1/H2 drop-down (do not paste Markdown `##`)
  - Code blocks: use Medium's code block (monospace block) — paste code after publishing to avoid formatting loss
  - Pull quotes: use Medium's drop cap or quote block for key sentences — these increase reading time metrics
  - Images: upload directly; always add a caption (Medium captions are indexed and read by the algorithm)
- No front matter block — Medium has its own metadata fields in the editor

### Tags
- Maximum 5 tags
- Medium tags are broader than dev.to — use topic-level tags: `Software Engineering`, `Programming`, `Technology`, `Startup`, `JavaScript`
- Tag checklist:
  - [ ] At least 1 tag matching a major Medium publication's focus area (improves submission fit)
  - [ ] No tags with no clear audience (avoid overly niche tags on Medium)

### Publication strategy
- Identify the most relevant Medium publication before writing — tailor the framing slightly toward that publication's audience
- Submit to only one publication per post — simultaneous submissions are not allowed
- If rejected, wait 48 hours before submitting to the next publication on your list
- Recommended publications for technical narrative posts:
  - *Better Programming* — engineering practice, architecture, team stories
  - *The Startup* — broader tech + business audience, good for migration stories with business impact
  - *Level Up Coding* — hands-on technical tutorials

### CTA for Medium
- Medium readers respond well to newsletter CTAs — end with a link to subscribe if you have one
- Avoid direct "share this post" asks — Medium's algorithm already handles distribution
- If you don't have a newsletter, end with a follow prompt: *"If this was useful, following me here means you'll see the next one."*

### Timing
- Post Wednesday–Friday, 12–3pm EST — Medium's peak reading window tracks US East Coast lunch and afternoon
- Do not post on weekends — Medium traffic drops significantly

### Canonical URL (cross-posting)
If publishing on both platforms:
- Decide which platform is **primary** (where the post lives first)
- On the secondary platform, set the canonical URL to the primary post's URL
- On dev.to: set `canonical_url` in the front matter
- On Medium: set via *More options → Advanced settings → Canonical link* before publishing
- Publish on the primary platform first, wait at least 24 hours, then publish on the secondary with the canonical set

---

## Platform optimisation checklist

### dev.to
- [ ] Front matter block complete (title, description, tags, canonical if cross-posting)
- [ ] 4 tags selected — 1 broad, 1–2 specific, 1 intent/format
- [ ] Code blocks use language-identified triple backticks
- [ ] Post ends with a community question CTA
- [ ] Scheduled for Tuesday–Thursday, 9–11am UTC

### Medium
- [ ] Submitted to one target publication
- [ ] 5 tags selected — at least 1 matching publication focus
- [ ] All images have captions
- [ ] Pull quote added for the most shareable sentence in the post
- [ ] Canonical URL set if cross-posting
- [ ] Post ends with newsletter or follow CTA
- [ ] Scheduled for Wednesday–Friday, 12–3pm EST

---

# Format A: Tutorial / How-To

## Agent Behavior

When writing or reviewing a tutorial-style post, follow this framework section by section. Each section has a clear purpose, target length, and SEO intent. Do not skip sections — each one serves either the reader experience or search discoverability (usually both).

---

## 1. Title (H1)

**Goal:** Hook the reader and signal relevance to search engines.

- Place the primary keyword within the first 60 characters
- Use an action verb + specific outcome format
- Formula: `"How to [do X] with [Y] (and avoid [Z])"`
- Avoid vague titles — be specific about what the reader will gain

**Example:**
> "How to Build a Rate Limiter in Go (and Avoid the Common Pitfalls)"

---

## 2. Introduction (150 words)

**Goal:** Confirm the reader is in the right place and establish the problem.

- Open with the pain point — not a definition
- State clearly what the reader will learn by the end
- Naturally include a secondary keyword
- Do not start with "In this post, we will..." — lead with the problem

**Checklist:**
- [ ] Pain point in sentence 1–2
- [ ] Promise of outcome by end of post
- [ ] Secondary keyword included naturally

---

## 3. TL;DR / Key Takeaways Box

**Goal:** Retain skimmers; improve search snippet coverage.

- 3–5 bullet points summarizing the post's core lessons
- Place immediately after the introduction
- Write these as standalone sentences (no context needed)

**Why it matters:** Search engines may pull this as a featured snippet. Skimmers who see value here are more likely to read the full post.

---

## 4. Prerequisites & Audience

**Goal:** Set skill-level expectations and reduce bounce rate from the wrong audience.

- State the assumed knowledge level (e.g., "Familiarity with Node.js and REST APIs")
- List any tools, versions, or accounts the reader needs before starting
- Keep this section brief — 3–5 lines maximum

---

## 5. Table of Contents (Anchor Links)

**Goal:** Improve navigation and earn sitelinks in search results.

- Generate anchor links to each H2 section
- Place after prerequisites
- Use short, descriptive link labels

**Why it matters:** Jump links in the ToC can appear as expandable sitelinks in Google results, dramatically improving click-through rate.

---

## 6. Body Sections — H2 + H3 Structure (Repeat 3–5×)

**Goal:** Deliver the core content in scannable, searchable chunks.

### H2 guidelines
- One concept per H2 section
- Include a keyword variant (synonym or related phrase) in the heading — not the exact primary keyword repeated
- Target 300–500 words per section

### H3 guidelines
- Use H3s to break long sections into sub-topics
- Aids scanning and reduces wall-of-text effect

### Within each section, include at least one of:

#### Code block
- Syntax highlighted
- Copyable (one-click copy button)
- Annotated with inline comments where logic is non-obvious

#### Diagram or screenshot
- Always include descriptive alt text (SEO + accessibility)
- Label key parts of the diagram
- Prefer custom diagrams over stock images

### Per-section checklist:
- [ ] One main idea per H2
- [ ] Keyword variant in heading
- [ ] 300–500 words
- [ ] At least one code block, diagram, or visual
- [ ] H3 subsections if section exceeds 400 words

---

## 7. Differentiated Insight

**Goal:** Provide value that cannot be found by rephrasing other sources.

Include at least one of the following:
- **Original benchmarks** — run the test yourself and share real numbers
- **Counterintuitive finding** — something that surprised you during research or implementation
- **"Why it works" explanation** — go below the surface of "what to do" into the mechanics
- **Pitfalls from experience** — mistakes you or your team actually made

**Why it matters:** Search engines increasingly reward content that demonstrates original expertise. This section is what earns links from other posts.

---

## 8. FAQ Section (Schema Markup)

**Goal:** Capture long-tail search queries and earn rich snippets.

- Write 3–5 questions that mirror "People also ask" queries on your topic
- Answer each in 2–4 sentences
- Mark up with `FAQPage` JSON-LD schema in the page source

**Format:**
```
Q: [Question readers actually search for]
A: [Direct, complete answer in 2–4 sentences]
```

---

## 9. Internal + External Links

**Goal:** Signal topical authority and improve crawlability.

| Type | Target | Notes |
|------|--------|-------|
| Internal | 3–5 links | Link to related posts on your site |
| External | 1–2 links | Link to authoritative sources (docs, papers, official specs) |

- Anchor text should be descriptive — never "click here"
- Internal links should point to posts that go deeper on a subtopic you mention

---

## 10. Conclusion + Call to Action

**Goal:** Cement the key lesson and give the reader one clear next step.

- Recap the single most important takeaway in 1–2 sentences
- Give exactly **one** CTA — multiple CTAs dilute each other

**CTA options (pick one):**
- Subscribe to the newsletter
- Share the post
- Try the linked demo or repo
- Read the next related post

---

## Meta Guidelines

### Publishing cadence
- Consistency beats volume — a predictable schedule signals freshness to search engines
- Aim for at least one post per 2 weeks when starting out

### Post length
- **1,200–2,000 words** for most technical posts
- Longer only if the extra content is genuinely useful — do not pad

### Updating old posts
- Update existing posts with new information rather than writing a new one
- Add an "Updated: [date]" note at the top
- This preserves ranking while signaling freshness

### Distribution (day of publish)
1. Publish the post
2. Share a Twitter/LinkedIn thread summarizing the key insight
3. Post in relevant communities (dev.to, Hacker News, relevant subreddits) where appropriate
4. Add to your newsletter if applicable

---

## SEO Checklist (per post)

- [ ] Primary keyword in title (first 60 chars)
- [ ] Secondary keyword in introduction
- [ ] Keyword variants in H2 headings
- [ ] Meta description written (150–160 chars, includes primary keyword)
- [ ] All images have descriptive alt text
- [ ] Table of contents with anchor links
- [ ] FAQPage schema added
- [ ] 3–5 internal links
- [ ] 1–2 external links to authoritative sources
- [ ] TL;DR / key takeaways box present
- [ ] One clear CTA at the end

---

## Post Template (Quick Start)

```markdown
# [Action verb] + [specific outcome] with [technology] (and [avoid/bonus outcome])

[Introduction — pain point first, 150 words, secondary keyword included]

## TL;DR
- [Takeaway 1]
- [Takeaway 2]
- [Takeaway 3]

## Prerequisites
- [Skill or tool 1]
- [Skill or tool 2]

## Table of Contents
- [Section 1](#section-1)
- [Section 2](#section-2)
- [Section 3](#section-3)

## [H2 — Core concept or step 1]
[300–500 words. Keyword variant in heading.]

### [H3 subsection if needed]

```code
// example
```

## [H2 — Core concept or step 2]

## [H2 — Core concept or step 3]

## The part nobody tells you
[Differentiated insight — original finding, benchmark, or pitfall]

## FAQ

**Q: [Long-tail question]**
A: [2–4 sentence answer]

**Q: [Long-tail question]**
A: [2–4 sentence answer]

## Conclusion
[1–2 sentence recap of the core lesson]

[Single CTA]
```

---

# Format B: Engineering Narrative

## Agent Behavior

When writing or reviewing an engineering narrative post, follow this framework. The goal is **not** to teach a process — it is to share lived judgment. Readers come for the reasoning behind decisions, the honest account of what broke, and the lesson they can apply to their own situation. Do not restructure this into a tutorial. Do not sanitize the failures. The credibility comes from specificity and honesty.

---

## 1. Title (H1)

**Goal:** Signal that this is a first-person account with a concrete outcome — not a tutorial.

- Lead with what happened and what changed, not what the reader will "learn to do"
- Include the technology names for search discoverability
- Formulas that work well:
  - `"Why we moved from [X] to [Y]"`
  - `"How we migrated [system] to [architecture] — and what we'd do differently"`
  - `"[X] wasn't working for us. Here's what we replaced it with and why"`

**Example:**
> "Why We Replaced Our Monolith with an Event-Driven Architecture (And What We Got Wrong)"

---

## 2. Opening — The Moment of Tension (200 words)

**Goal:** Pull the reader into the situation before explaining any technical context.

- Open with the specific moment things broke, the decision that had to be made, or the constraint that forced change
- Do **not** open with background on your company or team — that comes later
- Do **not** open with "In this post, we will..." — drop the reader into the scene
- The reader should feel the pressure of the situation before they understand the technical details

**What to capture:**
- What was happening at the time (scale, incident, business pressure)
- Why the status quo was no longer acceptable
- The stakes of getting the decision wrong

**Checklist:**
- [ ] Tension or problem established in first 2–3 sentences
- [ ] Reader understands why this decision mattered
- [ ] No solution mentioned yet — just the problem

---

## 3. Context — The Before State

**Goal:** Help the reader understand what you had and why it made sense at the time.

- Describe the original architecture or approach neutrally — it worked once, and that's worth acknowledging
- Explain when and why it started showing cracks (traffic, team size, deployment pain, incidents)
- Include concrete signals: latency numbers, deploy frequency, incident count, on-call load
- Keep this honest — avoid making the old system sound obviously bad in hindsight

**What to include:**
- A brief architecture diagram or description of the old system
- The specific symptoms that signaled a problem (with real numbers where possible)
- How long you lived with the problem before acting

---

## 4. The Decision — Options Considered and Why You Chose What You Did

**Goal:** This is the most valuable section. Share the reasoning, not just the outcome.

- List the real alternatives you considered — at least two, ideally three
- For each option, explain what made it attractive and what ruled it out
- Be honest about uncertainty: if you weren't sure, say so
- Explain what finally tipped the decision

**Format for each option considered:**

```
### Option: [Name]
**What appealed to us:** [1–2 sentences]
**Why we didn't choose it:** [1–2 sentences]
```

**For the chosen approach:**
- Explain the core tradeoff you accepted — every architecture decision trades one thing for another
- Name the assumption your decision depended on (e.g., "This only works if traffic growth stays linear")

**Checklist:**
- [ ] At least 2 alternatives considered and explained
- [ ] Tradeoffs named explicitly — not just "X was better"
- [ ] The deciding factor is stated clearly
- [ ] Any uncertainty or risk acknowledged

---

## 5. The Migration — What Actually Happened

**Goal:** Give an honest account of the execution, including what surprised you.

Structure this chronologically, not as a cleaned-up success story.

### What to cover:
- **The plan going in** — what you expected the migration to look like
- **What broke or surprised you** — the thing you didn't anticipate; this is the most valuable part of the post
- **The pivots** — decisions you had to revise mid-migration
- **Tooling and tactics** — specific tools, patterns, or techniques that helped (strangler fig, feature flags, dual writes, shadow traffic, etc.)
- **The rollback moment** — if you had to roll back or pause, describe it; if you didn't, explain what safeguards prevented it

### What not to do:
- Don't skip the hard parts to get to the success
- Don't describe the migration as smoother than it was — readers know migrations are painful
- Don't list every step — focus on the moments of decision and surprise

---

## 6. The After State — Concrete Results

**Goal:** Give the reader a clear, honest picture of what changed.

- Use real numbers wherever possible: latency (p50, p95, p99), error rates, deploy frequency, incident count, cost
- Acknowledge what didn't improve or what got worse as a tradeoff
- Compare to the specific symptoms you described in the Before State — close the loop

**Format:**

| Metric | Before | After |
|--------|--------|-------|
| p99 latency | 1,200ms | 180ms |
| Deploys per week | 2 | 14 |
| On-call incidents / month | 18 | 4 |

- If you don't have numbers, describe the qualitative change specifically — not "it was better" but "the on-call rotation went from weekly pages to one incident in the following month"

---

## 7. What We'd Do Differently

**Goal:** Provide the lesson that readers can apply without going through the same pain.

- Be specific — "start the migration earlier" is not actionable; "migrate the write path before the read path — we did it backwards and had to redo three weeks of work" is
- Include at least one thing you'd do the same, not just regrets — this builds credibility
- This section is what gets the post bookmarked and shared

**Prompts to answer:**
- What was the biggest incorrect assumption going in?
- What would you tell a team starting this migration today?
- What would you do in week 1 that you didn't do until week 6?

---

## 8. Internal + External Links

**Goal:** Connect to related context without interrupting the narrative flow.

| Type | Target | Notes |
|------|--------|-------|
| Internal | 2–4 links | Link to posts that explain concepts you reference but don't explain |
| External | 1–3 links | Link to the docs, papers, or posts that influenced your decision |

- Place links inline where they're relevant — do not cluster them at the end
- Anchor text should name the concept: "the strangler fig pattern" not "this pattern"

---

## 9. Conclusion — The One Lesson

**Goal:** Land on the single transferable insight, not a summary of what you did.

- Do not recap the migration — the reader just read it
- State the one thing you'd tell a team facing the same situation
- This should be an opinion, not a platitude: "Don't migrate your auth service last — it touches everything and you'll regret saving it" beats "plan carefully"
- End with one CTA

**CTA options (pick one):**
- Ask a question that invites comments ("We're still not sure about X — how did your team handle it?")
- Link to the next related post
- Link to the repo, RFC, or design doc if it's public

---

## Narrative Tone Guidelines

The full storytelling voice rules are in the [Storytelling Voice protocol](#agent-protocol-storytelling-voice) and apply to every section of this post. In addition, these rules are specific to Format B:

- Write in first-person plural ("we decided", "our team") — this is a team story, not a personal essay
- Use past tense for what happened; use present tense for lessons and recommendations
- Name the people involved only where the Sensitive Information Guard permits — role titles are usually sufficient
- Avoid hedging language that undermines your authority: "it seemed like maybe" → "we believed"
- Avoid corporate language: "we leveraged synergies" → "we reused the existing pipeline"
- One technical depth level: go deep enough to be credible, not so deep that context is required to follow along

---

## SEO Checklist for Narrative Posts

Narrative posts rank differently from tutorials — they earn links rather than search volume. Still run this checklist:

- [ ] Technology names in the title (for search discoverability)
- [ ] Meta description written as a one-sentence story hook (150–160 chars)
- [ ] Architecture/system names used consistently (not abbreviated differently across sections)
- [ ] Real numbers in the After State (these get cited and linked)
- [ ] "What we'd do differently" section present (this is the most-linked section in narrative posts)
- [ ] 2–4 internal links to related posts
- [ ] One clear CTA at the end

---

## Narrative Post Template (Quick Start)

```markdown
# Why we [did X] — and what we'd do differently

[Opening scene — the moment of tension, 2–3 sentences. No background yet.]

[Context paragraph — what the situation looked like before you acted.]

## TL;DR
- [The core decision in one sentence]
- [The biggest surprise]
- [The one thing you'd do differently]

## Table of Contents
- [The before state](#the-before-state)
- [Why we decided to change](#why-we-decided-to-change)
- [What we considered](#what-we-considered)
- [The migration](#the-migration)
- [Results](#results)
- [What we'd do differently](#what-wed-do-differently)

## The before state
[Describe the original system neutrally. Include the symptoms that signaled a problem — with real numbers.]

## Why we decided to change
[The tipping point. What made the status quo unacceptable at that specific moment.]

## What we considered

### Option 1: [Name]
**What appealed to us:** [1–2 sentences]
**Why we didn't choose it:** [1–2 sentences]

### Option 2: [Name]
**What appealed to us:** [1–2 sentences]
**Why we didn't choose it:** [1–2 sentences]

### What we chose: [Name]
[Why this won. The tradeoff you accepted. The assumption it depends on.]

## The migration
[Chronological account. Lead with what you planned, then what surprised you.]

### What broke
[The thing you didn't anticipate.]

### How we handled it
[The pivot, the fix, the rollback if there was one.]

## Results

| Metric | Before | After |
|--------|--------|-------|
| [Metric 1] | [Value] | [Value] |
| [Metric 2] | [Value] | [Value] |

[What didn't improve, or what got worse as a tradeoff.]

## What we'd do differently
- [Specific, actionable lesson 1]
- [Specific, actionable lesson 2]
- [One thing you'd do the same]

## The bottom line
[One paragraph. The single transferable lesson for a team facing the same situation.]

[Single CTA]
```