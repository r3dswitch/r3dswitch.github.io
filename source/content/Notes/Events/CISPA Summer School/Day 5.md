### Mathias Lecuyer

Mathias Lécuyer is an assistant professor at the University of British Columbia in Vancouver. He is a member of several research groups, including Systopia, UBC S&P, TrustML, and CAIDA. Before his position at UBC, he was a postdoctoral researcher at Microsoft Research in New York and earned his PhD from Columbia University.

**f-DP**
- DP as a bound on hypothesis test's power
- Key Properties of f-DP:
    - Gaussian Mechanism
    - Post processing still f-DP
    - Composition
- Power of adversary as a bound between norm 2 and norm infinity

**Robustness**
- How to make models robust with guarantees?
- Proving robustness using f-DP type 2 errors using hypothesis testing
- Problems(Randomised Smoothing): noise degrades accuracy, difficulty scaling
- Solution: Adaptive Randomised Smoothing
- Provable input adaptive adversarial robustness with adaptive randomised smoothing
- DP Guided Diffusion Denoising

**Data Leakage**
- Measuring data leakage without access to out-of-distribution data with panorama
- Lee-Luda Chatbot
- Memorisation big problem

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
