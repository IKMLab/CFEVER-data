# CFEVER-data

## Introduction to CFEVER
This repository contains the dataset for our AAAI 2024 paper, "CFEVER: A Chinese Fact Extraction and VERification Dataset". (Paper link will be provided soon.)

## Leaderboard website
Please visit https://ikmlab.github.io/CFEVER to check the leaderboard of CFEVER.

## Repository structure
```
CFEVER-data
├── data
│   ├── dev.jsonl # CFEVER development set
│   ├── test.jsonl # CFEVER test set without labels and evidence
│   └── train.jsonl # CFEVER training set
├── LICENSE
└── README.md
```

## Getting started
- Download this repository
```
git clone https://github.com/IKMLab/CFEVER-data.git
cd CFEVER-data
```
- Download the processed Wikipedia fact database from [this google drive link](https://drive.google.com/file/d/1uFkoHbJ2iqm2pMR3rHHBTym3Q7pukKm8/view?usp=sharing) and unzip it.
```
unzip wiki-pages.zip
```
- Then you will get a folder named `wiki-pages` containing 24 jsonl files. Each file contains the 50,000 processed Wikipedia pages.
    - In each jsonl file, each line is a json object representing a Wikipedia page. The json object has the following fields:
        - `id`: the Wikipedia page name
        - `text`: the processed text of the Wikipedia article
        - `lines`: the processed text of the Wikipedia article including **the sentence numbers**

## Evaluation
- Please refer to our codebase: https://github.com/IKMLab/CFEVER-baselines

## Submission
- Please include two fields: `predicted_label` and `predicted_evidence` for each claim in the test set. The `predicted_label` should be one of `SUPPORTS`, `REFUTES`, or `NOT ENOUGH INFO`. The `predicted_evidence` should be a list of evidence sentences, where each evidence sentence is represented by a list of `[page_id, line_number]`. For example:

```
# One evidence sentence for the claim
{
    "id": 1,
    "predicted_label": "REFUTES",
    "predicted_evidence": [
        ["page_id_2", 2],
    ]
}
```

```
# Two evidence sentences for the claim
{
    "id": 1,
    "predicted_label": "SUPPORTS",
    "predicted_evidence": [
        ["page_id_1", 1],
        ["page_id_2", 2],
    ]
}
```

```
# The claim cannot be verified
{
    "id": 1,
    "predicted_label": "NOT ENOUGH INFO",
    "predicted_evidence": None
}
```
- After creating the prediction file, please email the file to yingjia.lin.public@gmail.com with a brief description of your method. We will evaluate your submission and update the leaderboard.