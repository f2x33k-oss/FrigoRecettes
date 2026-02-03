# Changelog

Toutes les modifications notables du projet FrigoRecettes seront documentées dans ce fichier.

Le format est basé sur [Keep a Changelog](https://keepachangelog.com/fr/1.0.0/),
et ce projet adhère au [Semantic Versioning](https://semver.org/lang/fr/).

---

## [Non publié]

### En cours
- PHASE 1 : Initialisation du projet Android Studio (à venir)

---

## [0.1.0] - 2026-02-03

### Phase 0 : Cadrage complet ✅

#### Ajouté
- **PHASE_0_CADRAGE.md** : Document principal définissant l'architecture MVVM, la structure de dossiers, les écrans, les modèles de données et les contrats API mockés
- **PHASE_0_SPECIFICATIONS_VISUELLES.md** : Spécifications UX/UI complètes avec wireframes ASCII, design system (couleurs, typographie, espacements), flux utilisateur et gestion des états
- **PHASE_0_EXEMPLES_CODE.md** : Exemples de code Kotlin illustrant les modèles de données, DTOs, mappers, repositories, use cases, ViewModels, navigation et configuration Hilt
- **PHASE_0_SYNTHESE.md** : Vue d'ensemble condensée en une page du projet avec diagrammes, stack technique, scope MVP et roadmap
- **QUICK_START.md** : Guide de démarrage rapide avec checklists détaillées pour chaque phase d'implémentation, conventions de code et debugging tips
- **README.md** : Documentation principale avec guide de navigation selon profils utilisateurs (PO, Designer, Développeur)
- **.gitignore** : Configuration pour projet Android (exclusion build, IDE, caches)

#### Défini

**Architecture** :
- MVVM (Model-View-ViewModel) avec Clean Architecture
- 3 couches : Presentation / Domain / Data
- Dependency Injection avec Hilt
- Repository Pattern pour abstraction des sources de données

**Stack technique** :
- Kotlin comme langage principal
- Jetpack Compose pour l'UI déclarative
- CameraX pour la capture photo
- Coroutines + Flow pour l'asynchrone
- Coil pour le chargement d'images
- Moshi pour le parsing JSON
- Navigation Compose pour la navigation

**Scope MVP** :
- ✅ 4 écrans : Camera / Analysis / Recipes / RecipeDetail
- ✅ Capture photo du frigo
- ✅ Analyse mockée des ingrédients
- ✅ Édition manuelle de la liste d'ingrédients
- ✅ Suggestions de recettes mockées
- ✅ Filtre par catégorie
- ✅ Affichage détail complet d'une recette
- ✅ Match score (% d'ingrédients disponibles)

**Hors scope MVP** :
- ❌ Authentification utilisateur
- ❌ Backend réel (tout en mock)
- ❌ API d'IA réelle
- ❌ Sauvegarde/favoris
- ❌ Historique
- ❌ Partage
- ❌ Liste de courses
- ❌ Notifications

**Modèles de données** :
- `Ingredient` : Représentation d'un ingrédient détecté
- `Recipe` : Recette complète avec métadonnées
- `RecipeIngredient` : Ingrédient avec quantité et disponibilité
- `RecipeStep` : Étape de préparation numérotée
- `AnalysisResult` : Résultat de l'analyse photo

**API mockées** :
- `POST /api/v1/analyze-image` : Détection d'ingrédients (~1500ms)
- `POST /api/v1/recipes/suggest` : Suggestions de recettes (~800ms)
- `GET /api/v1/recipes/{id}` : Détail d'une recette (~500ms)

**Design System** :
- Palette : Vert primaire (#4CAF50), Orange secondaire (#FF9800)
- Typographie : Roboto (H1: 24sp Bold, Body: 16sp Regular, etc.)
- Espacements standards : 8dp / 16dp / 24dp
- Composants : Cards (12dp radius), Chips (32dp height), Buttons (elevation 2dp)

#### Commits
- `f7183f4` Initial commit - README.md
- `05c8072` Phase 0 - Cadrage complet application Frigo Recettes MVP
- `5b056b2` Mise à jour README avec guide complet de la documentation PHASE 0
- `628c0ea` Ajout guide Quick Start pour démarrage rapide implémentation
- `16f9c21` Ajout document de synthèse PHASE 0 (vue d'ensemble une page)
- `4a4603a` Mise à jour README avec navigation complète documentation
- `06cb4c6` Ajout .gitignore pour projet Android

---

## Format des versions

- **Majeur (X.0.0)** : Changements majeurs incompatibles avec versions précédentes
- **Mineur (0.X.0)** : Ajout de fonctionnalités rétrocompatibles
- **Patch (0.0.X)** : Corrections de bugs rétrocompatibles

### Phases du projet

- **PHASE 0** : Cadrage et architecture (v0.1.0) ✅
- **PHASE 1** : Initialisation projet (v0.2.0) ⬜
- **PHASE 2** : Data Layer (v0.3.0) ⬜
- **PHASE 3** : Domain Layer (v0.4.0) ⬜
- **PHASE 4** : Presentation Layer (v0.5.0 - v0.8.0) ⬜
- **PHASE 5** : Tests & Polish (v0.9.0) ⬜
- **MVP Release** : v1.0.0 🎯

---

## Notes

Les versions 0.x.x sont considérées comme pre-release (développement).  
La version 1.0.0 correspondra à la première version MVP fonctionnelle.
