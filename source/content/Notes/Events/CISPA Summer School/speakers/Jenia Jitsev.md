### Jenia Jitsev

Jenia Jitsev is a computer scientist and neuroscientist. He is a co-founder and the scientific lead of LAION e.V., a German non-profit research organization focused on open science for large-scale foundation models and datasets. Jitsev also leads the Scalable Learning & Multi-Purpose AI (SLAMPAI) lab at the Jülich Supercomputing Centre of the Helmholtz Association in Germany.

**Open Foundation Models: Scaling Laws and Generalisation**

- Generic Transfer Learning

**Scaling Laws**
- DiT variants
- Scaling Law Derivation
- Discrepancy Kaplan vs Hoffmann
- Tune hyper parameters for each measurement
- Pre training procedure comparison
- Improving training sets leads to better models that are cheaper to train
- xLSTM not a scaling law paper

**Pipeline:**
- Dataset and Dataset Composition
- Training Procedure, Model Weights, Checkpoints
- Evaluation Benchmarks, Downstream Transfer Procedures

**Learning Procedure Comparison**
- CLIP vs MaMMUT
- Checking scaling law fit quality using holdout points on Pareto front, consistency checks

**How to test generalisation**
- Strong fluctuations across variations(Alice in Wonderland paper)
- Small models, severe collapse, large models, strong fluctuations
- Reasoning models still show strong fluctuations across variations

**Distributed Training, Scalable Code**
- SigLIP as good as CLIP the differentiation is in the closed data
