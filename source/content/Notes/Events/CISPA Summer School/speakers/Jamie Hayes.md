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
