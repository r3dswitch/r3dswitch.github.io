- **Purpose**: Foundational probability distributions serve as building blocks for more complex models in machine learning.
- **Density Estimation**: The task of modeling the probability distribution from observed data. This is inherently ambiguous because many distributions can fit the same data.

---

### **3.1 Discrete Variables**
#### **Bernoulli Distribution**
- Models binary outcomes (e.g., coin flips).
- Defined by a single parameter representing the probability of success.
- Mean and variance are derived directly from this parameter.
- Maximum likelihood estimation for the parameter simplifies to the fraction of observed successes.

#### **Binomial Distribution**
- Extends Bernoulli to count the number of successes in multiple independent trials.
- Shape depends on the number of trials and success probability.
- For many trials, the distribution approximates a Gaussian (Central Limit Theorem).

#### **Multinomial Distribution**
- Generalizes Bernoulli to multiple categories (e.g., dice rolls).
- Each category has its own probability, and the distribution tracks counts across categories.
- Maximum likelihood estimates for probabilities are the observed frequencies.
- The joint distribution of counts across categories is the multinomial distribution.

---

### **3.2 The Multivariate Gaussian**
#### **Definition and Geometry**
- A bell-shaped distribution for continuous vectors, parameterized by a mean vector and covariance matrix.
- Contours of constant probability form ellipsoids whose orientation and scale are determined by the covariance matrix.
- The "spread" in any direction is governed by the eigenvalues of the covariance matrix.

#### **Properties**
- The mean vector centers the distribution.
- The covariance matrix controls the shape and correlations between dimensions.
- The distribution’s symmetry and exponential decay lead to tractable computations.

#### **Limitations**
1. **Complexity**: The full covariance matrix requires many parameters (grows quadratically with dimensionality).
   - Simplified versions (diagonal or isotropic covariance) reduce parameters but limit flexibility.
2. **Unimodality**: Cannot naturally represent data with multiple "clusters."
3. **Solutions**:
   - **Latent Variables**: Introduce hidden variables to model complex structure (e.g., mixtures of Gaussians).
   - **Nonparametric Methods**: Adapt to data structure without fixed parameters but may scale poorly.

### **Conditional Distribution**
- **Key Idea**: If two subsets of variables \(\mathbf{x}_a\) and \(\mathbf{x}_b\) are jointly Gaussian, their conditional distribution \(p(\mathbf{x}_a | \mathbf{x}_b)\) is also Gaussian.
- **Properties**:
  - The conditional mean is a **linear function** of \(\mathbf{x}_b\).
  - The conditional covariance is **independent** of \(\mathbf{x}_b\).
- **Precision Matrix**: Simpler expressions arise when using the partitioned precision matrix (inverse covariance) rather than the covariance matrix.

### **Marginal Distribution**
- **Key Idea**: The marginal distribution \(p(\mathbf{x}_a)\) of a partitioned Gaussian is also Gaussian.
- **Properties**:
  - The marginal mean and covariance are directly extracted from the corresponding partitions of the joint mean and covariance matrix.
  - Unlike the conditional distribution, the marginal depends only on the covariance matrix, not the precision matrix.

### **Bayes’ Theorem for Gaussian Variables**
- **Linear-Gaussian Model**: When a Gaussian prior \(p(\mathbf{x})\) and a Gaussian likelihood \(p(\mathbf{y}|\mathbf{x})\) (with linear mean and constant covariance) are combined:
  - The marginal \(p(\mathbf{y})\) is Gaussian.
  - The posterior \(p(\mathbf{x}|\mathbf{y})\) is Gaussian, with mean and covariance depending on both prior and likelihood.
- **Interpretation**: The posterior is a "weighted average" of prior knowledge and observed data.

### **Maximum Likelihood for Gaussians**
- **Estimation**:
  - **Mean**: The MLE is the sample mean (average of observed data points).
  - **Covariance**: The MLE is the sample covariance, but it is **biased** (underestimates true covariance). An unbiased estimator divides by \(N-1\) instead of \(N\).
- **Sufficient Statistics**: The likelihood depends only on the sum of data points (\(\sum \mathbf{x}_n\)) and their outer products (\(\sum \mathbf{x}_n \mathbf{x}_n^T\)).

### **Sequential Estimation**
- **Online Updates**: For streaming data, the mean can be updated incrementally:
  - New estimate = Old estimate + (Step size) × (Error between new data point and old estimate).
  - Useful for large datasets or real-time applications.

### **Mixtures of Gaussians**
- **Motivation**: A single Gaussian is often too limited (e.g., cannot model multi-modal data like the "Old Faithful" dataset).
- **Mixture Model**:
  - A weighted sum of \(K\) Gaussians, each with its own mean and covariance.
  - Mixing coefficients \(\pi_k\) act as probabilities (sum to 1, non-negative).
- **Interpretation**:
  - Each component represents a "cluster" in the data.
  - Responsibilities \(\gamma_k(\mathbf{x})\) quantify how much each component explains a given data point (posterior probability of component \(k\) given \(\mathbf{x}\)).
- **Learning**: Maximum likelihood is complex (no closed-form solution). The **Expectation-Maximization (EM)** algorithm is typically used to iteratively estimate parameters.

---

### **Periodic Variables**
- **Challenge**: Standard distributions (e.g., Gaussian) are ill-suited for periodic data (e.g., wind direction, time of day) because their results depend arbitrarily on the choice of origin.
- **Example**: For two angles near 0° and 360°, a Gaussian’s mean and variance change drastically if the origin is shifted.

### **Von Mises Distribution**
- **Purpose**: A periodic analog of the Gaussian, invariant to the choice of origin.
- **Key Idea**: Represent angles as points on a unit circle in 2D space and compute statistics in Cartesian coordinates.
  - The **mean direction** is found by averaging the 2D unit vectors and converting back to an angle.
  - The **concentration parameter** (like inverse variance) controls how tightly the distribution clusters around the mean.

#### **Properties**:
1. **Periodicity**: Naturally enforces \( p(\theta) = p(\theta + 2\pi) \).
2. **Unimodal**: Peaks at a single preferred direction (the mean).
3. **Normalization**: Uses a Bessel function for the normalization constant.
4. **Gaussian Approximation**: For high concentration, it resembles a Gaussian.

#### **Parameter Estimation**:
- **Mean Direction**: Computed from the arctangent of the average sine and cosine components of the data.
- **Concentration**: Estimated by solving a transcendental equation involving Bessel functions.

#### **Limitations**:
- **Unimodality**: Cannot model multi-modal periodic data (e.g., two dominant wind directions). Mixtures of von Mises distributions can address this.
- **Alternatives**: 
  - **Histograms**: Simple but lack smoothness and scalability.
  - **Wrapped Distributions**: Created by "wrapping" a Gaussian around the circle, but more complex to work with.

---

### **Exponential Family Overview**
The exponential family is a broad class of probability distributions that share common mathematical properties and can be expressed in a standardized form. Many distributions (e.g., Bernoulli, Gaussian, Multinomial) are special cases of this family.

#### **Key Components**:
1. **General Form**:
   - A distribution in the exponential family can be written in terms of:
     - **Natural parameters** (\(\eta\)): Control the shape of the distribution.
     - **Sufficient statistic** (\(u(x)\)): A function of the data that captures all information needed for estimation.
     - **Base measure** (\(h(x)\)): A scaling factor independent of parameters.
     - **Normalization term** (\(g(\eta)\)): Ensures the distribution integrates to 1.

2. **Examples**:
   - **Bernoulli**: The natural parameter is the log-odds of success, and the sufficient statistic is the observation itself.
   - **Multinomial**: The natural parameters are log-transformed probabilities, and the sufficient statistic is the one-hot encoded vector of observations.
   - **Gaussian**: The natural parameters combine the mean and precision, and the sufficient statistics are the data and its square.

#### **Properties**:
1. **Sufficient Statistics**:
   - For maximum likelihood estimation, only the sum of the sufficient statistics over the dataset is needed (e.g., sum of observations for Bernoulli, sum and sum of squares for Gaussian).
   - This reduces storage requirements and simplifies computation.

2. **Moment Estimation**:
   - Moments (mean, variance, etc.) of the sufficient statistic can be obtained by differentiating the log-normalizer \(\ln g(\eta)\).
   - For example, the expected value of \(u(x)\) is given by the gradient of \(\ln g(\eta)\).

3. **Maximum Likelihood Estimation**:
   - The MLE for \(\eta\) depends only on the average of the sufficient statistics over the data.
   - As the dataset grows, the MLE converges to the true parameter value.

#### **Special Cases and Extensions**:
- **Softmax Parameterization (Multinomial)**:
  - To handle the constraint that probabilities sum to 1, the multinomial is reparameterized using \(M-1\) parameters, with the remaining probability derived via the softmax function.
- **Scaled Exponential Family**:
  - A variant introduces a shared scale parameter across classes while allowing class-specific natural parameters.

#### **Why It Matters**:
- **Unified Framework**: Provides a common structure for diverse distributions, simplifying theoretical analysis and algorithm design.
- **Efficient Estimation**: Sufficient statistics enable compact data representation and streamlined computation.
- **Generality**: Many models in machine learning (e.g., generalized linear models) leverage exponential family properties.

---

### **3.5 Nonparametric Methods**
#### **Limitations of Parametric Models**
- Parametric approaches (e.g., Gaussian, Bernoulli) assume a fixed functional form, which may poorly capture complex data structures (e.g., multimodality).  
- **Solution**: Nonparametric methods adapt flexibly to the data, making minimal assumptions about the underlying distribution.

---

### **3.5.1 Histograms**
- **Method**:  
  - Divide the data space into bins of width \(\Delta\) and count observations per bin.  
  - Normalize counts by total observations \(N\) and bin volume to estimate density.  
- **Pros**: Simple, computationally efficient (data can be discarded after binning).  
- **Cons**:  
  - Discontinuous estimates (artificial edges at bin boundaries).  
  - **Curse of dimensionality**: Requires exponentially more bins in higher dimensions (e.g., \(M^D\) for \(D\) dimensions).  
- **Trade-off**:  
  - Small \(\Delta\): Noisy, overfitted estimates.  
  - Large \(\Delta\): Oversmoothing, misses structure (e.g., bimodality).  

---

### **3.5.2 Kernel Density Estimation**
- **Method**:  
  - Place a **kernel** (e.g., Gaussian, uniform cube) around each data point.  
  - Sum kernel contributions and normalize to estimate density.  
  - **Smoothing parameter \(h\)**: Controls kernel width.  
- **Key Properties**:  
  - **Kernel requirements**: Non-negative, integrates to 1 (e.g., Gaussian, Epanechnikov).  
  - Smoother than histograms (no bin-edge discontinuities).  
- **Trade-off**:  
  - Small \(h\): High variance (noisy).  
  - Large \(h\): High bias (oversmoothing).  
- **Limitation**: Computationally expensive for large datasets (requires storing all data).  

---

### **3.5.3 \(K\)-Nearest Neighbors (KNN)**
- **Method**:  
  - Fix the number of neighbors \(K\) (instead of bin/kernel size).  
  - For a point \(x\), grow a sphere until it encloses \(K\) neighbors; estimate density as \(K/(N \times \text{sphere volume})\).  
- **Adaptive Smoothing**:  
  - Automatically adjusts locality: Small \(K\) in dense regions, large \(K\) in sparse regions.  
- **Classification Extension**:  
  - For a test point, assign the majority class among its \(K\) nearest neighbors.  
  - **Nearest-neighbor rule (\(K=1\))**: Asymptotically, error ≤ 2 × optimal classifier error.  
- **Limitations**:  
  - Not a true density model (integral diverges).  
  - Requires storing all training data; computationally intensive.  

---

### **Key Takeaways**
1. **Trade-offs**:  
   - **Histograms**: Simple but rigid; suffers in high dimensions.  
   - **Kernels**: Smooth but fixed bandwidth; computationally heavy.  
   - **KNN**: Adaptive but scales poorly with data size.  
2. **Model Complexity**:  
   - All methods require tuning a smoothing parameter (\(h\) or \(K\)), analogous to choosing polynomial degree in regression.  
3. **Dimensionality**:  
   - Nonparametric methods struggle in high dimensions due to sparsity of data (**curse of dimensionality**).  

---

### **Practical Considerations**
- **Storage vs. Flexibility**: Nonparametric methods retain all data, making them expensive for large datasets.  
- **Deep Learning**: Offers a middle ground—flexible models with fixed complexity, trained to capture data structure without storing raw data.  
