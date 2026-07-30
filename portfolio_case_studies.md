# Frame It as Cases: Work That Speaks for Itself

**Author**: Samar Jamal  
**Profile**: B.Tech AI & ML Student | Amazon ML Summer School Trainee  
**Proof Statement**: As a B.Tech AI & ML student and Amazon ML Summer School trainee, I build and evaluate leak-free, production-ready machine learning pipelines on real data. This portfolio exists for a Senior Machine Learning Engineering Lead at an AI-first tech company who values evaluation rigor, clean PyTorch code, and benchmark transparency over generic resume buzzwords. By inspecting my verifiable end-to-end pipeline code, baseline comparisons, and client-holdout validation reports, I want them to take one single action: schedule a 15-minute technical screening call with me.

---

## Case Study 1: MediScan AI — RAG-Powered Healthcare Intelligence Platform

### The Problem
Out-of-the-box LLMs frequently hallucinate medical treatments, misinterpret dosage guidelines, or offer ungrounded health advice. In healthcare software, a hallucinated recommendation isn't a cosmetic bug—it poses real clinical risks. Medical query retrieval requires strict grounding: responses must be constrained exclusively to verified medical literature and clinical databases, while maintaining fast response times and persistent multi-turn conversational context.

### What I Did
- Engineered a full-stack RAG healthcare platform utilizing React, TypeScript, Node.js, and PostgreSQL for state management.
- Integrated vector similarity search using Pinecone and Gemini API embeddings over clinical vector indexes.
- Designed a **contextual query rewriting pipeline**: before retrieval, user queries are normalized and expanded to resolve ambiguous medical terms and conversational pronouns.
- Implemented **source-grounded prompt constraint**: enforced strict system instructions demanding that the model output "Insufficient context" if the vector search similarity threshold fell below $\cos(\theta) < 0.72$.
- Resolved vector store latency by caching frequent semantic query embeddings in PostgreSQL, reducing average query latency by ~40%.

### Outcome
- Achieved zero ungrounded medical hallucinatory claims in test evaluation benchmarks across 100+ standard clinical query scenarios.
- Average retrieval-to-generation pipeline latency reduced to < 1.2 seconds.
- *Lesson learned*: RAG performance is dominated by chunking strategy and metadata filtering, not model parameter count.

### Before / After Comparison

> **Generic AI Version**:
> *"MediScan AI is a state-of-the-art revolutionary AI healthcare platform leveraging cutting-edge LLMs and vector databases to deliver seamless, ultra-accurate medical insights and transform patient care."*

> **Samar's Version**:
> *"Built a full-stack RAG medical intelligence platform using TypeScript, Pinecone, and Gemini API. Implemented contextual query rewriting and a strict cosine similarity cutoff (< 0.72) to eliminate ungrounded LLM hallucinations and enforce source-backed medical responses."*

*Why Samar's version is stronger*: Strips marketing hype ("revolutionary", "cutting-edge") and explicitly names the engineering decisions (similarity thresholding, query rewriting) and concrete architecture.

---

## Case Study 2: AI Disaster Response Coordinator — OpenEnv Reinforcement Learning Environment

### The Problem
During natural disaster events, emergency dispatchers face severe resource constraints and time-critical priority triage decisions. Standard heuristic dispatch algorithms fail to handle dynamic demand spikes, while off-the-shelf LLMs lack structured environment interfaces to test multi-step resource allocation strategies under constraints.

### What I Did
- Built a custom **OpenEnv-compliant Reinforcement Learning environment** simulating disaster-response resource dispatching with priority queues and supply constraints.
- Benchmarked baseline agent performance against **Qwen2.5-72B-Instruct** across three complexity tiers (Easy, Medium, Hard).
- Designed a custom weighted reward function balancing response urgency, travel distance, and resource depletion rate.
- Containerized the environment with Docker and exposed microservice APIs via FastAPI for reproducible testing.

### Outcome
- Achieved a **0.884 weighted evaluation score** across all difficulty tiers.
- Demonstrated that structured RL environment constraints prevent agent resource exhaustion by 34% compared to greedy baseline heuristics.
- *Lesson learned*: Designing clean state representations and reward penalties is far more critical for agent convergence than scaling model parameters.

### Before / After Comparison

> **Generic AI Version**:
> *"Created a groundbreaking AI-powered disaster management system that revolutionizes emergency response using advanced reinforcement learning and state-of-the-art LLMs."*

> **Samar's Version**:
> *"Built an OpenEnv-compliant RL simulation environment for disaster resource allocation. Benchmarked Qwen2.5-72B-Instruct against priority-dispatch heuristics, achieving an 0.884 weighted score across Easy, Medium, and Hard evaluation tiers."*

*Why Samar's version is stronger*: Replaces vague buzzwords with concrete environment compliance standards (OpenEnv), specific models evaluated (Qwen2.5-72B), and real benchmark scores (0.884 weighted score).

---

## Case Study 3: Scene Classification with EfficientNet-B2 — Deep Learning Image Classifier

### The Problem
Training deep learning image classifiers on large-scale datasets (such as SUN397 with 60K+ images across 397 fine-grained scene categories) suffers from heavy computational bottlenecks, long epoch times, and memory overruns on single-GPU hardware.

### What I Did
- Fine-tuned an **EfficientNet-B2** architecture using PyTorch and `timm` on the SUN397 dataset (397 classes, 60,000+ images).
- Implemented **CUDA Automatic Mixed Precision (AMP)** (`torch.cuda.amp`), cutting GPU memory footprint by ~45% and reducing training time per epoch from 18 minutes to 9.5 minutes.
- Applied **Test-Time Augmentation (TTA)** (flipping and multi-scale crops) during evaluation to boost inference robustness on out-of-distribution scene samples.
- Conducted hyperparameter sweeps across learning rate schedules (Cosine Annealing with Warm Restarts) and weight decay.

### Outcome
- Achieved **75% macro F1-score** and **72–75% top-1 accuracy** across 397 fine-grained scene classes.
- Reduced total model training time by 47% while maintaining zero loss of numerical precision.
- *Lesson learned*: Mixed precision and inference-time augmentations deliver higher performance gains than simply picking a larger backbone model.

### Before / After Comparison

> **Generic AI Version**:
> *"Engineered a high-performance deep learning image classification model using advanced PyTorch neural networks to achieve industry-leading computer vision accuracy."*

> **Samar's Version**:
> *"Fine-tuned EfficientNet-B2 on SUN397 (397 classes, 60K+ images) using PyTorch and CUDA AMP. Achieved a 75% macro F1-score while cutting training time by 47% through mixed-precision training and Test-Time Augmentation."*

*Why Samar's version is stronger*: Replaces generic claims ("high-performance", "industry-leading") with exact metrics (75% macro F1, 47% training time reduction) and specific execution techniques (CUDA AMP, TTA).

---

## Case Study 4: SenseLink — Edge-AI Assistive System on ESP32

### The Problem
Visually and hearing-impaired users require real-time obstacle detection and scene navigation, but cloud-dependent computer vision systems suffer from high latency and connectivity dropouts on mobile hardware.

### What I Did
- Engineered an edge-AI hardware prototype using ESP32 microcontrollers integrated with lightweight object detection models.
- Quantized and optimized **YOLO object detection** models for low-power edge inference.
- Combined real-time visual detection with on-device NLP live captioning to deliver multimodal auditory and visual navigation alerts.

### Outcome
- Achieved low-latency on-device obstacle detection under constrained RAM/power budgets.
- *Lesson learned*: Edge deployment requires strict memory layout optimization and model quantization before pushing code to microcontrollers.

### Before / After Comparison

> **Generic AI Version**:
> *"Developed a futuristic IoT accessibility wearable utilizing cutting-edge computer vision to transform the lives of impaired users."*

> **Samar's Version**:
> *"Built an edge-AI assistive system on ESP32 combining quantized YOLO object detection and live captioning for real-time visual and auditory navigation on constrained hardware."*

*Why Samar's version is stronger*: Direct, concise, and focuses strictly on edge constraints, microcontrollers, and quantization.

---

## Bio & Contact Section

- **Bio**: Samar Jamal is a B.Tech AI & ML student at Graphic Era Hill University and Machine Learning Trainee at Amazon ML Summer School. He specializes in building leak-free ML pipelines, PyTorch computer vision systems, and full-stack AI applications.
- **GitHub**: [github.com/Samarjamal326](https://github.com/Samarjamal326)
- **LinkedIn**: [linkedin.com/in/samar-jamal](https://linkedin.com/in/samar-jamal)
- **Email**: Samarjamal326@gmail.com
- **Call-to-Action**: *"Looking for a Machine Learning or Software Engineering Intern who values clean code, reproducible benchmarks, and validation rigor? Schedule a 15-minute technical screening call with me."*
