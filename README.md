# iDeploy Examples

<div align="center">

[![License](https://img.shields.io/badge/License-MIT-blue.svg)](LICENSE)
[![GitHub Stars](https://img.shields.io/github/stars/Idem-AI/ideploy-examples.svg)](https://github.com/Idem-AI/ideploy-examples)
[![GitHub Forks](https://img.shields.io/github/forks/Idem-AI/ideploy-examples.svg)](https://github.com/Idem-AI/ideploy-examples)

**Une collection complète d'exemples et de templates prêts à déployer avec iDeploy**

[Documentation](#documentation) • [Quick Start](#quick-start) • [Frameworks Supportés](#frameworks-supportés) • [Contribution](#contribution)

</div>

---

## 📌 À Propos

**iDeploy Examples** est un repository officiel contenant une collection curatée d'exemples fonctionnels et de templates de déploiement pour diverses applications, frameworks et services. Chaque exemple est optimisé pour fonctionner de manière transparente avec la plateforme **iDeploy**.

Ce repository est conçu pour :
- ✅ Fournir des points de départ rapides pour vos projets
- ✅ Démontrer les meilleures pratiques de déploiement
- ✅ Supporter une large gamme de technologies et frameworks
- ✅ Faciliter l'intégration continue et le déploiement automatisé

### À Propos d'iDeploy

**iDeploy** est une plateforme de déploiement open-source et auto-hébergée qui simplifie le processus de mise en production de vos applications. Elle combine la puissance de Docker, la détection automatique des frameworks via Nixpacks, et une interface intuitive pour un déploiement sans friction.

**Caractéristiques principales** :
- 🚀 Déploiements rapides et fiables
- 🐳 Support natif de Docker et Docker Compose
- 🔄 Intégration Git (webhooks automatiques)
- 🔐 Variables d'environnement sécurisées
- 📊 Monitoring et logs en temps réel
- 🌐 Support multi-domaines
- 🔒 SSL/TLS automatique avec Caddy

---

## 🚀 Quick Start

### Installation d'iDeploy

```bash
# Cloner le repository iDeploy
git clone https://github.com/Idem-AI/ideploy.git
cd ideploy

# Installation avec Docker
docker-compose up -d

# Accéder à l'interface
open http://localhost:3000
```

### Déployer un Exemple

1. **Cloner ce repository** :
```bash
git clone https://github.com/Idem-AI/ideploy-examples.git
cd ideploy-examples
```

2. **Choisir votre application** :
```bash
# Exemple : Node.js avec Fastify
cd nodejs
npm install
npm start
```

3. **Configurer dans iDeploy** :
   - Connecter votre repository Git
   - iDeploy détecte automatiquement le type d'application
   - Configurer les variables d'environnement
   - Cliquer sur "Deploy"

4. **Accéder à votre application** :
```
https://votre-app.votre-domaine.com
```

---

## 📚 Documentation

### Structure du Repository

Ce repository contient **30+** exemples d'applications et services organisés par catégorie :

```
ideploy-examples/
├── 🔵 JavaScript / Node.js
│   ├── nodejs/                # Node.js + Fastify
│   ├── nestjs/                # NestJS (Backend TypeScript)
│   ├── nextjs/                # Next.js (React Full-Stack)
│   ├── remix/                 # Remix (Full-Stack React)
│   ├── nuxt/                  # Nuxt (Vue.js SSR)
│   ├── vite/                  # Vite (Build Tool)
│   ├── vue/                   # Vue.js
│   ├── astro/                 # Astro (Static Site Generator)
│   ├── bun/                   # Bun Runtime
│   ├── t3-app/                # T3 Stack (TypeScript Full-Stack)
│   ├── t3-nextauth/           # T3 + NextAuth
│   ├── turbo-nextjs/          # Turborepo + Next.js
│   ├── turbo-t3-nextauth/     # Turborepo + T3 Stack
│   └── adonisjs/              # AdonisJS
│
├── 🟢 Python
│   └── flask/                 # Flask Web Framework
│
├── 🔴 PHP
│   ├── laravel/               # Laravel
│   ├── laravel-inertia/       # Laravel + Inertia.js
│   ├── laravel-pure/          # Laravel (Pur)
│   └── symfony/               # Symfony
│
├── 🟠 Autres Langages
│   ├── rust/                  # Rust
│   ├── go/                    # Go
│   ├── elixir-phoenix/        # Elixir + Phoenix
│   └── rails-example/         # Ruby on Rails
│
├── 🐳 Services
│   ├── docker-compose/        # Exemples Docker Compose
│   ├── docker-compose-caddy/  # Docker Compose + Caddy
│   ├── docker-compose-test/   # Configurations de test
│   ├── dockerfile/            # Exemples Dockerfile avancés
│   ├── shopware6/             # Shopware 6 (E-commerce)
│   ├── strapi/                # Strapi (CMS Headless)
│   └── static/                # Contenu statique
```

### Configuration ideploy.json

Chaque application inclut un fichier `ideploy.json` qui définit comment la déployer :

```json
{
  "version": "1.0",
  "name": "mon-app",
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
      {"key": "NODE_ENV", "value": "production"},
      {"key": "DATABASE_URL", "value": "SERVICE_DATABASE_URL"}
    ]
  }
}
```

**Paramètres clés** :

| Clé | Type | Description |
|-----|------|-------------|
| `version` | string | Version du format ideploy.json |
| `name` | string | Nom unique de l'application |
| `build.type` | string | `nixpacks` (détection auto) ou `dockerfile` |
| `build.install_command` | string | Commande d'installation |
| `build.build_command` | string | Commande de compilation |
| `build.start_command` | string | Commande de démarrage |
| `domains.ports_exposes` | string | Ports exposés (ex: "3000" ou "3000,8080") |
| `environment_variables` | object | Variables d'env par environnement |

### Types de Build Supportés

#### 1. **Nixpacks** (Recommandé)
Détection automatique du langage et du framework - pas besoin de Dockerfile :

```json
{
  "build": {
    "type": "nixpacks",
    "install_command": "npm install",
    "build_command": "npm run build",
    "start_command": "npm start"
  }
}
```

#### 2. **Dockerfile**
Contrôle total sur le processus de build :

```json
{
  "build": {
    "type": "dockerfile"
  }
}
```

---

## 🎯 Frameworks Supportés

### JavaScript / TypeScript / Node.js

#### Node.js (Fastify)
- **Chemin** : `nodejs/`
- **Description** : Application simple avec Fastify et CORS
- **Port** : 3000
- **Utilisation** :
```bash
cd nodejs
npm install && npm start
```

#### NestJS
- **Chemin** : `nestjs/`
- **Description** : Framework backend TypeScript robuste pour APIs REST
- **Port** : 3000
- **Scripts** :
  - `npm run build` - Compilation TypeScript
  - `npm run start` - Production
  - `npm run start:dev` - Développement avec hot-reload
  - `npm run test` - Tests Jest

#### Next.js
- **Chemin** : `nextjs/`
- **Variantes** :
  - `ssr/` - Server-Side Rendering
  - `spa/` - Single Page Application
  - `spa-with-image-optimization/` - SPA avec optimisation d'images
  - `prisma/` - Avec ORM Prisma
- **Description** : Framework React complet pour applications full-stack
- **Port** : 3000

#### Remix
- **Chemin** : `remix/`
- **Description** : Framework React moderne avec support Server Components
- **Port** : 3000

#### Nuxt
- **Chemin** : `nuxt/`
- **Description** : Framework Vue.js pour applications SSR/SSG
- **Port** : 3000

#### Vue.js
- **Chemin** : `vue/`
- **Description** : Application Vue.js pure
- **Port** : 5173

#### Vite
- **Chemin** : `vite/`
- **Description** : Build tool moderne pour React/Vue
- **Port** : 5173

#### Astro
- **Chemin** : `astro/`
- **Variantes** :
  - `static/` - Static Site Generation
  - `server/` - Server-Side Rendering
- **Description** : Static site generator moderne
- **Port** : 3000

#### Bun
- **Chemin** : `bun/`
- **Description** : Application utilisant le runtime Bun (TypeScript natif)
- **Port** : 3000
- **Features** :
  - TypeScript natif
  - Bundler intégré
  - Test runner intégré

#### Create T3 App (T3 Stack)
- **Chemin** : `t3-app/`, `t3-nextauth/`
- **Stack** : TypeScript + Next.js + Tailwind CSS + Prisma + NextAuth
- **Description** : Full-stack TypeScript opinioné
- **Port** : 3000

#### Turborepo
- **Chemin** : `turbo-nextjs/`, `turbo-t3-nextauth/`
- **Description** : Monorepos avec build caching haute-performance
- **Port** : 3000

#### AdonisJS
- **Chemin** : `adonisjs/`
- **Description** : Framework Node.js full-featured avec ORM intégré
- **Port** : 3333

### Python

#### Flask
- **Chemin** : `flask/`
- **Description** : Framework web minimaliste et flexible
- **Port** : 5000
- **Structure** :
```
flask/
├── app.py                # Application principale
├── requirements.txt      # Dépendances
├── templates/            # Templates Jinja2
└── static/               # CSS, JS, images
```

### PHP

#### Laravel
- **Chemin** : `laravel/`, `laravel-inertia/`, `laravel-pure/`
- **Variantes** :
  - `laravel/` - Configuration standard
  - `laravel-inertia/` - Avec Inertia.js
  - `laravel-pure/` - Pur Laravel
- **Description** : Framework PHP moderne avec ORM Eloquent
- **Port** : 8000
- **Features** : Migrations, Seeders, Artisan CLI

#### Symfony
- **Chemin** : `symfony/`
- **Description** : Framework PHP complet et modulaire
- **Port** : 8000

### Autres Langages

#### Rust
- **Chemin** : `rust/`
- **Description** : Application compilée Rust
- **Port** : 8080

#### Go
- **Chemin** : `go/`, `go/gin/`
- **Description** : Application Go avec framework Gin
- **Port** : 8080

#### Elixir + Phoenix
- **Chemin** : `elixir-phoenix/`
- **Description** : Framework web Elixir moderne avec LiveView
- **Port** : 4000
- **Structure** :
```
elixir-phoenix/
├── lib/          # Code applicatif
├── test/         # Tests
├── assets/       # Frontend assets
├── config/       # Configuration
└── mix.exs       # Dépendances Mix
```

#### Ruby on Rails
- **Chemin** : `rails-example/`
- **Description** : Framework Ruby complet et monolithique
- **Port** : 3000

### Services et CMS

#### Shopware 6
- **Chemin** : `shopware6/`
- **Type** : E-commerce
- **Description** : Plateforme e-commerce open-source
- **Port** : 8000

#### Strapi
- **Chemin** : `strapi/`
- **Type** : CMS Headless
- **Description** : CMS flexible basé sur Node.js
- **Port** : 1337

---

## 🐳 Docker et Docker Compose

### Exemples Docker Compose

#### docker-compose/
Configuration de base pour applications multi-conteneurs :

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
      - ./data:/app/data
```

#### docker-compose-caddy/
Docker Compose avec Caddy comme reverse proxy :

```yaml
version: '3.8'
services:
  caddy:
    image: caddy:latest
    ports:
      - "80:80"
      - "443:443"
    volumes:
      - ./Caddyfile:/etc/caddy/Caddyfile
  
  app:
    build: .
    expose:
      - "3000"
```

#### docker-compose-test/
Configurations spécialisées pour testing :

- `docker-compose-simple.yaml` - Configuration minimale
- `docker-compose-volumes.yaml` - Gestion des volumes
- `docker-compose-cifs.yaml` - Volumes CIFS/SMB
- `docker-compose-parser.yaml` - Parsing configuration
- Et plus...

### Dockerfile Avancé

**dockerfile/** contient des exemples avancés :

```dockerfile
FROM node:18-alpine

WORKDIR /app

COPY package*.json ./
RUN npm install

COPY . .
RUN npm run build

EXPOSE 3000
CMD ["npm", "start"]
```

---

## ⚙️ Configuration Avancée

### Variables d'Environnement

Définir les variables dans `ideploy.json` :

```json
{
  "environment_variables": {
    "production": [
      {
        "key": "NODE_ENV",
        "value": "production"
      },
      {
        "key": "DATABASE_URL",
        "value": "SERVICE_DATABASE_URL"
      },
      {
        "key": "API_SECRET",
        "value": "SERVICE_BASE64_32"
      }
    ]
  }
}
```

### Variables Spéciales iDeploy

| Variable | Description |
|----------|-------------|
| `SERVICE_DATABASE_URL` | URL de base de données générée |
| `SERVICE_PASSWORD_64` | Mot de passe encodé base64 |
| `SERVICE_BASE64_32` | String aléatoire base64 (32 chars) |
| `SERVICE_*` | Services liés |

### Accès aux Variables

**Node.js / JavaScript** :
```javascript
const dbUrl = process.env.DATABASE_URL;
const secret = process.env.API_SECRET;
```

**Python** :
```python
import os
db_url = os.getenv('DATABASE_URL')
secret = os.getenv('API_SECRET')
```

**PHP / Laravel** :
```php
$dbUrl = env('DATABASE_URL');
$secret = env('API_SECRET');
```

---

## 📋 Cas d'Usage

### 1. API Node.js Simple

```bash
cd nodejs
npm install
npm start
```

### 2. Application Full-Stack Next.js

```bash
cd nextjs/ssr
npm install
npm run build
npm start
```

### 3. Backend Laravel avec Base de Données

```bash
cd laravel
composer install
php artisan migrate
php artisan serve
```

### 4. Microservices Docker Compose

```bash
cd docker-compose
docker-compose up -d
```

---

## 🔧 Installation Locale

### Prérequis

- **Git** : Contrôle de version
- **Docker & Docker Compose** : Containerization
- **Node.js 18+** : Pour les applications JavaScript
- **Python 3.8+** : Pour Flask
- **PHP 8.1+** : Pour Laravel
- **Ruby 3.0+** : Pour Rails

### Installation de Base

```bash
# Cloner le repository
git clone https://github.com/Idem-AI/ideploy-examples.git
cd ideploy-examples

# Entrer dans le dossier de l'application
cd nodejs

# Installer les dépendances
npm install

# Démarrer localement
npm start
```

### Utilisation avec Docker

```bash
cd docker-compose

# Voir la configuration
docker-compose config

# Démarrer les services
docker-compose up -d

# Voir les logs
docker-compose logs -f

# Arrêter les services
docker-compose down
```

---

## 🚀 Déploiement sur iDeploy

### Étape 1 : Préparer votre Application

```bash
# Cloner et modifier
git clone https://github.com/Idem-AI/ideploy-examples.git
cd ideploy-examples/nodejs

# Customizer selon vos besoins
# Mettre à jour package.json, ideploy.json, etc.
```

### Étape 2 : Configurer iDeploy

1. **Accéder à iDeploy** : `http://localhost:3000`
2. **Créer une nouvelle application**
3. **Connecter votre repository Git**
4. **iDeploy détecte automatiquement** le type d'application
5. **Configurer les variables d'environnement**
6. **Cliquer sur "Deploy"**

### Étape 3 : Accéder à l'Application

```
https://votre-app.votre-domaine.com
```

### Processus de Déploiement

```
Code Push (Git)
    ↓
iDeploy détecte changement
    ↓
Build (Nixpacks ou Dockerfile)
    ↓
Tests (optionnel)
    ↓
Image Docker création
    ↓
Container déploiement
    ↓
Health check
    ↓
Application accessible 🎉
```

---

## 🤝 Contribution

Nous accueillons les contributions ! Que ce soit des bug fixes, nouvelles applications ou améliorations, votre aide est bienvenue.

### Ajouter un Nouvel Exemple

1. **Créer un dossier** pour votre application :
```bash
mkdir mon-framework
cd mon-framework
```

2. **Créer `ideploy.json`** :
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

3. **Ajouter `README.md`** avec instructions :
```markdown
# Mon Application

## Description
...

## Installation
npm install

## Démarrage
npm start
```

4. **Tester localement** avec iDeploy
5. **Créer une Pull Request**

### Standards de Qualité

- ✅ Chaque exemple doit fonctionner indépendamment
- ✅ Inclure un `README.md` détaillé
- ✅ Inclure un `ideploy.json` valide
- ✅ Exclure fichiers de build (`node_modules`, `vendor`, etc.)
- ✅ Utiliser les meilleures pratiques du framework
- ✅ Tester sur une instance iDeploy

### Pull Request

```bash
# Fork le repository
# Créer une branche
git checkout -b feature/mon-exemple

# Committer vos changements
git commit -am 'Add: Mon nouvel exemple'

# Pusher vers votre fork
git push origin feature/mon-exemple

# Créer une Pull Request sur GitHub
```

---

## 📖 Ressources

### Documentation Officielle
- 📘 [iDeploy Documentation](https://ideploy.ai/docs)
- 🔧 [Nixpacks](https://nixpacks.com)
- 🐳 [Docker Documentation](https://docs.docker.com)

### Frameworks & Technologies
- ⚛️ [Next.js](https://nextjs.org)
- 🏗️ [NestJS](https://nestjs.com)
- 🚀 [Laravel](https://laravel.com)
- 🐍 [Flask](https://flask.palletsprojects.com)
- 📦 [Docker Compose](https://docs.docker.com/compose)

### Outils Recommandés
- 🔐 [Caddy Web Server](https://caddyserver.com)
- 🗄️ [Prisma ORM](https://www.prisma.io)
- 🔄 [GitHub Actions](https://github.com/features/actions)

---

## 📜 License

Ce repository est sous licence **MIT**. Voir [LICENSE](LICENSE) pour plus de détails.

---

## 🙋 Support

- 💬 [GitHub Discussions](https://github.com/Idem-AI/ideploy-examples/discussions)
- 🐛 [Signaler un Bug](https://github.com/Idem-AI/ideploy-examples/issues)
- 📧 [Contact](mailto:support@ideploy.ai)

---

## 🌟 Remerciements

Merci à tous les contributeurs qui rendent ce projet possible !

<div align="center">

**[⬆ Retour en haut](#ideploy-examples)**

Fabriqué avec ❤️ par la [communauté iDeploy](https://ideploy.ai)

</div>
