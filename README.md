<img src="https://pbs.twimg.com/profile_images/1126981606533672960/H4NiVXXg.jpg" alt="drawing" width="200"/>

## Fact verification on news - BusterAI
The goal of this project is to create an IA to check the facts of news sentence based on their evidences.

The evidence text either _supports_ or _refutes_ the claim.


### Requirements

In order to be able to execute the following steps, you will need to create a Python 3.7 Environement.
This can be done by:

```bash
pip install requirements.txt
```

### Directory Structure

```
fact_verification_news_busterai
│   README.md 
│   requirements.txt
|   Merge all datasets.ipynb   <- notebook to merge data 
├── fever_data_prep
│   │   FEVER_data_preparation_and_analysis.ipynb  
│   ├── preprocessed_data      <- preprocessed data
│   |   │   fever_train.pkl
│   |   │   fever_dev.pkl
│   |   │   fever_test.pkl
|   ├── data        <- raw data 
│       │   license.html
|       ├── fever_data
|       |   dev.jsonl
|       |   test.jsonl
|       |   train.jsonl
├── hoaxes_data_prep
│   │   hoaxes_data_preparation_and_analysis.ipynb  
│   ├── preprocessed_data      <- preprocessed data
│   |   │   hoaxes.pkl
├── liar_plus_dataset_prep
│   │   LiarPlus_data_preparation_and_analysis.ipynb
│   ├── preprocessed_data      <- preprocessed data
│   |   │   liar_plus_test.pkl
│   |   │   liar_plus_train.pkl
│   |   │   liar_plus_val.pkl
|   ├── data                   <- raw data 
|   |   test2.tsv
|   |   train2.tsv
|   |   val2.tsv
|   ├── .ipynb_checkpoints        <- checkpoints 
|   |   LiarPlus Analysis and Preparation checkpoint.ipynb
|   
├── runs                        <- cache memory from executions
|   │   
|   ├── Nov09_22-09-39_Station-TitanX-Xp
│   |   │   events.out.tfevents.1573333779.Station-TitanX-Xp
|   ├── Nov09_23-33-23_Station-TitanX-Xp
│       │   events.out.tfevents.1573338803.Station-TitanX-Xp
|   ├── Nov10_00-18-01_Station-TitanX-Xp
│   |   │   events.out.tfevents.1573341481.Station-TitanX-Xp
├── utils                       <- useful functions and model
|   │   losses.py
|   │   metrics.py
|   │   multilabel_task.py
|   │   utils.py
|   │   xlm_for_multilabel.py

```


### 1 - Data Collection and Preparation

In order to perform this task, we are going to use mainly two datasets: FEVER and LIAR_PLUS. As the labels of those
datasets were not the same, we had to do the convertion of the labels from one dataset to the other, which is
explained in details in each data_preprocessing notebook.

Each folder named in which the name includes data_prep has a notebook for the data preparation step, if you want to
perform it by yourself. If not, each folder also contains a folder named preprocessed data, where preprocessed data can
be found.

In order to execute the merging of all dataset, use the notebook _Merge all datasets.ipynb_. 

### 2 - Model Training and Evaluation

In order to train the model in order to reproduce the results shown, use the following line of command:

```bash
python run_glue.py --data_dir dataset --model_type xlm --model_name_or_path xlm-clm-enfr-1024 --task_name buster --output_dir output --do_train --evaluate_during_training --do_eval 
```
If you do not want to perform evaluation during training, remove  the --evaluate_during_training parameter.

### 3 - Results 

In order to compare our results with current SOTA models, we have performed the evaluation on the test set of
the FEVER dataset.

|SentimentxModel|     Watson    |      ELMo     |     mLSTM     |     NVIDIA Transformer   |   XLM (ours)  | 
| ------------- | ------------- | ------------- | ------------- |       -------------      | ------------- | 
|     anger     |     0.498     |     0.614     |     0.548     |           0.771          |     0.763     |
| anticipation  |       -       |     0.294     |     0.275     |           0.403          |    **0.405**  |
|    disgust    |     0.331     |     0.662     |     0.576     |           0.764          |     0.760     |
|      fear     |     0.149     |     0.388     |     0.319     |           0.765          |     0.731     |
|      joy      |     0.684     |     0.734     |     0.651     |           0.818          |   **0.839**   |
|    sadness    |     0.359     |     0.531     |     0.491     |           0.691          |     0.691     |
|   surprise    |       -       |     0.154     |     0.122     |           0.400          |   **0.473**   |
|     trust     |       -       |     0.181     |     0.168     |           0.271          |   **0.286**   |
|    Average    |       -       |     0.445     |     0.394     |           0.610          |   **0.619**   |


### References

[1] Wolf, T., et al. "Huggingface’s transformers: State-of-the-art natural language processing." ArXiv, abs (1910).


[2] Soleimani, Amir, Christof Monz, and Marcel Worring. "BERT for Evidence Retrieval and Claim Verification." arXiv preprint arXiv:1910.02655 (2019).


