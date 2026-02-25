Why Regularise?
- Preference over weights
- Make model simple for test data
- Introduce curvature for optimisation(L2)
- Can also make training faster
L2 likes to spread out weights
Numeric Gradient: Slow, Easy to Write and Approximate
Analytic Gradient(chain rule and calculus): Exact, Fast, Error Prone
In Practice: always use analytic gradient but check using numerical gradient
Problems of SGD: 
- If one direction changes more rapidly than another(high condition number) then SGD oscillates and might shoot out or jitter 
- In local minima and saddle points it gets stuck
- Updates can be noisy because of batching
SGD+Momentum helps
RMSProp is element wise scaling of the gradient based on sum of squares in each dimension(per parameter/ adaptive LR)
ADAM is RMSProp with Momentum with bias correction term based on time step to prevent 0/0 initially
ADAMW is ADAM with Weight Decay only looking at data loss and not regularisation separating it into two functions instead of one to make it dependent on weights and not loss
Learning Rate Decay/Scheduler: Timestep, Cosine, Linear, Inv Sqrt
Linear warmup to increase value before decreasing
Empirical Rule of thumb: if you increase batch size by N scale learning rate by N
Second Order Optimisation using Hessian not generally used in deep learning as second order taylor optimisation becomes too large in terms of memory
