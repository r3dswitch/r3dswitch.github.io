[https://www.youtube.com/watch?v=UBDgSHPxVME](GP_Intro)

#### **1. Introduction**  
- **Definition**: A Gaussian Process (GP) is a **non-parametric**, probabilistic model for functions.  
- **Key Idea**: Instead of learning fixed parameters (like in neural networks), GPs define a **distribution over possible functions** that fit the data.  
- **Analogy**: "Infinite-dimensional Gaussian distribution," where any finite set of function values follows a joint Gaussian distribution.  

#### **2. Key Components**  
- **Mean Function** (*m(x)*): Represents the expected function value at input *x* (often set to zero for simplicity).  
- **Kernel (Covariance) Function** (*k(x, x’)*):  
  - Encodes **similarity** between inputs (e.g., smoothness, periodicity).  
  - Common kernels: **RBF (squared exponential)**, Matérn, periodic.  

#### **3. Predictions**  
- **Posterior Distribution**: Given data *(X, y)*, predictions at new points *X** are Gaussian:  
  - **Mean**: Weighted combination of training outputs.  
  - **Variance**: Uncertainty estimate (shrinks near observed data).  
- **Closed-Form Solution**: Exact inference is computationally tractable for small datasets (*O(N³)* for *N* points).  

#### **4. Strengths**  
- **Uncertainty Quantification**: Naturally provides **error bars** (predictive variance).  
- **Flexibility**: Captures complex patterns via kernel choice (no need for manual feature engineering).  
- **Interpolation**: Excels where data is sparse (e.g., Bayesian optimization).  

#### **5. Limitations**  
- **Scalability**: Cubic complexity in dataset size (*N*).  
- **Kernel Design**: Choice of kernel requires domain knowledge (though automated methods exist).  

#### **6. Applications**  
- **Regression**: Small datasets with noise (e.g., geostatistics, robotics).  
- **Bayesian Optimization**: Efficiently optimizes expensive black-box functions (e.g., hyperparameter tuning).  
- **Time Series**: Forecasting with uncertainty.  

#### **7. Extensions**  
- **Sparse GPs**: Approximations (e.g., SVGP) for large datasets.  
- **Deep GPs**: Hierarchical compositions for richer function spaces.  

### **Key Takeaways**  
GPs offer a **principled, interpretable** framework for regression and uncertainty-aware modeling, but scalability remains a challenge. Their elegance lies in unifying **kernel methods** with **Bayesian inference**.  