# ResearchLens AI

ResearchLens AI is an AI-assisted research-paper exploration project designed to support semantic literature search, research-gap exploration, paper recommendations, and Sustainable Development Goal (SDG) analysis.

## Features

- Semantic search using Sentence Transformers and FAISS
- Research-gap exploration
- Research-paper recommendations
- SDG analysis
- OpenAlex data collection
- BM25 and semantic retrieval comparison

## Technologies Used

- **Python** — core programming language
- **Streamlit** — interactive application interface
- **Sentence Transformers** — text embeddings for semantic search
- **FAISS** — vector similarity search
- **BM25** — keyword-based retrieval comparison
- **OpenAlex** — research-paper metadata source
- **Pandas** — data processing

## Dataset

The primary dataset is:

`data/research_papers_real.csv`

The dataset contains 2,200 records across 10 research domains. The publication dates range from 2020-01-01 to 2026-05-20. These dates represent publication dates, not the dataset collection period.

**Data source:** OpenAlex.

Additional CSV files are included in the `data/` directory for sample, domain-specific, and testing purposes.

## Project Structure

```text
ResearchLens-AI/
│
├── app.py
├── compare_retrieval.py
├── requirements.txt
├── README.md
├── ResearchLens AI_POSTER.png
│
├── data/
│   ├── agriculture_papers.csv
│   ├── healthcare_papers.csv
│   ├── openalex_test.csv
│   ├── research_gap_dataset.csv
│   ├── research_papers_real.csv
│   └── research_papers_sample.csv
│
└── modules/
    ├── embeddings.py
    ├── gap_detection.py
    ├── merge_dataset.py
    ├── openalex_collector.py
    ├── preprocess.py
    ├── recommendation.py
    ├── sdg_analysis.py
    ├── search.py
    └── semantic_search.py
```

## Installation

### 1. Clone the repository

```powershell
git clone https://github.com/RESHAAL/ResearchLens-AI.git
cd ResearchLens-AI
```

### 2. Create a virtual environment

```powershell
python -m venv .venv
```

### 3. Activate the environment

For Windows PowerShell:

```powershell
.\.venv\Scripts\Activate.ps1
```

### 4. Install dependencies

```powershell
python -m pip install -r requirements.txt
```

## Running the Application

Start the Streamlit application:

```powershell
python -m streamlit run app.py
```

The application will open in your browser. If it does not open automatically, navigate to:

```text
http://localhost:8501
```

Use the application interface to explore research papers and the available project features.

## Retrieval Comparison Experiment

The project includes a preliminary comparison between BM25 and semantic retrieval.

Run the experiment:

```powershell
python compare_retrieval.py
```

The script writes its results to:

`retrieval_comparison_results.csv`

The `Relevant` column requires manual assessment. The experiment is preliminary, and the two methods currently use different candidate-generation procedures. Therefore, the results should not be interpreted as a controlled, apples-to-apples benchmark.

## Preliminary Evaluation Results

The preliminary evaluation used 5 research queries, with 10 retrieved results per query for each method, resulting in 100 result rows.

| Metric | BM25 | Semantic Search (MiniLM + FAISS) |
|---|---:|---:|
| Mean Precision@10 | 0.20 | 0.26 |
| Mean nDCG@10 | 0.38 | 0.69 |

These results are based on preliminary, title-based relevance judgments and have not been independently validated.

On this small query set, semantic search obtained higher mean Precision@10 and nDCG@10 than BM25. These results do not establish general superiority of one retrieval method over the other.

Detailed per-query metrics are available in:

`retrieval_metrics.csv`

### Evaluation Limitations

- Only five research queries were evaluated.
- Relevance labels require verification using paper titles and abstracts.
- The methods use different candidate-generation procedures; the comparison is not controlled.
- Latency measurements are preliminary and should be repeated with warm-up runs and multiple trials.
- Recall is not reported because the total number of relevant papers per query has not been established.

Further evaluation with a larger query set, verified relevance judgments, and controlled retrieval procedures is required.

## Configuration and Models

Keep secrets and credentials in a local `.env` file. Do not commit this file to the repository.

Model artifacts may be excluded through `.gitignore` and may need to be regenerated when running the project in a new environment.

## Limitations

ResearchLens AI is an exploratory research-support project. Its outputs depend on the available dataset, metadata quality, retrieval methods, and relevance judgments.

Research-gap suggestions and retrieval results should be reviewed by researchers before being used to draw academic conclusions.

## Conclusion

ResearchLens AI brings together semantic literature retrieval and research-paper exploration in an interactive application. The project provides a foundation for exploring relevant literature, examining potential research gaps, and supporting further research through data-driven retrieval techniques.

The preliminary evaluation indicates promising results for semantic retrieval on the tested queries, while further validation is needed to assess its performance more broadly.
