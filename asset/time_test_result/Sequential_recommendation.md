## Time  and memory cost of sequential recommendation models 

### Datasets information:

| Dataset    | #User   | #Item  | #Interaction | Sparsity |
| ---------- | ------- | ------ | ------------ | -------- |
| ml-1m      | 6,041   | 3,707  | 1,000,209    | 0.9553   |
| DIGINETICA | 59,425  | 42,116 | 547,416      | 0.9998   |
| Yelp       | 102,046 | 98,408 | 2,903,648    | 0.9997   |

### 1) ml-1m dataset:

#### Time and memory cost on ml-1m dataset:

| Method           | Training Time (s) | Evaluate Time (s) | Memory (GB) |
| ---------------- | -----------------: | -----------------: | -----------: |
| Improved GRU-Rec | 7.78              | 0.11              | 1.27     |
| SASRec           | 17.78             | 0.12              | 1.84     |
| NARM             | 8.29              | 0.11              | 1.29     |
| FPMC             | 7.51              | 0.11              | 1.18     |
| STAMP            | 7.32              | 0.11              | 1.20     |
| Caser            | 44.85             | 0.12              | 1.14     |
| NextItNet        | -               | - | - |
| TransRec         | 10.08             | 0.16              | 8.18     |
| S3Rec            | - | - | -       |
| GRU4RecF         | 10.20             | 0.15              | 1.80     |
| SASRecF          | 18.84             | 0.17              | 1.78    |
| BERT4Rec         | 36.09             | 0.34              | 1.97    |
| FDSA             | 31.86             | 0.19              | 2.32     |
| SRGNN            | 327.38            | 2.19              | 1.21     |
| GCSAN            | 335.27            | 0.02             | 1.58     |
| KSR              | - | - | - |
| GRU4RecKG        | - | - | - |

#### Config file of ml-1m dataset:

```
# dataset config
field_separator: "\t"
seq_separator: " "
USER_ID_FIELD: user_id
ITEM_ID_FIELD: item_id
TIME_FIELD: timestamp
NEG_PREFIX: neg_
ITEM_LIST_LENGTH_FIELD: item_length
LIST_SUFFIX: _list
MAX_ITEM_LIST_LENGTH: 20
POSITION_FIELD: position_id
load_col:
  inter: [user_id, item_id, timestamp]
min_user_inter_num: 0
min_item_inter_num: 0

# training and evaluation
epochs: 500
train_batch_size: 2048
eval_batch_size: 2048
valid_metric: MRR@10
eval_setting: TO_LS,full
training_neg_sample_num: 0
```

**NOTE :** 

1) For FPMC and TransRec model,  `training_neg_sample_num`  should be  `1` . 

2) For  SASRecF, GRU4RecF and FDSA,   `load_col` should as below:

```
load_col:
  inter: [user_id, item_id, timestamp]
  item: [item_id, genre]
```

### 2）DIGINETICA dataset:

#### Time and memory cost on DIGINETICA dataset:

| Method           | Training Time (s) | Evaluate Time (s) | Memory (GB) |
| ---------------- | -----------------: | -----------------: | -----------: |
| Improved GRU-Rec | 4.10              | 1.05              | 4.02     |
| SASRec           | 8.36              | 1.21              | 4.43     |
| NARM             | 4.30              | 1.08              | 4.09     |
| FPMC             | 2.98              | 1.08              | 4.08     |
| STAMP            | 4.27              | 1.04              | 3.88     |
| Caser            | 17.15             | 1.18              | 3.94    |
| NextItNet        | - | - | - |
| TransRec         | -                 | -                 | -           |
| S3Rec            | - | - | - |
| GRU4RecF         | 4.79              | 1.17              | 4.83     |
| SASRecF          | 8.66              | 1.29              | 5.11     |
| BERT4Rec         | 16.80             | 3.54              | 7.97    |
| FDSA             | 13.44             | 1.47              | 5.66     |
| SRGNN            | 88.59             | 15.37             | 4.01     |
| GCSAN            | 96.69             | 17.11             | 4.25     |
| KSR              | - | - | - |
| GRU4RecKG        | - | - | - |

#### Config file of DIGINETICA dataset:

```
# dataset config
field_separator: "\t"
seq_separator: " "
USER_ID_FIELD: session_id
ITEM_ID_FIELD: item_id
TIME_FIELD: timestamp
NEG_PREFIX: neg_
ITEM_LIST_LENGTH_FIELD: item_length
LIST_SUFFIX: _list
MAX_ITEM_LIST_LENGTH: 20
POSITION_FIELD: position_id
load_col:
  inter: [session_id, item_id, timestamp]
min_user_inter_num: 6
min_item_inter_num: 1

# training and evaluation
epochs: 500
train_batch_size: 2048
eval_batch_size: 2048
valid_metric: MRR@10
eval_setting: TO_LS,full
training_neg_sample_num: 0
```

**NOTE :** 

1) For FPMC and TransRec model,  `training_neg_sample_num`  should be  `1` . 

2) For  SASRecF, GRU4RecF and FDSA,   `load_col` should as below:

```
load_col:
   inter: [session_id, item_id, timestamp]
   item: [item_id, item_category]
```



