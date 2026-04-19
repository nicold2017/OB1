# Founder OS — Product Specification
**Version:** 1.7  
**Owner:** Dirk  
**Status:** Ready to build — final spec before handoff to Claude Code  
**Purpose:** Shared context for Claude Code and any developer building this system

### Changelog
| Version | Changes |
|---|---|
| 0.1 | Core architecture, data schema, capture layer, MCP server, daily digest |
| 0.2 | Conway context, Business Discovery Engine, Creator Tracking, Content Engine |
| 0.3 | Security, idempotency SQL, Hono route fix, /generate-digest, Day 0 setup, voice profile, weekly review prompt, TokScript/Snowball, LinkedIn migration, pull/push paradigm, auto-save Skill |
| 0.4 | Themes system, tasks table, theme field on signals, real-time alerts, digest grouped by theme, manage_themes MCP tool, three output modes, weekly review pattern detection |
| 0.5 | Claude Projects integration — brain as unified memory layer, project system prompt template, project knowledge migration, Google Drive as signal source |
| 0.6 | Build strategy — OB1 as foundation codebase, Claude Code as build tool, Extension 5 adapts to people table, daily digest recipe as /generate-digest starting point |
| 1.0 | Version milestone. Strengthened Vision & Value Proposition. Added Why This Exists section. |
| 1.1 | LLM Council round 1. Phase 1 radically simplified (Slack-only). Review UI before MCP server. Two-stage classification. Quarantine lane. People routing fixed (people_drafts). Cost controls. Data export plan. Pre-build validation exercise. |
| 1.2 | LLM Council round 2. Jobs table queue (durable pipeline). Importance scoring layer. Multi-signal LLM splitting removed. Quarantine capped at 3 per digest. Cost degradation behavior defined. Rules engine observability footer. |
| 1.3 | LLM Council round 3 — final round. Fixed jobs worker (inline waitUntil primary, pg_cron 1-minute retry, SELECT FOR UPDATE SKIP LOCKED). Importance formula simplified to 2 variables. Delimiter capture pattern added. Dead jobs requeue MCP tool. Degraded-mode digest notification. Section numbering fixed. Auto-save contradiction resolved. Version reference corrected. Backup SQL fixed for Supabase Cloud. |
| 1.4 | Pre-build bookmark analysis incorporated. Themes expanded from 5 to 8 (added health, book, finance as Day 1 seeds). followed_creators pre-populated with 8 creators from frequency analysis. AEO flagged as Magentics training data. Skills theme updated for AI content. |
| 1.5 | Gemini API added as required dependency for Phase 2 creator scanning. /scan-creators fully specified with YouTube → Gemini API workflow, morning digest format, setup instructions. Manual YouTube interim workflow documented for Phase 1. |
| 1.6 | Grok API added for X/Twitter enrichment and to replace Nitter. Email monitoring added (Kill the Newsletter → RSS, Gmail filter + forward). X quote tweet classification rules added. Phase 1.5 updated. |
| 1.7 | Today Board added (Section 13.5) — execution layer that answers "what should I do today?" Generated fresh each morning as first section of digest. Hard caps: 3 MUST DO, 5 SHOULD DO. Deterministic SQL selection, no LLM. defer_task and skip_signal MCP tools added. Morning digest format updated with Today Board as opening section. |

---

## 1. Why This Exists — The Founder's Problem

Every insight you have as a founder evaporates. You read something interesting — it's gone by tomorrow. You have a great conversation with a founder in your network — the context fades within a week. You notice a competitor move and mean to do something about it — life intervenes. You have a business idea at 11pm — you think you'll remember it — you don't.

Your brain is running a constant background process trying to hold all of this together. It is losing.

And you're not just managing one business. You're running three or four in parallel — Magentics, Kovalency, AI Transformation, and whatever comes next — treating them as A/B tests in a market that's shifting faster than anyone can track. Every week, new AI tools emerge that could help or threaten each one. Competitors move. Your network has people who could open doors, if only you remembered to reach out. There are business opportunities hiding in Reddit threads and job boards and niche forums that no one has found yet. You're trying to stay on top of all of it by scrolling, bookmarking, and hoping your memory holds.

It doesn't. No one's does.

The Founder OS is the infrastructure layer that fixes this. It captures what you notice, classifies it automatically, stores it in a database you own, and surfaces it back to you — as a daily briefing, as real-time alerts, as content ideas, as relationship nudges, as business opportunities already pre-scored against your criteria. Nothing evaporates. Everything compounds.

### What You Actually Gain

**A daily briefing that assembles itself.** Every morning at 7am, one structured message arrives. It takes 60 seconds to read. You know exactly what matters today — what's urgent across your four businesses, who needs a follow-up, what tasks are due, what the best content opportunity is this week. You didn't gather any of it. It assembled itself overnight.

**An end to scrolling as a strategy.** You follow a handful of creators whose work matters. The brain reads everything they publish and sends you a curated daily update. You go from 45 minutes of scrolling to 60 seconds of digest. The signal-to-noise ratio inverts completely.

**A real A/B test across your businesses.** Right now, the decision about which business to double down on happens on intuition and recency bias — whatever feels most active this week. With the Founder OS, you get a signal-based weekly ranking of all four businesses by momentum. Which one is generating interesting signals? Which one's competitors are accelerating? Which one does your network keep bringing up? The A/B test becomes a real test with real data, not a gut feeling. And when one business is weakening, the system tells you before you've wasted another month on it.

**Content ideas that come to you.** The brain watches what signals are accumulating, notices when a topic has enough substance to write about, and surfaces it with the source material already organized. You go from staring at a blank screen to picking from a ranked list of topics the brain has been building for you all week — with a draft ready in the format you need.

**Relationships that don't go cold.** The CRM watches your contacts. It notices when you haven't talked to someone in 60 days, recalls the last context of your conversation, and surfaces a reason to reach out. The relationships that used to cool off quietly because life got busy now get a nudge at the right moment.

**A scout for your next business, running continuously.** Every week the discovery engine scans Reddit, job boards, Craigslist, and trend data looking for lifestyle business opportunities — under $25K to start, $100K/year potential, AI-resistant, manageable hours. It simulates each one, scores it against your rubric, and delivers a pre-analyzed shortlist Sunday evening. You stop vaguely wondering what else to build and start reviewing a ranked report.

**A to-do list that lives outside your head.** "Don't forget to take out the garbage tonight" goes into Slack, gets classified as a task, shows up in tomorrow's morning digest, and disappears when you mark it done. The mental RAM that was holding that open loop gets freed. Over time the background hum of *don't forget to...* quiets down significantly.

**Real-time alerts for the things that actually matter.** When a competitor launches a feature that threatens one of your businesses, your phone buzzes immediately. When a creator you follow publishes something directly relevant to your current build, you know within minutes — not the next time you happen to scroll past it.

**An AI that knows you.** After three months of using this, the brain holds things about your pattern of thinking that you would struggle to articulate yourself — what you keep coming back to, which business is generating the most interesting signals, who your highest-leverage relationships are, which content topics resonate with your audience. Every AI you use gets better because it has more context to work with. You stop re-explaining yourself and start doing actual work.

### The Compounding Advantage

This is the hardest thing to explain but the most important to understand: the system gets more valuable the longer you use it.

Every signal captured makes the next search smarter. Every person added to the CRM makes relationship surfacing more useful. Every content piece published gets tracked, and over time the brain learns which signal types actually drive engagement for your audience. Every business decision logged becomes context that informs the next one.

The people who build this kind of persistent, AI-accessible context infrastructure will have AI that gets better every week. The people who keep opening new chat windows and re-explaining themselves will wonder why AI still feels like a party trick. Same models. Same Tuesday. Wildly different outcomes.

### What It Is Not

It is not an autonomous system that runs your business for you. Every draft it writes, you review. Every opportunity it surfaces, you decide on. Every relationship it flags, you judge. The agent does the remembering, the pattern-finding, and the drafting. You do the deciding, the calling, and the building. That division is intentional — it is what makes the system trustworthy enough to actually use.

### In One Sentence

The Founder OS gives a solo founder running four parallel businesses the intelligence infrastructure that a well-resourced team would otherwise provide — and it gets smarter every week, costs almost nothing to run, and belongs entirely to you.

---

## 2. Vision & North Star

The Founder OS is a personal AI operating system built on the Open Brain architecture. It is self-hosted, personally owned infrastructure that makes AI genuinely useful across time and across multiple parallel businesses.

A founder running 3–4 parallel businesses-as-A/B-tests is constantly generating signals across fragmented sources. None of those signals compound — they evaporate. The Founder OS captures, classifies, stores, and surfaces those signals so they accumulate into strategic intelligence over time — and turns that intelligence into published content and validated business opportunities.

**The one-sentence test:** Did an offhand comment in June become an actionable insight in December, without the founder having to remember it? If yes, the system is working.

**Honest scope note (added after LLM Council review):** The full time-bridging value proposition — where a signal from June surfaces autonomously in December — requires Phase 3 (autonomous scanning and proactive surfacing). Phase 1 delivers a searchable inbox with a daily digest and manual semantic search via MCP. That is genuinely valuable and solves the real problem (bookmarks that sit in a bucket and never compound). But it is not yet the autonomous intelligence system described in Section 1. Build trust with Phase 1, then unlock the deeper value in later phases.

---

## 3. Design Principles

1. **Data ownership over convenience.** Everything lives in a Supabase Postgres instance the founder controls. No SaaS lock-in, no vendor memory silos.
2. **One capture habit beats five perfect tools.** Every input mechanism requires no more than a single gesture.
3. **Classify, don't organize.** The founder never decides where something belongs. The classification engine routes everything.
4. **The judgment line.** The agent surfaces and suggests. The founder decides and approves. The agent never acts autonomously without explicit approval.
5. **Build for restart, not perfection.** Missing a week is normal. Don't catch up — just restart.
6. **One workflow, then modules.** Build the core capture → classify → store → surface loop first. Add modules only after the core loop is trusted.
7. **Cross-model portability.** The brain connects via MCP. Claude, ChatGPT, Cursor, and any future model can read and write to the same database.
8. **Time-bridging is the core value.** A signal from six months ago should be available and actionable today, automatically.
9. **The brain is raw material, not the finished product.** Separate tools consume the brain's output — the Content Engine drafts posts, the Discovery Engine surfaces business ideas.
10. **Pull and push are both first-class.** Conversational clients handle pull (you ask, agent reasons). Autonomous agents handle push (they scan on schedule, surface proactively). Same database, different interfaces.
11. **Categories are configuration, not code.** New themes, goals, and life areas can be added by updating a database row — no code deployment required.
12. **The brain is the memory layer across all Claude Projects.** Individual Claude Projects hold focused context for specific work. The brain (Supabase via MCP) holds the cross-project intelligence — decisions, signals, and insights that matter regardless of which project you're working in. Projects are workspaces. The brain is memory.

---

## 4. The Four Active Businesses (Classification Context)

| ID | Name | Description | Stage |
|---|---|---|---|
| `magentics` | Magentics | AEO (Answer Engine Optimization) / GEO tool | Active |
| `kovalency` | Kovalency | Agent audit and compliance tool for regulated industries | Active |
| `ai_transformation` | AI Transformation | Education service helping companies transition to AI | Active |
| `new_idea` | New Idea | White space / blue ocean / lifestyle business opportunities | Scanning |

---

## 5. System Architecture Overview

```
╔══════════════════════════════════════════════════════════════════╗
║                        CAPTURE LAYER                             ║
║  Slack  │  Telegram  │  Chrome Ext  │  MCP Direct  │  RSS Auto   ║
╚══════════════════════════════╤═══════════════════════════════════╝
                               │
                               ▼
╔══════════════════════════════════════════════════════════════════╗
║                  SUPABASE EDGE FUNCTIONS                         ║
║  /ingest-signal    — classify, embed, route all manual inputs    ║
║  /telegram-brain   — Telegram webhook, same pipeline             ║
║  /generate-digest  — daily (7am) + weekly (Sun 6pm) digest       ║
║  /alert            — real-time Telegram push for act_now items   ║
║  /scan-creators    — daily RSS polling for followed creators     ║
║  /scan-discovery   — weekly lifestyle business scan              ║
╚══════════════════════════════╤═══════════════════════════════════╝
                               │
                               ▼
╔══════════════════════════════════════════════════════════════════╗
║                      SUPABASE POSTGRES                           ║
║  themes │ tasks │ signals │ people │ ideas                       ║
║  competitors │ competitor_signals │ learnings                    ║
║  followed_creators │ lifestyle_opportunities                     ║
║  content │ digests                                               ║
╚══════════════════════════════╤═══════════════════════════════════╝
                               │
               ┌───────────────┴───────────────┐
               ▼                               ▼
╔══════════════════════╗       ╔═══════════════════════════════════╗
║     MCP SERVER       ║       ║   ALWAYS-ON AGENT (Phase 3+)     ║
║  PULL interface:     ║       ║   PUSH interface:                 ║
║  Claude, ChatGPT,    ║       ║   Conway (Anthropic) or OpenClaw  ║
║  Cursor query brain  ║       ║   runs on schedule, surfaces      ║
║  on demand           ║       ║   proactively without prompting   ║
╚══════════════════════╝       ╚═══════════════════════════════════╝
```

**No n8n, no Zapier, no Make** for the core loop.

**On Conway (April 2026):** In internal testing at Anthropic. It is the natural always-on agent for Phase 3 — execution layer, not memory. Conway reads from and writes to Supabase. They are complementary, not competing. Monitor for MCP compatibility before committing. OpenClaw/Kilo Claw is the fallback.

---

## 6. Output Modes

The brain has three distinct ways of communicating with you. Understanding all three is important for setting up the system correctly.

### Mode 1 — Morning Briefing (proactive, scheduled)

Delivered at 7am daily via Slack `#founder-brain`. One structured message grouped by theme. Read it once, know what matters today. Full format in Section 10.

### Mode 2 — Real-Time Alerts (proactive, event-driven)

When a signal is classified as `urgency: act_now`, the `/alert` Edge Function fires immediately — it does not wait for the 7am digest. Delivered as a Telegram push notification so your phone buzzes regardless of whether you're looking at it.

Triggers for immediate alert:
- Any signal classified `act_now`
- A creator you follow publishes content flagged `build_relevant: true`
- A task's `due_date` arrives and status is still `open`
- A relationship `follow_up_date` arrives

The rule: **act_now → immediate Telegram push AND morning digest. Everything else → morning digest only.**

No SMS needed for most scenarios. If you want SMS escalation for truly critical items, that can be added later via Twilio — but Telegram covers 99% of use cases and requires no additional cost or setup.

### Mode 3 — On-Demand Queries (reactive, you-initiated)

Any time, from Slack or Claude: ask a question, the brain answers from accumulated context.

```
"What's in my skills backlog?"
"Who haven't I talked to in 60 days?"
"What should I write about this week?"
"Show me all Kovalency competitor moves this month"
"What lifestyle opportunities are above 7.0 score?"
"Have I learned anything relevant to building MCP servers?"
```

These work via MCP in Claude Desktop today. With a small Slack bot addition (Phase 2), they'll also work directly in Slack by prefixing with `/brain`.

---

## 7. Themes System

**This is the extensibility layer of the Founder OS.** Every captured item is tagged with both a `product_tag` (which business it relates to) and a `theme` (what area of life it belongs to). Themes define how the morning digest is structured, how the classification engine routes items, and what the weekly review looks for.

Adding a new life area — skills, health, travel, reading, gratitude — is a single database insert. No code changes. No redeployment. The classification prompt rebuilds dynamically from the themes table on every call.

### 7.1 `themes` Table

```sql
CREATE TABLE themes (
  id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  created_at TIMESTAMPTZ DEFAULT NOW(),

  name TEXT NOT NULL,            -- Display name: 'Skills to Build'
  slug TEXT UNIQUE NOT NULL,     -- Machine key: 'skills'
  description TEXT NOT NULL,     -- What belongs here (injected into classifier)
  goal TEXT NOT NULL,            -- What you want the brain to do with items here
  capture_examples TEXT[],       -- Phrases that should route to this theme
  digest_priority INT DEFAULT 5, -- 1=always show even if empty, 10=only if items exist
  active BOOLEAN DEFAULT TRUE
);
```

### 7.2 Starting Themes (Seed Data)

**v1.4 update:** Expanded from 5 to 8 themes based on pre-build bookmark analysis of the founder's actual capture behavior. Health, Book, and Finance are not "add later" themes — they are active capture categories with significant existing signal volume. All 8 are seeded on Day 1.

```sql
INSERT INTO themes (name, slug, description, goal, capture_examples, digest_priority)
VALUES

('Business Intelligence', 'business',
 'Signals about my four businesses — trends, competitors, tools, market moves, 
  anything that affects Magentics, Kovalency, AI Transformation, or new ideas.
  Includes Future of Work content (how AI changes team structure, startups, VC, 
  enterprise) and new business trends worth investigating.',
 'Surface threats and opportunities before they become obvious. Help me decide 
  which of my four businesses deserves more attention each week. Flag content 
  that is also worth turning into social media thought leadership.',
 ARRAY['competitor', 'trend', 'market', 'tool', 'oss', 'funding', 'launch',
       'future of work', 'startup', 'saas', 'enterprise ai', 'business model'],
 1),

('Skills to Build', 'skills',
 'Technologies, frameworks, techniques, or capabilities worth learning. 
  Includes Claude Code tutorials, GitHub repos, MCP patterns, agentic workflows, 
  open-source tools, and any hands-on technical capability that increases 
  founder leverage. Dual-purpose items (both a skill AND a business signal) 
  get tagged to both themes — classify by primary intent.',
 'Keep a prioritized backlog of things worth learning. Surface the oldest items 
  so they do not rot. Connect each skill to the business it serves. 
  Flag items sitting in backlog for more than 30 days.',
 ARRAY['learn', 'figure out', 'should understand', 'add to skills',
       'need to know', 'claude code', 'github repo', 'tutorial', 'how to build',
       'course', 'technique', 'workflow', 'mcp', 'open source'],
 3),

('Personal Tasks', 'personal',
 'Life admin, errands, one-time reminders, household items. Things that have 
  nothing to do with business but need to happen.',
 'Be a reliable to-do list. Surface time-sensitive items in the morning digest. 
  Clear these from mental RAM so they stop living rent-free in my head.',
 ARRAY['don''t forget', 'remind me', 'need to', 'have to', 'take out',
       'call', 'schedule', 'buy', 'fix', 'pick up', 'book'],
 6),

('Relationships', 'relationships',
 'People I want to stay in touch with, reach out to, or think about. 
  Both professional network and personal connections.',
 'Surface relationships going cold before it is too late. Prompt me to reach 
  out with context about why it matters and what to say.',
 ARRAY['should reach out', 'haven''t talked to', 'want to contact',
       'check in with', 'follow up with', 'owe a call to'],
 2),

('Content', 'content',
 'Ideas for posts, articles, videos, newsletters. Topics worth writing about 
  on LinkedIn, X, or TikTok. Future of Work and AI signals that have strong 
  thought leadership angles belong here when the primary intent is to publish.',
 'Turn accumulated signals into a content backlog. Surface opportunities 
  when signal density justifies writing something. Track what published 
  content performed and why.',
 ARRAY['write about', 'post idea', 'article', 'good topic', 'should share',
       'would make a good', 'thought leadership', 'linkedin post', 'thread'],
 5),

('Health & Longevity', 'health',
 'Content about maintaining health, reversing aging, reducing disease risk, 
  and sustaining performance through the founder years. Includes exercise 
  protocols, nutrition, supplements, lab tests, sleep, and longevity research. 
  Primary sources: David Sinclair, Peter Attia, and similar.',
 'Build a personal health protocol grounded in current research. Surface 
  actionable changes I can make. Flag anything that contradicts my current 
  habits. Keep a running list of tests or interventions worth trying.',
 ARRAY['longevity', 'aging', 'exercise', 'supplement', 'heart', 'sleep',
       'protein', 'vo2 max', 'zone 2', 'sinclair', 'attia', 'health protocol',
       'reverse aging', 'biological age', 'cardiovascular'],
 7),

('Book Project', 'book',
 'Content for the mental models book aimed at young adults who are lost. 
  Covers neuroscience, goal setting, identity formation, habits, addiction, 
  cognitive load, and Christian worldview (prayer, renewing the mind, 
  apologetics, biblical typology). Wes Huff content belongs here.',
 'Build a content library that feeds the book. Cluster by chapter topic. 
  Surface research that supports or challenges key arguments. Flag anything 
  that would work as a story, illustration, or case study in the manuscript.',
 ARRAY['neuroscience', 'mental model', 'habit', 'identity', 'addiction',
       'goal setting', 'young adult', 'christian', 'apologetics', 'prayer',
       'renewing the mind', 'biblical', 'worldview', 'cognitive', 'psychology',
       'melchizedek', 'wes huff', 'book research'],
 8),

('Finance & Investment', 'finance',
 'Personal financial strategy for a 59-year-old founder approaching exit window. 
  Covers 401k/IRA management, tax strategy, borrowing strategies, geopolitical 
  and monetary shifts that affect portfolio, and wealth preservation. 
  Distinct from business finance — this is personal wealth management.',
 'Surface actionable financial decisions before deadlines create urgency. 
  Flag geopolitical or monetary shifts that require portfolio adjustment. 
  Keep a running list of strategies to discuss with financial advisor.',
 ARRAY['401k', 'ira', 'tax', 'retirement', 'invest', 'portfolio', 'wealth',
       'borrow', 'geo', 'monetary', 'inflation', 'tariff', 'estate',
       '59 and a half', 'roth', 'withdrawal', 'financial advisor'],
 9);
```

### 7.3 Classification Note — Ambiguous AI Content

The "AI Features / Leverage" category is the hardest to route correctly. A Claude Code tutorial can simultaneously be:
- A `skills` signal (you want to learn this technique)  
- A `business` signal (this changes how you think about your products)
- A `content` signal (this is worth posting about)

**Routing rule for the classifier:** Use primary intent.
- Hands-on tutorial → `skills`
- Strategic implication for a specific business → `business` + product_tag
- Strong thought leadership angle → `content`
- When genuinely ambiguous → `skills` as default, tag the relevant product

The AEO/SEO/Agents category is a special case: signals here should always be tagged `magentics` AND flagged as potential training data for the Magentics product brain. The `recommended_action` field should note when something is training-data-worthy: *"Add to Magentics AEO best practices corpus."*

### 7.4 Examples of Themes to Add Later

These are genuinely deferred — not present in current capture behavior:

| Theme | When to add | Signal |
|---|---|---|
| Gratitude / Wins | When weekly review feels like only problems | "I keep forgetting what's working" |
| Hiring / Talent | When building a team | First job posting |
| Travel | When planning trips | More than 2 travel saves per month |
| Local Durham | When coffee/restaurant saves become frequent | 5+ local saves in a month |

### 7.5 How the Weekly Review Suggests New Themes

The Sunday weekly review prompt (Section 13.4) includes a pattern detection pass:

```
Scan all signals from the past 30 days that have low confidence scores 
or were routed to 'signals' with no clear theme match.
Look for clusters of 3+ signals that share a topic not covered by 
existing themes. If found, suggest a new theme with a proposed 
description and goal. Present as: "I noticed X signals about [topic] 
this month that don't fit existing categories. Should we create a 
[Theme Name] theme?"
```



---

## 8. Data Schema

### 8.1 `tasks` — Personal To-Dos and Reminders

Separate from `signals` (which is intelligence). Tasks are actionable items that need to be done and checked off.

```sql
CREATE TABLE tasks (
  id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  created_at TIMESTAMPTZ DEFAULT NOW(),

  title TEXT NOT NULL,
  notes TEXT,
  theme_slug TEXT REFERENCES themes(slug), -- 'personal' | 'skills' | 'relationships'
  product_tag TEXT,                         -- Set if task is business-related

  due_date DATE,
  due_includes_time BOOLEAN DEFAULT FALSE,
  due_datetime TIMESTAMPTZ,               -- Set when time matters (e.g., "call at 3pm")

  status TEXT DEFAULT 'open',             -- 'open' | 'done' | 'deferred' | 'cancelled'
  completed_at TIMESTAMPTZ,
  priority TEXT DEFAULT 'normal',         -- 'high' | 'normal' | 'low'

  source TEXT,                            -- 'slack' | 'telegram' | 'mcp'
  source_signal_id UUID REFERENCES signals(id)
);
```

**How tasks are created:** When the classification engine routes input to `tasks` (based on theme detection), it creates a task record. The classifier determines this based on theme match against the `personal`, `skills`, or `relationships` themes — specifically when the input describes something actionable rather than informational.

**Completion:** Reply to the thread in Slack: "done" or "✓" and the agent marks the task complete. Or via MCP: `complete_task(id)`.

### 8.2 `signals` — Primary Intelligence Inbox

```sql
CREATE TABLE signals (
  id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  created_at TIMESTAMPTZ DEFAULT NOW(),

  -- Raw input
  raw_content TEXT NOT NULL,
  source TEXT,              -- 'slack' | 'telegram' | 'chrome_ext' | 'mcp' |
                            --  'rss_creator' | 'rss_auto' | 'reddit' | 'github'
  source_url TEXT,
  creator_id UUID REFERENCES followed_creators(id),

  -- Idempotency
  slack_event_id TEXT,

  -- Classification
  signal_type TEXT,         -- 'tool_or_oss' | 'competitor_move' | 'market_trend' |
                            --  'blue_ocean_problem' | 'learning' | 'person' | 'idea'
  valence TEXT,             -- 'opportunity' | 'threat' | 'neutral'
  urgency TEXT,             -- 'act_now' | 'this_week' | 'monitor' | 'archive'
  theme_slug TEXT REFERENCES themes(slug), -- PRIMARY THEME for this signal

  product_tags TEXT[],
  recommended_action TEXT,

  -- Content potential
  content_worthy BOOLEAN DEFAULT FALSE,
  content_formats TEXT[],

  -- Semantic search
  embedding VECTOR(1536),

  -- Metadata
  confidence FLOAT,
  reviewed BOOLEAN DEFAULT FALSE,
  notes TEXT
);

-- DB-level deduplication
CREATE UNIQUE INDEX IF NOT EXISTS signals_slack_event_id_uidx
  ON public.signals (slack_event_id)
  WHERE slack_event_id IS NOT NULL;
```

### 8.3 `people` — Founder Network CRM

```sql
CREATE TABLE people (
  id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  created_at TIMESTAMPTZ DEFAULT NOW(),
  updated_at TIMESTAMPTZ DEFAULT NOW(),

  name TEXT NOT NULL,
  email TEXT,
  linkedin_url TEXT,
  company TEXT,
  role TEXT,

  relationship_type TEXT,   -- 'accelerator_network' | 'fcat' | 'nc_idea' |
                            --  'advisor' | 'potential_customer' | 'partner' | 'investor'
  how_we_met TEXT,
  notes TEXT,

  product_tags TEXT[],
  customer_potential TEXT,  -- 'high' | 'medium' | 'low' | 'none'

  last_contact_date DATE,
  follow_up_date DATE,
  follow_up_trigger TEXT,
  relationship_strength TEXT, -- 'strong' | 'warm' | 'cold' | 'dormant'

  embedding VECTOR(1536)
);
```

### 8.4 `ideas` — Product & Business Ideas Pipeline

```sql
CREATE TABLE ideas (
  id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  created_at TIMESTAMPTZ DEFAULT NOW(),

  title TEXT NOT NULL,
  one_liner TEXT,
  description TEXT,
  source TEXT,
  source_signal_id UUID REFERENCES signals(id),

  idea_type TEXT,            -- 'new_business' | 'feature' | 'pivot' | 'partnership'
  product_tags TEXT[],

  status TEXT DEFAULT 'new', -- 'new' | 'exploring' | 'validating' | 'building' |
                             --  'paused' | 'rejected' | 'promoted_to_project'
  rejection_reason TEXT,
  council_summary TEXT,
  council_date TIMESTAMPTZ,

  embedding VECTOR(1536)
);
```

### 8.5 `competitors` + `competitor_signals`

```sql
CREATE TABLE competitors (
  id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  created_at TIMESTAMPTZ DEFAULT NOW(),
  name TEXT NOT NULL,
  url TEXT,
  product_tag TEXT NOT NULL,
  notes TEXT,
  last_reviewed DATE
);

CREATE TABLE competitor_signals (
  id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  created_at TIMESTAMPTZ DEFAULT NOW(),
  competitor_id UUID REFERENCES competitors(id),
  signal_id UUID REFERENCES signals(id),
  move_description TEXT,
  our_response TEXT,
  urgency TEXT
);
```

### 8.6 `learnings` — Technology & AI Updates

```sql
CREATE TABLE learnings (
  id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  created_at TIMESTAMPTZ DEFAULT NOW(),
  title TEXT NOT NULL,
  summary TEXT,
  source_url TEXT,
  source_type TEXT,          -- 'release_notes' | 'article' | 'video' | 'podcast' | 'paper'
  product_tags TEXT[],
  theme_slug TEXT REFERENCES themes(slug),
  applied BOOLEAN DEFAULT FALSE,
  application_notes TEXT,
  embedding VECTOR(1536)
);
```

### 8.7 `followed_creators` — Creator Registry

```sql
CREATE TABLE followed_creators (
  id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  created_at TIMESTAMPTZ DEFAULT NOW(),

  name TEXT NOT NULL,
  why_i_follow TEXT NOT NULL,
  product_tags TEXT[],

  -- Automated (push mode)
  substack_rss TEXT,
  x_rss TEXT,                -- Nitter proxy: https://nitter.net/[handle]/rss
  youtube_rss TEXT,          -- https://www.youtube.com/feeds/videos.xml?channel_id=[ID]
  github_username TEXT,

  -- Manual only (pull mode)
  linkedin_handle TEXT,      -- No API. Chrome extension only.
  tiktok_handle TEXT,        -- No API. Slack/Telegram URL drop + TokScript.

  scan_frequency TEXT DEFAULT 'daily',
  last_scanned TIMESTAMPTZ,
  active BOOLEAN DEFAULT TRUE
);
```

**RSS and API by platform:**
| Platform | Method | Access |
|---|---|---|
| Substack | ✅ RSS | Native feed |
| X/Twitter | ✅ Grok API | Replaces Nitter — reliable, richer context |
| YouTube | ✅ RSS + Gemini API | RSS detects new videos, Gemini watches and summarizes |
| GitHub | ✅ RSS | Releases per repo |
| LinkedIn | ❌ | Chrome extension only |
| TikTok | ❌ | TokScript + Slack/Telegram URL drop |
| Email newsletters | ✅ Kill the Newsletter → RSS | Convert to RSS feed, no inbox access needed |

**Day 1 seed data — populated from pre-build creator frequency analysis (17 bookmarks = highest priority):**

```sql
INSERT INTO followed_creators 
  (name, why_i_follow, product_tags, substack_rss, youtube_rss, scan_frequency)
VALUES

('Nate B. Jones', 
 'AEO, Open Brain architecture, agentic workflows. Primary source for Magentics 
  strategy and the foundation this entire system is built on.',
 ARRAY['magentics', 'ai_transformation'],
 'https://natesnewsletter.substack.com/feed',
 'https://www.youtube.com/feeds/videos.xml?channel_id=[NateBJonesChannelID]',
 'daily'),

('Sabrina Ramonov',
 'Hands-on Claude Code and Lovable tutorials. Best source for practical AI 
  engineering techniques that increase solo founder output.',
 ARRAY['magentics', 'kovalency'],
 NULL,
 'https://www.youtube.com/feeds/videos.xml?channel_id=[SabrinaChannelID]',
 'daily'),

('Greg Isenberg',
 'Founder strategy — customer acquisition, vibe coding critique, SaaS business 
  models. Strong social media content angle.',
 ARRAY['ai_transformation', 'new_idea'],
 NULL,
 'https://www.youtube.com/feeds/videos.xml?channel_id=[GregIsenbergChannelID]',
 'daily'),

('Brock Mesarich',
 'Specialized tutorials on Claude Cowork and Perplexity. High leverage for 
  AI tooling skills.',
 ARRAY['magentics', 'kovalency'],
 NULL,
 'https://www.youtube.com/feeds/videos.xml?channel_id=[BrockChannelID]',
 'daily'),

('Wes Huff',
 'Christian apologetics, biblical history, worldview content. Primary source 
  for the Book Project — mental models for young adults.',
 ARRAY[],
 NULL,
 'https://www.youtube.com/feeds/videos.xml?channel_id=[WesHuffChannelID]',
 'weekly'),

('Lenny Rachitsky',
 'High-level AI state of the union and AEO/product strategy. Thought leadership 
  content. Strong LinkedIn post angle.',
 ARRAY['magentics', 'ai_transformation'],
 'https://www.lennysnewsletter.com/feed',
 'https://www.youtube.com/feeds/videos.xml?channel_id=[LennyChannelID]',
 'daily'),

('Ben AI',
 'Agent team builds and Claude Skill tutorials. Practical agentic system 
  architecture.',
 ARRAY['kovalency', 'magentics'],
 NULL,
 'https://www.youtube.com/feeds/videos.xml?channel_id=[BenAIChannelID]',
 'daily'),

('Rob Walling',
 'SaaS architecture, PMF stages, B2B SaaS design. Relevant for all four 
  businesses.',
 ARRAY['magentics', 'kovalency', 'ai_transformation', 'new_idea'],
 NULL,
 'https://www.youtube.com/feeds/videos.xml?channel_id=[RobWallingChannelID]',
 'weekly');
```

**Note:** Replace `[ChannelID]` placeholders with actual YouTube channel IDs before running. Find a channel ID by going to the channel page and using a YouTube channel ID lookup tool — it looks like `UCxxxxxxxxxxxxxxx`.



### 8.8 `lifestyle_opportunities` — Business Discovery Engine

```sql
CREATE TABLE lifestyle_opportunities (
  id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  created_at TIMESTAMPTZ DEFAULT NOW(),

  title TEXT NOT NULL,
  description TEXT,
  source_signals TEXT[],
  discovery_method TEXT,

  score_lifestyle_fit FLOAT,
  score_revenue_floor FLOAT,
  score_capital_efficiency FLOAT,
  score_ai_resistance FLOAT,
  score_time_to_revenue FLOAT,
  score_competitive_moat FLOAT,
  score_personal_energy FLOAT,   -- Founder-assessed manually
  score_total FLOAT,             -- Average. >= 6.5 proceeds to simulation.

  sim_customer_profile TEXT,
  sim_acquisition_sketch TEXT,
  sim_unit_economics TEXT,
  sim_90_day_plan TEXT,
  sim_top_failure_modes TEXT,
  sim_comparable_businesses TEXT,

  status TEXT DEFAULT 'surfaced',
  rejection_reason TEXT,
  founder_notes TEXT,
  embedding VECTOR(1536)
);
```

**Lifestyle Scoring Rubric (v1 — calibrate with 10 manual examples before automating):**

```
Each dimension 1–10:
1. LIFESTYLE FIT — Operable 30hrs/week or less by year 2?
2. REVENUE FLOOR — $100K/year achievable within 18 months solo?
3. CAPITAL EFFICIENCY — Startable under $25K?
4. AI DISRUPTION RESISTANCE — Core value physical, relational, or local?
5. TIME TO FIRST DOLLAR — Paying customer within 30 days?
6. COMPETITIVE MOAT — Local reputation, licensing, or equipment barrier?
7. PERSONAL ENERGY MATCH — Tolerable for 3–5 years? (founder-assessed)

Threshold: Average >= 6.5 proceeds to simulation. Below 6.5 archived.
```

### 8.9 `content` — Content Engine Output

```sql
CREATE TABLE content (
  id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  created_at TIMESTAMPTZ DEFAULT NOW(),

  topic TEXT NOT NULL,
  source_signal_ids UUID[],
  source_creator_posts TEXT[],

  format TEXT NOT NULL,          -- 'linkedin_article' | 'linkedin_post' | 'x_thread' |
                                 --  'tiktok_script' | 'newsletter_section'
  draft TEXT,
  draft_version INT DEFAULT 1,

  status TEXT DEFAULT 'draft',   -- 'draft' | 'revision_requested' | 'approved' |
                                 --  'scheduled' | 'published' | 'killed'
  revision_notes TEXT,
  approved_at TIMESTAMPTZ,

  platform TEXT,
  published_url TEXT,
  published_at TIMESTAMPTZ,
  impressions INT,
  engagement_rate FLOAT,
  performance_notes TEXT
);
```

### 8.10 `digests` — Digest History Log

```sql
CREATE TABLE digests (
  id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  created_at TIMESTAMPTZ DEFAULT NOW(),
  digest_type TEXT,              -- 'morning' | 'weekly' | 'alert'
  content TEXT,
  signal_count INT,
  sent_to TEXT
);
```

### 8.11 `jobs` — Processing Queue (Durable Pipeline)

**Council finding (v1.2):** "You fixed the brain's thinking. You didn't fix its nervous system." Without a queue, signals that fail during async enrichment are silently lost — no retry, no recovery, no visibility.

The `jobs` table is a lightweight queue that decouples ingestion from enrichment. Signals are stored immediately on receipt. Enrichment (LLM classification, embedding generation) runs as a separate job with retry logic.

```sql
CREATE TABLE jobs (
  id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  created_at TIMESTAMPTZ DEFAULT NOW(),
  updated_at TIMESTAMPTZ DEFAULT NOW(),

  job_type TEXT NOT NULL,       -- 'classify_signal' | 'generate_embedding' |
                                --  'generate_digest' | 'scan_creators' | 'alert'
  status TEXT DEFAULT 'pending', -- 'pending' | 'processing' | 'done' | 'failed' | 'dead'
  signal_id UUID REFERENCES signals(id),
  payload JSONB,                -- Job-specific data (signal content, options, etc.)

  retry_count INT DEFAULT 0,
  max_retries INT DEFAULT 3,
  last_error TEXT,              -- Error message from last failure
  next_retry_at TIMESTAMPTZ,
  completed_at TIMESTAMPTZ
);

CREATE INDEX jobs_status_idx ON jobs(status) WHERE status IN ('pending', 'failed');
CREATE INDEX jobs_next_retry_idx ON jobs(next_retry_at) WHERE status = 'failed';
```

**Processing flow — correct implementation (v1.3):**

The council identified two errors in v1.2's worker design: pg_cron cannot run every 10 seconds (minimum is 60 seconds), and Edge Functions cannot run as persistent polling loops. The correct architecture uses `waitUntil()` as the primary path and pg_cron as a 1-minute retry sweep:

```
Slack webhook received
    ↓
1. Return 200 immediately (< 100ms)
2. Store raw signal in signals table (no LLM — always succeeds)
3. Create job record: { status: 'pending', signal_id: X }
    ↓
4. Process the job INLINE via EdgeRuntime.waitUntil():
   → Stage 1 rules engine (synchronous, no API calls)
   → Stage 2 LLM enrichment via OpenRouter
   → Embedding generation
   → Update signal with enrichment results
   → Job status = 'done'
   
   On failure:
   → Job status = 'failed', error logged, retry_count++
   → Signal remains with urgency = 'quarantine'
   ↓
5. pg_cron runs ONCE PER MINUTE (achievable with standard cron):
   SELECT id FROM jobs
   WHERE status = 'failed' AND retry_count < 3
   AND next_retry_at <= NOW()
   FOR UPDATE SKIP LOCKED  ← prevents race conditions
   LIMIT 5;
   
   → Reprocess failed jobs
   → After 3 failures: status = 'dead'
   → Dead jobs surface in next morning digest stats footer
```

**SELECT FOR UPDATE SKIP LOCKED** is required — without it, simultaneous pg_cron invocations can pick up the same job and double-process it (double OpenRouter spend, duplicate records). This is the standard Postgres job queue primitive and must be in the implementation.

**pg_cron configuration (once per minute):**
```sql
SELECT cron.schedule(
  'retry-failed-jobs',
  '* * * * *',  -- Every minute — achievable with standard cron syntax
  $$
    SELECT process_failed_jobs();  -- Supabase Function or Edge Function
  $$
);
```

### 8.12 Importance Scoring

**Council finding (v1.2):** "There is no scoring model for importance. 3 mediocre signals can crowd out 1 critical one. The digest is unprotected from noise."

Add `importance_score` to the signals table — computed separately from the LLM classification, based on objective factors the LLM doesn't control:

```sql
ALTER TABLE signals ADD COLUMN importance_score FLOAT DEFAULT 0.5;
```

**Phase 1 importance score — 2 variables only (v1.3):**

The 4-variable formula was correct in concept but premature. With 0–200 signals in Phase 1, cluster_density and product_relevance are near-zero and near-equal for all signals — the formula produces ~0.5 for everything and the sort is meaningless exactly when it matters most.

Phase 1 uses 2 variables that produce meaningful differentiation from day one:

```
importance_score = (urgency_weight × 0.6) + (recency_weight × 0.4)

urgency_weight:  act_now = 1.0 | this_week = 0.7 | monitor = 0.4 | quarantine = 0.2

recency_weight:  Age 0–24hrs = 1.0 | Age 1–3 days = 0.7 | Age 3–7 days = 0.4 | Age 7+ days = 0.1
```

This is computable from day one with zero historical data, produces clear differentiation immediately, and is easy to reason about when debugging. A recent `act_now` signal scores 1.0. An old `monitor` signal scores ~0.28.

**Phase 2 expansion (when 200+ signals exist):**

Add cluster_density (how many signals share theme + product_tag this week) and product_relevance (based on signal frequency per product over 30 days). The formula reverts to the 4-variable version at that point.

---

## 9. Security Requirements

**Implement before going live. Do not skip.**

### 9.1 Slack Webhook Signature Verification (CRITICAL)

Without this, anyone who finds the webhook URL can POST to your brain and drain OpenRouter credits.

```typescript
async function verifySlackSignature(req: Request, body: string): Promise<boolean> {
  const slackSignature = req.headers.get('x-slack-signature');
  const timestamp = req.headers.get('x-slack-request-timestamp');
  const signingSecret = Deno.env.get('SLACK_SIGNING_SECRET');

  if (!slackSignature || !timestamp || !signingSecret) return false;
  if (Math.abs(Date.now() / 1000 - Number(timestamp)) > 300) return false;

  const baseString = `v0:${timestamp}:${body}`;
  const key = await crypto.subtle.importKey(
    'raw', new TextEncoder().encode(signingSecret),
    { name: 'HMAC', hash: 'SHA-256' }, false, ['sign']
  );
  const signature = await crypto.subtle.sign('HMAC', key, new TextEncoder().encode(baseString));
  const expectedSig = 'v0=' + Array.from(new Uint8Array(signature))
    .map(b => b.toString(16).padStart(2, '0')).join('');

  return slackSignature === expectedSig;
}
```

### 9.2 MCP Authentication (CRITICAL)

- Auth token in headers only (`x-brain-key`), never URL query params
- Separate token per client — one compromised token = rotate only that client
- Rate limit MCP endpoint: 100 req/hour per token

### 9.3 Hono Route Pattern

```typescript
app.all("*", async (c) => { ... })  // CORRECT for Supabase Edge Functions
app.all("/", async (c) => { ... })  // WRONG — never matches
```

### 9.4 OpenRouter Data Retention

Raw signal content passes through OpenRouter. Use MCP direct capture (`capture_thought`) for sensitive information — it bypasses OpenRouter entirely.

---

## 10. Classification Engine

**Council finding (incorporated in v1.1):** A single prompt doing signal type, theme, urgency, product tags, routing, content worthiness, and alert behavior simultaneously is overloaded. Failures cascade. The revised approach uses two stages: fast rules-based routing first, LLM enrichment second. Low-confidence items go to a quarantine lane — not silent archive.

### 10.1 Stage 1 — Rules-Based Fast Routing

Runs synchronously before any LLM call. Handles 70–80% of inputs cheaply and instantly. Zero OpenRouter cost for these.

```typescript
function quickClassify(input: string): QuickResult | null {
  const lower = input.toLowerCase().trim();

  // TASK PATTERNS — route to tasks table, skip LLM entirely
  const taskTriggers = [
    /^(don't forget|remind me|remember to|need to|have to|must|todo)/i,
    /^(call|email|text|ping|follow up with|reach out to|contact)\s/i,
    /^(buy|order|schedule|book|fix|clean|pick up|drop off)/i,
    /\b(tonight|today|tomorrow|this week|by friday|due|deadline)\b/i,
  ];
  if (taskTriggers.some(p => p.test(lower))) {
    return { routing_table: 'tasks', signal_type: 'task', skip_llm: true };
  }

  // PERSON PATTERNS — pre-route to people_drafts, still enrich with LLM
  const personTriggers = [
    /^(met|talked to|spoke with|had coffee with|connected with)\s/i,
    /^(should reach out|haven't talked to|owe.*call|follow up with)\s/i,
  ];
  if (personTriggers.some(p => p.test(lower))) {
    return { routing_table: 'people_drafts', signal_type: 'person', skip_llm: false };
  }

  // URL TYPE DETECTION — route to the right enrichment API before LLM classify
  if (/^https?:\/\//i.test(lower)) {
    
    // YouTube → Gemini API (watches the video)
    if (/youtube\.com\/watch|youtu\.be\//i.test(lower)) {
      return { routing_table: 'signals', needs_url_fetch: false, 
               enrichment_api: 'gemini', skip_llm: false };
    }
    
    // X/Twitter → Grok API (fetches full thread + author context)
    if (/x\.com\/|twitter\.com\//i.test(lower)) {
      return { routing_table: 'signals', needs_url_fetch: false,
               enrichment_api: 'grok', skip_llm: false };
    }
    
    // Everything else → fetch URL content, pass to OpenRouter classifier
    return { routing_table: 'signals', needs_url_fetch: true, 
             enrichment_api: 'openrouter', skip_llm: false };
  }

  // Everything else → full LLM Stage 2 via OpenRouter
  return null;
}
```

**Enrichment API routing:**

| URL Type | API Called | What It Returns | Cost |
|---|---|---|---|
| YouTube | Gemini Flash | Video summary, key takeaways, build_relevant flag | ~$0.00015/call |
| X/Twitter | Grok API | Full thread, author context, quote chain | ~$0.001/call |
| Substack/blog | OpenRouter fetch | Page content for classification | ~$0.0001/call |
| Other URL | OpenRouter fetch | Page content for classification | ~$0.0001/call |

### 10.2 Stage 2 — LLM Enrichment (Async via EdgeRuntime.waitUntil)

Runs after 200 is returned to Slack. For X/Twitter signals, the enriched content from Grok (full thread + context) is passed here instead of raw URL. For YouTube, Gemini output feeds directly in. Themes list is dynamically loaded from the `themes` table on every call.

```
You are the classification engine for a founder's intelligence system.

BUSINESSES:
- magentics: AEO / GEO tool
- kovalency: Agent audit and compliance
- ai_transformation: Enterprise AI education
- new_idea: Blue ocean or lifestyle opportunity

THEMES (dynamically loaded from themes table):
{{THEMES_LIST}}

{{#if pre_classified}}
Stage 1 pre-routing: {{routing_table}} | {{signal_type}}
Confirm or override these if the full input suggests different.
{{/if}}

Input: {{INPUT}}
{{#if url_content}}Fetched content: {{url_content}}{{/if}}
{{#if grok_context}}X/Twitter context (from Grok): {{grok_context}}{{/if}}
{{#if gemini_summary}}YouTube summary (from Gemini): {{gemini_summary}}{{/if}}

Return ONLY valid JSON:
{
  "signal_type": "tool_or_oss | competitor_move | market_trend | blue_ocean_problem | learning | person | idea | task",
  "theme_slug": "[active theme slug from themes table]",
  "valence": "opportunity | threat | neutral | action_required",
  "urgency": "act_now | this_week | monitor | quarantine",
  "product_tags": ["magentics", "kovalency", "ai_transformation", "new_idea"],
  "recommended_action": "One concrete sentence. Not generic.",
  "routing_table": "signals | tasks | people_drafts | competitors | learnings",
  "confidence": 0.0 to 1.0,
  "summary": "2–3 sentence summary",
  "content_worthy": true | false,
  "content_formats": ["linkedin_article", "x_thread", "tiktok_script", "newsletter_section"],
  "alert_immediately": true | false,
  "person_name_extracted": "Name if signal_type is person, else null"
}

Rules:
- confidence < 0.7: set urgency to "quarantine" — goes to review lane, never archive
- alert_immediately = true ONLY when urgency = "act_now" AND confidence >= 0.8
- routing_table = "people_drafts" when signal_type = "person" (NEVER write directly to people)
- recommended_action must be specific — "Research this" is not acceptable
- theme_slug must match an active slug from the themes table

X/Twitter specific rules:
- For quote tweets or replies: classify the ORIGINAL idea being discussed,
  not the commentary. The recommended_action should reference the original
  source and author, not the person quoting.
- If a signal is derivative of another signal (same topic, same source, 
  captured within 48 hours): set urgency = "monitor" and note in summary
  which primary signal it relates to. Do not set act_now or this_week
  for pure commentary or restatements.
- AEO/SEO signals: always add product_tag = "magentics" and note in
  recommended_action if this is potential Magentics training data.
- Dual-purpose signals (both a skill AND a business implication): 
  classify by primary intent. Tag both themes if genuinely equal weight.
```



### 10.3 Quarantine Lane

**Council finding:** "Archiving uncertainty is quiet data loss." Low-confidence items need a review lane with founder input, not silent routing.

When `confidence < 0.7`, urgency is set to `quarantine`. These items surface in the morning digest as a brief review section — typically 1–5 items:

```
❓ NEEDS YOUR CALL (3 items)
• "Interesting thread about cabinet makers in Durham..."
  → AI guessed: new_idea / blue_ocean | Confidence: 58%
  → Reply: CONFIRM | RECLASSIFY [theme] | ARCHIVE

• "Check out this repo for vector search..."
  → AI guessed: tool_or_oss / magentics | Confidence: 61%  
  → Reply: CONFIRM | RECLASSIFY | ARCHIVE
```

Founder replies in Slack thread. The correction is logged. Over time, patterns in quarantine items reveal gaps in the classification prompt or missing themes.

```sql
-- 'quarantine' is a value in the urgency field — no separate table needed
-- urgency: 'act_now' | 'this_week' | 'monitor' | 'archive' | 'quarantine'
-- reviewed = true once founder acts
```

### 10.4 People Routing Fix

**Council finding:** "When the classifier routes to people, the raw signal has none of the structured fields the people table requires. This creates garbage records or silent failures."

The fix: signals NEVER write directly to the `people` table. Person signals write to `signals` (as always) and also create a `people_drafts` record for founder review:

```sql
CREATE TABLE people_drafts (
  id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  created_at TIMESTAMPTZ DEFAULT NOW(),
  source_signal_id UUID REFERENCES signals(id),
  person_name_extracted TEXT,  -- Best guess from LLM extraction
  raw_context TEXT,            -- Original signal text
  status TEXT DEFAULT 'pending', -- 'pending' | 'promoted' | 'merged' | 'discarded'
  promoted_to_person_id UUID REFERENCES people(id)
);
```

The morning digest surfaces pending people drafts:
```
👤 PEOPLE TO ADD (2 pending)
• "Met interesting founder at Duke event, building compliance tools"
  → Extracted name: unknown | [ADD TO CRM] [SKIP]
• "Sarah Chen mentioned she's moving to a new role"
  → Extracted name: Sarah Chen | [ADD TO CRM] [UPDATE EXISTING] [SKIP]
```

Founder taps "Add to CRM" → opens a pre-filled form with the raw context. They complete the structured fields. The draft is promoted to a proper `people` record.

### 10.5 Creator-Enriched Prompt

```
SIGNAL SOURCE: {{creator_name}} ({{platform}})
WHY WE FOLLOW: {{why_i_follow}}
[Standard Stage 2 prompt — same JSON plus:]
"full_read_recommended": true | false,
"build_relevant": true | false
```

---

## 11. Capture Layer

**Council finding (incorporated in v1.1):** The spec built four capture surfaces simultaneously. This violates our own "one workflow then modules" principle and dramatically increases Phase 1 scope. Phase 1 is now **Slack only**. Additional capture surfaces are Phase 1.5 and Phase 2 after the core loop is trusted.

### 11.1 Slack — Only Capture Surface in Phase 1

- Channel: `#founder-brain`
- Pin message: *"One message per item. URLs, thoughts, tasks, names, trends. Don't organize."*
- Webhook → `/ingest-signal` with Slack signature verification (HMAC-SHA256)
- Extract `x-slack-request-id` → `slack_event_id`, enforce unique DB constraint
- Return 200 immediately, process async via `EdgeRuntime.waitUntil()`
- Thread reply: `✓ [signal_type] → [theme] | [urgency]`
- If `alert_immediately: true` → also fires `/alert` for Telegram push

**Note on "one message per item":** One message = one signal. This is the default rule. However, the council correctly identified that forcing founders to re-send multiple messages under time pressure is behavioral fragility.

**Delimiter exception:** A single message may contain multiple signals separated by `---` or `;` on its own line. The Stage 1 rules engine splits these before creating job records — one job per segment, no LLM involved in the splitting. The thread reply acknowledges: `✓ Found 3 signals — 3 jobs queued.`

```
Example Slack message:
"Competitor X launched AEO audit feature
---
Should reach out to Marcus about NC IDEA program
---
Learn Supabase Edge Functions this week"

→ 3 separate jobs created
→ Each classified independently
→ Thread reply: ✓ 3 signals queued
```

This preserves "one signal per record" in the database while allowing "one message per capture session" in practice. The splitting is deterministic (string split on delimiter), not LLM-based, so it is reliable and cheap.

**Deduplication across capture surfaces:** All signals get a `content_hash` (SHA-256 of normalized raw_content). If the same URL or text arrives via multiple surfaces, the unique constraint prevents duplicate storage.

**Semantic deduplication (Phase 2):** Content_hash catches exact duplicates but not semantic ones — same URL with different commentary, same idea phrased differently, same signal captured twice days apart. These create digest noise. Phase 1 accepts this limitation. The weekly review prompt is instructed to surface obvious clusters and the founder can manually archive redundant signals. Full semantic deduplication (embedding-distance comparison on insert) is a Phase 2 addition — it requires a vector similarity query on every new signal insert, which adds latency and cost that isn't justified until the signal volume makes it necessary.

```sql
ALTER TABLE signals ADD COLUMN content_hash TEXT;
CREATE UNIQUE INDEX IF NOT EXISTS signals_content_hash_uidx
  ON public.signals (content_hash)
  WHERE content_hash IS NOT NULL;
```

### 11.2 Telegram — Alert Delivery Only (Phase 1)

Telegram is used in Phase 1 **only** as the alert delivery channel for `act_now` signals. It is not a capture interface in Phase 1.

- BotFather → token → Supabase secret
- `/alert` Edge Function posts to Telegram when urgency = `act_now`
- Full Telegram capture (send to brain from Telegram) is Phase 1.5

### 11.3 Chrome Extension — Phase 1.5

**Council finding:** "Building a Manifest V3 Chrome extension — even adapting a community version — involves MV3 service worker constraints, Chrome Web Store review (1–7 days, can be rejected), cross-origin request handling, secure credential storage, and ongoing maintenance. This is a full engineering project disguised as a checklist item."

Chrome extension is deferred to Phase 1.5 — after 30 days of Slack-only operation proves the core loop. Starting point remains Karin Byom's community build. The interim workaround for browser capture: select text → copy → paste into Slack. One extra step but no engineering risk.

### 11.4 MCP Direct Capture — Phase 1.5

`capture_thought` tool on MCP server. Bypasses OpenRouter — use for sensitive content. Deferred until after review UI is live and data quality is validated.

### 11.5 Creator RSS Scanning — Phase 2

**This is the feature that ends the need to manually find new content from creators you follow.** The `/scan-creators` Edge Function runs daily via pg_cron. For each active creator in `followed_creators`, it fetches their RSS feed, checks for entries newer than `last_scanned`, and for each new item creates a signal and a job for enrichment.

**The Gemini API is required for this to deliver real value.** Without it, the scanner can detect new videos but only surfaces the title — which you could find yourself. The Gemini summary is what makes the automation worth building. Title-only scanning is not worth the complexity.

**YouTube video workflow (the primary use case):**

```
1. pg_cron fires /scan-creators daily at 6am
2. Fetch RSS for each creator in followed_creators
3. For each new entry since last_scanned:
   a. If YouTube URL → call Gemini API (google/gemini-flash-1.5)
      Prompt: "Watch this video and return JSON:
               { summary: '2-3 sentences', 
                 key_takeaways: ['...', '...', '...'],
                 relevant_to_founder: 'one sentence on why a founder building 
                   AI tools in [products] would care',
                 full_read_recommended: true|false,
                 build_relevant: true|false }"
   b. If Substack/blog URL → fetch content, pass to standard LLM classifier
   c. Store enriched signal with creator_id, theme from why_i_follow context
4. Update followed_creators.last_scanned
```

**What appears in your morning digest:**

```
📡 CREATOR UPDATES (3 new)

• Nate B. Jones: "You Built an AI Memory System — Now What?"
  Six extensions for Open Brain — CRM, meal planning, job hunt pipeline. 
  Community contribution system with automated PR review agent.
  → Relevant: magentics, ai_transformation | Full read: YES ⭐

• Greg Isenberg: "SaaS is Minting Millionaires Again"  
  Vertical AI SaaS with high retention outperforming horizontal tools.
  Three niches worth targeting: compliance, local services, creative tools.
  → Relevant: new_idea | Full read: YES

• Wes Huff: "The Priesthood of Melchizedek Explained"
  Biblical typology connecting Melchizedek to priestly identity. Strong 
  illustration for the identity chapter of the book.
  → Relevant: book | Full read: maybe
```

You never searched for any of this. It assembled itself.

**Gemini API setup (Google AI Studio):**
- Account: console.cloud.google.com or aistudio.google.com
- Model: `gemini-1.5-flash` (cheapest, fast, supports YouTube URLs natively)
- Cost: ~$0.00015 per video summary — essentially free at this volume
- API key stored as Supabase secret: `GEMINI_API_KEY`
- Call pattern: pass YouTube URL directly, Gemini fetches and watches the video

**Manual YouTube capture (Phase 1 interim):**

Until `/scan-creators` is built, drop YouTube URLs into Slack manually. The thread reply will note: `💡 YouTube — paste a Gemini summary for richer classification.` Use Gemini in the browser for videos that genuinely matter, paste the summary alongside the URL. 90-second workflow, no API required.

**X/Twitter creator scanning (via Grok API — replaces Nitter):**

Nitter is fragile and increasingly unreliable. The Grok API replaces it entirely for X creator scanning. For each creator with an X handle in `followed_creators`, the scanner calls Grok API to fetch their recent posts, filtering for anything newer than `last_scanned`:

```
Grok API call:
"Fetch the last 5 posts from @[handle] on X. For each post, return:
 { text, url, posted_at, is_reply, is_quote_tweet, original_author_if_quote }"
```

Posts that are replies or quote tweets are handled per the classification rule: classify the original idea, not the commentary. If the post is pure commentary on someone else's content, `urgency = 'monitor'` and the summary references the original source.



### 11.6 Business Discovery Scanning — Phase 3

`/scan-discovery` Edge Function runs weekly (Sunday). Sources: Reddit, Craigslist, Google Trends, BLS, Yelp gaps, job boards. Scores against lifestyle rubric, simulates survivors, surfaces in weekly review.

### 11.7 Autonomous General Scanning — Phase 3

| Source | Tool | What it captures |
|---|---|---|
| Tech/AI RSS | Supabase cron | Blogs, newsletters, industry news |
| Reddit | Gummy Search API | Problem threads |
| GitHub Trending | GitHub API | New OSS by topic |
| Perplexity | Scheduled API calls | "What's new in [domain]?" |

### 11.8 Email Monitoring — Phase 1.5

Email is a significant signal source — newsletters, specific sender alerts, and industry updates. The approach avoids broad inbox access (privacy risk) in favor of two surgical patterns.

**Pattern A — Kill the Newsletter → RSS (newsletters without RSS feeds)**

Most newsletters worth following have Substack or RSS. The ones that don't can be converted:

1. Go to [kill-the-newsletter.com](https://kill-the-newsletter.com)
2. Create a feed for each newsletter — it gives you a forwarding email address and an RSS URL
3. Subscribe to the newsletter using that forwarding address
4. Add the RSS URL to `followed_creators` — the `/scan-creators` function picks it up automatically

This covers newsletters that live exclusively in email (Morning Brew, TLDR AI, specific industry digests) without touching your actual inbox. Takes 5 minutes per newsletter.

**Pattern B — Gmail Filter + Forward (specific high-value senders)**

For tracking specific senders — a competitor's announcement list, an investor's updates, a creator who doesn't have RSS:

1. In Gmail: Settings → Filters → Create filter by sender email
2. Action: Forward to `brain-ingest@[your-domain].com` (a dedicated address)
3. Set up that address with Postmark or similar to POST the email body to `/ingest-signal`
4. The Edge Function receives it as a signal with `source: 'email'`

This is surgical — you pick exactly which senders flow into the brain. No broad inbox scanning, no sensitive email exposure.

**What does NOT belong in email monitoring:**
- Your full inbox — too broad, too sensitive, too noisy
- Business email threads — these are conversations, not signals
- Automated receipts, notifications, calendar invites — pure noise

**Setup priority:**
1. Run Kill the Newsletter for any newsletter you currently open regularly
2. Gmail forward for 2-3 specific senders whose emails you consider high-signal
3. Everything else — ignore. The RSS + Slack capture handles the rest.





## 12. Review UI (Build Before MCP Server)

**Council finding (incorporated in v1.1):** "Build the review UI before building the MCP server. The review loop is the quality gate. The MCP server exposes unvalidated data. Until the founder has reviewed 100 signals and seen where classification fails, the MCP server is premature."

The review UI is the most important Phase 1 deliverable after the digest. It is a single-page HTML interface hosted on Supabase or Vercel, pointed at the Supabase backend. No framework needed — plain HTML, vanilla JS, Supabase JS client.

### 12.1 What the Review UI Does

Shows unreviewed signals in reverse chronological order. For each signal:
- Raw content (what you sent)
- Classification result (theme, signal type, urgency, product tags)
- Recommended action
- Confidence score (with visual indicator — green/yellow/red)
- Quarantine flag if confidence < 0.7

Actions available per signal:
- **Confirm** — mark as reviewed, classification was correct
- **Reclassify** — change theme, urgency, or product tag with dropdowns
- **Add note** — append context that improves future recall
- **Archive** — remove from active queue
- **Promote to person** — opens people draft form for person signals

### 12.2 Minimum Viable Review UI (Phase 1)

```html
<!-- Single page, hosted at https://[project].supabase.co/storage/v1/object/public/review/index.html -->
<!-- Or deploy to Vercel in 2 minutes -->

Key elements:
- Supabase JS client with anon key (read + write to signals, tasks, people_drafts)
- Filter bar: All | Quarantine | Unreviewed | By theme | By product
- Signal card: raw_content, classification badges, confidence bar, action buttons
- People drafts panel: pending person signals with "Add to CRM" form
- Stats header: signals this week, quarantine count, reviewed today
```

### 12.3 MCP Server Tools (Phase 1.5 — after review UI is live)

Deferred until after 30 days of Slack capture + review UI operation. The MCP server is the reward for a validated, clean dataset — not a Phase 1 deliverable.

```
capture_thought(content, source?)
  → Direct write, bypasses OpenRouter — use for sensitive content

search_brain(query, limit?)
  → Semantic search across all tables

list_recent(table?, theme_slug?, limit?, days?)
  → Recent entries filtered by table and/or theme

get_tasks(theme_slug?, status?, due_before?)
  → Task list filtered by theme and status

complete_task(id)
  → Marks task done, records completed_at

defer_task(id, days?)
  → Pushes task due_date forward (default 1 day). Notes "deferred" on the record.

skip_signal(id)
  → Downgrades signal urgency to 'monitor'. Removes from Today Board candidates.

get_people(product_tag?, relationship_type?, days_since_contact?)
  → Network CRM queries

get_signals(product_tag?, theme_slug?, signal_type?, urgency?, reviewed?)
  → Signal queries with theme and product filtering

get_creator_updates(creator_name?, days_back?)
  → Signals from tracked creators

get_content_opportunities(min_signal_count?, format?)
  → Topic clusters worth writing about

get_lifestyle_opportunities(min_score?, status?)
  → Business discovery results

manage_themes(action, slug?, name?, description?, goal?, capture_examples?, digest_priority?)
  → Add, update, or deactivate themes without touching code
  → action: 'add' | 'update' | 'deactivate' | 'list'

retry_dead_jobs()
  → Requeue all dead jobs back to 'failed' status for one more retry pass
  → Use when dead jobs appear in digest and you want to attempt recovery
  → Returns: count of jobs requeued

get_stats(theme_slug?)
  → Signal and task counts by theme, urgency, product for current week
  → Includes: rules vs LLM split, quarantine count, dead job count, worker last heartbeat
```

**Claude Desktop config:**

```json
{
  "mcpServers": {
    "FounderBrain": {
      "command": "npx",
      "args": [
        "mcp-remote",
        "https://<PROJECT>.supabase.co/functions/v1/founder-brain-mcp",
        "--header",
        "x-brain-key: ${AUTH_TOKEN}"
      ],
      "env": { "AUTH_TOKEN": "<your-token>" }
    }
  }
}
```

---



## 13. Digests & Alerts

### 13.1 /generate-digest Edge Function

Runs on two schedules:
- **Daily at 7am** — morning briefing
- **Sunday at 6pm** — weekly review + business discovery report

### 13.2 /alert Edge Function

Fires immediately when `/ingest-signal` returns `alert_immediately: true` in classification output. Posts a Telegram message with:
- Signal summary
- Recommended action
- Link to full signal in brain

### 13.3 Morning Briefing Format (7am daily)

Signals within each section are sorted by `importance_score DESC` — not just by urgency. This protects the digest from LLM inconsistency: a highly clustered signal that's been building for 3 days outranks a single one-off signal even if both are tagged `this_week`.

Quarantine items are capped at **3 per digest**. If more exist, the digest notes "and N more in review UI." This prevents the quarantine section from becoming a daily chore that causes abandonment.

```
Good morning Dirk. [Day], [Date].
{{#if degraded_mode}}
⚠️ SYSTEM NOTE: LLM enrichment is paused (API budget reached). 
Classification is rules-only today. Digest may be less precise.
New signals are stored safely and will be enriched when budget resets.
{{/if}}
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

🎯 TODAY'S FOCUS

🔴 MUST DO (max 3)
• [task/signal/person] — [reason it matters now]
• [task/signal/person] — [reason it matters now]

🟡 SHOULD DO (max 5)
• [item]
• [item]
• [item]

⚪ OPTIONAL
• [item]

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

🔴 SIGNALS NEEDING ATTENTION
[act_now and this_week signals sorted by importance_score]
• Kovalency: [summary] → [action]
• Magentics: [summary] → [action]

💼 BUSINESS INTELLIGENCE
[this_week signals grouped by product]

🤝 RELATIONSHIPS
• [name] — [X] days since contact. [last topic].

🎓 SKILLS BACKLOG
• [skill] (flagged [N] days ago) — [business relevance]

✅ PERSONAL TASKS ([N] open)
• [task] — [due date]

❓ NEEDS YOUR CALL (max 3 shown)
• "[raw content snippet]" → guessed: [theme] | confidence: [X]%
  Reply: CONFIRM | RECLASSIFY | ARCHIVE

📡 CREATOR UPDATES (Phase 2+)
• [creator]: "[title]" | full read: yes/no

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
📊 [N] signals | [X] via rules | [Y] via LLM | [Z] quarantined | [W] dead jobs
```

The stats footer line gives you a daily health check on the pipeline — if dead jobs accumulate, something is broken.



### 13.4 Weekly Review Prompt (Sunday 6pm)

```
You are synthesizing a founder's week across all themes.

DATA:
- Signals (7 days): {{signals_json}}
- Tasks (open + completed this week): {{tasks_json}}
- Ideas pipeline: {{ideas_json}}
- Network overdue: {{people_json}}
- Creator updates: {{creator_signals_json}}
- Lifestyle opportunities: {{opportunities_json}}
- All signals from past 30 days (for pattern detection): {{signals_30d_json}}

Generate a weekly review with:

1. WEEK IN NUMBERS
   Signals by theme. Tasks opened vs completed. 
   Content published. Opportunities scored.

2. BUSINESS A/B TEST SCORE
   Rank the 4 businesses by signal momentum this week.
   Be honest if one is weakening. Cite specific signals.

3. COMPETITOR ALERTS
   Any moves that need a response?

4. SKILLS BACKLOG REVIEW
   Items > 30 days old. Should they be scheduled, delegated, or dropped?

5. RELATIONSHIP HEALTH
   Who is drifting? Who deserves recognition for a win?

6. PATTERNS
   What themes emerged this week that didn't exist last week?
   What are you repeatedly capturing that suggests a concern or interest?

7. LLM COUNCIL CANDIDATES
   Ideas with 3+ signals in 30 days — name them.

8. NEW THEME SUGGESTION
   Scan signals with low theme_match confidence from the past 30 days.
   If 3+ cluster around a topic not covered by existing themes,
   suggest a new theme: name, description, goal.

Then append the Business Discovery Report (lifestyle opportunities).
```

### 13.5 Execution Layer — Today Board

**Purpose:** Convert accumulated signals, tasks, and relationship nudges into a daily, prioritized action plan. This is the bridge between intelligence (what the brain knows) and execution (what gets done today).

**Core principle:** The system does not manage projects or long-term workflows. It answers one question: *"What should I do today?"*

The Today Board is:
- **Generated** (not maintained — rebuilt fresh each morning)
- **Constrained** (not exhaustive — hard caps enforce focus)
- **Ephemeral** (not stored as a system of record — derived view only)

**Generation timing:** Generated alongside the morning digest at 7am. Included as the **first section** of the digest, before all intelligence sections. Not stored in a separate table.

**Output format:**

```
🎯 TODAY'S FOCUS

🔴 MUST DO (max 3)
• [item] — [reason it matters now]
• [item] — [reason it matters now]
• [item] — [reason it matters now]

🟡 SHOULD DO (max 5)
• [item]
• [item]
• [item]

⚪ OPTIONAL
• [item]
• [item]
```

**Selection logic — Phase 1 (deterministic, no LLM):**

MUST DO (max 3) — selected from:
- `tasks` where `due_date <= today` AND `status = 'open'`
- `signals` where `urgency = 'act_now'`
- `people` where `follow_up_date = today`

Sorted by `importance_score DESC`, then recency. Hard cap: 3 items. If more candidates exist, only the highest-scoring 3 are shown. The rest surface tomorrow.

SHOULD DO (max 5) — selected from:
- `signals` where `urgency = 'this_week'`
- `people` where `last_contact_date < (today - 30 days)` AND `relationship_strength IN ('strong', 'warm')`
- `content` where `content_worthy = true` AND `status = 'draft'`

Sorted by `importance_score DESC`. Hard cap: 5 items.

OPTIONAL — selected from:
- `tasks` where `theme_slug = 'skills'` AND `status = 'open'`
- Creator signals and saved articles (signals where `source IN ('rss_creator', 'slack')` AND `urgency = 'monitor'`)
- `signals` where `urgency = 'monitor'`

No hard cap on OPTIONAL — show up to 5, collapsed by default.

**Critical constraints — these are non-negotiable:**
- MUST DO is capped at 3. Never 4. Never "3 plus one exception."
- SHOULD DO is capped at 5. Never more.
- The system enforces these limits in the digest generation query, not in the prompt.
- If the board feels too empty on a quiet day, that is correct — a quiet day is a good day.

**Interaction model — Phase 2 (via Slack reply or MCP):**

```
User replies to digest thread:
  "done [item]"   → tasks.status = 'done', completed_at = now()
  "defer [item]"  → tasks.due_date = tomorrow, note "deferred"  
  "skip [item]"   → signal urgency downgraded to 'monitor'
```

MCP tools:
```
complete_task(id)         → marks done
defer_task(id, days?)     → pushes due_date forward (default 1 day)
skip_signal(id)           → downgrades urgency to monitor
```

**Non-goals — what the Today Board is not:**
- Not a Kanban board
- Not a persistent task manager
- Not a project planning tool
- Not a replacement for the `tasks` table
- No drag-and-drop UI
- No columns, no backlog grooming, no sprints

**Design alignment:**

| Existing principle | How Today Board supports it |
|---|---|
| Classify, don't organize | Board is generated from classified data, not manually curated |
| Agent surfaces, founder decides | Board proposes; founder marks done/defer/skip |
| One workflow, then modules | Board is a view on existing tables, no new schema needed |
| Build for restart | Missing a day means tomorrow's board regenerates fresh — no backlog guilt |

**Role in the system:**

The digest provides context — what's happening across all four businesses, all themes, all signals. The Today Board drives action — what to do about it in the next 16 hours. These are two different questions and two different sections of the same morning message.

A founder who reads the digest and ignores the Today Board has intelligence but no execution. A founder who reads only the Today Board and skips the digest has action but no context. Both sections together are what make the morning routine genuinely useful.

---

## 14. Content Engine

### 14.1 Founder Voice Profile

*(Draft — Dirk must review and refine before Phase 2 content builds begin)*

```
TONE: Founder-to-founder. Pragmatic, not hype. Concrete over abstract.
      Direct. No throat-clearing. Lead with the insight, not the context.

AUDIENCE: Founders, operators, AI-curious business people.
          Busy and skeptical. Earn their attention in the first line.

DOES NOT DO:
- Hype AI without grounding it in business outcomes
- Generic listicles ("top 5 tips")
- Overly polished corporate tone
- Lengthy preambles before the point

DOES DO:
- Shares what he's actually building and learning in real time
- Names the uncomfortable truth others are avoiding
- Uses his own businesses as real, named examples
- Ends with something actionable or a sharp question

BUSINESS CONTEXT FOR CONTENT:
- Building 4 parallel businesses as A/B tests in the AI era
- Believes most SaaS will be commoditized; lifestyle businesses underrated
- Building personal AI infrastructure (Founder OS) and writing openly about it
- Deeply technical but communicates for non-technical founders
```

### 14.2 Content Draft Formats

| Format | Length | Key constraint |
|---|---|---|
| LinkedIn article | 800–1200 words | Strong POV in first line |
| LinkedIn post | 150–300 words | Hook → 3–5 insight lines → CTA |
| X thread | 8–12 tweets | Each tweet standalone-readable |
| TikTok script | 45–90 seconds | Written for speaking: Hook (0–3s) → Problem → Insight → Payoff |
| Newsletter section | 300–500 words | Connects to prior issues, ends with question |

### 14.3 Review → Approval → Schedule

```
Draft → Slack #content-drafts
    ↓
"approve" / "revise: [notes]" / "kill"
    ↓
Approved → Slack #content-ready → copy to Typefully/Buffer
Revise → redraft, version increments
Kill → stored for pattern learning
```

The brain never posts directly. Scheduling is always human-operated.

---

## 15. Claude Projects Integration

### 15.1 The Relationship Between Projects and the Brain

Claude Projects and the Founder OS brain are not competing systems — they are complementary layers with different jobs.

```
CLAUDE PROJECTS                    OPEN BRAIN (Supabase)
───────────────                    ─────────────────────
Focused workspace for              Persistent memory layer
specific work                      across ALL projects

Founder OS Project  ─────┐
Kovalency Project   ─────┤───► MCP CONNECTION ───► Supabase
Magentics Project   ─────┤         (shared)          brain
AI Transform Project─────┘

Each project has its own         All projects share the
system prompt, knowledge          same brain via MCP.
files, conversation history.      The brain holds the
                                  cross-project intelligence.
```

The MCP connection is configured at the Claude Desktop level, not the project level. This means the Founder OS brain is available in **every project** — not just the Founder OS project. Any session in any project can read from and write to the same Supabase database.

**No Notion. No Obsidian.** Google Drive (Docs, Slides, Sheets) is the document working environment. The brain is the intelligence layer. They coexist without conflict.

### 15.2 Three Patterns for Bridging Projects and Brain

**Pattern 1 — Suggest-and-confirm Skill in every project**

The Claude Skill should be installed in the system prompt of every Claude Project. It surfaces high-signal moments for capture but asks before saving — preserving the judgment line (Design Principle 4: the agent suggests, the founder decides).

Add this snippet to every project's system prompt:

```
You have access to the Founder OS brain via MCP (FounderBrain server).
When you encounter an important decision, insight, or piece of context 
in our conversation, flag it: "This seems worth saving to your brain: 
[one-sentence summary]. Should I capture it?"

Wait for confirmation before calling capture_thought.
Tag confirmed captures with the appropriate product 
(magentics | kovalency | ai_transformation | new_idea) and theme.
Do NOT save anything without explicit approval.
```

**Pattern 2 — Session-end capture (manual fallback)**

At the end of any significant work session, if the auto-save Skill missed something important, ask:

```
"What from this conversation is worth saving to my Founder OS brain? 
 Summarize key decisions, insights, and open questions as 
 capture-ready entries tagged to [product name]."
```

Paste the output into Slack `#founder-brain`. This is the fallback when the auto-save Skill is not yet installed in a project.

**Pattern 3 — Project knowledge as brain seeds**

Existing Claude Project knowledge files (uploaded documents, system prompts, research) can be migrated into the brain as a one-time batch. This is covered in the Day 0 setup sequence (Step 7 below).

### 15.3 Project System Prompt Template

Add this block to the system prompt of every Claude Project:

```markdown
## Founder OS Brain Connection

You have access to the Founder OS brain via the FounderBrain MCP server.
Use it actively:

READING: Before answering complex questions about this project, check if 
relevant context exists in the brain (search_brain, get_signals, 
get_people). Surface it proactively.

WRITING: When important decisions, insights, or context emerge in our 
conversation, save them using capture_thought. Tag with:
- product_tag: [magentics | kovalency | ai_transformation | new_idea]
- theme: [business | skills | personal | relationships | content]

THE JUDGMENT LINE: Surface and suggest. Never send, post, purchase, 
or act autonomously without Dirk's explicit approval.
```

### 15.4 Current Claude Projects and Their Brain Tags

| Claude Project | product_tag | Notes |
|---|---|---|
| Founder OS | all | This spec lives here. Migrate to brain on Day 0. |
| Kovalency | `kovalency` | Product decisions, compliance research, feature work |
| Magentics | `magentics` | AEO research, product direction, competitor analysis |
| AI Transformation | `ai_transformation` | Curriculum, client work, education strategy |
| [Any new project] | Assign on creation | Add to this table as projects are created |

### 15.5 Google Drive Integration

Google Drive is the document working environment — Docs for writing, Sheets for analysis, Slides for presentations. It does not need to be replaced or migrated into Supabase.

**How Google Drive connects to the brain:**

**As a signal source (manual):** Drop any Google Doc or Sheet URL into Slack `#founder-brain`. The Edge Function fetches publicly accessible content and classifies it. Works natively — no additional setup.

**As a reference layer:** The brain stores metadata and summaries, not full documents. A signal saying "reviewed Q1 Kovalency pipeline in Drive [URL], key finding: churn risk in enterprise segment" is more useful than copying the spreadsheet into Supabase.

**Via Google Drive MCP (Phase 3 optional):** Anthropic provides a Google Drive MCP connector that lets Claude search your Drive directly during a conversation. This would allow: *"Find any Kovalency documents we've worked on and cross-reference with recent competitor signals."* Not a dependency for Phase 1 — add when the need becomes real.

**What does NOT go in Google Drive:** Captured signals, tasks, people records, ideas — these go in Supabase. The brain is queryable by agents. Google Drive is not.

```
GOOGLE DRIVE                    OPEN BRAIN (Supabase)
────────────                    ─────────────────────
Working documents               Intelligence layer
Slide decks                     Signals and insights
Spreadsheet analysis            People and relationships
Long-form writing               Tasks and reminders
                                Ideas pipeline
                                Content drafts
                                Summaries of Drive docs
```

---

## 16. Day 0 Setup Sequence

**Step 0 runs BEFORE building anything.** Steps 1–8 run after the system is live.

---

**Step 0 — Pre-Build Validation Exercise (before writing a line of code)**

The council's most important question: *"What happened to the last important signal you saved?"*

The founder currently captures bookmarks into a flat bucket with no review structure — the exact problem the brain solves. Before building, manually process 20–30 existing bookmarks to validate the classification framework and calibrate the prompt with real data. This is the cheapest possible test of whether the routing logic is right.

Run this in Claude:

```
Here are my last 30 bookmarks: [paste them]

For each one, apply this classification framework:
- Which of my four businesses does it relate to?
  (magentics / kovalency / ai_transformation / new_idea / none)
- Which theme? (business / skills / personal / relationships / content)
- Urgency? (act_now / this_week / monitor / archive)
- Recommended action in one sentence?
- Would I have been glad to see this in a morning digest?

Then tell me:
1. What % were unclear or would have been misrouted?
2. Are there signal types that don't fit existing categories?
3. How many are still actionable vs. stale?
4. What adjustments should be made to the classification rules?
```

The survivors become your first 20–30 signals on Day 1 — you start with a populated system, not an empty one. Populated systems get used. Empty systems get abandoned.

---

**Step 1 — Memory Migration** (once per AI platform)
Extract everything Claude and ChatGPT already know about you. Ask each:
*"Extract everything you know about me — my work, businesses, goals, relationships, decisions — and format as one-sentence capture entries I can paste into Slack."*

**Step 2 — Open Brain Spark** (once)
*"Interview me to generate my First 30 Captures list — the most important things to put in the system today, organized by theme."*

**Step 3 — Quick Capture Templates** (use for first 2 weeks)
```
DECISION: I decided [X] because [Y]. Alternative was [Z].
PERSON: [Name] at [Company]. Met via [context]. Relevant to [business].
INSIGHT: I learned [X]. Changes my thinking about [Y].
SIGNAL: [Source] says [X]. [Opportunity/Threat] for [business].
TASK: [Action item]. Due [when]. Theme: [personal/skills/relationships].
```

**Step 4 — LinkedIn Backlog Migration** (one-time)
- Request LinkedIn data export (Settings → Data Privacy → Get a copy of your data)
- For last 90 days of saves: TokScript/Chrome ext → content → paste to Claude → capture to brain
- For older saves: delete and start fresh — stale
- Going forward: LinkedIn save = Slack forward, same moment

**Step 5 — Populate Starting Themes** (run the seed INSERT in Section 7.2)

**Step 6 — CLAUDE.md System Context File**

```markdown
# Founder OS — Claude Persistent Instructions

## System purpose
[Brief description]

## My four businesses
[One paragraph each]

## The judgment line
I surface and suggest. Dirk decides. Never send, post, purchase, or act
without explicit approval.

## Active themes
[List with one-line description of each]

## Key commands
/capture [text] — save to brain
/find [query] — semantic search
/tasks — show open tasks by theme
/digest — generate current snapshot
/themes — list active themes

## Current focus this week
[Update weekly]

## Voice profile
[Reference Section 13.1]
```

**Step 7 — Claude Projects Knowledge Migration** (one-time, per project)

For each active Claude Project, migrate its key knowledge into the brain so it persists across model updates and project resets.

For each project, run this prompt inside that project:

```
I'm migrating the key knowledge from this Claude Project into my 
Founder OS brain so it persists permanently in Supabase.

Please generate a list of capture-ready entries covering:
- Key decisions made in this project and their reasoning
- Current status of work in progress
- Important context that any future session should know
- Open questions and unresolved issues
- Key people mentioned and their relevance
- Insights or learnings that emerged

Format each entry as one sentence starting with a keyword 
(DECISION | STATUS | CONTEXT | QUESTION | PERSON | INSIGHT).
Tag each with product: [magentics | kovalency | ai_transformation | new_idea]
and theme: [business | skills | relationships | content | personal].
```

Paste the output into Slack `#founder-brain` in batches. The classification engine routes each entry to the appropriate table.

**Priority order for migration:**
1. This Founder OS project (highest priority — the spec and all architectural decisions)
2. Kovalency project
3. Magentics project
4. AI Transformation project
5. Any other active projects

**After migration:** Add the Project System Prompt Template from Section 14.3 to each project so future sessions auto-save to the brain.

**Step 8 — Install Auto-Save Skill in All Projects**

After completing project migrations, update the system prompt of every Claude Project to include the brain connection block from Section 14.3. This ensures ongoing sessions in any project continue to feed the brain without manual capture steps.

---

## 17. Third-Party Tools & Services

| Tool | Role | Cost | Notes |
|---|---|---|---|
| **Supabase** | Database, Edge Functions, pgvector | Free tier (~$0.10/mo) | Core infrastructure |
| **Slack** | Primary capture + digest delivery | Free tier | #founder-brain, #content-drafts, #content-ready |
| **Telegram** | Mobile capture + real-time alerts | Free | BotFather. Alert channel for act_now items. |
| **OpenRouter** | LLM API for classification + embeddings | ~cents/day | `gpt-4o-mini` + `text-embedding-3-small`. Phase 1 core. Not for sensitive content. |
| **Gemini API** (Phase 2) | YouTube video analysis for creator scanning | ~$0.00015/video | `gemini-1.5-flash` via Google AI Studio. Required for `/scan-creators` to deliver summaries. Native YouTube URL support. Store as `GEMINI_API_KEY` in Supabase secrets. |
| **Grok API** (Phase 1.5) | X/Twitter URL enrichment + X creator scanning | ~$0.001/call | Replaces Nitter. Fetches full thread + author context for X URLs. Used in Stage 1 URL routing and `/scan-creators` for X posts. Verify X data access included in your plan. Store as `GROK_API_KEY`. |
| **Kill the Newsletter** (Phase 1.5) | Email newsletters → RSS conversion | Free | kill-the-newsletter.com. 5 min/newsletter. No inbox access needed. Feeds directly into `/scan-creators`. |
| **Postmark** (Phase 1.5) | Email forwarding webhook for specific senders | Free tier | Receives Gmail-forwarded emails from specific senders, POSTs to `/ingest-signal`. Pair with Gmail filters. |
| **Chrome** | Browser extension | Free | Adapt Karin Byom's build — Phase 1.5 |
| **mcp-remote** | MCP bridge for Claude Desktop | Free (npm) | Required — Claude Desktop needs this |
| ~~Nitter~~ | ~~X/Twitter RSS proxy~~ | — | **Replaced by Grok API.** Removed. |
| **TokScript** | TikTok/Reels/Shorts transcript extraction | Free tier | Chrome extension for real-time; bulk import for backlog |
| **Snowball** | TikTok analytics overlay | Free Chrome ext | Discover which creators belong in followed_creators |
| **Gummy Search** (Phase 3) | Reddit scanning API | Paid | Blue ocean and signal scanning |
| **Typefully** | X + LinkedIn scheduling | Paid | Human-operated. Brain drafts, Typefully distributes. |
| **Buffer / Later** (optional) | Broader social scheduling | Paid | Alternative to Typefully |
| **Conway** (Phase 3) | Always-on agent runtime (Anthropic) | TBD | In internal testing April 2026. Verify MCP compat first. |
| **OpenClaw / Kilo Claw** (Phase 3 fallback) | Always-on agent runtime | TBD | Fallback if Conway delays |

---

## 18. Build Strategy — Start with OB1, Not a Blank Supabase

**Do not build the Founder OS from scratch. Build on top of OB1.**

OB1 (github.com/NateBJones-Projects/OB1) is Nate B. Jones's open-source reference implementation of Open Brain. It contains working, debugged code for the core infrastructure — Supabase setup, MCP server, Slack webhook, Edge Function scaffolding, and six pre-built extensions. The Founder OS spec is the extension layer on top of OB1, not a replacement for it.

### 18.1 OB1 Repo Structure

| Folder | Contents | Founder OS Relevance |
|---|---|---|
| `/docs` | Setup guide, AI-assisted setup, companion prompts, FAQ | **Start here** — use AI-assisted setup guide |
| `/extensions/professional-crm` | Working CRM: contacts, interactions, relationship context | **HIGH** — adapt directly as `people` table |
| `/extensions/job-hunt` | Application tracking pipeline | **MEDIUM** — adapt as prospect pipeline |
| `/recipes/daily-digest-generator` | Automated Slack/email digest from thoughts table | **HIGH** — starting point for `/generate-digest` |
| `/recipes/chatgpt-conversation-import` | Ingest ChatGPT export into thoughts | Useful for Day 0 memory migration |
| `/dashboards` | Vercel/Netlify frontend templates (knowledge dashboard, weekly review, mobile capture) | Phase 3 human-readable layer |
| `/integrations/browser-extension-connector` | Chrome extension MCP bridge | Starting point for Chrome extension build |
| `/primitives/shared-mcp` | Scoped MCP access for multiple clients | Reference for multi-token auth |
| `/primitives/rls` | Row Level Security for Postgres | Reference for future multi-user isolation |

### 18.2 The Build Sequence

```
STEP 1 — Clone OB1
git clone https://github.com/NateBJones-Projects/OB1

STEP 2 — Run AI-assisted setup
Open Claude Code in the repo root.
Feed it docs/04-ai-assisted-setup.md + this Founder OS spec.
Instruct: "Build the Open Brain base system per the AI-assisted 
setup guide, then extend it with the Founder OS specification."

STEP 3 — Validate base Open Brain is working
thoughts table live in Supabase
Slack webhook capturing → classifying → storing
MCP server connected in Claude Desktop
Morning digest posting at 7am

STEP 4 — Layer Founder OS extensions on top
Replace/extend the thoughts table with the enriched signals schema
Add: themes, tasks, people (from Extension 5), ideas, competitors,
     competitor_signals, learnings, followed_creators,
     lifestyle_opportunities, content, digests tables
Update MCP server with Founder OS tools (manage_themes, get_tasks, etc.)
Implement theme-aware classification prompt

STEP 5 — Adapt Extension 5 (Professional CRM) → people table
OB1's Professional CRM already tracks contacts, interactions,
relationship context. Adapt its schema and edge functions to match
the Founder OS people table spec, adding:
- product_tags, customer_potential, relationship_type
- follow_up_date, follow_up_trigger, relationship_strength
- embedding field for semantic search

STEP 6 — Adapt daily digest recipe → /generate-digest Edge Function
OB1's daily digest recipe is the starting point.
Extend it with Founder OS theme grouping (Section 12.3) and
weekly review prompt (Section 12.4).

STEP 7 — Build Founder OS-specific Edge Functions
/alert — real-time Telegram push for act_now items
/scan-creators — daily RSS polling (Phase 2)
/scan-discovery — weekly lifestyle business scan (Phase 3)

STEP 8 — Security hardening
Slack signature verification (Section 8, already in spec)
MCP auth via header not URL param
Rate limiting
```

### 18.3 What OB1 Provides vs. What the Spec Adds

```
OB1 PROVIDES (use as-is or minimally adapt)    FOUNDER OS SPEC ADDS
─────────────────────────────────────────      ────────────────────────────
thoughts table + vector search                  themes table (extensible categories)
Slack webhook + Edge Function scaffold           tasks table (to-dos and reminders)
MCP server (search, list, capture tools)        signals table (enriched schema)
Supabase setup + pgvector                       13 custom MCP tools
Daily digest recipe                             Theme-aware classification engine
Professional CRM (Extension 5)                  /alert real-time push
Browser extension connector                     Creator tracking + RSS scanning
Companion prompts (memory migration, spark)     Business discovery engine
                                                Content engine + draft chains
                                                Claude Projects integration
                                                Day 0 setup sequence
```

### 18.4 Claude Code Build Instructions

When starting the build session with Claude Code, provide:
1. This spec (the full Founder OS spec v1.3)
2. The OB1 repo (cloned locally or referenced by URL)
3. The OB1 AI-assisted setup guide: `docs/04-ai-assisted-setup.md`

Opening prompt for Claude Code:

```
I'm building the Founder OS — a personal AI operating system for a 
founder running multiple parallel businesses. The full spec is in 
[path to spec].

Use the OB1 repo (github.com/NateBJones-Projects/OB1) as the base 
codebase. Follow their AI-assisted setup guide to get the core Open 
Brain running first, then extend it with the Founder OS spec.

Start with:
1. Core Open Brain setup (OB1 docs/04-ai-assisted-setup.md)
2. Validate the base system works (Slack → classify → store → MCP)
3. Then begin layering the Founder OS tables and features per the spec

Do not build from scratch — build on OB1.
Do not skip the security requirements in Section 8 of the spec.
Use app.all("*") not app.all("/") in Hono routes.
```

---

## 19. Build Phases

**Council finding (incorporated in v1.1):** Phase 1 as originally written was 9–10 distinct engineering deliverables. That is at minimum 3–6 months of solo evening work, not a "45-minute setup." The revised phases reflect honest scope. Phase 1 is now the minimum viable core loop. Everything else is sequenced properly.

### Phase 1 — Minimum Viable Core Loop

**Goal:** Slack capture → two-stage classification → Supabase storage → morning digest → review UI. Prove the loop works and you'll actually use it.

**Capture: Slack only. No Chrome extension. No Telegram capture. No MCP.**

Pre-build:
- [ ] Run pre-build validation exercise (Section 16, Step 0) — manually process 20–30 existing bookmarks through the classification framework by hand before writing any code
- [ ] Clone OB1 repo
- [ ] Run OB1 AI-assisted setup (docs/04-ai-assisted-setup.md) with Claude Code
- [ ] Validate base Open Brain: Slack → thoughts table → morning digest working

Schema:
- [ ] Create `themes` table and seed with 5 starting themes
- [ ] Create `tasks` table
- [ ] Create `people_drafts` table
- [ ] Create `jobs` table (processing queue with status/retry/dead-letter)
- [ ] Add `content_hash` column + unique index to signals (deduplication)
- [ ] Add `importance_score` FLOAT column to signals (default 0.5)
- [ ] Add `urgency = 'quarantine'` as valid value (quarantine lane)
- [ ] Extend signals table: add theme_slug, content_hash, content_worthy, importance_score fields
- [ ] Create `people`, `ideas`, `competitors`, `competitor_signals`, `learnings` tables (schema only — populate later)

Edge Functions:
- [ ] `/ingest-signal` — Slack signature verification + Stage 1 rules engine
- [ ] `/ingest-signal` — immediately stores raw signal, creates job record (returns 200 fast)
- [ ] `/process-jobs` — worker that polls jobs table, runs Stage 2 LLM enrichment + embedding
- [ ] `/process-jobs` — retry logic (3 retries with exponential backoff), dead-letter handling
- [ ] `/process-jobs` — importance_score computation after enrichment
- [ ] `/process-jobs` — quarantine routing for confidence < 0.7
- [ ] `/process-jobs` — people_drafts queue for person signals
- [ ] `/process-jobs` — content_hash deduplication check before insert
- [ ] `/alert` — Telegram push for act_now signals (confidence >= 0.8 only)
- [ ] `/generate-digest` — Today Board as first section (deterministic SQL query, no LLM, hard caps enforced in query)
- [ ] `/generate-digest` — morning digest with importance-sorted sections + quarantine cap (max 3) + pipeline stats footer
- [ ] Supabase pg_cron enabled: `/process-jobs` every 10 seconds, `/generate-digest` at 7am daily

Review UI:
- [ ] Single-page review interface (plain HTML + Supabase JS client)
- [ ] Unreviewed signals queue with confirm/reclassify/archive actions
- [ ] Quarantine panel for low-confidence items
- [ ] People drafts panel with "Add to CRM" form
- [ ] Deploy to Vercel or Supabase Storage

Cost controls (add before going live):
- [ ] OpenRouter monthly budget cap set (start at $10/month)
- [ ] Alert if daily spend exceeds $1
- [ ] Supabase daily automated backup enabled
- [ ] Weekly export script (pg_dump to local JSON)

Setup:
- [ ] CLAUDE.md system context file
- [ ] Run Day 0 setup sequence (Section 16)

**Done when:** Slack URL → classified thread reply → appears in 7am digest → visible in review UI → founder marks it reviewed. This loop, working reliably for 30 days, is Phase 1 complete.

### Phase 1.5 — Extend Capture + MCP Server

**Unlock after:** 30 days of Phase 1 operation, 100+ signals reviewed, classification accuracy spot-checked at >80%.

- [ ] Chrome extension (adapt Karin Byom's community build — allow 2–4 weeks including Chrome Web Store review)
- [ ] Telegram capture (`/telegram-brain` Edge Function)
- [ ] Grok API setup — `GROK_API_KEY` in Supabase secrets, verify X data access included in plan
- [ ] X/Twitter URL enrichment in Stage 1 → Grok API fetch → richer classification
- [ ] Kill the Newsletter: convert active email newsletters to RSS, add to `followed_creators`
- [ ] Gmail filter + forward for 2–3 high-value specific senders → Postmark → `/ingest-signal`
- [ ] MCP server with 13 Founder OS tools (Phase 1.5 reward for validated data)
- [ ] Connect Claude Desktop via mcp-remote
- [ ] Auto-save Skill (suggest-and-confirm) installed in all Claude Projects
- [ ] Claude Projects knowledge migration (Section 15, Step 7)

### Phase 2 — Network + Creator + Content Ideation

- [ ] Populate `people` table from existing contacts (using people_drafts as staging)
- [ ] Network section in morning digest
- [ ] Founder voice profile reviewed and finalized
- [ ] `followed_creators` already seeded (Section 8.7) — confirm YouTube channel IDs are filled in
- [ ] Set up Google AI Studio account → get `GEMINI_API_KEY` → store in Supabase secrets
- [ ] `/scan-creators` Edge Function — daily RSS polling for all active `followed_creators`
- [ ] `/scan-creators` — detect YouTube URLs → call `gemini-1.5-flash` for video summary + takeaways
- [ ] `/scan-creators` — detect Substack/blog URLs → standard OpenRouter classification
- [ ] `/scan-creators` — update `last_scanned` after each successful run
- [ ] Creator section in morning digest (Gemini summaries, full_read flag, build_relevant flag)
- [ ] `get_content_opportunities` MCP tool
- [ ] Content draft chains for LinkedIn article and X thread
- [ ] #content-drafts and #content-ready Slack channels

### Phase 3 — Discovery + Autonomous Scanning + Always-On Agent

- [ ] Lifestyle scoring rubric calibrated (10 manual examples first)
- [ ] `/scan-discovery` Edge Function (weekly)
- [ ] Business simulation prompt chain
- [ ] Business Discovery Report in weekly review
- [ ] Autonomous scanning: RSS, Reddit, GitHub, Perplexity
- [ ] Deduplication across automated sources
- [ ] Evaluate Conway MCP compatibility
- [ ] If unavailable: evaluate OpenClaw

### Phase 4 — LLM Council + Full Content Pipeline

- [ ] Ideas with 3+ signals auto-flagged for LLM Council
- [ ] Council outputs stored in `ideas.council_summary`
- [ ] TikTok script and newsletter section draft chains
- [ ] Content performance tracking
- [ ] Content → CRM feedback loop

---



## 20. Memory Taxonomy

| Type | Where It Lives | Examples |
|---|---|---|
| **Permanent Context** | CLAUDE.md + system prompt | Business theses, voice profile, judgment line, theme goals |
| **Structural Facts** | `competitors`, product metadata | Competitor landscape, market structure |
| **Active Initiatives** | `ideas`, `lifestyle_opportunities` | Current bets, opportunities under evaluation |
| **Procedural Memory** | `learnings`, `signals.notes`, `content.performance_notes` | What worked, which content formats perform |
| **Working Memory** | `signals` + `tasks` (last 7 days) | This week's signals, open tasks, drafts in review |

---

## 21. Cost Controls

**Council finding:** "Cost control is barely addressed. There is no hard budget enforcement, model fallback policy, token spend dashboard, or kill switch if OpenRouter usage spikes."

### 21.1 OpenRouter Budget Cap

Set a hard monthly spend limit in the OpenRouter dashboard before going live. Recommended starting cap: **$10/month**. At the expected volume (20–30 signals/day, daily digest, weekly review), actual cost should be under $2/month. The cap exists to catch runaway automation bugs.

```
OpenRouter dashboard → Settings → Billing → Set monthly limit: $10
Alert threshold: $1/day (email notification)
```

If the cap is hit: the Edge Function should catch OpenRouter `402` errors gracefully and route the signal to quarantine with a note: `"Classification skipped — API budget reached. Review manually."` The signal is never lost.

### 21.2 Stage 1 Cost Savings

The rules-based Stage 1 classifier (Section 10.1) handles ~70–80% of inputs without any LLM call. This alone reduces OpenRouter cost by 3–4x compared to classifying everything with the LLM.

### 21.3 Daily Spend Alert

Add a Supabase pg_cron job that runs nightly and checks the OpenRouter usage API. If daily spend exceeds $1, send a Telegram alert:

```
⚠️ COST ALERT: OpenRouter spend today = $X
Check for runaway automation or unusual signal volume.
```

### 21.4 Defined Degradation When Budget Cap Is Hit

**Council finding (v1.2):** "Cost control exists conceptually but what happens when the cap is hit is undefined — degrade to rules-only? Queue backlog? Drop signals?"

When the OpenRouter budget cap is reached mid-month, the system degrades gracefully in a defined order:

```
Level 0 (normal):      Stage 1 rules → Stage 2 LLM enrichment → embedding
Level 1 (75% of cap):  Telegram alert: "OpenRouter spend at 75% of monthly budget"
Level 2 (cap hit):     Stage 1 rules only. All LLM enrichment paused.
                       Signals stored with:
                         urgency = 'quarantine'
                         confidence = 0
                         notes = "enrichment paused — API budget reached"
                       Job status = 'pending' (not failed — will resume next month)
Level 3 (manual reset): Founder increases cap in OpenRouter dashboard
                         → Worker picks up pending jobs automatically
                         → No signals lost
```

Signals are NEVER dropped due to budget. They're always stored raw and queued for enrichment when budget resets. The quarantine lane catches them and the digest shows them for manual review in the interim.



If OpenRouter is unavailable or returns errors:
- Stage 1 rules engine still runs (no OpenRouter dependency)
- Stage 2 LLM enrichment fails gracefully → signal stored with `urgency = 'quarantine'`, `confidence = 0`
- Thread reply: `✓ Stored (enrichment pending — API unavailable)`
- Quarantine items surface in next morning digest for manual review

No signals are ever lost due to API failure.

---

## 22. Data Export & Exit Plan

**Council finding:** "There is no serious exit plan. The spec talks about ownership but does not define export formats, restore procedures, migration off Supabase Cloud, or how to reconstruct state if classification logic changes."

### 22.1 Weekly Automated Backup

Enable Supabase's built-in Point-in-Time Recovery (PITR) in your project dashboard — available on Pro tier ($25/month) for full PITR. For free tier, use Supabase's database backup feature (Settings → Database → Backups).

For an additional local backup, `pg_dump` works from your local machine using the Supabase connection string (not from inside Supabase Edge Functions):

```bash
# Run LOCALLY (not in a Supabase Edge Function — those can't write to local filesystem)
# Find your connection string: Supabase Dashboard → Settings → Database → Connection string

pg_dump "postgresql://postgres.[project-ref]:[password]@aws-0-[region].pooler.supabase.com:6543/postgres" \
  --format=custom \
  --file="founder_os_backup_$(date +%Y%m%d).dump"
```

### 22.2 Human-Readable Export

The `COPY ... TO '/tmp'` pattern does not work on Supabase Cloud (no local filesystem access). Use the Supabase REST API instead — works from any machine, no special access needed:

```bash
# Export signals as JSON via REST API (run locally)
curl "https://[project-ref].supabase.co/rest/v1/signals?select=*" \
  -H "apikey: [your-anon-key]" \
  -H "Authorization: Bearer [your-anon-key]" \
  > signals_export_$(date +%Y%m%d).json

# Export all tables similarly — one curl per table
# Or use Supabase CLI: supabase db dump --data-only > brain_data.sql
```

Store exports in Google Drive. Human-readable, importable into any future system.

### 22.3 Raw Content Is Always Preserved

The `raw_content` field on every signal stores exactly what was captured before any classification. Even if the classification logic changes completely, the original signals are intact and can be reclassified. This is the data durability guarantee.

### 22.4 Migration Off Supabase

If you ever want to move off Supabase Cloud:

```bash
# Export from Supabase Cloud (run locally)
pg_dump "postgresql://postgres.[project-ref]:[password]@aws-0-[region].pooler.supabase.com:6543/postgres" \
  --format=custom --file=brain_full.dump

# Import to any Postgres instance (Neon, Railway, local Docker, etc.)
pg_restore --dbname=$NEW_DB_URL brain_full.dump
```

The MCP server URL in Claude Desktop config is the only thing that changes. Your entire brain migrates in one command.

### 22.5 What "You Own Your Data" Actually Means

- Raw signal text: always stored, never deleted unless you explicitly archive
- Classification results: stored, overridable via review UI
- Full Postgres dump: available any time, no export fee
- No proprietary format: everything is SQL, JSON, or plain text
- No vendor lock-in beyond Postgres itself (the most portable database in existence)

---

## 23. Open Questions

| # | Question | Current Assumption | Impact if Wrong |
|---|---|---|---|
| 1 | Conway MCP compatibility? | TBD — not shipped | Phase 3 agent choice |
| 2 | OpenRouter vs. direct Anthropic API? | OpenRouter for portability | Minor — easy to swap |
| 3 | Slack as primary, Telegram alerts only? | Yes for Phase 1 | UX preference |
| 4 | Embedding model? | `text-embedding-3-small` via OpenRouter | Cost and quality |
| 5 | Supabase Cloud or self-hosted? | Cloud (free tier to start) | Data sovereignty tradeoff |
| 6 | Chrome extension: custom or adapt Karin Byom's? | Adapt — in Phase 1.5 | Build time |
| 7 | Morning digest: thread or DM? | Thread in #founder-brain | Notification preference |
| 8 | LLM Council signal threshold? | 3+ signals in 30 days | Tunable post-launch |
| 9 | Lifestyle opportunity score threshold? | 6.5 average | Calibrate manually first |
| 10 | ~~Nitter or RSS Bridge for X?~~ | **Resolved — Grok API replaces Nitter** | N/A |
| 11 | Founder voice profile accurate as drafted? | Draft only — needs founder review | Content engine quality |
| 12 | Separate MCP auth tokens per client? | Yes | Security posture |
| 13 | TikTok: scripting only or full video workflow? | Scripting only | Scope creep risk |
| 14 | Digest themes ordering: static priority or dynamic? | Static from themes table | Tunable |
| 15 | Google Drive MCP connector — Phase 3? | Optional, not a dependency | Cross-referencing Drive docs |
| 16 | Stage 1 rules coverage — what % of real signals does it catch? | ~70–80% estimated | LLM cost and latency |
| 17 | Review UI — how often will founder actually use it? | Daily in Week 1, weekly after habit forms | System data quality |
| 18 | OpenRouter $10/month cap — enough headroom? | Yes for Phase 1 volume | Cost spike risk |
| 19 | Jobs table worker — pg_cron or Edge Function? | pg_cron 1-minute retry sweep | Implementation complexity |
| 20 | Importance score weights correct? | Starting estimate, tune after Week 2 | Digest relevance quality |
| 21 | At what quarantine rate does system feel broken? | >30% = prompt problems | Adoption risk |
| 22 | If 70% accurate after 30 days, will founder continue? | Yes, if 1 useful insight/day | Core adoption question |
| 23 | Grok API plan — does it include X data access? | Needs verification before Phase 1.5 | X enrichment feasibility |
| 24 | Gmail forward + Postmark — worth the setup for 2–3 senders? | Yes for very high-signal senders | Phase 1.5 scope |
| 25 | Kill the Newsletter — which newsletters to convert first? | Newsletters opened >50% of the time | Signal quality vs noise |



---

## 24. What This Is NOT Building

- Autonomous posting to any social platform
- Video production or editing (TikTok scripts only)
- Email drafting or sending
- Any purchasing or transaction
- LinkedIn or TikTok API scraping (ToS violation)
- Multi-user / team access
- Mobile app (Telegram + Slack mobile handles this)
- Newsletter platform or distribution
- Competitor pricing monitoring via scraping
- A review workflow that works without the founder actually reviewing (the system surfaces, the human decides)

---

## 25. Success Metrics

**Phase 1 success (30-day check):**

| Metric | Target | What it proves |
|---|---|---|
| Signals captured per week | 20–30 | Capture habit is forming |
| Quarantine rate | < 20% of signals | Classification prompt is well-calibrated |
| Review UI used | 4+ days per week | Founder trusts the system |
| Morning digest opened | 5 of 7 days | Digest is delivering value |
| Zero unauthorized POSTs | 0 | Security is working |
| OpenRouter monthly spend | < $5 | Stage 1 rules doing their job |
| One signal acted on that would have been lost | 1+ | The core value proposition is real |

**Phase 2 success (90-day check):**

| Metric | Target | What it proves |
|---|---|---|
| Tasks created and completed per week | 5–10 | Personal task habit formed |
| Network follow-ups surfaced and acted on | 2+/month | CRM is earning trust |
| Creator updates surfaced automatically | 3+/week, zero manual input | RSS scanning working |
| Act_now alerts acted on | >70% | Alerts are relevant, not noise |
| Quarantine items reviewed within 24hrs | >80% | Review habit strong |

**Phase 3 success (6-month check):**

| Metric | Target | What it proves |
|---|---|---|
| Content drafts produced/week | 2–3 | Content engine active |
| Lifestyle opportunities scored/week | 3–5 | Discovery engine running |
| New theme added from pattern detection | 1+ | System is learning |
| Signal that changed a product decision | 1+ | Intelligence is compounding |
| Weakest A/B test business identified | 1 clear answer | The original promise is delivered |

---



## 26. Reference Implementations & Resources

**OB1 Repository (primary codebase — build on this):**
- **OB1 Main Repo:** https://github.com/NateBJones-Projects/OB1
- **AI-Assisted Setup Guide:** https://github.com/NateBJones-Projects/OB1/blob/main/docs/04-ai-assisted-setup.md
- **Setup Guide (manual):** https://github.com/NateBJones-Projects/OB1/blob/main/docs/01-getting-started.md
- **Companion Prompts:** https://github.com/NateBJones-Projects/OB1/blob/main/docs/02-companion-prompts.md
- **FAQ:** https://github.com/NateBJones-Projects/OB1/blob/main/docs/03-faq.md
- **Extension 5 — Professional CRM:** https://github.com/NateBJones-Projects/OB1/blob/main/extensions/professional-crm
- **Daily Digest Recipe:** https://github.com/NateBJones-Projects/OB1/blob/main/recipes
- **Browser Extension Connector:** https://github.com/NateBJones-Projects/OB1/blob/main/integrations
- **Dashboard Templates:** https://github.com/NateBJones-Projects/OB1/blob/main/dashboards
- **Shared MCP Primitive:** https://github.com/NateBJones-Projects/OB1/blob/main/primitives/shared-mcp
- **OB1 Discord (real-time help):** https://discord.gg/Cgh9WJEkeG

**Nate's Substack guides:**
- **Open Brain guide (March 2):** https://natesnewsletter.substack.com/p/every-ai-you-use-forgets-you-heres
- **Open Brain extensions (March 13):** https://natesnewsletter.substack.com/p/you-built-an-ai-memory-system-now
- **Prompt kit:** https://promptkit.natebjones.com/20260224_uq1_promptkit_1

**Community implementations:**
- **Chrome Extension base (Karin Byom):** https://github.com/konepone/open_brain_feature
- **MCP write capability (Jay Smith):** https://docs.google.com/document/d/18yd6661CvyKCF-06J5S7aezo8fnTNlc73418gxTDE8I/edit
- **Versioned MCP tools (Mark Madsen):** https://gist.github.com/mmadsen/4f1ff37f19af99ecf0bb6c1b100412df
- **Context Map Interview prompt (Aaron Lawson):** https://www.notion.so/Context-Map-Generator-317909822eb7803c9037c90e14fb810d
- **LifeOS seed prompt (Jon Barton):** See Nate Jan 9 Substack comments

**Other references:**
- **Karpathy AutoResearch (loop pattern):** https://github.com/karpathy/autoresearch
- **Conway leak (TestingCatalog):** https://www.testingcatalog.com/exclusive-anthropic-tests-its-own-always-on-conway-agent/
- **TokScript:** https://tokscript.com
- **Snowball:** https://www.snowballapp.ai

**Key technical gotchas (do not skip):**
- Slack signature verification: HMAC-SHA256 against X-Slack-Signature header
- Hono route: `app.all("*")` not `app.all("/")`
- Duplicate entry fix: Return 200 immediately + `EdgeRuntime.waitUntil()` + unique index on slack_event_id
- MCP auth: header (`x-brain-key`), never URL query param
- Claude Desktop needs `mcp-remote` — cannot use direct HTTP MCP config

---

*Version 1.7 — Today Board added. Execution layer complete. 8 themes, 8 creators, 3 enrichment APIs, hard-capped daily action plan. Ready to build.*
