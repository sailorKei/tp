# Détection de Deepfakes avec XceptionNet (FaceForensics++ C23)

Projet réalisé en PyTorch pour la classification d’images **Original vs Deepfake**  
en utilisant le modèle **XceptionNet pré-entraîné**.

---

## 📁 Structure du projet

deepfake-xception/
│── notebooks/
│ └── deepfake_xception.ipynb ← Notebook principal
│
│── models/
│ └── best_xception_deepfake.pth ← Poids sauvegardés
│
│── data/
│ └── README.md ← instructions pour télécharger le dataset Kaggle
│
│── requirements.txt
│── README.md

yaml
 

---

## 📦 Installation

### 1) Créer un environnement Python 3.10

```bash
python -m venv labenv310
.\labenv310\Scripts\activate
2) Installer les dépendances
bash
 
pip install -r requirements.txt

🗂️ Jeu de données FaceForensics++ C23
Dataset téléchargé depuis Kaggle :

👉 https://www.kaggle.com/datasets/fatimahirshad/faceforensics-extracted-dataset-c23

Classes utilisées :

0 : Original

1 : Deepfake

Données organisées en :

 
faceforensics_c23/
│── CSVS/
│     ├── Original.csv
│     └── Deepfakes.csv
│
└── FF++C23-Frames/
      ├── Original/
      └── Deepfakes/
⚠️ Le dataset n’est pas inclus dans ce repo (taille trop grande).
Merci de le télécharger et de le placer sous ./faceforensics_c23/.

🧠 Modèle utilisé : XceptionNet
Nous utilisons XceptionNet via la bibliothèque timm.

Caractéristiques :

Architecture State of the Art

Pré-entraînée sur ImageNet

Convolutions séparables en profondeur

Nous remplaçons uniquement la dernière couche pour 2 classes

Détails de l’optimisation :
Fonction de perte : CrossEntropyLoss

Optimiseur : AdamW (lr=1e-4)

Régularisation : weight_decay=1e-4 (L2)

Scheduler : ReduceLROnPlateau (réduction dynamique du LR)

Early stopping (patience = 3 epochs)

🧪 Résultats obtenus
🔢 Scores
Metric	Valeur
Validation Accuracy max	~80.5 %
Test Accuracy	~75.6 %

📊 Matrice de confusion (test)
Prédit Original	Prédit Deepfake
Vrai Original	811	189
Vrai Deepfake	299	701

📋 Rapport de classification (test)
Original : Recall = 0.81

Deepfake : Precision = 0.79

Conclusion :

Le modèle détecte bien les originaux.

Certains deepfakes compressés restent difficiles.

📓 Notebook fourni
Tout le code, l’entraînement, les tests et les métriques sont détaillés dans :

bash
 
notebooks/deepfake_xception.ipynb
🏗️ Framework utilisé
PyTorch

timm

Transfert learning

GPU CUDA (RTX 3050)

📚 Référence principale (Article FaceForensics++)
Rössler et al., FaceForensics++: Learning to Detect Manipulated Facial Images, ICCV 2019.

📝 Licence
Projet académique — usage pédagogique uniquement.

yaml
 