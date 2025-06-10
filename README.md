# Report on Neural Network Model

## Overview

The purpose of this analysis is to help the nonprofit foundation Alphabet Soup to select the applicants for funding with the best chance of success in their ventures.

## Results

### Data Processing

* The target variable for the model is **"IS_SUCCESSFUL"**.
* The features used for prediction include:

* **APPLICATION_TYPE**
* **AFFILIATION**
* **CLASSIFICATION**
* **USE_CASE**
* **ORGANIZATION**
* **STATUS**
* **INCOME_AMT**
* **SPECIAL_CONSIDERATIONS**
* **ASK_AMT**
* The columns **EIN** and **NAME** were removed because they are neither features nor targets.

### Compiling, Training, and Evaluation of the Model

### Attempt 1

* **Compile:**

* Loss: `binary_crossentropy`
* Optimizer: `adam`
* Metrics: `accuracy`

* **Training:**

* Epochs: 50
* Batch size: 32
* Validation split: 20%
* Shuffle data every epoch
* ModelCheckpoint callback saves weights every 5 epochs

### Attempt 2

* **Compile:**

* Loss: `binary_crossentropy`
* Optimizer: `adam`
* Metrics: `accuracy`

* **Training:**

* Epochs: 60
* Batch size: 32
* Validation split: 20%
* ModelCheckpoint callback saves weights every 5 epochs

### Attempt 3

* **Compile:**

* Loss: `binary_crossentropy`
* Optimizer: `adam`
* Metrics: `accuracy`

* **Training:**

* Epochs: 50
* Batch size: 32
* Validation split: 20%
* Added **EarlyStopping** callback to prevent overfitting (monitor `val_loss`, patience 5)
* Restores best weights on early stopping

### Conclusion

| **Attempt** | **Hidden Layers & Neurons** | **Activation Functions** | **Epochs** | **Accuracy (%)** | **Loss** | **Notes** |
| ----------- | -------------------------------------- | ------------------------ | ---------- | ---------------- | -------- | -------------------------------- |
| Attempt 1 | 2 layers: 256, 128 | ReLU | 50 | 72.47 | 0.5624 | Basic model, no dropout |
| Attempt 2 | 3 layers: 512, 256, 64 | Tanh | 60 | 72.54 | 0.5552 | Larger model, more complex |
| Attempt 3 | 2 layers: 128, 64 + Dropout (0.3, 0.2) | ReLU | 50 | 72.54 | 0.5552 | Added dropout and early stopping |


All three attempts achieved an accuracy just below the target of 75%. Attempts 2 and 3 showed small improvements in loss and accuracy compared to Attempt 1, but none surpassed the 75% threshold. Early stopping and dropout helped maintain model generalization but did not significantly increase accuracy.

