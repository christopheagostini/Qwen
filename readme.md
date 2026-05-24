Qwen3-0.6B for llama.cpp-mblt

cat Qwen_?? > Qwen3.tar.gz


Pre-packaged bundle of Qwen3-0.6B for use with llama.cpp-mblt on Mobilint Regulus NPUs.

The transformer forward pass runs entirely on the NPU (.mxq body); the CPU handles tokenization, embedding lookup, chat templating, and sampling via llama.cpp.
Quickstart

# Auto-download and run
llama-cli-mblt -hf mobilint/Qwen3-0.6B-GGUF

# Or from a local directory
llama-cli-mblt -M /path/to/Qwen3-0.6B-GGUF

Works with every tool in the llama.cpp-mblt suite:
Tool 	Purpose
llama-cli-mblt 	Interactive chat / single-prompt CLI
llama-simple-mblt 	Minimal text generation
llama-server-mblt 	OpenAI-compatible HTTP server
llama-bench-mblt 	Prefill + decode throughput benchmark
llama-perplexity-mblt 	Perplexity on a text corpus
llama-compare-mblt 	Output comparison (KL divergence + cosine)
Contents
File 	Purpose
Qwen3-0.6B-W8.mxq 	Pre-compiled NPU model (W8 quantized, Single-IO, Regulus single-core)
qwen3-0.6b-vocab.gguf 	Vocab-only GGUF (tokenizer + chat template)
target_emb.bin 	Input embedding matrix (float32, shape [vocab=151936, hidden=1024])
config.json 	Model geometry (hidden_size, layers, RoPE θ, etc.)
proxy_qwen3.py 	Optional HF transformers proxy class
README.md 	This file
Format

    Model format: Single-IO (input: embeddings; output: logits). RoPE and attention masks are baked into the MXQ.
    Core mode: single (Regulus has 1 cluster × 1 local core).
    Quantization: W8 (8-bit weights).
    EAGLE3: Not supported for Qwen3 (Single-IO format).
    Context length: 16 384 tokens (per config.json).

Hardware & Software Requirements

    Mobilint Regulus NPU (e.g., regulus2 board)
    llama.cpp-mblt built against qbruntime ≥ v1.2.0 / regulus-release v3.4.0
    NPU driver installed on host (see docs.mobilint.com)

This bundle was prepared with regulus-release v3.4.0 (qbruntime v1.2.0).
Source Model

This is a quantized + NPU-compiled derivative of Qwen/Qwen3-0.6B. The original model is © Alibaba Cloud and is distributed under the Apache 2.0 license — see the upstream LICENSE for terms.

The unquantized Mobilint source model with .mxq + .safetensors is available at mobilint/Qwen3-0.6B; this repo is the llama.cpp-mblt-ready bundle.
