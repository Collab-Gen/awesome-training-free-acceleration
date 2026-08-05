# Awesome Training-Free Video Generation Acceleration

A curated survey of **training-free acceleration methods for video generation**, with an emphasis on video diffusion transformers (video DiTs), inference-time reuse, sparse computation, feature approximation, and token or resolution reduction.

Last updated: 2026-08-05

## Scope

This project tracks methods that accelerate video generation without retraining or fine-tuning the base video generation model. A method is in scope when its main speedup comes from inference-time changes such as reusing intermediate computation, selecting sparse token interactions, approximating feature evolution, reducing token or latent resolution, or improving the execution path of an otherwise unchanged generator.

The scope is intentionally narrow. General video generation papers, architecture redesigns, distillation methods, quantization-only methods, and training-based compression methods are outside the core scope unless they also introduce a clearly separable training-free inference acceleration mechanism.

## Positioning

Existing efficient-video-generation lists are useful but broad: they often mix training-time methods, distillation, architecture design, deployment systems, and inference tricks. This repository is narrower: it treats training-free video-generation acceleration as its own slice and classifies each paper by stable method axes rather than by a changing set of paper batches.

Related resources and differences are summarized in [docs/related-resources.md](docs/related-resources.md).

## Method Axes

The taxonomy is organized as reusable axes. New papers can be added to the table without rewriting the surrounding survey structure. The same axis definitions are kept in [data/taxonomy.yaml](data/taxonomy.yaml) for later expansion.

### Acceleration Target

| Target | What is reduced | Typical examples |
|---|---|---|
| Denoising step path | Repeated computation across adjacent or selected timesteps | attention output broadcast, residual caching, step-adaptive cache |
| Attention computation | Dense spatio-temporal token interactions | head routing, block-sparse attention, token grouping |
| Feature evolution | Expensive exact feature recomputation | feature reuse, feature forecasting, solver-style approximation |
| Token or resolution budget | Number of tokens processed in selected stages | low-resolution intermediate sampling, token carving |
| Guidance or branch path | Duplicate conditional/unconditional computation | CFG branch reuse or cache |
| Execution path | Latency hidden behind memory layout, kernels, or communication | hardware-friendly layouts, custom kernels, distributed broadcast |

### Mechanism Family

| Family | Core idea | Typical risk |
|---|---|---|
| Cache / reuse | Reuse previously computed activations or outputs. | stale features may weaken motion or fine details |
| Sparse / select | Compute only important token, block, head, or branch interactions. | sparse pattern search may miss prompt-specific dependencies |
| Forecast / approximate | Predict or approximate future features instead of recomputing them exactly. | approximation error may accumulate across steps |
| Progressive budget | Change resolution or token budget during selected denoising stages. | detail recovery depends on when full resolution returns |
| Hybrid pipeline | Combine multiple acceleration levers. | interactions between levers may be model- or prompt-sensitive |

### Decision Signal

| Signal | What it uses | Example use |
|---|---|---|
| Fixed schedule | Hand-designed or profiled timestep ranges | broadcast or cache intervals |
| Runtime activation signal | Input, residual, magnitude, or feature change | adaptive cache trigger |
| Attention structure | QK scores, head behavior, block importance, token grouping | sparse attention pattern |
| Semantic or spatial structure | token position, semantic grouping, frame layout | token permutation or carving |
| Solver trajectory | historical feature trajectory across timesteps | feature forecasting |

## Papers

The table is append-only: new papers can be added as new rows while preserving the same taxonomy above.

| # | Method | Year | Family | Main idea | Links |
|---|---|---:|---|---|---|
| 1 | PAB | 2024 | Cache / reuse | Broadcast attention outputs with different reuse ranges for spatial, temporal, and cross attention. | [paper](https://arxiv.org/abs/2408.12588), [code](https://github.com/NUS-HPC-AI-Lab/VideoSys) |
| 2 | FasterCache | 2024 | Cache / reuse | Reuse adjacent-step features while compensating feature differences, and exploit conditional/unconditional CFG redundancy. | [paper](https://arxiv.org/abs/2410.19355), [code](https://github.com/Vchitect/FasterCache) |
| 3 | TeaCache | 2024 | Cache / reuse | Use timestep-embedding-modulated input differences as a cheap proxy for output changes. | [paper](https://arxiv.org/abs/2411.19108), [code](https://github.com/ali-vilab/TeaCache) |
| 4 | Sparse VideoGen | 2025 | Sparse / select | Identify spatial and temporal sparse attention heads in video DiTs and compute only important interactions. | [paper](https://arxiv.org/abs/2502.01776), [code](https://github.com/svg-project/Sparse-VideoGen) |
| 5 | AdaSpa | 2025 | Sparse / select | Search dynamic block-sparse patterns online with LSE caching and head-adaptive sparsity. | [paper](https://arxiv.org/abs/2502.21079), [CVF](https://openaccess.thecvf.com/content/ICCV2025/html/Xia_Training-free_and_Adaptive_Sparse_Attention_for_Efficient_Long_Video_Generation_ICCV_2025_paper.html) |
| 6 | TaylorSeer | 2025 | Forecast / approximate | Predict future diffusion features with Taylor-style extrapolation instead of directly reusing cached features. | [paper](https://arxiv.org/abs/2503.06923), [code](https://github.com/Shenyi-Z/TaylorSeer) |
| 7 | XAttention | 2025 | Sparse / select | Score attention blocks using antidiagonal sums as a lightweight proxy for block importance. | [paper](https://arxiv.org/abs/2503.16428), [code](https://github.com/mit-han-lab/x-attention) |
| 8 | Bottleneck Sampling | 2025 | Progressive budget | Use a high-low-high denoising workflow to exploit low-resolution priors and reduce intermediate computation. | [paper](https://arxiv.org/abs/2503.18940), [code](https://github.com/tyfeld/Bottleneck-Sampling) |
| 9 | GRAT | 2025 | Sparse / select | Group tokens before attention so sparse computation better matches GPU-friendly memory and kernel behavior. | [paper](https://arxiv.org/abs/2505.14687), [code](https://github.com/OliverRensu/GRAT), [project](https://oliverrensu.github.io/project/GRAT/) |
| 10 | Jenga | 2025 | Hybrid pipeline | Combine dynamic token carving with progressive-resolution generation for video DiT inference. | [paper](https://arxiv.org/abs/2505.16864), [code](https://github.com/JIA-Lab-research/Jenga) |
