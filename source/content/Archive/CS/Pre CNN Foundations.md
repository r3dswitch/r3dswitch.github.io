**L1 vs. L2.** It is interesting to consider differences between the two metrics. In particular, the L2 distance is much more unforgiving than the L1 distance when it comes to differences between two vectors. That is, the L2 distance prefers many medium disagreements to one big one. L1 and L2 distances (or equivalently the L1/L2 norms of the differences between a pair of images) are the most commonly used special cases of a [p-norm](https://planetmath.org/vectorpnorm).

Image classification approach has two major components: a **score function** that maps the raw data to class scores, and a **loss function** that quantifies the agreement between the predicted scores and the ground truth labels. This is then cast as an optimization problem where the loss function is minimized with respect to the parameters of the score function.

Bias Trick

The Multiclass Support Vector Machine "wants" the score of the correct class to be higher than all other scores by at least a margin of delta. If any class has a score inside the red region (or higher), then there will be accumulated loss. Otherwise the loss will be zero. Our objective will be to find the weights that will simultaneously satisfy this constraint for all examples in the training data and give a total loss that is as low as possible.

Hinge Loss, Squared Hinge Loss

To encode some preference for a certain set of weights **W** over others to remove ambiguity of weights. We can do so by extending the loss function with a **regularization penalty** R(W). The most appealing property is that penalizing large weights tends to improve generalization, because it means that no input dimension can have a very large influence on the scores all by itself.

The Softmax classifier minimizes the cross-entropy between the estimated class probabilities and the “true” distribution, which in this interpretation is the distribution where all probability mass is on the correct class (i.e. p=[0,…1,…,0] contains a single 1 at the yi -th position.).

_SVM classifier_ uses the _hinge loss_, or also sometimes called the _max-margin loss_. The _Softmax classifier_ uses the _cross-entropy loss_.

The difference between the SVM and Softmax classifiers for one datapoint. In both cases we compute the same score vector **f** (e.g. by matrix multiplication in this section). The difference is in the interpretation of the scores in **f**: The SVM interprets these as class scores and its loss function encourages the correct class (class 2, in blue) to have a score higher by a margin than the other class scores. The Softmax classifier instead interprets the scores as (unnormalized) log probabilities for each class and then encourages the (normalized) log probability of the correct class to be high (equivalently the negative of it to be low). The final loss for this example is 1.58 for the SVM and 1.04 (note this is 1.04 using the natural logarithm, not base 2 or base 10) for the Softmax classifier, but note that these numbers are not comparable; They are only meaningful in relation to loss computed within the same classifier and with the same data. Compared to the Softmax classifier, the SVM is a more _local_ objective, which could be thought of either as a bug or a feature.

A tuple is an (immutable) ordered list of values. A tuple is in many ways similar to a list; one of the most important differences is that tuples can be used as keys in dictionaries and as elements of sets, while lists cannot.

One useful trick with integer array indexing is selecting or mutating one element from each row of a matrix:
// Create a new array from which we will select elements
a = np.array([[1,2,3], [4,5,6], [7,8,9], [10, 11, 12]])
print(a)
// Create an array of indices
b = np.array([0, 2, 0, 1])
// Select one element from each row of a using the indices in b
print(a[np.arange(4), b]) # Prints "[ 1 6 7 11]"

Broadcasting is a powerful mechanism that allows numpy to work with arrays of different shapes when performing arithmetic operations.

Backprop Considerations:
**Cache forward pass variables**. To compute the backward pass it is very helpful to have some of the variables that were used in the forward pass. In practice you want to structure your code so that you cache these variables, and so that they are available during backpropagation. If this is too difficult, it is possible (but wasteful) to recompute them.

**Gradients add up at forks**. The forward expression involves the variables **x,y** multiple times, so when we perform backpropagation we must be careful to use `+=` instead of `=` to accumulate the gradient on these variables (otherwise we would overwrite it). This follows the _multivariable chain rule_ in Calculus, which states that if a variable branches out to different parts of the circuit, then the gradients that flow back to it will add.

Vector, Matrix and Tensor Derivatives: https://cs231n.stanford.edu/vecDerivs.pdf
To summarize, one can use the chain rule in the setting of vector and matrix derivatives
by:
- Clearly stating intermediate results and the variables used to represent them.
- Expressing the chain rule for individual components of the final derivatives.
- Summing appropriately over the intermediate results within the chain rule expression.

One can derive a simple equation to compute ∂L/∂W without explicitly forming
the Jacobian ∂Y/∂W by using:
∂L/∂W = XTrans * ∂L/∂Y