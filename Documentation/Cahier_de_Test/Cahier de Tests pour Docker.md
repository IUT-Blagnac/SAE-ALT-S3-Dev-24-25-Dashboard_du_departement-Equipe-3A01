# Cahier de Recette : Tests pour Docker et ses conteneurs  

## Contexte

Ces tests visent à valider les fonctionnalités liées à l'utilisation de Docker et de ses conteneurs.
Les cas de test couvrent la création, le démarrage, l'arrêt et la suppression de conteneurs Docker.

### Références

**Issue GitHub** : [Effectuer les tests pour Docker](https://github.com/IUT-Blagnac/SAE-ALT-S3-Dev-24-25-Dashboard_du_departement-Equipe-3A01/issues/25)

### Assignees

- [Penicaud-Bernal Diego](https://github.com/Diego-PB)
- [Crisini Aidan](https://github.com/Smogita)

---

## Tests à effectuer

### 1. Démarrage des conteneurs Docker

**Objectif**

Vérifier que les conteneurs Docker (Nginx, PHP, Node-RED, TimescaleDB) démarrent correctement.

**Préconditions**

- Docker et Docker Compose sont installés sur la machine.

**Étapes**

1. Exécuter le script `docker_control.sh`.
2. Sélectionner l'option `1` pour démarrer les conteneurs.

**Critères d'acceptation**

- Tous les conteneurs sont démarrés sans erreur.
- Les services sont accessibles via leurs ports respectifs (ex. : `http://localhost` pour Nginx).

---

### 2. Arrêt des conteneurs Docker

**Objectif**

Vérifier que les conteneurs Docker s'arrêtent correctement et que les volumes sont supprimés.

**Préconditions**

- Les conteneurs sont en cours d'exécution.

**Étapes**

1. Exécuter le script `docker_control.sh`.
2. Sélectionner l'option `2` pour arrêter les conteneurs.

**Critères d'acceptation**

- Tous les conteneurs sont arrêtés.
- Les volumes associés sont supprimés.

---

### 3. Vérification des ports utilisés

**Objectif**

S'assurer que les ports 80 et 1880 ne sont pas déjà utilisés avant le démarrage des conteneurs.

**Préconditions**

- Aucun autre service n'utilise les ports 80 ou 1880.

**Étapes**

1. Exécuter le script `docker_control.sh`.
2. Observer les messages affichés lors de la vérification des ports.

**Critères d'acceptation**

- Un message d'erreur est affiché si un port est occupé.
- Aucun conflit de port ne se produit lors du démarrage des conteneurs.

---

### 4. Accès à la page d'accueil (Nginx)

**Objectif**

Vérifier que la page d'accueil du site s'affiche correctement via Nginx.

**Préconditions**

- Les conteneurs Docker sont démarrés.

**Étapes**

1. Ouvrir un navigateur web.
2. Accéder à l'URL `http://localhost`.

**Critères d'acceptation**

- La page d'accueil s'affiche sans erreur.
- Les éléments de la page sont chargés correctement.

---

### 5. Accès à l'interface Node-RED

**Objectif**

S'assurer que l'interface de Node-RED est accessible.

**Préconditions**

- Le conteneur Node-RED est démarré.

**Étapes**

1. Ouvrir un navigateur web.
2. Accéder à l'URL `http://localhost:1880`.

**Critères d'acceptation**

- L'interface de Node-RED s'affiche correctement.
- Les flux Node-RED sont fonctionnels.

---

### 6. Insertion des données dans TimescaleDB via Node-RED

**Objectif**

Vérifier que Node-RED insère correctement les données MQTT dans la base de données TimescaleDB.

**Préconditions**

- Un flux Node-RED est configuré pour insérer des données dans TimescaleDB.

**Étapes**

1. Configurer un flux MQTT dans Node-RED pour écouter un topic spécifique.
2. Vérifier l'insertion des données dans la table `Mesures` via une requête SQL.

**Critères d'acceptation**

- Les données sont insérées dans la table `Mesures` sans erreur.
- Les données insérées correspondent aux données MQTT reçues.

---

### 7. Connexion à la base de données TimescaleDB

**Objectif**

Vérifier la connexion à la base de données TimescaleDB via `psql`.

**Préconditions**

- La base de données TimescaleDB est en cours d'exécution.

**Étapes**

1. Exécuter la commande suivante :
   ```bash
   psql -h localhost -U admin -d dashboard_db