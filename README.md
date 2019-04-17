## Structure du cours
- [x] Vision de l'écosystème
- [x] Deep dive sur chaque élément consistuant de l'écosystème
  - [x] HDFS
  - [x] Spark
- [x] Cas d'usage
- [x] Critères de sélection
- [x] Le Datalake


- - -

## Installation de hadoop sous ubuntu

- Installation de java : apt-get install oracle-java8-jdk (par exemple)

- Dans le fichier /etc/environment ajouter la ligne : JAVA_HOME="/usr/lib/jvm/oracle-java8-jdk-amd64"

- Commande : source /etc/environment

- Commande : export JAVA_HOME

- Telecharger le binaire hadoop depuis le lien suivant : http:/hadoop.apache.org/releases.html

- Decompresser l'archive dans le dossier de votre choix : tar -xzvf [Nom de l'archive]

- Si ssh localhost ne marche pas : generer cle sans passphrase (ssh-keygen -t rsa) et eventuellement activer le remote login (sudo systemsetup -setremotelogin on)
