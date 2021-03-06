# Overview

This is the third assignment for the course NLP (CSE-538) at Stony Brook University during Fall 19.

This repo is an implementation of a neural Dependency Parsing model by using the following papers as a guide:

From Incrementality in Deterministic Dependency Parsing (2004, Nivre)
- the arc-standard algorithm

From A Fast and Accurate Dependency Parser using Neural Networks (2014, Danqi and Manning)

- feature extraction
- the neural network architecture including activation function
- loss function


# Installation

The environment is same as assignment 2. But we would *strongly* encourage you to make a new environment for assignment 3.

This assignment is implemented in python 3.6 and tensorflow 2.0. Follow these steps to setup your environment:

1. [Download and install Conda](http://https://conda.io/projects/conda/en/latest/user-guide/install/index.html "Download and install Conda")
2. Create a Conda environment with Python 3.6
```
conda create -n nlp-hw3 python=3.6
```

3. Activate the Conda environment. You will need to activate the Conda environment in each terminal in which you want to use this code.
```
conda activate nlp-hw3
```
4. Install the requirements:
```
pip install -r requirements.txt
```

5. Download glove wordvectors:
```
./download_glove.sh
```

**NOTE:** We will be using this environment to check your code, so please don't work in your default or any other python environment.


# Data

You have training, development and test set for dependency parsing in conll format. The `train.conll` and `dev.conll` are labeled whereas `test.conll` is unlabeled

For quick code development/debugging, this time we have explicitly provided small fixture dataset. You can use this as training and development dataset while working on the code.


# Code Overview

## Train, Predict, Evaluate


You have three scripts in the repository `train.py`, `predict.py` and `evaluate.py` for training, predicting and evaluating a Dependency Parsing Model. You can supply `-h` flag to each of these to figure out how to use these scripts.

Here we show how to use the commands with the defaults.


#### Train a model
```
python train.py data/train.conll data/dev.conll

# stores the model by default at : serialization_dirs/default
```

#### Predict with model
```
python predict.py serialization_dirs/default \
                  data/dev.conll \
                  --predictions-file dev_predictions.conll
```

#### Evaluate model predictions

```
python evaluate.py serialization_dirs/default \
                   data/dev.conll \
                   dev_predictions.conll
```


## Dependency Parsing

  - `lib.model:` Defines the main model class of the neural dependency parser.

  - `lib.data.py`: Code dealing with reading, writing connl dataset, generating batches, extracting features and loading pretrained embedding file.

  - `lib.dependency_tree.py`: The dependency tree class file.

  - `lib.parsing_system.py`: This file contains the class for a transition-based parsing framework for dependency parsing.

  - `lib.configuration.py`: The configuration class file. Configuration reflects a state of the parser.

  - `lib.util.py`: This file contain function to load pretrained Dependency Parser.

  - `constants.py`: Sets project-wide constants for the project.



## What experiments to try

You can try experiments to figure out the effects of following on learning:

1. activations (cubic vs tanh vs sigmoid)
2. pretrained embeddings
3. tunability of embeddings

The file `experiments.sh` enlists the commands you will need to train and save these models.

As shown in the `experiments.sh`, you can use `--experiment-name` argument in the `train.py` to store the models at different locations in `serialization_dirs`. You can also use `--cache-processed-data` and `--use-cached-data` flags in `train.py` to not generate the training features everytime. Please look at training script for details. Lastly, after training your dev results will be stored in serialization directory of the experiment with name `metric.txt`.

Take a look at the report.pdf to find my report and findings as part of this assignment.