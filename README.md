# StatAnalyse Pro — Déploiement

## Structure du projet
```
statanalyse/
├── index.html                    ← Application principale
├── netlify.toml                  ← Config Netlify
└── netlify/functions/
    └── proxy.js                  ← Proxy API (clés cachées ici)
```

## Étapes de déploiement

### 1. GitHub
- Push tout le dossier sur ton repo GitHub
- Le `index.html` peut être public — il ne contient AUCUNE clé

### 2. Netlify
1. Va sur https://netlify.com → "Add new site" → "Import from GitHub"
2. Sélectionne ton repo
3. Build settings : laisser vide (pas de build)
4. Clique "Deploy"

### 3. Variables d'environnement (clés API)
Dans Netlify → Site settings → Environment variables → Add variable :

| Variable       | Ta clé API                     | Obligatoire |
|----------------|--------------------------------|-------------|
| CEREBRAS_KEY   | csk-...                        | ✅ free      |
| GROQ_KEY       | gsk_...                        | ✅ free      |
| GEMINI_KEY     | AIza...                        | ✅ free      |
| MISTRAL_KEY    | ...                            | ✅ free      |
| DEEPSEEK_KEY   | sk-...                         | ⚠️ payant   |
| CLAUDE_KEY     | sk-ant-api03-...               | ⚠️ payant   |

> Les clés non configurées sont simplement ignorées — la cascade passe au suivant.

### 4. Redéployer après ajout des clés
Netlify → Deploys → "Trigger deploy"

## Cascade AI
Ordre automatique : Cerebras → Groq → Gemini → Mistral → DeepSeek → Claude

Si un provider échoue (quota épuisé, clé absente), le suivant prend le relais automatiquement.
