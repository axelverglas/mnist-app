# 🧠 MNIST App – Reconnaissance de chiffres manuscrits (TP CNN & MLOps)

## 📝 Groupe :

- Sofiane Zouaoui
- Arthur Sornin
- Axel Verglas

Ce projet est une application complète de reconnaissance de chiffres manuscrits basée sur le dataset MNIST, réalisée dans le cadre d’un TP d’introduction au Deep Learning, à la MLOps et à l’orchestration de services.  
L’application combine un backend FastAPI (inférence du modèle PyTorch) et un frontend Streamlit (interface utilisateur), le tout orchestré avec Docker Compose.

---

## 📝 Objectifs pédagogiques du TP

- **Découvrir le dataset MNIST** et la visualisation de données.
- **Construire et entraîner un modèle CNN** pour la classification d’images.
- **Structurer un projet MLOps** (séparation du code, gestion des modèles, reproductibilité).
- **Déployer une API d’inférence** (FastAPI).
- **Créer une interface utilisateur** (Streamlit).
- **Orchestrer l’ensemble avec Docker Compose**.

---

## 📁 Structure du projet

```
mnist-app/
│
├── backend/         # Backend FastAPI + code d'entraînement PyTorch
│   ├── notebook/    # Notebooks exploratoires (visualisation, tests)
│   ├── src/         # Code source (modèles, entraînement, API)
│   └── model/       # Modèles sauvegardés (.pt)
│
├── frontend/        # Interface utilisateur Streamlit
│
├── docker-compose.yml  # Orchestration des services
└── readme.md           # Ce fichier
```

---

## 1️⃣ Découverte et visualisation du dataset MNIST

- Utilisation de `torchvision.datasets.MNIST` pour télécharger et charger les images.
- Visualisation des 10 chiffres (0 à 9) dans le notebook `backend/notebook/load_mnist.py`.
- Normalisation des images pour l’entraînement.

---

## 2️⃣ Construction et entraînement du modèle CNN

- Architecture CNN définie dans `backend/src/model/convnet.py` :
  - 2 couches convolutionnelles + ReLU + MaxPool
  - 1 couche fully-connected cachée
  - 1 couche de sortie (10 classes)
- Entraînement du modèle avec AdamW (`backend/src/model/train.py`).
- Application d’une permutation Toeplitz (optionnelle) pour le désordre spatial.
- Sauvegarde du modèle entraîné dans `backend/model/mnist-0.0.1.pt`.

---

## 3️⃣ Structuration MLOps

- Séparation claire entre :
  - **Code d’entraînement** (`src/model/`, `src/train_cnn.py`)
  - **API d’inférence** (`src/app/`)
  - **Notebooks exploratoires** (`notebook/`)
  - **Modèles sauvegardés** (`model/`)
- Utilisation de requirements.txt pour la reproductibilité.
- README d’installation et d’utilisation.

---

## 4️⃣ Déploiement d’une API d’inférence (FastAPI)

- API FastAPI dans `backend/src/app/main.py` :
  - Endpoint `/api/v1/predict` pour recevoir une image et retourner la prédiction du chiffre.
  - Chargement du modèle PyTorch au démarrage.
  - Gestion du device (CPU, CUDA, MPS).
  - CORS activé pour permettre l’accès depuis le frontend.

---

## 5️⃣ Création d’une interface utilisateur (Streamlit)

- Application Streamlit dans `frontend/app.py` :
  - Canvas interactif pour dessiner un chiffre à la souris.
  - Envoi de l’image à l’API FastAPI pour obtenir la prédiction.
  - Affichage du chiffre prédit et du score de confiance.

---

## 6️⃣ Orchestration et déploiement (Docker Compose)

- Fichier `docker-compose.yml` pour lancer simultanément le backend et le frontend.
- Les deux services communiquent via le réseau Docker.
- Commandes de build et de lancement unifiées.

---

## 🚀 Guide d’installation et d’utilisation

### 1. Cloner le projet avec les sous-modules

```bash
git clone --recurse-submodules <url-du-repo>
cd mnist-app
```

### 2. Lancer l’application avec Docker Compose

```bash
docker-compose up --build
```

- Le backend FastAPI sera accessible sur [http://localhost:8000](http://localhost:8000)
- Le frontend Streamlit sera accessible sur [http://localhost:8501](http://localhost:8501)

### 3. Utilisation

- Rendez-vous sur l’interface Streamlit, dessinez un chiffre, cliquez sur "Envoyer à l'API pour prédiction" et obtenez la prédiction en temps réel.

---

## 🛠️ Détails techniques

- **Backend** : PyTorch, FastAPI, gestion du modèle, API REST.
- **Frontend** : Streamlit, canvas interactif, requêtes HTTP.
- **MLOps** : Séparation des environnements, reproductibilité, gestion des dépendances.
- **Docker** : Conteneurisation, orchestration multi-service.

---

## 📚 Pour aller plus loin

- Possibilité d’entraîner d’autres architectures (MLP, etc.).
- Ajout de tests unitaires, CI/CD (voir `.github/workflows/`).
- Déploiement sur le cloud, monitoring, etc.

---

## 👨‍🏫 Conclusion

Ce projet met en pratique l’ensemble du cycle de vie d’un modèle de deep learning, de la data à l’inférence, en passant par le déploiement et l’industrialisation.  
Il répond point par point aux objectifs du TP : compréhension du dataset, modélisation, structuration, API, interface utilisateur et orchestration.
