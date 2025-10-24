# Multi-Hop Question Answering Corpus for Historical Research
## Parliamentary Debates from the French Third Republic (1870-1940)

[![Dataset](https://img.shields.io/badge/Dataset-Available-green)](./dataset/)
[![Paper](https://img.shields.io/badge/LREC%202026-Submission-orange)](https://lrec2026.info/)
[![License](https://img.shields.io/badge/License-CC--BY--4.0-blue.svg)](LICENSE)

---

## Overview

This repository contains a French-language dataset of **1,782 questions** (897 single-hop + 885 multi-hop) derived from parliamentary debates and newspapers of the French Third Republic. The dataset is designed to evaluate Retrieval-Augmented Generation (RAG) systems and large language models on complex, domain-specific historical tasks requiring cross-source synthesis, temporal reasoning, and the integration of sparse evidence.

![Dataset Overview](images/main_visu.jpg)
*Figure 1: Sample multi-hop question requiring synthesis across parliamentary debates and newspaper sources from 1887. The RAG pipeline retrieves relevant documents from heterogeneous sources to answer questions about the military law debate.*

---

## Abstract

We present a French-language dataset of multi-hop historical questions derived from parliamentary debates and newspapers of the French Third Republic. Designed in collaboration with a historian, the corpus captures complex reasoning patterns typical of historical inquiry, including cross-source synthesis, temporal reasoning, and the integration of sparse evidence. 

The dataset comprises **1,782 questions** and emphasizes multi-hop connections across heterogeneous historical documents, providing a resource for evaluating retrieval-augmented and large language model systems in domain-specific contexts. We describe the methodology for constructing the corpus, including the selection and alignment of sources, question validation, and metadata integration. 

While the dataset focuses on French historical documents, our methodology can be readily adapted to other languages and national corpora. Finally, we demonstrate how the corpus can support realistic evaluation scenarios for multi-hop question answering, bridging the gap between NLP benchmarks and the needs of historical scholarship.

**Keywords**: Digital Humanities, Question Answering, Multi-Hop Reasoning, Historical Corpus, French Language, Retrieval-Augmented Generation

---

## Dataset Statistics

### Corpus Overview

The corpus focuses on the year **1887** from the French Third Republic, comprising:

| Source | Documents | Avg Tokens | Median Tokens | Range (min-max) |
|--------|-----------|------------|---------------|-----------------|
| **Les Débats Parlementaires** (filtered) | 963 | 4,433 | 716 | 143-62,998 |
| **Le Gaulois** (newspaper) | 78 | 922 | 802 | 51-4,023 |
| **L'Intransigeant** (newspaper) | 79 | 376 | 317 | 6-1,335 |

### Question Dataset

| Question Type | Count | Description |
|---------------|-------|-------------|
| **Single-hop** | 897 | Questions answerable from a single document chunk |
| **Multi-hop** | 885 | Questions requiring synthesis across multiple sources |
| **Total** | **1,782** | Complete question dataset |

#### Multi-hop Question Breakdown

- **Follow-up questions**: Questions tracing parliamentary debates to press coverage
- **Bridge-entity questions**: Questions connecting sources via shared entities (politicians, events)
- **Comparative questions**: Questions contrasting viewpoints across newspapers or between press and parliament

---

## Historical Context

This dataset focuses on the French Third Republic (1870-1940), specifically the year **1887**, a period marked by:

- **Political Crisis**: The Boulangist crisis, posing major challenges to the republican regime
- **International Tensions**: Particularly with Germany
- **Media Landscape**: Rise of the "*grande presse d'information*" (mass-circulation newspapers)
- **Parliamentary Autonomy**: Powerful legislature with extensive policy-making powers

The dataset combines **parliamentary debates** (official proceedings from the Chamber of Deputies) with contemporary **newspaper coverage** from two ideologically opposed publications:
- **Le Gaulois**: Monarchist and conservative right-wing perspective
- **L'Intransigeant**: Socialist perspective (gradually shifting toward populism)

This multimodal design tests whether systems can connect institutional discourse with mediated public interpretation across heterogeneous sources.

---

## Dataset Files

The `dataset/` folder contains:

### 1. `question_dataset.jsonl`

Complete question dataset with metadata. Each line contains:

```json
{
  "question": "Question text in French",
  "question_type": "single-hop | multi-hop",
  "multi_hop_type": "follow-up | comparative | bridge-entity (for multi-hop only)",
  "date": "YYYY-MM-DD",
  "source_documents": [
    {
      "source": "Les Débats | Le Gaulois | L'Intransigeant",
      "document_id": "unique_document_identifier",
      "chunk_text": "Relevant text passage"
    }
  ],
  "answer": "Reference answer (ground truth)",
  "metadata": {
    "generation_model": "model_name",
    "similarity_score": 0.0-1.0,
    "temporal_constraint": "details on temporal filtering"
  }
}
```

**Fields**:
- `question`: The generated question in French
- `question_type`: Classification as single-hop or multi-hop
- `multi_hop_type`: For multi-hop questions, specifies the reasoning pattern required
- `date`: Date(s) associated with the source documents
- `source_documents`: Array of document chunks used to generate the question
- `answer`: Ground truth answer generated from source documents
- `metadata`: Additional information about question generation

### 2. `corpus_dataset.jsonl`

Complete corpus of source documents. Each line contains:

```json
{
  "document_id": "unique_identifier",
  "source": "Les Débats | Le Gaulois | L'Intransigeant",
  "date": "YYYY-MM-DD",
  "text": "Full document text",
  "tokens": 1234,
  "metadata": {
    "session_info": "for debates",
    "article_title": "for newspapers",
    "speakers": ["list of speakers (debates only)"]
  }
}
```

---

## Dataset Construction Methodology

### Single-Hop Question Generation

Questions were generated from individual document chunks using iteratively refined prompts developed in collaboration with a historian. The process emphasized:

1. **Substantive Content**: Focus on central debate topics rather than procedural details
2. **Political Positions**: Highlight key political positions and historical issues
3. **Paraphrasing**: Avoid verbatim text reproduction

Quality was assessed through **TF-IDF semantic distance analysis**: optimized prompts produced questions with higher semantic divergence from source texts (cosine distance: 1.26 vs 1.04 baseline), indicating greater conceptual reformulation rather than lexical copying.

### Multi-Hop Question Generation

Multi-hop questions were identified through:

1. **Embedding-based Similarity**: Using Cohere embed-v4.0, compute cosine similarity between all document pairs
2. **Similarity Threshold**: Filter pairs with similarity ≥ 0.7
3. **Temporal Constraints**: For newspaper-to-newspaper pairs, require publication dates within 7 days
4. **Question Type Selection**: Generate follow-up, comparative, or bridge-entity questions based on document relationships

The generation process was validated through:
- UMAP visualization of semantic relationships between press and debate articles
- Historian review of question relevance and historical accuracy
- Clustering analysis to identify thematic connections

---

## Key Findings & Benchmarks

### Retrieval Performance

| Configuration | Queries | Recall@3 | Recall@5 | Recall@10 | Accuracy@3 | MRR@3 |
|---------------|---------|----------|----------|-----------|------------|-------|
| **Single-hop** | 897 | 67.8% | 71.6% | 76.4% | 67.8% | 60.6% |
| **Multi-hop (all)** | 885 | 35.9% | 44.1% | 54.6% | 15.5% | 26.0% |
| Cross-newspaper | 314 | 14.3% | 19.9% | 29.3% | 1.3% | 10.3% |
| Newspaper-Debate | 571 | 47.8% | 57.4% | 68.6% | 23.3% | 34.6% |

**Key Observations**:
- Single-hop retrieval is highly effective with dense embeddings alone
- Multi-hop retrieval remains challenging, especially for cross-newspaper queries
- **Corpus bias**: Retrievers favor parliamentary debates (80.6% of retrieved documents) even for newspaper-only queries
- Reranking can improve Recall@10 but sometimes reduces top-3 performance

### Answer Generation Performance

Evaluation using LLM-as-a-judge on filtered dataset (K=3, no reranking):

| Model | Single-hop Accuracy | Multi-hop Accuracy |
|-------|--------------------|--------------------|
| **gpt-oss-20b** | **58.85%** | **18.86%** |
| Llama-3.3-70B-Instruct | 53.53% | 17.92% |
| gpt-4o-mini | 52.72% | 13.77% |
| Llama-3.3-3B-Instruct | 24.10% | 3.2% |

**Key Observations**:
- Substantial gap between single-hop and multi-hop performance across all models
- Multi-hop reasoning requires effective integration across multiple long contexts
- Model capacity matters significantly for compositional reasoning

### LLM-as-a-Judge Alignment

Comparison of LLM-based evaluation with human historian annotations (N=50 questions):

| Evaluation Mode | Agreement on Correct Answers | Agreement on Incorrect Answers | Overall Alignment |
|-----------------|------------------------------|--------------------------------|-------------------|
| **Source-oracle** | 100% (20/20) | 46.7% (14/30) | 68% |
| Answer-reference | 50% (10/20) | 80% (24/30) | 68% |

**Key Observations**:
- Source-oracle mode (LLM judge with access to gold documents) shows perfect agreement for correct answers
- LLM judges are highly reliable when marking answers as correct with high-capacity models
- Lower agreement on incorrect answers suggests conservative LLM evaluation

---

## Use Cases

This dataset can be used for:

1. **RAG System Evaluation**: Benchmark retrieval and generation components on domain-specific, long-context tasks
2. **Multi-Hop Reasoning Research**: Study compositional reasoning across heterogeneous sources
3. **Historical NLP**: Develop models for historical document understanding and synthesis
4. **Cross-Source Integration**: Evaluate systems' ability to connect institutional records with media coverage
5. **Temporal Reasoning**: Test models on questions requiring temporal alignment and chronological understanding
6. **French Language Models**: Evaluate performance on complex French-language tasks beyond standard benchmarks

---

## Dataset Examples

### Aligned Newspaper Sources

![Aligned Newspaper Chunks](images/question_display/opera_chunks_page-0001.jpg)
*Figure 2: Direct evidence of text alignment between Le Gaulois and L'Intransigeant. Short passages from both newspapers, published within 7 days, discuss the same event (safety issues at the Opéra-Comique). Cosine similarity scores quantify how closely related the language is across sources, demonstrating parallel reporting.*

### Single-Hop Question Examples

![Single-Hop Questions](images/question_display/singlehop_examples_page-0001.jpg)
*Figure 3: Examples of single-hop questions with English translations. These questions are answerable from a single document within the corpus, focusing on parliamentary debates and legislative issues from 1887.*

### Multi-Hop Question Examples

![Multi-Hop Questions](images/question_display/multihop_examples_page-0001.jpg)
*Figure 4: Examples of multi-hop questions with English translations. These complex questions require synthesizing information across multiple sources (newspapers and/or parliamentary debates), demonstrating three question types: Follow-up, Comparative, and Bridge-entity.*

---

## Appendix: Question Generation Prompts

The following prompts were used to generate questions, refined iteratively with historian feedback:

### Single-Hop Prompt

![Single-Hop Prompt](images/prompts/prompt_SH_page-0001.jpg)
*Figure 5: Prompt for generating single-hop questions from individual parliamentary debate chunks.*

### Multi-Hop Prompts

#### Follow-up Questions (Debate → Press)

![Follow-up Debate-Press](images/prompts/prompt_MH_followup_debate_press_page-0001.jpg)
*Figure 6: Prompt for generating follow-up questions that trace how parliamentary debates were covered in the press.*

#### Follow-up Questions (Press ↔ Press)

![Follow-up Press-Press](images/prompts/prompt_MH_followup_press_press_page-0001.jpg)
*Figure 7: Prompt for generating follow-up questions comparing newspaper coverage across different publications.*

#### Bridge Entity Questions (Debate ↔ Press)

![Bridge Entity](images/prompts/prompt_MH_bridgeentity_debate_press_page-0001.jpg)
*Figure 8: Prompt for generating bridge entity questions connecting debates and newspapers through shared entities.*

#### Comparative Questions (Debate ↔ Press)

![Comparative Debate-Press](images/prompts/prompt_MH_comparative_debate_press_page-0001.jpg)
*Figure 9: Prompt for generating comparative questions contrasting parliamentary and press perspectives.*

#### Comparative Questions (Press ↔ Press)

![Comparative Press-Press](images/prompts/prompt_MH_comparative_press_press_page-0001.jpg)
*Figure 10: Prompt for generating comparative questions analyzing different newspaper perspectives on the same events.*

---

## Citation

If you use this dataset in your research, please cite:

```bibtex
@inproceedings{anonymous2026multihop,
  title={Multi-Hop Question Answering Corpus for Historical Research, Parliamentary Debates from the French Third Republic (1870-1940)},
  author={Anonymous},
  booktitle={Proceedings of the 2026 Joint International Conference on Computational Linguistics, Language Resources and Evaluation (LREC-COLING 2026)},
  year={2026}
}
```

---

## License

This dataset is released under the **Creative Commons Attribution 4.0 International License (CC-BY 4.0)**.

The historical documents are in the public domain and sourced from the Bibliothèque nationale de France (BnF) digital library [Gallica](https://gallica.bnf.fr/).

---

## Ethical Considerations

- **Public Domain Sources**: All historical documents are in the public domain, sourced from the Bibliothèque nationale de France
- **Historical Biases**: The corpus contains viewpoints and biases from 1887, which the dataset captures for research purposes, not to endorse
- **Historian Validation**: A historian-in-the-loop methodology was employed for question validation to mitigate risks of historically biased or misleading interpretations
- **Intended Use**: This dataset is designed for academic research on NLP, information retrieval, and digital humanities

---

## Limitations

- **Temporal Scope**: Limited to a single year (1887), which may not capture the full diversity of the Third Republic period
- **Geographic Scope**: Focuses on French parliamentary debates and two Parisian newspapers
- **Language**: French-only dataset, though methodology is transferable to other languages
- **Annotator Coverage**: Question validation performed by a single historian; future work would benefit from multiple annotators
- **Model Dependency**: Question generation used Cohere API models; results may vary with alternative models

---

## Acknowledgments

We gratefully acknowledge:

- **Bibliothèque nationale de France (BnF)**: For providing digitized parliamentary debates and newspaper archives via [Gallica](https://gallica.bnf.fr/)
- The historian collaborator who provided domain expertise for question validation and prompt refinement

---

## Contact

For questions about the dataset or collaboration opportunities, please open an issue in this repository.

---

**Note**: This repository contains the dataset and supporting materials for an anonymous submission to LREC-COLING 2026. Author information and full repository will be made public upon paper acceptance.
