# TP 1 - Deploiement d'une application fullstack

## Objectif

Deployer une application web (React + Node.js) sur un serveur Linux avec **Nginx** et **PM2**.

- Le **frontend** sera accessible sur `votre-domaine.com`
- L'**API** sera accessible sur `api.votre-domaine.com`

## Le projet

Une application de gestion de taches composee de :

- `front/` — Application React (Vite) qui affiche et gere les taches
- `back/` — API Express qui stocke les taches dans un fichier JSON

### Lancer le projet en local

```bash
# Terminal 1 - Backend
cd back
npm install
npm start

# Terminal 2 - Frontend
cd front
npm install
npm run dev
```

Le front tourne sur `http://localhost:5173` et appelle l'API sur `http://localhost:3000`.

## Etapes du TP

### 1. Mettre le projet sur votre GitHub

Ce repository contient le frontend et le backend ensemble. A vous de creer **deux repositories separes** sur votre compte GitHub :

- Un repository pour le **frontend** (contenu du dossier `front/`)
- Un repository pour le **backend** (contenu du dossier `back/`)

### 2. Preparer le serveur

Connectez-vous a votre serveur en SSH et installez les outils necessaires :

- **Node.js** (v20)
- **PM2** (gestionnaire de processus Node)
- **Nginx** (serveur web)

### 3. Cloner et lancer le backend

- Clonez votre repository sur le serveur
- Installez les dependances du backend
- Lancez le backend avec **PM2** (pas avec `npm start` directement)
- Verifiez que l'API repond sur le port 3000

### 4. Build le frontend

- Installez les dependances du frontend
- **Avant de build** : modifiez les appels API dans le code React pour pointer vers `https://api.votre-domaine.com` au lieu de `/tasks`
- Buildez le frontend (`npm run build`)
- Le resultat se trouve dans le dossier `dist/`

### 5. Configurer Nginx pour le frontend

Creez un fichier de configuration Nginx pour servir le frontend :

- Le site doit etre accessible sur `votre-domaine.com`
- Nginx doit servir les fichiers statiques du dossier `dist/`

N'oubliez pas d'activer le site et de recharger Nginx.

### 6. Configurer Nginx pour l'API

Creez un **deuxieme fichier** de configuration Nginx pour l'API :

- L'API doit etre accessible sur `api.votre-domaine.com`
- Nginx doit rediriger les requetes vers le port ou tourne votre backend
- Pensez a configurer le **DNS** (quel type d'enregistrement pour un sous-domaine ?)

### 7. Verifier

- [ ] Le frontend s'affiche sur `votre-domaine.com`
- [ ] Vous pouvez ajouter une tache
- [ ] Vous pouvez cocher/decocher une tache
- [ ] Vous pouvez supprimer une tache
- [ ] Les taches persistent apres un rafraichissement de la page

## Indices

- `pm2 start` permet de lancer un processus en arriere-plan
- `pm2 list` pour voir les processus en cours
- Les fichiers de config Nginx vont dans `/etc/nginx/sites-available/`
- `proxy_pass` est la directive Nginx pour rediriger vers un autre serveur

## Pour aller plus loin

- Configurez PM2 pour redemarrer automatiquement au reboot du serveur (`pm2 startup`)
- Mettez en place HTTPS avec **Let's Encrypt** (`certbot`)
