### Antti Honkela

Antti Honkela is a Professor of Data Science, with a focus on Machine Learning and AI, at the University of Helsinki's Department of Computer Science. He is also the coordinating professor for the Research Programme in Privacy-preserving and Secure AI at the Finnish Center for Artificial Intelligence (FCAI).

**Differential Privacy**
- Epsilon DP
- Epsilon delta DP
- Approximate DP
- Gaussian DP

**Properties of DP:**
- DP guarantees can't be made weaker by post processing
- DP Composition
- Group Privacy
- DP is a property of an algorithm not its output

**Mechanisms:**
- Randomised Response

**Design Choices for DP Implementations:**
- Def
- Relation
- Budget
- Mechanism

**Privacy Accounting for DP-SGD**


### Matthew Jagielski

Matthew Jagielski is a research scientist at Google DeepMind, where he focuses on the security, privacy, and memorization aspects of machine learning systems. His work encompasses areas like privacy auditing, data poisoning, model stealing, and understanding memorization in generative models.

**Data Poisoning**
- AlexNet -> Transfer Learning -> GPT2 -> Chat LLMs -> Better LLMs

**Attacker Objectives:**
- Targeted
- Availability
- Backdoors
- Sub Population

**Domain vs Capability Specific Attacks**

**Attacks on In-context Learning**
- Prompt Engineering Reinforces Backdoor Behaviours
- Prompt Injection is easier than Data Poisoning

**Training Data Curation**
- Pre Training from internet, Post Training from contractors
- Successful post training can work with 0.5% of data
- Pre Training: Feed in Common Crawl, Web Page Filtering, Download Image Text Pairs, Content Filtering, Store Data (LAION-5B Curation Pipeline)

**Poisoning Vectors**
- Buying Expired Domains
- Poisoning as a service in response to profiling crawlers paper

**Solutions:**
- checksums(not perfect)
- Wikipedia checkpoints are highly regular
- Dolma Dataset
- Pretraining Poisoning at 0.1% for 7B models

**Defenses:**
- Pessimistic about anomaly detection type defenses
- SUP-NATINST Dataset
- Poisoning Forensics
- Training Data Attribution
- System-Level Defenses
- Data Attribution Heirarchial
