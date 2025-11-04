# Automatic Hindi MCQ’s Generation System

This project focuses on generating **Multiple Choice Questions (MCQs)** automatically from Hindi text using a combination of **mBART** for question–answer generation and **FastText** for distractor (wrong option) generation. It aims to simplify assessment creation for Hindi educational content.

## Table of Contents
- [Overview](#overview)
- [Features](#features)
- [Installation](#installation)
- [Usage](#usage)
- [Model](#model)
- [Dataset](#dataset)
- [Technologies](#technologies)
- [Contributing](#contributing)

## Overview
This project implements an **end-to-end MCQ generation system** in Hindi.  
It takes a Hindi paragraph as input, extracts context, and generates:
1. A relevant **question–answer pair** using a fine-tuned **mBART model**.  
2. **Distractors** (incorrect but similar options) using **FastText word embeddings**.  

The result is a complete multiple-choice question that can be directly used in quizzes, e-learning platforms, or educational assessments.

## Features
- Automatically generates **Hindi questions and answers** from text.  
- Produces **distractors** (wrong options) using semantic similarity with FastText.  
- Fine-tuned **mBART model** for context-aware QA generation.  
- End-to-end pipeline — from **data preprocessing → model training → MCQ generation**.  
- Deployed using a **Gradio web interface** for real-time interaction.  
- Generates **multiple question variations** using beam search and sampling.

## Installation
1. Clone the repository:
   ```bash
   git clone https://github.com/your-username/Automatic-Hindi-MCQ-Generation.git
   cd Automatic-Hindi-MCQ-Generation

## Usage
1. **Prepare the Dataset**
    Run the script to clean, normalize, and split the Hindi QA     dataset:  
    python QA.py
2.**Train the Model** 
    Fine-tune the mBART model on the Hindi QA dataset:
    python QA.py
    The script automatically saves the trained model as:
    ./mbart_hindi_qa_model
3. **Launch the Gradio App**
    Run the application to generate questions and MCQs interactively:
    python QA.py

## Model
Base Model: **facebook/mbart-large-50-many-to-many-mmt**
-Architecture: Encoder–Decoder Transformer
-Encoder: Bidirectional (context understanding)
-Decoder: Auto-regressive (text generation)
-Language: Hindi-to-Hindi fine-tuning
-Training Setup:
-Optimizer: AdamW
-Learning Rate: 3e-5
-Epochs: 5
-Batch Size: 4
-Framework: PyTorch + Hugging Face Transformers
**Distractor Generation (FastText)**
-Embedding Model: **FastText** (Hindi pre-trained model)
**Approach:**
-Convert the correct answer into a vector using FastText.
-Find nearest neighbors in vector space via cosine similarity.
-Select top 3–4 semantically similar but incorrect words as distractors.
-This ensures distractors like **“मुंबई, चेन्नई, कोलकाता” for the correct answer “दिल्ली”**.

## Dataset
-Source: Hindi textbook QA dataset (QA_Dataset_Hindi_Final.csv)
**Processing Steps:**
-Removal of English rows and empty cells.
-Unicode normalization and whitespace cleaning.
-Length-based filtering for Seq2Seq training.
-Split: 80% Train, 10% Validation, 10% Test
**Input Format**:
-input_text  →  "context: <Hindi paragraph>"
-target_text →  "question: <Hindi question> answer: <Hindi answer>"

## Technologies
-Python
-PyTorch
-Hugging Face Transformers
-FastText
-Gradio Interface
-Pandas, scikit-learn
-mBART (Multilingual BART)

## Contributing
Contributions are welcome!
If you’d like to improve question generation, enhance distractor logic, or expand the dataset, feel free to open an issue or submit a pull request.

## Author 
**Mayank Narwal**
**mayanknarwal0506@gmail.com**