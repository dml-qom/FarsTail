# FarsTail
**A Persian Natural Language Inference Dataset**


[![PyPI - Python Version](https://img.shields.io/pypi/pyversions/farstail?color=red)](https://pypi.org/project/farstail/)
[![PyPI](https://img.shields.io/pypi/v/farstail)](https://pypi.org/project/farstail/)
[![PyPI - Downloads](https://img.shields.io/pypi/dm/farstail?color=Purple)](https://pypi.org/project/farstail/)
[![PyPI - License](https://img.shields.io/pypi/l/farstail)](https://pypi.org/project/farstail/)

![alt-text](./farstail.png)
## Persian Natural Language Inference
Natural Language Inference (NLI) who is also called [Texual Entailment](https://en.wikipedia.org/wiki/Textual_entailment) is an important task in NLP that its goal is to determine the inference relationship between a premise p and a hypothesis h. It is a three-class problem, where each pair (p, h) is assigned to one of these classes: "ENTAILMENT" if the hypothesis can be inferred from the premise, "CONTRADICTION" if the hypothesis contradicts with the premise, and "NEUTRAL" if infering hypothesis from premise is not possible.
<br>In English, large datasets such as [SNLI](https://www.aclweb.org/anthology/D15-1075/), [MNLI](https://www.aclweb.org/anthology/N18-1101/), [SciTail](https://www.aaai.org/ocs/index.php/AAAI/AAAI18/paper/viewFile/17368/16067) are created for this task. Even for some other languages, datasets has been created that has improved this task in these languages. But we see this less for poor source languages like persian.
<br>Persian (Farsi) language is a [pluricentric language](https://en.wikipedia.org/wiki/Pluricentric_language) spoken by around 110 million people in countries such as Iran, Afghanistan, and Tajikistan. In this github, we present the first large scale Persian corpus for NLI task, called [FarsTail](https://arxiv.org/).
<br>
<br>

We divided the data into test, train, and dev based on the following distribution:

| Split |     Number   |
|-------|--------------|
| Train |     7266     |
| Dev   |     1537     |
| Test  |     1564     |

## Folder Structure

```bash
.
├──  data
│        ├── Indexed-FarsTail.npz
│        ├── Train-word.csv
│        ├── Val-word.csv
│        └── Test-word.csv
├── farstail_image.png
├── LICENSE
└── README.md
```

## Getting started with package
We have provided an API in the form of a python package to read and use FarsTail easier. In the following, we will explain how to use this package.
<br>You'll need Python 3.6 or higher.
### Installation
```
pip install farstail
```
### using
* Loading the the original FarsTail dataset.
```python
from farstail.datasets import farstail
train_data, val_data, test_data = farstail.load_original_data()
```


* Loading the the indexed FarsTail dataset.
```python
from farstail.datasets import farstail
train_ind, val_ind, test_ind, dictionary = farstail.load_indexed_data()
```

## results
|Model | Word2vec | fastText | ELMo | BERT |
| --- | --- | --- | --- | --- |
|**DecompAtt** | **0.6566** | 0.5831 | 0.5505 | 0.5722 |
|**ESIM** | 0.7110 | **0.7136** | 0.6873 | **0.7136** |
|**HBMP** | **0.6604** | 0.6521 | 0.6349 | 0.6432 |
|**Translate-Source** | 0.7653 | **0.7813** | ------ | 0.7519 |
|**Translate-Target** | 0.6822 | **0.7046** | ------ | 0.6899 |
<br>

| Model | Test Accuracy |
| --- | --- |
|**ULMFiT** | **0.7244** |
|**ESIM-BERT-XLing** | **0.7462** |

## License
The content of this project is licensed under the MIT license.

## References

Please cite our paper if you find this dataset, article or package useful.

[1] Hossein Amirkhani, Mohammad Azari Jafari, Azadeh Amirak, Zohreh Pourjafari, Soroush Faridan Jahromi and Zeinab Kouhkan, [FarsTail: A Persian Natural Language Inference Dataset](https://arxiv.org/abs/2009.08820), arxiv, 2020.

```bibtex
@inproceedings{Amirkhani2020FarsTail,
  title={FarsTail: A Persian Natural Language Inference Dataset},
  author={Hossein Amirkhani and Mohammad Azari Jafari and Azadeh Amirak and Zohreh Pourjafari and Soroush Faridan Jahromi and Zeinab Kouhkan},
  journal={arXiv preprint arXiv:2009.08820},
  year={2020}
}
```
