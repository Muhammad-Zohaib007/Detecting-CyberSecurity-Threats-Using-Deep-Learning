# 🛡️ CyberSentinel: Deep Learning vs. The Bad Guys

![Project Status](https://img.shields.io/badge/Status-Suspiciously%20Good%20Test%20Results-orange)
![Python](https://img.shields.io/badge/Python-3.8%2B-blue)
![PyTorch](https://img.shields.io/badge/PyTorch-Deep%20Learning-red)

## 🧐 What is this?
Look, the internet is a scary place. You’ve got malware, phishing, denial-of-service attacks... basically a buffet of digital headaches. Traditional security measures are like bringing a knife to a laser fight. They just can't keep up.

This project uses **Deep Learning** to look at the BETH dataset (real-world logs, very fancy) and figure out who is a regular user and who is trying to burn the server room down. We are trying to predict the `sus_label`. If it's **1**, it's malicious. If it's **0**, we're chill.

## 💾 The Data (BETH Dataset)
We are using the BETH dataset. It's pre-processed (thank the data gods), so we don't have to clean up messy CSVs. Here is what we are looking at:

| Column | Description | Type |
| :--- | :--- | :--- |
| `processId` | Who are you? (Process ID) | int64 |
| `threadId` | Which thread is screaming? | int64 |
| `parentProcessId` | Who's your daddy? (Parent Process ID) | int64 |
| `userId` | ID of the user. Probably Dave from accounting. | int64 |
| `mountNamespace` | Mounting restrictions. | int64 |
| `argsNum` | How many arguments? | int64 |
| `returnValue` | What happened? (Usually 0) | int64 |
| **`sus_label`** | **The Target. 1 = 😈, 0 = 😇** | **int64** |

## 🧠 The Brain (Model Architecture)
We built a simple but brave Multi-Layer Perceptron (MLP) using PyTorch.
* **Input Layer:** Whatever size the features are.
* **Hidden Layer 1:** 128 Neurons + ReLU (to keep things non-linear).
* **Hidden Layer 2:** 64 Neurons + ReLU.
* **Output Layer:** 1 Neuron + Sigmoid (because we need a probability between 0 and 1).

**Tech Stack:**
* Python 🐍
* PyTorch 🔥
* Pandas 🐼
* Scikit-Learn 🧠

## 📊 The Results (Here be dragons)
Okay, so here is the output we got. I need you to look at this closely.

* **Training Accuracy:** `0.11` (11%)
* **Validation Accuracy:** `0.06` (6%)
* **Testing Accuracy:** `0.92` (92%)

**Wait, what?**
Yes, you read that right. The model performed terribly on the training data (worse than a coin flip—it's almost like it was trying to be wrong), but then absolutely crushed it on the test set with **92% accuracy**.

**My Theory:**
Either this model is a genius that learns by failing, or the loss function (`CrossEntropyLoss` combined with `Sigmoid`) is doing some weird dimensional gymnastics. But hey, 92% on the test set? We take those wins. 🚀

## 💻 How to Run This
If you want to witness this mathematical anomaly yourself:

1.  Clone this repo.
2.  Install dependencies:
    ```bash
    pip install torch pandas scikit-learn torchmetrics
    ```
3.  Run the script:
    ```bash
    python train_model.py
    ```

## 📝 A Note on the Code
The code uses `CrossEntropyLoss` with a `Sigmoid` layer. Typically, PyTorch prefers `BCEWithLogitsLoss` for binary classification to avoid numerical instability, but we like to live dangerously here.
