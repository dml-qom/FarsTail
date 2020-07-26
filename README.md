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
<table class="tg">
  <tr>
    <td class="tg-lboi" colspan="2" rowspan="2">premise</td>
    <td class="tg-lboi" align="right" dir="rtl">مجمع عمومی سازمان ملل متحد رسماً آنتونیو گوترش را بعنوان دبیرکل بعدي سازمان ملل متحد و جانشین بان کی مون انتخاب کرد.</td>
  </tr>
  <tr>
    <td class="tg-lboi">The United Nations General Assembly formally elected António Guterres as the next UN Secretary-General and Ban Kimoon's successor.</td>
  </tr>
  <tr>
    <td class="tg-lboi" rowspan="6">hypothesis</td>
    <td class="tg-lboi" rowspan="2">entailment</td>
    <td class="tg-lboi" align="right" dir="rtl">دبیر کل سازمان ملل متحد قبل از آنتونیو گوترش، بان کی مون بود.</td>
  </tr>
  <tr>
    <td class="tg-lboi">Ban Ki-moon was the Secretary-General of the United Nations before António Guterres.</td>
  </tr>
  <tr>
    <td class="tg-0pky" rowspan="2">contradiction</td>
    <td class="tg-0pky" align="right" dir="rtl">کوفی عنان پیش از آنتونیو گوترش بعنوان دبیر کل سازمان ملل متحد انتخاب شده بود.</td>
  </tr>
  <tr>
    <td class="tg-0pky">Before António Guterres, Kofi Annan had been selected as the United Nations Secretary-General.</td>
  </tr>
  <tr>
    <td class="tg-0pky" rowspan="2">neutral</td>
    <td class="tg-0pky" align="right" dir="rtl">اعضاي سازمان ملل متحد به اتفاق آرا آنتونیو گوترش را بعنوان نامزد دبیر کلی سازمان ملل متحد معرفی کردند.</td>
  </tr>
  <tr>
    <td class="tg-0pky">The United Nations members unanimously nominated António Guterres as UN Secretary-General.</td>
  </tr>
</table>

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
│        ├── train.csv
│        ├── devc.csv
│        └── test.csv
├──  models
│        ├── ESIM
│        │      ├── model.h5
│        │      └── code.ipynb
│        ├── HBMP
│        │      ├── model.h5
│        │      └── code.ipynb
│        ├── ULMFit
│        │      ├── model.h5
│        │      └── code.ipynb
│        ├── DecompAtt
│        │      ├── model.h5
│        │      └── code.ipynb
│        └── cross-lingual transfer learning
│               ├── model.h5
│               └── code.ipynb
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
* Loading the the FarsTail dataset.
```python
from farstail.datasets import farstail
(p_train, h_train, l_train), (p_dev, h_dev, l_dev), (p_test, h_test, l_test) = farstail.load_data()
```

* Retrieving a dict mapping words to their index in the IMDB dataset.
```python
from farsfail.datasets import farstail
farstail_word_index = farstail.get_word_index()
```

## results
|Model | Word2vec | fastText | BERT |
| --- | --- | --- | --- |
|**ESIM** | 81.1 | 86.3 | 92.4 |
|**HPMP** | 79.4 | 83.1 | **93.7** |
|**ULMFIT** | 81.5 | 86.4 | 92.7 |
|**DecompAtt** | 81.5 | 86.4 | 92.7 |
|**X-Ling transfer learning** | 81.5 | 86.4 | 92.7 |


## License
The content of this project is licensed under the AAA license.

## References

Please cite our paper if you find this dataset, article or package useful.

[1] authors. 2020. [FarsTail: A Persian Natural Language Inference Dataset](https://arxiv.org/). dml-qom. 25 (4), 467-482.

```bibtex
@Article{dml-qom2020,
  author        = {dml-qom},
  title         = {FarsTail: A Persian Natural Language Inference Dataset},
  journal       = {arxiv.org},
  year          = {2020},
  month         = {oct}
}
```
