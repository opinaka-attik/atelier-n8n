# 04 — Dépannage n8n

## Problèmes fréquents

---

### ⚠️ Le webhook ne répond pas

**Cause 1** : Workflow non activé  
→ Vérifier le toggle en haut à droite de l'éditeur — il doit être **On**

**Cause 2** : Mauvaise URL  
→ En test : utiliser l'URL **Test URL** affichée dans le nœud Webhook  
→ En production : utiliser l'URL **Production URL**

**Cause 3** : Port non exposé  
→ Vérifier que Docker expose bien le port `5678:5678`

```bash
docker ps | grep n8n
# Doit afficher : 0.0.0.0:5678->5678/tcp
```

---

### ⚠️ Erreur « Cannot read property of undefined » dans Code

**Cause** : L'item précédent n'a pas la structure attendue

**Fix** : Ajouter une vérification
```javascript
const data = $input.first().json;
if (!data || !data.current_condition) {
  return [{ json: { erreur: 'Données manquantes' } }];
}
```

---

### ⚠️ HTTP Request échoue (timeout / ECONNREFUSED)

**Cause 1** : Réseau Docker isolé  
→ Tester depuis le host :
```bash
curl -s "https://wttr.in/Paris?format=j1" | head -c 100
```

**Cause 2** : URL incorrecte ou API indisponible  
→ Tester l'URL manuellement avec curl avant d'intégrer dans n8n

---

### ⚠️ Groq retourne une erreur 401

**Cause** : Clé API invalide ou mal configurée  
→ Vérifier que le header vaut exactement : `Authorization: Bearer sk-...`  
→ Générer une nouvelle clé sur [console.groq.com](https://console.groq.com)

---

### ⚠️ Le nœud IF ne route pas correctement

**Cause** : Comparaison de types différents (string vs number)  
→ Forcer la conversion :
```
{{ Number($json.score) }} > 70
```

---

### ⚠️ Les données sont perdues entre les nœuds

**Cause** : Un nœud ne retourne pas les champs précédents  
→ Dans le nœud Code, utiliser le spread operator :
```javascript
return items.map(item => ({
  json: {
    ...item.json,       // conserver les champs précédents
    nouveau_champ: 42
  }
}));
```

---

### 🔍 Inspecter les données entre nœuds

Cliquer sur un nœud après exécution → onglet **Output** → voir le JSON exact transmis au nœud suivant. C'est la méthode la plus rapide pour déboguer.
