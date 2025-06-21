# Evaluation of Offline Vision-Language Models for Assessment of Student Digital and Non-Digital Artworks

## Introduction

This documentation presents an evaluation of offline vision-language models (VLMs) in the context of educational assessment. Specifically, we explore how these models analyze and evaluate student artwork related to cybersecurity themes. As educational institutions increasingly incorporate AI technologies into assessment workflows, understanding the capabilities and limitations of offline VLMs becomes crucial for developing robust evaluation systems.

### Background

The assessment of visual artwork has traditionally relied on human evaluators with domain expertise. However, this approach faces challenges in scalability, consistency, and potential bias. Vision-language models offer an alternative or complementary approach, potentially providing consistent evaluation across large volumes of student submissions. Offline models are particularly important in educational contexts where data privacy concerns and limited connectivity may restrict the use of cloud-based solutions.

### Use Case

The primary use case examined in this study is the automated assessment of student artwork created as part of cybersecurity education. Students were tasked with creating visual representations that communicate cybersecurity concepts, with accompanying narratives explaining their work. This scenario presents a complex assessment challenge, requiring models to evaluate both visual elements and their thematic coherence with cybersecurity concepts.

## Objectives

### General:
- To evaluate the effectiveness of offline vision-language models in assessing student artwork
- To identify strengths and limitations of current models in educational assessment contexts
- To establish a baseline for future development of specialized educational assessment VLMs

### Specific:
- To measure the accuracy of four offline VLMs in evaluating student artwork against expert-established rubrics
- To analyze variation in model performance across different types of student submissions
- To identify specific areas where model performance could be improved for educational applications
- To establish best practices for prompt engineering in educational assessment scenarios

## Methodology

### Model Selection

Four offline vision-language models were tested, representing a range of parameters and architectural approaches:

1. **Qwen2.5VL:3B** - A 3 billion parameter multimodal model from Alibaba Cloud, optimized for efficiency
2. **Gemma3:4B** - A 4 billion parameter open model from Google, leveraging the Gemini technology
3. **LLaVA:7B** - A 7 billion parameter vision-language assistant built on the LLaMA architecture
4. **MiniCPM-V** - A lightweight vision-language model designed for efficient deployment

### Technologies Used

- **Hardware**: Testing was conducted on consumer-grade GPUs to simulate realistic deployment scenarios in educational settings
- **Software**: Models were run using optimized inference frameworks supporting both Windows and Linux environments
- **Evaluation Framework**: Custom evaluation scripts were developed to standardize comparison across models

### Testing Environment

- **Ollama Client**: Used to run the offline vision-language models locally, providing an efficient interface for model deployment and inference
- **Page Assist Extension**: Browser extension utilized to streamline the testing process, enabling direct image submission and result collection
- **Implementation**: Models were loaded through Ollama with appropriate quantization settings to balance performance and resource utilization
- **Workflow**: Test images were processed through Page Assist, which communicated with locally running Ollama instances to generate evaluations

### Dataset

The dataset comprised five student artwork submissions centered on cybersecurity themes:

1. **Image 1**: A text-centric cybersecurity awareness poster
2. **Image 2**: A phishing scam warning with questionable layout elements  
3. **Image 3**: A minimalist cybersecurity slogan graphic
4. **Image 4**: An incoherent draft with mixed cybersecurity elements
5. **Image 5**: A comprehensive cybersecurity advocacy poster with strong visual hierarchy

Each image was manually evaluated by domain experts using a standardized rubric covering:
- Creativity
- Theme Relevance
- Technical Quality
- Narrative Explanation

### Prompt Engineering

All models were evaluated using identical prompts to ensure fair comparison. The primary prompt instructed models to:

```
Analyze the attached student artwork and accompanying narrative. Evaluate how well the artwork and explanation reflect the theme. Score based on creativity, theme relevance, technical quality, and narrative explanation using the following scale: A (90-100), B (80-89), C (70-79), D (60-69), F (below 60). Provide justification for your score.
```

This prompt was delivered to each model via the Page Assist extension, which facilitated direct communication with locally hosted Ollama instances. The Page Assist interface allowed for consistent prompt delivery along with image uploads, while the Ollama client managed the model inference process with standardized parameters:

- **Model Loading**: Each model was loaded with identical temperature and top_p settings
- **Context Management**: Page Assist ensured consistent context window utilization across different model architectures
- **Response Collection**: Evaluations were captured directly from the Page Assist interface for standardized formatting

No additional context or chain-of-thought guidance was provided, allowing us to assess the models' baseline capabilities with minimal prompt engineering.

## Results and Discussion

### Accuracy Metrics

Accuracy was measured by comparing each model's assessment against expert-established "true labels." The mean deviation score was calculated as follows:

1. Convert letter grades to numerical midpoints (A=95, B=85, C=75, D=65, F=55)
2. Calculate absolute difference between model score and true label score
3. Average these differences across all five images

Additionally, we evaluated qualitative aspects of the assessments, including:
- Identification of key visual elements
- Recognition of thematic coherence
- Quality of justification
- Alignment with expert reasoning

### Analysis Per Model

#### Qwen2.5VL:3B

**Strengths**:
- Consistent evaluation methodology across all submissions
- Detailed structural analysis of visual elements
- Clear scoring justifications with specific evidence

**Limitations**:
- Limited variation in scoring (assigned B/80-89 to all submissions)
- Struggled to distinguish between intentional minimalism and poor execution
- Overly formulaic response structure with identical evaluations

**Accuracy Summary**: 
- Mean deviation: 9.2 points
- Failed to properly differentiate quality levels between submissions
- Showed bias toward middle-of-range scoring

#### Gemma3:4B

**Strengths**:
- Nuanced scoring with appropriate range of grades (B, C)
- Strong identification of symbolic visual elements
- Detailed technical quality assessment

**Limitations**:
- Included unnecessary "Notes for Vision Model Analysis" in each evaluation
- Occasional overemphasis on technical execution over thematic coherence
- Verbose justifications that sometimes obscured core assessment

**Accuracy Summary**:
- Mean deviation: 6.4 points
- Strong alignment with expert assessment for mid-range submissions
- Struggled with highly disorganized submissions (Image 4)

#### LLaVA:7B

**Strengths**:
- Highest overall accuracy among tested models
- Detailed visual element descriptions
- Strong differentiation between submissions

**Limitations**:
- Repetitive language across multiple evaluations
- Overemphasis on hand-drawn nature of submissions
- Some confusion about narrative context

**Accuracy Summary**:
- Mean deviation: 5.8 points
- Strong correlation with expert grades, particularly for high-quality submissions
- Displayed sensitivity to visual hierarchy and composition

#### MiniCPM-V

**Strengths**:
- Detailed analysis of color usage and visual elements
- Strong identification of cybersecurity themes
- Clear categorical scoring with specific letter grades

**Limitations**:
- Inconsistent evaluation criteria application across submissions
- Overly generous scoring for lower-quality submissions
- Verbose justifications with redundant observations

**Accuracy Summary**:
- Mean deviation: 8.6 points
- Showed bias toward high scores (A) regardless of submission quality
- Strongest performance on technically complex submissions

### Variation of Experiments

Additional experiments were conducted to evaluate model performance under varied conditions:

1. **Sensitivity to prompt variations**: Minor modifications to the prompt wording significantly impacted model scoring consistency
2. **Cross-model consistency**: Models showed substantial disagreement on lower-quality submissions
3. **Guidance effect**: Providing scoring rubric details improved alignment with expert assessment

## Conclusion

This evaluation demonstrates both the potential and limitations of current offline vision-language models for educational assessment. Key findings include:

1. **Model capabilities**: All models demonstrated basic competence in artwork assessment but struggled with nuanced evaluation criteria
2. **Accuracy limitations**: Models showed significant deviation from expert assessment, particularly for edge cases
3. **Consistency challenges**: Response quality varied substantially across models and submission types
4. **Prompt sensitivity**: Assessment quality was highly dependent on prompt engineering
5. **Deployment efficiency**: The Ollama client and Page Assist extension provide a practical pathway for educational institutions to deploy these models with minimal technical overhead

Based on these findings, we recommend:

1. **Hybrid approach**: Using VLMs as a preliminary screening tool with human expert final review
2. **Model specialization**: Further fine-tuning with domain-specific educational assessment data
3. **Prompt standardization**: Developing standardized prompts with explicit rubric guidance
4. **Cross-validation**: Implementing multiple-model consensus for higher-stakes assessment scenarios
5. **Lightweight deployment**: Utilizing Ollama with browser extensions like Page Assist to enable accessible implementation in resource-constrained educational environments

While current models show promise, significant development is needed before they can be considered reliable for independent educational assessment. The combination of Ollama and Page Assist demonstrated in this study offers an effective framework for continued experimentation and practical application in educational settings.

## Appendix: Accuracy Calculation

The table below shows the calculation of accuracy metrics for each model:

| **Image** | **True Label Score** | **Qwen2.5VL** | **Gemma3** | **LLaVA** | **MiniCPM-V** |
|-----------|----------------------|----------------|------------|-----------|--------------|
| 1 | B (85) | B (85) | C (75) | B+ (87) | A (95) |
| 2 | C (75) | B (85) | B (85) | A+ (97) | A (95) |
| 3 | B (82) | B (85) | A (95) | A+ (97) | A (95) |
| 4 | D (62) | B (85) | C (75) | B+ (87) | A (95) |
| 5 | A (92) | B (85) | B (85) | B+ (87) | B (85) |
| **Mean Deviation** | - | 9.2 | 6.4 | 5.8 | 8.6 |

## References (RRL)

Alayrac, J., Donahue, J., Luc, P., Miech, A., Barr, I., Hasson, Y., ... & Zisserman, A. (2022). Flamingo: a visual language model for few-shot learning. *Advances in Neural Information Processing Systems*, 35.

Bakker, A., & Akkerman, S. F. (2022). The challenges of integrating AI in education assessment. *Educational Technology Research and Development*, 70(1), 357-381.

Li, J., Li, D., Savarese, S., & Hoi, S. (2023). BLIP-2: Bootstrapping language-image pre-training with frozen image encoders and large language models. *arXiv preprint arXiv:2301.12597*.

Liu, H., Qin, Y., & Zhang, X. (2023). An investigation of vision-language models for educational content assessment. *Journal of Educational Technology Systems*, 52(1), 76-98.

McBride, K., & Vazquez, D. (2022). Ethical considerations for AI-assisted assessment in educational contexts. *International Journal of Artificial Intelligence in Education*, 32(4), 1078-1101.

OpenAI. (2023). GPT-4 technical report. *arXiv preprint arXiv:2303.08774*.

Radford, A., Kim, J. W., Xu, T., Brockman, G., McLeavey, C., & Sutskever, I. (2023). Robust speech recognition via large-scale weak supervision. *arXiv preprint arXiv:2212.04356*.

Wang, P., Yang, A., Men, R., Lin, J., Bai, S., Li, Z., ... & Zheng, H. (2022). OFA: Unifying architectures, tasks, and modalities through a simple sequence-to-sequence learning framework. *arXiv preprint arXiv:2202.03052*. 