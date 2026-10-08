# sgbd-local

Serveurs de bases de données locaux via Docker (MariaDB + PostgreSQL) pour le développement.

## Prérequis

- [Docker](https://www.docker.com/get-started) et [Docker Compose](https://docs.docker.com/compose/) installés

## Configuration

1. Dupliquer le fichier d'exemple :

```bash
cp exemple.env .env
```

2. Éditer `.env` avec vos propres valeurs :

```env
# MariaDB Configuration
MARIADB_ROOT_PASSWORD=leMotDePasseRoot
MARIADB_DATABASE=nomDeVotreBase
MARIADB_USER=nomUtilisateur
MARIADB_PASSWORD=motDePasseUtilisateur

# PostgreSQL Configuration
POSTGRES_PASSWORD=motDePasseUtilisateur
POSTGRES_DB=nomDeVotreBase
POSTGRES_USER=nomUtilisateur
```

## Utilisation

### Démarrer les serveurs

```bash
docker-compose up -d
```

Cela démarre deux conteneurs :

| Service | Image | Port | Container |
|---------|-------|------|-----------|
| MariaDB | `mariadb:latest` | 3306 | `mariadb_server` |
| PostgreSQL | `postgres:latest` | 5432 | `postgres_server` |

### Arrêter les serveurs

```bash
docker-compose down
```

### Arrêter et supprimer les données

```bash
docker-compose down -v
```

> **Note** : L'option `-v` supprime également les volumes Docker persistants (données des bases).

### Voir les logs

```bash
docker-compose logs -f
```

### Se connecter aux bases

**MariaDB**

```bash
docker exec -it mariadb_server mysql -u root -p
```

**PostgreSQL**

```bash
docker exec -it postgres_server psql -U postgres
```

## Structure

```
sgbd-local/
├── docker-compose.yml
├── exemple.env       # template à dupliquer
├── .env              # créé depuis exemple.env
└── .gitignore        # .env ignoré
```

## Volumes

Les données sont persistées dans des volumes Docker nommés :

- `mariadb_data` → `/var/lib/mysql`
- `postgres_data` → `/var/lib/postgresql/data`
