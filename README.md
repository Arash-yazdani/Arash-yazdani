### 👋 Hi, I'm Arash

🤖 I'm an AI product manager who ships the product himself. I run [Modeo](https://modeo.io) 🏢, an AI consulting and product studio in San Francisco 🌉, and I build voice agents 🎙️, agent tooling 🛠️, and the evaluation systems 🧪 that keep them honest.

## 🚀 What I'm building

**[FamilyCheck](https://family-checker.com)** 📞💊 is my flagship: a production voice AI agent that calls elderly patients at medication times, classifies every outcome (✅ confirmed / ⏳ deferred / ❌ denied / 🚨 concern / ❓ unclear / 📵 no-answer), and alerts family caregivers 👨‍👩‍👧 within seconds when a dose is missed or a health concern surfaces. Live in private beta with 10 households at $29.99/mo.

🧱 The stack: Vapi + gpt-4.1 + Deepgram Flux (STT) + Cartesia Sonic 3.5 (TTS) + Twilio, on a FastAPI + React/TypeScript codebase I wrote solo (~18K LOC 📊, 90+ commits 🔁). The code is private 🔒 because it's a healthcare product, but the part I care most about is public knowledge:

**🛡️ How I keep a voice agent trustworthy.** Every release is gated by a 50-scenario golden evaluation suite 🥇 (the v8 prompt passes 100% ✔️). In production, LangSmith online judges score six quality dimensions on every call, a weekly calibration loop 🔄 checks the judges against human verdicts, and failures are mined into regression datasets so the same mistake never ships twice 🚫🔁. Traces are PII-redacted 🕵️ with NER scrubbing before upload, because patient data does not belong in an observability tool.

## 📦 Public projects

| Project | What it is |
|---|---|
| 🗡️ [EXCALIBUR](https://github.com/Arash-yazdani/excalibur-ai-prd-generator) | Agentic PRD generator: six specialist agents turn a paragraph of product context into a stakeholder-ready PRD. Local, MIT, runs on a Claude subscription. |
| 🏠 [Flip Finder](https://github.com/Arash-yazdani/Flip_Finder_Real_Estate_Agent) | Multi-agent real estate investment analyzer with a live dashboard. Four agents score market, property, and financials into a ranked recommendation. |
| 📈 [Daily Macro Briefing](https://economy-dashboard-2tn.pages.dev/) ([repo](https://github.com/Arash-yazdani/Market-Control-Center)) | The U.S. economy in one quotable read: inflation, jobs, growth, and rates, refreshed twice a day. |
| 🖥️ [PersepolisOS](https://github.com/Arash-yazdani/persepolis-os) | Experimental single-operator cockpit for orchestrating LLM agents across projects, with Claude and local Ollama backends. |

## 🎓 Background

💼 Eight-plus years in product across enterprise AI consulting (EVOTEK: AEG Presents 🎪, Target 🎯, UCLA Health 🏥, ActOne Group), product delivery at STRV, and my own 0-to-1 launches 🌱 (REC.US municipal marketplace, ROEME iOS app 📱). 🎓 MBA in Finance, Marketing, and Analytics from Pepperdine, and an M.S. in Cell and Molecular Biology 🧬, which is why healthcare AI keeps pulling me back.

## 📬 Find me

🌐 [family-checker.com](https://family-checker.com) · 🏢 [modeo.io](https://modeo.io) · 💼 [LinkedIn](https://www.linkedin.com/in/arashyazdanimba) · 🐙 [GitHub](https://github.com/Arash-yazdani)

💬 Open to conversations about voice agents, agent evaluation, and healthcare AI.
