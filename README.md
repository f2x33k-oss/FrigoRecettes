# 🍳 Frigo Recettes - Application Android MVP

> **Photo du frigo → Suggestions de recettes**

Application Android native permettant de photographier le contenu de son réfrigérateur et recevoir des suggestions de recettes réalisables avec les ingrédients détectés.

## 📋 État du projet

**Phase actuelle** : PHASE 0 - Cadrage complet ✅

Le cadrage technique et fonctionnel est finalisé. L'implémentation n'a pas encore commencé.

## 📚 Documentation PHASE 0

### 🌟 [PHASE_0_SYNTHESE.md](./PHASE_0_SYNTHESE.md) ⭐ **NOUVEAU**
**Vue d'ensemble en une page** - Pour comprendre rapidement le projet

**Contenu** :
- Concept en diagrammes visuels ASCII
- Architecture en 3 couches illustrée
- Modèles de données résumés
- Flux de données typique
- Design system condensé
- Stack technique et scope MVP
- Roadmap des phases
- Métriques de succès

> 💡 **Recommandé pour débuter** : Lire ce document en premier pour avoir une vision globale avant de plonger dans les détails.

---

### 1. [PHASE_0_CADRAGE.md](./PHASE_0_CADRAGE.md)
**Document principal** - Architecture et définitions

**Contenu** :
- Vue d'ensemble du projet MVP
- Architecture globale MVVM (Model-View-ViewModel)
- Structure de dossiers Android complète
- Liste des 4 écrans nécessaires
- Modèles de données principaux (Domain Models)
- Contrats d'API JSON (reconnaissance ingrédients + suggestions recettes)
- Stratégie de mock pour le MVP
- Gestion des états et erreurs
- Permissions Android requises
- Checklist MVP (features incluses/exclues)

### 2. [PHASE_0_SPECIFICATIONS_VISUELLES.md](./PHASE_0_SPECIFICATIONS_VISUELLES.md)
**Spécifications UX/UI** - Wireframes et flux utilisateur

**Contenu** :
- Flux utilisateur complet (diagrammes ASCII)
- Wireframes détaillés de chaque écran
- Design system (couleurs, typographie, espacements)
- Composants UI réutilisables
- États de chargement et d'erreur
- Animations et transitions
- Gestion des permissions (flows)
- Scénarios d'usage (happy path + edge cases)
- Accessibilité (A11y)
- Métriques de performance cibles

### 3. [PHASE_0_EXEMPLES_CODE.md](./PHASE_0_EXEMPLES_CODE.md)
**Exemples de code Kotlin** - Référence d'implémentation

**Contenu** :
- Modèles de données (Domain Layer)
- DTOs (Data Transfer Objects)
- Mappers (Data ↔ Domain)
- Repository interfaces et implémentations
- Use Cases (logique métier)
- Mock API Service avec données hardcodées
- Utility classes (Resource wrapper, Constants)
- ViewModel States
- Navigation (Jetpack Compose)
- Dependency Injection (Hilt modules)
- Configuration Gradle (dépendances)

> ⚠️ **Note** : Les exemples de code sont fournis pour clarifier l'architecture. Ils ne doivent PAS être implémentés pendant la PHASE 0.

---

### 4. [QUICK_START.md](./QUICK_START.md)
**Guide de démarrage rapide** - Pour passer à l'implémentation

**Contenu** :
- Checklist avant de commencer
- PHASE 1 : Initialisation projet (étape par étape)
- PHASE 2-5 : Ordre d'implémentation détaillé
- Conventions de code et nommage
- Configuration Gradle complète
- Debugging tips et problèmes fréquents
- Definition of Done du MVP
- Priorités d'implémentation (P0 à P3)
- Ressources utiles

> 🚀 **Pour développeurs** : Suivre ce guide pour démarrer l'implémentation après validation de la PHASE 0.

## 🎯 Objectifs du MVP

### Fonctionnalités incluses ✅
- Capture photo du frigo (CameraX)
- Analyse mockée des ingrédients avec détection simulée
- Édition manuelle de la liste d'ingrédients
- Suggestions de recettes mockées basées sur ingrédients
- Filtre simple par catégorie (entrée, plat, dessert)
- Affichage détail complet d'une recette
- Interface moderne avec Jetpack Compose
- Architecture MVVM propre et maintenable

### Hors scope pour MVP ❌
- Authentification utilisateur
- Sauvegarde/favoris des recettes
- Historique des analyses
- Partage de recettes
- Mode hors ligne avec synchronisation
- Notifications
- Liste de courses
- Timer de cuisine
- Backend réel (tout en mock)
- API d'IA réelle (simulation locale)

## 🛠 Stack technique

**Langage** : Kotlin  
**Architecture** : MVVM + Clean Architecture (Domain/Data/Presentation)  
**UI** : Jetpack Compose  
**DI** : Hilt  
**Asynchrone** : Kotlin Coroutines + Flow  
**Caméra** : CameraX  
**Images** : Coil  
**Navigation** : Navigation Compose  
**Network** : Retrofit + Moshi (préparé pour V2, mock en MVP)  

## 📱 Écrans de l'application

1. **CameraScreen** - Capture photo du frigo
2. **AnalysisScreen** - Validation/édition des ingrédients détectés
3. **RecipesScreen** - Liste des recettes suggérées avec filtres
4. **RecipeDetailScreen** - Détail complet d'une recette

## 🚀 Prochaines étapes

### PHASE 1 : Initialisation du projet
- Création projet Android Studio
- Configuration Gradle et dépendances
- Structure de packages selon architecture définie
- Theme Compose (couleurs, typographie)
- Navigation skeleton

### PHASE 2 : Data Layer
- Mock API Service et MockDataProvider
- Repository implementations
- Mappers (DTO ↔ Domain)

### PHASE 3 : Domain Layer
- Use Cases avec logique métier
- Business validations

### PHASE 4 : Presentation Layer
- Implémentation des 4 écrans avec Compose
- ViewModels et gestion d'état
- Composants UI réutilisables

### PHASE 5 : Tests et polish
- Tests unitaires (Use Cases, Repositories)
- Tests UI basiques
- Corrections UX et performance

## 📖 Comment lire la documentation

### Parcours recommandé

**1️⃣ Pour une vision globale rapide** :  
→ Commencer par `PHASE_0_SYNTHESE.md` (vue d'ensemble en une page)

**2️⃣ Pour comprendre l'architecture en détail** :  
→ Lire `PHASE_0_CADRAGE.md` (spécifications complètes)

**3️⃣ Pour visualiser l'interface utilisateur** :  
→ Consulter `PHASE_0_SPECIFICATIONS_VISUELLES.md` (wireframes + design system)

**4️⃣ Pour voir des exemples de code** :  
→ Référence dans `PHASE_0_EXEMPLES_CODE.md` (modèles Kotlin)

**5️⃣ Pour démarrer l'implémentation** :  
→ Suivre `QUICK_START.md` (guide étape par étape)

### Selon votre profil

**Product Owner / Chef de projet** :  
- `PHASE_0_SYNTHESE.md` (essentiel)
- `PHASE_0_SPECIFICATIONS_VISUELLES.md` (wireframes)

**Designer UI/UX** :  
- `PHASE_0_SPECIFICATIONS_VISUELLES.md` (design system)
- `PHASE_0_SYNTHESE.md` (contexte)

**Développeur Android** :  
- `PHASE_0_SYNTHESE.md` (vue d'ensemble)
- `PHASE_0_CADRAGE.md` (architecture)
- `PHASE_0_EXEMPLES_CODE.md` (référence code)
- `QUICK_START.md` (implémentation)

## 📄 Licence

[À définir]

---

**Développé avec Kotlin ❤️**
