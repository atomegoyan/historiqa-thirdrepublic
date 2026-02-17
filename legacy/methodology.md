---
layout: default
title: Methodology
nav_order: 3
permalink: /methodology/
---

# Dataset Construction Methodology

---

## Overview

Questions were generated using large language models (Cohere Command-R) with prompts developed iteratively in collaboration with a historian. The process emphasized:

1. **Historical Accuracy** — Questions reflect genuine historical inquiry patterns
2. **Substantive Content** — Focus on political positions and central debates, not procedural details
3. **Paraphrasing** — Avoid verbatim copying from source texts
4. **Source Diversity** — Balance across debate and newspaper sources

---

## Single-Hop Generation

**Process:**
1. Select individual document chunks from corpus
2. Generate question using refined prompts (see [prompts below](#single-hop-prompt))
3. Validate question quality through TF-IDF semantic distance analysis
4. Historian review for historical plausibility

**Quality Control:** Optimized prompts achieved higher semantic divergence from source texts (cosine distance: 1.26 vs 1.04 baseline), indicating conceptual reformulation rather than lexical copying.

![Single-Hop Questions]({{ site.baseurl }}/assets/images/singlehop_examples_page-0001.jpg)
*Single-hop question examples with English translations. These questions are answerable from individual parliamentary debate or newspaper documents.*

---

## Multi-Hop Generation

### Document Pairing

1. **Embedding** — Compute dense embeddings (Cohere embed-v4.0) for all documents
2. **Similarity Filtering** — Identify pairs with cosine similarity ≥ 0.7
3. **Temporal Constraints** — For newspaper pairs, require publication within 7 days
4. **Type Selection** — Choose question type (Generic, Comparative, BridgeEntity) based on relationship

### Validation

- UMAP visualization of semantic relationships
- Historian review for accuracy and relevance
- Manual inspection of generated question quality

![Multi-Hop Questions]({{ site.baseurl }}/assets/images/multihop_examples_page-0001.jpg)
*Multi-hop question examples with English translations. These questions require synthesizing information across multiple sources, demonstrating Generic, Comparative, and BridgeEntity question types.*

---

## Question Type Illustrations

### Multi-Hop — BridgeEntity

![BridgeEntity]({{ site.baseurl }}/assets/images/bridgeentity.png)

### Multi-Hop — Comparative

![Comparative]({{ site.baseurl }}/assets/images/comparative.png)

### Multi-Hop — Generic

![Generic]({{ site.baseurl }}/assets/images/generic.png)

---

## Historian-in-the-Loop

Throughout construction, a historian provided:
- Domain expertise on 1887 French politics
- Validation of historical accuracy
- Feedback on question relevance and complexity
- Identification of anachronisms or biases

---

## Question Generation Prompts

### Single-Hop Prompt

![Single-Hop Prompt]({{ site.baseurl }}/assets/images/prompt_SH_page-0001.jpg)
*Prompt template for generating single-hop questions from individual parliamentary debate chunks. Emphasizes substantive political content and paraphrasing.*

### Multi-Hop Prompts

#### Follow-up Questions (Debate → Press)

![Follow-up Debate-Press]({{ site.baseurl }}/assets/images/prompt_MH_followup_debate_press_page-0001.jpg)
*Prompt for generating follow-up questions tracing parliamentary debates to press coverage.*

#### Follow-up Questions (Press ↔ Press)

![Follow-up Press-Press]({{ site.baseurl }}/assets/images/prompt_MH_followup_press_press_page-0001.jpg)
*Prompt for generating follow-up questions comparing coverage across different newspapers.*

#### Bridge Entity Questions (Debate ↔ Press)

![Bridge Entity]({{ site.baseurl }}/assets/images/prompt_MH_bridgeentity_debate_press_page-0001.jpg)
*Prompt for bridge entity questions connecting debates and newspapers through shared entities.*

#### Comparative Questions (Debate ↔ Press)

![Comparative Debate-Press]({{ site.baseurl }}/assets/images/prompt_MH_comparative_debate_press_page-0001.jpg)
*Prompt for comparative questions contrasting parliamentary and press perspectives.*

#### Comparative Questions (Press ↔ Press)

![Comparative Press-Press]({{ site.baseurl }}/assets/images/prompt_MH_comparative_press_press_page-0001.jpg)
*Prompt for comparative questions analyzing different newspaper perspectives (monarchist vs. socialist) on the same events.*
