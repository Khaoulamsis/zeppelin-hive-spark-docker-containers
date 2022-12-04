
## Mise en place de Spark sur Apache Zeppelin pour l’exécution d’un pipeline ML

L’objectif principal de notre projet est la mise en place de Spark sur Apache Zeppelin pour l’exécution d’un pipeline Machine Learning. Pour cela, on a utilisé ce cluster Docker qui contient le conteneur Docker de Apache Hive 2.3.2 et le conteneur de Apache Zeppelin 0.10.0.


Pour cloner ce repository Github:
```
    git clone https://github.com/Khaoulamsis/zeppelin-hive-spark-docker-containers.git
```

Pour créer les conteneurs et les exécuter : 
```
    docker-compose up -d
```


### Testing

Tester la connexion avec Hive:
```
  $ docker exec -u root -it hive-hive-server-1 /bin/bash
  # /opt/hive/bin/beeline -u jdbc:hive2://localhost:10000
  > show databases;
  > create database test;
```

Pour tester le bon fonctionnement de Zeppelin:
```
    https://localhost:8080
```

### Ajout des jars dans le conteneur Zeppelin
```
    docker exec -u root -it zeppelin-test bash
    cd /opt/zeppelin/interpreter/jdbc
    wget -c https://repo1.maven.org/maven2/org/apache/hive/hive-jdbc/2.3.2/hive-jdbc-2.3.2-standalone.jar  -O hive-jdbc-2.3.2-standalone.jar 
    wget -c https://repo1.maven.org/maven2/org/apache/hadoop/hadoop-common/2.6.0/hadoop-common-2.6.0.jar -O hadoop-common-2.6.0.jar
```

### Configuration de l'interpreteur Hive
```
    default.url  jdbc:hive2://hive-hive-server-1:10000/
    default.use   hive
    default.password    hive
    default.driver    org.apache.hive.jdbc.HiveDriver
```
Dependencies: 

``` 
/opt/zeppelin/interpreter/jdbc/hive-jdbc-2.3.2-standalone.jar
/opt/zeppelin/interpreter/jdbc/hadoop-common-2.6.0.jar
```

### Déplacer un fichier depuis la machine local à un conteneur Docker

``` 
docker cp fichier.csv 'identifiant du conteneur':/fichier.csv
```

