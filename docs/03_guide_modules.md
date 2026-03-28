# 03 — Guide des modules

## Module 01 — Hello Webhook
**Fichier** : `workflows/01_hello_webhook.json`  
**Niveau** : Débutant | **Durée** : 10 min

### Objectif
Créer un endpoint HTTP qui répond avec un message JSON dynamique.

### Pipeline
```
Webhook (GET /hello) → Respond to Webhook
```

### Test
```bash
# Activer le workflow puis :
curl "http://localhost:5678/webhook/hello?nom=Alice"
```

### Résultat attendu
```json
{ "message": "Bonjour depuis n8n !", "timestamp": "2026-03-28T..." }
```

---

## Module 02 — HTTP Request Météo
**Fichier** : `workflows/02_http_request.json`  
**Niveau** : Débutant | **Durée** : 15 min

### Objectif
Récupérer la météo réelle de Montpellier via `wttr.in` et extraire les données utiles.

### Pipeline
```
Schedule (1h) → HTTP Request (wttr.in) → Code (extraire JSON)
```

### Concepts appris
- Nœud **Schedule Trigger** : déclenchement périodique
- Nœud **HTTP Request** : appel API GET
- Nœud **Code** : extraction et transformation JSON

### Test manuel
Cliquer **Execute workflow** pour lancer sans attendre le schedule.

### Résultat attendu (dans le nœud Code)
```json
{
  "ville": "Montpellier",
  "temperature_c": "18",
  "ressenti_c": "17",
  "humidite": "65",
  "description": "Partly cloudy",
  "timestamp": "2026-03-28T..."
}
```

---

## Module 03 — Condition & Switch
**Fichier** : `workflows/03_condition_switch.json`  
**Niveau** : Intermédiaire | **Durée** : 20 min

### Objectif
Router une demande selon un score : admis (>70) ou refusé.

### Pipeline
```
Webhook (POST /classify) → IF (score > 70) → Réponse Admis
                                           → Réponse Refusé
```

### Test
```bash
# Cas admis
curl -X POST http://localhost:5678/webhook/classify \
  -H "Content-Type: application/json" \
  -d '{"score": 85}'

# Cas refusé
curl -X POST http://localhost:5678/webhook/classify \
  -H "Content-Type: application/json" \
  -d '{"score": 45}'
```

---

## Module 04 — AI Summarizer (Groq)
**Fichier** : `workflows/04_ai_summarizer.json`  
**Niveau** : Intermédiaire | **Durée** : 25 min

### Prérequis
Remplacer `YOUR_GROQ_API_KEY` dans le nœud **Groq LLM** par votre clé Groq.

### Objectif
Exposer un endpoint POST qui résume n'importe quel texte via Groq llama3.

### Pipeline
```
Webhook (POST /summarize) → HTTP Request (Groq API) → Code (extraire) → Réponse
```

### Test
```bash
curl -X POST http://localhost:5678/webhook/summarize \
  -H "Content-Type: application/json" \
  -d '{"texte": "n8n est une plateforme open-source d automatisation de workflows. Elle permet de connecter des centaines de services sans coder, ou avec du JavaScript pour les cas avancés. Elle peut être self-hostée sur Docker."}'  
```

### Résultat attendu
```json
{
  "resume": "n8n est une plateforme open-source...",
  "tokens": 142
}
```

---

## Module 05 — Data Pipeline
**Fichier** : `workflows/05_data_pipeline.json`  
**Niveau** : Avancé | **Durée** : 30 min

### Objectif
Fetcher des données JSON, les filtrer, les transformer, puis agréger des statistiques.

### Pipeline
```
Schedule (6h) → HTTP Request (JSONPlaceholder) → Code (filter+transform) → Code (agréger stats)
```

### Concepts appris
- **Manipulation de tableaux** avec `$input.all()` et `.map()` / `.filter()`
- **Agrégation** : comptage par groupe, calcul de moyenne
- **Pipeline multi-étapes** : chaque nœud affine les données

### Test manuel
Cliquer **Execute workflow** — résultat dans le deuxième nœud Code :
```json
{
  "total": 30,
  "par_user": { "user_1": 10, "user_2": 10, "user_3": 10 },
  "longueur_moyenne": 196
}
```

---

## Progression recommandée

```
01 Hello Webhook    → comprendre trigger + réponse
02 HTTP Request     → appeler une API externe
03 Condition Switch → router selon les données
04 AI Summarizer    → intégrer un LLM
05 Data Pipeline    → transformer et agréger
```
