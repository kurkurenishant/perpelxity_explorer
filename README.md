# 🌌 Perplexity Explorer — Premium AI Language Model Playground

**Perplexity Explorer** is a zero-build, client-side educational playground that helps students, researchers, and developers understand how autoregressive causal language models predict tokens, evaluate probability distributions, and calculate sequence perplexity.

The entire application runs **locally in the browser** using **Transformers.js v3** and an 8-bit quantized ONNX model (`Xenova/distilgpt2`). No server, no Python backend, no build tools, and no API keys are required.

![Perplexity Explorer Banner](https://img.shields.io/badge/Model-Xenova%2Fdistilgpt2--q8-cyan?style=for-the-badge)
![Transformers.js v3](https://img.shields.io/badge/Powered%20by-Transformers.js%20v3-8B5CF6?style=for-the-badge)
![Zero Dependencies](https://img.shields.io/badge/Dependencies-Zero%20(Pure%20HTML%2FCSS%2FJS)-A3E635?style=for-the-badge)

---

## ⚡ Quick Start

You can run the application using any standard local development server.

### Option 1: Python 3 HTTP Server
```bash
python3 -m http.server 8000
```
Open [http://localhost:8000](http://localhost:8000) in any modern browser.

### Option 2: Node.js (npx serve)
```bash
npx serve .
```

---

## 🎯 Key Features

### 1. 🧪 Sentence Lab
- Interactive multiline input with live character, word, and subword token counters.
- One-click sample sentences demonstrating high fluency vs ungrammatical/scrambled perplexity contrasts (e.g., `"I love Python"` vs `"Python love I"`).
- Real-time Hugging Face Hub download progress bar and memory initialization indicator.

### 2. 🔤 Tokenization & Token Inspector
- Byte-Pair Encoding (BPE) subword segmentation.
- Distinct color-coded token chips:
  - **Context Prefix**: Token `50256` (`<|endoftext|>`)
  - **Word Tokens**: Alphanumeric words
  - **Whitespace Tokens**: Visible `␣` glyphs
  - **Punctuation**: Syntactic separators
- Interactive Token Inspector drawer revealing Token ID, sequence position, raw logit, softmax probability $P$, negative log-likelihood (nats), and information content in bits.

### 3. 📊 Perplexity Calculator
- Glowing gradient typography displaying the sequence perplexity:
  $$\text{Perplexity} = \exp\left(\frac{1}{N} \sum_{i=1}^N -\ln P(t_i \mid \text{context})\right)$$
- 3-step educational breakdown:
  - **Step 1**: Calculate individual token surprises ($-\ln P$)
  - **Step 2**: Calculate Average Negative Log-Likelihood ($\overline{\text{NLL}}$)
  - **Step 3**: Exponentiate to yield effective branching factor
- Educational tooltips clarifying that perplexity measures statistical predictability under training data, not factual truth or reasoning capability.

### 4. 📋 Token Probability Analysis Table
- Numerically stable log-softmax outputs across the entire sequence.
- Interactive sorting by position, token name, token ID, probability, or surprise.
- Filter search box.
- Advanced columns toggle for raw logits and bits ($-\log_2 P$).

### 5. 🌡️ Token Probability Heatmap
- Visual intensity mapping across the sentence.
- View toggles:
  - **Probability View**: Glowing orange and white intensity for high-confidence tokens.
  - **Surprise View**: Fiery orange-red glow highlighting unexpected tokens.
- Hover popovers with exact metrics.

### 6. 🔮 Next-Token Predictions
- Computes distribution over the 50,257 vocabulary entries at the final sequence position.
- Selectable Top 5, 8, 10, or 20 candidates with animated probability bars.
- One-click **+ Append** button to add candidate tokens directly to the sentence.

### 7. ✍️ Autoregressive Text Continuation
- Generates text step-by-step in browser memory with live token streaming.
- Adjustable sampling hyperparameters:
  - **Max New Tokens**: 5 to 50
  - **Temperature**: 0.0 (greedy) to 1.5 (creative)
  - **Top-k**: 0 to 100
  - **Top-p (Nucleus)**: 0.1 to 1.0
  - **Repetition Penalty**: 1.0 to 2.0
- Instant **"Use generated text as input"** workflow.

### 8. 🎲 Perplexity Sandbox (Simulated Calculator)
- Explicitly badged as `SIMULATED — NOT FROM THE MODEL`.
- Allows students to manually experiment with token probabilities ($0 < P \le 1.0$) using sliders.
- Real-time recalculation of simulated perplexity, showing how a single low-probability token dramatically spikes perplexity.

---

## 🔬 Mathematical Foundation

### Why Prepend Token `50256`?
In causal autoregressive language models, each prediction is conditioned on prior context:
$$P(t_i \mid t_1, t_2, \dots, t_{i-1})$$
For the very first token $t_1$ of an isolated sentence, there is no preceding text. DistilGPT-2 uses token `50256` (`<|endoftext|>`) as the Start-of-Sequence marker, providing a prior distribution $P(t_1 \mid \text{BOS})$ without including it in the final sentence length $N$.

### Stable Log-Softmax
To prevent floating-point overflow when calculating $e^z$ on large logits:
$$\ln P(t_i) = (z_{t_i} - \max_j z_j) - \ln\left(\sum_j \exp(z_j - \max_j z_j)\right)$$

---

## 🎨 Design System

- **Color Palette & Glassmorphism**:
  - Main Background: Deep Warm Obsidian (`#0B0A0E`) with floating organic ambient light orbs
  - Primary Orange: `#FF6B00` (Electric Sunset Orange)
  - Light Orange / Amber: `#FF9E44` & `#FFA500`
  - Pristine White: `#FFFFFF`
  - Frosted Glass Cards: `rgba(22, 18, 26, 0.58)` with `backdrop-filter: blur(24px)`
  - Specular Glass Highlights: `border: 1px solid rgba(255, 255, 255, 0.14)` and `border-top: 1px solid rgba(255, 255, 255, 0.3)`
  - Success Green: `#A3E635`
  - Error Rose: `#FF4D4D`
- **Typography**: Inter & Fira Code
- **Themes**: Orange Obsidian Glass (Default), Frost White Glass (Light Mode), Amber Sunset Glass

---

## 📄 License

MIT License. Designed and built for AI education and exploration.
