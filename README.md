# FlashAttention in Triton

This repository contains a Triton-based reimplementation and extension of the FlashAttention algorithm, originally proposed by Dao et al. (2022), as part of a final project for COS 484: Natural Language Processing at Princeton University. 

📄 [**Project Report: [Re] FlashAttention Three Years On**](https://github.com/Astoria-ni/FlashAttentionTriton/blob/main/COS484_Final_Paper.pdf)  
👤 Kia Ghods\*, Jishnu Roychoudhury\*, Addison Wu\*  
\*All authors contributed equally.

## Overview

FlashAttention is an IO-aware exact attention algorithm designed to optimize memory bandwidth bottlenecks in transformers. We implement the full forward and backward pass in [Triton](https://github.com/openai/triton), introduce pipelining and autotuning for further performance gains, and benchmark our kernel against naive PyTorch SDPA, the original CUDA implementation, and PyTorch's FlashAttention-2 backend.

We also extend our implementation to support **Multi-Query Attention (MQA)** — reducing memory and compute by sharing key/value tensors across heads — and provide benchmarking of FlashAttention-style MQA.

## Features

- Triton implementation of FlashAttention (fwd & bwd)
- Pipelined execution and autotuning for A100/H100 GPUs
- Benchmarks vs. PyTorch and CUDA baselines
- Next-token prediction with WikiText-103
- Multi-Query Attention (MQA) support and evaluation

## Results

Our Triton kernel achieves:
- Higher throughput than the original CUDA FlashAttention kernel
- Competitive performance with PyTorch’s scaled dot-product attention (FlashAttention-2 backend)
- Comparable validation perplexity to standard attention in language modeling on WikiText-103

## Setup

Install dependencies:
```bash
pip install -r requirements.txt
```
Ensure you’re running on an A100 or H100 GPU with [Triton](https://github.com/openai/triton) installed.

## Acknowledgments
- [Professor Tri Dao](https://tridao.me/) for clarifying discussions and the original algorithm
- [Alex Dremov](https://alexdremov.me/) for Triton tutorials
- Princeton’s Della cluster for computational resources
