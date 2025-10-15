
# 📘 Overview

This project aims to train a BERT-based sentiment classification model to identify the emotional tendency of movie reviews as either **positive** or **negative**.

* **Dataset**: The Large Movie Review Dataset, which contains 25,000 positive and 25,000 negative movie reviews for training and testing.
* **Model**: The project uses **BERT (Bidirectional Encoder Representations from Transformers)** for fine-tuning. BERT is a pre-trained deep bidirectional transformer model that excels at understanding language context.
* **Task**: To train a BERT classification model that takes a piece of text as input and outputs its sentiment category.

The assignment requires completing the `TODO` items in the code to ensure the model can be successfully trained and produce a Testing Accuracy result.

# ⚙️ Training Flow

The project's training workflow can be divided into the following steps:

## 1. Data Preparation and Processing
* **Load Data**: Load the `imdb` dataset, which includes `train` and `test` subsets.
* **Merge and Split Data**: The original training and testing sets are merged and then re-split into a new **training (train)**, **validation (val)**, and **testing (test)** set, with an 8:1:1 ratio.
* **Custom `Dataset`**: A `CustomDataset` class is created to handle the data. In this class, `AutoTokenizer` is used to convert the raw text into the input format required by the BERT model, including `input_ids`, `attention_mask`, and `token_type_ids`.

## 2. Model Construction
* **`BertClassifier`**: A custom classifier inheriting from `BertPreTrainedModel` is built. The model consists of a BERT base model followed by a `Dropout` layer and a `Linear` layer (the classifier).
* **Model Output**: The model's `forward` function passes the sentence representation (the output of the `[CLS]` token) from BERT to the classifier layer, finally outputting the raw logits without a Softmax activation.

## 3. Training and Evaluation
* **Hyperparameter Settings**: The model's hyperparameters are defined, such as `model_name`, `learning_rate`, `epochs`, `batch_size`, and `dropout`.
* **Initialization**: The pre-trained `bert-base-uncased` model is loaded, and the optimizer (`Adam`) and loss function (`CrossEntropyLoss`) are defined.
* **Training Loop**: In each epoch, the model performs the following steps:
    1.  The data is passed to the model for training.
    2.  The loss is calculated, and backpropagation (`loss.backward()`) is performed.
    3.  The optimizer is used to update the model parameters (`optimizer.step()`).
    4.  The loss and metrics (accuracy, F1-score, recall, and precision) are calculated and recorded for the training set.
    5.  After each epoch, the model's performance is evaluated on the validation set (`val_loader`), and the metrics are recorded.
* **Model Saving**: After training is complete, the trained model weights are saved to a file named `bert.pt`.

## 4. Prediction and Results

* **Single-entry Prediction**: The `predict_one()` function is available to input a single text query and use the trained model to predict its sentiment category.
* **Batch Prediction**: The `predict()` function can be used to pass the entire test set to the model for prediction, and the results are saved as `result.tsv`.
* **Final Accuracy**: Finally, the overall accuracy of the model on the test set is calculated and printed.

---
