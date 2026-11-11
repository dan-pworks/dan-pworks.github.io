---
title: "Can I leverage AI on-device?"
description: "How much of my daily AI usage actually runs on the hardware in my pocket — and where Apple's on-device models still can't replace OpenAI and Anthropic."
pubDate: 2026-11-11
updatedDate: 2026-11-11
tags: ["Mobile", "Apple", "Apple Intelligence", "iOS", "iPadOS", "MacOS"]
---

Here's my AI footprint on a normal Tuesday: Copilot writes half my commits at work, Codex and OpenCode handle the side quests, and the ChatGPT app on my phone covers everything from dinner ideas to "explain this stack trace like I'm five." Every one of those prompts leaves my house, lands in someone else's data center, and shows up on a bill — or in a privacy policy I didn't read closely enough.

So I've been sitting with one question: how much of that could run on the hardware I already own? Not as a privacy stunt — as a practical split. On-device for what fits, cloud for what doesn't. The answer changed more this year than in the previous two combined, so it felt worth writing down.

## How Apple actually runs "on-device" AI

Apple Intelligence was never one model. It's a ladder. The bottom rung is a ~3-billion-parameter language model that runs entirely on the device. Above it sits Private Cloud Compute — Apple's servers, with published guarantees that requests aren't stored. And at the top, if you opt in, ChatGPT handles the world-knowledge questions. The tiering exists because physics: nobody is stuffing a frontier model into a phone without it catching fire.

This summer the ladder got rebuilt. At WWDC26 Apple announced the third generation of its foundation models — five models, built in collaboration with Google. The one that matters for this question is **AFM 3 Core Advanced**: a 20-billion-parameter sparse model that runs on the device, activates only 1–4 billion parameters per request, and keeps its full weight set in flash storage, streaming experts into memory only when a prompt needs them. It's natively multimodal, so text and images both go in. Two years ago, the on-device ceiling was a 3B model for notification summaries and proofreading. Now it's this.

One detail worth knowing before you assume "on-device" means "Apple only": the biggest server model in the family, AFM 3 Cloud Pro, runs on NVIDIA GPUs in Google Cloud under the same Private Cloud Compute rules. That's fine — it's disclosed — but it changes what "local" means in this story, and I'd rather you hear it from me than from a footnote.

## The part you can call from code

Since iOS 26, the Foundation Models framework gives Swift developers direct access to Apple's on-device model. No API key, no network call, no per-token bill. You get guided generation (declare a struct, the model fills it in — typed output instead of JSON prayer), tool calling, and streaming. It's the same model the OS features use, running in its own sandboxed process.

What changed at WWDC26 is the part that reshuffles my answer:

- **Any model can back a session now.** A new `LanguageModel` protocol means the on-device system model, Private Cloud Compute (32K context, adjustable reasoning levels, no accounts, no API keys), Core AI (local models on the Neural Engine), and MLX (thousands of open models from MLX-Community on Hugging Face) all speak the same API.
- **Anthropic and Google are publishing Swift packages** so Claude and Gemini plug into that same API, and the framework itself is going open source — it'll run anywhere Swift runs, Linux servers included.
- **New built-in system tools**: OCR, barcode reading, and a Spotlight-powered local RAG tool. All on-device.
- **A free tier that sounds made up**: if you're in the App Store Small Business Program with fewer than 2 million first-time downloads, you can call Apple's models running in Private Cloud Compute with no cloud API cost.

Here's the honest sizing from Apple's own machine learning team: the on-device model is built for summarization, entity extraction, text understanding, refinement, and short dialog — their 2025 write-up says outright it's "not designed to be a chatbot for general world knowledge." That's the lane. Stay in it and the thing is genuinely good.

| Task | Where I'd run it |
|---|---|
| Summarize an email thread | On-device |
| Extract entities from a document | On-device |
| Draft a standup note or a reply | On-device |
| RAG over my own files | On-device (Spotlight tool) |
| Read a barcode, OCR a receipt | On-device |
| Refactor a Spring service | Cloud |
| Agentic, multi-file coding work | Cloud |
| Anything needing current world knowledge | Cloud |

## The hardware gate

This is the fine print that decides whether any of it works for *your* users, not just for you.

The floor for Apple Intelligence today is an iPhone 15 Pro, anything in the iPhone 16 family or newer, iPads and Macs with M1 or later. The advanced on-device model needs the newest tier: iPhone Air or iPhone 17 Pro, iPads with M4 or later and at least 12GB of memory, Macs with M3 or later and 12GB. Yes, macOS is on 27 now — "Golden Gate," which sounds like a bridge budget overrun but is apparently an operating system. The models themselves take up to 8GB of storage, 14GB on the advanced devices.

If your app's audience includes an iPhone 14, your "on-device" feature needs a fallback: Private Cloud Compute, a smaller local model, or a feature flag. Apple's requirements page is the source of truth here, and it moves.

## Rolling your own on the Mac

The Mac, meanwhile, has quietly become the best consumer inference box you can buy. Unified memory means CPU and GPU share one pool — no PCIe taxi between them — so the RAM you bought is the VRAM you get.

I keep three tools around:

- [MLX](https://github.com/ml-explore/mlx) — Apple's own array framework for Apple silicon, out of their ML research group. Python API that follows NumPy, higher-level packages that follow PyTorch. It's also now a first-class citizen of the Foundation Models framework itself.
- [Ollama](https://ollama.com) — the easiest way to run open models, full stop. Nine million installs a month says I'm not the only one who thinks so.
- [LM Studio](https://lmstudio.ai) — the GUI option, with MLX and llama.cpp under the hood.

And underneath half the local-AI world sits [llama.cpp](https://github.com/ggml-org/llama.cpp), where Apple silicon is a first-class citizen — Metal, Accelerate, the works. A 7B-class model runs comfortably on basically any modern Mac. The big open models want RAM to spare and a fan that means business.

## Where the cloud still wins

Now the part I have to be honest about, because it's most of my actual job.

My day job is Java services for healthcare reporting. The work I do with Copilot and Codex — reading across an entire codebase, planning a migration, writing the regression tests that prove it didn't break anything — needs frontier-class reasoning and a context window measured in whole repositories. Nothing on-device touches that. Apple isn't pretending otherwise; they built AFM 3 Cloud Pro for exactly that kind of work and put it in Private Cloud Compute, which is a server, not your phone.

Two more realities to price in. Server-side Apple Intelligence features have daily usage limits, and Apple has said expanded access will be available "for a fee" in the future. And on-device isn't billed per token, but it's not free either — it costs battery, memory, and thermals. Physics again.

## So, can you?

Yes — for a bigger slice than a year ago, and the boundary is still moving.

My working split: everything small and text-shaped (summaries, extraction, classification, drafts, search over my own files) stays on my devices. The heavy reasoning and agentic coding stays in the cloud, deliberately, because pretending a 3B model should do that job is how you get confident garbage. The middle ground — tasks too big for the phone but too sensitive for a third party — goes to Private Cloud Compute, which is still someone else's computers, just with better manners than most.

If your goal is specifically cutting OpenAI and Anthropic out of the loop: doable for consumer-facing features, not yet doable for serious engineering work. But the direction is real. The phone in my pocket now runs a 20-billion-parameter model and reads barcodes offline. It still won't refactor my Spring beans — but that first sentence would've gotten me laughed out of a design review in 2024.

## References

- [Introducing the Third Generation of Apple's Foundation Models — Apple Machine Learning Research](https://machinelearning.apple.com/research/introducing-third-generation-of-apple-foundation-models)
- [Updates to Apple's On-Device and Server Foundation Language Models (2025) — Apple Machine Learning Research](https://machinelearning.apple.com/research/apple-foundation-models-2025-updates)
- [Introducing Apple's On-Device and Server Foundation Models (2024) — Apple Machine Learning Research](https://machinelearning.apple.com/research/introducing-apple-foundation-models)
- [Foundation Models framework — Apple Developer Documentation](https://developer.apple.com/documentation/foundationmodels)
- [Get started with the Foundation Models framework — Apple Developer](https://developer.apple.com/foundation-models-framework/)
- [What's new in the Foundation Models framework — WWDC26 session](https://developer.apple.com/videos/play/wwdc2026/241/)
- [Meet the Foundation Models framework — WWDC25 session](https://developer.apple.com/videos/play/wwdc2025/286/)
- [Get started with the next generation of Apple Intelligence (device requirements) — Apple Support](https://support.apple.com/en-us/121115)
- [Apple Intelligence — Apple](https://www.apple.com/apple-intelligence/)
- [MLX — GitHub](https://github.com/ml-explore/mlx)
- [Ollama](https://ollama.com)
- [LM Studio](https://lmstudio.ai)
- [llama.cpp — GitHub](https://github.com/ggml-org/llama.cpp)
