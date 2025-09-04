Introduction to Normalizing Flows

  Normalizing flows are a class of generative models that are based on the
  principle of transforming a simple probability distribution (the "base"
  distribution) into a more complex one through a series of invertible and
  differentiable transformations.

  Core Idea:
  The key idea is to construct a complex distribution by applying a sequence of
  invertible functions to a simple base distribution, typically a Gaussian. The
  change of variables formula is used to compute the probability density of the
  transformed variable.

  Key Properties:
   * Invertibility: The transformation function must be invertible, meaning that
     for every output, there is a unique input. This allows for a one-to-one
     mapping between the latent space and the data space.
   * Differentiability: The transformation and its inverse must be differentiable.
      This is necessary to compute the Jacobian determinant, which is a crucial
     part of the change of variables formula.

  Change of Variables Formula:
  If z is a random variable with a known probability density p(z), and x = f(z)
  is an invertible transformation, then the probability density of x is given
  by:

  p(x) = p(z) * |det(J(f^-1(x)))|

  where J is the Jacobian of the transformation. The absolute value of the
  determinant of the Jacobian, |det(J)|, measures how the volume of a small
  region in the latent space is stretched or compressed by the transformation.

  Coupling Flows

  Coupling flows are a type of normalizing flow that are designed to have a
  simple and efficient computation of the Jacobian determinant.

  Real NVP (Non-Volume Preserving):
  A popular type of coupling flow is the Real NVP model. The core idea is to
  partition the input vector z into two parts, z_A and z_B. The transformation
  is then defined as:

   * x_A = z_A (identity transformation)
   * x_B = s(z_A) * z_B + t(z_A) (affine transformation)

  where s and t are scaling and translation functions, respectively, that are
  implemented as neural networks.

  Key Features of Real NVP:
   * Invertibility: The transformation is easily invertible.
   * Efficient Jacobian: The Jacobian matrix of this transformation is triangular,
     which means its determinant is simply the product of the diagonal elements.
     This makes the computation of the determinant very efficient.
   * Flexibility: By stacking multiple Real NVP layers and alternating which part
     of the vector is transformed, it is possible to build very expressive models.


  Autoregressive Flows

  Autoregressive flows are another class of normalizing flows that are based on
  autoregressive models.


  Masked Autoregressive Flow (MAF):
  In a MAF, each dimension of the output x_i is conditioned on the previous
  dimensions x_1, ..., x_{i-1}. The transformation is defined as:

  x_i = s_i(x_1, ..., x_{i-1}) * z_i + t_i(x_1, ..., x_{i-1})

  where s_i and t_i are again neural networks.

  Key Features of MAF:
   * Efficient Likelihood Evaluation: The likelihood of a data point can be
     computed efficiently in a single pass.
   * Slow Sampling: Generating new samples is a sequential process and can be
     slow, as each dimension must be generated one at a time.

  Inverse Autoregressive Flow (IAF):
  IAFs are designed to address the slow sampling issue of MAFs. They have the
  same functional form as MAFs but with the roles of x and z reversed.

   * Efficient Sampling: New samples can be generated in a single parallel pass.
   * Slow Likelihood Evaluation: The likelihood evaluation is sequential and can
     be slow.

  Continuous Flows (Neural ODEs)

  Continuous normalizing flows, also known as Neural Ordinary Differential
  Equations (Neural ODEs), are a more recent development that models the
  transformation as a continuous-time process.

  Core Idea:
  Instead of a discrete sequence of transformations, a Neural ODE defines the
  transformation as the solution to an ordinary differential equation (ODE):

  dz(t)/dt = f(z(t), t, w)

  where f is a neural network. The transformation is the result of integrating
  this ODE from a starting time t_0 to an ending time t_1.

  Key Features of Neural ODEs:
   * Continuous Transformation: The model learns a continuous transformation,
     which can be more expressive than a discrete sequence of layers.
   * Adaptive Computation: The ODE solver can adaptively choose the number of
     steps needed for integration, which can be more efficient than using a fixed
     number of layers.
   * Memory Efficiency: The adjoint sensitivity method allows for the training of
     Neural ODEs with constant memory cost, regardless of the "depth" of the
     integration.