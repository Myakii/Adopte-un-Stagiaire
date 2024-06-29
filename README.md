# Adopte-un-Stagiaire
Site de recrutement pour stagiaire (et autres)

# Hackaton - Adopte un stagiaire | REACT JS & NODE JS

- Site internet : [LIENSITE](https://github.com/HETIC-WEB2-Hackathon-2024)
- Github :
  
    Ensemble du projet : https://github.com/HETIC-WEB2-Hackathon-2024
  
    Github du projet : https://github.com/HETIC-WEB2-Hackathon-2024/bleu-aus
  
    Github de la base de données : https://github.com/HETIC-WEB2-Hackathon-2024/aus-database

---
## Tech Stack
- REACT JS
- NODE JS
- Material UI
- NPM
- CSS
- Docker

---

## Installation
### Configuration initiale
Récupérer le projet sur github, équivalent à un `git clone`.

```bash
git clone https://github.com/HETIC-WEB2-Hackathon-2024/bleu-aus
```

Récupérer la base de données.
```bash
cd web-service
git clone https://github.com/HETIC-WEB2-Hackathon-2024/aus-database
cd aus-database
cd postgresql
docker network create web
docker compose up -d
# Note: vous pouvez ignorer les warnings sur Mac M1/M2
# creates aus database
docker compose exec -it postgres-aus psql -U aus-user -d postgres -f /tmp/sql/create-database.sql
# creates the postgis postgreSQL extension
# for geo spatial data types
docker compose exec -it postgres-aus psql -U aus-user -d aus -f /tmp/sql/create-extension.sql
# creates aus tables
docker compose exec -it postgres-aus psql -U aus-user -d aus -f /tmp/sql/create-tables.sql
# loads data in tables from CSV files
docker compose exec -it postgres-aus psql -U aus-user -d aus -f /tmp/sql/load-data.sql
```

Création de la base de données PgAdmin (postgres)
```bash
Depuis votre navigateur, allez à l'adresse localhost:5010/

Connectez vous avec

login: prof@aus.floless.fr
mdp: aus2025
Ajoutez la connection vers postgres

Click-droit sur Servers > Register > Server

**Name**: mettez Local

Dans le tab Connection:

**Host name / address**: postgres-aus
**port**: 5432
**user**: aus-user
**password**: aus2025

**sauvgarder**

Vous devriez avoir accès aux tables de aus dans le schéma public
```

Utilisation de la base de données
```bash
Allez sur : http://localhost:5010/browser/ sur le navigateur
Identifiant: prof-aus
Mot de passe : aus2025
Local -> Base de données -> aus -> Schémas -> public -> Table 
Ajouter la table suivante :
```
```sql
CREATE TABLE selection_offre (
    selection_offre_id SERIAL PRIMARY KEY,
    candidat_id INT NOT NULL,
    offre_id INT NOT NULL,
    date_ajout DATE NOT NULL DEFAULT CURRENT_DATE,
    FOREIGN KEY (candidat_id) REFERENCES candidat(id),
    FOREIGN KEY (offre_id) REFERENCES offre(id)
);
```

Ouvrir un terminal frontend :
```bash
cd frontend
npm i
npm run dev
```

Ouvrir un autre terminal pour le backend :
⚠️ Il faut toujours avoir Docker d'ouvert pour lancer le processus ⚠️
```bash
cd web-service
npm i
npm run dev
```

Le projet est utilisable !

---

Ce projet rassemble 8 personnes pour une durée de 35 heures sur une semaine. L'objectif était de créer un site de recrutement de stagiaires avec une API, un backend et un frontend fourni.
