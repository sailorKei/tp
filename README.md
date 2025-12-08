# Deepfake Detection using XceptionNet (FaceForensics++ C23)

This project performs binary classification (**Real vs Deepfake**) using a **pretrained XceptionNet** model fined-tuned on the **FaceForensics++ C23 dataset**.

---

## 📁 Project Structure

deepfake-xception/
│── notebooks/
│     └── deepfake_xception.ipynb   ← Main notebook
│
│── models/
│     └── best_xception_deepfake.pth   ← Saved model weights
│
│── data/
│     └── README.md   ← Instructions to download the dataset
│
│── requirements.txt
│── README.md

---

## ⚙️ Installation

### 1) Create Python environment (3.10 recommended)

```bash
python -m venv labenv310
.\labenv310\Scriptsctivate
```

### 2) Install required libraries

```bash
pip install -r requirements.txt
```

---

## 🗂️ Dataset — FaceForensics++ C23

Download from Kaggle:

https://www.kaggle.com/datasets/fatimahirshad/faceforensics-extracted-dataset-c23

Classes:
- **0 = Original**
- **1 = Deepfake**

Folder structure:

faceforensics_c23/
│── CSVS/
│     ├── Original.csv
│     └── Deepfakes.csv
│
└── FF++C23-Frames/
      ├── Original/
      └── Deepfakes/

⚠️ The dataset is **NOT included** in this repository due to size.  
Please download and place it in `./faceforensics_c23/`.

---

## 🧠 Model — XceptionNet

We use **XceptionNet** through the `timm` library.

### Key characteristics:
- **State-of-the-art architecture** for image forensics
- **Pretrained on ImageNet**
- Depthwise separable convolutions
- Adapted for **binary classification**

### Customization:
- Final layer changed from **1000 outputs → 2 outputs**
- Fine-tuned on our dataset (transfer learning)

### Optimization:
- Loss: `CrossEntropyLoss`
- Optimizer: `AdamW(lr=1e-4, weight_decay=1e-4)`
- Scheduler: `ReduceLROnPlateau` (reduces LR when validation stalls)
- Regularization: L2 (weight decay)
- Early stopping: patience = 3 epochs

---

## 📊 Results

### 🔢 Metrics
| Metric | Value |
|------|------|
Validation Accuracy (best) | ~80.5 %  
Test Accuracy | ~75.6 %  

### 🧮 Confusion Matrix
|               | Pred Original | Pred Deepfake |
|---------------|----------------|----------------|
| True Original | 811 | 189 |
| True Deepfake | 299 | 701 |

### 📝 Classification Report
- Original: Recall = **0.81**
- Deepfake: Precision = **0.79**

📌 Interpreting results:
- The model performs well overall.
- Detecting compressed/realistic deepfakes remains challenging (consistent with literature).

---

## 📓 Notebook

Everything (data loading, training, evaluation, metrics) is inside:

```
notebooks/deepfake_xception.ipynb
```

---

## 🧑‍🔬 Scientific Reference

**FaceForensics++: Learning to Detect Manipulated Facial Images**  
Rössler et al., ICCV 2019.

---

## 🏷️ License

Educational use only.
