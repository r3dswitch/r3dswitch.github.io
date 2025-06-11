### Basic Framework

- **Goal**: Select action _a_ that maximizes expected utility
- **Components**:
    - Actions: _a_ (choices available)
    - States: _x_ (possible world states)
    - Probabilities: P(x|a) (state probabilities given action)
    - Utility: U(x,a) (payoff for state _x_ and action _a_)

### Key Insight

- Decision theory is conceptually simple: maximize expected utility
- Computational complexity arises in practice (like chess - simple rules, complex execution)
- Alternative: Minimize expected loss L(x,a) instead of maximizing utility

## Rational Prospecting Example

### Problem Setup

- **Scenario**: Choose optimal Tanzanite mining site from N options
- **Unknown**: Return xₙ from each site n (revenue minus costs)
- **Decision sequence**:
    1. Decide whether/where to prospect
    2. Choose which site to mine
- **Information gathering**: Prospecting at site n costs cₙ, yields data dₙ about xₙ

### Mathematical Model (Gaussian Case)

#### Prior Information

- Return distributions: P(xₙ) = Normal(xₙ; μₙ, σₙ²)
- Prospecting data: P(dₙ|xₙ) = Normal(dₙ; xₙ, σ²)
- Utility functions:
    - No prospecting: U = xₙₐ
    - With prospecting: U = -cₙₚ + xₙₐ

#### Bayesian Updates

- **Prior distribution of data**: P(dₙ) = Normal(dₙ; μₙ, σ² + σₙ²)
- **Posterior after prospecting**: P(xₙ|dₙ) = Normal(xₙ; μ'ₙ, σ'ₙ²)
- **Updated parameters**:
    - μ'ₙ = (dₙ/σ² + μₙ/σₙ²)/(1/σ² + 1/σₙ²)
    - 1/σ'ₙ² = 1/σ² + 1/σₙ²

### Decision Analysis

#### Without Prospecting

- **Optimal action**: Choose site with highest mean return
- **Decision rule**: nₐ = argmaxₙ μₙ

#### With Prospecting

- **Key insight**: Prospecting value comes from potentially changing the optimal action
- **Uncertainty**: Don't know dₙ in advance, so don't know final action
- **Distribution of updated mean**: μ'ₙ ~ Normal(μₙ, s²)
- **Variance**: s² = σₙ²σ²/(σ² + σₙ²)

#### Value of Information

- **Expected utility with prospecting**:
- **Decision criterion**: Prospect if expected benefit exceeds cost cₙ
- **Depends on**:
    - Difference between current best site and prospecting site (μₙ - μ₁)
    - Uncertainty levels (σₙ, σ)
    - Prospecting cost cₙ

## Key Practical Challenges

### Complexity Issues

- **Sequential decisions**: Each action provides information affecting future choices
- **Computational explosion**: Decision trees become enormous in realistic problems
- **Forward/backward reasoning**: Mix of probability and inverse probability computations

### Real-World Considerations

- **Utility function design**: Choosing appropriate U(x,a) can be difficult
- **Bounded rationality**: Perfect optimization often computationally intractable
- **Information economics**: Value of gathering information vs. cost

## General Principles

### When to Gather Information

- Value depends on potential to change optimal action
- Higher uncertainty increases information value
- Must weigh information cost against expected benefit

### Bayesian Decision Making

- Combine prior beliefs with new data
- Update beliefs using Bayes' theorem
- Make decisions based on posterior distributions

### Risk and Uncertainty

- Linear utility functions lead to risk-neutral behavior
- Nonlinear utilities can capture risk preferences
- Uncertainty levels affect information gathering decisions