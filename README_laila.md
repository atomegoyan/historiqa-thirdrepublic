# SWE-QA: A Dataset and Benchmark for Complex Code Understanding

[![GitHub Pages](https://img.shields.io/badge/GitHub-Pages-blue)](https://lailanelkoussy.github.io/swe-qa/)
[![Paper](https://img.shields.io/badge/Paper-PDF-red)](paper/paper.pdf)
[![LREC 2026](https://img.shields.io/badge/LREC-2026-green)](https://lrec-coling-2026.org/)

**Accepted at LREC-COLING 2026**

## Overview

This repository contains **SWE-QA**, a comprehensive dataset and benchmark for evaluating multi-hop code comprehension. The dataset includes:

- 🎯 **9,072 multiple-choice questions** for complex code understanding
- 📦 **12 Python repositories** from SWE-bench
- 🔍 **2 question categories**: Declaration-and-Call (DC) and Interacting Entities (IE)
- ⚙️ **2 experimental settings**: Oracle (clean) and Noisy Oracle (with distractors)

## Quick Links

- 🌐 **[Project Page](https://lailanelkoussy.github.io/swe-qa/)** - Jekyll-powered project site with interactive overview
- 📄 **[Paper](paper/paper.pdf)** - Full research paper (PDF)
- 📊 **[Dataset](datasets/)** - Download datasets and view documentation

### Main Branch Contents

```
.
├── paper/
│   └── paper.pdf          # Research paper
├── datasets/
│   ├── README.md          # Detailed dataset documentation
│   ├── mcq_dataset.zip    # Oracle setting questions (9,072 questions)
│   ├── mcq_dataset_with_distractors.zip  # Noisy oracle setting
│   └── repos/             # Code chunks and metadata (12 repositories)
├── assets/
│   └── teaser.pdf         # Teaser figure
└── README.md              # This file
│   └── paper.pdf          # Research paper
├── datasets/
│   ├── README.md          # Detailed dataset documentation
│   ├── mcq_dataset.zip    # Oracle setting questions
│   ├── mcq_dataset_with_distractors.zip  # Noisy oracle setting
│   └── repos/             # Code chunks and metadata (12 repositories)
└── assets/                # Optional images and resources
```

## Datasets

### Download

- **[Oracle Questions](datasets/mcq_dataset.zip)** (9,072 questions) - Questions with only relevant code chunks
- **[Noisy Oracle Questions](datasets/mcq_dataset_with_distractors.zip)** - Questions with additional distractor chunks
- **[Code Repositories](datasets/repos/)** - Processed code chunks and entity metadata

### Repositories Included

The dataset covers 12 popular Python repositories:
- astropy
- django
- matplotlib
- seaborn
- flask
- requests
- pylint
- pytest
- xarray
- scikit-learn
- sphinx
- sympy

## Getting Started

1. **View the project page**: Visit the [Jekyll-powered project site](https://lailanelkoussy.github.io/swe-qa/) for an interactive overview
2. **Download the datasets**: Get the question sets from the [datasets](datasets/) folder
3. **Read the documentation**: Check the [Dataset README](datasets/README.md) for detailed structure and usage information

## Dataset Structure

Each question in the dataset includes:
- **Code chunks**: Formatted code snippets with metadata
- **Question**: Natural language question about the code
- **Multiple-choice options**: 4 options (A, B, C, D)
- **Correct answer**: Ground truth label
- **Category**: DC (Declaration-and-Call) or IE (Interacting Entities)
- *Citation

If you use this dataset in your research, please cite our paper:

```bibtex
@inproceedings{elkoussy2026sweqa,
  title={SWE-QA: A Dataset and Benchmark for Complex Code Understanding},
  author={ElKoussy, Laila and Perez, Julien},
  booktitle={Proceedings of LREC-COLING 2026},
  year={2026}
}
```

## License

This dataset is released for research purposes. Please see the paper for detailed terms.


