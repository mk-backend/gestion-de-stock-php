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
- UwAmp comme serveur local

## Ce que j'ai appris

- Organiser le code en dossiers **model** (accès aux données) et **vue** (pages affichées).
- Utiliser des **requêtes préparées** PDO pour se protéger des injections SQL.
- Regrouper les lectures en base derrière une classe unique (`DataFacade`, patron de conception Façade).
- Gérer les sessions et l'authentification sans framework.

## Pourquoi une version Symfony ensuite

Cette version montre ses limites quand le projet grandit : pas de routeur, du SQL écrit à la main dans chaque fichier, pas de tests.
Le projet AlphaRetail reprend la même application avec Symfony (routes, Doctrine, Twig) pour la rendre plus simple à maintenir.

## Lancer le projet en local

1. Copier le dossier dans le répertoire web de UwAmp, XAMPP ou WAMP (par exemple `www/gestion_de_stock`).
2. Créer une base MySQL nommée `gestion_de_stock`.
3. Si besoin, définir les variables d'environnement `DB_HOST`, `DB_NAME`, `DB_USER` et `DB_PASSWORD` (par défaut : `localhost`, `gestion_de_stock`, `root`, `root`).
4. Ouvrir `http://localhost/gestion_de_stock/vue/login.php`.

Le script de création des tables n'est pas inclus dans ce dépôt.

## Organisation du code

| Dossier | Rôle |
|---|---|
| `model` | Connexion à la base, fonctions de lecture et traitements des formulaires (ajout, modification, suppression) |
| `vue` | Les pages de l'application (connexion, tableau de bord, articles, ventes, reçus...) |
| `public` | Feuille de style, images et icônes |
