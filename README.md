## Hi, I'm Arash

I'm an AI product manager who ships the product himself. I run [Modeo](https://modeo.io), an AI consulting and product studio in San Francisco, and I build voice agents, agent tooling, and the evaluation systems that keep them honest.

Most of what I know about production AI I learned from things going wrong at 2am. The repos below are mostly what I extracted afterward.

### What I'm building

**[FamilyCheck](https://family-checker.com)** is my flagship: a production voice AI agent that calls patients at medication times, classifies every outcome (confirmed / deferred / denied / concern / **unclear** / no-answer), and alerts family caregivers within seconds when a dose is missed or a health concern surfaces. Live in private beta.

The stack is Vapi + GPT 4.1 + Deepgram Flux (STT) + Cartesia Sonic 3.5 (TTS) + Twilio, on a FastAPI + React/TypeScript codebase I wrote solo (~18K LOC).

The source is private because it's a healthcare product. The engineering is not:

**→ [familycheck-engineering](https://github.com/Arash-yazdani/familycheck-engineering)**: architecture, design decisions, and the full evaluation progression. No source, all reasoning.

The short version of the eval story: when I made my first suite five times harder, scenario pass fell to 56%, and that harder number was the useful one. The current 53-scenario adversarial suite passes 52 of 53 on three consecutive runs against an 80% bar, with PII and UUID leaks held at 0 of 53. A separate judge model grades every production call on six dimensions at about 0.4¢ per call, and a pre-registered blinded study put its agreement with human labels at 96% on values and 86% on status.

**vault-rag** is a local retrieval-augmented generation (RAG) system over the 445-note knowledge base my Claude agents use as long-term memory. It stores 5,715 chunks in SQLite with sqlite-vec vector search and FTS5, embeds them with bge-m3 on local Ollama, and ranks notes by reciprocal rank fusion of chunk vectors, note-summary vectors and BM25. Claude answers only from the retrieved passages, cites every sentence, and replies "NOT IN VAULT" when the passages do not hold the answer. Agents reach it over MCP; it re-indexes and health-checks itself nightly.

I froze a 27-question holdout set and 14 ship gates before writing any retrieval code. Against the plugin search it replaced, the correct note ranks first 44.4% of the time (from 29.6%), lands in the top 10 96.3% of the time (from 85.2%), and MRR rose from 0.500 to 0.608. Per question: 10 better, 5 worse, 12 unchanged, so treat it as a measured gain on a small set, not a significant one. Answers: 81.5% correct, all 27 grounded in the retrieved text, and 5 of 5 unanswerable questions declined. Incremental cost: $0 beyond an existing Claude subscription.

**[claude-econ-dashboard](https://github.com/Arash-yazdani/claude-econ-dashboard)** is my production economic briefing agent, migrated from Gemini/Groq to Claude on Amazon Bedrock. Rules pick the economic regime; Claude only writes the paragraph; a deterministic validator checks every number against the source data before anything publishes, and fails closed to a fallback card. It publishes twice a day at [claude-econ.modeo.io](https://claude-econ.modeo.io).

The AWS side was most of the work. IAM user scoped to Bedrock inference plus the Marketplace permissions model access needs; Anthropic models sold through AWS Marketplace (a card on file, not direct debit); a new account refused every Claude model with 403 while token counting still succeeded, so I rewrote the model probe to a one-token generation call and wrote it up as an incident; a 0 tokens/min quota on Haiku 5.5, so it runs Claude Haiku 4.5 through `us.` and `global.` cross-region inference profiles on bedrock-runtime, with structured output through a single forced tool because the runtime rejected `output_config`. A 12-case regression gate ran before schedules were turned on, and healthchecks.io dead-man switches page Slack.

Measured, not claimed: in a side-by-side run of the 12 locked cases, the original stack passed 11/12 and Claude 10/12. One Claude miss was a validator bug (it graded the year in "June 18, 2026" as a data value); the other was a low tone score. In production, one morning fell back to the safe card because an unchanged daily fed-funds print counted as a "release". Both bugs are fixed with tests (452 passing). Writer and judge are the same model, so I treat judge scores as weak evidence and the validator as the gate.

### Open source

| Repo | What it is |
|---|---|
| **[crisp-eval](https://github.com/Arash-yazdani/crisp-eval)** | An opinionated LLM-as-judge harness. CRISP scenario taxonomy, turn-pass vs scenario-pass, judge-family checks, deterministic safety keys, judge-vs-human agreement statistics, failure mining. 42 tests, no dependencies. |
| **[webhook-outbox-kit](https://github.com/Arash-yazdani/webhook-outbox-kit)** | Fail-closed webhook signature verification across three vendor schemes, plus a transactional outbox so a queued alert can't be silently lost. 41 tests, no dependencies. |
| **[EXCALIBUR](https://github.com/Arash-yazdani/excalibur-ai-prd-generator)** | Agentic PRD generator: six specialist agents turn a paragraph of product context into a stakeholder-ready PRD. Local, MIT. |
| **[persepolis-os](https://github.com/Arash-yazdani/persepolis-os)** | Single-operator cockpit for orchestrating LLM agents across projects. Claude subscription + local Ollama backends. |
| **[Flip Finder](https://github.com/Arash-yazdani/Flip_Finder_Real_Estate_Agent)** | Multi-agent real estate investment analyzer. Four agents score market, property, and financials into a ranked recommendation. Built for a property development client. |
| **[claude-econ-dashboard](https://github.com/Arash-yazdani/claude-econ-dashboard)** | The economic briefing agent on Claude in Amazon Bedrock: IAM and model-access setup, cross-region inference, forced-tool structured output, validator-gated publishing, regression gate, incident write-ups. [Live](https://claude-econ.modeo.io). |
| **[Market Control Center](https://github.com/Arash-yazdani/Market-Control-Center)** | The U.S. economy in one quotable read: inflation, jobs, growth, rates, refreshed twice a day. [Live dashboard](https://economy-dashboard-2tn.pages.dev/). Built for an investment firm. |

### Two things I believe about production AI

**Anything a regex can decide should be decided by a regex.** Handing a deterministic question to a judge model is how you end up with 0.97 on "no PII leaked" and no idea which three percent leaked.

**A guardrail that isn't wired to something that fails a build is a wish.** Prompt text is not a safety property. A test assertion is.

### Background

11 years in product management, from a geospatial platform integration through enterprise AI programs to building AI products hands-on: enterprise AI programs at EVOTEK (UCLA Health, Target, AEG Presents, ActOne Group), AI/ML product delivery at STRV, enterprise HCM accounts at ADP, product ownership at Kumon, and my own 0-to-1 launches. MBA in Finance, Marketing and Analytics from Pepperdine, and an M.S. in Cell and Molecular Biology, which is why healthcare AI keeps pulling me back.

### Find me

[family-checker.com](https://family-checker.com) · [modeo.io](https://modeo.io) · [LinkedIn](https://www.linkedin.com/in/arashyazdanimba)

Open to conversations about voice agents, agent evaluation, and healthcare AI.
