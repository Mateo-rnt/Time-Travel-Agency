# 🕰️ TimeTravel Agency — Webapp Interactive

**Projet académique · MVP · 2025**

> Webapp immersive de voyage dans le temps permettant de découvrir des destinations temporelles, interagir avec un agent conversationnel IA et planifier son aventure.

---

## 📋 Table des matières

1. [Description du projet](#1--description-du-projet)
2. [Technologies utilisées](#2--technologies-utilisées)
3. [Features implémentées](#3--features-implémentées)
4. [Outils IA utilisés (transparence)](#4--outils-ia-utilisés-transparence)
5. [Instructions d'installation](#5--instructions-dinstallation)
6. [Crédits](#6--crédits)

---

## 1. 📖 Description du projet

TimeTravel Agency est une **webapp interactive de voyage dans le temps**, conçue comme un **MVP (Minimum Viable Product)** dans le cadre d'un projet académique évalué.

### Objectif

Créer une application web moderne, immersive et fonctionnelle qui permet à l'utilisateur de :

- **Découvrir 3 destinations temporelles** richement documentées :
  - 🗼 **Paris 1889** — Exposition Universelle
  - 🦖 **Crétacé** — L'Âge des Dinosaures
  - 🏛️ **Florence 1504** — Atelier de la Renaissance
- **Interagir avec un agent conversationnel IA** capable de recommander des destinations, répondre aux questions et proposer des actions contextuelles
- **Personnaliser un voyage** selon ses préférences (centres d'intérêt, budget, tolérance au risque)
- **Planifier une réservation** via un wizard guidé en 3 étapes

### Approche

- **MVP** : peu de fonctionnalités, mais parfaitement exécutées
- **Mobile-first** : responsive, accessible, pensé pour tous les écrans
- **100% frontend** : aucun backend requis, données mockées localement
- **Entièrement en français** : UI, textes, boutons, messages, FAQ, chat

---

## 2. 🛠️ Technologies utilisées

| Technologie | Version | Rôle |
|---|---|---|
| **React** | 18.3 | Framework frontend — composants fonctionnels, hooks (useState, useEffect, useRef, useCallback) |
| **JavaScript (JSX)** | ES2022 | Logique applicative, service IA, gestion d'état |
| **Vite** | 6.x | Build tool et serveur de développement |
| **CSS Custom Properties** | — | Design system complet : thème sombre premium, 25+ variables CSS |
| **Hash-based Routing** | Natif | Navigation SPA via `window.location.hash`, sans dépendance externe |
| **Google Fonts** | — | Typographies premium : Cormorant Garamond (titres) + Outfit (corps) |
| **Vercel** | — | Hébergement et déploiement continu |

### Architecture technique

```
timetravel-agency/
│
├── index.html              # Point d'entrée Vite
├── package.json            # Dépendances et scripts (dev/build/preview)
├── vite.config.js          # Configuration Vite + plugin React
├── vercel.json             # Configuration déploiement Vercel
├── .gitignore
├── README.md               # Ce fichier
│
├── public/
│   └── robots.txt
│
└── src/
    ├── main.jsx            # ReactDOM.createRoot — point d'entrée React
    └── App.jsx             # Application complète (composants, données, services)
```

### Structure interne de App.jsx

```
App.jsx
│
├── DATA (données mock)
│   ├── destinations[]          # 3 destinations complètes
│   ├── faqData[]               # 10 questions/réponses
│   └── chatResponses{}         # Réponses type de l'agent IA
│
├── SERVICES
│   └── ChatService (classe)    # Moteur conversationnel IA
│       ├── setContext()         # Définir le contexte de page
│       └── sendMessage()       # Traiter un message utilisateur → { text, actions }
│
├── COMPONENTS
│   ├── Icons{}                 # 12 icônes SVG inline
│   ├── Header                  # Navigation fixe responsive + menu mobile
│   ├── Footer                  # Crédits, mentions légales, transparence IA
│   ├── ChatWidget              # Agent conversationnel persistant (bulle/drawer)
│   └── DestCard                # Carte destination réutilisable
│
├── PAGES
│   ├── HomePage                # Accueil : hero, étapes, aperçu destinations
│   ├── DestinationsPage        # Galerie filtrable (6 filtres)
│   ├── DestinationDetail       # Détail complet : timeline, précautions, avis
│   ├── PlanifierPage           # Wizard 3 étapes : préférences → IA → validation
│   └── FAQPage                 # FAQ en accordéon + suggestions
│
└── App (export default)        # Routeur hash-based + composition principale
```

---

## 3. ✅ Features implémentées

### 3.1 — Pages (5 pages complètes)

| Page | Route | Contenu |
|---|---|---|
| **Accueil** | `#/` | Hero animé avec effet shimmer, section "Comment ça marche" en 3 étapes, aperçu des 3 destinations, bandeau de confiance |
| **Destinations** | `#/destinations` | Galerie filtrable (6 chips : Culture, Aventure, Famille, Risque faible, Risque élevé, Tous), 3 cards interactives avec tags et CTAs |
| **Détail destination** | `#/destinations/:id` | Hero immersif avec dégradé, 3 cards "À ne pas manquer", itinéraire timeline (Jour 1/2/3), précautions de sécurité, encadré "À éviter", témoignages voyageurs |
| **Planification** | `#/planifier` | Wizard 3 étapes avec barre de progression : Étape 1 (préférences) → Étape 2 (proposition IA + checklist) → Étape 3 (récapitulatif + confirmation) |
| **FAQ** | `#/faq` | 10 questions en accordéon, suggestions de questions cliquables, lien vers l'agent IA |

### 3.2 — Agent conversationnel IA (ChatWidget)

| Fonctionnalité | Description |
|---|---|
| **Widget persistant** | Bulle flottante en bas à droite (desktop) / bottom sheet (mobile) |
| **Recommandation guidée** | Flow en 2 questions (intérêts → tolérance au risque) puis recommandation personnalisée avec justification |
| **Contexte de page** | L'agent détecte la destination consultée et adapte ses réponses (itinéraire, risques, avis) |
| **FAQ intégrée** | Détection par mots-clés, réponse directe depuis la base locale |
| **Actions interactives** | Boutons cliquables dans le chat : "Voir la destination", "Planifier ce voyage", etc. |
| **Suggestions rapides** | 4 chips pré-remplis pour faciliter l'interaction |
| **Indicateur de saisie** | Animation "typing" (3 points) pendant le traitement |
| **Garde-fous** | Ne jamais inventer d'information, rediriger vers FAQ ou options si hors périmètre |

### 3.3 — UX / UI

| Aspect | Détail |
|---|---|
| **Design** | Premium sombre — palette midnight (#0a0b14) avec accents dorés (#d4a853) |
| **Typographie** | Cormorant Garamond (display/titres) + Outfit (body/interface) |
| **Animations** | fadeInUp au scroll, shimmer sur le hero, hover lift sur les cards, pulse sur le bouton chat |
| **États UI** | Loading (typing indicator), confirmation (écran succès), vide (filtres sans résultat) |
| **Navigation** | Header fixe avec backdrop blur, menu hamburger mobile, CTAs sticky en bas sur mobile |
| **Accessibilité** | aria-labels, contrastes suffisants, navigation clavier, boutons descriptifs |

### 3.4 — Données mock

| Donnée | Contenu |
|---|---|
| **3 destinations** | id, nom, époque, accroche, description, niveauRisque, durée, tags, catégorie, gradient, 3 incontournables, itinéraire 3 jours, précautions (4-5), zone "À éviter", 2 témoignages avec notes |
| **10 FAQ** | Questions/réponses couvrant : sécurité, personnalisation, familles, Crétacé, durée, IA, urgences, fiabilité, paiement, annulation |
| **Réponses chat** | Salutations, flow de recommandation (2 questions), réponse par défaut, message hors périmètre |

---

## 4. 🤖 Outils IA utilisés (transparence)

### 4.1 — IA dans le développement

| Outil | Éditeur | Utilisation |
|---|---|---|
| **Claude Opus 4.5** | Anthropic | Génération du code source, architecture applicative, design system, rédaction du contenu mock (destinations, FAQ, dialogues), documentation README |

L'intégralité du code a été générée avec l'assistance de **Claude (Anthropic)**. Le prompt initial décrivait les spécifications complètes du projet. Le code a été produit avec assistance IA, puis revu et déployé.

### 4.2 — IA dans l'application (côté utilisateur)

| Composant | Type | Détail |
|---|---|---|
| **Agent conversationnel** | Simulateur local | Pattern matching par expressions régulières (regex) + machine à états. **Aucun modèle de langage n'est appelé.** Toutes les réponses sont pré-écrites ou assemblées depuis les données locales. |
| **Proposition IA (wizard étape 2)** | Logique conditionnelle | Le pack recommandé (Culture / Aventure / Premium) est déterminé par des règles simples basées sur les préférences saisies. Pas de modèle prédictif. |

### 4.3 — Transparence dans l'application

Un bandeau de transparence est affiché **dans le footer sur toutes les pages** :

> « Certaines recommandations sont générées par une intelligence artificielle »

### 4.4 — Limites du simulateur IA

| Limite | Explication |
|---|---|
| Pas de NLP réel | L'agent utilise du pattern matching (regex) pour détecter les intentions |
| Pas de mémoire longue | L'état conversationnel est réinitialisé au rechargement de la page |
| Vocabulaire limité | Seuls certains mots-clés déclenchent des réponses contextuelles |
| Pas de génération de texte | Toutes les réponses sont pré-écrites ou assemblées depuis les données |
| Pas d'apprentissage | L'agent ne s'améliore pas avec l'usage |

### 4.5 — Évolution : brancher une vraie API IA

Le `ChatService` est conçu pour être **remplacé facilement** par une API externe (Claude, GPT, Mistral…). L'interface unique à modifier est la méthode `sendMessage()` qui renvoie `{ text, actions }`.

**Étapes :**

1. Remplacer le corps de `sendMessage()` par un appel `fetch` vers l'API choisie
2. Rendre le composant `ChatWidget` asynchrone (`async/await` au lieu de `setTimeout`)
3. Maintenir l'historique conversationnel au format `[{ role, content }]` et l'envoyer à chaque appel

---

## 5. 🚀 Instructions d'installation

### Prérequis

- **Node.js** ≥ 18
- **npm** ≥ 9
- Un navigateur récent (Chrome, Firefox, Safari, Edge)

### Installation locale

```bash
# 1. Cloner le repo
git clone https://github.com/Mateo-rnt/Time-Travel-Agency.git
cd Time-Travel-Agency

# 2. Installer les dépendances
npm install

# 3. Lancer le serveur de développement
npm run dev
```

L'application sera accessible sur **http://localhost:5173**

### Commandes disponibles

| Commande | Action |
|---|---|
| `npm run dev` | Lance le serveur de développement Vite (hot reload) |
| `npm run build` | Génère le build de production dans `dist/` |
| `npm run preview` | Prévisualise le build de production en local |

### Déploiement sur Vercel

Le projet est configuré pour un déploiement automatique sur Vercel :

1. Connecter le repo GitHub à [vercel.com](https://vercel.com)
2. Vercel détecte automatiquement Vite via `vercel.json`
3. Chaque `git push` sur `main` déclenche un redéploiement

**Configuration Vercel (vercel.json) :**

```json
{
  "buildCommand": "npm run build",
  "outputDirectory": "dist",
  "framework": "vite",
  "rewrites": [
    { "source": "/(.*)", "destination": "/index.html" }
  ]
}
```

### Notes

- **Aucun backend requis** : toutes les données sont embarquées dans le code
- **Aucune dépendance lourde** : React + Vite uniquement, pas de React Router ni de librairie CSS
- **Connexion internet** requise uniquement pour charger les Google Fonts (dégradation gracieuse si offline)

---

## 6. 🏷️ Crédits

### Modèles IA

| Modèle | Éditeur | Utilisation |
|---|---|---|
| **Claude Opus 4.5** | [Anthropic](https://anthropic.com) | Assistance à la génération du code, de l'architecture, du contenu et de la documentation |

### APIs et services

| Service | Utilisation | Licence |
|---|---|---|
| **Google Fonts** | Typographies Cormorant Garamond & Outfit | SIL Open Font License |
| **Vercel** | Hébergement et déploiement | Gratuit (plan Hobby) |
| **Aucune API externe** | L'application fonctionne entièrement côté client | — |

### Assets

| Asset | Description | Source |
|---|---|---|
| Emojis | Visuels des destinations (🗼🦖🏛️) | Unicode standard |
| Icônes SVG | 12 icônes : navigation, actions, états | Créées inline, inspirées de [Lucide Icons](https://lucide.dev) (licence MIT) |
| Arrière-plans | Dégradés CSS + pattern SVG inline | Générés par code |

### Contenu

Toutes les données sont **fictives** et créées exclusivement pour ce projet académique :

- Descriptions de destinations, itinéraires et précautions
- Témoignages de voyageurs (noms et avis inventés)
- Questions/réponses de la FAQ
- Réponses de l'agent conversationnel

**Aucune donnée réelle n'est utilisée.** Les personnages, avis et événements décrits sont entièrement inventés à des fins de démonstration.

---

## 📜 Licence

Projet académique — Usage éducatif uniquement. Ne pas utiliser en production.

---

*Dernière mise à jour : Février 2025*
