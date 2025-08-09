
### Mario Fritz

Mario Fritz is a faculty member at the CISPA Helmholtz Center for Information Security and an honorary professor at Saarland University. He is also a fellow of the European Laboratory for Learning and Intelligent Systems (ELLIS). His research focuses on trustworthy artificial intelligence, at the intersection of information security and machine learning.

**Reasons for non-interpretability:**
- Speed
- Lack of training data
- Incapacity to process all evidence

**Approaches to interpretability:**
- Cognitive modelling
- Laws of thought
- Turing test
- Rational agents

**Most Systems:**
- End to End
- Many Parameters and Representation Learning
- Visual Turing Test

**Why Foundational Models:**
- Task Generalisation
- Scaling Laws

**Cyber Threat Landscape:**
- MITRE Atlas
- OWASP Top 10
- COSAI
- Papernot'16 SoK, CIA Triade

**Challenges:**
- Scaling Security is a big challenge

**Future Directions:**
- ctf.spylab.ai
- codeLMSec
- Representation Engineering
- Hallucinations through activation functions
- AI 2027

### Jamie Hayes

Jamie Hayes is a Senior Research Scientist at Google DeepMind. His research focuses on adversarial machine learning, network traffic analysis, privacy, anonymity, and the application of machine learning to information security.

**Lessons from defending Gemini against indirect prompt attacks:**
- Data Exfiltration
- Why PI exists? Self Attention. k for all, q for one, v for all (masked attention is slightly different)
- Labelling of tokens needed (Instructions: trusted, data: mixed)
- MCP Case Study: Mutate definitions after installations, malicious override or intercept, tool poisoning : invariant labs
- Payphone whistles(red box), NX bits, SQL injection

**Model: Security targeted data to improve intelligence**
- Create prompt injection datasets to include in post training
	- System Instructions
	- Previous Interactions
	- User Instructions
	- Function Call
	- Data Point = Attack x Function X (History + Private Info)
	- Split func into train and eval and have 10, thousands samples
- Define realistic adversarial capabilities, goals and scenarios
	- Adversarial eval framework simulating and iteratively optimising attacks
		- Actor Critic
		- Beam Search
		- Tree of Attacks with Pruning(TAP)
	- Cost quite high, to improve have secondary generation pipeline to generate new examples to train using working ones as seed
	- Eval with old and new, training with only new model, also cross evals
	- Multi round attacks a challenge
	- Manual red-teaming is expensive and slow
	- Scalability is a problem
	- Generate adversarial examples for downstream eval and adversarial training/fine-tuning
- Construct datasets of diverse and working set of PI
- Include in SFT and RL
	- Generate Diverse Base Scenarios
	- Generating Strong Adversarial Attacks
	- Synthesising Corrective Responses
- Establish robust eval frameworks for improvements and regressions
	- Attack Success Rate
	- Queries needed to measure
	- Non binary success metrics
	- Attackers are multilingual
	- Adaptive Evals: On adaptive attacks to adversarial example defenses
	- Defenses: Self Reflection, ICL, Spotlighting, ...
	- Adversarial training doesn't make models worse
	- Objective functions for IPI is a difficult problem
	- Multimodal PI is a big problem

**Scaffolding:**
- Filtering, Input and output classifiers and monitors

**System:**
- Rate limits, access control policies

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
