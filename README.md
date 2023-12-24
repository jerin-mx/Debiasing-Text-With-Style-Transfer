# Debiasing Text With Style Transfer
Neutralize biases in text by transferring stylistic elements without compromising content.

- [CI/CD Pipeline Status](#cicd-pipeline-status)
- [Abstract](#abstract)
- [Dataset Description](#dataset-description)
- [Model Architectures and Implementations](#model-architectures-and-implementations)
- [Evaluation](#evaluation)
- [References](#references)

***

## CI/CD Pipeline Status

[![Debiasing Text CI/CD](https://github.com/RU-Insane/Debiasing-Text-With-Style-Transfer/actions/workflows/pipeline.yml/badge.svg?branch=main)](https://github.com/RU-Insane/Debiasing-Text-With-Style-Transfer/actions/workflows/pipeline.yml)

***

## Abstract

The project addresses bias in language by leveraging Text Style Transfer, focusing on converting biased language into neutral form while preserving content. The main model successfully transformed biased text into a neutral style, demonstrating the feasibility and effectiveness of text style transfer in mitigating bias. The approach to this problem is twofold: there was a successful development and implementation of a model that effectively transforms biased language into a more neutral form. Then, it involves a classification task where the model discerns between biased and neutral text categories for evaluation. Initial results show promising bias mitigation, with the BART model effectively neutralizing subjective language while retaining content. The STI and CPS scores from BERT-based evaluations provide quantitative insights into the efficacy of our approach. This report highlights the project's objective, methodology, and successful outcomes.

***

## Dataset Description

The **Wiki Neutrality Corpus (WNC)**, comprising 181,473 aligned sentences pre- and post-neutralization by English Wikipedia editors, serves as the primary data source. It’s a rich dataset, sourced from public domain revisions made between 2004 and 2019, provides a comprehensive foundation for the exploration into language neutrality and bias mitigation. One-word edits were selected from the dataset due to its considerable size (~56,000). This choice simplified the analysis, contrasting with the more complex and larger full version of the dataset. The dataset, accessible on Kaggle, is split into three segments: 90% for training, and 5% each for testing and validation. It includes raw and tokenized texts, with part-of-speech and syntactic parse tags.

***

## Model Architectures and Implementations:

  1. **LSTM-Based Baseline Model:**

  - **Architecture:** A custom LSTM sequence-to-sequence model designed for transforming biased text to a neutral form.
  - **Tokenization:** Utilizes the BERT tokenizer for converting text into token sequences, leveraging pre-trained word embeddings to capture contextual nuances.

  2. **BART Model - Main Style Transfer Model:**

  - **Architecture:** Implements the 'facebook/bart-base' variant, a Bidirectional and Auto-Regressive Transformer model sourced from Hugging Face. Known for high-quality text generation.
  - **Fine-Tuning and Tokenization:** Fine-tuned specifically for bias mitigation, BART's tokenizer converts text into token sequences, maintaining attention masks. Pre-trained embeddings capture contextual nuances effectively.

  3. **BERT Model for Classification Task:**

  - **Architecture:** Utilizes 'bert-base-uncased,' a deep bidirectional BERT variant from the Hugging Face Model Hub, with 12 layers, 768 hidden units, and 12 self-attention heads.
  - **Fine-Tuning and Tokenization:** Adapted for binary classification to distinguish biased from neutral texts. BERT's tokenizer processes text into token sequences, standardized to 128 tokens. Outputs probabilities for each class (0-neutral, 1-biased) using a softmax function. Pre-trained embeddings capture contextual nuances effectively.

***

## Evaluation

### Metrics:
Evaluation of text style transfer quality involves considering two key criteria: Style Strength (how well the generated text achieves the target style) and Content Preservation (the extent to which the generated text retains the semantic meaning of the source text).

### Challenges with Traditional Metrics:
Traditional metrics like BLUE score only count identical n-grams, leading to underestimation of performance as they may penalize semantically correct phrases differing in lexical form. Hence, reference-free evaluation methods align better with human judgments.

### Evaluation Methods:

  1. **Style Transfer Intensity (STI):**

  - **Approach:** Developed a custom formula equating STI to the accuracy of style transfer and the intensity of transfer from the original text.
  - **Methodology:** Used Earth Mover Distance (EMD) between probability distributions of source, predicted, and target texts generated by the BERT classification model.

  2. **Content Preservation Score (CPS):**
  
  - **Approach:** Dynamically calculated local, sentence-level feature importances using Integrated Gradients on a fine-tuned BERT subjectivity classifier.
  - **Methodology:** Determined style-independent versions of input and output sentences by removing stylistic elements, enabling accurate assessment of content preservation through embedding-based similarity.

### Results:
Analysis of STI and CPS on the baseline model showed better style transfer than BART. However, despite higher STI, the baseline model produced irrelevant output, leading to poor Content Preservation (CPS). BART excelled in CPS, preserving most meaning in the original texts while ensuring credible style transfer.

***

## References

1. [An Empirical Survey of the Effectiveness of Debiasing Techniques for
Pre-trained Language Models](https://arxiv.org/pdf/2110.08527.pdf)

2. [Automatically Neutralizing Subjective Bias in Text](https://arxiv.org/pdf/1911.09709.pdf)

3. [Evaluating Style Transfer for Text](https://arxiv.org/pdf/1904.02295.pdf)

***
