# 📊 PHASE 0 - Synthèse du projet (Vue d'ensemble)

## 🎯 Concept en une ligne

**"Prends ton frigo en photo → Reçois des recettes adaptées à tes ingrédients"**

---

## 📱 Application en 4 écrans

```
┌──────────────┐    ┌──────────────┐    ┌──────────────┐    ┌──────────────┐
│   📷 CAMERA  │───>│  🔍 ANALYSE  │───>│ 📋 RECETTES  │───>│  👨‍🍳 DÉTAIL  │
│              │    │              │    │              │    │              │
│  Capture la  │    │ Valide les   │    │ Liste des    │    │ Instructions │
│  photo du    │    │ ingrédients  │    │ suggestions  │    │ complètes de │
│  frigo       │    │ détectés     │    │ (avec %)     │    │ la recette   │
└──────────────┘    └──────────────┘    └──────────────┘    └──────────────┘
```

---

## 🏗 Architecture en 3 couches

```
┌─────────────────────────────────────────────────────────────────┐
│                     PRESENTATION LAYER                          │
│  ┌────────────┐  ┌────────────┐  ┌──────────┐  ┌────────────┐ │
│  │  Camera    │  │ Analysis   │  │ Recipes  │  │RecipeDetail│ │
│  │ViewModel   │  │ ViewModel  │  │ViewModel │  │ ViewModel  │ │
│  └─────┬──────┘  └─────┬──────┘  └────┬─────┘  └─────┬──────┘ │
│        │               │               │               │        │
│        └───────────────┴───────────────┴───────────────┘        │
│                            │                                    │
└────────────────────────────┼────────────────────────────────────┘
                             │
┌────────────────────────────┼────────────────────────────────────┐
│                      DOMAIN LAYER                               │
│                     ┌──────┴────────┐                           │
│                     │   USE CASES   │                           │
│  ┌──────────────────┼───────────────┼─────────────────┐        │
│  │                  │               │                 │        │
│  │ AnalyzeImage     │  GetRecipe    │ GetRecipeDetails│        │
│  │                  │  Suggestions   │                 │        │
│  └──────────────────┴───────────────┴─────────────────┘        │
│                            │                                    │
└────────────────────────────┼────────────────────────────────────┘
                             │
┌────────────────────────────┼────────────────────────────────────┐
│                       DATA LAYER                                │
│                   ┌────────┴────────┐                           │
│                   │  REPOSITORIES   │                           │
│         ┌─────────┴─────────────────┴──────────┐               │
│         │                                       │               │
│  ┌──────┴──────┐                     ┌─────────┴────────┐      │
│  │ Ingredient  │                     │     Recipe       │      │
│  │ Repository  │                     │   Repository     │      │
│  └──────┬──────┘                     └─────────┬────────┘      │
│         │                                      │               │
│         └──────────────┬───────────────────────┘               │
│                        │                                       │
│                ┌───────┴────────┐                              │
│                │ MockApiService │                              │
│                │ (Données hard- │                              │
│                │     codées)    │                              │
│                └────────────────┘                              │
└─────────────────────────────────────────────────────────────────┘
```

---

## 💾 Modèles de données (Core)

### Ingredient
```
id           : String
name         : String (ex: "Tomate")
category     : String (ex: "Légume")
quantity     : String? (ex: "200g")
confidence   : Float? (score IA 0-1)
imageUrl     : String?
```

### Recipe
```
id               : String
name             : String (ex: "Omelette aux légumes")
description      : String
imageUrl         : String
category         : RecipeCategory (STARTER/MAIN_COURSE/DESSERT/SNACK)
preparationTime  : Int (minutes)
cookingTime      : Int (minutes)
difficulty       : Difficulty (EASY/MEDIUM/HARD)
servings         : Int
ingredients      : List<RecipeIngredient>
steps            : List<RecipeStep>
matchScore       : Float (0-1, % d'ingrédients disponibles)
```

### RecipeIngredient
```
ingredient   : Ingredient
quantity     : String (ex: "3 tomates moyennes")
isAvailable  : Boolean (dispo dans le frigo?)
```

### RecipeStep
```
order            : Int
instruction      : String
durationMinutes  : Int?
```

---

## 🔄 Flux de données typique

```
User Action
    │
    ↓
[Camera]  ────capture────> [ViewModel]
                              │
                              ↓ call UseCase
                         [AnalyzeImage]
                              │
                              ↓ execute
                      [IngredientRepository]
                              │
                              ↓ fetch
                        [MockApiService]
                              │
                              ↓ delay(1500ms)
                        [MockDataProvider]
                              │
                              ↓ return DTO
                      [IngredientRepository]
                              │
                              ↓ map to Domain
                         [AnalyzeImage]
                              │
                              ↓ return Result
                          [ViewModel]
                              │
                              ↓ update State
                            [View]
                              │
                              ↓ recompose
                        User sees result
```

---

## 🎨 Design System (Résumé)

### Couleurs principales
```
Primary       : #4CAF50  (Vert frais)
Secondary     : #FF9800  (Orange chaleureux)
Background    : #FFFFFF  (Blanc)
Surface       : #F5F5F5  (Gris très clair)
Error         : #F44336  (Rouge)
```

### Typographie
```
H1 (Titres)   : 24sp, Bold
H2 (Sections) : 20sp, SemiBold
Body          : 16sp, Regular
Caption       : 14sp, Regular
```

### Espacements standards
```
Small    : 8dp
Medium   : 16dp  ← Le plus utilisé
Large    : 24dp
```

---

## 📚 API Mockées (Endpoints fictifs)

### 1. Analyse d'image
```
POST /api/v1/analyze-image
Input  : Image (multipart)
Output : List<Ingredient> avec confidence scores
Délai  : ~1500ms
```

### 2. Suggestions de recettes
```
POST /api/v1/recipes/suggest
Input  : List<ingredientIds>, category?, minMatchScore?
Output : List<Recipe> avec match scores
Délai  : ~800ms
```

### 3. Détail recette
```
GET /api/v1/recipes/{id}
Input  : recipeId, availableIngredientIds?
Output : Recipe complète (avec steps)
Délai  : ~500ms
```

**Note** : Toutes les réponses sont des données hardcodées dans `MockDataProvider`.

---

## 🛠 Stack technique (Résumé)

| Catégorie              | Technologie                |
|------------------------|----------------------------|
| **Langage**            | Kotlin                     |
| **UI**                 | Jetpack Compose            |
| **Architecture**       | MVVM + Clean Architecture  |
| **DI**                 | Hilt                       |
| **Asynchrone**         | Coroutines + Flow          |
| **Navigation**         | Navigation Compose         |
| **Caméra**             | CameraX                    |
| **Images**             | Coil                       |
| **JSON**               | Moshi                      |
| **Network (préparé)**  | Retrofit (mock pour MVP)   |

---

## ✅ Scope MVP (Ce qui est inclus)

| Feature                              | Status |
|--------------------------------------|--------|
| Capture photo frigo                  | ✅ MVP  |
| Détection ingrédients (mock)         | ✅ MVP  |
| Édition manuelle ingrédients         | ✅ MVP  |
| Suggestions recettes (mock)          | ✅ MVP  |
| Filtre par catégorie                 | ✅ MVP  |
| Affichage détail recette             | ✅ MVP  |
| Match score (% compatibilité)        | ✅ MVP  |
| UI moderne Compose                   | ✅ MVP  |

---

## ❌ Hors scope MVP (Prévu pour V2)

| Feature                              | Status    |
|--------------------------------------|-----------|
| Authentification utilisateur         | ❌ Post-MVP |
| Sauvegarde favoris                   | ❌ Post-MVP |
| Historique analyses                  | ❌ Post-MVP |
| Backend réel + API IA                | ❌ Post-MVP |
| Mode hors ligne                      | ❌ Post-MVP |
| Partage recettes                     | ❌ Post-MVP |
| Liste de courses                     | ❌ Post-MVP |
| Timer cuisine                        | ❌ Post-MVP |
| Notifications                        | ❌ Post-MVP |
| Filtres allergènes/régimes           | ❌ Post-MVP |

---

## 📂 Structure de dossiers (Simplifiée)

```
com.example.frigorecettes/
│
├── di/                    # Hilt modules
│   ├── AppModule
│   ├── DataModule
│   └── UseCaseModule
│
├── data/                  # Data Layer
│   ├── model/             # DTOs
│   ├── repository/        # Implémentations
│   ├── source/remote/     # Mock API
│   └── mapper/            # DTO ↔ Domain
│
├── domain/                # Domain Layer
│   ├── model/             # Business objects
│   ├── repository/        # Interfaces
│   └── usecase/           # Logique métier
│
├── presentation/          # Presentation Layer
│   ├── theme/             # Design system
│   ├── components/        # Composables réutilisables
│   ├── camera/            # Écran + ViewModel
│   ├── analysis/          # Écran + ViewModel
│   ├── recipes/           # Écran + ViewModel
│   ├── recipedetail/      # Écran + ViewModel
│   ├── navigation/        # NavGraph
│   └── MainActivity
│
└── util/                  # Utilitaires
    ├── Resource.kt
    ├── Constants.kt
    └── Extensions.kt
```

---

## 🔑 Concepts clés à retenir

### 1. Séparation des couches
- **Presentation** : UI + ViewModels (seulement affichage)
- **Domain** : Use Cases (logique métier pure)
- **Data** : Repositories + API (gestion des données)

### 2. Flow de données unidirectionnel
```
Action → ViewModel → UseCase → Repository → API
Result ← ViewModel ← UseCase ← Repository ← API
```

### 3. States immutables
- Chaque écran a un `State` data class
- Les ViewModels exposent `StateFlow<State>`
- Compose recompose automatiquement sur changement

### 4. Resource Wrapper
```kotlin
sealed class Resource<T> {
    class Loading<T>
    class Success<T>(data: T)
    class Error<T>(message: String)
}
```
Permet de gérer proprement : chargement, succès, erreur.

### 5. Dependency Injection (Hilt)
- Injecte automatiquement les dépendances
- Facilite les tests (on peut mocker)
- Centralise la création d'objets

---

## 📝 Étapes de développement (Roadmap)

```
PHASE 0 ✅ Cadrage (actuel)
   │
   ├─ Architecture définie
   ├─ Modèles de données spécifiés
   ├─ Wireframes créés
   └─ Contrats API documentés
   
PHASE 1 ⬜ Initialisation (next)
   │
   ├─ Projet Android Studio
   ├─ Configuration Gradle
   ├─ Structure de packages
   └─ Theme Compose
   
PHASE 2 ⬜ Data Layer
   │
   ├─ DTOs et Domain models
   ├─ Mappers
   ├─ Mock API Service
   └─ Repositories
   
PHASE 3 ⬜ Domain Layer
   │
   └─ Use Cases
   
PHASE 4 ⬜ Presentation Layer
   │
   ├─ Composants réutilisables
   ├─ Écran Camera
   ├─ Écran Analysis
   ├─ Écran Recipes
   └─ Écran RecipeDetail
   
PHASE 5 ⬜ Tests & Polish
   │
   ├─ Tests unitaires
   ├─ Tests UI
   └─ Corrections UX
   
MVP READY 🚀
```

---

## 🎯 Métriques de succès MVP

L'application MVP sera considérée comme réussie si :

1. **Fonctionnel** : Les 4 écrans fonctionnent sans crash
2. **Utilisable** : Le parcours utilisateur est fluide
3. **Réaliste** : Les délais mock simulent une vraie API
4. **Propre** : Architecture MVVM respectée
5. **Maintenable** : Code structuré, nommage cohérent
6. **Performant** : 60 FPS, pas de freezes
7. **Accessible** : Permissions gérées correctement

---

## 📖 Documents de référence

| Document                                 | Utilité                              |
|------------------------------------------|--------------------------------------|
| `README.md`                              | Introduction et guide navigation     |
| `PHASE_0_CADRAGE.md`                     | Architecture et spécifications       |
| `PHASE_0_SPECIFICATIONS_VISUELLES.md`    | Wireframes et design system          |
| `PHASE_0_EXEMPLES_CODE.md`               | Exemples Kotlin pour implémentation  |
| `QUICK_START.md`                         | Guide démarrage rapide               |
| `PHASE_0_SYNTHESE.md` (ce document)      | Vue d'ensemble en une page           |

---

## 🚀 Pour démarrer maintenant

1. **Lire** `README.md` pour comprendre le contexte
2. **Étudier** `PHASE_0_CADRAGE.md` pour l'architecture
3. **Visualiser** `PHASE_0_SPECIFICATIONS_VISUELLES.md` pour l'UI
4. **Suivre** `QUICK_START.md` pour l'implémentation

---

## 💡 Philosophie du projet

**Simplicité** : MVP minimal, pas de features inutiles  
**Qualité** : Code propre et architecture solide  
**Réalisme** : Mock qui simule une vraie app  
**Évolutivité** : Préparé pour intégrer une vraie API plus tard  

---

**La PHASE 0 est terminée. Le projet est prêt pour l'implémentation ! 🎉**
