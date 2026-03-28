# 01 — Interface n8n

## Vue d'ensemble

n8n est une plateforme **no-code / low-code** d'automatisation de workflows. L'interface est divisée en 4 zones principales.

---

## 🖼️ Zones de l'interface

### 1. Barre latérale gauche
| Icône | Section | Rôle |
|-------|---------|------|
| 🔀 | **Workflows** | Liste et gestion de tous vos workflows |
| ⏰ | **Executions** | Historique de toutes les exécutions |
| 🔑 | **Credentials** | Clés API et connexions aux services |
| ℹ️ | **Variables** | Variables globales réutilisables |
| ⚙️ | **Settings** | Configuration de l'instance |

### 2. Canvas (zone centrale)
- **Glisser-déposer** des nœuds
- **Clic droit** sur le canvas → ajouter un nœud
- **Ctrl+Z** pour annuler
- **Ctrl+A** pour tout sélectionner
- **Scroll** pour zoomer

### 3. Panneau de nœud (droite)
S'ouvre en cliquant sur un nœud :
- Paramètres du nœud
- Onglet **Input** : données reçues
- Onglet **Output** : données produites
- Onglet **Settings** : nom, notes, retry

### 4. Barre du haut
- **Execute workflow** : lancer manuellement
- **Save** : sauvegarder
- **Active toggle** : activer/désactiver le workflow

---

## 🔵 Types de nœuds

| Catégorie | Exemples | Rôle |
|-----------|---------|------|
| **Triggers** | Webhook, Schedule, Manual | Démarrer le workflow |
| **Core** | IF, Switch, Merge, Split | Logique et flux |
| **Transform** | Code, Set, Function | Manipuler les données |
| **Actions** | HTTP Request, Email, Slack | Interagir avec des services |
| **AI** | AI Agent, OpenAI, Groq | Intelligence artificielle |

---

## 💡 Raccourcis clavier

| Raccourci | Action |
|-----------|--------|
| `Ctrl+S` | Sauvegarder |
| `Ctrl+Z` | Annuler |
| `Ctrl+Shift+Z` | Rétablir |
| `Ctrl+A` | Tout sélectionner |
| `Suppr` | Supprimer nœud sélectionné |
| `F2` | Renommer le nœud |
| `Ctrl+D` | Dupliquer le nœud |

---

## 🔗 Connexions entre nœuds

- Glisser depuis le **point de sortie** (rond à droite) vers l'entrée d'un autre nœud
- Un nœud peut avoir **plusieurs sorties** (ex: IF → true/false)
- Un nœud peut avoir **plusieurs entrées** (ex: Merge)
- Les données transitent sous forme de **tableau JSON** (`items`)
