---
layout: default
title: Benchmarks
nav_order: 5
permalink: /benchmarks/
---

# Benchmarks & Baselines

For detailed benchmark results including retrieval performance, answer generation accuracy, and LLM-as-judge validation, please refer to our [paper]({{ site.baseurl }}/assets/paper.pdf).

---

## Key Findings

| Task | Metric | Performance |
|------|--------|-------------|
| **Single-hop retrieval** | Recall@3 | ~68% |
| **Multi-hop retrieval** | Recall@3 | ~36% |
| **Single-hop answer generation** | Accuracy | ~54–59% |
| **Multi-hop answer generation** | Accuracy | ~14–19% |

### Observations

- **Retrieval gap**: Multi-hop retrieval remains significantly more challenging than single-hop
- **Generation gap**: Large performance drop from single-hop to multi-hop answer generation
- **Corpus bias**: Retrievers favor parliamentary debates even for newspaper-only queries
- **Cross-newspaper difficulty**: Queries requiring both Le Gaulois and L'Intransigeant sources are particularly challenging

---

## Use Cases & Applications

### 1. Retrieval-Augmented Generation (RAG)
- Benchmark retrieval quality on domain-specific historical texts
- Evaluate generation with long-context, multi-document inputs
- Test handling of heterogeneous source types

### 2. Multi-Hop Reasoning
- Study compositional reasoning across documents
- Evaluate entity linking and coreference across sources
- Test temporal reasoning and chronological alignment

### 3. Historical NLP & Digital Humanities
- Develop models for historical document understanding
- Build tools for historians conducting archival research
- Study language evolution and historical French

### 4. Cross-Source Information Synthesis
- Evaluate integration of institutional vs. media discourse
- Test perspective-taking and bias detection
- Study information propagation from debates to press

### 5. French Language Model Evaluation
- Benchmark on complex, domain-specific French tasks
- Test beyond standard benchmarks with realistic historical texts
- Evaluate handling of 19th-century French language

---

## Limitations & Future Work

### Current Limitations

- **Temporal scope**: Single year (1887) may not capture full Third Republic diversity
- **Geographic scope**: Focus on Parisian press and national parliamentary debates
- **Single annotator**: Historian validation by one expert; multiple annotators would strengthen validity
- **Language**: French-only, though methodology is transferable
- **Generation model**: Questions generated with Cohere models; alternative models may produce different results

### Future Directions

- Expand to multiple years across the Third Republic (1870–1940)
- Include regional newspapers and multiple political perspectives
- Add answer annotations validated by multiple historians
- Develop multilingual versions for comparative parliamentary research
- Create fine-tuned models for historical French document understanding
