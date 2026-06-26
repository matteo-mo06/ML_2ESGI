# Travaux pratiques a rendre (versions a completer)

Ce dossier contient les **notebooks a trous** : a vous de remplacer les `...` et
les `# TODO`. Les **corriges** sont dans [`../notebooks/`](../notebooks) (a ne
consulter qu'apres avoir cherche). Tous les TP utilisent de **vrais jeux de
donnees** fournis par scikit-learn.

## Installation

Depuis le dossier `tp/` :

```bash
make install      # avec uv (cree la venv .tp_ml_2esgi)
# ou, stack plus ancienne :
make venv-pip     # python -m venv .tp_ml_2esgi + pip install -r requirements.txt
```

Puis ouvrez les notebooks : `make lab` (ou `jupyter lab` dans `todo/`).

---

## TP1 — Clustering K-means + ACP (`TP1_kmeans_acp_TODO.ipynb`)

**Jeu de donnees : *Iris*** (150 fleurs, 4 mesures, 3 especes reelles).
**Type : apprentissage non supervise.**
> Le corrige applique la **meme demarche sur le dataset *Wine*** : meme structure,
> donnees differentes. A vous de l'adapter a Iris.

**But.** Retrouver les 3 especes **sans utiliser l'etiquette**, puis valider et
qualifier les groupes.

**Ce que vous devez faire :**
1. **Explorer** : statistiques descriptives, constater les differences d'echelle.
2. **Standardiser** les variables (`StandardScaler`) — justifiez pourquoi.
3. **Choisir k** : tracer la **methode du coude** (inertie) et le **score de
   silhouette** sur k = 2..8. Ici la silhouette suggere **k = 2** ; comme on sait
   qu'il y a 3 especes, on poursuit avec **k = 3** (la silhouette ne donne pas
   toujours le vrai nombre de classes).
4. **Evaluer & valider** : inertie, silhouette, puis comparer les clusters aux
   vraies especes (`adjusted_rand_score` + `pd.crosstab`).
5. **Visualiser** : projeter en 2D par **ACP** (`PCA`), colorer par cluster.
6. **Integrer & qualifier** : ajouter la colonne `cluster`, calculer le profil
   moyen par cluster, puis le caracteriser avec des **boxplots** (distribution) et
   une **heatmap** des moyennes standardisees (signature) ; interpreter.
7. **Aller plus loin (CAH)** : tracer un **dendrogramme** (clustering hierarchique
   ascendant, methode de Ward), decouper en 3 clusters avec
   `AgglomerativeClustering`, et comparer a K-means et aux especes (`adjusted_rand_score`).

**Attendu.** Le k retenu (justifie), l'ARI obtenu, les variables les plus
discriminantes (boxplots), une qualification par cluster appuyee sur la heatmap,
la comparaison K-means vs CAH.
**Bonus.** Refaire sans standardisation : impact sur l'ARI ?

---

## TP2 — Classification par arbre de decision (`TP2_arbre_decision_TODO.ipynb`)

**Jeu de donnees : *Breast Cancer Wisconsin*** (569 tumeurs, 30 mesures, malin/benin).
**Type : apprentissage supervise (classification binaire).**

**But.** Predire le diagnostic avec un modele **explicable**, en soignant le
**rappel sur les cas malins**.

**Ce que vous devez faire :**
1. **Explorer** : repartition des classes (malin vs benin).
2. **Modeliser** : split train/test (`stratify`), entrainer un
   `DecisionTreeClassifier` (`max_depth=3`).
3. **Evaluer** : accuracy train/test, `classification_report`, **matrice de
   confusion**. Commenter le **rappel** de la classe `malignant`.
4. **Visualiser** : tracer l'**arbre** et l'**importance des variables**.
5. **Decider** : predire 5 cas du test avec leur probabilite ; discuter le seuil.

**Attendu.** Accuracy test + lecture de la matrice de confusion, justification du
rappel prioritaire, variables les plus determinantes.
**Bonus.** Faire varier `max_depth` (2, 3, 6, None) : ou commence le surapprentissage ?

---

## TP3 — Regression lineaire (`TP3_regression_lineaire_TODO.ipynb`)

**Jeu de donnees : *California Housing*** (20 640 districts, 8 variables, prix median).
**Type : apprentissage supervise (regression).**

**But.** Predire la valeur mediane des logements et **interpreter** les facteurs.

**Ce que vous devez faire :**
1. **Explorer** : correlation de chaque variable avec le prix.
2. **Modeliser** : split train/test, `LinearRegression`, lire intercept + coefficients.
3. **Evaluer** : **R2**, **RMSE**, **MAE**.
4. **Visualiser** : (a) prix vs `MedInc` + droite, (b) **predit vs reel**,
   (c) **residus**.
5. **Interpreter** : effet (en k USD) du revenu median et de l'age du bati ;
   estimer le prix de 3 districts.

**Attendu.** R2/RMSE/MAE commentes, lecture des residus (effet de plafond),
effet du revenu median sur le prix.
**Bonus.** Comparer le R2 avec une seule variable (`MedInc`) vs toutes.

---

## Bareme indicatif (chaque TP)

| Critere | Points |
|---|---|
| Code correct et execute sans erreur | 8 |
| Choix methodologiques justifies (k, max_depth, metriques) | 6 |
| Interpretation metier des resultats | 4 |
| Bonus | 2 |
