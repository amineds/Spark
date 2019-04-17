### Séance 1

Voir limites en NameNode

Nombre de jobs MR à lancer dans un cluster limité

HDP 1.0 to HDP 2.0 : problème de scalabilité au niveau du name node

Voir DCOS - Data Center Operating System / MESOS / Marathon / Chronos

Approfondir la notion de DAG, exemple TEZ

Comprendre le job map reduce hadoop

Comprendre le job spark

sites web : Données Produits, Clients et Paiements

https://databricks.com/blog/2015/04/13/deep-dive-into-spark-sqls-catalyst-optimizer.html

https://mesosphere.com/blog/high-performance-edge-load-balancer/

Machine Master : Name Node, Job Tracker

Machine Slave : Data Node, Task Tracker

HA Deployment : Failover manager qui s'appuie sur Zookeeper (créateur de consensus lors de la perte du master --> élection du master)

https://www.elastic.co/products/beats

### Séance 2

HDFS
----
1- pas besoin de gérer la partie metadata des gros fichiers coupés - abstraction globale de la répartition des fichiers
abstraction pour faciliter la manipulation des fichiers

2- réplication des données pour éviter le SPOF, fiabilité et résilience & disponibilité
Les disques tombent en panne souvent, les réseaux ne sont pas fiables

3- GFS expose un système de metadata qui permettent la communication de ces données aux jobs de data processing.
Expose une interface pour optimiser le processing

4- Scalabilité

Plus on montera en abstraction, plus on ajoutera de la compléxité, par exemple parcourir un fichier avec HBASE est plus coûteux que de le faire avec HDFS

Avro/Parquet : sérialisation de la donnée afin de mieux gérer le requêtage et l'évolutivité de la donnée

Petit ou gros fichiers : même API

Parallélisation : partager le travail en plusieurs tâches qui partage le même état (Shared state, MPP), beaucoup de RAM

Distribué : partager le travail en plusieurs tâches qui ne partage pas le même état

De plus en plus d'entreprises, mettent leurs données sur S3.

Il est important de bien comprendre la distribution, la nature et la charactéristique des datasets.

Merge and Sort algorithm : https://en.wikipedia.org/wiki/Merge_sort

Bien Comprendre le MPP et les FS distribués

2 grandes familles distribuées : Master-Worker & 

Hadoop : NameNode vs Data Node
MR : JobTracker vs TaskTracker

Voir Pattern de systèmes distribués

NameNode : 
1- ne stocke pas la donnée : pour limiter la responsabilié (une seule) et ne fasse pas quelque chose qui le mette en péril.
2- état global du cluster : topologie, index d'accès aux fichiers (état du FS), exposition des metadonnées
3- point d'accès, d'entrée
4- garant de la consistence du FS, distribution des données

DataNode
1- stockage de la donnée
2- The DataNodes are responsible for serving read and write requests from the file system’s clients. 
3- The DataNodes also perform block creation, deletion, and replication upon instruction from the NameNode. 

Block : unité de lecture ou d'écriture - le FS gère des blocks, ne gère pas les fichiers
HDFS va écrire des blocks

Ecriture du fichier dans HDFS
1- Contact du NameNode
2- Retour avec des informations sur les blocks, les pointeurs pour streamer la data

### Séance 3
Installer sbt (Simple Build Tool)
Installer scala
Installer IDE (intellij)

Spark
-----
Trois bin importants : spark-shell, pyspark, spark-submit (pour le déploiement)

Selon le langage, on package et on lance spark-submit

2 types d'actions en Spark : transformations & actions

Faire du shell pour bien comprendre le schéma inféré

RDD = (Parent,Operation) --> Type

Shuffle : 

Job = DAG = Suite de tâches, les tâches sont regroupées par stage

Yarn - MRv2

Yarn (ressources manager) est le point d'entrée de l'Application Master 
Yarn gère les Nodes Managers

4 façons de déployer
standalone
Mesos
Yarn
Kubernetes

Lancement de Spark : Lancement d'un driver et des executors

Spark : application pour démontrer l'allocation dynamique des ressources

Conception de jobs Spark : combien d'executeurs par machine, combien de cores par executeur

Yarn/MESOS : limitation par application (par exemple 100 cores par app)

Coder un job spark  utiliser un minimum de ressources possibles.

JVM Executor : petite partie pour la JVM + Mémoire partagée par Executor + Tasks + RDD

Ne jamais faire le collect

Pour pallier aux crashs de switchs, il faut cacher en mémoire

Penser aux RDD LAZY

S'assurer de la bonne répartition des données à travers les partitions


### Séance 4

Livrer en prod : définir des règles

Architecture : les éléments difficiles voir impossibles à défaire

Règle Architecture : livrer des packages system (.rpm pour CentOS)

Job Spark : qu'est ce qu'on livre ?

Choisir son modèle de packaging pour la testabilité, portabilité

Maven : gestion des dépendances par xml, approche déclarative

Sbt : gestion des dépendances par code, approche programatique






