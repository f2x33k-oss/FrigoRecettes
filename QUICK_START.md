# 🚀 Quick Start - Démarrage rapide

Guide condensé pour démarrer l'implémentation après la PHASE 0.

---

## ✅ Checklist avant de commencer

- [ ] Lire `PHASE_0_CADRAGE.md` (architecture globale)
- [ ] Consulter `PHASE_0_SPECIFICATIONS_VISUELLES.md` (wireframes)
- [ ] Parcourir `PHASE_0_EXEMPLES_CODE.md` (référence code)
- [ ] Android Studio installé (version Hedgehog ou supérieure)
- [ ] SDK Android 34 (minimum SDK 24)
- [ ] Kotlin 1.9.x configuré

---

## 📦 PHASE 1 : Initialisation (Checklist)

### 1.1 Créer le projet Android Studio
```
- File → New → New Project
- Template : "Empty Activity"
- Name : FrigoRecettes
- Package : com.example.frigorecettes
- Language : Kotlin
- Minimum SDK : API 24 (Android 7.0)
- Build configuration : Kotlin DSL (build.gradle.kts)
```

### 1.2 Configuration Gradle

**build.gradle.kts (Project)** :
```kotlin
plugins {
    id("com.android.application") version "8.2.2" apply false
    id("org.jetbrains.kotlin.android") version "1.9.22" apply false
    id("com.google.dagger.hilt.android") version "2.50" apply false
}
```

**build.gradle.kts (App)** :
- Activer Jetpack Compose
- Ajouter Hilt plugin
- Configurer Kapt
- Ajouter toutes les dépendances (voir PHASE_0_EXEMPLES_CODE.md section 13)

**Dépendances critiques** :
- Jetpack Compose (BOM 2024.01.00)
- Hilt 2.50
- CameraX 1.3.1
- Coil 2.5.0
- Navigation Compose 2.7.6
- Moshi 1.15.0
- Coroutines 1.7.3

### 1.3 Structure de dossiers

Créer l'arborescence complète (voir PHASE_0_CADRAGE.md section 2) :

```
app/src/main/kotlin/com/example/frigorecettes/
├── di/
├── data/
│   ├── model/
│   ├── repository/
│   ├── source/
│   │   └── remote/
│   └── mapper/
├── domain/
│   ├── model/
│   ├── repository/
│   └── usecase/
├── presentation/
│   ├── theme/
│   ├── components/
│   ├── camera/
│   ├── analysis/
│   ├── recipes/
│   ├── recipedetail/
│   └── navigation/
└── util/
```

### 1.4 AndroidManifest.xml

Ajouter :
```xml
<uses-permission android:name="android.permission.CAMERA" />
<uses-permission android:name="android.permission.READ_MEDIA_IMAGES" />
<uses-permission android:name="android.permission.INTERNET" />

<application
    android:name=".FrigoRecettesApplication"
    ...>
```

### 1.5 Theme Compose

Créer dans `presentation/theme/` :
- `Color.kt` (palette définie dans PHASE_0_SPECIFICATIONS_VISUELLES.md)
- `Type.kt` (typographie Roboto)
- `Theme.kt` (MaterialTheme wrapper)

### 1.6 Application Class + Hilt

Créer `FrigoRecettesApplication.kt` :
```kotlin
@HiltAndroidApp
class FrigoRecettesApplication : Application()
```

### 1.7 Navigation skeleton

- Créer `Screen.kt` (sealed class)
- Créer `NavGraph.kt` (structure de base)
- Modifier `MainActivity.kt` avec NavHost

---

## 🔨 PHASE 2 : Data Layer (Ordre d'implémentation)

### 2.1 Modèles DTO
1. `IngredientDto.kt`
2. `RecipeDto.kt`
3. `AnalysisResponseDto.kt`
4. `RecipeSuggestionsResponseDto.kt`

### 2.2 Domain Models
1. `Ingredient.kt`
2. `Recipe.kt` + enums
3. `RecipeIngredient.kt`
4. `RecipeStep.kt`
5. `AnalysisResult.kt`

### 2.3 Mappers
1. `IngredientMapper.kt`
2. `RecipeMapper.kt`

### 2.4 Mock Data Provider
1. `MockDataProvider.kt` (avec toutes les données hardcodées)
2. `MockApiService.kt` (avec delays simulés)

### 2.5 Repository Interfaces (Domain)
1. `IIngredientRepository.kt`
2. `IRecipeRepository.kt`

### 2.6 Repository Implementations (Data)
1. `IngredientRepository.kt`
2. `RecipeRepository.kt`

### 2.7 Utility
1. `Resource.kt` (sealed class)
2. `Constants.kt`

---

## 🎯 PHASE 3 : Domain Layer

### 3.1 Use Cases
1. `AnalyzeImageUseCase.kt`
2. `GetRecipeSuggestionsUseCase.kt`
3. `GetRecipeDetailsUseCase.kt`

---

## 🎨 PHASE 4 : Presentation Layer (Ordre)

### 4.1 Composants réutilisables
1. `LoadingIndicator.kt`
2. `ErrorMessage.kt`
3. `IngredientChip.kt`
4. `RecipeCard.kt`

### 4.2 Écran Camera
1. `CameraState.kt`
2. `CameraViewModel.kt`
3. `CameraScreen.kt`

### 4.3 Écran Analysis
1. `AnalysisState.kt`
2. `AnalysisViewModel.kt`
3. `AnalysisScreen.kt`

### 4.4 Écran Recipes
1. `RecipesState.kt`
2. `RecipesViewModel.kt`
3. `RecipesScreen.kt`

### 4.5 Écran RecipeDetail
1. `RecipeDetailState.kt`
2. `RecipeDetailViewModel.kt`
3. `RecipeDetailScreen.kt`

---

## 🔌 Dependency Injection (Hilt)

**Ordre de création** :
1. `AppModule.kt` (Moshi, etc.)
2. `DataModule.kt` (bind repositories)
3. `UseCaseModule.kt` (provide use cases)

**Annotations nécessaires** :
- `@HiltAndroidApp` sur Application
- `@AndroidEntryPoint` sur MainActivity
- `@HiltViewModel` sur tous les ViewModels
- `@Inject` sur constructeurs

---

## 🧪 PHASE 5 : Tests

### 5.1 Tests unitaires (priorité haute)
1. Mappers (facile à tester)
2. Use Cases (logique métier)
3. Repositories (avec mock data)

### 5.2 Tests UI (priorité moyenne)
1. Navigation flow
2. Composants réutilisables
3. États d'erreur

---

## 📝 Conventions de code

### Nommage
- **Classes** : PascalCase (`RecipeRepository`)
- **Fonctions** : camelCase (`getRecipeSuggestions`)
- **Variables** : camelCase (`ingredientList`)
- **Constants** : UPPER_SNAKE_CASE (`MAX_IMAGE_SIZE`)
- **Fichiers** : PascalCase (`CameraScreen.kt`)

### Structure fichiers
- 1 classe publique = 1 fichier
- Regrouper classes internes liées (ex: Recipe + enums)
- Ordre : companion object → properties → init → methods

### Documentation
- KDoc pour classes publiques et fonctions d'API
- Commentaires inline pour logique complexe
- TODO pour features futures marquées

### Git
- Commits fréquents par feature
- Messages en français
- Format : `type: description`
- Types : `feat`, `fix`, `docs`, `refactor`, `test`, `style`

---

## 🐛 Debugging Tips

### Problèmes fréquents

**Hilt ne compile pas** :
- Vérifier que kapt est activé
- Rebuild project (Clean → Rebuild)
- Vérifier annotations @Inject/@Provides

**Compose ne s'affiche pas** :
- Vérifier buildFeatures { compose = true }
- Vérifier kotlinCompilerExtensionVersion

**CameraX erreur permission** :
- Vérifier AndroidManifest
- Implémenter runtime permission request
- Tester sur device physique (pas émulateur)

**Navigation crash** :
- Vérifier route strings exactes
- Encoder les URIs si caractères spéciaux
- Logger navController.currentBackStackEntry

---

## 📚 Ressources utiles

**Documentation officielle** :
- [Jetpack Compose](https://developer.android.com/jetpack/compose)
- [CameraX](https://developer.android.com/training/camerax)
- [Hilt](https://developer.android.com/training/dependency-injection/hilt-android)
- [Navigation Compose](https://developer.android.com/jetpack/compose/navigation)

**Design** :
- [Material Design 3](https://m3.material.io/)
- [Compose Material 3](https://developer.android.com/jetpack/androidx/releases/compose-material3)

---

## ✅ Definition of Done (MVP)

L'application MVP est considérée comme terminée quand :

- [ ] Les 4 écrans sont implémentés et fonctionnels
- [ ] La navigation entre écrans fonctionne correctement
- [ ] La caméra capture une photo (stockage temporaire)
- [ ] L'analyse mock retourne 4-5 ingrédients avec délai réaliste
- [ ] Les ingrédients peuvent être ajoutés/supprimés manuellement
- [ ] La liste de recettes s'affiche avec filtres par catégorie
- [ ] Le détail d'une recette affiche tous les champs (ingrédients + steps)
- [ ] Les ingrédients disponibles/manquants sont indiqués visuellement
- [ ] Aucun crash sur les parcours nominaux
- [ ] Les états de chargement s'affichent correctement
- [ ] Les messages d'erreur sont clairs et pertinents
- [ ] L'UI respecte le design system défini
- [ ] Le code suit l'architecture MVVM proprement
- [ ] Les permissions caméra sont gérées correctement
- [ ] L'app fonctionne sur Android 7.0+ (API 24+)
- [ ] Pas de lint errors critiques
- [ ] Au moins 3 use cases testés unitairement

---

## 🎯 Priorités d'implémentation

### P0 (Critical - MVP bloqué sans ça)
- Structure de projet complète
- Data Layer (models, repositories, mock)
- Navigation de base
- Les 4 écrans (même versions basiques)

### P1 (High - Nécessaire pour demo)
- UI/UX polish selon design system
- Gestion des états de chargement
- Gestion des erreurs
- Permission caméra

### P2 (Medium - Nice to have MVP)
- Animations et transitions
- Tests unitaires
- Accessibilité de base
- Optimisations performance

### P3 (Low - Post-MVP)
- Tests UI complets
- Documentation inline exhaustive
- Logs et analytics
- Easter eggs 😄

---

**Bon développement ! 🚀**

Pour toute question, se référer aux 3 documents principaux de la PHASE 0.
