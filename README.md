# PROJET-ESME

Le but de ce projet est de collecter les données météos de plusieurs villes, ici Paris, London, Tokyo, Melbourne, Milan, en utilisant l'API OpenWeather. Le producer collecte les données météo et les envoie au topic kafka (broker) qui les stocks. Ensuite, le consumer récupère les données depuis le broker, les transforme et les analyse en ajoutant des variables comme un indice de chaleur par exemple. 


## Détail des différents éléments de l'architecture

Le producer collecte des données météo grâce à l'API OpenWeather et les renvoie à un topic Kafka, ici topic-weather toutes les 60 secondes. Avant l'envoi, les données sont encodées en JSON afin de garantir leur compatibilité avec Kafka.

le topic Kafka stocke et diffuse les messages envoyés par le producer. Un premier topic, topic-weather, contient les données brutes collectées directement depuis l'API. Un second topic, topic-weather-final, stocke les données transformées par Spark Streaming après analyse et enrichissement.

Le consumer lit les messages du topic topic-weather et extrait les informations pertinentes. Plusieurs transformations sont appliquées aux données pour enrichir leur contenu. Une fois les transformations effectuées, les données enrichies sont soit affichées dans la console pour vérification, soit renvoyées vers Kafka dans le topic topic-weather-final pour être utilisées par d'autres applications ou stockées pour des analyses ultérieures.

Lien Producer-Consumer : le producer récupère en continu les données météo et les envoie à Kafka. Kafka joue le rôle d’un message broker en assurant la persistance et la diffusion des messages aux consommateurs. Spark Streaming agit comme un consumer en lisant ces messages en temps réel, en les transformant et en générant de nouvelles informations exploitables. Ces données sont ensuite renvoyées vers Kafka dans un second topic, ce qui permet une gestion efficace et évolutive du flux de données.
