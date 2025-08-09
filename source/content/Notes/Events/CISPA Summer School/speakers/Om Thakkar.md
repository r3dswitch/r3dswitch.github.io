### Om Thakkar

Om Thakkar is a research engineer at OpenAI, focusing on privacy-preserving AI, particularly differential privacy in deep learning for production systems. He previously worked as a senior research scientist at Google for five years.

**Privacy Leakage in Speech Models: Attacks and Mitigations**

**Privacy Leakage:**
- Training Data: Unauthorised Access
- ML Algorithms: Gradient Leakage
	- Utterance Labels
	- Speaker Identity
- Released NN: Secret Sharer, Fill in the blank attacks, membership inference

**Speech Models:**
- TTS, STT(ASR), S2S, Speaker Recognition, S2S Translation, Foundation Speech Models(Whisper)

**Types of Privacy Leakage:**
- Extraction Attacks
- Memorisation Audits

**Data Extraction:**
- Noise Masking
- Extraction from Pre-trained Speech Encoders: LibriLight vs LibriSpeech
- Large Dataset means Less Memorisation
- Fine tune Encoder with ASR data to make a ASR attack model
- Mitigations: Deduplication, sanitisation during pre-training

**Secret Sharer:**
- Insert Handcrafted Samples (Canaries) in training data, measure performance on canaries, contrast with holdout set
- Exposure as a metric
- Auditing large ASR is very expensive
- SOTA uses thousands of shadow models for calibration
- Canaries have variation in:
	- Transcript
	- Audio
	- Frequency
- Exposure using Character Error Rate
- Separate Learning from Memorisation
- Larger models memorise more

**Empirical Privacy Techniques:**
- Differential Privacy
- Sensitivity Bounded Training
- Per Example Clipping for Memorisation
- PEC limits batch processing in GPUs resulting in slowdown
- PEC also adds excessive bias during training
- Reducing Overhead: Microbatch Clipping, Per-core Clipping
- Adaptive Clipping for Adaptive Optimisers an open question

**Future Directions:**
- Multimodal User Data Privacy Attacks
- Moving privacy upstream in model training (earliest stages), DP-fy your Data Tutorial ICML25
- Private Synthetic Data, Private Rewriting
