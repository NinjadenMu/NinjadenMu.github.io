---
layout: page
title: Research at UB
---

I've doing research in an internship at the University at Buffalo under the guidance of Professor Hongxin Hu, PhD candidate Keyan Guo, and several other researchers (2 years and still ongoing).  I feel like I'm learning a lot working with them, and they've given me a lot of guidance.  Throughout the internship, I've helped produce several papers.  I've included a link and a summary of each one below:
<br>
### - My First Paper: "Understanding the Generalizability of Hateful Memes Detection Models Against COVID-19-related Hateful Memes" (Accepted to ICMLA 2022)
#### [link (Hosted on NSF Public Repository)](https://par.nsf.gov/servlets/purl/10399964#:~:text=Our%20studies%20show%20that%20these,textual%20modality%20actually%20provides%20significantly) 
This work studied the inner workings, effectiveness, and generalizability of multimodal models when applied to hateful memes.  Memes are surprisingly hard for ML methods to understand, since the text and image of a meme must be interpreted together in context.  Although this paper seems like just another hate speech detection paper at first glance, the research done in it is actually quite interesting.  

Because multimodal models have to understand both text and images, we first measured the "importance" the model gives to each using an Explainable AI method called Integrated Gradients.  We then performed ablation testing, removing either the image or textual modalities to see the impact on the models' performance - this told us whether images or text provided the most useful/meaningful information.  The models ended up paying much more attention (according to Integrated Gradients) to the image modality, but the textual modality in ablation testing actually turned out to be the more useful factor in determining hatefulness (according to ablation tests).  This suggests that more research can be done to encourage multimodal models to give additional emphasis on the textual component of a meme.  The results of the ablation testing also reinforce the idea that memes must be interpreted using both text and images - using only text or only images performed much worse than using both.

We also measured not only the performance of several multimodal models on classifying hateful memes, but also whether they were truly understanding the relationship between the text and image modalities, and whether they were able to generalize to new forms of hate.  For a multimodal model to successfully classify a hateful meme, it must learn "semantic grounding", or how each modality is affected by the context provided by the other.  For example, a meme with an image of a rose saying "you smell like this" is quite nice, while a meme with an image of a skunk saying the same thing is pretty mean.  
![Context in memes example](/assets/research/meme.png)   
Attention heads from the models were used to study semantic grounding.
To study performance and generalizability to novel forms of hate, we applied models trained only on traditional forms of hate to new hateful memes generated during the Covid-19 pandemic.  All models performed quite poorly, revealing that current SOTA multimodal models are unable to generalize effectively.

### - "Understanding and Analyzing COVID-19-related Online Hate Propagation Through Hateful Memes Shared on Twitter" (Accepted to ASONAM 2023)

### - "An Investigation of Large Language Models for Real-World Hate Speech Detection" (Accepted to ICMLA 2023)
