# CAFA 5

This is the [CAFA 5](https://www.kaggle.com/competitions/cafa-5-protein-function-prediction) dataset for protein function and taxonomy prediction. The original dataset was unformatted and scattered over multiple raw files. This version formats the dataset into tabular form so that it can be made useful to downstream machine learning and data analysis tasks.

The code to export this dataset can be found [here](https://github.com/andrewdalpino/CAFA5).

## Subsets

The dataset is divided into four subsets according to the GO terms that the sequences are annotated with.

- `all` - All annotations
- `mf` - Only molecular function terms
- `cc` - Only celluar component terms
- `bp` - Only biological process terms

## Splits

We provide a 90/10 `train` and `test` split for your convenience. The splits were determined using a stratified approach which assigns cluster numbers to sequences based on their terms embeddings. Accordingly, we expect that each split is a faithful representation of GO term distribution of the full set. 

## Example Usages

To load the default CAFA 5 dataset with all function annotations you can use the example below.

```python
from datasets import load_dataset

dataset = load_dataset("andrewdalpino/CAFA5")
```

To load a subset of the CAFA 5 dataset use the example below.

```python
dataset = load_dataset("andrewdalpino/CAFA5", "mf")
```

You can also specify a split to load like in the example below.

```python
dataset = load_dataset("andrewdalpino/CAFA5", split="train")
```

Filter records by the length of the sequence like in the example below.

```python
dataset = dataset.filter(lambda sample: sample["length"] <= 2048)
```

### Original Dataset Citation

Iddo Friedberg, Predrag Radivojac, Clara De Paolis, Damiano Piovesan, Parnal Joshi, Walter Reade, and Addison Howard. CAFA 5 Protein Function Prediction. https://kaggle.com/competitions/cafa-5-protein-function-prediction, 2023. Kaggle.