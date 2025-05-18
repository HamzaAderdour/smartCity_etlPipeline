# Pipeline ETL pour l'analyse de données de capteurs IoT

## Description
Ce projet implémente un pipeline ETL complet pour l'analyse en temps réel des données de capteurs IoT dans une ville intelligente. Le système collecte, traite et analyse les données de température, d'humidité et de pollution provenant de capteurs répartis dans différents quartiers.

## Architecture
- **Ingestion de données** : Kafka pour la collecte en temps réel
- **Orchestration** : Airflow pour la gestion du pipeline ETL
- **Traitement** : Celery pour les tâches de transformation et d'agrégation
- **Stockage** : Elasticsearch pour le stockage et la recherche
- **API** : FastAPI pour l'exposition des données
- **Interface** : React.js pour la visualisation
- **Monitoring** : Prometheus & Grafana

## Structure du projet
```
├── 📂 config/           # Fichiers de configuration
├── 📂 data-ingestion/   # Composants d'ingestion Kafka
├── 📂 etl-pipeline/     # Pipeline ETL (Airflow, Celery)
├── 📂 data-storage/     # Stockage Elasticsearch
├── 📂 api/             # API FastAPI
```

## Installation
1. Cloner le repository
2. Installer les dépendances : `pip install -r requirements.txt`
3. Configurer les variables d'environnement
4. Lancer les services (instructions détaillées à venir)

## Configuration
Les fichiers de configuration se trouvent dans le dossier `config/` :
- `airflow.cfg` : Configuration Airflow
- `kafka.yml` : Configuration Kafka
- `elasticsearch.yml` : Configuration Elasticsearch
- `env.yml` : Variables d'environnement

## Développement
Instructions pour le développement à venir...

## Licence
Propriétaire - Tous droits réservés 