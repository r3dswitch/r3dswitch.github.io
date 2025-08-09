### Franziska Boenisch

Franziska Boenisch is a tenure-track faculty member at the CISPA Helmholtz Center for Information Security, where she co-leads the SprintML lab, which focuses on Secure, Private, Robust, INterpretable, and Trustworthy Machine Learning.

**Memorisation in Foundation Models**

- History of memo in supervised learning
- Is memorisation overfitting? No in both directions.
- When memo happens? Mislabeled samples, Atypical samples, Under-represented samples
- A short tale about a long tail paper, Feldman 2020, Definition of memorisation, Leave one out style memo
- Memorisation influenced by dataset size, model capacity and data distribution

**Memorisation in self-supervised models**
- Alignment loss in SSL
- SSL memorisation
- SSL mem metric
- outliers experience high memorisation
- memorisation helps format the embedding space
- memorisation improves downstream generalisation

**Memorisation is multimodal(CLIPMem)**
- Measuring denoising trajectories to measure memo
- ssim and zscore for identifying memorisation
- localising memo
- coarse preselection followed by finegrained measurement on topk neurons
- few neurons responsible for memorisation

**Mitigation**
- removing neurons as empirical method for mitigating memo
- mitigating memo in diffusion models
