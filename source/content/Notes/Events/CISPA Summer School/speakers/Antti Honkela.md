# Antti Honkela

Antti Honkela is a Professor of Data Science, with a focus on Machine Learning and AI, at the University of Helsinki's Department of Computer Science. He is also the coordinating professor for the Research Programme in Privacy-preserving and Secure AI at the Finnish Center for Artificial Intelligence (FCAI).

## Day 3: Differential Privacy

**Differential Privacy Definitions:**
- Epsilon DP
- Epsilon delta DP
- Approximate DP
- Gaussian DP

**Properties of DP:**
- DP guarantees can't be made weaker by post processing
- DP Composition
- Group Privacy
- DP is a property of an algorithm not its output

**Mechanisms:**
- Randomised Response

**Design Choices for DP Implementations:**
- Def
- Relation
- Budget
- Mechanism

**Privacy Accounting for DP-SGD**

## Day 4: Advanced Topics in DP

**Privacy Accounting for DP-SGD:**
- k-fold adaptive compositions in approximate DP
- Numerical Accounting
- Formalising Privacy Accounting

**Transfer Learning and DP:**
- Releasing just the final model not gradients?
- Transfer Learning and High Utility Model
- DP CV with pre training on public data
- DP Text Generation with pre-training on public data
- DP few shot learning by finetuning
- Transfer Difficulty (TD) a big factor between datasets
- Which classes to fine tune?
- Data cost of DP training
- Fine tuning caveats (public pre training public fine tuning)

**DP-SGD and Hyperparameters:**
- Clipping Threshold, Noise Magnitude
- Subsampling Amplification
- Clipping hurts accuracy of difficult classes while improving accuracy of easy classes
- Even adaptive clipping is susceptible to this
- Excessive MIA(membership inference attack) vulnerability of HPO(hyper parameter tuning)

**DP Optimisation Algorithms:**
- DP-SGD, DP-Adam, DP-FTRL
- Correlated Noise Mechanisms

**Software for DP Deep Learning:**
- Opacus, JAX handle better, Ghost Clipping and Book Keeping, Random Sampling still a problem(JAX, uses JIT compilation)
- Benchmarking frameworks, Beltran et al 2024
- Opacus, FastDP, JAX-Privacy, JaxDPopt

**Auditing and attacking DP-SGD**
