This repository contains the implementation of RE-Net.


## Installation
Install PyTorch (>= 0.4.0) and DGL following the instuctions on the [PyTorch](https://pytorch.org/) and [DGL](https://www.dgl.ai).
Our code is written in Python3.

## Train and Test
Before running, you should preprocess datasets.

```bash
cd data/DATA_NAME
python3 get_history_graph.py
```

Then, we are ready to train and test.
We first pretrain the global model.
```bash
python3 pretrain.py -d DATA_NAME --gpu 0 --dropout 0.5 --n-hidden 200 --lr 1e-3 --max-epochs 20 --batch-size 1024
```

Then, we train the model.
```bash
python3 train.py -d DATA_NAME --gpu 0 --dropout 0.5 --n-hidden 200 --lr 1e-3 --max-epochs 20 --batch-size 1024
```

We are ready to test!
```bash
python3 test.py -d DATA_NAME --gpu 0 --n-hidden 200
```

The default hyperparameters give the best performances.


## Datasets
There are five datasets: [ICEWS18](https://dataverse.harvard.edu/file.xhtml?persistentId=doi:10.7910/DVN/28075/Z1ZFYG&version=25.0), [GDELT](https://blog.gdeltproject.org/gdelt-2-0-our-global-world-in-realtime/), [ICEWS14](https://dataverse.harvard.edu/file.xhtml?persistentId=doi:10.7910/DVN/28075/K7L9Y8&version=25.0), [WIKI](https://www.wikidata.org/wiki/Wikidata:Main_Page), and [YAGO](https://www.mpi-inf.mpg.de/departments/databases-and-information-systems/research/yago-naga/yago/).
Each data folder has 'stat.txt', 'train.txt', 'valid.txt', 'test.txt', and 'get_history_graph.py'.
- 'get_history_graph.py': This is for getting history and graph for model 3.
- 'stat.txt': First value is the number of entities, and second value is the number of relations.
- 'train.txt', 'valid.txt', 'test.txt': First column is subject entities, second column is relations, and third column is object entities. The fourth column is time. The fifth column is for know-evolve's data format. It is ignored in RE-Net.

## Baselines
We use public codes for baselines and hyperparameters. We validated embedding sizes among presented values.

We implemented TA-TransE, TA-DistMult, and TTransE. The user can run the baselines by the following command.

```bash
cd ./baselines
CUDA_VISIBLE_DEVICES=0 python3 TA-TransE.py -f 1 -d ICEWS18 -L 1 -bs 1024 -n 1000
```

The reviwers can find implementations in the 'baselines' folder.

