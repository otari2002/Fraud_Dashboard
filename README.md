# Détection de Fraudes avec Kafka Streams

Ce projet vise à développer une application Kafka Streams capable de détecter des transactions financières suspectes en temps réel, de les stocker dans une base de données, et de visualiser les données via un tableau de bord Grafana.

![Enregistrement2024-12-21114431-ezgif com-video-to-gif-converter](https://github.com/user-attachments/assets/c35364e1-94e1-4454-9950-efac9547f69b)

## Fonctionnalités Principales

1. **Traitement des Transactions en Temps Réel**
   - Lecture des transactions depuis le topic Kafka `transactions-input`.
   - Détection des transactions suspectes avec une règle simple : `montant > 8 000`.

2. **Configuration du Pipeline Kafka Streams**
   - Topics Kafka :
     - `transactions-input` : contient les transactions brutes.
     - `fraud-alerts` : reçoit les transactions détectées comme suspectes.
   - Kafka Streams applique les règles de détection de fraudes et publie les résultats.

3. **Stockage des Transactions Suspectes**
   - Intégration d'InfluxDB pour enregistrer les transactions suspectes en temps réel.

4. **Visualisation en Temps Réel avec Grafana**
   - Tableau de bord interactif :
     - Nombre de transactions suspectes par utilisateur.
     - Montant total des transactions suspectes sur une période donnée.
   - Graphiques mis à jour automatiquement.

5. **Environnement de Déploiement Complet**
   - Un fichier `docker-compose.yml` facilite le déploiement de Kafka et InfluxDB.
   - Grafana est installé depuis <a href="`https://grafana.com/docs/grafana/latest/setup-grafana/installation/`">https://grafana.com/docs/grafana/latest/setup-grafana/installation/</a>


---

## Installation

1. **Cloner le Répertoire du Projet**
   ```bash
   git clone https://github.com/otari2002/Fraud_Dashboard.git
   cd fraud_detection

2. **Lancer les Services avec Docker Compose**
   ```bash
   docker-compose up -d

  ![image](https://github.com/user-attachments/assets/364b268e-5207-4a4e-8c81-68f52283eafd)


3. **Configurer les Connexions**
   - Kafka : Assurez-vous que les topics transactions-input et fraud-alerts sont créés.
   ![Capture d’écran 2024-12-17 235123](https://github.com/user-attachments/assets/79b23166-b418-425d-bb59-59fdcfaf2691)
   ![Capture d’écran 2024-12-17 235131](https://github.com/user-attachments/assets/232a9b5d-fc27-40e4-8704-014184913705)

   - Grafana : Connectez Grafana à InfluxDB et configurez le tableau de bord.
     Lancer les services avec Docker Compose va créer un bucket `fraud`.
      ![Capture d’écran 2024-12-20 205625](https://github.com/user-attachments/assets/ee4af40f-6a1e-4d59-985e-43ed161e6532)
      
     Dans la partie API Keys, il faut créer un clé et l'utiliser pour connecter Graphana avec InfluxDB.
     ![Capture d’écran 2024-12-20 205658](https://github.com/user-attachments/assets/f6c0a07b-1eb5-4683-81ef-91468234b489)

     Utilisez le nom d'utilisateur et le mot de passe de InfluxDB pour la partie `Basic Auth`.
  
   ![Capture d’écran 2024-12-20 225915](https://github.com/user-attachments/assets/2c737f31-942f-491d-90ed-1a06571f1e8c)

     Enfin, ajoutez le dashboard en utilisant le fichier json dans le dossier `graphana`.
   ![image](https://github.com/user-attachments/assets/ad76f675-a1ee-4f7c-b01b-034f7434a79d)


