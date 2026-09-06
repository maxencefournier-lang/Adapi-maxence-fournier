ADAPI — La Remise

API REST réalisée avec Node.js, Express et PostgreSQL.

Installation et lancement

1. Installer les dépendances

npm install

2. Configurer la base de données

Créer un fichier .env à la racine du projet :

DB_HOST=localhost
DB_PORT=5432
DB_USER=postgres
DB_PASSWORD=votre_mot_de_passe
DB_NAME=laremise

Créer ensuite la base PostgreSQL puis importer :

psql -U postgres -d laremise -f migration_up.sql
psql -U postgres -d laremise -f seed.sql

3. Lancer le projet

npm run dev

Le serveur est disponible sur :

http://localhost:3000

La documentation Swagger est disponible sur :

http://localhost:3000/api-docs

Routes disponibles

Méthode

Route

Description

GET

/

Vérifie que le serveur fonctionne

GET

/objets

Liste les objets avec leur catégorie

GET

/objets/:id

Affiche un objet

PUT

/objets/:id

Modifie le libellé et le poids d'un objet

PATCH

/objets/:id/statut

Modifie le statut et éventuellement le prix

POST

/personnes

Crée une personne

POST

/depots

Crée un dépôt

POST

/depots/:id/objets

Ajoute un objet à un dépôt

GET

/categorie

Liste les catégories

GET

/stats

Retourne les statistiques sur les objets

Les créations renvoient un statut 201, les requêtes réussies 200, les données incorrectes 400 et une ressource introuvable 404.

Tester l'API

L'API peut être testée avec Bruno, Postman, Insomnia, Swagger ou curl.

Exemple pour créer une personne :

curl -X POST http://localhost:3000/personnes \
  -H "Content-Type: application/json" \
  -d '{"nom":"Martin","prenom":"Julie","telephone":"0612345678","adherente":false}'

Exemple pour créer un dépôt :

curl -X POST http://localhost:3000/depots \
  -H "Content-Type: application/json" \
  -d '{"personne_id":1,"date_depot":"2026-09-06","type":"boutique"}'

Exemple pour consulter les statistiques :

curl http://localhost:3000/stats