# Gestion de stock (PHP natif)

Application web de gestion des stocks d'un magasin, écrite en PHP natif avec MySQL (2024).

C'est la version d'origine de mon projet de fin d'études : je l'ai ensuite modernisée avec Symfony dans le projet **AlphaRetail**.
Version Symfony : [mk-backend/Symfony](https://github.com/mk-backend/Symfony)

## Fonctionnalités

- **Connexion et inscription** des gestionnaires, avec mots de passe hachés (`password_hash`) et page « mot de passe oublié ».
- **Articles, catégories, clients et fournisseurs** : ajout, modification et suppression.
- **Ventes et commandes fournisseurs**, avec un reçu imprimable pour chacune.
- **Tableau de bord** : chiffre d'affaires, dernières ventes et articles les plus vendus.
- **Recherche** d'articles.

## Technologies

- PHP (sans framework) et PDO
- MySQL
- HTML et CSS
- Docker (PHP 8.3 avec Apache, MySQL 8, phpMyAdmin)

## Ce que j'ai appris

- Organiser le code en dossiers **model** (accès aux données) et **vue** (pages affichées).
- Utiliser des **requêtes préparées** PDO pour se protéger des injections SQL.
- Regrouper les lectures en base derrière une classe unique (`DataFacade`, patron de conception Façade).
- Gérer les sessions et l'authentification sans framework.
- Conteneuriser l'application avec **Docker** : un conteneur par service et la configuration dans un fichier `.env`.

## Pourquoi une version Symfony ensuite

Cette version montre ses limites quand le projet grandit : pas de routeur, du SQL écrit à la main dans chaque fichier, pas de tests.
Le projet AlphaRetail reprend la même application avec Symfony (routes, Doctrine, Twig) pour la rendre plus simple à maintenir.

## Lancer le projet en local

Avec Docker :

1. Copier `.env.example` en `.env` et choisir les mots de passe.
2. Lancer `docker compose up -d --build`.
3. Ouvrir `http://localhost:8081` pour l'application et `http://localhost:8082` pour phpMyAdmin.
4. Créer un compte depuis la page d'inscription.

Au premier lancement, MySQL crée les tables à partir des scripts du dossier `database`.

| Service | Rôle | Adresse |
|---|---|---|
| `web` | PHP 8.3 et Apache, le code est monté depuis le dossier du projet | `http://localhost:8081` |
| `db` | MySQL 8, les données sont gardées dans un volume Docker | `localhost:3307` |
| `phpmyadmin` | Interface pour consulter la base | `http://localhost:8082` |

Commandes utiles :

| Commande | Effet |
|---|---|
| `docker compose up -d` | Démarre l'application |
| `docker compose down` | Arrête l'application (les données sont conservées) |
| `docker compose logs -f web` | Affiche les erreurs PHP et Apache |
| `docker compose down -v` | Arrête et efface la base, qui sera recréée au prochain lancement |

À savoir :

- Le fichier `.env` contient les mots de passe : il n'est pas versionné, seul `.env.example` l'est.
- Pour charger des données de test, ajouter un fichier `database/2-donnees.sql` avant le premier lancement. Il n'est pas versionné.
- Les connexions au site sont enregistrées dans `logs/connexion.log`.
- L'email de « mot de passe oublié » n'est pas envoyé en local, car aucun serveur d'envoi n'est configuré.

Sans Docker (UwAmp, XAMPP ou WAMP) :

1. Copier le dossier dans le répertoire web du serveur (par exemple `www/gestion_de_stock`).
2. Créer une base MySQL nommée `gestion_de_stock` et y importer `database/1-structure.sql`.
3. Si besoin, définir les variables d'environnement `DB_HOST`, `DB_NAME`, `DB_USER` et `DB_PASSWORD` (par défaut : `localhost`, `gestion_de_stock`, `root`, `root`).
4. Ouvrir `http://localhost/gestion_de_stock/vue/login.php`.

## Organisation du code

| Dossier | Rôle |
|---|---|
| `model` | Connexion à la base, fonctions de lecture et traitements des formulaires (ajout, modification, suppression) |
| `vue` | Les pages de l'application (connexion, tableau de bord, articles, ventes, reçus...) |
| `public` | Feuille de style, images et icônes |
| `database` | Script de création des tables, chargé par MySQL au premier lancement |
| `logs` | Journal des connexions |
| `Dockerfile`, `docker-compose.yml` | Image PHP et description des conteneurs |
