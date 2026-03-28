# 02 — Concepts clés n8n

## Le modèle de données : les `items`

Dans n8n, chaque nœud reçoit et produit un **tableau d'items**. Chaque item est un objet JSON :

```json
[
  { "json": { "nom": "Alice", "score": 85 } },
  { "json": { "nom": "Bob",   "score": 62 } }
]
```

Dans les expressions, on accède aux données avec :
- `{{ $json.nom }}` → valeur du champ `nom` de l'item courant
- `{{ $item(0).json.nom }}` → premier item
- `{{ $items().length }}` → nombre total d'items

---

## 🔗 Les Triggers

Tout workflow commence par un **trigger** (déclencheur) :

| Trigger | Déclenchement |
|---------|---------------|
| **Manual** | Clic sur "Execute" |
| **Schedule** | Cron ou intervalle régulier |
| **Webhook** | Appel HTTP entrant (GET/POST) |
| **Email** | Réception d'un email |
| **File** | Modification d'un fichier |

---

## 🔀 Logique conditionnelle

### Nœud IF
Route les items selon une condition booléenne :
- Sortie **true** : condition respectée
- Sortie **false** : condition non respectée

### Nœud Switch
Route vers plusieurs branches selon une valeur :
```
valeur == "A" → branche 1
valeur == "B" → branche 2
default       → branche 3
```

---

## 💻 Nœud Code (JavaScript)

Le nœud Code exécute du JavaScript pour transformer les données :

```javascript
// Accéder à tous les items
const items = $input.all();

// Transformer chaque item
return items.map(item => ({
  json: {
    ...item.json,
    score_double: item.json.score * 2,
    traite_le: new Date().toISOString()
  }
}));
```

Variables disponibles dans le nœud Code :
- `$input.all()` : tous les items entrants
- `$input.first()` : premier item
- `$now` : timestamp actuel
- `$workflow.name` : nom du workflow

---

## 🌐 Nœud HTTP Request

Appel vers n'importe quelle API externe :
- Méthodes : GET, POST, PUT, DELETE, PATCH
- Auth : Basic, Bearer, API Key, OAuth2
- Body : JSON, Form Data, Binary
- Réponse : JSON auto-parsé

---

## 🔗 Webhooks

URL de format : `http://localhost:5678/webhook/MON_PATH`

- **Test URL** : disponible seulement pendant l'exécution manuelle
- **Production URL** : active quand le workflow est activé
- En mode test : cliquer **Listen for test event** avant d'appeler l'URL

---

## 🔁 Expressions et template

n8n utilise la syntaxe `{{ }}` pour les expressions dynamiques :

```
{{ $json.nom }}                    → valeur d'un champ
{{ $json.score > 70 ? 'admis' : 'refusé' }}  → ternaire
{{ new Date().toISOString() }}     → code JS
{{ $node["HTTP Request"].json.body }} → données d'un autre nœud
```
