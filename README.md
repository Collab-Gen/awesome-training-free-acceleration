# **🚀 Awesome Training-Free Video Generation Acceleration**

A curated survey of **training-free acceleration methods for video generation**, 

with a focus on **video diffusion transformers (Video DiTs)**, inference-time 

optimization, feature reuse, sparse computation, and token/resolution reduction.


We categorize existing methods into three major directions:

- Feature cache and reuse
- Sparse attention and token reduction
- Progressive sampling and resolution scheduling


The survey mainly covers papers from **2024-2026** that explicitly target

training-free, inference-time acceleration for video diffusion models.



# **🚀 Quick Start**

- [Overview](#overview)

- [Feature Cache and Reuse](#1-feature-cache-and-reuse)

- [Sparse Attention and Token Reduction](#2-sparse-attention-and-token-reduction)

- [Progressive Sampling and Resolution Scheduling](#3-progressive-sampling-and-resolution-scheduling)




# **Overview**

The computational cost of video diffusion models mainly comes from:

1. Repeated denoising steps/blocks/CFG

2. Expensive spatial-temporal attention

3. Large video token sequences


Training-free acceleration methods aim to reduce inference cost without

modifying model parameters.



| Category | Core idea |
|---|---|
| Cache / Reuse | Avoid redundant computation by reusing or predicting intermediate features |
| Sparse Attention | Reduce attention cost by selecting important interactions |
| Progressive Sampling | Reduce intermediate computation through adaptive schedules |




# **1. Feature Cache and Reuse**

Feature reuse methods exploit the temporal redundancy of diffusion models.

Because adjacent denoising steps often produce similar intermediate features,

these methods reduce redundant computation by reusing historical states or

predicting future features based on previous feature evolution.


Different methods mainly differ in:

- what features are reused

- how reuse decisions are made

- whether features are directly reused or predicted

- how error accumulation is controlled



| Method | Year | Main Idea | Links |
|---|---:|---|---|
| PAB | 2024 | Pyramid attention broadcast with different reuse ranges for spatial, temporal and cross attention | [Paper](https://arxiv.org/abs/2408.12588) |
| FasterCache | 2024 | Feature reuse with compensation and CFG-cache to reduce redundant computation | [Paper](https://arxiv.org/abs/2410.19355) |
| TeaCache | 2024 | Estimate output variation using timestep embedding-modulated input differences | [Paper](https://arxiv.org/abs/2411.19108) |
| TaylorSeer | 2025 | Predict future diffusion features using Taylor expansion instead of directly reusing cached features | [Paper](https://arxiv.org/abs/2503.06923) |
| MagCache | 2025 | Magnitude-aware cache decision based on residual evolution | [Project](https://zehong-ma.github.io/MagCache/) |
| EasyCache | 2025 | Runtime adaptive caching without offline profiling | [Paper](https://arxiv.org/abs/2507.02860) |
| MixCache | 2025 | Hybrid caching across step, CFG and block levels | [Paper](https://arxiv.org/abs/2508.12691) |
| HyCa | 2026 | Feature-dimension adaptive caching using dynamic evolution modeling | [Project](https://darrenzheng303.github.io/HyCa.github.io/) |
| SeaCache | 2026 | Spectral evolution aware cache with frequency-domain filtering | [Paper](https://arxiv.org/abs/2602.18993) |
| PreciseCache | 2026 | Step-wise and block-wise precise feature skipping | [Paper](https://arxiv.org/abs/2603.00976) |




# **2. Sparse Attention and Token Reduction**

Video DiTs suffer from quadratic attention complexity because video tokens

grow rapidly with spatial resolution and temporal length.

Sparse methods reduce computation by identifying important token interactions,

attention blocks, or structured sparse patterns.



| Method | Year | Main Idea | Links |
|---|---:|---|---|
| Sparse VideoGen | 2025 | Spatial-temporal sparse attention heads for video DiTs | [Paper](https://arxiv.org/abs/2502.01776) |
| AdaSpa | 2025 | Dynamic sparse pattern search with adaptive block selection | [Paper](https://arxiv.org/abs/2502.21079) |
| XAttention | 2025 | Block importance estimation using antidiagonal scoring | [Paper](https://arxiv.org/abs/2503.16428) |
| GRAT | 2025 | Token grouping for GPU-friendly sparse attention | [Paper](https://arxiv.org/abs/2505.14687) |
| Sparse VideoGen2 | 2025 | Semantic-aware token permutation for efficient sparse attention | [Paper](https://arxiv.org/abs/2505.18875) |
| Radial Attention | 2025 | Distance-aware sparse attention with O(n log n) complexity | [Paper](https://arxiv.org/abs/2506.19852) |
| SVOO | 2026 | Offline sparsity profiling and online QK co-clustering | [Paper](https://arxiv.org/abs/2603.18636) |
| LVSA | 2026 | Structured sparse attention for long video diffusion | [Paper](https://arxiv.org/abs/2605.31057) |




# **3. Progressive Sampling and Resolution Scheduling**

These methods reduce computation by dynamically changing the inference

trajectory instead of accelerating individual transformer operations.


Typical strategies include:

- changing latent resolution during sampling

- allocating computation differently across denoising stages



| Method | Year | Main Idea | Links |
|---|---:|---|---|
| Bottleneck Sampling | 2025 | High-low-high resolution denoising pipeline using low-resolution priors | [Paper](https://arxiv.org/abs/2503.18940) |
| Jenga | 2025 | Dynamic token carving with progressive resolution generation | [Paper](https://arxiv.org/abs/2505.16864) |

