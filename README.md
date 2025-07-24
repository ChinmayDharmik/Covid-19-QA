# COVID-19 Question Answering System (CORD-19 based)

## Project Overview

This project implements a **COVID-19 Question Answering (QA) System** that leverages state-of-the-art Natural Language Processing (NLP) techniques to retrieve accurate and reliable answers from the extensive CORD-19 dataset containing scientific articles related to COVID-19.

The system uses *RoBERTa*, a transformer-based QA model, combined with entity recognition via *SciSpaCy* and parallel processing to improve efficiency and accuracy. Additionally, answers are converted into natural language sentences and can be output as speech.



## Features

* **Paragraph-Level Search**: Conducts searches at the paragraph level for higher precision compared to paper-level searches[^1].
* **Entity-Based Context Retrieval**: Uses `scispaCy` to identify entities in the user's question and matches them with paragraphs in the dataset to build a relevant context[^1].
* **Transformer-Based QA**: Employs a `RoBERTa` model fine-tuned for COVID-related questions to accurately extract answers from the context[^1].
* **Natural Language Generation**: Converts the model's raw text snippet into a complete, human-readable sentence using a `BART` summarization model[^1].
* **Text-to-Speech**: Includes an optional feature to read the final answer aloud using the `pyttsx3` library[^1].
* **Optimized Performance**: Utilizes parallel processing to reduce query handling time and improve system efficiency[^1].


## System Architecture

The system follows a multi-stage pipeline to process a user query and generate an answer[^1]:

1. **Data Ingestion \& Preprocessing**: The CORD-19 dataset is loaded, and articles are filtered to include only English-language papers published since 2019. The text is cleaned by removing irrelevant elements like links, citations, and stop words[^1].
2. **Entity Indexing**: `scispaCy` is used to perform Named Entity Recognition (NER) on the entire corpus. An index is created that maps each entity to the paragraphs where it appears[^1].
3. **Paragraph Ranking**: When a user submits a question, the system extracts entities from the query. It uses the entity index to retrieve all paragraphs containing a subset of these entities. These paragraphs are then ranked by their similarity to the query using `spaCy`'s similarity function[^1].
4. **Question Answering**: The top-ranked paragraphs are concatenated to form the context. The question and context are passed to the `RoBERTa` model, which extracts a text snippet containing the most likely answer[^1].
5. **Answer Generation**: The extracted snippet is converted into a full sentence. This is achieved by masking the "wh-" word (like "what" or "who") in the original question and using the `bart-large-cnn` model to generate a complete statement[^1].
6. **Voice Output**: If requested by the user, the final answer sentence is converted to speech[^1].

[image:1]

## Dataset

The system is built on the **COVID-19 Open Research Dataset (CORD-19)**. This is a comprehensive resource of over one million scholarly articles, including more than 400,000 with full text, focused on COVID-19, SARS-CoV-2, and related coronaviruses[^1]. For this project, only articles in PDF format were used[^1].

## Technologies Used

* **Core Models**:
    * **QA**: `RoBERTa` (deepset/roberta-base-squad2-covid) fine-tuned on a COVID-QA dataset[^1].
    * **NLP/Entity Recognition**: `spaCy` and `scispaCy`[^1].
    * **Answer Generation**: `BART` (facebook/bart-large-cnn)[^1].
* **Libraries**:
    * `pandas` for data manipulation[^2].
    * `pyttsx3` for text-to-speech functionality[^1].
    * `Hugging Face Transformers` for model integration[^1].


## Setup and Installation

1. **Clone the repository:**

```bash
git clone https://github.com/ChinmayDharmik/Covid-19-QA.git
cd cord19-qa-system
```

2. **Install dependencies:**
(It is recommended to create a virtual environment first.)

```bash
pip install -r requirements.txt
```

*Note: A `requirements.txt` file would need to be created containing libraries such as `pandas`, `torch`, `transformers`, `spacy`, `scispacy`, and `pyttsx3`.*
3. **Download models and data:**
    * Download the required `spaCy` and `scispaCy` models.
    * Download the CORD-19 dataset and place it in the designated data directory. The code expects a `metadata.csv` file and the `document_parses` directory[^2].

## Usage

Run the main Jupyter Notebook or Python script. The system will prompt you to enter a question and then ask if you want the answer to be spoken aloud[^1].

1. Run the Jupyter File.
2. At the prompt, type your question about COVID-19.
3. You will be asked if you want the answer dictated. Type `y` for yes or `n` for no.
4. The system will process the query and print the answer in natural language. If selected, it will also read the answer out loud[^1].

## Limitations

* **Source Uncertainty**: The system may not always be able to provide a specific citation for its answers due to the aggregation of information from multiple paragraphs[^1].
* **Training Data Bias**: The model's accuracy is dependent on the training data. Biases in the annotated data may affect performance on certain topics or question types[^1].
* **Domain Specificity**: The system is trained exclusively on English-language scientific literature from the CORD-19 dataset. Its effectiveness on unstructured, non-scientific, or multilingual data has not been tested[^1].
* **Ground Truth**: The CORD-19 dataset lacks a predefined ground truth for QA tasks, making model evaluation challenging[^1].


## Future Work

* **Integration**: The system could be integrated with chatbots or search engines via APIs to make scholarly information more accessible[^1].
* **Scalability**: `PySpark` and `Spark NLP` could be used to enhance parallel processing capabilities, improve efficiency, and handle even larger datasets[^1].
* **Broader Data Sources**: The system could be expanded to include other trusted medical data sources beyond CORD-19[^1].


---

*This project was developed as part of the Natural Language Processing course, Tri1 2023.*
