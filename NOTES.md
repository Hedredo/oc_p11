# La mission

## Présentation
Je suis Data Scientist pour une très jeune start-up nommée "Fruits!" spécialisée dans l'AgriTech. Mon collègue Paul m'a présenté le notebook et le jeu de données.

Il m'a prévenu des points suivants:
- Développer les scripts en PySpark et utilisation du cloud AWS (instance EMR, stockage S3, IAM)
- Démonstration de la mise en place d'une instance EMR opérationnelle
- Explication pas à pas du script PySpark enrichi de :
  - Traitement de diffusion des poids du modèle TensorFlow sur les cluster. -> Ajouter le broadcast des weights du modèle en s'appuyant sur l'article “Model inference using TensorFlow Keras API (en anglais)”. https://docs.azure.cn/en-us/databricks/machine-learning/model-inference/resnet-model-inference-keras
  - Ajout d'une étape de réduction de dimension -> PCA en PySpark.
  - Respect des contraintes RGPD en deploy sur Europe
  - Retour critique de la solution
  - EMR classique ou serverless ? Niveau des coûts

**`AgriTech` :** L’agritech (ou agrotechnologie) désigne l’ensemble des technologies appliquées à l’agriculture pour la rendre plus productive, durable et innovante. C’est la contraction de "agriculture" et "technologie". Agritech = agriculture + technologie. 

**Objectifs de l'agritech :**
- Optimiser les ressources
- Améliorer les rendements agricoles
- Réduire l'impact environnemental
- Répondre aux enjeux alimnetaires mondiaux

  **Objectif de la start-up :** Préserver la biodiversité des fruits en développant des robots ceuilleurs intelligents avec des traitements spécifiques pour chaque espèce de fruits.

  <img width="1517" height="601" alt="16783555381729_Data Scientist-P9-01-banner" src="https://github.com/user-attachments/assets/90a9f803-bdbe-4cac-be97-61dbe704970b" />

## Développer une application de classification des images de fruits
La start-up souhaite se faire connaître avec une application mobile qui permettrait aux utilisateurs de prendre un fruit en photo et d'obtenir des informations de ce fruit.

Le développement de l'application mobile permettra de construire une première version de l'architecture BigData nécessaire.

Une première approche a été testé dans un environnement Big Data `AWS EMR`.

**`AWS EMR` :** Amazon EMR (Elastic MapReduce) est un service managé d’AWS qui permet de traiter et d’analyser de grandes quantités de données. Il est conçu pour exécuter des jobs de big data (ETL, machine learning, traitement de logs, analytics, etc.) de manière scalable, rapide, et économique, sans devoir gérer toi-même l’infrastructure.

| Avantage       | Description                                                                                  |
| -------------- | -------------------------------------------------------------------------------------------- |
| **Managé**     | AWS gère les clusters, les mises à jour, la sécurité.                                        |
| **Scalable**   | Ajout/retrait automatique de nœuds en fonction de la charge.                                 |
| **Économique** | Facturation à la minute, possibilité d’utiliser des instances Spot.                          |
| **Flexible**   | Peut être déployé sur EC2, EKS (containers), ou S3 (mode serverless via **EMR Serverless**). |
| **Intégrable** | Compatible avec S3, RDS, DynamoDB, Redshift, SageMaker, etc.                                 |

**Architecture typique d'un cluster EMR classique:**
- Master node : coordonne le cluster.
- Core nodes : exécutent les tâches et stockent les données (HDFS).
- Task nodes (optionnels) : exécutent uniquement des tâches.

**Principe du EMR Serverless (mode sans cluster) :**
- Pas besoin de gérer des nœuds ou des clusters.
- Tu soumets un job Spark ou Hive, EMR s’occupe du reste.
- Bon choix pour les workloads intermittents ou imprévus.

**Cas d’usage typiques :**
- Traitement de données massives (logs, clics, IoT…)
- Nettoyage et transformation de données (ETL)
- Apprentissage automatique avec Spark MLlib
- Business Intelligence avec Hive, Presto, ou Spark SQL

## Le jeu de données d'images et de labels de fuits
-> Téléchargeable au lien suivant : https://s3.eu-west-1.amazonaws.com/course.oc-static.com/projects/Data_Scientist_P8/fruits.zip
-> Kaggle dataset: https://www.kaggle.com/moltean/fruits

## Base de travail
-> Notebook de l'alternant : https://s3.eu-west-1.amazonaws.com/course.oc-static.com/projects/Data_Scientist_P8/P8_Mode_ope%CC%81ratoire.zip

# Etapes préconisées
1. Ajout de l'étape PCA dans le notebook
2. Identifier les services pertienents pour migrer chaque étape de la chaîne de traitement en local vers le cloud AWS
3. Mise en place du cluster EMR
4. Connceter le notebook cloud pour réaliser la chaîne de traitement jusqu'à la réduction de dimensions.
5. Notebook & scripts bien commentées, bonne organisation dans le cloud
6. Présenter l'architecture cloud et le processus de traitement pyspark en justifiant les choix techno.
7. Démonstration technique

# Livrables
1. Notebook sur le cloud contrenant les scripts PySpark exécutables (préprocessing + réduction de dimension de type PCA)
2. Les images du jeu de données initial ainsi que la sortie de réduction de dimension (matrice sur un fichier CSV ou parquet) dans un espace de stockage S3
3. Un support de présentation pour la soutenance :
   - les différentes briques d'architecture choisies sur le cloud
   - leur rôle dans l’architecture Big Data
   - la démarche de mise en oeuvre de l’environnement Big Data (EMR ou Databricks)
   - les étapes de la chaîne de traitement PySpark.
  
# Soutenance
Pendant la soutenance, l’évaluateur jouera le rôle de Paul. Vous lui présenterez l’ensemble de votre travail. 

**Présentation (20 minutes)**
- Rappel de la problématique et présentation du jeu de données (3 mn)
- Présentation du processus de création de l’environnement Big Data, S3 et EMR ou Databricks (6 mn)
- Présentation de la réalisation de la chaîne de traitement des images dans un environnement Big Data dans le cloud, à l'aide de votre support de présentation (6 mn)
- Démonstration d’exécution du script PySpark sur le Cloud (2 mn)
- Synthèse et conclusion (3 mn)

**Discussion (5 minutes) :** L’évaluateur vous challengera sur votre compréhension de concepts et techniques mis en oeuvre. 

**Débriefing (5 minutes)**
