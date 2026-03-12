# Documentation Détaillée - Coolify Examples Repository

## 📋 Table des Matières

1. [Vue d'ensemble](#vue-densemble)
2. [Structure du Repository](#structure-du-repository)
3. [Configuration Coolify](#configuration-coolify)
4. [Applications Supportées](#applications-supportées)
5. [Guide par Framework](#guide-par-framework)
6. [Docker et Containerization](#docker-et-containerization)
7. [Déploiement](#déploiement)
8. [Variables d'Environnement](#variables-denvironnement)
9. [Guide de Contribution](#guide-de-contribution)

---

## 🎯 Vue d'Ensemble

**ideploy-examples** est un repository officiel de **Coolify** contenant une collection d'exemples et de templates pour déployer diverses applications et services en utilisant la plateforme Coolify.

### Objectif Principal
Fournir des exemples fonctionnels et prêts à déployer pour les développeurs souhaitant tester ou intégrer leurs applications avec Coolify.

### Technologie de Base
- **Coolify** : Plateforme open-source de déploiement et d'orchestration
- **Docker** : Containerization des applications
- **Nixpacks** : Alternative à Dockerfile pour le build
- **Docker Compose** : Orchestration multi-conteneurs

---

## 📁 Structure du Repository

```
ideploy-examples/
├── coolify.json                    # Configuration Coolify racine
├── README.md                       # Readme principal
├── LICENSE                         # Licence du projet
│
├── 🔵 FRAMEWORKS NODEJS/JavaScript
│ ├── nodejs/                       # Application Node.js simple (Fastify)
│ ├── nestjs/                       # Framework NestJS (TypeScript)
│ ├── nextjs/                       # Framework Next.js avec 3 variantes
│ │  ├── prisma/
│ │  ├── spa/
│ │  ├── spa-standalone/
│ │  ├── spa-with-image-optimization/
│ │  └── ssr/
│ ├── remix/                        # Framework Remix
│ ├── nuxt/                         # Framework Nuxt (Vue.js)
│ ├── t3-app/                       # Create T3 App (TypeScript Stack)
│ ├── t3-nextauth/                  # T3 App avec NextAuth
│ ├── turbo-nextjs/                 # Monorepo avec Turbo & Next.js
│ ├── turbo-t3-nextauth/            # Monorepo avec T3 Stack
│ ├── vite/                         # Vite + React
│ ├── vue/                          # Vue.js
│ ├── astro/                        # Astro (Static/SSR)
│ │  ├── server/
│ │  └── static/
│ └── bun/                          # Runtime Bun (TypeScript)
│
├── 🟢 FRAMEWORKS PYTHON
│ ├── flask/                        # Flask (Python Web)
│ │  ├── app.py
│ │  ├── requirements.txt
│ │  ├── static/
│ │  └── templates/
│
├── 🔴 FRAMEWORKS BACKEND
│ ├── laravel/                      # Laravel (PHP)
│ ├── laravel-inertia/              # Laravel + Inertia.js
│ ├── laravel-pure/                 # Laravel pur
│ ├── symfony/                      # Symfony (PHP)
│ ├── elixir-phoenix/               # Phoenix Framework (Elixir)
│ ├── rails-example/                # Ruby on Rails
│ ├── shopware6/                    # Shopware 6 (E-commerce)
│
├── 🟠 AUTRES LANGAGES
│ ├── rust/                         # Application Rust
│ └── go/                           # Application Go
│      └── gin/                     # Gin framework (Go)
│
├── 🐳 DOCKER & ORCHESTRATION
│ ├── docker-compose/               # Exemples Docker Compose complets
│ │  ├── docker-compose.yaml        # Configuration de base
│ │  ├── docker-compose-deep-parse.yaml
│ │  ├── docker-compose-test.yaml
│ │  ├── Dockerfile                 # Image personnalisée
│ │  ├── index.ts                   # Application TypeScript
│ │  ├── scripts/                   # Scripts utilitaires
│ │  └── package.json
│ ├── docker-compose-caddy/         # Docker Compose avec Caddy
│ │  ├── Caddyfile
│ │  └── docker-compose.yaml
│ └── docker-compose-test/          # Configurations de test
│      ├── docker-compose-cifs.yaml
│      ├── docker-compose-local-volumes.yaml
│      ├── docker-compose-parser.yaml
│      ├── docker-compose-raw.yaml
│      ├── docker-compose-shared-volume.yaml
│      ├── docker-compose-simple.yaml
│      ├── docker-compose-test-new-parser.yaml
│      ├── docker-compose-variable-volume.yaml
│      ├── docker-compose-volume-change.yaml
│      ├── docker-compose-volumes.yaml
│      ├── docker-compose-weird.yaml
│      ├── db/
│      └── empty/
│
├── dockerfile/                     # Exemples avancés Docker
│ ├── coolify.json
│ ├── Dockerfile
│ ├── apps/
│ └── packages/
│
├── static/                         # Contenu statique
└── strapi/                         # Strapi (CMS Headless)
```

---

## ⚙️ Configuration Coolify

### Fichier `coolify.json` - Structure Complète

```json
{
  "version": "1.0",
  "name": "test-app",
  "build": {
    "type": "nixpacks",
    "install_command": "npm install",
    "build_command": "npm run build",
    "start_command": "npm start"
  },
  "domains": {
    "ports_exposes": "3000"
  },
  "environment_variables": {
    "production": [
      {"key": "DB_PASSWORD", "value": "SERVICE_PASSWORD_64"},
      {"key": "APP_SECRET", "value": "SERVICE_BASE64_32"}
    ]
  }
}
```

### Paramètres Clés

| Paramètre | Type | Description |
|-----------|------|-------------|
| `version` | string | Version du format coolify.json |
| `name` | string | Nom de l'application |
| `build.type` | string | Type de build : `nixpacks` ou `dockerfile` |
| `build.install_command` | string | Commande pour installer les dépendances |
| `build.build_command` | string | Commande pour compiler/builder l'app |
| `build.start_command` | string | Commande de démarrage |
| `domains.ports_exposes` | string | Port(s) exposé(s) |
| `environment_variables` | object | Variables d'environnement par env |

### Types de Build Supportés

#### 1. **Nixpacks**
- Détection automatique du langage et framework
- Pas besoin de Dockerfile
- Léger et rapide

```json
"build": {
  "type": "nixpacks",
  "install_command": "npm install",
  "build_command": "npm run build",
  "start_command": "npm start"
}
```

#### 2. **Dockerfile**
- Contrôle total sur le processus de build
- Plus de flexibilité
- Plus verbeux

```json
"build": {
  "type": "dockerfile"
}
```

---

## 📦 Applications Supportées

### Applications Node.js / TypeScript

#### **1. Node.js Simple**
- **Chemin** : `nodejs/`
- **Framework** : Fastify
- **Description** : Application simple avec Fastify et CORS
- **Port** : 3000

#### **2. NestJS**
- **Chemin** : `nestjs/`
- **Type** : Backend TypeScript robuste
- **Description** : Framework full-featured pour API REST
- **Scripts** :
  - `npm run build` : Compilation
  - `npm run start` : Production
  - `npm run start:dev` : Développement
  - `npm run test` : Tests Jest

#### **3. Next.js**
- **Chemin** : `nextjs/`
- **Variantes** :
  - `prisma/` : Avec ORM Prisma
  - `spa/` : Single Page App
  - `spa-standalone/` : SPA autonome
  - `spa-with-image-optimization/` : SPA avec optimisation images
  - `ssr/` : Server-Side Rendering
- **Description** : Framework React complet

#### **4. Remix**
- **Chemin** : `remix/`
- **Type** : Framework React moderne
- **Description** : Full-stack React framework

#### **5. Nuxt**
- **Chemin** : `nuxt/`
- **Type** : Framework Vue.js
- **Description** : Vue.js SSR/SSG framework

#### **6. Vite**
- **Chemin** : `vite/`
- **Type** : Frontend tool
- **Description** : Build tool moderne pour React/Vue

#### **7. Vue.js**
- **Chemin** : `vue/`
- **Type** : Framework frontend
- **Description** : Application Vue.js

#### **8. Astro**
- **Chemin** : `astro/`
- **Variantes** :
  - `server/` : Astro avec rendu serveur
  - `static/` : Astro SSG
- **Description** : Static site generator moderne

#### **9. Create T3 App**
- **Chemin** : `t3-app/` et `t3-nextauth/`
- **Stack** : TypeScript + Next.js + Tailwind + Prisma + NextAuth
- **Description** : Full-stack opinioné TypeScript

#### **10. Turborepo**
- **Chemin** : `turbo-nextjs/` et `turbo-t3-nextauth/`
- **Type** : Monorepo management
- **Description** : Monorepo avec Turborepo

#### **11. Bun**
- **Chemin** : `bun/`
- **Type** : Runtime JavaScript alternatif
- **Description** : Application utilisant le runtime Bun
- **Features** :
  - TypeScript natif
  - Bundler intégré
  - Test runner intégré

### Applications Python

#### **Flask**
- **Chemin** : `flask/`
- **Description** : Framework web minimaliste
- **Structure** :
  - `app.py` : Application principale
  - `requirements.txt` : Dépendances Python
  - `templates/` : Templates HTML
  - `static/` : Fichiers statiques

### Applications PHP

#### **Laravel**
- **Chemin** : `laravel/`, `laravel-inertia/`, `laravel-pure/`
- **Variantes** :
  - `laravel/` : Laravel classique
  - `laravel-inertia/` : Avec Inertia.js
  - `laravel-pure/` : Laravel pur
- **Features** : ORM Eloquent, Migrations, Artisan CLI

#### **Symfony**
- **Chemin** : `symfony/`
- **Description** : Framework PHP complet et modulaire

### Autres Frameworks

#### **Elixir - Phoenix**
- **Chemin** : `elixir-phoenix/`
- **Type** : Backend Elixir
- **Description** : Framework web Elixir moderne

#### **Ruby on Rails**
- **Chemin** : `rails-example/`
- **Type** : Backend Ruby
- **Description** : Monolithic framework complet

#### **Shopware 6**
- **Chemin** : `shopware6/`
- **Type** : E-commerce
- **Description** : Plateforme e-commerce Shopware

#### **Strapi**
- **Chemin** : `strapi/`
- **Type** : CMS Headless
- **Description** : Headless CMS flexible basé sur Node.js

### Applications Compilées

#### **Rust**
- **Chemin** : `rust/`
- **Description** : Application compilée Rust

#### **Go**
- **Chemin** : `go/`
- **Sous-dossiers** :
  - `gin/` : Framework Gin pour Go
- **Description** : Application compilée Go

---

## 📚 Guide par Framework

### Node.js + Fastify (nodejs/)

```
nodejs/
├── index.js              # Point d'entrée
├── package.json          # Dépendances
├── README.md
└── coolify.json         # Configuration Coolify
```

**Configuration** :
```json
{
  "build": {
    "type": "nixpacks",
    "install_command": "npm install",
    "start_command": "node index.js"
  },
  "domains": {
    "ports_exposes": "3000"
  }
}
```

### NestJS (nestjs/)

```
nestjs/
├── src/                  # Code source
├── test/                 # Tests
├── package.json
├── tsconfig.json
├── nest-cli.json         # Configuration NestJS CLI
└── README.md
```

**Scripts Importants** :
- `npm run build` : Compilation TypeScript
- `npm run start:dev` : Mode développement avec reload
- `npm run start:prod` : Production optimisée
- `npm run test` : Jest tests

### Next.js (nextjs/)

**Variantes disponibles** :

1. **SSR (Server-Side Rendering)**
   ```
   ssr/
   ├── pages/
   ├── public/
   ├── package.json
   └── next.config.js
   ```

2. **SPA (Single Page App)**
   ```
   spa/
   ├── pages/
   ├── public/
   └── package.json
   ```

3. **Avec Prisma**
   ```
   prisma/
   ├── pages/
   ├── prisma/
   │  └── schema.prisma
   └── package.json
   ```

### Laravel (laravel/)

```
laravel/
├── app/                  # Code applicatif
├── config/               # Configuration
├── database/             # Migrations & seeders
├── routes/               # Routes
├── resources/            # Views & assets
├── storage/              # Fichiers générés
├── bootstrap/            # Bootstrap app
├── composer.json         # Dépendances PHP
├── artisan              # CLI Laravel
└── phpunit.xml          # Configuration tests
```

**Commandes Clés** :
```bash
php artisan migrate       # Exécuter migrations
php artisan serve        # Démarrer le serveur dev
php artisan tinker       # Shell interactif
composer install         # Installer dépendances
```

### Flask (flask/)

```
flask/
├── app.py               # Application Flask
├── requirements.txt     # Dépendances Python
├── templates/           # Templates Jinja2
├── static/              # Fichiers statiques (CSS, JS)
└── README.md
```

**Dépendances** :
```plaintext
flask
```

### Elixir + Phoenix (elixir-phoenix/)

```
elixir-phoenix/
├── lib/                 # Code applicatif
├── test/                # Tests
├── priv/                # Ressources
├── assets/              # Frontend assets
├── config/              # Configuration
├── mix.exs              # Dépendances Mix
└── README.md
```

---

## 🐳 Docker et Containerization

### Docker Compose - Structure

#### **docker-compose/**

Contient des configurations Docker Compose complètes :

```
docker-compose/
├── docker-compose.yaml         # Configuration de base
├── docker-compose-test.yaml    # Configuration de test
├── docker-compose-deep-parse.yaml
├── Dockerfile                  # Image personnalisée
├── index.ts                    # App TypeScript
├── package.json
├── tsconfig.json
└── scripts/                    # Scripts utilitaires
```

#### **Exemple : docker-compose.yaml**

```yaml
version: '3.8'
services:
  app:
    build: .
    ports:
      - "3000:3000"
    environment:
      - NODE_ENV=production
    volumes:
      - ./src:/app/src
```

### Docker Compose Test - Configurations Spécialisées

#### **docker-compose-test/**

Contient 11 variantes de configuration :

| Fichier | Objectif |
|---------|----------|
| `docker-compose-simple.yaml` | Configuration minimale |
| `docker-compose-volumes.yaml` | Gestion des volumes |
| `docker-compose-local-volumes.yaml` | Volumes locaux |
| `docker-compose-shared-volume.yaml` | Volumes partagés |
| `docker-compose-cifs.yaml` | Volumes CIFS/SMB |
| `docker-compose-variable-volume.yaml` | Volumes avec variables |
| `docker-compose-volume-change.yaml` | Changements de volumes |
| `docker-compose-parser.yaml` | Parsing configuration |
| `docker-compose-raw.yaml` | Configuration brute |
| `docker-compose-test-new-parser.yaml` | Nouveau parser |
| `docker-compose-weird.yaml` | Cas limites & edge cases |

### Docker Compose avec Caddy

#### **docker-compose-caddy/**

Intègre Caddy comme reverse proxy :

```
docker-compose-caddy/
├── docker-compose.yaml
├── Caddyfile           # Configuration Caddy
└── ...
```

**Caddyfile** : Configuration du reverse proxy Caddy

```
example.com {
  reverse_proxy localhost:3000
}
```

### Dockerfile Avancé

#### **dockerfile/**

Exemples avancés de Dockerfiles :

```
dockerfile/
├── Dockerfile          # Dockerfile principal
├── coolify.json       # Configuration Coolify
├── apps/              # Applications multi-conteneurs
└── packages/          # Packages/modules
```

---

## 🚀 Déploiement

### Processus de Déploiement Général

```
1. Code Push (Git)
    ↓
2. Coolify détecte changement
    ↓
3. Build (Nixpacks ou Dockerfile)
    ↓
4. Tests (optionnel)
    ↓
5. Image Docker création
    ↓
6. Container déploiement
    ↓
7. Health check
    ↓
8. Application accessible
```

### Configuration Minimale pour Déployer

#### Étape 1 : coolify.json

```json
{
  "version": "1.0",
  "name": "mon-app",
  "build": {
    "type": "nixpacks"
  },
  "domains": {
    "ports_exposes": "3000"
  }
}
```

#### Étape 2 : Package.json (Node.js)

```json
{
  "scripts": {
    "start": "node index.js",
    "build": "echo 'Build complete'"
  }
}
```

### Ports et Domaines

```json
"domains": {
  "ports_exposes": "3000"       // Single port
  // ou
  "ports_exposes": "3000,8080"  // Multiple ports
}
```

### Health Checks

Coolify effectue des vérifications de santé :
- HTTP requests sur les ports exposés
- Vérification de la réponse 200 OK
- Timeout configurable

---

## 🔐 Variables d'Environnement

### Configuration dans coolify.json

```json
{
  "environment_variables": {
    "production": [
      {
        "key": "DATABASE_URL",
        "value": "SERVICE_DATABASE_URL"
      },
      {
        "key": "APP_SECRET",
        "value": "SERVICE_BASE64_32"
      }
    ],
    "development": [
      {
        "key": "DEBUG",
        "value": "true"
      }
    ]
  }
}
```

### Variables Spéciales de Coolify

| Variable | Type | Description |
|----------|------|-------------|
| `SERVICE_PASSWORD_64` | string | Mot de passe encodé en base64 |
| `SERVICE_BASE64_32` | string | String aléatoire base64 (32 chars) |
| `SERVICE_DATABASE_URL` | string | URL de base de données générée |
| `SERVICE_*` | string | Services liés |

### Accès aux Variables dans l'Application

#### Node.js
```javascript
const dbUrl = process.env.DATABASE_URL;
const secret = process.env.APP_SECRET;
```

#### Python
```python
import os
db_url = os.getenv('DATABASE_URL')
secret = os.getenv('APP_SECRET')
```

#### PHP / Laravel
```php
$dbUrl = env('DATABASE_URL');
$secret = env('APP_SECRET');
```

---

## 📋 Cas d'Usage Typiques

### 1. Déployer un API Node.js

1. Copier `nodejs/` comme base
2. Modifier `index.js` avec votre logique
3. Ajouter dépendances à `package.json`
4. Configurer `coolify.json`
5. Push vers Git
6. Coolify détecte et déploie

### 2. Déployer un Full-Stack Next.js

1. Utiliser `nextjs/ssr/` comme template
2. Créer pages dans `pages/`
3. Ajouter Prisma si base de données
4. Configurer variables d'environnement
5. Déployer via Coolify

### 3. Déployer une API Laravel

1. Utiliser `laravel/` comme base
2. Créer controllers et models
3. Configurer base de données dans `.env`
4. Exécuter migrations : `php artisan migrate`
5. Déployer

### 4. Déployer Docker Compose Multi-Services

1. Utiliser `docker-compose/` comme base
2. Configurer services dans `docker-compose.yaml`
3. Définir volumes et networks
4. Coolify exécute `docker-compose up`
5. Services accessible via domaines

---

## 🔧 Installation et Utilisation Locale

### Prérequis

- Git
- Docker & Docker Compose
- Node.js 18+ (pour Node.js apps)
- Python 3.8+ (pour Flask)
- PHP 8.1+ (pour Laravel)
- Docker (pour tous)

### Utilisation Générale

```bash
# Cloner le repository
git clone https://github.com/coollabs/ideploy-examples.git
cd ideploy-examples

# Entrer dans le dossier de l'app
cd nodejs

# Installer dépendances
npm install

# Démarrer localement
npm start
```

### Utilisation avec Docker

```bash
cd docker-compose

# Afficher les services
docker-compose config

# Démarrer les services
docker-compose up

# Voir les logs
docker-compose logs -f

# Arrêter les services
docker-compose down
```

---

## 🌍 Exemples de Production

### Configuration Production - Node.js

```json
{
  "version": "1.0",
  "name": "api-production",
  "build": {
    "type": "nixpacks",
    "install_command": "npm install --production",
    "build_command": "npm run build",
    "start_command": "npm run start:prod"
  },
  "domains": {
    "ports_exposes": "3000"
  },
  "environment_variables": {
    "production": [
      {
        "key": "NODE_ENV",
        "value": "production"
      },
      {
        "key": "LOG_LEVEL",
        "value": "error"
      },
      {
        "key": "DATABASE_URL",
        "value": "SERVICE_DATABASE_URL"
      }
    ]
  }
}
```

### Configuration Production - Laravel

```json
{
  "version": "1.0",
  "name": "laravel-production",
  "build": {
    "type": "nixpacks",
    "install_command": "composer install --no-dev",
    "build_command": "php artisan optimize",
    "start_command": "php artisan serve"
  },
  "domains": {
    "ports_exposes": "8000"
  },
  "environment_variables": {
    "production": [
      {
        "key": "APP_ENV",
        "value": "production"
      },
      {
        "key": "APP_DEBUG",
        "value": "false"
      },
      {
        "key": "APP_KEY",
        "value": "SERVICE_BASE64_32"
      }
    ]
  }
}
```

---

## 📖 Lexique et Concepts

| Terme | Explication |
|-------|-------------|
| **Coolify** | Plateforme de déploiement open-source |
| **Nixpacks** | Build system qui détecte framework automatiquement |
| **Docker** | Containerization technology |
| **Docker Compose** | Orchestration multi-conteneurs |
| **Framework** | Structure de développement |
| **SSR** | Server-Side Rendering |
| **SPA** | Single Page Application |
| **ORM** | Object-Relational Mapping |
| **Headless CMS** | CMS sans frontend intégré |
| **Monorepo** | Repository avec plusieurs projets |
| **Health Check** | Vérification que l'app fonctionne |
| **Reverse Proxy** | Proxy qui redirige requêtes |

---

## 📚 Ressources Supplémentaires

### Documentation Officielle
- [Coolify Docs](https://coolify.io/docs)
- [Nixpacks Docs](https://nixpacks.com)
- [Docker Docs](https://docs.docker.com)

### Frameworks
- [Next.js](https://nextjs.org)
- [NestJS](https://nestjs.com)
- [Laravel](https://laravel.com)
- [Flask](https://flask.palletsprojects.com)

### Outils
- [Docker Compose](https://docs.docker.com/compose)
- [Caddy](https://caddyserver.com)
- [Prisma ORM](https://www.prisma.io)

---

## 🤝 Guide de Contribution

### Ajouter un Nouvel Exemple

1. **Créer un dossier** : `mkdir my-framework`
2. **Ajouter coolify.json** :
```json
{
  "version": "1.0",
  "name": "my-app",
  "build": {
    "type": "nixpacks"
  }
}
```

3. **Ajouter README.md** avec instructions
4. **Tester localement** avec Coolify
5. **Créer Pull Request**

### Standards

- ✅ Chaque exemple doit fonctionner indépendamment
- ✅ Inclure un `README.md` explicatif
- ✅ Inclure `coolify.json` valide
- ✅ Exclure `node_modules`, `vendor`, etc. (.gitignore)
- ✅ Utiliser les meilleures pratiques du framework
- ✅ Tester sur une instance Coolify

---

## 📝 License

Voir le fichier [LICENSE](./LICENSE) dans le repository.

---

**Dernière mise à jour** : Janvier 2026  
**Version** : 1.0  
**Repository** : [ideploy-examples](https://github.com/coollabs/ideploy-examples)

