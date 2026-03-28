# 🔧 Atelier n8n — Workflows de démonstration

Atelier pratique pour découvrir **n8n** à travers des workflows JSON progressifs.

## 🗂️ Structure

```
atelier-n8n/
├── workflows/          # Fichiers JSON importables dans n8n
│   ├── 01_hello_webhook.json
│   ├── 02_http_request.json
│   ├── 03_condition_switch.json
│   ├── 04_ai_summarizer.json
│   └── 05_data_pipeline.json
├── docker/
│   └── docker-compose.yml
└── README.md
```

## 🚀 Démarrage rapide

```bash
git clone https://github.com/opinaka-attik/atelier-n8n
cd atelier-n8n/docker
docker compose up -d
# Ouvrir http://localhost:5678
```

## 📦 Importer un workflow

1. Ouvrir n8n → **Workflows** → **Import from file**
2. Sélectionner un fichier `.json` du dossier `workflows/`
3. Activer le workflow et tester

## 📚 Modules

| # | Fichier | Niveau | Concept |
|---|---------|--------|---------|
| 01 | `01_hello_webhook.json` | Débutant | Webhook + réponse HTTP |
| 02 | `02_http_request.json` | Débutant | Appel API externe (wttr.in météo) |
| 03 | `03_condition_switch.json` | Intermédiaire | IF/Switch + routage conditionnel |
| 04 | `04_ai_summarizer.json` | Intermédiaire | Nœud AI + résumé de texte (Groq) |
| 05 | `05_data_pipeline.json` | Avancé | Pipeline de données : fetch → transform → output |

## ⚙️ Prérequis

- Docker + Docker Compose
- Compte [Groq](https://console.groq.com) (gratuit) pour les modules AI
