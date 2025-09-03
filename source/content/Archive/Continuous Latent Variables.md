* Principal Component Analysis (PCA): The chapter begins with a detailed look
     at PCA, a widely used technique for dimensionality reduction. It is
     presented from two perspectives:
       * Maximum Variance Formulation: Finding the linear projection that
         maximizes the variance of the projected data.
       * Minimum-Error Formulation: Finding the linear projection that minimizes
         the sum-of-squares of the projection errors.

   * Probabilistic PCA (PPCA): This section introduces a probabilistic,
     generative formulation of PCA. This model has several advantages over the
     conventional approach, including:
       * It defines a proper probability distribution, allowing for direct
         comparison with other models.
       * It can be trained efficiently using the EM algorithm.
       * It can handle missing data in a principled way.
       * It can be extended to mixtures of probabilistic PCA models.

   * Factor Analysis: This is presented as a closely related linear-Gaussian
     latent variable model. The key difference from PPCA is that the conditional
     distribution of the observed data has a diagonal, rather than isotropic,
     covariance matrix. This allows it to model independent noise for each
     observed variable.

   * Independent Component Analysis (ICA): The chapter discusses ICA as a
     generalization where the latent variable distribution is non-Gaussian. This
     is motivated by problems like blind source separation, where the goal is to
     recover original signals from mixed observations.

   * Nonlinear Latent Variable Models: The chapter concludes by introducing the
     idea of using deep neural networks to create nonlinear mappings from the
     latent space to the data space. This allows for the modeling of complex,
     non-linear manifolds in the data, setting the stage for more advanced
     generative models discussed in later chapters.

```embed
title: "Lecture 15 - EM Algorithm & Factor Analysis | Stanford CS229: Machine Learning Andrew Ng -Autumn2018"
image: "https://i.ytimg.com/vi/tw6cmL5STuY/maxresdefault.jpg"
description: "For more information about Stanford’s Artificial Intelligence professional and graduate programs, visit: https://stanford.io/aiAndrew Ng Adjunct Professor of..."
url: "https://www.youtube.com/watch?v=tw6cmL5STuY"
favicon: ""
aspectRatio: "56.25"
```
