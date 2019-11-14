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
emotions_bustai
│   README.md 
│   requirements.txt
|   train_transformer_model.py   <- main python file to execute
├── data
│   │   Data Analysis.ipynb      <- notebook for data analysis
│   │   train_en.csv             <- data
│   │   train_fr.csv             <- data
│   │   val_en.csv               <- data
│   ├── preprocessed_data        <- preprocessed data
│       │   train_examples.pkl
│       │   validation_examples.pkl
├── images                       <- images 
|   │   logo.svg
|   │   run_han.png
|   │   run_roberta.png
|   │   run_xlnet.png
|   │   wheel.png
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
