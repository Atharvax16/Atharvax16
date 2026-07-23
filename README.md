<!-- PROFILE README for Atharvax16 -->

<h1 align="center">Hi, I'm Atharva Kocharekar 👋</h1>

<p align="center">
  <a href="https://readme-typing-svg.demolab.com">
    <img src="https://readme-typing-svg.demolab.com?font=Fira+Code&size=20&pause=1000&center=true&vCenter=true&width=720&lines=MSc+Artificial+Intelligence+%40+Dublin+City+University;Robust+%26+Explainable+ML+for+High-Stakes+Vision;Currently%3A+episodic+memory+for+vision-language+agents;I+rebuild+the+papers+I+read+%E2%80%94+and+report+what+didn't+work" alt="Typing SVG" />
  </a>
</p>

<p align="center">
  <a href="https://www.linkedin.com/in/atharva-kocharekar-3512b4224/"><img src="https://img.shields.io/badge/LinkedIn-Connect-blue?logo=linkedin" /></a>
  <a href="mailto:atharvakocharekar0@gmail.com"><img src="https://img.shields.io/badge/Email-Contact-informational?logo=gmail" /></a>
  <a href="https://atharvax16.github.io/Portfolio/"><img src="https://img.shields.io/badge/Portfolio-Visit-success?logo=vercel" /></a>
  <a href="https://atharvax16.github.io/Portfolio/#/lab"><img src="https://img.shields.io/badge/Architecture%20Lab-6%20built-2B4C8C" /></a>
  <a href="https://github.com/Atharvax16/til"><img src="https://img.shields.io/badge/til-paper%20journal-9A7B1F" /></a>
  <img src="https://komarev.com/ghpvc/?username=Atharvax16&label=Profile%20views&color=0e75b6&style=flat" />
</p>

---

## 🔬 Abstract

I'm an MSc **Artificial Intelligence** student at **Dublin City University**, supervised by **Prof. Alessandra Mileo**, working on robust and explainable machine learning for high-stakes vision.

The thread running through everything I do is one question:

> **Does a model actually work — or does it just look like it does?**

My dissertation surfaces a **diagnostic paradox**: generative restorers can add pixel fidelity (Cold Diffusion, +12 dB PSNR) while *failing to recover — and often harming —* downstream diagnostic accuracy, because the "restored" images push the classifier off-distribution. Explanations also **drift faster than accuracy** as quality drops, meaning a model can be right for the wrong reasons. Currently **under review at OMIA / MICCAI 2026**.

That reliability lens shapes *how* I work, not just what I work on. I read a paper, then rebuild its mechanism small enough to watch it run — and I report the reproductions that failed as prominently as the ones that worked. **Two of the results below are negative.** They're the ones I'd want you to read.

---

## 🧵 Research threads

- **Generative restoration for DR screening** — benchmarking CLAHE, A-ESRGAN, SwinIR+GAN, Cold Diffusion and a conditional DDPM as restorers against CNNs and a ViT-Base classifier under **nine synthetic degradations** (blur / exposure / noise × 3 severities) on APTOS 2019. ViTs proved substantially more robust under severe noise (**~62% vs ~20%** accuracy) — a gap invisible on clean benchmarks.
- **Explainability under distribution shift** — quantifying how Grad-CAM, SHAP and attention rollout *drift* as quality degrades, scored by insertion/deletion AUC for faithfulness and Spearman stability rather than eyeballed heatmaps — and finding where restoration silently breaks interpretability.
- **Generative-image forensics** — separating authentic photographs from diffusion/GAN output via frequency artifacts and intermediate transformer features, extending toward reference-free, generator-agnostic hallucination detection for medical images.
- **Episodic memory for vision-language agents** — the current track, below. 🔴 *active*

---

## 🧭 Current track — VoxSight Recall

**Episodic memory for vision-language agents.** *(active since July 2026 · reading → reproducing → building)*

VoxSight can describe what the camera sees right now. It cannot answer *"where did I leave my keys?"* — because nothing it saw an hour ago survives the turn it was seen in. An agent that perceives continuously but remembers nothing has no episodic memory, only perception.

The bet: this is a **memory-architecture problem before it is a model problem**. Rather than fine-tune a bigger VLM and hope recall emerges from scale, I'm following the differentiable-memory literature from its origin and rebuilding each mechanism by hand.

One idea connects the whole reading list: **you cannot hard-pick one memory slot, because a hard pick has no gradient — so you softly blend several.** NTM blends notebook rows; RAG blends Wikipedia passages. Same trick, different scale. MemGPT then breaks the pattern in the useful direction — it gives up the gradient entirely and lets the model hard-pick at runtime by calling a function — making the real premise explicit: *the bottleneck was never capacity, it was allocation.*

| | Paper | Status |
|:--:|---|---|
| ✅ | **Neural Turing Machines** — Graves et al., 2014 | read · notes written |
| ✅ | **RAG for Knowledge-Intensive NLP** — Lewis et al., 2020 | **reproduced end to end** ↓ |
| ✅ | **MemGPT: LLMs as Operating Systems** — Packer et al., 2023 | read · notes written |
| 🔨 | Episodic-memory layer for VoxSight | design — once the reading lands |

**The gap I'm aiming at:** MemGPT never asks whether a memory can be *trusted*. Every self-edit lands with no source, no timestamp, no confidence, and no record of what it overwrote — and recursive summarisation compounds the error with no path back to the original observation. For a user who can't see, a confidently wrong memory is worse than an absent one. **Provenance over episodic memory** is the thread, and it's orthogonal to the paging mechanism.

---

## 🧪 Reproductions — including the ones that didn't work

Rebuilt from the paper on Apple Silicon (MPS), not cloned from a reference repo. Every number here is measured in my own notebook.

### RAG — Lewis et al. 2020, rebuilt end to end

15,077-passage index · 96 SQuAD-dev questions asked open-domain · exact MIPS · both equations written from scratch in log-space.

| Claim | My measurement | |
|---|---|:--:|
| Eq (1) & (2) from scratch match `transformers` | \|Δ\| = 0.0e+00 | ✅ |
| Retrieval beats closed-book (same generator weights) | 1.0 ± 1.0 → 24.0 ± 4.4 EM | ✅ |
| Retrieval beats *random* passages | 2.1 ± 1.5 → 24.0 ± 4.4 EM | ✅ |
| Answer-only loss moves the retriever (no passage labels) | gold-passage trust 0.097 → 0.354 | ✅ |
| Index hot-swap changes world knowledge, zero retraining | 2016 → 2020, weights untouched | ✅ |
| answer-recall@k rises monotonically with k | 26 → 36 → 50 → 61 → 71 | ✅ |
| Retriever has not collapsed (Appendix H) | 427 distinct docs / 480 slots | ✅ |
| Learned DPR beats BM25 *(paper: 43.5 vs 29.7)* | **24.0 ± 4.4 vs 44.8 ± 5.1 EM** | ❌ |

**BM25 winning is the interesting result.** A corpus-size artifact, not a refutation: DPR's query tower was fine-tuned on NaturalQuestions, my questions are SQuAD, and lexical overlap is unusually strong when the haystack is 15k passages instead of 21M. Reporting it beats quietly dropping the row.

### SteerViT — Ruthardt et al. 2026, small-scale

Frozen DINOv2 + gated cross-attention · RefCOCOg / COCO · 4,500 images · 3,000 steps *(the paper trains 20–50k)*.

| Condition | patch-grid IoU | PR-AUC |
|---|---|---|
| baseline (frozen, no text) | 0.1295 | 0.2208 |
| **steerability** (correct prompt) | **0.2940** | **0.5113** |
| wrong prompt (mismatched) | 0.2323 | 0.3926 |

Steering emerges — but the sanity check is the point. Feed a prompt describing a *different image* and localisation must collapse toward baseline. It didn't: **collapse ratio 0.625** against a 0.30 pass bar, so **62.5% of the gain survived a mismatched prompt**. At this scale the model is reading the image, not the text. **FAIL** — and it's the one number worth reporting. The gate (`tanh(α·ω)`, α initialised at 0) was verified to reproduce frozen DINOv2 *exactly* at ω=0.

---

## 🏗️ The Architecture Lab

Every architecture I study gets rebuilt as a hand-drawn, steppable sketch you can walk through and turn the knobs on — patch size, kernel size, the prompt you steer with, how many documents you retrieve. **[Enter the Lab →](https://atharvax16.github.io/Portfolio/#/lab)**

| Built | What you can step through |
|---|---|
| **Vision Transformer** | image → patchify → flatten → project → +CLS/pos |
| **CNN** | convolve · pool · receptive field · the transposed-conv step that becomes an AI-image detector |
| **DINOv2** | student–teacher → EMA → frozen embedding → XGBoost / MLP head |
| **SteerViT** | frozen ViT → gated cross-attention → prompt-steered features → the sanity check that failed |
| **RAG** | index → MIPS → concatenate → marginalise → the gradient that reaches the retriever |
| **AI-image forensics** | six lenses on a fake: FFT · ELA · up-convolution · CLIP · DINOv2 · learned artifacts |

**On the bench:** JEPA · Embedding space · VLM · NTM · MemGPT · Encoder–Decoder · Diffusion

---

## 📄 Publications & preprints

- *Towards a Robust and Explainable Pipeline for Diabetic Retinopathy Classification through Quality-Aware GenAI Image Restoration* — **under review, OMIA / MICCAI 2026**
- *Autonomous Drone Navigation* — pitched at the International Conference on Engineering Research and Innovations, 2025

---

## 🌟 Selected work

- **[Robust & Explainable AI for Diabetic Retinopathy](https://github.com/Atharvax16/Comparative-Study-for-Diabetic-Retinopathy-Detection-and-Interpretability-methods)** &nbsp;·&nbsp; *MSc thesis*
  A five-phase pipeline: 26,370 synthetic degraded fundus images → three DR graders (ResNet-50 / EfficientNet / ViT, ordinal focal loss, quadratic-weighted kappa) → a quantitative XAI benchmark (IG, SHAP, attention-rollout, Grad-CAM) → seven restorers (Cold Diffusion, conditional DDPM, SwinIR+GAN, …) → a **quality-aware trust router** that decides per image whether to enhance, which grader to trust, and which explanation to return. The central contribution is a **pathology-preserving DDPM** — a restorer constrained not to hallucinate lesions it cannot justify.

- **[VoxSight — Real-Time Accessibility Co-Pilot](https://github.com/Atharvax16/voxsight-copilot)** &nbsp;·&nbsp; *Cursor Hackathon → product*
  A conversational agent that "sees" for you: point a camera, hold a button, ask by voice, get a spoken answer. Audio + frame → STT → vision LLM → TTS in a single WebSocket round-trip. Built end-to-end in one night in mock mode with **zero API keys** — every service behind a swappable mock/live flag — then wired to real models the next morning without touching orchestration. Since grown intent routing, persistent memory, and **deterministic** turn-by-turn walking navigation (a routing engine, so it costs no model calls per step). The memory gap in this system is what started **VoxSight Recall** above.

- **AI-Generated Image Detection — Etsy Research Challenge** &nbsp;·&nbsp; 🥈 **2nd place**
  Authentic photographs vs diffusion/GAN images on a stratified ~4,340-image marketplace dataset. Hand-crafted forensics (FFT F1 0.60, ELA F1 0.65) against learned representations — and **intermediate CLIP layers beat the final embedding, 0.92 vs 0.85 F1**. A 6,018-dim fusion with 5-fold CV (0.87 ± 0.01), TTA and pseudo-labeling, then an Optuna-weighted 4-model ensemble reaching **≈0.94 F1**. Placed 2nd on Etsy's research leaderboard and was invited to present at Etsy HQ, Dublin. *(Repository private.)*

- **[HealEdge — Federated Learning for DR Detection with XAI](https://github.com/Atharvax16/Federated-Learning-for-Diabetic-Retinopathy-using-XAI)** &nbsp;·&nbsp; 🥉 *3rd of 70*
  AdvanceHealth MedTech Hackathon, Trinity College Dublin. FedAvg-trained ResNet-50 across non-IID hospital data so raw images never leave the client, with Grad-CAM heatmaps so clinicians can verify each prediction — addressing both the privacy and the trust barrier at once.

- **[Cyberattack Detection from CPU Usage Logs](https://github.com/Atharvax16/Cyberattack-Detection-using-CPU-Usage-Logs-Alert-System)** &nbsp;·&nbsp; 🏅 *AWS hackathon winner*
  Isolation Forest vs Random Forest on CPU telemetry — **98% accuracy, 78% recall**, recall deliberately optimised over precision, because a few false alarms beat missing the spike that matters. Deployed on SageMaker with Lambda inference and SNS real-time alerts.

- **[3D Spatial Reasoning — Nomad AI](https://github.com/Atharvax16/3D-Spatial-Reasoning-Nomad-AI)**
  Neuro-symbolic system for collision-free, explainable object placement. The LLM parses intent into constraints; a deterministic geometry engine (AABB checks, clearance/walkway rules) computes valid candidates — avoiding LLM "coordinate hallucination."

<details>
<summary><b>More projects — agents, multimodal & analytics</b></summary>

<br>

- **[CATAS — Compliance & Treasury Agents](https://github.com/Atharvax16/CATAS---Compilance-and-Treasury-Agentic-Solution)** *(Lyzr Hackathon)*
  A dual-agent system automating treasury reconciliation and compliance, **grounding LLM reasoning in deterministic ML** — Isolation Forest, Prophet and logistic regression underneath, with an immutable audit log on every action.

- **[Research Growth Companion](https://github.com/Atharvax16/Research-Growth-Companion---A-Multi-Agent-Research-Assistant)**
  A six-agent assistant (orchestrator + 5 specialists) keeping ML researchers current on papers, conferences, benchmarks and careers — sourcing from arXiv, Semantic Scholar and top venues.

- **VenueFlow — AI Wedding Coordinator** *(Build with Gemini XPRIZE)*
  Four agents — intake · venue · supplier · quote — sourcing vendors, drafting timelines and tracking budgets, with an `AgentDecisionLog` on every action so the whole run is auditable.

- **[Parkinson's — Gait, Voice & Tapping](https://github.com/Atharvax16/Parkinson-Detection-using-GAIT-Voice-Tapping-Analysis)**
  Multimodal screening fusing three signal types: gait, voice, and finger-tapping.

- **[Credit-Card Fraud Analysis](https://github.com/Atharvax16/Credit-Card-Fraud-Analysis)**
  Recall-first detection over 1.29M+ highly imbalanced transactions — target encoding, infrequent-class weighting, and F1 over accuracy as the evaluation metric by design.

</details>

---

## 🧱 Foundations — built from scratch

Because you don't really know a mechanism until you've written its backward pass.

- **[RNN + BPTT in NumPy](https://github.com/Atharvax16/Recurrent-Neural-Network-using-Numpy-from-Scratch)** — backpropagation through time by hand, to watch the gradient flow across timesteps
- **[Feed-Forward Neural Language Model](https://github.com/Atharvax16/FeedForward-Neural-Network-for-language-Modelling-from-Scratch)** — a Bengio-style neural LM from the ground up: embeddings, hidden layer, softmax
- **[Vanilla RNN & the Vanishing Gradient](https://github.com/Atharvax16/Vanilla-RNN-vanishing-gradient-problem-and-it-solutions)** — demonstrating why long-range dependencies collapse, and what fixes them

---

## 📖 `til` — the paper journal

Papers read in my own words, with notebooks where the idea needs to be *felt* rather than read. **[Browse the journal →](https://github.com/Atharvax16/til)**

Currently running threads on **image forensics** (Durall's up-convolution spectral tell, Frank's DCT counterpart, Gragnaniello's FFT baseline, and the argument that the detection arms race is unwinnable by design) and **memory architectures** (NTM → RAG → MemGPT), alongside *Attention Is All You Need*, *Generative Adversarial Nets*, and the MPNN → SchNet → DimeNet → NequIP arc.

---

## 🧰 Methods & tools

| | |
|---|---|
| **Modeling & Deep Learning** | PyTorch · timm · TensorFlow / Keras · scikit-learn · HF Transformers |
| **Generative & Diffusion** | DDPM · Cold Diffusion · GANs · SwinIR |
| **Explainability (XAI)** | Integrated Gradients · SHAP · Grad-CAM · Attention Rollout |
| **Representation & Forensics** | CLIP · DINOv2 · FFT / ELA · XGBoost |
| **Memory & Retrieval** | DPR / dense retrieval · MIPS · BM25 · vector DBs · agent design |
| **Foundations (from scratch)** | NumPy · BPTT / RNNs · Neural LMs · Optimization |
| **Infra & MLOps** | AWS SageMaker · Lambda / SNS · Docker · FastAPI · WebSockets |

<p>
  <img src="https://skillicons.dev/icons?i=python,pytorch,fastapi,flask,docker,linux,git,postgres,sqlite,aws&perline=10" />
</p>

---

## 📊 GitHub at a glance

<p align="center">
  <img height="170" src="https://github-readme-stats.vercel.app/api?username=Atharvax16&show_icons=true&rank_icon=github&include_all_commits=true" />
  <img height="170" src="https://github-readme-stats.vercel.app/api/top-langs/?username=Atharvax16&layout=compact" />
</p>

<p align="center">
  <img src="https://streak-stats.demolab.com?user=Atharvax16" />
</p>

<p align="center">
  <img src="https://github-readme-activity-graph.vercel.app/graph?username=Atharvax16" />
</p>

---

## 🏆 Highlights

<p align="center">
  <img src="https://github-profile-trophy.vercel.app/?username=Atharvax16&row=1&column=7" />
</p>

- 🥈 **2nd place**, Etsy Research Leaderboard — invited to present AI-image detection research at Etsy HQ, Dublin
- 🥉 **3rd of 70 teams** — Advanced HealthTech & MedTech Innovation Hackathon, Trinity College Dublin (2026)
- 🏅 **Winner** — Motivalogic Hackathon, sponsored by AWS, Dublin (2025)
- 🌍 Ambassador, **Thinking About Thinking** — responsible-AI community (AE Global Summit, London 2026)

---

<details>
<summary><b>📌 What I'm focusing on right now</b></summary>

<br>

- Resubmitting the OMIA/MICCAI paper with revised result tables and consistency fixes
- **VoxSight Recall** — designing the episodic-memory layer, with **provenance** as a first-class property rather than an afterthought
- Building a quality-aware triage pipeline (selective prediction + calibrated trust scores) as a practical fix for the diagnostic paradox
- Extending AI-image detection toward reference-free, generator-agnostic hallucination detection in the medical domain
- Working through the Architecture Lab backlog — **NTM and MemGPT are next on the bench**

</details>

<details>
<summary><b>🗺️ How I got here</b></summary>

<br>

| Year | | |
|---|---|---|
| **2021** | The Spark — TEC Mumbai | B.E. in AI & Data Science. Fell for the question behind the model: *why does this work?* |
| **2023** | First Impact — Data Science Intern | Production ML pipelines. Learned that clean data beats clever models. |
| **2024** | Going Global — Dublin | MSc in Artificial Intelligence at DCU; began the thesis on robust, explainable DR screening. |
| **2025** | Research Mode | Diffusion restoration + a quantitative XAI benchmark; a separate study on detecting AI-generated images. Reading and reproducing foundational papers in parallel. |
| **2026** | Etsy Recognition | The detection research placed 2nd on Etsy's leaderboard — presented in person at Etsy HQ, Dublin. |
| **2026** | What's next | ML / applied-research roles and collaborations — robustness, explainability, memory architectures. |

</details>

<details>
<summary><b>🤝 For collaborators / researchers</b></summary>

<br>

I'm especially keen to connect with people working on **medical imaging, generative models, memory architectures, model trustworthiness, or interpretability**. Happy to talk about diagnostic reliability, synthetic data, episodic memory for agents, or where generative AI quietly breaks the things it claims to fix.

I care about correctness, clarity, and shipping — and about reporting the result that didn't go my way. Open to research and collaboration opportunities.

</details>

---

## 📫 Let's connect

- **LinkedIn:** [atharva-kocharekar](https://www.linkedin.com/in/atharva-kocharekar-3512b4224/)
- **Email:** atharvakocharekar0@gmail.com
- **Portfolio:** [atharvax16.github.io/Portfolio](https://atharvax16.github.io/Portfolio/)
- **Architecture Lab:** [the mechanisms, steppable](https://atharvax16.github.io/Portfolio/#/lab)
- **Paper journal:** [`til`](https://github.com/Atharvax16/til)
