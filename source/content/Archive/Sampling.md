Basic Sampling Algorithms: The chapter begins with fundamental methods. It
     explains how sampling can be used to approximate expectations of functions.
     It then covers techniques for sampling from standard distributions using the
     transformation method (based on the inverse cumulative distribution
     function), with the Box-Muller method for Gaussians as a key example. It also
      introduces two more general, but limited, techniques:
       * Rejection Sampling: Uses a simpler "proposal" distribution to generate
         candidate samples, which are then accepted or rejected based on a
         criterion. Its efficiency drops significantly in high dimensions.
       * Importance Sampling: Aims to estimate expectations directly by drawing
         samples from a proposal distribution and re-weighting them.

   * Markov Chain Monte Carlo (MCMC) Methods: This is the core of the chapter,
     presenting a powerful framework for sampling from complex, high-dimensional
     distributions. The key idea is to create a Markov chain whose stationary
     distribution is the desired target distribution. The main algorithms
     discussed are:
       * Metropolis-Hastings Algorithm: A general MCMC method where a new state is
         proposed and then accepted or rejected based on a probability that depends
          on the proposal distribution and the target distribution.
       * Gibbs Sampling: A special case of Metropolis-Hastings where each variable
          is sampled sequentially from its conditional distribution given the
         current values of all other variables. It is widely used, especially in
         the context of graphical models.
       * Ancestral Sampling: A simple and efficient method for sampling from
         directed graphical models (Bayesian networks) by following the
         topological ordering of the variables.

   * Langevin Sampling: This section introduces more advanced MCMC methods that
     leverage the gradient of the log probability distribution (the "score"). By
     moving in the direction of the gradient, these methods can explore the
     sample space more efficiently than the random walks often produced by
     simpler MCMC techniques. This section connects sampling to Energy-Based
     Models (EBMs) and discusses how to train them by approximating the
     likelihood gradient, a technique that is central to modern generative models
      - like diffusion models.