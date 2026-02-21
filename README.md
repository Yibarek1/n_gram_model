---

## Predicting Code Tokens via N-gram Models

This repository implements an end-to-end NLP pipeline that mines Java repositories, preprocesses method-level code, and trains probabilistic N-gram language models for code completion tasks.

---

## Dependencies & Installation

This project requires **Python 3.10+**. The following libraries are used for parsing, repository management, and data handling:

* `javalang`: Parsing and tokenizing Java source code.
* `GitPython`: Automated repository cloning.
* `pandas`: Managing repository metadata.

Install the dependencies via pip (this setup is also included within the Jupyter Notebook):

```bash
pip install javalang GitPython pandas

```

---

## Execution Guide

The entire pipeline—from data mining to model evaluation—is contained within `N_gram_training.ipynb`.

1. **Setup**: Run the file locally (recommended) to install and import the relevant packages.
2. **Storage & Network**: Ensure ample storage space and a stable internet connection to allow the script to clone up to 500 top Java repositories from GitHub.
3. **Workflow**: Run the notebook cells sequentially to perform the following:
* **Data Mining**: Fetch, clone, and parse Java repositories.
* **Preprocessing**: Clean, filter (removing non-ASCII characters and methods with <10 tokens), and deduplicate the data.
* **Vocabulary Building**: Map unseen validation and test tokens to `<UNK>`.
* **Training**: Train 3-gram, 5-gram, and 7-gram models across the T1, T2, and T3 splits.
* **Evaluation**: Generate predictions and export the results.



---

## Project Structure & Outputs

All `.json` and `.txt` files are stored in `dataset/ngram_dataset/`.
Cloned GitHub repos are stored in `dataset/java_repos/`.

### Dataset Splits

* `train_T1.txt` / `train_T2.txt` / `train_T3.txt`: Training sets capped at 15k, 25k, and 35k methods, respectively.
* `val.txt`: 1,000 methods for validation.
* `test.txt`: 1,000 methods (self-created test set).
* `given_test.txt`: 1,000 methods (instructor-provided test set).

### Evaluation & Metadata

* `results-self-test.json`: Predictions and probabilities for the self-created test set.
* `results-given-test.json`: Predictions and probabilities for the instructor-provided test set.
* `metadata.json`: Logs specific repository and file information.

---

## Model Hyperparameters

* **Context Windows (n):** {3, 5, 7}
* **Smoothing:** Add- smoothing to handle unseen n-grams and prevent zero-probability errors.
* **Alpha:** Chose an alpha value of 0.1
* **Backoff Strategy:** The model falls back to the most frequent unigram from the training distribution if an unseen context is encountered.

---
