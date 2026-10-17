# Déjà Code — Semantic Search for Competitive Programming

Déjà Code is a natural-language search system that helps users discover relevant competitive programming problems by describing what they want to solve.

Instead of relying exclusively on exact keyword matches, the system uses semantic search to identify problems with similar meanings. A TF-IDF-based retrieval method is also implemented as a baseline for comparison.

## Quick Links

- **[Open Notebook in Google Colab](https://colab.research.google.com/github/shyamgayke/Deja_Code/blob/main/D%C3%A9j%C3%A0_Code.ipynb)**
- **[View Source Notebook](https://github.com/shyamgayke/Deja_Code/blob/main/D%C3%A9j%C3%A0_Code.ipynb)**
- **[View Dataset](https://github.com/shyamgayke/Deja_Code/blob/main/questions.csv)**

## Features

- **Natural-language search:** Find programming problems by describing their requirements in your own words.
- **Semantic retrieval:** Use sentence embeddings to identify problems with similar meanings.
- **TF-IDF baseline:** Compare semantic search with traditional keyword-based retrieval.
- **Text preprocessing:** Clean HTML-formatted problem statements before indexing.
- **Retrieval evaluation:** Evaluate search results using Precision@5, Recall@5, and Mean Reciprocal Rank (MRR).
- **Interactive interface:** Search through a Gradio interface and view ranked problems, difficulty levels, similarity scores, and problem links.
- **Automatic dataset loading:** Download the dataset directly from GitHub instead of manually uploading the CSV to Colab.

## Technology Stack

| Component | Technology |
|---|---|
| Programming language | Python |
| Data processing | Pandas, NumPy |
| HTML preprocessing | BeautifulSoup |
| Keyword retrieval | Scikit-learn TF-IDF |
| Semantic embeddings | Sentence Transformers |
| Deep learning framework | PyTorch |
| User interface | Gradio |
| Development environment | Google Colab |

## Dataset

The project uses a dataset of competitive programming problems containing fields such as:

- `QCode` — problem identifier
- `Title` — problem title
- `level` — problem difficulty
- `link` — problem URL
- `statement` — problem description

**Dataset file:** [`questions.csv`](https://github.com/shyamgayke/Deja_Code/blob/main/questions.csv)

The notebook loads the dataset from the following raw GitHub URL:

```text
https://raw.githubusercontent.com/shyamgayke/Deja_Code/main/questions.csv
```

Problem statements may contain HTML markup, which is cleaned during preprocessing.

## How It Works

The system follows a retrieval pipeline that transforms problem statements into searchable representations and ranks them against a user's query.

### 1. Data Loading

The dataset is loaded directly from GitHub using Pandas. This makes the notebook easier to reproduce without manually uploading the dataset each time a new Colab runtime starts.

### 2. Text Preprocessing

BeautifulSoup extracts readable text from HTML-formatted problem statements. HTML entities are decoded, scripts and styles are removed, and whitespace is normalized.

Each problem's title is combined with its cleaned statement to create the text used for retrieval.

### 3. TF-IDF Keyword Retrieval

TF-IDF represents each problem as a sparse numerical vector based on the importance of its terms.

Cosine similarity is used to rank problems according to their lexical similarity to the user's query.

This method provides a traditional keyword-based baseline against which semantic retrieval can be compared.

### 4. Semantic Search

The project uses the pretrained `sentence-transformers/all-MiniLM-L6-v2` model to encode problem descriptions and user queries into dense vector embeddings.

The problem embeddings are normalized, allowing dot products to calculate cosine similarity efficiently.

Problems are ranked according to their semantic similarity to the query, helping retrieve relevant results even when the query and problem statement use different words.

**Note:** The model is pretrained. It is not trained from scratch or fine-tuned on the project dataset.

### 5. Retrieval Evaluation

The notebook evaluates retrieval performance using three metrics:

- **Precision@5:** The proportion of the top five retrieved problems that are relevant.
- **Recall@5:** The proportion of known relevant problems retrieved in the top five results.
- **Mean Reciprocal Rank (MRR):** Measures how highly the first relevant result appears in the ranking.

Evaluation uses a set of natural-language queries and manually specified relevant problem codes.

The reliability of these metrics depends on the accuracy and coverage of the relevance labels.

### 6. Interactive Search Interface

Gradio provides an interface for entering natural-language queries and exploring the ranked results.

Depending on the query and selected options, users can inspect problem titles, difficulty levels, similarity scores, and links to the original problems.

## Project Structure

```text
Deja_Code/
├── Déjà_Code.ipynb
├── README.md
├── questions.csv
└── requirements.txt
```

## Getting Started

### Prerequisites

- A Google account to use Google Colab
- Internet access to download the dataset and pretrained model
- The required Python dependencies

A GPU-enabled Colab runtime is recommended, although a GPU is not strictly required for this dataset's size.

### Run the Project

1. Open the [Déjà Code notebook in Google Colab](https://colab.research.google.com/github/shyamgayke/Deja_Code/blob/main/D%C3%A9j%C3%A0_Code.ipynb).
2. Run the notebook cells from top to bottom, starting with the dependency installation cell.
3. The dataset is downloaded automatically from GitHub.
4. The problem statements are cleaned and prepared for retrieval.
5. The TF-IDF index is created.
6. The pretrained Sentence Transformer is loaded and problem embeddings are generated.
7. Run the evaluation cell to compare retrieval methods.
8. Run the final cell to launch the Gradio interface.
9. Enter a natural-language query and explore the retrieved problems.

The dataset does not need to be uploaded manually each time the notebook is run.

## Dependencies

The primary dependencies are listed in `requirements.txt`:

```text
numpy
pandas
beautifulsoup4
scikit-learn
sentence-transformers
torch
gradio
```

The notebook's installation cell can install the required packages in a fresh Colab runtime.

## Limitations

- Semantic similarity does not guarantee an exact match to the user's intent.
- Only a truncated portion of each problem statement is used to generate semantic embeddings, which may omit important constraints or details.
- Search quality depends on the dataset's coverage and the quality of its problem descriptions.
- Specialized competitive programming terminology may not always be interpreted correctly.
- The initial evaluation set is small, so its results should be considered preliminary.
- Manually specified relevance labels can affect the evaluation metrics and should be verified before drawing strong conclusions.

## Future Improvements

- Expand the evaluation set with more manually verified queries and relevant problem codes.
- Improve ranking by combining lexical and semantic retrieval.
- Cache and reuse embeddings to reduce repeated computation.
- Incorporate problem tags, constraints, and algorithm categories into retrieval.
- Improve difficulty filtering and ranking for algorithm-specific queries.
- Evaluate performance on a larger and more diverse set of natural-language queries.

## Project Status

Déjà Code is a prototype of a semantic search system for competitive programming problems. It combines a traditional keyword-based baseline, pretrained semantic embeddings, retrieval evaluation, and an interactive search interface.

## Author

**Shyam Gayke**

GitHub: [@shyamgayke](https://github.com/shyamgayke)

**Repository:** [shyamgayke/Deja_Code](https://github.com/shyamgayke/Deja_Code)
