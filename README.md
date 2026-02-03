# 🍳 Frigo Recettes - Application Android MVP

> **Photo du frigo → Suggestions de recettes**

Application Android native permettant de photographier le contenu de son réfrigérateur et recevoir des suggestions de recettes réalisables avec les ingrédients détectés.

## 📋 État du projet

**Phase actuelle** : PHASE 0 - Cadrage complet ✅

Le cadrage technique et fonctionnel est finalisé. L'implémentation n'a pas encore commencé.

## 📚 Documentation PHASE 0

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

**Pour comprendre l'architecture** :  
→ Commencer par `PHASE_0_CADRAGE.md`

**Pour visualiser l'interface** :  
→ Consulter `PHASE_0_SPECIFICATIONS_VISUELLES.md`

**Pour voir le code à venir** :  
→ Référence dans `PHASE_0_EXEMPLES_CODE.md`

## 📄 Licence

[À définir]

---

**Développé avec Kotlin ❤️**
