# COVID-19 Question Answering System (CORD-19 based)

## Project Overview

This project implements a **COVID-19 Question Answering (QA) System** that leverages state-of-the-art Natural Language Processing (NLP) techniques to retrieve accurate and reliable answers from the extensive CORD-19 dataset containing scientific articles related to COVID-19.

The system uses *RoBERTa*, a transformer-based QA model, combined with entity recognition via *SciSpaCy* and parallel processing to improve efficiency and accuracy. Additionally, answers are converted into natural language sentences and can be output as speech.

## Features

- **Paragraph-level search:** Improves precision over paper-level search by focusing on relevant paragraphs.
- **Entity indexing and matching:** Utilizes named entity recognition to index and quickly retrieve paragraphs related to query entities.
- **Pre-trained RoBERTa QA model:** Fine-tuned on COVID-19 annotated datasets to generate accurate answers.
- **Answer generation with summarization:** Uses Facebook’s `bart-large-cnn` model to convert extracted answers into coherent natural language sentences.
- **Text-to-speech output:** Implements `pyttsx3` to optionally deliver answers via speech.
- **Parallel processing:** Speeds up query handling by distributing computation.

## Dataset

- **CORD-19**: COVID-19 Open Research Dataset containing over 1,000,000 scholarly articles (400,000+ with full text) about COVID-19, SARS-CoV-2, and related coronaviruses [Source](https://www.kaggle.com/datasets/allen-institute-for-ai/CORD-19-research-challenge).

## Technology Stack

| Component                | Tool/Library                               |
| ------------------------ | ------------------------------------------ |
| NLP & QA Model           | RoBERTa (fine-tuned on COVID-QA dataset)   |
| Named Entity Recognition | SciSpaCy                                   |
| Paragraph Ranking        | spaCy similarity / cosine similarity       |
| Summarization            | Facebook's `bart-large-cnn` model        |
| Text-to-Speech           | `pyttsx3` Python library                 |
| Parallel Processing      | Python `multiprocessing` or equivalent   |
| Data Handling            | Pandas, JSON processing on CORD-19 dataset |

## Installation

1. Clone this repository:

```

git clone https://github.com/yourusername/covid19-qa-system.git
cd covid19-qa-system

```

2. Create and activate a virtual environment (recommended):

```

python -m venv venv
source venv/bin/activate  \# On Windows: venv\Scripts\activate

```

3. Install required packages:

```

pip install -r requirements.txt

```

4. Download the CORD-19 dataset from Kaggle and place it in the appropriate directory.

## Usage

Run the QA system and interactively enter your COVID-19 related question.

```

python run_qa_system.py

```

You will be prompted to:

- Enter your question.
- Choose whether to receive the answer as voice output (yes/no).

The system will return an accurate natural language answer sourced from the CORD-19 scientific literature.

## Project Structure

- `data/` - Preprocessed CORD-19 data and metadata
- `models/` - Pre-trained models and checkpoints (RoBERTa, BART summarizer)
- `src/` - Source code including entity extraction, paragraph ranking, QA, and TTS
- `run_qa_system.py` - Main executable script for running the system

## Results and Performance

- Improved query response time using parallel processing (under 5 minutes per query on sample data).
- Answers generated as natural language sentences outperform paper-level search results.
- Optional text-to-speech enables accessibility for users preferring auditory output.

## Limitations

- Answers rely on the English-only subset of the CORD-19 dataset.
- Entity recognition accuracy is challenged by biomedical terminology outside SpaCy's scope.
- Some queries may lack explicit source citations due to dataset limitations.
- The system is domain-specific and may not generalize to unrelated content.

## Future Work

- Integration with search engines and chatbots for broader accessibility.
- Use of APIs to enable real-time data retrieval and updating.
- Explore alternative parallel processing frameworks like PySpark for scalability.
- Extend multilingual support beyond English.

## References

- [RoBERTa Model for COVID-QA](https://huggingface.co/deepset/roberta-base-squad2-covid)
- [SciSpaCy Library](https://allenai.github.io/scispacy/)
- [Facebook’s bart-large-cnn Model](https://huggingface.co/facebook/bart-large-cnn)
- [CORD-19 Dataset](https://www.kaggle.com/datasets/allen-institute-for-ai/CORD-19-research-challenge)
- [Pyttsx3 Text-to-Speech](https://pypi.org/project/pyttsx3/)

## Authors

- Harpreet Kaur Hans (A1873328)
- Priyank Dave (A1843068)
- Chinmay Dharmik (A1855351)

## License

Specify your project license here (e.g., MIT License).

---

*This project was developed as part of the Natural Language Processing course, Tri1 2023.*
