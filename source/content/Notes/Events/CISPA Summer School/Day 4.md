
### Antti Honkela

Privacy Accounting for DP-SGD
k-fold adaptive compositions in approximate DP
Numerical Accounting
Formalising Privacy Accounting
Releasing just the final model not gradients?
Transfer Learning and High Utility Model
DP CV with pre training on public data
DP Text Generation with pre-training on public data
DP few shot learning by finetuning
Transfer Difficulty (TD) a big factor between datasets
Which classes to fine tune?
Data cost of DP training
Fine tuning caveats (public pre training public fine tuning)
DP-SGD and Hyperparameters (Clipping Threshold, Noise Magnitude)
Subsampling Amplification
Clipping hurts accuracy of difficult classes while improving accuracy of easy classes
Even adaptive clipping is susceptible to this
Excessive MIA(membership inference attack) vulnerability of HPO(hyper parameter tuning)
DP Optimisation Algorithms(DP-SGD, DP-Adam, DP-FTRL)
Correlated Noise Mechanisms
Software for DP Deep Learning(Opacus, JAX handle better, Ghost Clipping and Book Keeping, Random Sampling still a problem(JAX, uses JIT compilation))
Benchmarking frameworks, Beltran et al 2024
Opacus, FastDP, JAX-Privacy, JaxDPopt
Auditing and attacking DP-SGD

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

### Joaquin Vanschoren

Joaquin Vanschoren is an Associate Professor of Machine Learning at the Eindhoven University of Technology (TU/e). His research is focused on understanding machine learning algorithms to create more automated and efficient AI systems. He is the founder of OpenML.org, an open science platform for sharing datasets, code, and experiments to make machine learning research more collaborative and reproducible.

**Measuring AI Safety**
- MIT AI Risk Database
- GP-AI models with Systemic Risk
- EU AI Act
- Code of Practice
- Paradigms of AI Evaluation Paper

**AI Safety Evaluation Frameworks**
- AISI Inspect
- HELM Leaderboards

**Problems with AI Eval**
- AI Capability Evaluation Framework
- AdeLe(Annotated Demand Levels)
- Sandbagging
- Observational Scaling Laws

**Capability vs Risk**
- AI Luminate, Inspect AI, LM Eval Harness, Safety Prompts
- Purple LLAMA, Frontier Safety Framework
- Make me pay, alignment faking
