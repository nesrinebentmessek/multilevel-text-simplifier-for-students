# Text Simplification with Fine-Tuned T5 

This repository contains a complete pipeline for text simplification using a fine-tuned T5-small model. The project involves dataset preparation, exploratory data analysis (EDA), model fine-tuning, and evaluation. The goal is to simplify complex sentences while preserving meaning, making text more accessible.

## Dataset
**Data Source / Credit:**  
This dataset was obtained from [Simple–complex Sentence Pairs](https://tudatalib.ulb.tu-darmstadt.de/items/d58abcb2-e416-4fb8-b3eb-c689eb4075f6) 

The dataset was sourced from complex_simple.txt, a text file of aligned complex-simple sentence pairs, available at source link . Each complex sentence is followed by its simplified version, separated by blank lines.

The datasets are stored in the `/dataset` folder:
- `simplification_dataset.csv`: Raw parsed data from complex-simple pairs.
- `simplification_dataset_clean.csv`: Cleaned version (removed empty/NA entries) for model training .
- `with_readability.csv`: Cleaned data augmented with FK and FRE scores for exploratory data analysis
- `train_dataset.csv`: Training split (90% of data).
- `val_dataset.csv`: Validation split (10% of data).

## Project Overview

Text simplification is a natural language processing task that rewrites complex text into simpler forms without losing essential information. This project fine-tunes the T5-small model from Hugging Face on a custom dataset of complex-simple sentence pairs.

Key steps:
- Parse and clean raw text files into a structured dataset.
- Perform EDA to analyze sentence lengths and readability scores.
- Preprocess data, split into train/validation, and fine-tune the model.
- Evaluate the model using BLEU and ROUGE metrics, with a demo for inference.

The repository includes Jupyter notebooks for each stage and the processed datasets.

## Notebooks

The project is divided into four Jupyter notebooks:

1. **[01_dataset_preparation_and_cleaning.ipynb](01_dataset_preparation_and_cleaning.ipynb)**: Parses raw text files into CSV, cleans data (removes NA/empty entries), and adds readability scores (FK and FRE) using .
   
2. **[02_explaratory_data_analysis.ipynb](02_explaratory_data_analysis.ipynb)**: Performs EDA, including sentence length distributions and readability comparisons. Visualizes how simplification reduces complexity (e.g., lower FK, higher FRE).

3. **[03_preprocessing_and_fine_tuning.ipynb](03_preprocessing_and_fine_tuning.ipynb)**: Cleans text further, splits into train/test, tokenizes with T5 tokenizer, and fine-tunes T5-small using Hugging Face's `Seq2SeqTrainer`. Training insights: Low validation loss indicates good generalization.

4. **[04_evaluation.ipynb](04_evaluation.ipynb)**: Generates predictions on validation samples, evaluates with BLEU and ROUGE, and includes a demo for interactive simplification.

**Note**: Some notebook JSON structures were modified to resolve GitHub rendering issues. The core code and logic remain intact. 

## Results

- **BLEU Score:** 0.54 → Indicates good overlap between model predictions and reference simplifications; much better than typical scores (0.2–0.4) for text generation tasks.  
- **ROUGE Scores:**  
  - ROUGE-1: 0.73  
  - ROUGE-2: 0.60  
  - ROUGE-L: 0.70  
  These high scores show the model preserves key words, phrases, and sentence structure effectively.

## Example Outputs

Input: "The Yowa era, marked by famine, ends in Japan."

Simplified Output: "The Yowa era ends in Japan."

Input: "She now has an album and a huge hit single, which topped the charts and attracted millions of views."

Simplified Output: "She now has an album and a huge hit single."

Input: "It was here that he composed Messiah, Zadok the Priest and Music for the Royal Fireworks."

Simplified Output: "He composed Messiah, Zadok the Priest and Music for the Royal Fireworks."

