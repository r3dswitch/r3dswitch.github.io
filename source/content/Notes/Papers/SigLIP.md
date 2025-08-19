```embed
title: "Using big_vision on GPUs"
image: "https://lucasb.eyer.be/articles/bv_tuto_data.webp"
description: "A tutorial on using the big_vision codebase on GPUs. It walks through a few common scenarios: fine-tuning the PaliGemma VLM on a multimodal task, fine-tuning the SigLIP image encoder as a classifier, and training a ResNet50 classifier from scratch."
url: "https://lucasb.eyer.be/articles/bv_tuto.html"
favicon: ""
aspectRatio: "48.320413436692505"
```

```embed
title: "Lucas Beyer - Sigmoid Loss for Language Image Pre-Training"
image: "https://i.ytimg.com/vi/Nk9YnMHB6hU/maxresdefault.jpg"
description: "About Speaker: Bio: Lucas grew up in Belgium wanting to make video games and their AI, went on to study mechanical engineering at RWTH Aachen in Germany, did..."
url: "https://www.youtube.com/watch?v=Nk9YnMHB6hU&t=1552s"
favicon: ""
aspectRatio: "56.25"
```

```embed
title: "Google Colab"
image: "https://colab.research.google.com/img/colab_favicon_256px.png"
description: ""
url: "https://colab.research.google.com/github/NielsRogge/Transformers-Tutorials/blob/master/SigLIP/Inference_with_%28multilingual%29_SigLIP,_a_better_CLIP_model.ipynb"
favicon: ""
aspectRatio: "100"
```

Language Pretraining Paper:
```embed
title: "cdn.openai.com"
image: ""
description: ""
url: "https://cdn.openai.com/research-covers/language-unsupervised/language_understanding_paper.pdf"
favicon: ""
```

- Generative Pretraining followed by Discriminative Finetuning leads to massive improvements
- Leveraging more than word level information is difficult because:
	- Optimisation objectives fro transfer unclear
	- Transfering learned representations to target task difficult
- Two stage training procedure:
	- Use language modelling objective on unlabeled data to learn inital parameters of model
	- Adapt parameters to target task using corresponding supervised objective
- Hypothesis on why language model pre-training of transformers is effective:
	- Underlying generative model learns to perform many of the tasks evaluated on in order to improve its language modeling capability 
	- The more structured attentional memory of the transformer assists in transfer compared to LSTMs.

### CLIP
- Dataset: Large with Annotations
- Predicting the exact words of the text accompanying each image. This is a difficult task due to the wide variety of descriptions, comments, and related text that co-occur with images.
- Motivation
	- Traditional computer vision models rely on costly, task-specific labeled datasets (e.g., ImageNet).
    
	- Natural language provides a rich, flexible, and widely available form of supervision.
- Key Idea
	- Train an image encoder and a text encoder jointly using **contrastive learning** on large-scale image–text pairs.
	- Align image and text representations in a shared embedding space so that matching image–text pairs are close together.
- Method

1. **Data**: ~400 million image–text pairs collected from the internet.
    
2. **Model**:
    
    - Image encoder: ResNet or Vision Transformer (ViT).
        
    - Text encoder: Transformer-based (similar to GPT-2).
        
3. **Training Objective**:
    
    - Contrastive loss: maximize cosine similarity of correct (image, text) pairs while minimizing similarity with incorrect pairs.
        
    - Implemented as a symmetric cross-entropy loss over similarity scores.
        

---

### Results

- **Zero-shot transfer**:
    
    - CLIP can classify images without training on task-specific labels—just by writing natural-language prompts (e.g., "a photo of a {label}").
        
    - Achieved competitive results across ImageNet, CIFAR-10, Oxford Pets, etc.
        
- **Broad capabilities**:
    
    - Performs well on OCR, geo-localization, action recognition, etc., without task-specific training.
        
- **Limitations**:
    
    - Struggles with fine-grained tasks (e.g., differentiating dog breeds).
        
    - Sensitive to phrasing of prompts.
        
    - Inherits biases present in internet data.

### SigLIP

## **SigLIP (2023): Sigmoid Loss for Language-Image Pre-Training**

**Key idea**: Instead of the standard contrastive softmax (InfoNCE) loss used in CLIP, SigLIP employs a **pairwise sigmoid loss** applied independently to each image–text pair. This removes the need for normalization across the entire batch, enabling more efficient scaling and better performance, especially at small batch sizes. ([arXiv](https://arxiv.org/abs/2303.15343?utm_source=chatgpt.com "Sigmoid Loss for Language Image Pre-Training"), [himanshustwts.com](https://www.himanshustwts.com/posts/siglip?utm_source=chatgpt.com "SigLIP Paper - hola sigmoid!"))

**Benefits**:

- **Efficiency gains**: Avoids global similarity normalization—reduces memory/compute overhead, enabling larger batches or faster runtimes. ([himanshustwts.com](https://www.himanshustwts.com/posts/siglip?utm_source=chatgpt.com "SigLIP Paper - hola sigmoid!"), [Hugging Face](https://huggingface.co/docs/transformers/v4.45.2/en/model_doc/siglip?utm_source=chatgpt.com "SigLIP - Hugging Face"))
    
- **Strong accuracy**: With just four TPUv4 chips and Locked-Image Tuning, a SigLIP model reached **84.5% zero-shot ImageNet accuracy** in two days. ([arXiv](https://arxiv.org/abs/2303.15343?utm_source=chatgpt.com "Sigmoid Loss for Language Image Pre-Training"), [Hugging Face](https://huggingface.co/docs/transformers/v4.45.2/en/model_doc/siglip?utm_source=chatgpt.com "SigLIP - Hugging Face"))
    
- **Batch size independence**: The sigmoid loss decouples performance from extreme batch sizes—training up to **1 million** batch size yielded diminishing returns, and a more moderate size (e.g., 32 k) sufficed. ([arXiv](https://arxiv.org/abs/2303.15343?utm_source=chatgpt.com "Sigmoid Loss for Language Image Pre-Training"), [Hugging Face](https://huggingface.co/papers/2303.15343?utm_source=chatgpt.com "Paper page - Sigmoid Loss for Language Image Pre-Training"))
    

**Implications**: SigLIP offers an effective, resource-efficient alternative to the standard CLIP loss, especially valuable for researchers with limited compute.

---

## **SigLIP 2 (February 2025): Enhanced Multilingual Vision-Language Encoders**

This follow-up builds upon SigLIP’s framework with new techniques to achieve richer, multilingual vision-language modeling.

**Enhancements introduced**:

1. **Unified training recipe** combining:
    
    - Captioning-based pretraining
        
    - Self-supervised losses (e.g., self-distillation, masked prediction)
        
    - Online data curation ([Hugging Face](https://huggingface.co/papers/2502.14786?utm_source=chatgpt.com "Paper page - SigLIP 2: Multilingual Vision-Language Encoders with ..."), [arXiv](https://arxiv.org/abs/2502.14786?utm_source=chatgpt.com "SigLIP 2: Multilingual Vision-Language Encoders with Improved Semantic Understanding, Localization, and Dense Features"))
        
2. Strong **performance gains** across core tasks:
    
    - Zero-shot classification
        
    - Image–text retrieval
        
    - Transfer learning for vision-language models ([Hugging Face](https://huggingface.co/papers/2502.14786?utm_source=chatgpt.com "Paper page - SigLIP 2: Multilingual Vision-Language Encoders with ..."), [arXiv](https://arxiv.org/abs/2502.14786?utm_source=chatgpt.com "SigLIP 2: Multilingual Vision-Language Encoders with Improved Semantic Understanding, Localization, and Dense Features"))
        
3. Improved **localization** and **dense prediction**, thanks to better feature modeling. ([arXiv](https://arxiv.org/abs/2502.14786?utm_source=chatgpt.com "SigLIP 2: Multilingual Vision-Language Encoders with Improved Semantic Understanding, Localization, and Dense Features"))
    
4. Support for multiple resolutions while preserving original aspect ratios. ([arXiv](https://arxiv.org/abs/2502.14786?utm_source=chatgpt.com "SigLIP 2: Multilingual Vision-Language Encoders with Improved Semantic Understanding, Localization, and Dense Features"))
    
5. Training on a more **diverse, debiased multilingual dataset**, yielding better fairness and cross-linguistic capacity. ([arXiv](https://arxiv.org/abs/2502.14786?utm_source=chatgpt.com "SigLIP 2: Multilingual Vision-Language Encoders with Improved Semantic Understanding, Localization, and Dense Features"))
    

**Model family**: SigLIP 2 comes in different sizes to balance performance and inference cost:

- ViT-B (86M parameters)
    
- ViT-L (303M)
    
- So400m (400M)
    
- A ~1B-parameter version ([arXiv](https://arxiv.org/abs/2502.14786?utm_source=chatgpt.com "SigLIP 2: Multilingual Vision-Language Encoders with Improved Semantic Understanding, Localization, and Dense Features"))
    

---

### **Summary Table**

|**Version**|**Key Improvements**|**Strengths**|**Considerations**|
|---|---|---|---|
|**SigLIP**|Pairwise sigmoid loss—no global normalization|Efficient training, strong zero-shot|Basic contrastive setup, no multilingual aspect|
|**SigLIP 2**|Adds captioning, self-supervision, denser features, multilingual data|Better retrieval, localization, fairness, multilingual|Larger models; more complex training recipe|
