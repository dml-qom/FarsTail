## FarsTail: A Persian Natural Language Inference Dataset


![alt-text](./farstail.png)

Natural Language Inference (NLI), also called [Textual Entailment](https://en.wikipedia.org/wiki/Textual_entailment), is an important task in NLP with the goal of determining the inference relationship between a premise `p` and a hypothesis `h`. It is a three-class problem, where each pair `(p, h)` is assigned to one of these classes: "ENTAILMENT" if the hypothesis can be inferred from the premise, "CONTRADICTION" if the hypothesis contradicts the premise, and "NEUTRAL" if none of the above holds. 
<br>There are large datasets such as [SNLI](https://www.aclweb.org/anthology/D15-1075/), [MNLI](https://www.aclweb.org/anthology/N18-1101/), and [SciTail](https://www.aaai.org/ocs/index.php/AAAI/AAAI18/paper/viewFile/17368/16067) for NLI in English, but there are few datasets for poor-data languages like [Persian](https://en.wikipedia.org/wiki/Persian_language). 
<br>Persian (Farsi) language is a pluricentric language spoken by around 110 million people in countries like Iran, Afghanistan, and Tajikistan. Here, we present the first relatively large-scale Persian dataset for NLI task, called FarsTail. A total of 10,367 samples are generated from a collection of 3,539 multiple-choice questions. The train, validation, and test portions include 7,266, 1,537, and 1,564 instances, respectively. Please refer to [the manuscript](https://arxiv.org/abs/2009.08820) for more details.

## Reading data
To read the raw data in Persian alphabet, use the following code:
```python
train_data = pd.read_csv('data/Train-word.csv', sep='\t')
val_data = pd.read_csv('data/Val-word.csv', sep='\t')
test_data = pd.read_csv('data/Test-word.csv', sep='\t')
```
Each of `train_data`, `val_data`, and `test_data` variables has three columns, `premise`, `hypothesis`, and `label`.

Non-Persian researchers can use the following code to read the indexed data:
```python
with np.load('data/Indexed-FarsTail.npz', allow_pickle=True) as f:
    train_ind, val_ind, test_ind, dictionary = f['train_ind'], f['val_ind'], f['test_ind'], f['dictionary'].item()
```
Each of `train_ind`, `val_ind`, and `test_ind` is a numpy array with the shape of `(n, 3)`, where `n` is the number of samples in each set. Each entry in these arrays includes the tokenized, indexed version of the premise and hypothesis along with the respective label for one instance. The `dictionary` variable maps the indexes to tokens.


## Results
Here is test accuracies obtained by training some models on FarsTail’s training set. Please refer to the manuscript for more results. 

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
|**ESIM-BERT (FarsTail+MNLI)** | **0.7462** |

The Model folder includes one of the lightweight, high-accuracy trained models along with a `ipynb` file for using this model. This is the BiGRU model trained on BERT_concat (last row of Table 3 in the manuscript). 

## Reference

Please cite the following paper if you find this dataset useful.

```bibtex
@article{amirkhani2020farstail,
  title={FarsTail: A Persian Natural Language Inference Dataset},
  author={Hossein Amirkhani, Mohammad Azari Jafari, Azadeh Amirak, Zohreh Pourjafari, Soroush Faridan Jahromi, and Zeinab Kouhkan},
  journal={arXiv preprint arXiv:2009.08820},
  year={2020}
}
```
