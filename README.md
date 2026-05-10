# 🎙️ EL-KW — Voice AI Platform

> **Manipulate, clone, and transform any voice using just 3–5 seconds of audio.**

EL-KW is a ComfyUI-based voice AI platform that combines three powerful custom node packages to deliver a complete suite of voice manipulation capabilities — including zero-shot voice cloning, emotion control, and multilingual speech synthesis — all within a visual, node-based workflow.

---

## ✨ What It Does

| Capability | Description |
|---|---|
| 🎭 **Voice Cloning** | Replicate any voice from a 3–5 second recording with zero training |
| 😄 **Emotion Control** | Change tone, style, and emotional delivery of synthesized speech |
| 🌍 **Language Management** | Generate speech across 10+ languages with natural prosody |
| 🗣️ **Multi-Speaker Dialogue** | Compose full conversations with multiple distinct voices |
| 🎨 **Voice Design** | Create entirely new voices from text descriptions |

---

## 🧩 Core Modules

This platform integrates three ComfyUI custom node packages:

### 1. [`ComfyUI-Qwen-TTS`](https://github.com/flybirdxx/ComfyUI-Qwen-TTS)
Powered by **Alibaba's Qwen3-TTS** model. Handles the core TTS, voice cloning, and voice design pipeline.

- Zero-shot voice cloning from short reference audio
- Voice design via natural language descriptions (e.g., *"a calm, deep male narrator"*)
- Preset speaker library with style instruction support
- Multi-role dialogue generation
- Supports 10 languages: Chinese, English, Japanese, Korean, German, French, Russian, Portuguese, Spanish, Italian
- Model sizes: **0.6B** (fast) and **1.7B** (high quality)

### 2. [`ComfyUI-IndexTTS2`](https://github.com/snicolast/ComfyUI-IndexTTS2)
Provides an additional TTS inference backbone for extended voice manipulation and synthesis options within the ComfyUI workflow.

### 3. [`ComfyUI_Fill-ChatterBox`](https://github.com/filliptm/ComfyUI_Fill-ChatterBox)
Adds voice emotion and style transfer capabilities, enabling fine-grained control over the emotional delivery of generated speech.

---

## 📁 Repository Structure

```
EL-KW/
├── ComfyUI-Qwen-TTS/          # Qwen3-TTS nodes: cloning, design, dialogue
├── ComfyUI-IndexTTS2/         # IndexTTS2 nodes: extended TTS backbone
└── ComfyUI_Fill-ChatterBox/   # ChatterBox nodes: emotion & style transfer
```

---

## ⚙️ Requirements

- [ComfyUI](https://github.com/comfyanonymous/ComfyUI)
- Python 3.10+
- CUDA-capable GPU (8GB+ VRAM recommended)
- `transformers==4.57.3` *(required — versions ≥ 5.0 are incompatible)*

### Install dependencies

```bash
pip install torch torchaudio transformers==4.57.3 librosa accelerate
```

For faster inference, optionally install an optimized attention backend:

```bash
pip install sage_attn   # Fastest (recommended)
# or
pip install flash_attn  # Fast
# sdpa is built into PyTorch — no install needed
```

---

## 🚀 Getting Started

1. **Clone this repo** into your ComfyUI `custom_nodes` directory:
   ```bash
   cd ComfyUI/custom_nodes
   git clone https://github.com/happyvictor-Vesper/EL-KW.git
   ```

2. **Download models** for Qwen-TTS and place them under `ComfyUI/models/qwen-tts/`:
   ```
   models/qwen-tts/
   └── Qwen/
       ├── Qwen3-TTS-12Hz-1.7B-Base/
       ├── Qwen3-TTS-12Hz-0.6B-Base/
       ├── Qwen3-TTS-12Hz-1.7B-VoiceDesign/
       └── Qwen3-TTS-Tokenizer-12Hz/
   ```

3. **Open ComfyUI** and load or build your workflow using the EL-KW nodes.

4. **Record a reference clip** (3–5 seconds of clean speech) and connect it to a voice cloning node to get started.

---

## 🎯 Workflow Overview

```
[Reference Audio (3–5s)]
         │
         ▼
[VoiceClonePromptNode]  ──→  Extract voice features
         │
         ▼
[VoiceCloneNode / DialogueInferenceNode]
         │         ╲
         │          [EmotionStyleNode (ChatterBox)]
         │
         ▼
[IndexTTS2 Node]  (optional extended synthesis)
         │
         ▼
[Audio Output]
```

---

## 💡 Tips

- **Clean audio = better clones.** Use noise-free reference recordings for best voice reproduction.
- **Always provide reference text** alongside the reference audio clip — this significantly improves clone quality.
- **Low VRAM?** Use the 0.6B model and enable `unload_model_after_generate` to free GPU memory between runs.
- **Multilingual output** works best when the target language matches the model's native language support.
- Use `attention: "auto"` to automatically select the fastest attention mechanism available on your system.

---

## 🙏 Credits

| Project | Author | Purpose |
|---|---|---|
| [Qwen3-TTS](https://github.com/QwenLM/Qwen3-TTS) | Alibaba Qwen Team | Core TTS & cloning model |
| [ComfyUI-Qwen-TTS](https://github.com/flybirdxx/ComfyUI-Qwen-TTS) | flybirdxx | ComfyUI integration |
| [ComfyUI-IndexTTS2](https://github.com/snicolast/ComfyUI-IndexTTS2) | snicolast | Extended TTS backbone |
| [ComfyUI_Fill-ChatterBox](https://github.com/filliptm/ComfyUI_Fill-ChatterBox) | filliptm | Emotion & style control |

---

## 📄 License

This project integrates open-source components. Each module is subject to its own license:
- **ComfyUI-Qwen-TTS** — Apache License 2.0
- Model weights — [Qwen3-TTS License Agreement](https://github.com/QwenLM/Qwen3-TTS#License)

Please review the individual licenses of each component before commercial use.
