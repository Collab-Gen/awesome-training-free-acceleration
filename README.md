# Awesome Training-Free Video Generation Acceleration

A curated survey of **training-free acceleration methods for video generation**, with an emphasis on video diffusion transformers (video DiTs), inference-time reuse, sparse computation, feature approximation, and token or resolution reduction.


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
