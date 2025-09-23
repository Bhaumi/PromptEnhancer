<div align="center">

# PromptEnhancer: A Simple Approach to Enhance Text-to-Image Models via Chain-of-Thought Prompt Rewriting

[**Linqing Wang**](https://scholar.google.com/citations?hl=en&view_op=list_works&gmla=AH8HC4z9rmDHYjp5o28xKk8U4ddD_n7BuMnk8UZFP-jygFBtHUSz6pf-5FP32B_yKMpRU9VpDY3iT8eM0zORHA&user=Hy12lcEAAAAJ) · 
[**Ximing Xing**](https://ximinng.github.io/) · 
[**Yiji Cheng**](https://scholar.google.com/citations?user=Plo8ZSYAAAAJ&hl=en) · 
Zhiyuan Zhao · 
Donghao Li ·
Tiankai Hang ·
[**Jiale Tao**](https://scholar.google.com/citations?user=WF5DPWkAAAAJ&hl=en) · 
[**QiXun Wang**](https://github.com/wangqixun) · 
[**Ruihuang Li**](https://scholar.google.com/citations?user=8CfyOtQAAAAJ&hl=en) · 
Comi Chen ·
Xin Li · 
[**Mingrui Wu**](https://scholar.google.com/citations?user=sbCKwnYAAAAJ&hl=en) · 
Xinchi Deng · 
Shuyang Gu · 
[**Chunyu Wang**](https://scholar.google.com/citations?user=VXQV5xwAAAAJ&hl=en)<sup>†</sup> · 
[**Qinglin Lu**](https://luqinglin.weebly.com/)<sup>*</sup>

Tencent Hunyuan

<sup>†</sup>Project Lead · <sup>*</sup>Corresponding Author

</div>

<p align="center">
  <a href="https://www.arxiv.org/abs/2509.04545"><img src="https://img.shields.io/badge/Paper-arXiv:2509.04545-red?logo=arxiv" alt="arXiv"></a>
  <a href="https://zhuanlan.zhihu.com/p/1949013083109459515"><img src="https://img.shields.io/badge/知乎-技术解读-0084ff?logo=zhihu" alt="Zhihu"></a>
  <a href="https://huggingface.co/tencent/HunyuanImage-2.1/tree/main/reprompt"><img src="https://img.shields.io/badge/Model-PromptEnhancer_7B-blue?logo=huggingface" alt="HuggingFace Model"></a>
  <!-- <a href="https://huggingface.co/PromptEnhancer/PromptEnhancer-32B"><img src="https://img.shields.io/badge/Model-PromptEnhancer_32B-blue?logo=huggingface" alt="HuggingFace Model"></a> -->
  <a href="https://huggingface.co/datasets/PromptEnhancer/T2I-Keypoints-Eval"><img src="https://img.shields.io/badge/Benchmark-T2I_Keypoints_Eval-blue?logo=huggingface" alt="T2I-Keypoints-Eval Dataset"></a>
  <a href="https://hunyuan-promptenhancer.github.io/"><img src="https://img.shields.io/badge/Homepage-PromptEnhancer-1abc9c?logo=homeassistant&logoColor=white" alt="Homepage"></a>
  <a href="https://github.com/Tencent-Hunyuan/HunyuanImage-2.1"><img src="https://img.shields.io/badge/Code-HunyuanImage2.1-2ecc71?logo=github" alt="HunyuanImage2.1 Code"></a>
  <a href="https://huggingface.co/tencent/HunyuanImage-2.1"><img src="https://img.shields.io/badge/Model-HunyuanImage2.1-3498db?logo=huggingface" alt="HunyuanImage2.1 Model"></a>
  <a href=https://x.com/TencentHunyuan target="_blank"><img src=https://img.shields.io/badge/Hunyuan-black.svg?logo=x height=22px></a>
</p>

---

<p align="center">
  <img src="assets/teaser-1.png" alt="PromptEnhancer Teaser"/>
</p>

## Overview

Hunyuan-PromptEnhancer is a prompt rewriting utility. It restructures an input prompt while preserving the original intent, producing clearer, layered, and logically consistent prompts suitable for downstream image generation or similar tasks.

- Preserves intent across key elements (subject/action/quantity/style/layout/relations/attributes/text, etc.).
- Encourages a "global–details–summary" narrative, describing primary elements first, then secondary/background elements, ending with a concise style/type summary.
- Robust output parsing with graceful fallback: prioritizes `<answer>...</answer>`; if missing, removes `<think>...</think>` and extracts clean text; otherwise falls back to the original input.
- Configurable inference parameters (temperature, top_p, max_new_tokens) for balancing determinism and diversity.

## 🔥🔥🔥Updates

- [2025-09-22] 🚀 Thanks @mradermacher for adding **GGUF model support** for efficient inference with quantized models!
- [2025-09-18] ✨ Try the [PromptEnhancer-32B](https://huggingface.co/PromptEnhancer/PromptEnhancer-32B) for higher-quality prompt enhancement!
- [2025-09-16] Release [T2I-Keypoints-Eval dataset](https://huggingface.co/datasets/PromptEnhancer/T2I-Keypoints-Eval).
- [2025-09-07] Release [PromptEnhancer-7B model](https://huggingface.co/tencent/HunyuanImage-2.1/tree/main/reprompt).
- [2025-09-07] Release [technical report](https://arxiv.org/abs/2509.04545).

## Installation

### Standard Installation (Transformers)
```bash
pip install -r requirements.txt
```

### GGUF Installation (Quantized Models)
```bash
# Install with CUDA support for faster inference
chmod +x install_gguf.sh
./install_gguf.sh
```

## Model Download

### Standard Models
```bash
# for PromptEnhancer-7B model
huggingface-cli download tencent/HunyuanImage-2.1/reprompt --local-dir ./models/promptenhancer-7b

# for PromptEnhancer-32B model
huggingface-cli download PromptEnhancer/PromptEnhancer-32B --local-dir ./models/promptenhancer-32b
```

### GGUF Models (Quantized)
```bash
# Download Q8_0 quantized model (35GB, highest quality)
huggingface-cli download mradermacher/PromptEnhancer-32B-GGUF PromptEnhancer-32B.Q8_0.gguf --local-dir ./models

# Download Q6_K quantized model (27GB, excellent quality)
huggingface-cli download mradermacher/PromptEnhancer-32B-GGUF PromptEnhancer-32B.Q6_K.gguf --local-dir ./models

# Download Q4_K_M quantized model (20GB, good quality)
huggingface-cli download mradermacher/PromptEnhancer-32B-GGUF PromptEnhancer-32B.Q4_K_M.gguf --local-dir ./models
```

## Quickstart

### Using HunyuanPromptEnhancer

```python
from inference.prompt_enhancer import HunyuanPromptEnhancer

models_root_path = "./models/promptenhancer-7b"

enhancer = HunyuanPromptEnhancer(models_root_path=models_root_path, device_map="auto")

# Enhance a prompt (Chinese or English)
user_prompt = "Third-person view, a race car speeding on a city track..."
new_prompt = enhancer.predict(
    prompt_cot=user_prompt,
    # Default system prompt is tailored for image prompt rewriting; override if needed
    temperature=0.7,   # >0 enables sampling; 0 uses deterministic generation
    top_p=0.9,
    max_new_tokens=256,
)

print("Enhanced:", new_prompt)
```

### Using GGUF Models (Quantized, Faster)

```python
from inference.prompt_enhancer_gguf import PromptEnhancerGGUF

# Auto-detects Q8_0 model in models/ folder
enhancer = PromptEnhancerGGUF(
    model_path="./models/PromptEnhancer-32B.Q8_0.gguf",  # Optional: auto-detected
    n_ctx=1024,        # Context window size
    n_gpu_layers=-1,   # Use all GPU layers
)

# Enhance a prompt
user_prompt = "woman in jungle"
enhanced_prompt = enhancer.predict(
    user_prompt,
    temperature=0.3,
    top_p=0.9,
    max_new_tokens=512,
)

print("Enhanced:", enhanced_prompt)
```

### Command Line Usage (GGUF)

```bash
# Simple usage - auto-detects model in models/ folder
python inference/prompt_enhancer_gguf.py

# Or specify model path
GGUF_MODEL_PATH="./models/PromptEnhancer-32B.Q8_0.gguf" python inference/prompt_enhancer_gguf.py
```

## GGUF Model Benefits

🚀 **Why use GGUF models?**
- **Memory Efficient**: 50-75% less VRAM usage compared to full precision models
- **Faster Inference**: Optimized for CPU and GPU acceleration with llama.cpp
- **Quality Preserved**: Q8_0 and Q6_K maintain excellent output quality
- **Easy Deployment**: Single file format, no complex dependencies
- **GPU Acceleration**: Full CUDA support for high-performance inference

| Model | Size | Quality | VRAM Usage | Best For |
|-------|------|---------|------------|----------|
| Q8_0  | 35GB | Highest | ~35GB      | High-end GPUs (H100, A100) |
| Q6_K  | 27GB | Excellent | ~27GB     | RTX 4090, RTX 5090 |
| Q4_K_M| 20GB | Good    | ~20GB      | RTX 3090, RTX 4080 |

## Parameters

### Standard Models (Transformers)
- `models_root_path`: Local path or repo id; supports `trust_remote_code` models.
- `device_map`: Device mapping (default `auto`).
- `predict(...)`:
  - `prompt_cot` (str): Input prompt to rewrite.
  - `sys_prompt` (str): Optional system prompt; a default is provided for image prompt rewriting.
  - `temperature` (float): `>0` enables sampling; `0` for deterministic generation.
  - `top_p` (float): Nucleus sampling threshold (effective when sampling).
  - `max_new_tokens` (int): Maximum number of new tokens to generate.

### GGUF Models
- `model_path` (str): Path to GGUF model file (auto-detected if in models/ folder).
- `n_ctx` (int): Context window size (default: 8192, recommended: 1024 for short prompts).
- `n_gpu_layers` (int): Number of layers to offload to GPU (-1 for all layers).
- `verbose` (bool): Enable verbose logging from llama.cpp.

## Citation

If you find this project useful, please consider citing:
```bibtex
@article{promptenhancer,
  title={PromptEnhancer: A Simple Approach to Enhance Text-to-Image Models via Chain-of-Thought Prompt Rewriting},
  author={Wang, Linqing and Xing, Ximing and Cheng, Yiji and Zhao, Zhiyuan and Tao, Jiale and Wang, QiXun and Li, Ruihuang and Chen, Comi and Li, Xin and Wu, Mingrui and Deng, Xinchi and Wang, Chunyu and Lu, Qinglin},
  journal={arXiv preprint arXiv:2509.04545},
  year={2025}
}
```

## Acknowledgements

We would like to thank the following open-source projects and communities for their contributions to open research and exploration: [Transformers](https://huggingface.co/transformers) and [HuggingFace](https://huggingface.co).

## Contact

If you would like to leave a message for our R&D and product teams, Welcome to contact our open-source team. You can also contact us via email (hunyuan_opensource@tencent.com).

## Github Star History

[![Star History Chart](https://api.star-history.com/svg?repos=Hunyuan-PromptEnhancer/PromptEnhancer&type=Date)](https://www.star-history.com/#Hunyuan-PromptEnhancer/PromptEnhancer&Date)