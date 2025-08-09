
### Battista Biggio

Battista Biggio is a Full Professor at the University of Cagliari in Italy and a co-founder of the cybersecurity company Pluribus One. His work focuses on machine learning and pattern recognition, particularly in the area of security. He has received recognition for his pioneering contributions to adversarial machine learning.

**Adversarial ML History:**
- AISec Workshop 2004-2006
- 2012 ICML
- 2013 ECML Poison, Evasion Attacks
- Wild Patterns: Ten Years after adv ml 2018

**Evasion Attack:**
- Good word insertion, bad word alteration
- Detection of Malicious PDF: Space of good vs bad, followed by optimisation to misclassification
- Nicolas Carlini adversarial landscape

**Challenges for AI/ML Testing:**
- Certified vs Empirical Robustness
- Obfuscated Gradients: not effective
- Indicators of Attack Failure as Semi Automated Framework
- Wrong PGD Attack Implementations
- Attack Bench
- sigma-zero paper, change label with lowest number of changes
- Mal-Conv: CNN for malware detection and attacks on it using bit manipulation injections
- saiferlab.ai

**Robust Optimisation Problem:**
- Regularisation as Noise(bounded perturbation to dual norm of perturbation)

**Denial of Service Poisoning Attacks:**
- Gradient Based Poisoning Attacks(Scaling not good)

**Backdoor Poisoning**

**Wild Patterns for LLM Security/ Gen AI:**
- Jailbreak Chat
- NVIDIA GARAK
- Encoding, Sandwich Attacks
- Gradient Based Optimisation of Adversarial Suffixes
- Weight Orthogonalisation
- Latent Break for Perplexity Filters

**Conclusion:**
- Adversarial ML Problems are Getting Harder to Solve and Evaluate

### Ilia Shumailov

Ilia Shumailov is a Research Scientist at Google DeepMind, with research interests in Machine Learning and Computer Security. He is also an Associate Member (Senior Research Fellow) at the University of Oxford.

**What is the thing hiding behind my model**

> The worst enemy of security is complexity, Bruce Schneider

- Log4j vulnerability
- How many people sandbox their ML code when running locally? hf trust remote code flag

**Data, Architecture, Compiler, Runtime Components**
- Pytorch nightly compromise
- Securing CI/CD is super hard, pytorch breached
- Imagenet dataset with malware

**Supply Chain Attacks in ML Frameworks**
- Number of dependencies for ML frameworks is crazy

**ML Backdoors**
- Compromised Dependencies
- Direct Weight Manipulation

**Architectural Backdoors in Neural Networks**
- ONNX Graph Vis
- Architectural Neural Backdoors from First Principles
- Hidden Layer Company: Signing Graphs
- Choice of Architecture and Model super subjective wrt coding style and preferences
- Humans indifferent to backdoors
- Magical Numbers a big problem
- Hjel2/userstudy on github

**Defenses:**
- Blocklisting
- Provenance
- Architecture Obfuscation
- ImpNet

**Poisoning Web-Scale Training Datasets is Practical**

**Quantization Backdoors**

**On Trusting Trust: Ken Thompson**


### Andrew Paverd

Andrew Paverd is a Principal Research Manager at Microsoft, focusing on AI security and privacy. He obtained his DPhil from the University of Oxford. His work includes research on prompt injection attacks, federated learning, and information leakage in natural language models.

**Secure Design Patterns for LLMs**

- Dual LLM Pattern(Previledged and Quarantined LLM)
- Code-the-Execute Pattern
- Camel Paper (ETH)
- Information Flow Control
- Context Minimisation Pattern
- Highlight and Summarise

**Open Questions:**
- Where else can we use secure design patterns?
- How do we combine probabilistic and system level defenses?
- How do we get informed user approval?
- What new secure design patterns can we build?
- AI for vulnerability detection startups
