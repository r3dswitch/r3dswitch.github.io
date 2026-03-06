Introduction

  Diffusion models, also known as Denoising Diffusion Probabilistic Models
  (DDPMs), are a class of generative models that have emerged as a
  state-of-the-art approach for many applications, particularly in image
  generation. The core idea is to gradually add noise to an image until it
  becomes pure noise, and then learn to reverse this process to generate new
  images from noise.

Forward Encoder

  The forward process, or the encoder, is a fixed process that gradually adds
  Gaussian noise to an image x over a series of T steps. This creates a
  sequence of increasingly noisy images z_1, z_2, ..., z_T.

   * The Process: At each step t, the noisy image z_t is generated from the
     previous noisy image z_{t-1} by adding Gaussian noise with a variance
     beta_t:
      z_t = sqrt(1 - beta_t) * z_{t-1} + sqrt(beta_t) * epsilon_t
      where epsilon_t is a sample from a standard normal distribution.

   * Diffusion Kernel: A key property of this process is that we can directly
     sample z_t for any t without having to iterate through all the previous
     steps. This is done using the diffusion kernel:
      q(z_t|x) = N(z_t | sqrt(alpha_t) * x, (1 - alpha_t) * I)
      where alpha_t is a product of the variances from previous steps.

   * Final State: After a large number of steps T, the image z_T becomes
     indistinguishable from pure Gaussian noise.

Reverse Decoder

  The reverse process, or the decoder, is a learned process that aims to reverse
   the forward noising process. The goal is to learn a model p(z_{t-1}|z_t, w)
  that can predict the less noisy image z_{t-1} from the noisier image z_t.

   * The Challenge: The true reverse conditional distribution q(z_{t-1}|z_t) is
     intractable to compute because it depends on the entire data distribution.


   * The Solution: We approximate the reverse process with a neural network,
     typically a U-Net architecture, that learns to predict the mean of the
     reverse conditional distribution.

Training the Decoder

  The decoder is trained by maximizing the Evidence Lower Bound (ELBO) on the
  log-likelihood of the data. The ELBO for a diffusion model can be broken down
  into:

   * Reconstruction Term: This term encourages the model to be able to
     reconstruct the original image from the final noisy image z_1.
   * Consistency Terms: These terms, which are KL divergences, encourage the
     learned reverse process p(z_{t-1}|z_t, w) to be consistent with the true
     reverse process q(z_{t-1}|z_t, x).

Predicting the Noise

  Instead of predicting the denoised image at each step, a more effective
  approach is to train the neural network to predict the total noise that was
  added to the original image to create the noisy image at that step. The loss
  function then becomes a simple squared error between the predicted noise and
  the actual noise.

Generating New Samples

  Once the decoder network is trained, we can generate new samples by:
   1. Sampling a random noise vector z_T from a standard Gaussian distribution.
   2. Iteratively applying the learned reverse process for t = T, T-1, ..., 1 to
      gradually denoise the image and obtain a final sample x.

Score Matching

  Denoising diffusion models are closely related to another class of generative
  models based on score matching.

   * The Score Function: The score function s(x) is the gradient of the
     log-likelihood of the data with respect to the data vector x.
   * Score Matching: The goal of score matching is to train a model s(x, w) to
     match the true score function of the data distribution.
   * Connection to Denoising: The loss function for denoising score matching is
     equivalent to the loss function used in denoising diffusion models.

Guided Diffusion

  To generate images conditioned on some information c (e.g., a class label or
  a text prompt), we can use guided diffusion.

   * Classifier Guidance: This approach uses a separate, pre-trained classifier
     p(c|x) to guide the diffusion process towards generating images that are
     consistent with the conditioning information.
   * Classifier-Free Guidance: This is a more effective approach that does not
     require a separate classifier. Instead, a single conditional diffusion model
     is trained, and during generation, the model is guided by a combination of
     the conditional and unconditional score estimates. This allows for a
     trade-off between sample quality and diversity.