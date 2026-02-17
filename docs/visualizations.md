---
layout: default
title: Visualizations
nav_order: 4
permalink: /visualizations/
---

# Interactive Visualizations

Explore the dataset through interactive sunburst charts and corpus projections.

---

## Sunburst Charts — Question Taxonomy

These interactive sunburst charts show the hierarchical distribution of questions by type and source. Click on segments to zoom in.

### All Questions

<iframe src="{{ site.baseurl }}/assets/sunbursts/sunburst_all_questions.html" width="100%" height="600" frameborder="0" style="border: 1px solid #ddd; border-radius: 8px;"></iframe>

### Multi-Hop — BridgeEntity

<iframe src="{{ site.baseurl }}/assets/sunbursts/sunburst_MH_-_BridgeEntity.html" width="100%" height="600" frameborder="0" style="border: 1px solid #ddd; border-radius: 8px;"></iframe>

### Multi-Hop — Comparative

<iframe src="{{ site.baseurl }}/assets/sunbursts/sunburst_MH_-_Comparative.html" width="100%" height="600" frameborder="0" style="border: 1px solid #ddd; border-radius: 8px;"></iframe>

### Multi-Hop — Generic

<iframe src="{{ site.baseurl }}/assets/sunbursts/sunburst_MH_-_Generic.html" width="100%" height="600" frameborder="0" style="border: 1px solid #ddd; border-radius: 8px;"></iframe>

---

## Corpus Projections

### Embedding Space Visualization

![Corpus Projection]({{ site.baseurl }}/assets/images/output.png)
*UMAP projection of document embeddings across the corpus.*

### Cross-Source Similarity

![Newspaper-Debate Similarity]({{ site.baseurl }}/assets/images/projection_newspaper_to_debat_similarity.png)
*Projection of newspaper-to-debate document similarity.*

![Newspaper-Debate Similarity (filtered)]({{ site.baseurl }}/assets/images/projection_newspaper_to_debat_similarity_cut.png)
*Filtered projection showing strongest newspaper-debate connections.*

![Newspaper-Debate + Newspaper Similarity]({{ site.baseurl }}/assets/images/projection_newspaper_to_debat_and_newspaper_similarity.png)
*Combined projection of newspaper-to-debate and inter-newspaper similarity.*

![Inter-Newspaper Similarity]({{ site.baseurl }}/assets/images/projection_newspaper_to_newspaper_similarity.png)
*Projection of inter-newspaper similarity (Le Gaulois ↔ L'Intransigeant).*

---

## Single-Hop Embedding Analysis

![PCA Embeddings]({{ site.baseurl }}/assets/images/pca_embeddings_questions_simplified_cut.png)
*PCA projection of question embeddings for single-hop questions, showing clustering by topic and source type.*
