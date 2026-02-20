\# CSCI 455/555: GenAI for SD - Assignment 1



\## Recommending Code Tokens via N-gram Models



This repository implements an end-to-end NLP pipeline that mines Java repositories, preprocesses method-level code, and trains probabilistic N-gram language models for code completion tasks.



---



\## Dependencies \& Installation



This project requires \*\*Python 3.10+\*\*. The following libraries are used for parsing, repository management, and data handling:



\* `javalang`: Parsing and tokenizing Java source code.

\* `gitpython`: Automated repository cloning.

\* `pandas`: Managing repository metadata.



Install dependencies via pip (already implemented in the jupyter notebook):



```bash

pip install javalang gitpython pandas



```



---



\## Execution Guide



The entire pipeline—from data mining to model evaluation—is contained within `N\_gram\_training.ipynb`.



1\. \*\*Setup\*\*: Run file locally (recommended) and install and import relevant packages.

2\. \*\*Setup\*\*: Ensure ample storage space and a connection to allow the script to clone up to 500 top Java repositories from Github

3\. \*\*Workflow\*\*: Run the notebook cells sequentially to perform the following:

\* \*\*Data Mining\*\*: Fetch, clone, and parse Java repositories.

\* \*\*Preprocessing\*\*: Clean, filter (removing non-ASCII and methods with <10 tokens), and deduplicate.

\* \*\*Vocabulary Building\*\*: Map unseen validation/test tokens to `<UNK>`.

\* \*\*Training\*\*: Train 3-gram, 5-gram, and 7-gram models across , , and  splits.

\* \*\*Evaluation\*\*: Generate predictions and export results.







---



\## Project Structure \& Outputs



All .json and .txt files are stored in `dataset/ngram\_dataset/`.

Cloned Github repos are stored in `dataset/java\_repos`



\### Dataset Splits



\* `train\_T1.txt` / `train\_T2.txt` / `train\_T3.txt`: Training sets capped at 15k, 25k, and ~35k methods respectively.

\* `val.txt`: 1,000 methods for validation.

\* `test.txt`: 1,000 methods (self-created test set).

\* `given\_test.txt`: 1,000 methods (provided test set).



\### Evaluation \& Metadata



\* `results-self-test.json`: Predictions and probabilities for the self-created test set.

\* `results-given-test.json`: Predictions and probabilities for the instructor-provided test set.

\* `metadata.json`: Logs specific repositories and files.



---



\## Model Hyper-parameters



\* \*\*Context Windows (n): {3, 5, 7}\*\* 

\* \*\*Smoothing:\*\* Add-alpha smoothing to handle unseen n-grams and prevent zero-probability errors.

\* \*\*Alpha (): 0.1\*\* 

\* \*\*Backoff Strategy:\*\* The model goes to the most frequent unigram from the training distribution if unseen context is encountered.



---



