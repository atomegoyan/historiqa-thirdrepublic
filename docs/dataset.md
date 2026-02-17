---
layout: default
title: Dataset
nav_order: 2
permalink: /dataset/
---

# Dataset Structure & Statistics

The dataset is available in the [`dataset/`](https://github.com/atomegoyan/historiqa-thirdrepublic/tree/main/dataset) folder and contains two JSONL files.

---

## Corpus Overview

The corpus focuses on the year **1887** from the French Third Republic, combining:

| Source | Document Chunks | Collection ID | Description |
|--------|-----------------|---------------|-------------|
| **Les Débats Parlementaires** | 3,229 | `debattre_1887__sectioncohere` | Parliamentary debate sections (coherence-based segmentation) |
| **Le Gaulois** | 78 | `legaulois_1887_v1` | Monarchist/conservative newspaper articles |
| **L'Intransigeant** | 79 | `lintransigeant_1887_v1` | Socialist newspaper articles |
| **Total** | **3,386** | | Complete corpus |

---

## Question Dataset Breakdown

| Question Type | Count | Description |
|---------------|-------|-------------|
| **Single-hop (SH)** | 897 | Questions answerable from a single document chunk |
| **Multi-hop – Generic** | 541 | Questions requiring synthesis of information from two documents |
| **Multi-hop – Comparative** | 192 | Questions comparing perspectives or information across sources |
| **Multi-hop – BridgeEntity** | 152 | Questions where the first document provides context for understanding the second |
| **Total** | **1,782** | Complete question dataset (897 SH + 885 MH) |

### Question Type Explanations

**Single-Hop (SH)** — Questions answerable from a single document chunk.
> *"Quelles réformes M. Blanc propose-t-il dans son discours d'ouverture de session?"*

**Multi-Hop – Generic** — Questions requiring synthesis of factual information from two sources. Pattern: tracing parliamentary debates to press coverage, or connecting related events.

**Multi-Hop – BridgeEntity** — Questions where understanding Document 1 provides essential context for Document 2. Pattern: entity, event, or concept in the first document is necessary to interpret the second.

**Multi-Hop – Comparative** — Questions explicitly comparing viewpoints across sources.
> *"Quelle est la réaction de la presse monarchiste comparée à la presse socialiste?"*

---

## File Format

### 1. `question_dataset.jsonl` (1,782 lines)

Each line is a JSON object representing one question with its associated documents:

```json
{
  "question_id": "sh_18870112",
  "question_type": "SH",
  "question": "Quelles réformes M. Blanc propose-t-il de prioriser dans son discours?",
  "gold_ids": ["18870112"],
  "id_1": "18870112",
  "source_1": "Le Gaulois",
  "document_1": "CHAMBRE DES DÉPUTÉS\nLA RENTRÉE...",
  "id_2": null,
  "source_2": null,
  "document_2": null
}
```

| Field | Type | Description |
|-------|------|-------------|
| `question_id` | string | Unique identifier (format: `{type}_{date}_{ids}`) |
| `question_type` | string | `SH`, `MH - Generic`, `MH - Comparative`, or `MH - BridgeEntity` |
| `question` | string | Question text in French |
| `gold_ids` | array | List of document IDs containing the answer(s) |
| `id_1` | string | First source document identifier |
| `source_1` | string | `Le Gaulois`, `L'Intransigeant`, or `Les Débats` |
| `document_1` | string/array | First document text |
| `id_2` | string/null | Second source document identifier (multi-hop only) |
| `source_2` | string/null | Second source name (multi-hop only) |
| `document_2` | string/array/null | Second document text (multi-hop only) |

**Notes:**
- Single-hop questions have `id_2`, `source_2`, and `document_2` set to `null`
- Parliamentary debate documents may be arrays of text segments (for complex interventions)
- Newspaper articles are typically single strings

### 2. `corpus_dataset.jsonl` (3,386 lines)

Each line is a JSON object representing one document chunk:

```json
{
  "collection": "debattre_1887__sectioncohere",
  "id": "1887-01-11_004_000.txt",
  "document": ["ALLOCUTION DE M. LE PRÉSIDENT...", "..."],
  "year": 1887,
  "month": 1,
  "day": 11,
  "base_name": "1887-01-11_004_000.txt",
  "chamber": "Chambre des Députés",
  "sommaire": "Ouverture de la session...",
  "vote": "",
  "excuse": "",
  "absent": "",
  "length_500": "yes"
}
```

| Field | Type | Description |
|-------|------|-------------|
| `collection` | string | Collection identifier |
| `id` | string | Unique document identifier |
| `document` | string/array | Document text |
| `year`, `month`, `day` | int | Publication/session date |
| `base_name` | string | Original source filename |
| `chamber` | string | Parliamentary chamber info (debates only) |
| `sommaire` | string | Session summary (debates only) |
| `vote` | string | Voting information (debates only) |
| `excuse` | string | Absences information (debates only) |
| `absent` | string | Absentees list (debates only) |
| `length_500` | string | `"yes"` if document exceeds 500 tokens |

**Collections:**
- `debattre_1887__sectioncohere` (3,229 docs) — Parliamentary debates, coherence-based segmentation
- `legaulois_1887_v1` (78 docs) — Le Gaulois newspaper articles
- `lintransigeant_1887_v1` (79 docs) — L'Intransigeant newspaper articles

---

## Aligned Newspaper Sources

![Aligned Newspaper Chunks]({{ site.baseurl }}/assets/images/opera_chunks_page-0001.jpg)
*Cross-newspaper alignment example. Le Gaulois and L'Intransigeant report on the same event (Opéra-Comique safety issues) within 7 days. Cosine similarity scores quantify semantic relatedness across ideological divides.*
