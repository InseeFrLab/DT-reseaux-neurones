### Ce dépôt contient les liens vers les programmes associés au document de travail :
# *Les réseaux de neurones appliqués à la statistique publique: méthodes et cas d'usages*.

Auteurs :
*Damien Babet*,
*Quentin Deltour*,
*Thomas Faria*,
*Stéphanie Himpens*


## Chapitre 1 : Apprentissage algorithmique (*Machine learning*) et réseaux de neurones, concepts et prise en main

Le répertoire [Chapitre_1](https://github.com/InseeFrLab/DT-RN-chapitre1) contient l'ensemble des programmes du chapitre 1.

*Les programmes sont en **R***

Le script principal [neural_network_cifar100.R](https://github.com/InseeFrLab/DT-RN-chapitre1/blob/main/R/neural_network_cifar100.R) contient le déroulé intégral de l'exemple de classification de meubles (chaises et tables) sur la base d'images *CIFAR100* c'est-à-dire :
1. L'import des images à utiliser
2. Un premier exemple de réseau de neurones avec la librairie **neuralnet**
3. Une classification par une régression pénalisée (Lasso)
4. Un réseau de neurones plus élaboré avec la librairie **Keras**

Le script [neural_network_cifar100_pytorch.R](https://github.com/InseeFrLab/DT-RN-chapitre1/blob/main/R/neural_network_cifar100_pytorch.R) le réseau de neurones du 4. précédent programmé avec **torch**

Le script [Un_premier_convnet.R](https://github.com/InseeFrLab/DT-RN-chapitre1/blob/main/R/Un_premier_convnet.R) effectue la classification des chaises et des tables de la base **CIFAR100** à l'aide d'un **convnet**. Cet exemple est à relier au chapitre 3 sur les parcelles cadastrales.

Les codes ont été écrits par [Stéphanie Himpens](https://github.com/srhimp) (Insee / Banque de France).

## Chapitre 2 : Prédire pour imputer
Le dépôt [Chapitre_2](https://github.com/InseeFrLab/DT-RN-chapitre2) contient le code produisant les résultats du chapitre 2. Le programme est en **python**, le réseau de neurone est réalisé avec les librairies **Keras** et **Tensorflow**.

Le code exploite des données disponibles uniquement en interne sur les serveurs de calcul de l'Insee (fichiers de production de l'enquête Emploi). Il s'agit d'un notebook jupyter conçu pour être exploitable directement sur les collections rpython et lab. 

Les résultats ne sont donc pas reproductibles en dehors de cet environnement et sans accès à ces données. La mise à disposition du code est à visée pédagogique

Le notebook se divise en 5 parties :
1. Un préambule de chargement des packages et fonctions mobilisées
2. La préparation des données: construction de la variable à imputer et des features, traitement des valeurs manquantes et vectorisation des nomenclatures
3. L'entraînement du RN: split train/test, construction du modèle, entraînement, analyse des résultats sur l'échantillon de validation et enregistrement du modèle
4. Prédiction sur l'échantillon test: différentes mesures de performances sur différents échantillons test, prédictions par tranche, résultats sur la population des non-répondants au salaire en clair qui ont répondu par tranche ("véritable" non-réponse)
5. Comparaison avec des modèles log-linéaires: sur les mêmes inputs que le RN, ou sur des variables plus classiques de modélisation économétrique

Les codes ont été écrits par [Damien Babet](https://github.com/DamienBabet) (Insee).

## Chapitre 3 : Réseaux convolutifs et analyse d'images
Le dépôt [Chapitre_3](https://github.com/InseeFrLab/DT-RN-chapitre3) contient le code produisant les résultats du chapitre 3. Les programmes de cette partie sont écrit en **python**. Le réseau (CNN) est réalisé avec la librairie **Keras** tandis que la forêt aléatoire utilise la librairie **sklearn**.

Le code se divise en 4 scripts distincts :

- [1-run_preprocessiong.py](https://github.com/InseeFrLab/DT-RN-chapitre3/blob/main/1-run_preprocessing.py) : Ce code consitue les échantillons de tests et d'entrainements de notre réseau de neurones. Pour cela :    
    - Il importe les données du cadastre (département de la Manche et de la Marne), ainsi que les empreintes des villages ;
    - Il transforme les données géométrique en images (rasters) ;
    - Il tire des échantillons d'images et crée les labels (suppression des images peu ou pas du tout remplies, identification des villes) ;
    - Il réalise le sur_échantillonage des villes, sous représentées.

- [2-run_CNN.py](https://github.com/InseeFrLab/DT-RN-chapitre3/blob/main/2-run_CNN.py) : Ce code permets de définir la structure du réseau de neurones que l'on souhaite estimer à l'aide de la librairie Keras. Il montre comment la sélection des hyperparamètres (nombre de couches de convolutions, profondeur et taille des filtres) peut être réalisées. Enfin il illustre également l'algorithme de Grad-CAM.

- [3-run_random_forest.py](https://github.com/InseeFrLab/DT-RN-chapitre3/blob/main/3-run_random_forest.py) : Ce script présente un modèle alternatif pour réaliser la même tâche de classification. Il estime une forêt aléatoire à l'aide de features préalablement construites.

Les codes ont été écrits par [Stéphanie Himpens](https://github.com/srhimp) (Insee / Banque de France).


## Chapitre 4 : Réduction de dimension
Le dépôt [Chapitre_4](https://github.com/InseeFrLab/DT-RN-chapitre4) contient le code produisant les résultats du chapitre 4.
Les programmes de cette partie sont écrit en **python**. Le réseau (*autoencoder*) est réalisé avec la librairie **Keras**.

Le code se divise en 4 scripts distincts :

- [1-runDataRetrieval.py](https://github.com/InseeFrLab/DT-RN-chapitre4/blob/main/1-runDataRetrieval.py) : Ce code télécharge automatiquement des données de la Banque Centrale Européenne via l'API de Statistical Data Warehouse (SDW). Nous téléchargeons ici des données d'indice des prix, mais ce script peut être utilisé pour récupérer toutes autres bases de données répertoriées dans SDW.
- [2-runPreprocessing.py](https://github.com/InseeFrLab/DT-RN-chapitre4/blob/main/2-runPreprocessing.py) : Cette partie définit tout d'abord le type de variables (catégorielle ou numérique). Elle procède ensuite à la préparation de la base de données en imputant les données manquantes, en ajustant l'échelle des données et en divisant les données en 3 sous-échantillons (*train*, *test*, *validation*).
- [3-runTraining.py](https://github.com/InseeFrLab/DT-RN-chapitre4/blob/main/3-runTraining.py) : Ce script définit les hyper-paramètres de l'autoencoder et procède à son estimation. On présente également une solution pour enregistrer les résultats en fonction des paramètres spécifiés.
- [4-runACP.py](https://github.com/InseeFrLab/DT-RN-chapitre4/blob/main/4-runACP.py) : Ce code réplique le travail effectué par le script précédent, en utilisant cette fois un algorithme d'Analyse par Composantes Principales (ACP) afin d'en comparer les performances.

Les codes ont été écrits par [Thomas Faria](https://github.com/ThomasFaria) (Insee).
