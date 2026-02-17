---
layout: default
title: Home
nav_order: 1
permalink: /
---

# HistoriQA-ThirdRepublic

**Multi-Hop Question Answering Corpus for Historical Research**

[![Dataset](https://img.shields.io/badge/Dataset-Available-green)](https://github.com/atomegoyan/historiqa-thirdrepublic/tree/main/dataset)
[![Paper](https://img.shields.io/badge/LREC%202026-Paper-orange)]({{ site.baseurl }}/assets/paper.pdf)
[![HAL](https://img.shields.io/badge/HAL-hal--05438255-blue)](https://hal.science/hal-05438255)
[![License](https://img.shields.io/badge/License-CC--BY--4.0-blue.svg)](https://creativecommons.org/licenses/by/4.0/)

---

## Overview

**HistoriQA-ThirdRepublic** is a French-language dataset of **1,782 questions** derived from parliamentary debates and newspapers of the French Third Republic (1887). The dataset is designed to evaluate Retrieval-Augmented Generation (RAG) systems and large language models on complex, domain-specific historical tasks requiring cross-source synthesis, temporal reasoning, and the integration of sparse evidence.

![Dataset Overview]({{ site.baseurl }}/assets/images/main_visu.jpg)
*Sample multi-hop question requiring synthesis across parliamentary debates and newspaper sources from 1887.*

---

## Key Features

- **1,782 questions**: 897 single-hop + 885 multi-hop (Generic, Comparative, BridgeEntity)
- **3,386 document chunks**: Parliamentary debates segmented for granular retrieval + newspaper articles
- **Heterogeneous sources**: Official parliamentary records + ideologically opposed newspapers
- **Historian-validated**: Developed in collaboration with a historian for historical accuracy
- **Multi-hop reasoning**: Questions requiring synthesis across multiple documents and sources
- **Temporal alignment**: Questions linking contemporaneous debates and press coverage

---

## Quick Statistics

| Metric | Value |
|--------|-------|
| **Total Questions** | 1,782 |
| **Single-hop (SH)** | 897 |
| **Multi-hop (MH)** | 885 |
| **Total Document Chunks** | 3,386 |
| **Parliamentary Debate Sections** | 3,229 |
| **Newspaper Articles** | 157 |
| **Time Period** | Year 1887 |
| **Language** | French |

---

## Abstract

We present a French-language dataset of multi-hop historical questions derived from parliamentary debates and newspapers of the French Third Republic. Designed in collaboration with a historian, the corpus captures complex reasoning patterns typical of historical inquiry, including cross-source synthesis, temporal reasoning, and the integration of sparse evidence. The dataset emphasizes multi-hop connections across heterogeneous historical documents, providing a resource for evaluating retrieval-augmented and large language model systems in domain-specific contexts. While focused on French historical documents, our methodology can be readily adapted to other languages and national corpora.

**Keywords**: Digital Humanities · Question Answering · Multi-Hop Reasoning · Historical Corpus · French Language · Retrieval-Augmented Generation

---

## Historical Context (1887)

This dataset focuses on the year **1887**, a pivotal period in French history characterized by:

- **Political Crisis**: The Boulangist crisis, challenging republican institutions
- **International Tensions**: Strained relations with Germany following the Schnaebelé affair
- **Media Landscape**: Rise of mass-circulation newspapers (*grande presse d'information*)
- **Parliamentary System**: Powerful legislature with extensive policy-making powers

### Sources

**Parliamentary Debates** — Official proceedings from the *Chambre des Députés*:
- Verbatim transcripts of legislative debates, speeches, votes, and procedural discussions
- Source: Bibliothèque nationale de France (BnF) via [Gallica](https://gallica.bnf.fr/)

**Newspapers** — Two ideologically opposed publications:

| Newspaper | Political Orientation | Circulation | Perspective |
|-----------|----------------------|-------------|-------------|
| **Le Gaulois** | Monarchist / Conservative | ~40,000 | Right-wing, supportive of monarchy |
| **L'Intransigeant** | Socialist (shifting to populist) | ~100,000+ | Left-wing, radical republican |

This heterogeneous source design enables evaluation of systems' ability to connect institutional discourse with public interpretation, compare contrasting ideological perspectives, and synthesize information across different text genres and registers.

---

## Quick Links

| Resource | Link |
|----------|------|
| 📄 Paper (PDF) | [Download]({{ site.baseurl }}/assets/paper.pdf) |
| 🔗 HAL Archive | [hal-05438255](https://hal.science/hal-05438255) |
| 📊 Dataset | [GitHub](https://github.com/atomegoyan/historiqa-thirdrepublic/tree/main/dataset) |
| 📈 Visualizations | [Interactive Sunbursts]({{ site.baseurl }}/visualizations/) |
| 📖 Citation | [BibTeX]({{ site.baseurl }}/cite/) |
