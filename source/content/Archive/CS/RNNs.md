To fit backprop through time, we truncate it using a windowed approach
RNN Tradeoffs:
	Adv: No context length
		model size doesn't increase for longer input
	Disadv: Slow, Difficult to access info from long back 
RNN + CNN for Image Captioning and VQA, Visual Language Navigation
Vanilla RNN: SV>1 exploding gradients, SV<1 vanishing gradients
Soln: LSTM
RWKV, Mamba are modern variants
