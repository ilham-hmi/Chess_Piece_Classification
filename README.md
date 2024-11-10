# Détection et Classification des Pièces d'Échecs avec Mask R-CNN

## Autrices
- HACHMI Ilham - M1 MASERATI
- TRAORE Assa - M1 MASERATI
- EL HACHMI Sehame - M1 MASERATI


## Objectif du Projet
L'objectif de ce projet est de créer un modèle capable de détecter les pièces d'échecs et de les classer selon leurs types (roi, reine, tour, cavalier, fou, pion).

## Technologies Utilisées
- **Python** (version 3.8.6)
- **TensorFlow** (version 1.15)
- **Keras** (version 2.3.1) avec `tensorflow.compat.v1`
- **Mask R-CNN**
- **Skimage** 
- **Scikit-learn**

## Hyper Paramètres
Les principaux hyperparamètres utilisés dans l'entraînement sont les suivants :

- **BACKBONE** : `resnet101`
- **IMAGES_PER_GPU** : `1`
- **NUM_CLASSES** : `7` 
- **STEPS_PER_EPOCH** : `250`
- **VALIDATION_STEPS** : `50`
- **LEARNING_RATE** : `0.001`
- **DETECTION_MIN_CONFIDENCE** : `0.9`
- **USE_MINI_MASK** : `False`
- **IMAGE_MIN_DIM** : `800`
- **IMAGE_MAX_DIM** : `1024`
- **RPN_ANCHOR_SCALES** : `(32, 64, 128, 256, 512)`
- **RPN_ANCHOR_RATIOS** : `[0.5, 1, 2]`
- **TRAIN_ROIS_PER_IMAGE** : `200`
- **BATCH_SIZE** : `1`


## Données
Le projet utilise un ensemble de données de pièces d'échecs comprenant :
- **Nombre total d'images** : `581`
- **Images d'entrainement** : `461`
- **Images de validation** : `120`

### Structure des Données
Les images et les annotations sont organisées de la manière suivante :
- `train/`: Contient les images et annotations au format JSON pour l'entraînement.
- `val/`: Contient les images et annotations au format JSON pour la validation.

## Rapport
Vous trouverez le rapport ainsi que le code d'entrainement et de validation ainsi que le dossier logs attachés au projet au format .ipynb. Vous trouverez également la matrice de confusion et le graphique des pertes au format .jpg.


## Difficultés Rencontrées
| Problème | Description | Solution |
|----------|-------------|----------|
| **Version de Python** | Ajustement de la version de Python pour assurer la compatibilité avec le MRCNN utilisé. | Utilisation de la version 3.8.6. |
| **Incompatibilités Keras/TensorFlow** | Problèmes récurrents d'import entre les versions Keras et TensorFlow. | Utilisation de `tensorflow.compat.v1` et installation des versions Keras 2.3.1 et Tensorflow 1.15 |
| **Incompatibilité TensorFlow/Mask RCNN** | La version de Mask R-CNN n’était pas compatible avec la version de TensorFlow utilisée. | Utilisation de TensorFlow 1.15 |
| **Création des fichiers d'annotation JSON** | Noms de fichiers d'images se répétant entre les différentes classes, entraînant des conflits dans les annotations. | Modification des chemins et noms de fichiers pour les rendre uniques dans le fichier JSON généré. |
| **Crash du noyau Jupyter** | Le noyau Jupyter a perdu la connexion pendant l'entraînement. | Reprise de l'entraînement en chargeant les poids sauvegardés de la dernière sauvegarde enregistrée dans le dossier logs/. |
| **Incompatibilité Google Colab avec la version requise de TensorFlow** | Google Colab ne supportait pas la version spécifique de TensorFlow utilisée dans le projet. | Réalisation du projet en local sur Jupyter Notebook. |
| **Problèmes de version de TensorFlow** | Erreurs récurrentes liées aux métriques. | Suppression des occurrences de metrics_tensor et utilisation explicite de tf.compat.v1 dans model.py. |
| **Avertissement Skimage** | Avertissement lors de l'utilisation de skimage.draw.polygon au moment du lancement de l'entrainement. | Ajout du paramètre order=0 dans utils.py pour supprimer l’avertissement lors de la création des masques. |
| **Erreur ValueError: zero-size array** | Les annotations JSON contenaient des segmentations vides ou mal formatées, causant une erreur lors de la création des masques. | Modification de la fonction load_mask pour ajouter une vérification des segmentations avant traitement. |
| **Coordonnées dépassant la résolution de l'image** | Annotations avec coordonnées de segmentation dépassant la taille de l'image, causant des erreurs de masques. | Restriction des coordonnées dans les limites de la résolution de l'image pour les segmentation problématiques. |

## Contribuer
Les contributions sont les bienvenues !



