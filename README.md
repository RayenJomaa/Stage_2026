# Stage_2026

Planning complet du stage — 2 mois
Projet : CookMotion AI
Sujet : Assistant IA pour la reconnaissance de gestes culinaires à partir de vidéos  
Tâche MVP : Couper un oignon en dés  
Durée : 8 semaines  
Technologies principales : Python, OpenCV, MediaPipe, Machine Learning, Streamlit
---
Objectif général du stage
Développer un prototype capable de :
analyser une vidéo d’une tâche culinaire ;
suivre les mouvements des mains avec MediaPipe ;
reconnaître les différentes étapes de la tâche ;
détecter les erreurs ou étapes manquantes ;
afficher les résultats dans une interface graphique.
> Priorité : finaliser correctement une seule tâche, **couper un oignon en dés**, avant de passer à d’autres tâches.
---
Semaine 1 — Cadrage du projet et collecte des vidéos
Objectif de la semaine
Cadrer précisément le sujet, valider la tâche MVP, collecter les premières vidéos et organiser le projet.
1. Cadrage du projet
[ ] Définir la méthode de travail hebdomadaire
[ ] Préparer un document de suivi du stage
1. Recherche de vidéos
[x] Chercher des vidéos avec le mot-clé `how to dice an onion`
[x] Chercher des vidéos avec le mot-clé `knife skills dice onion`
[x] Chercher des vidéos avec le mot-clé `how to chop an onion`
[x] Chercher des vidéos avec le mot-clé `how to cut onion step by step`
[x] Chercher des vidéos en français avec `comment couper un oignon en dés`
[x] Sauvegarder les liens des vidéos retenues
1. Collecte du dataset
[ ] Collecter au minimum 20 vidéos exploitables
[ ] Viser idéalement 30 à 40 vidéos
[ ] Classer les vidéos selon leur qualité
[ ] Identifier les vidéos de type expert
[ ] Identifier les vidéos de type débutant ou amateur
[ ] Garder quelques vidéos à part pour les tests finaux
[ ] Filmer quelques vidéos internes si les vidéos publiques ne suffisent pas
1. Organisation du projet
[ ] Créer le dossier principal `CookingGestureAI`
[ ] Créer le dossier `data/raw_videos`
[ ] Créer le dossier `data/processed_videos`
[ ] Créer le dossier `data/annotations`
[ ] Créer le dossier `data/landmarks`
[ ] Créer le dossier `data/splits`
[ ] Créer le dossier `models`
[ ] Créer le dossier `outputs`
[ ] Créer le dossier `src`
[ ] Créer le dossier `app`
[ ] Créer le dossier `notebooks`
[ ] Créer le fichier `README.md`
[ ] Créer le fichier `requirements.txt`
1. Fichier de suivi dataset
Créer un fichier `dataset.csv` avec les colonnes suivantes :
[ ] `video_id`
[ ] `filename`
[ ] `path`
[ ] `source`
[ ] `url`
[ ] `duration`
[ ] `fps`
[ ] `resolution`
[ ] `view_angle`
[ ] `quality`
[ ] `status`
[ ] `comment`
Livrables de la semaine 1
[ ] Sujet bien cadré
[ ] Tâche MVP validée
[ ] Premier dataset collecté
[ ] Structure du projet créée
[ ] Fichier `dataset.csv` créé
[ ] Liste des vidéos sources préparée
---
Semaine 2 — Nettoyage vidéo et définition des labels
Objectif de la semaine
Nettoyer les vidéos, standardiser les fichiers et définir précisément les étapes à reconnaître.
1. Prétraitement des vidéos
[ ] Supprimer les introductions inutiles
[ ] Supprimer les parties où il n’y a pas d’action
[ ] Garder uniquement la partie utile de la tâche
[ ] Couper les vidéos trop longues
[ ] Standardiser le format en `.mp4`
[ ] Standardiser la résolution
[ ] Standardiser le FPS
[ ] Vérifier que chaque vidéo est lisible
[ ] Sauvegarder les vidéos nettoyées dans `data/processed_videos`
1. Paramètres recommandés
[ ] Résolution choisie : `640x480` ou `720p`
[ ] FPS choisi : `15` ou `30`
[ ] Format choisi : `.mp4`
[ ] Nommer chaque vidéo proprement
Exemple :
```text
onion_001_expert_topview.mp4
onion_002_expert_frontview.mp4
onion_003_beginner_internal.mp4
```
1. Définition des labels
Version MVP recommandée :
[ ] `idle`
[ ] `preparation`
[ ] `peeling`
[ ] `cut_in_half`
[ ] `hand_positioning`
[ ] `cutting`
[ ] `finish`
Version détaillée possible plus tard :
[ ] `prepare_workspace`
[ ] `cut_ends`
[ ] `peel_onion`
[ ] `cut_in_half`
[ ] `position_hand`
[ ] `vertical_cuts`
[ ] `horizontal_cuts`
[ ] `dice_onion`
[ ] `finish`
1. Validation des labels
[ ] Vérifier que chaque label correspond à une étape claire
[ ] Éviter les labels trop proches entre eux
[ ] Éviter trop de labels au début
[ ] Valider les labels avec l’encadrant
[ ] Créer un fichier `label_map.json`
Exemple :
```json
{
  "idle": 0,
  "preparation": 1,
  "peeling": 2,
  "cut_in_half": 3,
  "hand_positioning": 4,
  "cutting": 5,
  "finish": 6
}
```
1. Préparation du labelling temporel
[ ] Choisir la méthode de labellisation
[ ] Décider si le labelling sera fait avec CSV manuel
[ ] Préparer le fichier `video_segments.csv`
[ ] Tester le labelling sur 2 ou 3 vidéos
[ ] Corriger les labels si nécessaire
Livrables de la semaine 2
[ ] Vidéos nettoyées
[ ] Résolution et FPS standardisés
[ ] Liste finale des labels
[ ] Fichier `label_map.json`
[ ] Début du fichier `video_segments.csv`
[ ] Première validation des labels
---
Semaine 3 — Labellisation temporelle et extraction MediaPipe
Objectif de la semaine
Labelliser les vidéos et extraire les landmarks des mains avec MediaPipe.
1. Labellisation temporelle
[ ] Regarder chaque vidéo nettoyée
[ ] Identifier le début de chaque action
[ ] Identifier la fin de chaque action
[ ] Associer chaque segment à un label
[ ] Remplir le fichier `video_segments.csv`
[ ] Vérifier qu’il n’y a pas de chevauchement incohérent
[ ] Vérifier qu’aucune partie utile n’est oubliée
[ ] Ajouter le label `idle` pour les moments inutiles si nécessaire
Format recommandé :
```csv
video_id,start_time,end_time,label
onion_001,0.00,4.20,preparation
onion_001,4.20,10.50,peeling
onion_001,10.50,18.00,cut_in_half
onion_001,18.00,35.00,cutting
onion_001,35.00,40.00,finish
```
1. Objectif de labellisation
[ ] Labelliser au minimum 10 vidéos
[ ] Viser 20 vidéos labellisées si possible
[ ] Garder quelques vidéos non labellisées pour les tests finaux
[ ] Revoir les vidéos difficiles
[ ] Supprimer les vidéos impossibles à labelliser proprement
1. Installation de l’environnement
[ ] Créer un environnement virtuel Python
[ ] Installer OpenCV
[ ] Installer MediaPipe
[ ] Installer NumPy
[ ] Installer Pandas
[ ] Installer Scikit-learn
[ ] Installer Matplotlib
[ ] Installer Streamlit
[ ] Mettre à jour `requirements.txt`
[ ] Tester l’environnement avec une vidéo simple
1. Extraction MediaPipe
[ ] Lire chaque vidéo frame par frame
[ ] Appliquer MediaPipe Hands
[ ] Extraire les 21 points de chaque main
[ ] Sauvegarder les coordonnées `x`, `y`, `z`
[ ] Identifier main gauche et main droite
[ ] Associer chaque frame au label correspondant
[ ] Sauvegarder les résultats en CSV
[ ] Sauvegarder aussi en NumPy si nécessaire
1. Vérification visuelle
[ ] Afficher quelques frames avec landmarks
[ ] Vérifier que les mains sont bien détectées
[ ] Vérifier si les mains disparaissent souvent
[ ] Calculer le pourcentage de frames avec détection
[ ] Identifier les vidéos problématiques
[ ] Supprimer ou corriger les vidéos de mauvaise qualité
Livrables de la semaine 3
[ ] Fichier `video_segments.csv` rempli
[ ] Script d’extraction MediaPipe
[ ] Fichiers landmarks générés
[ ] Premières visualisations MediaPipe
[ ] Rapport simple sur la qualité de détection
---
Semaine 4 — Nettoyage des données et premier modèle
Objectif de la semaine
Préparer les données pour l’apprentissage et entraîner un premier modèle simple.
1. Nettoyage des landmarks
[ ] Charger les fichiers de landmarks
[ ] Vérifier les valeurs manquantes
[ ] Remplir les frames sans détection
[ ] Supprimer les séquences trop bruitées
[ ] Normaliser les coordonnées
[ ] Lisser les mouvements
[ ] Vérifier la cohérence main gauche / main droite
[ ] Sauvegarder les données nettoyées
1. Normalisation
[ ] Tester une normalisation par rapport au poignet
[ ] Tester une normalisation par taille de la main
[ ] Vérifier que la position dans l’image influence moins le modèle
[ ] Comparer les résultats avant/après normalisation
1. Création des séquences
[ ] Définir `window_size = 30 frames`
[ ] Définir `stride = 10 frames`
[ ] Créer des séquences de landmarks
[ ] Associer chaque séquence à un label
[ ] Sauvegarder `X` et `y`
[ ] Vérifier la forme des données
Exemple attendu :
```text
X.shape = (nombre_sequences, 30, 126)
y.shape = (nombre_sequences,)
```
1. Split train / validation / test
[ ] Séparer les données par vidéo
[ ] Ne pas mélanger les frames d’une même vidéo entre train et test
[ ] Créer `train.csv`
[ ] Créer `val.csv`
[ ] Créer `test.csv`
[ ] Appliquer une répartition 70 / 15 / 15
[ ] Vérifier que chaque label existe dans le train
1. Premier modèle simple
[ ] Extraire des features statistiques simples
[ ] Tester Random Forest
[ ] Tester éventuellement SVM
[ ] Tester éventuellement XGBoost
[ ] Évaluer le modèle
[ ] Calculer l’accuracy
[ ] Calculer precision, recall, F1-score
[ ] Générer une matrice de confusion
[ ] Identifier les labels mal reconnus
[ ] Noter les premiers résultats
Livrables de la semaine 4
[ ] Données nettoyées
[ ] Séquences créées
[ ] Split train / validation / test
[ ] Premier modèle entraîné
[ ] Premiers résultats d’évaluation
[ ] Matrice de confusion
---
Semaine 5 — Modèle séquentiel et amélioration des prédictions
Objectif de la semaine
Passer d’un modèle simple à un modèle capable de mieux gérer les séquences temporelles.
1. Préparation pour LSTM / GRU
[ ] Charger les séquences au bon format
[ ] Vérifier la dimension des données
[ ] Encoder les labels
[ ] Préparer DataLoader si PyTorch est utilisé
[ ] Séparer train, validation et test proprement
1. Modèle LSTM ou GRU
[ ] Implémenter un modèle LSTM
[ ] Tester un modèle GRU si nécessaire
[ ] Définir la fonction de perte
[ ] Définir l’optimiseur
[ ] Entraîner le modèle
[ ] Suivre la loss train
[ ] Suivre la loss validation
[ ] Suivre l’accuracy validation
[ ] Sauvegarder le meilleur modèle
1. Comparaison des modèles
[ ] Comparer Random Forest avec LSTM
[ ] Comparer Random Forest avec GRU
[ ] Comparer accuracy
[ ] Comparer F1-score
[ ] Comparer matrice de confusion
[ ] Choisir le meilleur modèle pour la démo
1. Post-processing
[ ] Ajouter un vote majoritaire sur les prédictions
[ ] Ajouter une durée minimale pour valider une étape
[ ] Ajouter des règles d’ordre logique
[ ] Supprimer les changements de labels trop rapides
[ ] Regrouper les prédictions en segments temporels
[ ] Générer une timeline propre
Ordre logique recommandé :
```text
preparation -> peeling -> cut_in_half -> hand_positioning -> cutting -> finish
```
1. Détection d’erreurs
[ ] Détecter les étapes manquantes
[ ] Détecter les étapes dans le mauvais ordre
[ ] Détecter les actions non reconnues
[ ] Détecter une durée anormalement longue
[ ] Détecter une absence de main trop fréquente
[ ] Générer un feedback clair
Messages possibles :
```text
Étape manquante : épluchage non détecté
Ordre incorrect : découpe détectée avant coupe en deux
Action non reconnue pendant plusieurs secondes
Qualité vidéo insuffisante : mains peu visibles
```
Livrables de la semaine 5
[ ] Modèle LSTM ou GRU entraîné
[ ] Comparaison avec modèle simple
[ ] Meilleur modèle sauvegardé
[ ] Post-processing fonctionnel
[ ] Premiers messages d’erreur générés
[ ] Timeline propre générée automatiquement
---
Semaine 6 — Interface graphique et visualisation
Objectif de la semaine
Créer une interface simple pour tester le système facilement et montrer les résultats à l’encadrant.
1. Création de l’interface Streamlit
[ ] Créer le fichier principal `app.py`
[ ] Créer une page d’accueil
[ ] Ajouter une description du projet
[ ] Ajouter un bouton upload vidéo
[ ] Ajouter un bouton analyser
[ ] Afficher la vidéo originale
[ ] Lancer l’extraction MediaPipe depuis l’interface
[ ] Lancer l’inférence depuis l’interface
1. Affichage des résultats
[ ] Afficher le nom de la vidéo
[ ] Afficher la durée de la vidéo
[ ] Afficher les étapes détectées
[ ] Afficher la durée de chaque étape
[ ] Afficher les étapes manquantes
[ ] Afficher l’ordre des étapes
[ ] Afficher les erreurs détectées
[ ] Afficher le score global
[ ] Afficher le feedback final
1. Timeline visuelle
[ ] Générer une timeline des étapes
[ ] Afficher les segments temporels
[ ] Afficher les labels prédits
[ ] Afficher les durées
[ ] Rendre la timeline lisible et simple
Exemple :
```text
0s ─── 5s ─── 12s ─── 20s ─── 35s ─── 45s
Préparation | Épluchage | Coupe en deux | Découpe | Fin
```
1. Vidéo annotée
[ ] Dessiner les landmarks sur chaque frame
[ ] Afficher le label courant sur la vidéo
[ ] Afficher le temps courant
[ ] Générer une vidéo annotée
[ ] Sauvegarder la vidéo annotée dans `outputs/demo_videos`
[ ] Permettre le téléchargement de la vidéo annotée
1. Dashboard simple
[ ] Afficher le score de complétion
[ ] Afficher le score d’ordre
[ ] Afficher le score de stabilité
[ ] Afficher le score global
[ ] Afficher le nombre d’étapes réussies
[ ] Afficher le nombre d’erreurs
[ ] Ajouter un résumé final clair
Livrables de la semaine 6
[ ] Interface Streamlit fonctionnelle
[ ] Upload vidéo fonctionnel
[ ] Analyse vidéo fonctionnelle
[ ] Timeline affichée
[ ] Feedback affiché
[ ] Vidéo annotée générée
[ ] Première démo utilisable
---
Semaine 7 — Tests, correction et stabilisation
Objectif de la semaine
Tester le système dans plusieurs conditions et corriger les problèmes avant la livraison finale.
1. Tests fonctionnels
[ ] Tester avec une vidéo experte
[ ] Tester avec une vidéo interne correcte
[ ] Tester avec une vidéo contenant une erreur
[ ] Tester avec une vidéo où l’épluchage est absent
[ ] Tester avec une vidéo où l’ordre est incorrect
[ ] Tester avec une vidéo de mauvaise qualité
[ ] Tester plusieurs angles de caméra
[ ] Tester plusieurs personnes
[ ] Tester une vidéo jamais vue par le modèle
1. Analyse des erreurs
[ ] Identifier les labels souvent confondus
[ ] Identifier les vidéos qui posent problème
[ ] Identifier les cas où MediaPipe échoue
[ ] Identifier les erreurs du post-processing
[ ] Identifier les problèmes de l’interface
[ ] Noter toutes les limites du système
1. Amélioration du modèle
[ ] Ajouter quelques vidéos si nécessaire
[ ] Corriger les labels douteux
[ ] Réentraîner le modèle
[ ] Ajuster les hyperparamètres
[ ] Ajuster la taille de fenêtre
[ ] Ajuster le stride
[ ] Comparer les nouvelles performances
1. Amélioration de l’interface
[ ] Corriger les bugs
[ ] Améliorer l’affichage des résultats
[ ] Améliorer la timeline
[ ] Améliorer les messages de feedback
[ ] Ajouter un résumé automatique
[ ] Ajouter un bouton pour exporter les résultats
[ ] Ajouter une meilleure gestion des erreurs
1. Documentation technique
[ ] Rédiger le README
[ ] Expliquer comment installer le projet
[ ] Expliquer comment préparer les vidéos
[ ] Expliquer comment faire le labelling
[ ] Expliquer comment extraire les landmarks
[ ] Expliquer comment entraîner le modèle
[ ] Expliquer comment lancer l’interface
[ ] Décrire la structure du projet
[ ] Décrire les limites du système
Livrables de la semaine 7
[ ] Système testé sur plusieurs vidéos
[ ] Bugs principaux corrigés
[ ] Interface stabilisée
[ ] Modèle amélioré si nécessaire
[ ] README rédigé
[ ] Limites du système identifiées
---
Semaine 8 — Finalisation, rapport et démonstration
Objectif de la semaine
Finaliser tous les livrables, préparer la démonstration et rédiger le rapport final.
1. Finalisation technique
[ ] Nettoyer le code
[ ] Organiser les scripts
[ ] Supprimer les fichiers inutiles
[ ] Vérifier que le projet se lance correctement
[ ] Vérifier que l’interface fonctionne
[ ] Vérifier que le modèle est bien chargé
[ ] Vérifier que les chemins sont corrects
[ ] Vérifier que les vidéos de démo fonctionnent
[ ] Préparer une version finale stable
1. Rapport final
Inclure dans le rapport :
[ ] Contexte du projet
[ ] Objectif du stage
[ ] Choix de l’idée
[ ] Justification du choix de la cuisine
[ ] Justification du choix de la tâche “couper un oignon”
[ ] Description du dataset
[ ] Méthode de collecte des vidéos
[ ] Méthode de prétraitement
[ ] Méthode de labellisation
[ ] Extraction MediaPipe
[ ] Préparation des séquences
[ ] Modèles testés
[ ] Résultats obtenus
[ ] Post-processing
[ ] Détection d’erreurs
[ ] Interface graphique
[ ] Difficultés rencontrées
[ ] Limites du projet
[ ] Perspectives
1. Présentation finale
Préparer des slides avec :
[ ] Titre du projet
[ ] Problématique
[ ] Objectif
[ ] Choix du cas d’usage
[ ] Pipeline global
[ ] Dataset
[ ] Labellisation
[ ] MediaPipe
[ ] Modèle utilisé
[ ] Interface graphique
[ ] Résultats
[ ] Démo
[ ] Limites
[ ] Perspectives
[ ] Conclusion
1. Démo finale
Préparer au moins 3 scénarios :
[ ] Vidéo experte reconnue correctement
[ ] Vidéo utilisateur correcte
[ ] Vidéo utilisateur avec étape manquante
[ ] Vidéo annotée avec landmarks
[ ] Timeline des étapes détectées
[ ] Feedback final
[ ] Score global
1. Livraison finale
[ ] Dataset organisé
[ ] Vidéos brutes
[ ] Vidéos nettoyées
[ ] Annotations temporelles
[ ] Fichiers landmarks
[ ] Scripts de preprocessing
[ ] Scripts MediaPipe
[ ] Scripts d’entraînement
[ ] Modèle entraîné
[ ] Script d’inférence
[ ] Interface Streamlit
[ ] Vidéos annotées
[ ] Rapport final
[ ] Présentation finale
[ ] README
[ ] Démo prête à lancer
Livrables de la semaine 8
[ ] Code final propre
[ ] Interface finale fonctionnelle
[ ] Rapport final terminé
[ ] Présentation finale terminée
[ ] Démo prête
[ ] Tous les livrables organisés
---

