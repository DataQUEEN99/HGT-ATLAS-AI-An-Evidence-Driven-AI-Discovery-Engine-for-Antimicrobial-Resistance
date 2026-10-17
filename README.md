#  HGT-ATLAS AI
### An Evidence-Driven AI Discovery Engine for Antimicrobial Resistance

**HGT-ATLAS AI** is a bioinformatics research exploration platform designed to help researchers investigate horizontal gene transfer (HGT), antimicrobial resistance, bacterial organisms, resistance-associated genes, and mobile genetic elements through scientific literature analysis and knowledge graph visualization.

The platform combines PubMed literature retrieval, biomedical entity extraction, graph-based relationship exploration, TF-IDF evidence retrieval, candidate-link ranking, and research data auditing in an interactive web application.

> **Research integrity notice:** This project is a research prototype. Graph edges represent sentence-level co-occurrence, not confirmed biological interactions. Candidate links are exploratory leads, not validated discoveries. The application must not be used to make clinical decisions.

---

##  Table of Contents

- [Project Overview](#-project-overview)
- [Problem Statement](#-problem-statement)
- [Objectives](#-objectives)
- [Key Features](#-key-features)
- [Technology Stack](#-technology-stack)
- [System Architecture](#-system-architecture)
- [Project Workflow](#-project-workflow)
- [Project Structure](#-project-structure)
- [Installation](#-installation)
- [Running the Application](#-running-the-application)
- [How to Use](#-how-to-use)
- [Knowledge Graph Methodology](#-knowledge-graph-methodology)
- [Machine Learning and NLP Methodology](#-machine-learning-and-nlp-methodology)
- [Evaluation Strategy](#-evaluation-strategy)
- [Data Sources](#-data-sources)
- [Example Research Questions](#-example-research-questions)
- [Current Limitations](#-current-limitations)
- [Future Enhancements](#-future-enhancements)
- [Responsible Research and Data Usage](#-responsible-research-and-data-usage)
- [Troubleshooting](#-troubleshooting)
- [Contributing](#-contributing)
- [License](#-license)
- [Author](#-author)

---

##  Project Overview

Antimicrobial resistance (AMR) is a major global public health challenge. The spread of resistance-associated genes between bacteria and through mobile genetic elements is an important area of microbiological research.

Scientific evidence relevant to AMR and HGT is distributed across research publications, abstracts, genomic studies, and biological databases. Identifying useful relationships across these sources can require extensive literature review.

HGT-ATLAS AI provides an interactive environment for organizing and exploring this information.

The current prototype enables users to:

1. Retrieve research publications from PubMed.
2. Import research abstracts through CSV files or manual input.
3. Extract entities from a predefined biomedical vocabulary.
4. Construct a graph of entities mentioned together in scientific sentences.
5. Retrieve potentially relevant evidence passages using TF-IDF.
6. Rank candidate links using graph-based structural features.
7. Explore detected entities and their neighboring nodes.
8. Audit dataset coverage and export results as CSV files.

The long-term vision is to develop an evidence-grounded scientific discovery assistant that helps researchers formulate research questions while preserving the connection between every displayed claim and its original source.

##  Problem Statement

Research into horizontal gene transfer and antimicrobial resistance involves large amounts of scientific literature containing information about genes, organisms, plasmids, resistance phenotypes, and biological mechanisms.

Traditional manual workflows can make it difficult to organize this evidence, explore connections between entities, and prioritize potentially interesting research questions.

HGT-ATLAS AI addresses this challenge by combining literature retrieval, entity extraction, graph analysis, and evidence search in one application.

The system is designed to support researchers in exploring available evidence rather than replacing scientific judgment or experimental validation.

##  Objectives

- Develop an interactive bioinformatics research application.
- Retrieve and organize relevant scientific publications.
- Extract selected biomedical entities from research text.
- Represent sentence-level entity co-occurrences as a graph.
- Explore relationships through interactive visualization.
- Retrieve relevant evidence passages for research questions.
- Rank exploratory candidate links using graph-based methods.
- Evaluate dataset completeness and extraction coverage.
- Preserve publication identifiers and source links wherever available.
- Establish a foundation for future biomedical NLP and knowledge graph research.

##  Key Features

### 1. PubMed Literature Search

Search PubMed using user-defined queries and import available publication metadata.

The application can retrieve:

- Publication titles
- PubMed identifiers (PMIDs)
- Abstracts, when available
- Publication dates, when available
- Source URLs

### 2. CSV and Manual Data Import

Import research records from CSV files or add abstracts manually.

Supported CSV column names include:

- `title`
- `abstract`
- `pmid`
- `id`
- `publication_date`
- `source`
- `url`

Column names such as `paper_title`, `text`, `publication_id`, and `source_url` are also recognized by the current import implementation.

### 3. Biomedical Entity Extraction

A dictionary-based extraction system identifies selected terms associated with:

- Horizontal gene transfer
- Antimicrobial resistance
- Bacterial species
- Plasmids and mobile genetic elements
- Selected resistance-associated genes
- Genomic and microbiome research

The vocabulary is configurable and can be expanded as the project develops.

### 4. Interactive Knowledge Graph

The application represents detected entities as nodes and sentence-level co-occurrences as edges.

The graph provides a visual way to inspect entities and their connections within the imported dataset.

Users can explore:

- Detected entities
- Neighboring entities
- Graph structure
- Connected components
- Frequently connected nodes

**Important:** An edge only means that two detected terms appeared in the same sentence. It does not establish causation, gene transfer, gene carriage, or a confirmed biological interaction.

### 5. Evidence Search

The evidence search module uses TF-IDF vectorization to retrieve sentences relevant to a research question.

It displays:

- Retrieved sentences
- Associated publication titles
- Available source links
- Retrieval similarity scores

These scores measure textual retrieval similarity. They are not probabilities that a scientific claim is true.

### 6. Candidate-Link Ranking

The application uses the Adamic–Adar graph metric to identify pairs of nodes that share graph neighbors.

This method can help explore the structure of the current graph.

Candidate links should be interpreted as exploratory leads. They may already be known, unsupported, or caused by incomplete data or extraction errors.

### 7. Entity Explorer

The entity explorer provides a table of detected entities, their record mentions, graph degrees, and neighboring nodes.

This helps researchers identify frequently occurring terms and navigate the graph.

### 8. Dataset Audit

The audit module reports basic data-quality indicators, including:

- Total number of records
- Records containing abstracts
- Records without abstracts
- Duplicate publication identifiers
- Records with source URLs
- Number of detected entities
- Number of graph edges

### 9. CSV Export

The application supports exporting:

- Imported publication records
- Detected entities and graph neighborhoods
- Candidate-link rankings
- Dataset audit results

These exports can support further analysis in Python, Excel, or other research tools.

---

## 🛠️ Technology Stack

| Technology | Purpose |
|---|---|
| Python | Main programming language |
| Gradio | Interactive web interface |
| Pandas | Data processing and CSV handling |
| Requests | PubMed API communication |
| XML ElementTree | Parsing PubMed XML responses |
| NetworkX | Knowledge graph construction and analysis |
| Plotly | Interactive graph visualization |
| Scikit-learn | TF-IDF text retrieval and cosine similarity |
| Regular expressions | Baseline biomedical term extraction |

The current implementation is intentionally lightweight so that the prototype can run in Google Colab or a Python notebook without a separate frontend or database server.

## System Architecture

```text
                  ┌─────────────────────────┐
                  │   Research Data Sources │
                  │ PubMed / CSV / Text     │
                  └────────────┬────────────┘
                               │
                               ▼
                  ┌─────────────────────────┐
                  │   Data Ingestion Layer  │
                  │ Validation / Deduplication│
                  └────────────┬────────────┘
                               │
                               ▼
                  ┌─────────────────────────┐
                  │ Biomedical Entity       │
                  │ Extraction              │
                  └────────────┬────────────┘
                               │
                               ▼
                  ┌─────────────────────────┐
                  │ Knowledge Graph         │
                  │ NetworkX                │
                  └────────────┬────────────┘
                               │
             ┌─────────────────┼────────────────┐
             ▼                 ▼                ▼
    ┌────────────────┐ ┌──────────────┐ ┌────────────────┐
    │ Evidence Search│ │ Graph Ranking│ │ Entity Explorer│
    │ TF-IDF         │ │ Adamic-Adar  │ │ Graph Analysis │
    └────────┬───────┘ └──────┬───────┘ └───────┬────────┘
             └─────────────────┼────────────────┘
                               ▼
                  ┌─────────────────────────┐
                  │ Gradio Research UI      │
                  │ Visualization / Exports │
                  └─────────────────────────┘
```

##  Project Workflow

### Step 1: Data Collection

Retrieve research abstracts from PubMed or import an existing CSV dataset.

### Step 2: Data Preparation

Normalize text, standardize record fields, and remove duplicate records according to the current deduplication rules.

### Step 3: Entity Extraction

Match selected biomedical terms against publication titles and abstracts.

### Step 4: Graph Construction

Create nodes for detected entities and connect entities that occur in the same sentence.

### Step 5: Evidence Retrieval

Use TF-IDF and cosine similarity to identify sentences that are textually relevant to a research question.

### Step 6: Candidate-Link Ranking

Use graph structure to rank selected pairs of entities for further exploration.

### Step 7: Data Auditing and Export

Review data coverage and export records, entity reports, candidate links, and audit results.

---

##  Project Structure

The current single-cell implementation does not require a multi-file repository. A recommended GitHub structure for future development is:

```text
HGT-ATLAS-AI/
│
├── README.md
├── requirements.txt
├── .gitignore
├── LICENSE
│
├── app/
│   ├── main.py
│   ├── config.py
│   ├── ingestion.py
│   ├── entity_extraction.py
│   ├── graph_builder.py
│   ├── evidence_search.py
│   ├── candidate_ranking.py
│   └── data_audit.py
│
├── data/
│   ├── samples/
│   └── annotations/
│
├── experiments/
│   ├── baseline_evaluation.py
│   └── evaluation_results.csv
│
├── tests/
│   ├── test_ingestion.py
│   ├── test_extraction.py
│   ├── test_graph.py
│   └── test_retrieval.py
│
└── docs/
    ├── architecture.md
    ├── methodology.md
    └── limitations.md
```

This is a proposed future structure. The current single-cell code does not automatically create these files.

---

##  Installation

### Option 1: Google Colab

The easiest way to run the current prototype is Google Colab.

1. Open Google Colab.
2. Create a new notebook.
3. Paste the complete single-cell application code into one code cell.
4. Run the cell.
5. Wait for the required packages to install.
6. Open the Gradio application link displayed in the output.

The code includes a package installation command, so a separate installation step is not required.

### Option 2: Local Python Environment

Use Python 3.10 or later and create a virtual environment.

**Linux / Ubuntu**

```bash
mkdir HGT-ATLAS-AI
cd HGT-ATLAS-AI

python3 -m venv .venv
source .venv/bin/activate

python -m pip install --upgrade pip
```

Create a `requirements.txt` file with:

```text
gradio
requests
pandas
networkx
plotly
scikit-learn
```

Install dependencies:

```bash
pip install -r requirements.txt
```

Save the application code as `main.py`. Because notebook magic commands are not valid in a normal Python script, remove the following line from the top of the code when running locally:

```python
%pip -q install gradio requests pandas networkx plotly scikit-learn
```

Run the application:

```bash
python main.py
```

The terminal should display the local Gradio URL.

> The current application launches with `share=True`, which creates a public sharing link when supported. For local-only use, change the launch statement to `app.launch(share=False, debug=False)`.

---

##  Running the Application

After starting the application, use the following workflow:

1. Open the Gradio interface.
2. Load the synthetic demo records to test the interface, or search PubMed for real research.
3. Import additional publications or a CSV dataset.
4. Open the Knowledge Graph tab and build the graph.
5. Use Evidence Search to retrieve relevant sentences.
6. Explore entities and candidate links.
7. Run the dataset audit.
8. Export the results for further analysis.

The synthetic demonstration records are generated for software testing and must not be treated as scientific evidence.

---

## How to Use

### Example PubMed Query

```text
("horizontal gene transfer" OR plasmid)
AND
("antimicrobial resistance" OR "antibiotic resistance")
```

This is a starting search query. Refine it according to the research question and the terminology used in the literature.

### Example Research Questions

- What research passages mention horizontal gene transfer and antimicrobial resistance?
- Which selected entities frequently appear together in the imported literature?
- What evidence passages mention plasmids and bacterial organisms?
- Which entities have the most graph neighbors in the current dataset?
- What candidate links are suggested by the graph structure?
- How many imported records contain abstracts and source URLs?

These questions are exploratory. The current application does not independently establish biological causality or prove horizontal gene transfer.

---

##  Knowledge Graph Methodology

The current prototype constructs an undirected graph.

Let:

\[
G = (V,E)
\]

where:

- \(V\) is the set of detected biomedical entities.
- \(E\) is the set of pairs of entities detected in the same sentence.

An edge is created between entities \(u\) and \(v\) when both are extracted from the same sentence.

The graph edge weight records the number of co-occurrences detected across processed sentences.

This approach is useful for exploratory visualization but has important limitations. It does not distinguish a causal relationship from a comparison, negation, background statement, or unrelated co-mention.

A future implementation should represent typed claims and evidence separately, including positive and negative claims, experimental context, publication provenance, and researcher review status.

### Candidate-Link Ranking

The prototype uses the Adamic–Adar index to rank node pairs based on their shared neighbors.

The score is:

\[
AA(u,v)=
\sum_{z\in N(u)\cap N(v)}
\frac{1}{\log |N(z)|}
\]

where \(N(u)\) represents the neighbors of node \(u\).

A high score indicates structural similarity in the current graph. It does not mean that a biological relationship exists, is novel, or is likely to be true.

---

##  Machine Learning and NLP Methodology

### Entity Extraction

The current implementation uses a curated dictionary and regular expressions to detect selected terms.

This is a transparent baseline rather than a trained biomedical named-entity recognition system.

Its performance depends on vocabulary coverage, naming conventions, aliases, spelling, and the context of each term.

### Evidence Retrieval

The application uses TF-IDF vectorization and cosine similarity.

TF-IDF emphasizes terms that are informative within the current corpus. Cosine similarity ranks sentences according to their vector similarity to the question.

This method can retrieve relevant text, but it does not understand scientific reasoning or independently verify claims.

### Candidate-Link Ranking

The Adamic–Adar index provides a graph-based baseline for exploring potential connections.

It should be compared against simpler baselines and evaluated using a carefully designed reference dataset before any scientific predictive claims are made.

---

## 📊 Evaluation Strategy

The current prototype does not provide validated scientific performance metrics. Future development should include a manually reviewed evaluation dataset.

| Component | Recommended evaluation |
|---|---|
| Entity extraction | Precision, recall and F1 score |
| Relation extraction | Precision, recall and F1 by relationship type |
| Evidence retrieval | Recall@k, precision@k and ranking metrics |
| Candidate-link ranking | Precision@k on a clearly defined held-out dataset |
| Source traceability | Proportion of displayed claims with valid source records |
| Data ingestion | Import success rate and duplicate detection |
| Application reliability | Automated tests, error rate and response time |

Evaluation should separate training and test publications to reduce data leakage. Results should include failure cases and uncertainty rather than reporting only the best-performing metric.

---

## 📚 Data Sources

### PubMed

PubMed is the supported external literature source in the current implementation.

- Search: https://pubmed.ncbi.nlm.nih.gov/
- NCBI E-utilities documentation: https://www.ncbi.nlm.nih.gov/books/NBK25501/

The application uses NCBI E-utilities to retrieve publication identifiers and metadata, including abstracts when available.

Additional sources such as NCBI Gene, NCBI Datasets, CARD, and other curated resistance resources could be considered in future versions, subject to their API terms, data licensing, and attribution requirements.

Do not assume that every publication is freely available in full text. This application primarily works with the metadata and abstracts retrieved or provided by the user.

---

##  Current Limitations

The current single-cell MVP has the following limitations:

1. **Limited vocabulary:** The entity dictionary covers only selected biomedical terms.
2. **No trained biomedical NER:** Entity detection relies on dictionary matching.
3. **Co-mention graph:** Edges do not establish a biological interaction.
4. **No validated relation extraction:** The application does not reliably classify biological relationships.
5. **Basic text retrieval:** TF-IDF does not perform semantic reasoning or scientific fact verification.
6. **Exploratory ranking:** Candidate links are generated from graph structure and are not validated discoveries.
7. **No persistent database:** The dataset is held in the current application session.
8. **No user authentication:** The current prototype is not designed for multi-user production use.
9. **Limited source validation:** Retrieved passages and links must be checked against original publications.
10. **No clinical validation:** The platform must not be used for diagnosis, treatment, or clinical resistance predictions.

These limitations define the scope of the current prototype and provide a clear roadmap for further research and engineering.

---

##  Future Enhancements

Planned directions include:

- Biomedical named-entity recognition using validated scientific NLP models.
- Typed biological relation extraction.
- Gene and organism identifier normalization.
- Synonym resolution and entity disambiguation.
- Evidence-level provenance and contradictory-claim handling.
- Semantic retrieval using scientific sentence embeddings.
- Evidence-grounded question answering with citation validation.
- PostgreSQL persistence for research records and investigations.
- Neo4j integration for persistent knowledge graph storage.
- Human-in-the-loop evidence review.
- Dataset versioning and reproducible experiments.
- Automated tests and continuous integration.
- Docker-based deployment.
- Model evaluation dashboards.
- Exportable research investigation reports.

Advanced discovery features should be introduced only after the evidence model and evaluation pipeline are reliable.

---

##  Responsible Research and Data Usage

HGT-ATLAS AI is intended for educational, research, and software-development purposes.

Users should:

- Verify scientific statements against their original publications.
- Preserve publication identifiers and source attribution.
- Respect API policies, publisher licenses, and dataset reuse restrictions.
- Distinguish extracted text from validated scientific claims.
- Document uncertainty and incomplete data.
- Avoid using candidate rankings as proof of biological relationships.
- Avoid using the application as a substitute for expert review or clinical decision-making.

The application does not validate biological discoveries and must not be used to infer that horizontal gene transfer occurred solely because two terms appear together in the literature.

---

##  Troubleshooting

### 1. PubMed import fails

Check your internet connection, search query, and NCBI availability. Retry after a short interval if the API is temporarily unavailable.

### 2. No entities are detected

The current vocabulary is limited. Try records containing supported terms or extend the `TERMS` list in the source code.

### 3. The graph is empty

Make sure research records have been imported and their titles or abstracts contain recognizable vocabulary terms.

### 4. Candidate links are unavailable

Candidate ranking requires a graph with enough connected nodes and shared-neighbor structure. Import additional relevant abstracts and rebuild the graph.

### 5. Evidence search returns no results

Try broader search terms or import more records. A failed retrieval does not establish that scientific evidence does not exist.

### 6. The application does not start locally

Confirm that the required packages are installed, that the notebook-only `%pip` line has been removed from `main.py`, and that the terminal displays no dependency or syntax errors.

### 7. CSV import fails

Verify that the file is a valid CSV and includes a title or abstract column. Check column names and encoding if the file contains unusual characters.

---

##  Contributing

Contributions that improve the scientific reliability and software quality of the project are welcome.

Suggested areas include:

- Expanding and validating the biomedical vocabulary.
- Improving entity extraction and alias normalization.
- Building a manually annotated test dataset.
- Improving graph provenance.
- Adding automated tests.
- Evaluating alternative retrieval methods.
- Improving accessibility and interface usability.
- Documenting known limitations and failure cases.

### Suggested contribution workflow

1. Fork the repository.
2. Create a feature branch.
3. Implement and test the changes.
4. Document the methodology and limitations.
5. Submit a pull request with a clear explanation.

Scientific claims and model performance improvements should be supported by reproducible evidence.

---

##  License

Choose a license before publicly distributing the repository. The MIT License is one option for the project's own code, but verify the licenses of all third-party dependencies, datasets, and research materials before redistributing them.

If you select MIT, add a `LICENSE` file containing the standard MIT License text and the appropriate copyright holder and year.

---

##  Author

**Project:** HGT-ATLAS AI  
**Domain:** Bioinformatics, Artificial Intelligence, Machine Learning, Scientific Literature Analysis  
**Primary language:** Python  
**Application framework:** Gradio

### Project Vision

To develop an evidence-grounded research exploration platform that connects scientific literature, biological entities, knowledge graphs, and AI-assisted investigation while maintaining scientific transparency and traceability.

---

##  Final Note

HGT-ATLAS AI is a foundation for exploring how computational methods can support antimicrobial resistance and horizontal gene transfer research.

Its long-term value will depend on reliable evidence extraction, traceable sources, rigorous evaluation, and careful interpretation—not merely on generating more candidate relationships.

**Evidence first. Discovery second. Scientific validation always.**
