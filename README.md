# Planning actualisé du stage — 2 mois

## Projet : CookMotion AI

**Sujet :** Assistant IA pour la reconnaissance de tâches culinaires à partir de vidéos  
**Cas d’usage principal :** reconnaissance de gestes culinaires dans des vidéos, avec un focus initial sur la tâche « couper un oignon »  
**Technologies principales :** Python, OpenCV, PyTorch, Hugging Face, EPIC-KITCHENS, VideoMAE, Google Colab, GitHub, Streamlit

---

# Objectif général du stage

Développer un prototype capable de :

- analyser des vidéos de tâches culinaires ;
- tester plusieurs modèles IA de reconnaissance d’actions ;
- générer des vidéos annotées avec les actions prédites et les scores associés ;
- comparer les performances des modèles testés ;
- identifier les limites actuelles des modèles pré-entraînés ;
- préparer une stratégie de fine-tuning sur un volume plus important de vidéos ;
- présenter une piste technique claire et évolutive à l’encadrant.

> Priorité actuelle : mettre en place un pipeline fonctionnel basé sur des modèles existants, produire des résultats visuels exploitables, puis améliorer progressivement les performances par fine-tuning.

---


Deux pistes principales sont donc retenues :

1. **Modèle EPIC-KITCHENS officiel**  
   Modèle de reconnaissance d’actions basé sur EPIC-KITCHENS, capable de prédire un couple verbe / objet.

2. **Modèle Hugging Face basé sur VideoMAE / HD-EPIC**  
   Modèle vidéo pré-entraîné ou fine-tuné sur des actions culinaires, testé sur des clips courts avec génération d’une vidéo annotée.

---

# Semaine 1 — Cadrage du projet et recherche des modèles existants

## Objectif de la semaine

Cadrer le sujet, définir le cas d’usage, identifier les datasets et rechercher les modèles IA existants adaptés aux gestes culinaires.

## 1. Cadrage du projet

- [x] Valider l’idée principale : reconnaissance de tâches culinaires à partir de vidéos
- [x] Définir le cas d’usage initial : tâches autour de la cuisine, notamment couper un oignon
- [x] Clarifier que l’objectif n’est pas de créer immédiatement un modèle from scratch
- [x] Définir une approche progressive : modèle pré-entraîné → test → annotation vidéo → comparaison → fine-tuning
- [x] Préparer un document de suivi du stage

## 2. Recherche de datasets et ressources

- [x] Identifier EPIC-KITCHENS comme dataset principal lié aux actions culinaires
- [x] Étudier les vidéos labelisées disponibles
- [x] Comprendre la structure des annotations : verbes, noms/objets, actions
- [x] Identifier les contraintes de stockage liées aux vidéos
- [x] Identifier la nécessité de filtrer les vidéos selon leur durée

## 3. Recherche de modèles existants

- [x] Rechercher des modèles déjà entraînés sur EPIC-KITCHENS
- [x] Identifier les modèles officiels EPIC-KITCHENS disponibles
- [x] Identifier une piste Hugging Face basée sur VideoMAE / HD-EPIC
- [x] Vérifier les limites d’accessibilité du pipeline complet Hugging Face
- [x] Choisir deux pistes à tester en priorité

## 4. Organisation du projet

- [x] Créer ou mettre à jour le dépôt GitHub
- [x] Préparer une structure de projet claire
- [x] Ajouter les notebooks de test
- [x] Ajouter les scripts utiles
- [x] Ajouter les premiers résultats d’inférence
- [x] Mettre à jour le README progressivement


---

# Semaine 2 — Préparation des vidéos et environnement d’expérimentation

## Objectif de la semaine

Préparer l’environnement de travail, organiser les vidéos et rendre les tests reproductibles sur Google Colab et localement.

## 1. Préparation des vidéos

- [x] Télécharger des vidéos labelisées courtes issues d’EPIC-KITCHENS
- [x] Filtrer les vidéos selon leur durée
- [x] Garder en priorité les vidéos de moins de 15 minutes
- [ ] Préparer aussi un sous-ensemble de vidéos de moins de 5 minutes
- [ ] Séparer les vidéos de test rapide et les vidéos destinées au fine-tuning
- [ ] Vérifier que les vidéos sont lisibles
- [ ] Convertir les vidéos problématiques si nécessaire



## 2. Préparation de Google Colab

- [x] Activer l’utilisation du GPU
- [x] Installer PyTorch, OpenCV et les dépendances nécessaires
- [x] Tester la lecture vidéo avec OpenCV
- [x] Tester l’extraction de frames
- [x] Préparer un notebook propre pour chaque modèle

## 3. Découpage des vidéos

- [x] Découper les vidéos longues en clips courts
- [x] Tester des fenêtres de 5 secondes
- [ ] Comparer avec des fenêtres de 2 ou 3 secondes
- [ ] Sauvegarder les clips générés
- [ ] Associer chaque clip à sa vidéo source


---

# Semaine 3 — Test du modèle EPIC-KITCHENS officiel

## Objectif de la semaine

Tester un premier modèle officiel lié à EPIC-KITCHENS et produire une vidéo annotée avec les prédictions.

## 1. Chargement du modèle

- [] Charger le modèle officiel EPIC-KITCHENS via PyTorch Hub
- [] Vérifier que le modèle fonctionne sur Colab
- [] Charger les classes de verbes
- [] Charger les classes de noms / objets
- [] Vérifier la sortie du modèle

## 2. Inférence sur une vidéo

- [] Extraire les frames nécessaires
- [] Préparer le tenseur d’entrée
- [] Lancer une prédiction sur une vidéo courte
- [] Afficher les meilleurs verbes prédits
- [] Afficher les meilleurs objets prédits
- [] Interpréter le couple verbe / objet

## 3. Inférence par segments

- [] Découper une vidéo en segments de quelques secondes
- [] Lancer la prédiction sur chaque segment
- [] Sauvegarder les résultats dans un CSV
- [] Afficher les scores de prédiction
- [] Identifier les segments mal reconnus

## 4. Vidéo annotée

- [] Générer une vidéo annotée avec :
  - action prédite ;
  - verbe ;
  - score du verbe ;
  - objet ;
  - score de l’objet.
- [] Visualiser la vidéo annotée dans Colab
- [] Télécharger la vidéo annotée
- [] Conserver cette vidéo comme première preuve de concept

## 5. Analyse des résultats

- [] Constater que les résultats ne sont pas encore totalement satisfaisants
- [] Identifier les raisons possibles :
  - modèle pas parfaitement adapté aux vidéos testées ;
  - clips parfois trop longs ou trop courts ;
  - différence entre dataset d’entraînement et vidéos utilisées ;
  - actions culinaires visuellement proches ;
  - manque de fine-tuning spécifique.


---

# Semaine 4 — Test du modèle Hugging Face VideoMAE / HD-EPIC

## Objectif de la semaine

Tester un second modèle pré-entraîné disponible sur Hugging Face et comparer ses résultats avec le modèle EPIC-KITCHENS.

## 1. Étude du modèle Hugging Face

- [] Identifier le modèle Hugging Face adapté aux actions culinaires
- [] Vérifier les fichiers disponibles
- [] Constater que le pipeline GitHub complet n’est pas accessible publiquement
- [] Adapter la stratégie pour tester directement le checkpoint exploitable
- [] Préparer un notebook Colab propre

## 2. Chargement du modèle

- [] Installer les dépendances Hugging Face
- [] Télécharger les poids du modèle
- [] Charger ou reconstruire la partie nécessaire pour l’inférence
- [] Vérifier la compatibilité avec Colab
- [] Tester l’inférence sur un clip court

## 3. Inférence sur vidéo

- [] Extraire 16 frames par clip
- [] Lancer le modèle sur un segment vidéo
- [] Récupérer les prédictions et scores
- [] Appliquer l’inférence sur plusieurs segments
- [] Sauvegarder les résultats dans un CSV

## 4. Vidéo annotée

- [] Générer une vidéo annotée avec les prédictions Hugging Face
- [] Afficher le label prédit
- [] Afficher les scores associés
- [] Télécharger la vidéo annotée
- [] Préparer cette vidéo comme deuxième preuve de concept

## 5. Comparaison initiale

- [] Comparer visuellement les deux vidéos annotées
- [] Comparer la stabilité des prédictions
- [] Comparer la pertinence des actions prédites
- [] Identifier les limites des deux modèles
- [] Préparer un message d’avancement à l’encadrant

---

# Semaine 5 — Analyse comparative et amélioration du pipeline

## Objectif de la semaine

Améliorer le pipeline d’inférence, analyser les résultats obtenus et préparer une base solide pour le fine-tuning.

## 1. Analyse comparative des deux modèles

- [ ] Comparer les prédictions segment par segment
- [ ] Comparer les scores moyens
- [ ] Identifier les actions souvent confondues
- [ ] Identifier les segments où les deux modèles échouent
- [ ] Identifier les segments où un modèle est meilleur que l’autre
- [ ] Construire un tableau comparatif

## 2. Amélioration du découpage vidéo

- [ ] Tester plusieurs tailles de fenêtre : 2 s, 3 s, 5 s, 8 s
- [ ] Tester différents strides
- [ ] Vérifier l’impact du découpage sur les prédictions
- [ ] Choisir une configuration stable pour la suite

## 3. Amélioration des vidéos annotées

- [ ] Ajouter les top-3 prédictions sur la vidéo
- [ ] Ajouter le temps courant du segment
- [ ] Ajouter une couleur ou un indicateur de confiance
- [ ] Ajouter une timeline simple
- [ ] Générer une sortie plus propre pour la démonstration

## 4. Structuration des résultats

- [ ] Sauvegarder tous les CSV de prédiction
- [ ] Organiser les vidéos annotées
- [ ] Ajouter une description des tests dans le README
- [ ] Créer un dossier `experiments`
- [ ] Documenter les commandes utilisées

## 5. Préparation du fine-tuning

- [ ] Identifier les classes prioritaires à améliorer
- [ ] Sélectionner un sous-ensemble de vidéos EPIC-KITCHENS
- [ ] Préparer un fichier de correspondance vidéo / label
- [ ] Vérifier le format attendu par le modèle
- [ ] Estimer le volume nécessaire de vidéos
- [ ] Identifier les limites de stockage et de temps d’entraînement


---

# Semaine 6 — Fine-tuning progressif sur un sous-ensemble de vidéos

## Objectif de la semaine

Commencer l’adaptation du modèle sur un sous-ensemble réaliste de vidéos culinaires afin d’améliorer les prédictions.

## 1. Préparation des données pour fine-tuning

- [ ] Sélectionner les vidéos les plus exploitables
- [ ] Préparer les clips d’entraînement
- [ ] Associer chaque clip à son label
- [ ] Vérifier l’équilibre entre les classes
- [ ] Écarter les clips ambigus ou inutilisables
- [ ] Créer les splits train / validation / test

## 2. Choix de la stratégie de fine-tuning

- [ ] Choisir le modèle à fine-tuner en priorité
- [ ] Geler une partie du backbone si nécessaire
- [ ] Adapter la tête de classification si nécessaire
- [ ] Définir les hyperparamètres de départ
- [ ] Définir une stratégie adaptée aux ressources Colab

## 3. Premier fine-tuning léger

- [ ] Lancer un premier entraînement sur un petit sous-ensemble
- [ ] Suivre la loss d’entraînement
- [ ] Suivre la loss de validation
- [ ] Sauvegarder le meilleur checkpoint
- [ ] Éviter le surapprentissage
- [ ] Noter les limites rencontrées

## 4. Évaluation

- [ ] Tester le modèle fine-tuné sur des vidéos non vues
- [ ] Comparer avec le modèle pré-entraîné non fine-tuné
- [ ] Calculer accuracy, precision, recall et F1-score si les labels sont disponibles
- [ ] Générer une matrice de confusion
- [ ] Générer une nouvelle vidéo annotée

## 5. Analyse des limites

- [ ] Documenter les contraintes de stockage
- [ ] Documenter les contraintes de temps d’entraînement
- [ ] Documenter les limites du volume de données utilisé
- [ ] Proposer une stratégie large scale pour la suite


---

# Semaine 7 — Interface de démonstration et documentation

## Objectif de la semaine

Créer une interface simple pour tester les vidéos et préparer une démonstration claire pour l’encadrant.

## 1. Interface Streamlit

- [ ] Créer une interface d’upload vidéo
- [ ] Permettre le choix du modèle à utiliser
- [ ] Ajouter un bouton d’analyse
- [ ] Afficher la vidéo originale
- [ ] Afficher la vidéo annotée
- [ ] Afficher le tableau des prédictions
- [ ] Permettre le téléchargement du CSV

## 2. Affichage des résultats

- [ ] Afficher les prédictions par segment
- [ ] Afficher les scores de confiance
- [ ] Afficher les top-3 prédictions
- [ ] Afficher une timeline simple
- [ ] Ajouter un résumé global de la vidéo
- [ ] Ajouter une indication sur la fiabilité des résultats

## 3. Comparaison intégrée

- [ ] Ajouter un mode comparaison entre les deux modèles
- [ ] Afficher les résultats EPIC-KITCHENS
- [ ] Afficher les résultats Hugging Face
- [ ] Montrer les différences principales
- [ ] Permettre de télécharger les deux vidéos annotées

## 4. Documentation technique

- [ ] Rédiger le README
- [ ] Expliquer l’installation
- [ ] Expliquer l’utilisation sur Colab
- [ ] Expliquer comment lancer l’inférence
- [ ] Expliquer comment générer une vidéo annotée
- [ ] Expliquer les limites actuelles
- [ ] Expliquer la stratégie de fine-tuning

## 5. Préparation de la démonstration

- [ ] Choisir 2 ou 3 vidéos représentatives
- [ ] Préparer une vidéo annotée par modèle
- [ ] Préparer un tableau comparatif
- [ ] Préparer une explication simple des résultats
- [ ] Préparer une partie sur les limites et perspectives


---

# Semaine 8 — Finalisation, rapport et soutenance

## Objectif de la semaine

Finaliser le prototype, organiser les livrables et préparer la présentation finale.

## 1. Finalisation technique

- [ ] Nettoyer les notebooks
- [ ] Organiser les scripts
- [ ] Supprimer les fichiers inutiles
- [ ] Vérifier les chemins
- [ ] Vérifier que les notebooks s’exécutent correctement
- [ ] Vérifier que l’interface fonctionne
- [ ] Vérifier que les vidéos annotées sont disponibles
- [ ] Préparer une version stable du projet

## 2. Rapport final

Inclure dans le rapport :

- [ ] Contexte du projet
- [ ] Objectif du stage
- [ ] Problématique
- [ ] Changement d’approche
- [ ] Justification du choix des modèles pré-entraînés
- [ ] Description d’EPIC-KITCHENS
- [ ] Description du modèle EPIC-KITCHENS officiel
- [ ] Description du modèle Hugging Face / VideoMAE
- [ ] Préparation des vidéos
- [ ] Découpage en segments
- [ ] Méthode d’inférence
- [ ] Génération des vidéos annotées
- [ ] Résultats obtenus
- [ ] Comparaison des modèles
- [ ] Limites observées
- [ ] Contraintes de stockage et d’entraînement
- [ ] Fine-tuning réalisé ou planifié
- [ ] Perspectives d’amélioration

## 3. Présentation finale

Préparer des slides avec :

- [ ] Titre du projet
- [ ] Objectif
- [ ] Ancienne approche vs nouvelle approche
- [ ] Pipeline global
- [ ] Dataset utilisé
- [ ] Modèle 1 : EPIC-KITCHENS
- [ ] Modèle 2 : Hugging Face / VideoMAE
- [ ] Démo vidéo annotée
- [ ] Comparaison des résultats
- [ ] Limites
- [ ] Fine-tuning et perspectives
- [ ] Conclusion

## 4. Démo finale

Préparer au minimum :

- [ ] Une vidéo annotée avec le modèle EPIC-KITCHENS
- [ ] Une vidéo annotée avec le modèle Hugging Face
- [ ] Un tableau CSV des prédictions
- [ ] Une interface ou un notebook de démonstration
- [ ] Une explication claire des résultats non satisfaisants
- [ ] Une proposition d’amélioration par fine-tuning large scale

## 5. Livraison finale

- [ ] Code source
- [ ] Notebooks Colab
- [ ] Scripts d’inférence
- [ ] Vidéos annotées
- [ ] CSV des prédictions
- [ ] README
- [ ] Rapport final
- [ ] Présentation finale
- [ ] Démo prête


---

# Tableau récapitulatif actualisé des 8 semaines

| Semaine | Objectif principal | Livrable principal |
|---|---|---|
| Semaine 1 | Cadrage et recherche de modèles existants | Approche validée + modèles identifiés |
| Semaine 2 | Préparation vidéos et environnement Colab | Vidéos prêtes + notebooks de base |
| Semaine 3 | Test du modèle EPIC-KITCHENS officiel | Vidéo annotée + CSV prédictions |
| Semaine 4 | Test du modèle Hugging Face / VideoMAE | Deuxième vidéo annotée + comparaison initiale |
| Semaine 5 | Analyse comparative et amélioration du pipeline | Tableau comparatif + pipeline amélioré |
| Semaine 6 | Fine-tuning progressif | Premier modèle adapté + analyse avant/après |
| Semaine 7 | Interface et documentation | Démo Streamlit + README |
| Semaine 8 | Finalisation et présentation | Rapport + slides + démo finale |

---

# Message clé à transmettre dans le rapport

Les premiers résultats obtenus avec les modèles pré-entraînés ne sont pas encore totalement satisfaisants. Cependant, cette étape a permis de valider une piste technique complète : chargement de modèles vidéo, découpage des vidéos en segments, inférence automatique, génération de vidéos annotées et comparaison des prédictions.

Les limites observées sont principalement liées à l’écart entre les vidéos utilisées et les données d’entraînement des modèles, au manque de fine-tuning spécifique, aux contraintes de stockage et au coût d’entraînement sur un grand volume de vidéos.

La suite logique du projet consiste donc à fine-tuner le modèle le plus prometteur sur un plus grand volume de clips culinaires, tout en améliorant le découpage temporel, la qualité des annotations et la stabilité des prédictions.
