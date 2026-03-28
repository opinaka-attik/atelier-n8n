# 00 — Installation de n8n

## Prérequis

- Docker Desktop (Windows/Mac) ou Docker Engine (Linux)
- Docker Compose v2+
- 2 Go de RAM minimum
- Ports disponibles : `5678`

---

## 🚀 Installation rapide (Docker Compose)

```bash
# Cloner le repo
git clone https://github.com/opinaka-attik/atelier-n8n
cd atelier-n8n/docker

# Lancer n8n
docker compose up -d

# Vérifier que le container tourne
docker ps
```

Ouvrir **http://localhost:5678** dans le navigateur.

Premier lancement : n8n demande de créer un compte admin local.

---

## ⚙️ Variables d'environnement importantes

| Variable | Défaut | Description |
|----------|--------|-------------|
| `N8N_HOST` | `localhost` | Hôte d'écoute |
| `N8N_PORT` | `5678` | Port HTTP |
| `WEBHOOK_URL` | `http://localhost:5678/` | URL de base pour les webhooks |
| `GENERIC_TIMEZONE` | `Europe/Paris` | Fuseau horaire des schedules |
| `N8N_BASIC_AUTH_ACTIVE` | `true` | Activer l'auth basique |

---

## 🔑 Configurer Groq (pour les modules AI)

1. Créer un compte sur [console.groq.com](https://console.groq.com)
2. Générer une clé API
3. Dans n8n : **Settings → Credentials → Add credential**
4. Chercher **HTTP Header Auth**
5. Nom : `Groq API`, Header : `Authorization`, Value : `Bearer VOTRE_CLE`

---

## 📦 Importer un workflow

1. Ouvrir n8n → **Workflows** → bouton **+**
2. Cliquer **Import from file**
3. Sélectionner un fichier `.json` du dossier `workflows/`
4. Cliquer **Save** puis activer le toggle en haut à droite

---

## 🔄 Commandes utiles

```bash
# Arrêter n8n
docker compose down

# Voir les logs
docker compose logs -f n8n

# Mettre à jour l'image
docker compose pull && docker compose up -d

# Sauvegarder les données
docker cp n8n:/home/node/.n8n ./backup-n8n
```
