# CAFA 5

This is the [CAFA 5](https://www.kaggle.com/competitions/cafa-5-protein-function-prediction) dataset of 142k protein sequences annotated with their gene ontology (GO) terms. The samples are divided into three subsets each containing a set of GO terms that are associated with one of the three subgraphs of the gene ontology - Molecular Function, Biological Process, and Cellular Component. In addition, we provide a stratified train/test split that utilizes term embeddings to distribute term labels equally. The term embeddings are included in the dataset and can be used to stratify custom splits or to search for sequences with similar gene ontologies.

The code to export this dataset can be found [here](https://github.com/andrewdalpino/CAFA5).

## Subsets

The [CAFA 5](https://huggingface.co/datasets/andrewdalpino/CAFA5) dataset is available on HuggingFace Hub and can be loaded using the HuggingFace [Datasets](https://huggingface.co/docs/datasets) library. 

The dataset is divided into three subsets according to the GO terms that the sequences are annotated with.

- `all` - All annotations
- `mf` - Only molecular function terms
- `cc` - Only celluar component terms
- `bp` - Only biological process terms

To load the default CAFA 5 dataset with all function annotations you can use the example below.

```python
from datasets import load_dataset

dataset = load_dataset("andrewdalpino/CAFA5")
```

To load a subset of the CAFA 5 dataset use the example below.

```python
dataset = load_dataset("andrewdalpino/CAFA5", "mf")
```

## Splits

We provide a 90/10 `train` and `test` split for your convenience. The subsets were determined using a stratified approach which assigns cluster numbers to sequences based on their terms embeddings. We've included the stratum IDs so that you can generate additional custom stratified splits as shown in the example below.

```python
from datasets import load_dataset

dataset = load_dataset("andrewdalpino/CAFA5", split="train")

dataset = dataset.class_encode_column("stratum_id")

dataset = dataset.train_test_split(test_size=0.2, stratify_by_column="stratum_id")
```

## Filtering

You can also filter the samples of the dataset like in the example below.

```python
dataset = dataset.filter(lambda sample: sample["length"] <= 2048)
```

## Tokenizing

Some tasks may require you to tokenize the amino acid sequences. In this example, we loop through the samples and add a `tokens` column to store the tokenized sequences.

```python
def tokenize(sample: dict): list[int]:
    tokens = tokenizer.tokenize(sample["sequence"])

    sample["tokens"] = tokens

    return sample

dataset = dataset.map(tokenize, remove_columns="sequence")
```

## Original Dataset

Iddo Friedberg, Predrag Radivojac, Clara De Paolis, Damiano Piovesan, Parnal Joshi, Walter Reade, and Addison Howard. CAFA 5 Protein Function Prediction. https://kaggle.com/competitions/cafa-5-protein-function-prediction, 2023. Kaggle.