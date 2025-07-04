# CFEVER-data

## Introduction to CFEVER
This repository contains the dataset for our AAAI 2024 paper, "CFEVER: A Chinese Fact Extraction and VERification Dataset". [Paper link](https://doi.org/10.1609/aaai.v38i17.29825).

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
├── README.md
└── sample_submission.jsonl # sample submission file of the test set
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
- Please refer to our codebase: https://github.com/IKMLab/CFEVER-baselines/?tab=readme-ov-file#evaluations

## Submission
- Please include three fields (necessary) in the prediction file for each claim in the test set.
    - `id`
    - `predicted_label`
    - `predicted_evidence`
- The `id` field has been already included in [the test set](data/test.jsonl). Please do not change the order.
- The `predicted_label` should be one of `supports`, `refutes`, or `NOT ENOUGH INFO`.
- The `predicted_evidence` should be a list of evidence sentences, where each evidence sentence is represented by a list of `[page_id, line_number]`. For example:

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
- A randomly generated submission file can be found [here](sample_submission.jsonl).
    - Note that `claim` is not necessary to be included in the submission file.
- You can also check [the prediction example for the development set](https://github.com/IKMLab/CFEVER-baselines/blob/main/simple_baseline/data/dumb_dev_pred.jsonl) and follow [the evaluation steps](https://github.com/IKMLab/CFEVER-baselines/tree/main?tab=readme-ov-file#sentence-retrieval-and-claim-verification) from [our CFEVER-baselines repo](https://github.com/IKMLab/CFEVER-baselines).


## Reference
If you find our work useful, please cite our paper.
```
@article{Lin_Lin_Yeh_Li_Hu_Hsu_Lee_Kao_2024,
    title = {CFEVER: A Chinese Fact Extraction and VERification Dataset},
    author = {Lin, Ying-Jia and Lin, Chun-Yi and Yeh, Chia-Jen and Li, Yi-Ting and Hu, Yun-Yu and Hsu, Chih-Hao and Lee, Mei-Feng and Kao, Hung-Yu},
    doi = {10.1609/aaai.v38i17.29825},
    journal = {Proceedings of the AAAI Conference on Artificial Intelligence},
    month = {Mar.},
    number = {17},
    pages = {18626-18634},
    url = {https://ojs.aaai.org/index.php/AAAI/article/view/29825},
    volume = {38},
    year = {2024},
    bdsk-url-1 = {https://ojs.aaai.org/index.php/AAAI/article/view/29825},
    bdsk-url-2 = {https://doi.org/10.1609/aaai.v38i17.29825}
}
```
