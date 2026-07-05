<!-- PROFILE README for Atharvax16 -->
<h1 align="center">Hi, I'm Atharva Kocharekar 👋</h1>
<p align="center">
  <a href="https://readme-typing-svg.demolab.com">
    <img src="https://readme-typing-svg.demolab.com?font=Fira+Code&size=20&pause=1000&center=true&vCenter=true&width=680&lines=MSc+Computing+(AI)+%40+Dublin+City+University;Researching+Generative+AI+for+Medical+Image+Restoration;Diagnostic+Reliability+%7C+Trustworthy+ML+%7C+XAI;Paper+under+review+%40+OMIA%2FMICCAI+2026" alt="Typing SVG" />
  </a>
</p>
<p align="center">
  <a href="https://www.linkedin.com/in/atharva-kocharekar-3512b4224/"><img src="https://img.shields.io/badge/LinkedIn-Connect-blue?logo=linkedin" /></a>
  <a href="mailto:atharvakocharekar0@gmail.com"><img src="https://img.shields.io/badge/Email-Contact-informational?logo=gmail" /></a>
  <a href="https://atharvax16.github.io/Portfolio/"><img src="https://img.shields.io/badge/Portfolio-Visit-success?logo=vercel" /></a>
  <img src="https://komarev.com/ghpvc/?username=Atharvax16&label=Profile%20views&color=0e75b6&style=flat" />
</p>
---
 
## 🔬 About my research
 
I'm an MSc Computing (AI) student at **Dublin City University**, supervised by **Prof. Alessandra Mileo**, working on generative-AI image restoration for **diabetic retinopathy (DR) screening**.
 
The thread running through everything I do is one question:
 
> **Does a model actually work — or does it just look like it does?**
 
My dissertation surfaces a **diagnostic paradox**: generative restorers can add pixel fidelity (e.g. Cold Diffusion, +12 dB PSNR) while *failing to recover — and often harming —* downstream diagnostic accuracy, because the "restored" images push the classifier off-distribution. I also find that **explanations drift faster than accuracy** as image quality drops, meaning a model can be right for the wrong reasons. This work is currently **under review at OMIA / MICCAI 2026**.
 
That same reliability lens shows up across my other work: telling AI-generated images from real ones, catching hallucinated pathology, and trusting calibration signals over surface-level metrics.
 
---
 
## 🧪 Current research threads
 
- **Generative restoration for DR screening** — benchmarking CLAHE, A-ESRGAN, SwinIR+GAN, Cold Diffusion and Conditional DDPM as restorers against CNNs and a ViT-Base classifier under nine synthetic degradations (blur / exposure / noise × 3 severities) on APTOS 2019. Found ViTs substantially more robust under severe noise (~62% vs ~20% accuracy) — a gap invisible on clean benchmarks.
- **Explainability under distribution shift** — quantifying how Grad-CAM, SHAP and attention rollout drift as quality degrades, and where restoration silently breaks interpretability.
- **AI-generated image detection** — CLIP-based ensemble work (0.941 F1) extending toward reference-free, generator-agnostic hallucination detection for medical images.
---
 
## 📄 Publications & preprints
 
- *Towards a Robust and Explainable Pipeline for Diabetic Retinopathy Classification through Quality-Aware GenAI Image Restoration* — **under review, OMIA/MICCAI 2026**
- *Autonomous Drone Navigation* — pitched at the International Conference on Engineering Research and Innovations, 2025
---
 
## 🌟 Featured repositories
 
- **[Comparative Study: DR Detection & Interpretability Methods](https://github.com/Atharvax16/Comparative-Study-for-Diabetic-Retinopathy-Detection-and-Interpretability-methods)**
  Core thesis repo — restoration pipelines, CNN vs ViT robustness benchmarking, and XAI-drift analysis behind the diagnostic paradox.
- **[3D Spatial Reasoning — Nomad AI](https://github.com/Atharvax16/3D-Spatial-Reasoning-Nomad-AI)**
  Neuro-symbolic system for collision-free, explainable object placement. The LLM parses intent into constraints; a deterministic geometry engine (AABB checks, clearance/walkway rules) computes valid candidates — avoiding LLM "coordinate hallucination."
- **AI-Generated Image Detection — Etsy ML Challenge** &nbsp; ⚠️ _add exact repo URL_
  Invited by Etsy to present. Separates authentic photos from diffusion/GAN images on a ~6,200-image dataset (0.941 F1). Found intermediate CLIP layers (18–23) beat final-layer features (0.923 vs 0.848 F1), fused with FFT/ELA frequency signals.
- **HealEdge — Federated Learning for DR Detection with XAI** &nbsp; ⚠️ _add exact repo URL_
  🥉 3rd place, Trinity College Dublin HealthTech Hackathon. GDPR/HIPAA-friendly ResNet-50 trained across non-IID hospital data, with Grad-CAM heatmaps so clinicians can verify predictions.
- **[Cyberattack Detection from CPU Usage Logs](https://github.com/Atharvax16/Cyberattack-Detection-using-CPU-Usage-Logs-Alert-System)**
  🏅 AWS-sponsored hackathon winner. Isolation Forest vs Random Forest anomaly detection, deployed on SageMaker with Lambda inference and SNS real-time alerts.
---
 
## 🧰 Technical toolkit
 
**ML / Data:** Python, NumPy, Pandas, scikit-learn, PyTorch, XGBoost, LightGBM
**Vision & GenAI:** CNNs, Vision Transformers, Diffusion models, GANs, image restoration, XAI (Grad-CAM, SHAP, Integrated Gradients, attention rollout)
**LLMs / Agents:** RAG, embeddings, vector DBs, prompt engineering, multimodal pipelines
**Backend / Infra:** FastAPI, Flask, Django, Docker
**Cloud:** AWS (S3, SageMaker, Lambda, SNS)
**DB:** PostgreSQL / SQLite, SQL, R
 
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
- 🥉 3rd place / 70 teams — Advanced HealthTech & MedTech Innovation Hackathon, Trinity College Dublin (2026)
- 🏅 Winner — Motivalogic Hackathon, sponsored by AWS, Dublin (2025)
- 🎤 Invited by **Etsy** to present AI-generated image detection research
- 🌍 Ambassador, **Thinking About Thinking** — responsible-AI community (AE Global Summit, London 2026)
---
 
<details>
<summary><b>📌 What I'm focusing on right now</b></summary>
- Resubmitting my OMIA/MICCAI paper with revised result tables and consistency fixes
- Building a quality-aware triage pipeline (selective prediction + calibrated trust scores) as a practical fix for the diagnostic paradox
- Extending AI-image detection toward reference-free hallucination detection in the medical domain
</details>
<details>
<summary><b>🤝 For collaborators / researchers</b></summary>
I'm especially keen to connect with people working on **medical imaging, generative models, model trustworthiness, or interpretability**. Happy to talk about diagnostic reliability, synthetic data, or where generative AI quietly breaks the things it claims to fix.
 
I care about: correctness, clarity, and shipping. Open to research and collaboration opportunities.
</details>
---
 
## 📫 Let's connect
- **LinkedIn:** [atharva-kocharekar](https://www.linkedin.com/in/atharva-kocharekar-3512b4224/)
- **Email:** atharvakocharekar0@gmail.com
- **Portfolio:** [atharvax16.github.io/Portfolio](https://atharvax16.github.io/Portfolio/)
