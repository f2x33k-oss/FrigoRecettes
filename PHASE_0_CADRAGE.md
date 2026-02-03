# PHASE 0 - Cadrage Application "Frigo Recettes" (MVP)

## Vue d'ensemble du projet

**Concept** : Une application Android permettant de prendre en photo le contenu de son frigo et recevoir des suggestions de recettes réalisables avec les ingrédients détectés.

**Périmètre MVP** : Fonctionnalités essentielles uniquement, sans backend réel (données mockées).

---

## 1. Architecture globale de l'application

### 1.1 Pattern architectural : MVVM (Model-View-ViewModel)

```
┌─────────────────────────────────────────────────────────────┐
│                        Presentation Layer                    │
│  ┌──────────┐      ┌──────────┐      ┌──────────┐          │
│  │ Activity │ ───> │ViewModel │ ───> │   View   │          │
│  │ Fragment │      │(LiveData)│      │  (Jetpack│          │
│  └──────────┘      └──────────┘      │ Compose) │          │
│                            │          └──────────┘          │
└────────────────────────────┼─────────────────────────────────┘
                             │
┌────────────────────────────┼─────────────────────────────────┐
│                        Domain Layer                          │
│                     ┌──────────┐                             │
│                     │ Use Cases│                             │
│                     │(Business │                             │
│                     │  Logic)  │                             │
│                     └──────────┘                             │
│                            │                                 │
└────────────────────────────┼─────────────────────────────────┘
                             │
┌────────────────────────────┼─────────────────────────────────┐
│                         Data Layer                           │
│  ┌────────────┐    ┌──────────────┐    ┌────────────┐      │
│  │ Repository │───>│ RemoteSource │    │ LocalSource│      │
│  │            │    │  (Mock API)  │    │  (Cache)   │      │
│  └────────────┘    └──────────────┘    └────────────┘      │
│                                                              │
└──────────────────────────────────────────────────────────────┘
```

### 1.2 Technologies et bibliothèques principales

**Langage** : Kotlin

**Architecture** :
- MVVM avec Architecture Components
- Repository Pattern pour la gestion des données
- Use Cases pour la logique métier

**Bibliothèques essentielles** :
- **Jetpack Compose** : UI déclarative moderne
- **ViewModel & LiveData/StateFlow** : Gestion d'état
- **Kotlin Coroutines** : Programmation asynchrone
- **Hilt** : Injection de dépendances
- **CameraX** : Capture photo simplifiée
- **Coil** : Chargement et affichage d'images
- **Retrofit** : Préparé pour futures API (mock pour MVP)
- **Moshi** : Parsing JSON
- **Room** : Cache local (optionnel pour MVP)

---

## 2. Structure de dossiers Android

```
app/
├── manifests/
│   └── AndroidManifest.xml
│
├── kotlin+java/
│   └── com.example.frigorecettes/
│       │
│       ├── FrigoRecettesApplication.kt
│       │
│       ├── di/                          # Dependency Injection (Hilt)
│       │   ├── AppModule.kt
│       │   ├── DataModule.kt
│       │   └── UseCaseModule.kt
│       │
│       ├── data/                        # Data Layer
│       │   ├── model/                   # Data Transfer Objects (DTO)
│       │   │   ├── IngredientDto.kt
│       │   │   ├── RecipeDto.kt
│       │   │   └── AnalysisResponseDto.kt
│       │   │
│       │   ├── repository/              # Repositories
│       │   │   ├── IngredientRepository.kt
│       │   │   └── RecipeRepository.kt
│       │   │
│       │   ├── source/                  # Data Sources
│       │   │   ├── remote/
│       │   │   │   ├── MockApiService.kt
│       │   │   │   └── MockDataProvider.kt
│       │   │   └── local/
│       │   │       └── (cache si nécessaire)
│       │   │
│       │   └── mapper/                  # Conversion DTO ↔ Domain
│       │       ├── IngredientMapper.kt
│       │       └── RecipeMapper.kt
│       │
│       ├── domain/                      # Domain Layer
│       │   ├── model/                   # Business Objects
│       │   │   ├── Ingredient.kt
│       │   │   ├── Recipe.kt
│       │   │   └── RecipeCategory.kt
│       │   │
│       │   ├── repository/              # Repository Interfaces
│       │   │   ├── IIngredientRepository.kt
│       │   │   └── IRecipeRepository.kt
│       │   │
│       │   └── usecase/                 # Use Cases
│       │       ├── AnalyzeImageUseCase.kt
│       │       ├── GetRecipeSuggestionsUseCase.kt
│       │       └── GetRecipeDetailsUseCase.kt
│       │
│       ├── presentation/                # Presentation Layer
│       │   ├── theme/                   # Compose Theme
│       │   │   ├── Color.kt
│       │   │   ├── Theme.kt
│       │   │   └── Type.kt
│       │   │
│       │   ├── components/              # Composables réutilisables
│       │   │   ├── RecipeCard.kt
│       │   │   ├── IngredientChip.kt
│       │   │   ├── LoadingIndicator.kt
│       │   │   └── ErrorMessage.kt
│       │   │
│       │   ├── camera/                  # Écran Caméra
│       │   │   ├── CameraScreen.kt
│       │   │   ├── CameraViewModel.kt
│       │   │   └── CameraState.kt
│       │   │
│       │   ├── analysis/                # Écran Analyse
│       │   │   ├── AnalysisScreen.kt
│       │   │   ├── AnalysisViewModel.kt
│       │   │   └── AnalysisState.kt
│       │   │
│       │   ├── recipes/                 # Écran Liste Recettes
│       │   │   ├── RecipesScreen.kt
│       │   │   ├── RecipesViewModel.kt
│       │   │   └── RecipesState.kt
│       │   │
│       │   ├── recipedetail/            # Écran Détail Recette
│       │   │   ├── RecipeDetailScreen.kt
│       │   │   ├── RecipeDetailViewModel.kt
│       │   │   └── RecipeDetailState.kt
│       │   │
│       │   ├── navigation/              # Navigation Compose
│       │   │   ├── NavGraph.kt
│       │   │   └── Screen.kt
│       │   │
│       │   └── MainActivity.kt          # Point d'entrée
│       │
│       └── util/                        # Utilitaires
│           ├── Resource.kt              # Wrapper pour état réseau
│           ├── Constants.kt
│           └── Extensions.kt
│
└── res/                                 # Resources Android
    ├── drawable/                        # Icônes et images
    ├── values/
    │   ├── strings.xml
    │   ├── colors.xml
    │   └── themes.xml
    └── xml/
        └── file_paths.xml               # Pour partage de fichiers (photos)
```

---

## 3. Liste des écrans nécessaires (MVP)

### 3.1 Écran 1 : Accueil / Caméra
**Nom** : `CameraScreen`

**Fonction** :
- Affichage de la preview de la caméra
- Bouton pour capturer la photo du frigo
- Accès à la galerie (optionnel pour MVP)

**Composants** :
- Preview caméra (CameraX)
- Bouton capture (FAB)
- Indicateur de chargement pendant l'analyse

**Navigation** :
- Après capture → `AnalysisScreen`

---

### 3.2 Écran 2 : Analyse des ingrédients
**Nom** : `AnalysisScreen`

**Fonction** :
- Afficher la photo capturée
- Afficher les ingrédients détectés (liste avec chips)
- Permettre d'ajouter/supprimer des ingrédients manuellement
- Bouton pour lancer la recherche de recettes

**Composants** :
- Image de la photo
- Liste de chips modifiables (ingrédients)
- Bouton "Trouver des recettes"
- Bouton "Reprendre une photo"

**Navigation** :
- Après validation → `RecipesScreen`
- Reprendre photo → retour `CameraScreen`

---

### 3.3 Écran 3 : Liste des recettes suggérées
**Nom** : `RecipesScreen`

**Fonction** :
- Afficher la liste des recettes correspondant aux ingrédients
- Filtrer par catégorie (entrée, plat, dessert)
- Afficher un indicateur de compatibilité (% d'ingrédients disponibles)

**Composants** :
- Liste scrollable de RecipeCard
- Filtre par catégorie (chips horizontales)
- État vide si aucune recette
- Pull-to-refresh (optionnel)

**Navigation** :
- Clic sur recette → `RecipeDetailScreen`
- Bouton retour → `AnalysisScreen`

---

### 3.4 Écran 4 : Détail d'une recette
**Nom** : `RecipeDetailScreen`

**Fonction** :
- Afficher les informations complètes d'une recette :
  - Nom et image
  - Temps de préparation
  - Difficulté
  - Liste complète des ingrédients (avec quantités)
  - Étapes de préparation
  - Ingrédients manquants (si applicable)

**Composants** :
- Image header
- Section ingrédients (liste avec icônes ✓/✗)
- Section étapes numérotées
- Bouton "Commencer la cuisson" (inactif pour MVP)

**Navigation** :
- Bouton retour → `RecipesScreen`

---

### 3.5 Navigation globale (résumé)

```
CameraScreen (démarrage)
     │
     │ [capture photo]
     ↓
AnalysisScreen
     │
     │ [chercher recettes]
     ↓
RecipesScreen
     │
     │ [sélection recette]
     ↓
RecipeDetailScreen
```

---

## 4. Modèles de données principaux

### 4.1 Ingredient (Domain Model)

```kotlin
/**
 * Représente un ingrédient détecté ou utilisé dans une recette
 */
data class Ingredient(
    val id: String,
    val name: String,           // Ex: "Tomate"
    val category: String,        // Ex: "Légume", "Viande", "Produit laitier"
    val quantity: String? = null,// Ex: "200g", "2 unités" (null si détection photo)
    val confidence: Float? = null,// Score de confiance IA (0.0 à 1.0)
    val imageUrl: String? = null // Icône de l'ingrédient
)
```

### 4.2 Recipe (Domain Model)

```kotlin
/**
 * Représente une recette complète
 */
data class Recipe(
    val id: String,
    val name: String,            // Ex: "Ratatouille provençale"
    val description: String,     // Description courte
    val imageUrl: String,        // Photo de la recette
    val category: RecipeCategory,
    val preparationTime: Int,    // En minutes
    val cookingTime: Int,        // En minutes
    val difficulty: Difficulty,  
    val servings: Int,           // Nombre de personnes
    val ingredients: List<RecipeIngredient>,
    val steps: List<RecipeStep>,
    val matchScore: Float        // % d'ingrédients disponibles (0.0 à 1.0)
)

enum class RecipeCategory {
    STARTER,     // Entrée
    MAIN_COURSE, // Plat
    DESSERT,     // Dessert
    SNACK        // Snack/Goûter
}

enum class Difficulty {
    EASY,        // Facile
    MEDIUM,      // Moyen
    HARD         // Difficile
}
```

### 4.3 RecipeIngredient (Domain Model)

```kotlin
/**
 * Ingrédient spécifique à une recette (avec quantité)
 */
data class RecipeIngredient(
    val ingredient: Ingredient,
    val quantity: String,        // Ex: "3 tomates moyennes"
    val isAvailable: Boolean     // True si détecté dans le frigo
)
```

### 4.4 RecipeStep (Domain Model)

```kotlin
/**
 * Étape de préparation d'une recette
 */
data class RecipeStep(
    val order: Int,              // Numéro de l'étape
    val instruction: String,     // Description de l'étape
    val durationMinutes: Int? = null // Durée estimée (optionnel)
)
```

### 4.5 AnalysisResult (Domain Model)

```kotlin
/**
 * Résultat de l'analyse d'une photo de frigo
 */
data class AnalysisResult(
    val imageUri: String,        // URI locale de la photo
    val ingredients: List<Ingredient>,
    val analysisDate: Long,      // Timestamp
    val processingTime: Long     // Temps d'analyse en ms
)
```

---

## 5. Contrats d'API (JSON)

### 5.1 API : Reconnaissance d'ingrédients

**Endpoint** : `POST /api/v1/analyze-image`

**Description** : Analyse une image de frigo et retourne les ingrédients détectés.

#### Request

**Headers** :
```
Content-Type: multipart/form-data
Authorization: Bearer {token} (pour V2, ignoré en MVP)
```

**Body (multipart)** :
```
image: [fichier binaire JPEG/PNG]
confidence_threshold: 0.7 (optionnel, défaut 0.6)
```

#### Response (Success - 200 OK)

```json
{
  "status": "success",
  "data": {
    "analysis_id": "a1b2c3d4-e5f6-7890-abcd-ef1234567890",
    "image_url": "https://storage.example.com/temp/analysis_123.jpg",
    "ingredients": [
      {
        "id": "ing_001",
        "name": "Tomate",
        "category": "Légume",
        "confidence": 0.95,
        "bounding_box": {
          "x": 120,
          "y": 340,
          "width": 80,
          "height": 80
        },
        "image_url": "https://cdn.example.com/ingredients/tomate.png"
      },
      {
        "id": "ing_002",
        "name": "Courgette",
        "category": "Légume",
        "confidence": 0.89,
        "bounding_box": {
          "x": 220,
          "y": 150,
          "width": 100,
          "height": 120
        },
        "image_url": "https://cdn.example.com/ingredients/courgette.png"
      },
      {
        "id": "ing_003",
        "name": "Oeuf",
        "category": "Produit laitier",
        "confidence": 0.92,
        "bounding_box": {
          "x": 50,
          "y": 200,
          "width": 60,
          "height": 70
        },
        "image_url": "https://cdn.example.com/ingredients/oeuf.png"
      },
      {
        "id": "ing_004",
        "name": "Lait",
        "category": "Produit laitier",
        "confidence": 0.78,
        "bounding_box": {
          "x": 300,
          "y": 100,
          "width": 70,
          "height": 150
        },
        "image_url": "https://cdn.example.com/ingredients/lait.png"
      }
    ],
    "processing_time_ms": 1245,
    "timestamp": "2026-02-03T10:30:45Z"
  }
}
```

#### Response (Error - 400 Bad Request)

```json
{
  "status": "error",
  "error": {
    "code": "INVALID_IMAGE",
    "message": "Le fichier fourni n'est pas une image valide",
    "details": "Format acceptés: JPEG, PNG. Taille max: 10MB"
  }
}
```

#### Response (Error - 422 Unprocessable Entity)

```json
{
  "status": "error",
  "error": {
    "code": "NO_INGREDIENTS_DETECTED",
    "message": "Aucun ingrédient n'a pu être détecté dans l'image",
    "details": "Assurez-vous que la photo est nette et bien éclairée"
  }
}
```

---

### 5.2 API : Suggestions de recettes

**Endpoint** : `POST /api/v1/recipes/suggest`

**Description** : Retourne des recettes correspondant aux ingrédients fournis.

#### Request

**Headers** :
```
Content-Type: application/json
Authorization: Bearer {token} (pour V2, ignoré en MVP)
```

**Body (JSON)** :
```json
{
  "ingredients": [
    "ing_001",
    "ing_002",
    "ing_003"
  ],
  "category": "MAIN_COURSE",
  "min_match_score": 0.5,
  "max_results": 20,
  "sort_by": "match_score"
}
```

**Paramètres** :
- `ingredients` (required) : Liste des IDs d'ingrédients disponibles
- `category` (optional) : Filtrer par catégorie (STARTER, MAIN_COURSE, DESSERT, SNACK)
- `min_match_score` (optional) : Score minimum de correspondance (0.0 à 1.0, défaut 0.3)
- `max_results` (optional) : Nombre max de résultats (défaut 20)
- `sort_by` (optional) : Tri (match_score, preparation_time, difficulty)

#### Response (Success - 200 OK)

```json
{
  "status": "success",
  "data": {
    "recipes": [
      {
        "id": "rec_001",
        "name": "Omelette aux légumes",
        "description": "Une omelette simple et savoureuse avec des légumes frais",
        "image_url": "https://cdn.example.com/recipes/omelette-legumes.jpg",
        "category": "MAIN_COURSE",
        "preparation_time": 10,
        "cooking_time": 15,
        "difficulty": "EASY",
        "servings": 2,
        "match_score": 0.95,
        "total_ingredients": 6,
        "available_ingredients": 4,
        "missing_ingredients": [
          {
            "id": "ing_105",
            "name": "Sel",
            "category": "Épice"
          },
          {
            "id": "ing_106",
            "name": "Poivre",
            "category": "Épice"
          }
        ]
      },
      {
        "id": "rec_002",
        "name": "Ratatouille",
        "description": "Plat méditerranéen traditionnel aux légumes du soleil",
        "image_url": "https://cdn.example.com/recipes/ratatouille.jpg",
        "category": "MAIN_COURSE",
        "preparation_time": 20,
        "cooking_time": 45,
        "difficulty": "MEDIUM",
        "servings": 4,
        "match_score": 0.75,
        "total_ingredients": 8,
        "available_ingredients": 6,
        "missing_ingredients": [
          {
            "id": "ing_107",
            "name": "Aubergine",
            "category": "Légume"
          },
          {
            "id": "ing_108",
            "name": "Huile d'olive",
            "category": "Condiment"
          }
        ]
      }
    ],
    "total_count": 2,
    "query_time_ms": 85
  }
}
```

#### Response (Error - 404 Not Found)

```json
{
  "status": "error",
  "error": {
    "code": "NO_RECIPES_FOUND",
    "message": "Aucune recette trouvée avec ces ingrédients",
    "details": "Essayez de réduire le score minimum ou d'ajouter plus d'ingrédients"
  }
}
```

---

### 5.3 API : Détail d'une recette

**Endpoint** : `GET /api/v1/recipes/{recipe_id}`

**Description** : Retourne les détails complets d'une recette.

#### Request

**Headers** :
```
Authorization: Bearer {token} (pour V2, ignoré en MVP)
```

**Path Parameters** :
- `recipe_id` : Identifiant de la recette

**Query Parameters** (optionnel) :
- `available_ingredients` : Liste d'IDs séparés par virgules pour marquer les ingrédients disponibles

#### Response (Success - 200 OK)

```json
{
  "status": "success",
  "data": {
    "recipe": {
      "id": "rec_001",
      "name": "Omelette aux légumes",
      "description": "Une omelette simple et savoureuse avec des légumes frais, parfaite pour un repas rapide et équilibré",
      "image_url": "https://cdn.example.com/recipes/omelette-legumes.jpg",
      "category": "MAIN_COURSE",
      "preparation_time": 10,
      "cooking_time": 15,
      "difficulty": "EASY",
      "servings": 2,
      "ingredients": [
        {
          "id": "ing_003",
          "name": "Oeuf",
          "category": "Produit laitier",
          "quantity": "4 oeufs",
          "is_available": true,
          "image_url": "https://cdn.example.com/ingredients/oeuf.png"
        },
        {
          "id": "ing_001",
          "name": "Tomate",
          "category": "Légume",
          "quantity": "2 tomates moyennes",
          "is_available": true,
          "image_url": "https://cdn.example.com/ingredients/tomate.png"
        },
        {
          "id": "ing_002",
          "name": "Courgette",
          "category": "Légume",
          "quantity": "1 courgette",
          "is_available": true,
          "image_url": "https://cdn.example.com/ingredients/courgette.png"
        },
        {
          "id": "ing_004",
          "name": "Lait",
          "category": "Produit laitier",
          "quantity": "50ml",
          "is_available": true,
          "image_url": "https://cdn.example.com/ingredients/lait.png"
        },
        {
          "id": "ing_105",
          "name": "Sel",
          "category": "Épice",
          "quantity": "1 pincée",
          "is_available": false,
          "image_url": "https://cdn.example.com/ingredients/sel.png"
        },
        {
          "id": "ing_106",
          "name": "Poivre",
          "category": "Épice",
          "quantity": "1 pincée",
          "is_available": false,
          "image_url": "https://cdn.example.com/ingredients/poivre.png"
        }
      ],
      "steps": [
        {
          "order": 1,
          "instruction": "Laver et couper les tomates et la courgette en petits dés",
          "duration_minutes": 5
        },
        {
          "order": 2,
          "instruction": "Dans un bol, battre les oeufs avec le lait, le sel et le poivre",
          "duration_minutes": 2
        },
        {
          "order": 3,
          "instruction": "Faire chauffer une poêle avec un peu d'huile et faire revenir les légumes 3-4 minutes",
          "duration_minutes": 4
        },
        {
          "order": 4,
          "instruction": "Verser les oeufs battus sur les légumes et laisser cuire à feu moyen",
          "duration_minutes": 5
        },
        {
          "order": 5,
          "instruction": "Retourner l'omelette ou la plier en deux, puis servir chaud",
          "duration_minutes": 2
        }
      ],
      "nutritional_info": {
        "calories": 245,
        "protein_g": 18,
        "carbs_g": 8,
        "fat_g": 15
      },
      "tags": ["rapide", "facile", "végétarien", "équilibré"]
    }
  }
}
```

#### Response (Error - 404 Not Found)

```json
{
  "status": "error",
  "error": {
    "code": "RECIPE_NOT_FOUND",
    "message": "La recette demandée n'existe pas",
    "details": "L'ID rec_999 ne correspond à aucune recette"
  }
}
```

---

## 6. Stratégie de Mock pour le MVP

### 6.1 MockApiService

Pour le MVP, toutes les API seront mockées côté client :

**Approche** :
- Classe `MockApiService` avec délais simulés (coroutines delay)
- Données hardcodées dans `MockDataProvider`
- Simulation de succès/erreurs aléatoires (optionnel)

**Exemple de mock** :
```kotlin
class MockApiService {
    
    suspend fun analyzeImage(imageUri: Uri): AnalysisResponseDto {
        delay(1500) // Simule latence réseau
        return MockDataProvider.getMockAnalysisResult()
    }
    
    suspend fun getRecipeSuggestions(ingredientIds: List<String>): List<RecipeDto> {
        delay(800)
        return MockDataProvider.getMockRecipes(ingredientIds)
    }
    
    suspend fun getRecipeDetails(recipeId: String): RecipeDto {
        delay(500)
        return MockDataProvider.getMockRecipeDetail(recipeId)
    }
}
```

### 6.2 Migration future vers API réelle

**Préparation** :
- Interface `ApiService` déjà définie
- Repository utilise l'interface (pas l'implémentation)
- Hilt injecte le mock en MVP
- Pour V2 : créer `RetrofitApiService` implémentant la même interface

---

## 7. États UI et gestion d'erreurs

### 7.1 Resource Wrapper

Pattern pour gérer les états de chargement/succès/erreur :

```kotlin
sealed class Resource<T> {
    class Loading<T> : Resource<T>()
    data class Success<T>(val data: T) : Resource<T>()
    data class Error<T>(val message: String, val code: String? = null) : Resource<T>()
}
```

### 7.2 États par écran

**CameraState** :
```kotlin
data class CameraState(
    val isLoading: Boolean = false,
    val error: String? = null,
    val capturedImageUri: Uri? = null
)
```

**AnalysisState** :
```kotlin
data class AnalysisState(
    val imageUri: Uri? = null,
    val ingredients: List<Ingredient> = emptyList(),
    val isAnalyzing: Boolean = false,
    val error: String? = null
)
```

**RecipesState** :
```kotlin
data class RecipesState(
    val recipes: List<Recipe> = emptyList(),
    val selectedCategory: RecipeCategory? = null,
    val isLoading: Boolean = false,
    val error: String? = null
)
```

**RecipeDetailState** :
```kotlin
data class RecipeDetailState(
    val recipe: Recipe? = null,
    val isLoading: Boolean = false,
    val error: String? = null
)
```

---

## 8. Permissions Android nécessaires

**AndroidManifest.xml** :
```xml
<!-- Caméra -->
<uses-feature android:name="android.hardware.camera" android:required="true" />
<uses-permission android:name="android.permission.CAMERA" />

<!-- Stockage (pour sauvegarder photo temporaire) -->
<uses-permission android:name="android.permission.READ_MEDIA_IMAGES" />

<!-- Internet (pour futures API, même si mockée) -->
<uses-permission android:name="android.permission.INTERNET" />
```

---

## 9. Checklist MVP (Hors scope)

**Fonctionnalités NON incluses dans le MVP** :
- ❌ Authentification utilisateur
- ❌ Sauvegarde/favoris des recettes
- ❌ Historique des analyses
- ❌ Partage de recettes
- ❌ Mode hors ligne avec synchronisation
- ❌ Notifications
- ❌ Liste de courses
- ❌ Timer de cuisine
- ❌ Vidéos de recettes
- ❌ Commentaires/notes sur recettes
- ❌ Recherche manuelle de recettes
- ❌ Filtres avancés (allergènes, régimes)
- ❌ API backend réelle
- ❌ Modification de recette par l'utilisateur

**Fonctionnalités INCLUSES dans le MVP** :
- ✅ Capture photo du frigo
- ✅ Analyse mockée des ingrédients
- ✅ Édition manuelle de la liste d'ingrédients
- ✅ Suggestions de recettes mockées
- ✅ Filtre simple par catégorie
- ✅ Affichage détail recette
- ✅ Interface Jetpack Compose moderne
- ✅ Architecture MVVM propre
- ✅ Gestion d'états et d'erreurs

---

## 10. Prochaines étapes (après PHASE 0)

Une fois ce cadrage validé :

1. **PHASE 1** : Initialisation du projet Android
   - Configuration Gradle
   - Dépendances Hilt, Compose, CameraX
   - Structure de packages

2. **PHASE 2** : Implémentation Data Layer
   - Mock API Service
   - Repositories
   - Modèles DTO et mappers

3. **PHASE 3** : Implémentation Domain Layer
   - Use Cases
   - Business logic

4. **PHASE 4** : Implémentation Presentation Layer
   - Écran Caméra
   - Écran Analyse
   - Écran Liste Recettes
   - Écran Détail

5. **PHASE 5** : Tests et polish
   - Tests unitaires (Use Cases, Repositories)
   - Tests UI basiques
   - Corrections UX

---

## Résumé

Ce document définit l'architecture complète du MVP "Frigo Recettes" :

- **Architecture** : MVVM avec couches Domain/Data/Presentation bien séparées
- **Technologies** : Kotlin, Jetpack Compose, Hilt, CameraX, Coroutines
- **4 écrans** : Caméra → Analyse → Liste Recettes → Détail
- **API mockées** : JSON prêt pour future intégration backend
- **Scope limité** : Fonctionnalités essentielles uniquement

Le projet est prêt à être implémenté de manière structurée et maintenable.
