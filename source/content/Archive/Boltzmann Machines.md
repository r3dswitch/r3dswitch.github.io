[https://www.youtube.com/watch?v=Y8cBT_Qt_fQ](YT_Video)

#### **1. Hopfield Networks & Energy Minimization**  
- **Binary Hopfield Networks** minimize an energy function:  
  \[
  E(\mathbf{x}) = -\frac{1}{2} \mathbf{x}^T W \mathbf{x}
  \]
  where \( \mathbf{x} \) is a binary state vector and \( W \) is a symmetric weight matrix.  
- **Continuous Hopfield Networks** approximate a probability distribution:  
  \[
  P(\mathbf{x}|W) = \frac{1}{Z(W)} \exp \left( \frac{1}{2} \mathbf{x}^T W \mathbf{x} \right)
  \]
  where \( Z(W) \) is the partition function.  

#### **2. Boltzmann Machines (Stochastic Hopfield Networks)**  
- **Activity Rule**: Neurons update stochastically:  
  \[
  x_i = +1 \text{ with probability } \frac{1}{1 + e^{-2a_i}}, \text{ else } x_i = -1
  \]
  where \( a_i \) is the activation.  
- **Learning Rule**: Adjust weights \( W \) to maximize the likelihood of observed data \( \{\mathbf{x}^{(n)}\} \).  
  - **Gradient of Log-Likelihood**:  
    \[
    \frac{\partial}{\partial w_{ij}} \ln P(\{\mathbf{x}^{(n)}\}|W) = \langle x_i x_j \rangle_{\text{Data}} - \langle x_i x_j \rangle_{P(\mathbf{x}|W)}
    \]
    - **First Term**: Empirical correlation in the data.  
    - **Second Term**: Model correlation (estimated via Gibbs sampling).  

#### **3. Limitations of Simple Boltzmann Machines**  
- **Second-Order Statistics Only**: Simple models only capture pairwise correlations, missing higher-order structure (e.g., images of chairs).  
- **Example: Shifter Ensembles**  
  - **Plain Shifter**: Pixels shifted left/right (second-order stats useless).  
  - **Labelled Shifter**: Extra neurons label shifts, but still not learnable with pairwise correlations alone.  

#### **4. Boltzmann Machines with Hidden Units**  
- **Solution**: Introduce hidden neurons to model higher-order dependencies indirectly.  
- **Likelihood with Hidden Variables**:  
  \[
  P(\mathbf{x}^{(n)}|W) = \sum_{\mathbf{h}} P(\mathbf{x}^{(n)}, \mathbf{h}|W)
  \]
- **Learning Rule**:  
  \[
  \frac{\partial}{\partial w_{ij}} \ln P(\{\mathbf{x}^{(n)}\}|W) = \langle y_i y_j \rangle_{P(\mathbf{h}|\mathbf{x}^{(n)},W)} - \langle y_i y_j \rangle_{P(\mathbf{x},\mathbf{h}|W)}
  \]
  - **First Term**: Correlation with visible units clamped.  
  - **Second Term**: Free-running model correlation.  

#### **5. Challenges & Alternatives**  
- **Computationally Expensive**: Requires Gibbs sampling for gradient estimation.  
- **Modern Alternatives**: More efficient models (e.g., Restricted Boltzmann Machines, Deep Belief Networks) have largely replaced traditional Boltzmann machines.  

### **Key Takeaways**  
- Boltzmann machines generalize Hopfield networks with stochastic dynamics.  
- Learning involves matching model correlations to empirical data correlations.  
- Hidden units enable modeling of complex, higher-order dependencies.  
- Computational cost led to more efficient variants (e.g., RBMs) in modern deep learning.  