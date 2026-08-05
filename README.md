# Awesome Training-Free Video Generation Acceleration

A curated survey of **training-free acceleration methods for video generation**, with an emphasis on video diffusion transformers (video DiTs), test-time caching, sparse attention, feature forecasting, and progressive-resolution inference.

Last updated: 2026-08-05

## Scope

This project tracks methods that accelerate video generation without retraining or fine-tuning the base video generation model. A method is in scope when acceleration is mainly obtained at inference time through scheduling, reuse, sparsity, token/resolution reduction, solver approximation, or systems-level execution changes.

The current seed list focuses on:

- **Step or feature caching:** reuse attention outputs, residuals, transformer block outputs, or CFG branches across denoising steps.
- **Sparse attention:** reduce dense spatio-temporal attention by selecting important heads, tokens, or blocks.
- **Feature forecasting:** predict feature evolution instead of directly reusing stale cached features.
- **Progressive or low-resolution sampling:** reduce intermediate token counts during selected denoising stages.
- **Hardware-aware execution:** make the algorithmic saving visible in latency through layout, kernels, or distributed execution.

## Positioning

Existing efficient-video-generation lists are useful but broad: they often mix training-time methods, distillation, architecture design, deployment systems, and inference tricks. This repository is intended to be narrower and more analytic: the goal is to maintain a survey table that makes it easy to compare **what is reused or skipped, how the decision is made, what models are tested, and where the speed-quality risk appears**.

Related resources and differences are summarized in [docs/related-resources.md](docs/related-resources.md).

## Taxonomy

| Family | Main lever | Typical question | Representative entries |
|---|---|---|---|
| Caching / reuse | Skip repeated computation across denoising steps or CFG branches | What can be reused, when, and for how long? | PAB, FasterCache, TeaCache |
| Sparse attention | Avoid computing unimportant token or block interactions | Which attention blocks are important enough to keep? | Sparse VideoGen, AdaSpa, XAttention, GRAT |
| Forecasting | Approximate future features from prior feature trajectories | Can we predict instead of merely copy? | TaylorSeer |
| Progressive resolution | Reduce intermediate latent/token resolution | Which stages really need full resolution? | Bottleneck Sampling, Jenga |
| Hybrid pipeline | Combine multiple orthogonal acceleration levers | Which savings multiply without compounding quality loss? | Jenga |

## Papers

This initial version only includes the first ten papers from the seed reading list. More entries will be added after the display format is validated.

| # | Method | Year | Family | Main idea | Links |
|---|---|---:|---|---|---|
| 1 | PAB | 2024 | Caching / attention broadcast | Broadcast attention outputs with different reuse ranges for spatial, temporal, and cross attention. | [paper](https://arxiv.org/abs/2408.12588), [code](https://github.com/NUS-HPC-AI-Lab/VideoSys) |
| 2 | FasterCache | 2024 | Feature reuse + CFG cache | Reuse adjacent-step features while compensating feature differences, and exploit conditional/unconditional CFG redundancy. | [paper](https://arxiv.org/abs/2410.19355), [code](https://github.com/Vchitect/FasterCache) |
| 3 | TeaCache | 2024 | Adaptive caching | Use timestep-embedding-modulated input differences as a cheap proxy for output changes. | [paper](https://arxiv.org/abs/2411.19108), [code](https://github.com/ali-vilab/TeaCache) |
| 4 | Sparse VideoGen | 2025 | Sparse attention | Identify spatial and temporal sparse attention heads in video DiTs and compute only important interactions. | [paper](https://arxiv.org/abs/2502.01776), [code](https://github.com/svg-project/Sparse-VideoGen) |
| 5 | AdaSpa | 2025 | Adaptive sparse attention | Search dynamic block-sparse patterns online with LSE caching and head-adaptive sparsity. | [paper](https://arxiv.org/abs/2502.21079), [CVF](https://openaccess.thecvf.com/content/ICCV2025/html/Xia_Training-free_and_Adaptive_Sparse_Attention_for_Efficient_Long_Video_Generation_ICCV_2025_paper.html) |
| 6 | TaylorSeer | 2025 | Feature forecasting | Predict future diffusion features with Taylor-style extrapolation instead of directly reusing cached features. | [paper](https://arxiv.org/abs/2503.06923), [code](https://github.com/Shenyi-Z/TaylorSeer) |
| 7 | XAttention | 2025 | Block-sparse attention | Score attention blocks using antidiagonal sums as a lightweight proxy for block importance. | [paper](https://arxiv.org/abs/2503.16428), [code](https://github.com/mit-han-lab/x-attention) |
| 8 | Bottleneck Sampling | 2025 | Progressive resolution | Use a high-low-high denoising workflow to exploit low-resolution priors and reduce intermediate computation. | [paper](https://arxiv.org/abs/2503.18940), [code](https://github.com/tyfeld/Bottleneck-Sampling) |
| 9 | GRAT | 2025 | Hardware-aware sparse attention | Group tokens before attention so sparse computation better matches GPU-friendly memory and kernel behavior. | [paper](https://arxiv.org/abs/2505.14687), [code](https://github.com/OliverRensu/GRAT), [project](https://oliverrensu.github.io/project/GRAT/) |
| 10 | Jenga | 2025 | Sparse attention + progressive resolution | Combine dynamic token carving with progressive-resolution generation for video DiT inference. | [paper](https://arxiv.org/abs/2505.16864), [code](https://github.com/JIA-Lab-research/Jenga) |

## Comparison Fields To Maintain

Each paper entry should eventually include:

- target model family
- training-free assumption and required calibration
- accelerated module or stage
- decision signal for caching/sparsity/resolution changes
- reported speedup and hardware
- quality metrics and observed failure modes
- implementation dependency, such as custom kernels or layout transforms

Structured metadata for the current entries is maintained in [data/papers.yaml](data/papers.yaml).

## Contribution Format

New entries should preserve the survey focus: do not add a paper only because it is about video generation or diffusion efficiency. The entry should make clear whether the acceleration is truly training-free for the base video model and what inference-time mechanism produces the speedup.
