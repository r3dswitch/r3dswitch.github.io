### **1. Types of Uncertainty**
- **Aleatoric**: Inherent randomness (e.g., noise in data).
- **Epistemic**: Due to lack of knowledge (reducible with more data).

### **2. Probability Rules**
- **Sum Rule**: \( P(X) = \sum_Y P(X, Y) \) (marginalization).
- **Product Rule**: \( P(X, Y) = P(X | Y) P(Y) \) (joint probability).
- **Bayes’ Theorem**: \( P(Y | X) = \frac{P(X | Y) P(Y)}{P(X)} \).

### **3. Independence**
- \( X \) and \( Y \) are independent if \( P(X, Y) = P(X)P(Y) \).

### **4. Distributions**
- **Proper**: Integrates to 1 (valid PDF/PMF).
- **Improper**: Does not integrate to 1 (e.g., uniform over \(\mathbb{R}\)).
- **Uniform**: Equal probability over \(\[a, b]\).
- **Exponential**: \( p(x) = \lambda e^{-\lambda x} \) (time between events).
- **Laplace**: Double-exponential, \( p(x) = \frac{1}{2b} e^{-|x - \mu|/b} \).
- **Empirical**: Derived from observed data frequencies.
- **Dirac Delta**: \(\delta(x)\) is a spike at 0; integrates to 1.

### **5. Expectations**
- **Discrete**: \( \mathbb{E}\[X] = \sum_x x P(x) \).
- **Continuous**: \( \mathbb{E}\[X] = \int x p(x) dx \).
- **Approximation**: Monte Carlo: \( \frac{1}{N} \sum_i f(x_i) \).
- **Conditional**: \( \mathbb{E}\[X | Y] \) averages \( X \) given \( Y \).

### **6. Variance & Covariance**
- **Variance**: \( \text{Var}(X) = \mathbb{E}\[(X - \mu)^2] \).
- **Covariance**: \( \text{Cov}(X, Y) = \mathbb{E}\[(X - \mu_X)(Y - \mu_Y)] \).

### **7. Gaussian (Normal) Distribution**
- PDF: \( p(x) = \frac{1}{\sqrt{2\pi \sigma^2}} e^{-(x - \mu)^2 / 2\sigma^2} \).
- **Multivariate**: \( \mathcal{N}(\mathbf{\mu}, \mathbf{\Sigma}) \), covariance matrix \( \mathbf{\Sigma} \).
- Properties: Closed under linear transforms, max entropy for given variance.

### **8. Likelihood & Estimation**
- **Likelihood**: \( L(\theta) = P(D | \theta) \) (not a probability).
- **MLE**: \( \hat{\theta} = \arg\max_\theta L(\theta) \).
- **Bias of MLE**: Asymptotically unbiased but may be biased for finite \( N \).
- **Unbiased Estimator**: \( \mathbb{E}\[\hat{\theta}] = \theta \).

### **9. Linear Regression**
- Models \( y = \mathbf{w}^T \mathbf{x} + \epsilon \).
- MLE/MSE solution: \( \mathbf{w} = (\mathbf{X}^T \mathbf{X})^{-1} \mathbf{X}^T \mathbf{y} \).

### **10. Density Transformations**
- **Univariate**: \( p_y(y) = p_x(x) \left| \frac{dx}{dy} \right| \).
- **Multivariate**: \( p_y(\mathbf{y}) = p_x(\mathbf{x}) \left| \det \mathbf{J} \right| \), Jacobian \( \mathbf{J} \).

### **11. Information Theory**
- **Entropy**: \( H(X) = -\sum P(x) \log P(x) \) (uncertainty).
- **Differential Entropy**: For continuous \( X \), \( H(X) = -\int p(x) \log p(x) dx \).
- **KL Divergence**: \( D_{KL}(P \| Q) = \sum P(x) \log \frac{P(x)}{Q(x)} \) (non-symmetric).
- **Conditional Entropy**: \( H(Y | X) = H(X, Y) - H(X) \).
- **Mutual Information**: \( I(X; Y) = H(X) - H(X | Y) \).

### **12. Convexity & Jensen’s Inequality**
- **Convex Function**: \( f(\lambda x + (1-\lambda)y) \leq \lambda f(x) + (1-\lambda)f(y) \).
- **Jensen’s Inequality**: For convex \( f \), \( f(\mathbb{E}\[X]) \leq \mathbb{E}\[f(X)] \).

### **13. MAP vs. MLE**
- **MLE**: Maximizes \( P(D | \theta) \) (data-driven).
- **MAP**: Maximizes \( P(\theta | D) \propto P(D | \theta) P(\theta) \) (includes prior).

---

**Key Themes**:  
- Probability rules form the foundation for inference.  
- Distributions model data, Gaussians are central.  
- Information theory quantifies uncertainty and relationships.  
- Estimation (MLE/MAP) balances data and prior beliefs.  