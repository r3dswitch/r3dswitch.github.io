### Probability & Graphical Models in Deep Learning
*   **Probability is foundational** for deep learning, providing the framework for models and training (e.g., cross-entropy error functions).
*   While some models like basic classifiers have simple probability structures (e.g., `p(t|x,w) = y^t (1-y)^(1-t)`), many advanced models (LLMs, VAEs, diffusion models, normalizing flows) have **richer probabilistic structures**.
*   **Probabilistic Graphical Models (PGMs)** are a powerful framework for describing and exploiting this structure, representing probability distributions as graphs.

---

### Graphical Models
*   **Purpose:** Visualize model structure, design new models, identify conditional independence properties, and express complex computations via graphical operations.
*   **Notation:** Red diagrams denote PGMs (vs. blue for neural networks).

####  Directed Graphs (Bayesian Networks)
*   **Structure:** Nodes = random variables. Edges (arrows) = probabilistic relationships.
*   **Decomposition:** The joint distribution decomposes into a product of conditional distributions, each depending only on a node's parents: `p(x1,...,xK) = ∏ p(xk | pa(k))`.
*   **Key Restriction:** Graphs must be **Directed Acyclic Graphs (DAGs)** (no directed cycles).

#### Representing Distributions
*   The graph's structure (which links are missing) conveys information by simplifying the joint distribution and reducing the number of parameters.
*   **Discrete Variables:** The number of parameters for a joint distribution grows exponentially with variables. Graphs reduce this by factoring the distribution and sharing parameters. **Parameterized conditional distributions** (e.g., using a sigmoid) can further reduce parameters.
*   **Linear-Gaussian Models:** If each node's conditional distribution is a Gaussian whose mean is a linear function of its parents, the **joint distribution is a multivariate Gaussian**. The graph structure imposes constraints on the covariance matrix.

#### Model Components & Inference
*   **Plates:** A box labelled with `N` represents a repetition of `N` identical nodes.
*   **Node Types:**
    *   Open Red Circle: Unobserved (latent/hidden) stochastic variable.
    *   Shaded Red Circle: Observed stochastic variable.
    *   Floating Variable: Deterministic parameter.
*   **Bayesian Inference:** The process of updating beliefs (posterior distributions) about unobserved variables after observing others. Graphically, observing a variable (shading a node) changes the flow of information and dependencies.

---

### Conditional Independence
*   **Definition:** `a` is conditionally independent of `b` given `c` if `p(a|b,c) = p(a|c)`. Shorthand: `a ⊥⊥ b | c`.
*   **D-separation** is the criterion for reading conditional independence properties directly from a directed graph.
    *   A path is **blocked** if it contains a node where:
        1.  Arrows meet **head-to-tail** or **tail-to-tail**, and the node is in the conditioning set `C`.
        2.  Arrows meet **head-to-head**, and **neither the node nor any of its descendants** is in the conditioning set `C`.
    *   If **all paths** between sets `A` and `B` are blocked by set `C`, then `A` and `B` are d-separated and `A ⊥⊥ B | C`.

#### Key Three-Node Examples:
*   **Tail-to-Tail (Fig 11.14):** `a` and `b` are dependent. Conditioning on `c` makes them independent.
*   **Head-to-Tail (Fig 11.16):** `a` and `b` are dependent. Conditioning on `c` makes them independent.
*   **Head-to-Head (Collider) (Fig 11.18):** `a` and `b` are **independent**. Conditioning on `c` (or any of its descendants) **makes them dependent**. This is called **explaining away**.

#### Applications:
*   **Naive Bayes:** A classifier that assumes input features are conditionally independent given the class label. While a strong assumption, it can be effective.
*   **Generative Models:** Model the causal process that generates the data (e.g., object class → position → image). Latent variables need not have a physical interpretation but allow building complex distributions from simple components.
*   **Markov Blanket:** For a node `xi`, the minimal set of nodes that makes it conditionally independent of all others is its **parents, children, and co-parents** (other parents of its children).

#### Graphs as Filters:
A graph defines a family of distributions `DF` that factorize according to its structure. The d-separation theorem states this is exactly the same set of distributions that obey all the conditional independence properties implied by the graph.

---

### Sequence Models
*   **Goal:** Model data with sequential structure (text, audio, time series).
*   **Autoregressive Model (General):** `p(x1,...,xN) = ∏ p(xn | x1,...,xn-1)`. This is fully general but has no simplifying assumptions.
*   **Markov Assumption:** Simplify by assuming limited dependence on the past.
    *   **M-th Order Markov:** `p(xn | x1,...,xn-1) = p(xn | xn-M,...,xn-1)`.
    *   Problem: Number of parameters grows exponentially with `M`.
*   **State-Space Model (Solution):** Introduce latent variables `z` that form a Markov chain. The observed sequence `x` is then generated from these states.
    *   **Joint Distribution:** `p(x1,...,xN, z1,...,zN) = p(z1) [∏ p(zn|zn-1)] [∏ p(xn|zn)]`.
    *   This structure allows the observed variables to have complex dependencies while keeping the number of parameters manageable.
    *   **Examples:** Hidden Markov Models (discrete `z`), Linear Dynamical Systems/Kalman Filters (Gaussian `z` and `x`). These can be made more powerful by using neural networks for the conditional distributions.