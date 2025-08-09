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
