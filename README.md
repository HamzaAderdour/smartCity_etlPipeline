# Pipeline ETL pour l'analyse de données de capteurs IoT

## Description
Ce projet implémente un pipeline ETL complet pour l'analyse en temps réel des données de capteurs IoT dans une ville intelligente. Le système collecte, traite et analyse les données de température, d'humidité et de pollution provenant de capteurs répartis dans différents quartiers.

## Architecture Technique

### 1. Data Ingestion Layer
- **Kafka Producers** : Collecte de données depuis APIs réelles
- **Topics Kafka** :
  - `raw-sensor-data` : données brutes des capteurs
  - `processed-data` : données traitées
  - `alerts` : alertes et anomalies
- **Sources de données** :
  - APIs météo (OpenWeatherMap)
  - APIs pollution (OpenAQ)
  - Capteurs simulés pour compléter

### 2. Processing Layer
- **Airflow DAGs** :
  - Pipeline ETL toutes les 10 minutes
  - Analyses historiques quotidiennes/hebdomadaires
- **Celery Workers** :
  - Nettoyage des données (suppression outliers)
  - Calculs d'agrégations (moyennes horaires/quotidiennes)
  - Détection d'anomalies

### 3. Storage Layer
- **Elasticsearch** :
  - Index `raw-sensor-data` : données brutes
  - Index `hourly-aggregations` : moyennes horaires
  - Index `daily-aggregations` : moyennes quotidiennes
  - Index `alerts` : anomalies détectées

### 4. API Layer
- **FastAPI Endpoints** :
  - `/api/v1/sensors/real-time` : données en temps réel
  - `/api/v1/aggregations/hourly/{district}` : moyennes horaires
  - `/api/v1/historical/{sensor_type}` : données historiques
  - `/api/v1/alerts` : anomalies détectées
  - `/api/v1/export/{format}` : export CSV/Excel

### 5. Frontend Layer
- Dashboard React responsive (microservice séparé)

## Configuration des Services
Services Docker Compose :
- zookeeper
- kafka
- elasticsearch
- airflow-webserver
- airflow-scheduler
- celery-worker
- redis (broker Celery)
- fastapi

## Types de Données Collectées
### Capteurs Environnementaux
- **Température** : °C (outliers: < -50°C ou > 60°C)
- **Humidité** : % (outliers: < 0% ou > 100%)
- **Pollution** :
  - PM2.5, PM10 (µg/m³)
  - NO2, SO2, CO (ppb)
  - Indice AQI

## Workflow ETL
### 1. Extract (Toutes les 10 minutes)
- Collecte depuis APIs externes
- Insertion dans Kafka topics
- Validation des formats

### 2. Transform
- Nettoyage (suppression outliers)
- Enrichissement (ajout métadonnées)
- Calculs d'agrégations
- Détection d'anomalies

### 3. Load
- Stockage dans Elasticsearch (données aberrantes et clean séparées)
- Indexation optimisée pour requêtes
- Archivage des données anciennes

## APIs Externes
### Données Météo
- OpenWeatherMap : Température, humidité, pression
### Données Pollution
- OpenAQ : Qualité de l'air mondial

## Fonctionnalités
✅ Collecte en continu depuis APIs réelles
✅ Pipeline ETL orchestré par Airflow
✅ Traitement asynchrone avec Celery
✅ Stockage optimisé avec Elasticsearch
✅ API complète avec FastAPI
✅ Dashboard React responsive
✅ Possibilité d'export des données
✅ Analyses historiques avancées

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