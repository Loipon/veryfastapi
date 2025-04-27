# Projet FastAPI - Docker 

## Fonctionnement Global du Projet

Ce projet est une **API** construite avec **FastAPI** qui permet de :
- Gérer des **clients** 
- Gérer des **produits** 
- Gérer des **commandes** 

La base de données utilisée est **PostgreSQL*.

---

## Rôle de chaque Conteneur

| Conteneur | Rôle |
| **fastapi_app** | Conteneur principal qui exécute l'API FastAPI (image : loipon/fastapi_project:latest) |
| **postgres_db** | Conteneur qui exécute la base de données PostgreSQL |

---

## Dockerfile

Le `Dockerfile` utilise `loipon/fastapi_project` :

1. **FROM** : Utilise l'image officielle `python:3.11`
2. **WORKDIR** : Définit `/app` comme dossier de travail
3. **COPY** : Copie tout le code source dans l'imag
4. **RUN** : Installe les dépendances listées dans `requirements.txt`
5. **EXPOSE** : Rend le port 8000 accessible
6. **CMD** : Lance FastAPI avec Uvicorn

---

## docker-compose.yml

- **Service FastAPI** :
  - Utilise l'image Docker Hub `loipon/fastapi_project:latest`
  - Expose le port `8000`
  - Service PostgreSQL
  - Utilise `DATABASE_URL` pour permeettre la connexion à PostgreSQL

- **Service PostgreSQL** :
  - Utilise l'image officielle `postgres:14`
  - Crée un utilisateur `postgres` avec mot de passe `postgres`
  - Crée la base de données `postgres`
  - Expose le port `5432`
  - Utilise un volume `postgres_data` pour persister les données.

- **Volumes** :
  - `postgres_data` permet de conserver les données de la base de données même après l'arrêt du conteneur.

- **Network** :
  - `app-network` permet aux services de communiquer entre eux de manière isolée.

---

## Guide de Lancement

### 1. Démarrer l'environnement 

docker-compose up


### 2. Accéder à l'API

- Aller à l'url suivante :


http://localhost:8000


- Documentation interactive FastAPI :


http://localhost:8000/docs


### 3. Arrêter l'environnement


docker-compose down


## Brève Explication du Code

- **FastAPI** : pour créer l'API REST.
- **SQLAlchemy** : pour gérer la base de données PostgreSQL.
- **Pydantic** : pour valider les données.
- **httpx** : pour effectuer des tests HTTP dans l'application.
- Modèles principaux : `Customer`, `Product`, `Order`.



## Dépendances 
- fastapi
- uvicorn
- sqlalchemy
- pydantic
- httpx
- psycopg2-binary





