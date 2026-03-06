Memory hierarchy in GPUs and Tensor Cores (mixed precision, 16in, 32 out)
A model with L layers operates on tensors of shape(Batch, Sequence, Dim)
Types of parallelism: 
- Data: Split on batch
	- Use mini batch of MN samples, split over M GPUs with N samples each
	- 1. Each GPU has its own copy of model + optimiser
	- 2. Each GPU loads its own batch of data
	- 3. Each GPU runs forward pass to compute loss
	- 4. Each GPU runs backward pass to compute gradients
	- 5. Average gradients across all GPUs(all-reduce operation)
	- 6. Each GPU updates its own weights
	- 4 and 5 can run parallel
	- Problem: Model size constrained by GPU memory
	- Fully Sharded Data Parallelism(Split model weights across GPUs)
		- Fetch Wi+1 while computing forward with Wi
		- Fetch Wi while computing with Wi+1, Send dL/dWi and update Wi while computing with Wi-1 for backward pass, don't delete last layer to optimise
	- Hybrid Sharded Data Parallelism(Split model into M groups of K and do FSDP on groups of K and DP across M groups)
	- Problem: Model activations themselves can fill up memory
	- Solution: Compute activations on the fly instead of storing them in memory (Activation Checkpointing, sqrt(N) checkpoints => O(N*sqrt(N) compute, O(sqrt(N) memory)))
	- Always set per-GPU batch size to max out GPU memory
	- Maximise model flops utilisation (MFU>30% good, >40% great)
- Context: Split on sequence
	- Ring Attention
	- Ulysses Attention
- Pipeline: Split on L
- Tensor: Split on Dim