# Related Resources

This page records the positioning of this survey against nearby GitHub resources. It is not an exhaustive benchmark; it is meant to keep the scope of this repository clear.

## Closest Resources

### Awesome-Efficient-Video-Generation

Link: <https://github.com/NUS-HPC-AI-Lab/Awesome-Efficient-Video-Generation>

What it does:

- Maintains a broad list of efficient video generation methods.
- Covers multiple families such as autoregressive generation, attention methods, caching, distillation, token reduction, VAE optimization, quantization, and system-level topics.
- Tracks many recent papers quickly and is useful as a discovery index.

How this repository is positioned:

- Stay narrower: training-free acceleration for video generation, especially video DiT inference.
- Organize papers by stable method axes rather than by a broad topic list.
- Keep the main paper table compact enough to scan.

### Efficient-Diffusion-Models

Link: <https://github.com/TsinghuaC3I/Efficient-Diffusion-Models>

What it does:

- Hosts resources for a broad efficient diffusion model survey.
- Uses a survey-paper style structure with updates, introduction, table of contents, and part-wise paper organization.

How this repository is positioned:

- Focus on video-generation inference acceleration rather than the whole diffusion-model efficiency landscape.
- Separate training-free methods from distillation, fine-tuning, architecture redesign, and deployment-only optimization.

### Awesome-Diffusion-Models

Link: <https://github.com/diff-usion/Awesome-Diffusion-Models>

What it does:

- Maintains a broad diffusion-model paper collection with survey sections and dated entries.
- Works well as a general bibliography index.

How this repository is positioned:

- Provide a more compact and analytical table for one narrow topic.
- Prioritize a stable taxonomy over comprehensiveness.

### training-free-methods

Link: <https://github.com/littlewhitesea/training-free-methods>

What it does:

- Collects training-free algorithms for visual generation and manipulation.
- Includes many topics beyond acceleration, such as editing, control, style, watermarking, and generation guidance.

How this repository is positioned:

- Focus only on training-free acceleration.
- Use video generation as the primary model/application setting, not general visual generation.

## Display Lessons

Good survey repositories usually make these choices visible:

- A one-paragraph scope statement near the top.
- A taxonomy before the paper list.
- Paper tables with stable columns and short descriptions.
- Separate structured metadata for long-term maintenance.
- A related-resources page that clarifies what the repository is and is not trying to replace.

Those practices are reflected in this repository's README and `data/papers.yaml`.
