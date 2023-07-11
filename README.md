## FarsTail: a Persian natural language inference dataset


![alt-text](./farstail.png)

Natural Language Inference (NLI), also called [Textual Entailment](https://en.wikipedia.org/wiki/Textual_entailment), is an important task in NLP with the goal of determining the inference relationship between a premise `p` and a hypothesis `h`. It is a three-class problem where each pair `(p, h)` is assigned to one of these classes: "ENTAILMENT" if the hypothesis can be inferred from the premise, "CONTRADICTION" if the hypothesis contradicts the premise, and "NEUTRAL" if none of the above holds. 
<br>There are large datasets such as [SNLI](https://www.aclweb.org/anthology/D15-1075/), [MNLI](https://www.aclweb.org/anthology/N18-1101/), and [SciTail](https://www.aaai.org/ocs/index.php/AAAI/AAAI18/paper/viewFile/17368/16067) for NLI in English, but there are few datasets for poor-data languages like [Persian](https://en.wikipedia.org/wiki/Persian_language). 
<br>Persian (Farsi) language is a pluricentric language spoken by around 110 million people in countries like Iran, Afghanistan, and Tajikistan. Here, we present the first relatively large-scale Persian dataset for NLI task, called FarsTail. A total of 10,367 samples are generated from a collection of 3,539 multiple-choice questions. The train, validation, and test portions include 7,266, 1,537, and 1,564 instances, respectively. Please refer to [the manuscript](https://arxiv.org/abs/2009.08820) for more details.

## Reading data
To read the raw data in Persian alphabet, use the following code:
```python
train_data = pd.read_csv('data/Train-word.csv', sep='\t')
val_data = pd.read_csv('data/Val-word.csv', sep='\t')
test_data = pd.read_csv('data/Test-word.csv', sep='\t')
```
The `train_data` and `val_data` have three columns, `premise`, `hypothesis`, and `label`. The `test_data` has two more columns denoted as *hard(hypothesis)* and *hard(overlap)* which indicate whether or not each sample belongs to the hard subset based on the *hypothesis-only* and *overlap-based* biased models, respectively.

Non-Persian researchers can use the following code to read the indexed data:
```python
with np.load('data/Indexed-FarsTail.npz', allow_pickle=True) as f:
    train_ind, val_ind, test_ind, dictionary = f['train_ind'], f['val_ind'], f['test_ind'], f['dictionary'].item()
```
The `train_ind` and `val_ind` are numpy arrays with the shape of `(n, 3)` where `n` is the number of samples in each set. Each entry in these arrays includes the tokenized, indexed version of the premise and hypothesis along with the respective label for one instance. The entries of `test_ind` variable have two more elements corresponding to the *hard(hypothesis)* and *hard(overlap)* columns, respectively. The `dictionary` variable maps the indexes to tokens.


## Results
Here is test accuracies obtained by training some models on FarsTail training set. Please refer to the manuscript for more results. 

| Model | Test Accuracy | Hypothesis-only (Easy) | Hypothesis-only (Hard) | Overlap-based (Easy) | Overlap-based (Hard) |
| --- | --- | --- | --- | --- | --- |
|**DecompAtt (word2vec)** | **0.6662** | **0.7341** | **0.5823** | **0.7633** | **0.5404**|
|**HBMP (word2vec)** | **0.6604** | **0.7618** | **0.5350** | **0.7565** | **0.5360** |
|**ESIM (fastText)** | **0.7116** | **0.7931** | **0.6109** | **0.8120** | **0.5815** |
|**mBERT** | **0.8338** | **0.8763** | **0.7811** | **0.8981** | **0.7504** |


## Reference
If you use this dataset, please cite the following paper:

Hossein Amirkhani, Mohammad AzariJafari, Soroush Faridan-Jahromi, Zeinab Kouhkan, Zohreh Pourjafari, Azadeh Amirak (2023). [FarsTail: a Persian natural language inference dataset](https://doi.org/10.1007/s00500-023-08959-3). *Soft Computing*.

```bibtex
@article{amirkhani2023farstail,
  title={Farstail: A persian natural language inference dataset},
  author={Amirkhani, Hossein and AzariJafari, Mohammad and Faridan-Jahromi, Soroush and Kouhkan, Zeinab and Pourjafari, Zohreh and Amirak, Azadeh},
  journal={Soft Computing},
  year={2023},
  publisher={Springer},
  doi={10.1007/s00500-023-08959-3}
}
```
