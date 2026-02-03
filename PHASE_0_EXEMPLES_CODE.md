# PHASE 0 - Exemples de Code (Référence)

> **Note** : Ces exemples sont fournis pour clarifier l'architecture.
> Ils ne doivent PAS être implémentés maintenant (PHASE 0 = cadrage uniquement).

---

## 1. Modèles de données (Domain Layer)

### 1.1 Ingredient.kt

```kotlin
package com.example.frigorecettes.domain.model

/**
 * Représente un ingrédient dans le domaine métier
 */
data class Ingredient(
    val id: String,
    val name: String,
    val category: String,
    val quantity: String? = null,
    val confidence: Float? = null,
    val imageUrl: String? = null
) {
    companion object {
        const val CATEGORY_VEGETABLE = "Légume"
        const val CATEGORY_MEAT = "Viande"
        const val CATEGORY_DAIRY = "Produit laitier"
        const val CATEGORY_SPICE = "Épice"
        const val CATEGORY_CONDIMENT = "Condiment"
    }
}
```

### 1.2 Recipe.kt

```kotlin
package com.example.frigorecettes.domain.model

data class Recipe(
    val id: String,
    val name: String,
    val description: String,
    val imageUrl: String,
    val category: RecipeCategory,
    val preparationTime: Int,
    val cookingTime: Int,
    val difficulty: Difficulty,
    val servings: Int,
    val ingredients: List<RecipeIngredient>,
    val steps: List<RecipeStep>,
    val matchScore: Float
) {
    val totalTime: Int
        get() = preparationTime + cookingTime
}

enum class RecipeCategory(val displayName: String) {
    STARTER("Entrée"),
    MAIN_COURSE("Plat"),
    DESSERT("Dessert"),
    SNACK("Snack")
}

enum class Difficulty(val displayName: String) {
    EASY("Facile"),
    MEDIUM("Moyen"),
    HARD("Difficile")
}
```

### 1.3 RecipeIngredient.kt

```kotlin
package com.example.frigorecettes.domain.model

data class RecipeIngredient(
    val ingredient: Ingredient,
    val quantity: String,
    val isAvailable: Boolean
)
```

### 1.4 RecipeStep.kt

```kotlin
package com.example.frigorecettes.domain.model

data class RecipeStep(
    val order: Int,
    val instruction: String,
    val durationMinutes: Int? = null
)
```

### 1.5 AnalysisResult.kt

```kotlin
package com.example.frigorecettes.domain.model

data class AnalysisResult(
    val imageUri: String,
    val ingredients: List<Ingredient>,
    val analysisDate: Long,
    val processingTime: Long
)
```

---

## 2. Data Transfer Objects (Data Layer)

### 2.1 IngredientDto.kt

```kotlin
package com.example.frigorecettes.data.model

import com.squareup.moshi.Json
import com.squareup.moshi.JsonClass

@JsonClass(generateAdapter = true)
data class IngredientDto(
    @Json(name = "id")
    val id: String,
    
    @Json(name = "name")
    val name: String,
    
    @Json(name = "category")
    val category: String,
    
    @Json(name = "confidence")
    val confidence: Float? = null,
    
    @Json(name = "bounding_box")
    val boundingBox: BoundingBoxDto? = null,
    
    @Json(name = "image_url")
    val imageUrl: String? = null
)

@JsonClass(generateAdapter = true)
data class BoundingBoxDto(
    @Json(name = "x")
    val x: Int,
    
    @Json(name = "y")
    val y: Int,
    
    @Json(name = "width")
    val width: Int,
    
    @Json(name = "height")
    val height: Int
)
```

### 2.2 AnalysisResponseDto.kt

```kotlin
package com.example.frigorecettes.data.model

import com.squareup.moshi.Json
import com.squareup.moshi.JsonClass

@JsonClass(generateAdapter = true)
data class AnalysisResponseDto(
    @Json(name = "status")
    val status: String,
    
    @Json(name = "data")
    val data: AnalysisDataDto
)

@JsonClass(generateAdapter = true)
data class AnalysisDataDto(
    @Json(name = "analysis_id")
    val analysisId: String,
    
    @Json(name = "image_url")
    val imageUrl: String,
    
    @Json(name = "ingredients")
    val ingredients: List<IngredientDto>,
    
    @Json(name = "processing_time_ms")
    val processingTimeMs: Long,
    
    @Json(name = "timestamp")
    val timestamp: String
)
```

### 2.3 RecipeDto.kt

```kotlin
package com.example.frigorecettes.data.model

import com.squareup.moshi.Json
import com.squareup.moshi.JsonClass

@JsonClass(generateAdapter = true)
data class RecipeDto(
    @Json(name = "id")
    val id: String,
    
    @Json(name = "name")
    val name: String,
    
    @Json(name = "description")
    val description: String,
    
    @Json(name = "image_url")
    val imageUrl: String,
    
    @Json(name = "category")
    val category: String,
    
    @Json(name = "preparation_time")
    val preparationTime: Int,
    
    @Json(name = "cooking_time")
    val cookingTime: Int,
    
    @Json(name = "difficulty")
    val difficulty: String,
    
    @Json(name = "servings")
    val servings: Int,
    
    @Json(name = "match_score")
    val matchScore: Float? = null,
    
    @Json(name = "total_ingredients")
    val totalIngredients: Int? = null,
    
    @Json(name = "available_ingredients")
    val availableIngredients: Int? = null,
    
    @Json(name = "missing_ingredients")
    val missingIngredients: List<IngredientDto>? = null,
    
    @Json(name = "ingredients")
    val ingredients: List<RecipeIngredientDto>? = null,
    
    @Json(name = "steps")
    val steps: List<RecipeStepDto>? = null
)

@JsonClass(generateAdapter = true)
data class RecipeIngredientDto(
    @Json(name = "id")
    val id: String,
    
    @Json(name = "name")
    val name: String,
    
    @Json(name = "category")
    val category: String,
    
    @Json(name = "quantity")
    val quantity: String,
    
    @Json(name = "is_available")
    val isAvailable: Boolean,
    
    @Json(name = "image_url")
    val imageUrl: String? = null
)

@JsonClass(generateAdapter = true)
data class RecipeStepDto(
    @Json(name = "order")
    val order: Int,
    
    @Json(name = "instruction")
    val instruction: String,
    
    @Json(name = "duration_minutes")
    val durationMinutes: Int? = null
)
```

### 2.4 RecipeSuggestionsResponseDto.kt

```kotlin
package com.example.frigorecettes.data.model

import com.squareup.moshi.Json
import com.squareup.moshi.JsonClass

@JsonClass(generateAdapter = true)
data class RecipeSuggestionsResponseDto(
    @Json(name = "status")
    val status: String,
    
    @Json(name = "data")
    val data: RecipeSuggestionsDataDto
)

@JsonClass(generateAdapter = true)
data class RecipeSuggestionsDataDto(
    @Json(name = "recipes")
    val recipes: List<RecipeDto>,
    
    @Json(name = "total_count")
    val totalCount: Int,
    
    @Json(name = "query_time_ms")
    val queryTimeMs: Long
)
```

---

## 3. Mappers (Data → Domain)

### 3.1 IngredientMapper.kt

```kotlin
package com.example.frigorecettes.data.mapper

import com.example.frigorecettes.data.model.IngredientDto
import com.example.frigorecettes.domain.model.Ingredient

object IngredientMapper {
    
    fun toDomain(dto: IngredientDto, quantity: String? = null): Ingredient {
        return Ingredient(
            id = dto.id,
            name = dto.name,
            category = dto.category,
            quantity = quantity,
            confidence = dto.confidence,
            imageUrl = dto.imageUrl
        )
    }
    
    fun toDomainList(dtos: List<IngredientDto>): List<Ingredient> {
        return dtos.map { toDomain(it) }
    }
}
```

### 3.2 RecipeMapper.kt

```kotlin
package com.example.frigorecettes.data.mapper

import com.example.frigorecettes.data.model.RecipeDto
import com.example.frigorecettes.data.model.RecipeIngredientDto
import com.example.frigorecettes.data.model.RecipeStepDto
import com.example.frigorecettes.domain.model.*

object RecipeMapper {
    
    fun toDomain(dto: RecipeDto): Recipe {
        return Recipe(
            id = dto.id,
            name = dto.name,
            description = dto.description,
            imageUrl = dto.imageUrl,
            category = mapCategory(dto.category),
            preparationTime = dto.preparationTime,
            cookingTime = dto.cookingTime,
            difficulty = mapDifficulty(dto.difficulty),
            servings = dto.servings,
            ingredients = mapIngredients(dto.ingredients ?: emptyList()),
            steps = mapSteps(dto.steps ?: emptyList()),
            matchScore = dto.matchScore ?: 0f
        )
    }
    
    fun toDomainList(dtos: List<RecipeDto>): List<Recipe> {
        return dtos.map { toDomain(it) }
    }
    
    private fun mapCategory(category: String): RecipeCategory {
        return when (category.uppercase()) {
            "STARTER" -> RecipeCategory.STARTER
            "MAIN_COURSE" -> RecipeCategory.MAIN_COURSE
            "DESSERT" -> RecipeCategory.DESSERT
            "SNACK" -> RecipeCategory.SNACK
            else -> RecipeCategory.MAIN_COURSE
        }
    }
    
    private fun mapDifficulty(difficulty: String): Difficulty {
        return when (difficulty.uppercase()) {
            "EASY" -> Difficulty.EASY
            "MEDIUM" -> Difficulty.MEDIUM
            "HARD" -> Difficulty.HARD
            else -> Difficulty.EASY
        }
    }
    
    private fun mapIngredients(dtos: List<RecipeIngredientDto>): List<RecipeIngredient> {
        return dtos.map { dto ->
            RecipeIngredient(
                ingredient = Ingredient(
                    id = dto.id,
                    name = dto.name,
                    category = dto.category,
                    imageUrl = dto.imageUrl
                ),
                quantity = dto.quantity,
                isAvailable = dto.isAvailable
            )
        }
    }
    
    private fun mapSteps(dtos: List<RecipeStepDto>): List<RecipeStep> {
        return dtos.map { dto ->
            RecipeStep(
                order = dto.order,
                instruction = dto.instruction,
                durationMinutes = dto.durationMinutes
            )
        }
    }
}
```

---

## 4. Repository Interfaces (Domain)

### 4.1 IIngredientRepository.kt

```kotlin
package com.example.frigorecettes.domain.repository

import android.net.Uri
import com.example.frigorecettes.domain.model.AnalysisResult
import com.example.frigorecettes.util.Resource

interface IIngredientRepository {
    
    /**
     * Analyse une image et retourne les ingrédients détectés
     */
    suspend fun analyzeImage(imageUri: Uri): Resource<AnalysisResult>
}
```

### 4.2 IRecipeRepository.kt

```kotlin
package com.example.frigorecettes.domain.repository

import com.example.frigorecettes.domain.model.Recipe
import com.example.frigorecettes.domain.model.RecipeCategory
import com.example.frigorecettes.util.Resource

interface IRecipeRepository {
    
    /**
     * Récupère des suggestions de recettes basées sur les ingrédients
     */
    suspend fun getRecipeSuggestions(
        ingredientIds: List<String>,
        category: RecipeCategory? = null,
        minMatchScore: Float = 0.3f
    ): Resource<List<Recipe>>
    
    /**
     * Récupère les détails complets d'une recette
     */
    suspend fun getRecipeDetails(
        recipeId: String,
        availableIngredientIds: List<String> = emptyList()
    ): Resource<Recipe>
}
```

---

## 5. Use Cases (Domain)

### 5.1 AnalyzeImageUseCase.kt

```kotlin
package com.example.frigorecettes.domain.usecase

import android.net.Uri
import com.example.frigorecettes.domain.model.AnalysisResult
import com.example.frigorecettes.domain.repository.IIngredientRepository
import com.example.frigorecettes.util.Resource
import javax.inject.Inject

class AnalyzeImageUseCase @Inject constructor(
    private val ingredientRepository: IIngredientRepository
) {
    suspend operator fun invoke(imageUri: Uri): Resource<AnalysisResult> {
        return ingredientRepository.analyzeImage(imageUri)
    }
}
```

### 5.2 GetRecipeSuggestionsUseCase.kt

```kotlin
package com.example.frigorecettes.domain.usecase

import com.example.frigorecettes.domain.model.Recipe
import com.example.frigorecettes.domain.model.RecipeCategory
import com.example.frigorecettes.domain.repository.IRecipeRepository
import com.example.frigorecettes.util.Resource
import javax.inject.Inject

class GetRecipeSuggestionsUseCase @Inject constructor(
    private val recipeRepository: IRecipeRepository
) {
    suspend operator fun invoke(
        ingredientIds: List<String>,
        category: RecipeCategory? = null,
        minMatchScore: Float = 0.3f
    ): Resource<List<Recipe>> {
        
        // Validation business logic
        if (ingredientIds.isEmpty()) {
            return Resource.Error("Au moins un ingrédient est requis")
        }
        
        // Récupération des recettes
        return recipeRepository.getRecipeSuggestions(
            ingredientIds = ingredientIds,
            category = category,
            minMatchScore = minMatchScore
        )
    }
}
```

### 5.3 GetRecipeDetailsUseCase.kt

```kotlin
package com.example.frigorecettes.domain.usecase

import com.example.frigorecettes.domain.model.Recipe
import com.example.frigorecettes.domain.repository.IRecipeRepository
import com.example.frigorecettes.util.Resource
import javax.inject.Inject

class GetRecipeDetailsUseCase @Inject constructor(
    private val recipeRepository: IRecipeRepository
) {
    suspend operator fun invoke(
        recipeId: String,
        availableIngredientIds: List<String> = emptyList()
    ): Resource<Recipe> {
        return recipeRepository.getRecipeDetails(recipeId, availableIngredientIds)
    }
}
```

---

## 6. Repository Implementation (Data)

### 6.1 IngredientRepository.kt

```kotlin
package com.example.frigorecettes.data.repository

import android.net.Uri
import com.example.frigorecettes.data.mapper.IngredientMapper
import com.example.frigorecettes.data.source.remote.MockApiService
import com.example.frigorecettes.domain.model.AnalysisResult
import com.example.frigorecettes.domain.repository.IIngredientRepository
import com.example.frigorecettes.util.Resource
import javax.inject.Inject

class IngredientRepository @Inject constructor(
    private val mockApiService: MockApiService
) : IIngredientRepository {
    
    override suspend fun analyzeImage(imageUri: Uri): Resource<AnalysisResult> {
        return try {
            val response = mockApiService.analyzeImage(imageUri)
            
            val ingredients = IngredientMapper.toDomainList(response.data.ingredients)
            
            val result = AnalysisResult(
                imageUri = imageUri.toString(),
                ingredients = ingredients,
                analysisDate = System.currentTimeMillis(),
                processingTime = response.data.processingTimeMs
            )
            
            Resource.Success(result)
        } catch (e: Exception) {
            Resource.Error("Erreur lors de l'analyse de l'image: ${e.message}")
        }
    }
}
```

### 6.2 RecipeRepository.kt

```kotlin
package com.example.frigorecettes.data.repository

import com.example.frigorecettes.data.mapper.RecipeMapper
import com.example.frigorecettes.data.source.remote.MockApiService
import com.example.frigorecettes.domain.model.Recipe
import com.example.frigorecettes.domain.model.RecipeCategory
import com.example.frigorecettes.domain.repository.IRecipeRepository
import com.example.frigorecettes.util.Resource
import javax.inject.Inject

class RecipeRepository @Inject constructor(
    private val mockApiService: MockApiService
) : IRecipeRepository {
    
    override suspend fun getRecipeSuggestions(
        ingredientIds: List<String>,
        category: RecipeCategory?,
        minMatchScore: Float
    ): Resource<List<Recipe>> {
        return try {
            val response = mockApiService.getRecipeSuggestions(
                ingredientIds = ingredientIds,
                category = category?.name,
                minMatchScore = minMatchScore
            )
            
            val recipes = RecipeMapper.toDomainList(response.data.recipes)
            
            Resource.Success(recipes)
        } catch (e: Exception) {
            Resource.Error("Erreur lors de la récupération des recettes: ${e.message}")
        }
    }
    
    override suspend fun getRecipeDetails(
        recipeId: String,
        availableIngredientIds: List<String>
    ): Resource<Recipe> {
        return try {
            val response = mockApiService.getRecipeDetails(recipeId, availableIngredientIds)
            
            val recipe = RecipeMapper.toDomain(response)
            
            Resource.Success(recipe)
        } catch (e: Exception) {
            Resource.Error("Erreur lors de la récupération de la recette: ${e.message}")
        }
    }
}
```

---

## 7. Mock API Service (Data Source)

### 7.1 MockApiService.kt

```kotlin
package com.example.frigorecettes.data.source.remote

import android.net.Uri
import com.example.frigorecettes.data.model.AnalysisResponseDto
import com.example.frigorecettes.data.model.RecipeDto
import com.example.frigorecettes.data.model.RecipeSuggestionsResponseDto
import kotlinx.coroutines.delay
import javax.inject.Inject
import javax.inject.Singleton

@Singleton
class MockApiService @Inject constructor(
    private val mockDataProvider: MockDataProvider
) {
    
    /**
     * Simule l'analyse d'une image
     * Délai : 1.5 secondes
     */
    suspend fun analyzeImage(imageUri: Uri): AnalysisResponseDto {
        delay(1500) // Simule latence réseau
        return mockDataProvider.getMockAnalysisResult()
    }
    
    /**
     * Simule la récupération de suggestions de recettes
     * Délai : 800ms
     */
    suspend fun getRecipeSuggestions(
        ingredientIds: List<String>,
        category: String? = null,
        minMatchScore: Float = 0.3f
    ): RecipeSuggestionsResponseDto {
        delay(800)
        return mockDataProvider.getMockRecipeSuggestions(
            ingredientIds,
            category,
            minMatchScore
        )
    }
    
    /**
     * Simule la récupération du détail d'une recette
     * Délai : 500ms
     */
    suspend fun getRecipeDetails(
        recipeId: String,
        availableIngredientIds: List<String>
    ): RecipeDto {
        delay(500)
        return mockDataProvider.getMockRecipeDetail(recipeId, availableIngredientIds)
    }
}
```

### 7.2 MockDataProvider.kt (Structure)

```kotlin
package com.example.frigorecettes.data.source.remote

import com.example.frigorecettes.data.model.*
import javax.inject.Inject
import javax.inject.Singleton

@Singleton
class MockDataProvider @Inject constructor() {
    
    fun getMockAnalysisResult(): AnalysisResponseDto {
        return AnalysisResponseDto(
            status = "success",
            data = AnalysisDataDto(
                analysisId = "mock-analysis-001",
                imageUrl = "mock://image",
                ingredients = listOf(
                    IngredientDto(
                        id = "ing_001",
                        name = "Tomate",
                        category = "Légume",
                        confidence = 0.95f,
                        imageUrl = "https://example.com/tomate.png"
                    ),
                    IngredientDto(
                        id = "ing_002",
                        name = "Courgette",
                        category = "Légume",
                        confidence = 0.89f,
                        imageUrl = "https://example.com/courgette.png"
                    ),
                    IngredientDto(
                        id = "ing_003",
                        name = "Oeuf",
                        category = "Produit laitier",
                        confidence = 0.92f,
                        imageUrl = "https://example.com/oeuf.png"
                    ),
                    IngredientDto(
                        id = "ing_004",
                        name = "Lait",
                        category = "Produit laitier",
                        confidence = 0.78f,
                        imageUrl = "https://example.com/lait.png"
                    )
                ),
                processingTimeMs = 1245,
                timestamp = "2026-02-03T10:30:45Z"
            )
        )
    }
    
    fun getMockRecipeSuggestions(
        ingredientIds: List<String>,
        category: String?,
        minMatchScore: Float
    ): RecipeSuggestionsResponseDto {
        // Logique de filtrage mock selon les paramètres
        val allRecipes = getAllMockRecipes()
        
        val filteredRecipes = allRecipes.filter { recipe ->
            (category == null || recipe.category == category) &&
            (recipe.matchScore ?: 0f) >= minMatchScore
        }
        
        return RecipeSuggestionsResponseDto(
            status = "success",
            data = RecipeSuggestionsDataDto(
                recipes = filteredRecipes,
                totalCount = filteredRecipes.size,
                queryTimeMs = 85
            )
        )
    }
    
    fun getMockRecipeDetail(
        recipeId: String,
        availableIngredientIds: List<String>
    ): RecipeDto {
        // Retourne une recette complète avec steps
        return when (recipeId) {
            "rec_001" -> getOmeletteRecipe(availableIngredientIds)
            "rec_002" -> getRatatouille(availableIngredientIds)
            else -> getDefaultRecipe(availableIngredientIds)
        }
    }
    
    private fun getAllMockRecipes(): List<RecipeDto> {
        return listOf(
            RecipeDto(
                id = "rec_001",
                name = "Omelette aux légumes",
                description = "Une omelette simple et savoureuse",
                imageUrl = "https://example.com/omelette.jpg",
                category = "MAIN_COURSE",
                preparationTime = 10,
                cookingTime = 15,
                difficulty = "EASY",
                servings = 2,
                matchScore = 0.95f,
                totalIngredients = 6,
                availableIngredients = 4,
                missingIngredients = listOf(
                    IngredientDto("ing_105", "Sel", "Épice"),
                    IngredientDto("ing_106", "Poivre", "Épice")
                )
            ),
            RecipeDto(
                id = "rec_002",
                name = "Ratatouille",
                description = "Plat méditerranéen traditionnel",
                imageUrl = "https://example.com/ratatouille.jpg",
                category = "MAIN_COURSE",
                preparationTime = 20,
                cookingTime = 45,
                difficulty = "MEDIUM",
                servings = 4,
                matchScore = 0.75f,
                totalIngredients = 8,
                availableIngredients = 6
            )
            // ... plus de recettes
        )
    }
    
    private fun getOmeletteRecipe(availableIds: List<String>): RecipeDto {
        return RecipeDto(
            id = "rec_001",
            name = "Omelette aux légumes",
            description = "Une omelette simple et savoureuse avec des légumes frais",
            imageUrl = "https://example.com/omelette.jpg",
            category = "MAIN_COURSE",
            preparationTime = 10,
            cookingTime = 15,
            difficulty = "EASY",
            servings = 2,
            ingredients = listOf(
                RecipeIngredientDto(
                    id = "ing_003",
                    name = "Oeuf",
                    category = "Produit laitier",
                    quantity = "4 oeufs",
                    isAvailable = availableIds.contains("ing_003"),
                    imageUrl = "https://example.com/oeuf.png"
                ),
                RecipeIngredientDto(
                    id = "ing_001",
                    name = "Tomate",
                    category = "Légume",
                    quantity = "2 tomates moyennes",
                    isAvailable = availableIds.contains("ing_001"),
                    imageUrl = "https://example.com/tomate.png"
                ),
                RecipeIngredientDto(
                    id = "ing_002",
                    name = "Courgette",
                    category = "Légume",
                    quantity = "1 courgette",
                    isAvailable = availableIds.contains("ing_002"),
                    imageUrl = "https://example.com/courgette.png"
                ),
                RecipeIngredientDto(
                    id = "ing_004",
                    name = "Lait",
                    category = "Produit laitier",
                    quantity = "50ml",
                    isAvailable = availableIds.contains("ing_004"),
                    imageUrl = "https://example.com/lait.png"
                ),
                RecipeIngredientDto(
                    id = "ing_105",
                    name = "Sel",
                    category = "Épice",
                    quantity = "1 pincée",
                    isAvailable = false,
                    imageUrl = "https://example.com/sel.png"
                ),
                RecipeIngredientDto(
                    id = "ing_106",
                    name = "Poivre",
                    category = "Épice",
                    quantity = "1 pincée",
                    isAvailable = false,
                    imageUrl = "https://example.com/poivre.png"
                )
            ),
            steps = listOf(
                RecipeStepDto(
                    order = 1,
                    instruction = "Laver et couper les tomates et la courgette en petits dés",
                    durationMinutes = 5
                ),
                RecipeStepDto(
                    order = 2,
                    instruction = "Dans un bol, battre les oeufs avec le lait, le sel et le poivre",
                    durationMinutes = 2
                ),
                RecipeStepDto(
                    order = 3,
                    instruction = "Faire chauffer une poêle avec un peu d'huile et faire revenir les légumes 3-4 minutes",
                    durationMinutes = 4
                ),
                RecipeStepDto(
                    order = 4,
                    instruction = "Verser les oeufs battus sur les légumes et laisser cuire à feu moyen",
                    durationMinutes = 5
                ),
                RecipeStepDto(
                    order = 5,
                    instruction = "Retourner l'omelette ou la plier en deux, puis servir chaud",
                    durationMinutes = 2
                )
            )
        )
    }
    
    private fun getRatatouille(availableIds: List<String>): RecipeDto {
        // Implémentation similaire pour la ratatouille
        TODO("Mock data pour ratatouille")
    }
    
    private fun getDefaultRecipe(availableIds: List<String>): RecipeDto {
        // Recette par défaut si ID inconnu
        return getOmeletteRecipe(availableIds)
    }
}
```

---

## 8. Utility Classes

### 8.1 Resource.kt

```kotlin
package com.example.frigorecettes.util

/**
 * Wrapper générique pour gérer les états de chargement, succès et erreur
 */
sealed class Resource<T>(
    val data: T? = null,
    val message: String? = null
) {
    class Success<T>(data: T) : Resource<T>(data)
    class Error<T>(message: String, data: T? = null) : Resource<T>(data, message)
    class Loading<T>(data: T? = null) : Resource<T>(data)
}
```

### 8.2 Constants.kt

```kotlin
package com.example.frigorecettes.util

object Constants {
    
    // API (pour future intégration)
    const val BASE_URL = "https://api.frigorecettes.com/"
    const val API_VERSION = "v1"
    
    // Timeouts
    const val CONNECT_TIMEOUT = 30L // secondes
    const val READ_TIMEOUT = 30L
    const val WRITE_TIMEOUT = 30L
    
    // Image
    const val MAX_IMAGE_SIZE_MB = 10
    const val IMAGE_QUALITY = 85 // Compression JPEG
    
    // Analyse
    const val DEFAULT_CONFIDENCE_THRESHOLD = 0.6f
    const val MIN_MATCH_SCORE = 0.3f
    
    // Pagination
    const val MAX_RECIPES_PER_REQUEST = 50
    
    // Cache
    const val CACHE_EXPIRY_HOURS = 24
}
```

---

## 9. ViewModel States

### 9.1 CameraState.kt

```kotlin
package com.example.frigorecettes.presentation.camera

import android.net.Uri

data class CameraState(
    val isLoading: Boolean = false,
    val error: String? = null,
    val capturedImageUri: Uri? = null,
    val hasPermission: Boolean = false
)
```

### 9.2 AnalysisState.kt

```kotlin
package com.example.frigorecettes.presentation.analysis

import android.net.Uri
import com.example.frigorecettes.domain.model.Ingredient

data class AnalysisState(
    val imageUri: Uri? = null,
    val ingredients: List<Ingredient> = emptyList(),
    val isAnalyzing: Boolean = false,
    val error: String? = null,
    val canProceed: Boolean = false
) {
    val hasIngredients: Boolean
        get() = ingredients.isNotEmpty()
}
```

### 9.3 RecipesState.kt

```kotlin
package com.example.frigorecettes.presentation.recipes

import com.example.frigorecettes.domain.model.Recipe
import com.example.frigorecettes.domain.model.RecipeCategory

data class RecipesState(
    val recipes: List<Recipe> = emptyList(),
    val filteredRecipes: List<Recipe> = emptyList(),
    val selectedCategory: RecipeCategory? = null,
    val isLoading: Boolean = false,
    val error: String? = null
) {
    val hasRecipes: Boolean
        get() = recipes.isNotEmpty()
}
```

### 9.4 RecipeDetailState.kt

```kotlin
package com.example.frigorecettes.presentation.recipedetail

import com.example.frigorecettes.domain.model.Recipe

data class RecipeDetailState(
    val recipe: Recipe? = null,
    val isLoading: Boolean = false,
    val error: String? = null
)
```

---

## 10. Navigation

### 10.1 Screen.kt

```kotlin
package com.example.frigorecettes.presentation.navigation

sealed class Screen(val route: String) {
    object Camera : Screen("camera")
    object Analysis : Screen("analysis/{imageUri}") {
        fun createRoute(imageUri: String) = "analysis/$imageUri"
    }
    object Recipes : Screen("recipes/{ingredientIds}") {
        fun createRoute(ingredientIds: String) = "recipes/$ingredientIds"
    }
    object RecipeDetail : Screen("recipe/{recipeId}") {
        fun createRoute(recipeId: String) = "recipe/$recipeId"
    }
}
```

### 10.2 NavGraph.kt (Structure)

```kotlin
package com.example.frigorecettes.presentation.navigation

import androidx.compose.runtime.Composable
import androidx.navigation.NavHostController
import androidx.navigation.compose.NavHost
import androidx.navigation.compose.composable
import androidx.navigation.navArgument

@Composable
fun NavGraph(navController: NavHostController) {
    NavHost(
        navController = navController,
        startDestination = Screen.Camera.route
    ) {
        composable(route = Screen.Camera.route) {
            // CameraScreen(navController)
        }
        
        composable(
            route = Screen.Analysis.route,
            arguments = listOf(navArgument("imageUri") { /* type */ })
        ) {
            // AnalysisScreen(navController)
        }
        
        composable(
            route = Screen.Recipes.route,
            arguments = listOf(navArgument("ingredientIds") { /* type */ })
        ) {
            // RecipesScreen(navController)
        }
        
        composable(
            route = Screen.RecipeDetail.route,
            arguments = listOf(navArgument("recipeId") { /* type */ })
        ) {
            // RecipeDetailScreen(navController)
        }
    }
}
```

---

## 11. Dependency Injection (Hilt)

### 11.1 AppModule.kt

```kotlin
package com.example.frigorecettes.di

import dagger.Module
import dagger.Provides
import dagger.hilt.InstallIn
import dagger.hilt.components.SingletonComponent
import com.squareup.moshi.Moshi
import com.squareup.moshi.kotlin.reflect.KotlinJsonAdapterFactory
import javax.inject.Singleton

@Module
@InstallIn(SingletonComponent::class)
object AppModule {
    
    @Provides
    @Singleton
    fun provideMoshi(): Moshi {
        return Moshi.Builder()
            .add(KotlinJsonAdapterFactory())
            .build()
    }
}
```

### 11.2 DataModule.kt

```kotlin
package com.example.frigorecettes.di

import com.example.frigorecettes.data.repository.IngredientRepository
import com.example.frigorecettes.data.repository.RecipeRepository
import com.example.frigorecettes.domain.repository.IIngredientRepository
import com.example.frigorecettes.domain.repository.IRecipeRepository
import dagger.Binds
import dagger.Module
import dagger.hilt.InstallIn
import dagger.hilt.components.SingletonComponent
import javax.inject.Singleton

@Module
@InstallIn(SingletonComponent::class)
abstract class DataModule {
    
    @Binds
    @Singleton
    abstract fun bindIngredientRepository(
        ingredientRepository: IngredientRepository
    ): IIngredientRepository
    
    @Binds
    @Singleton
    abstract fun bindRecipeRepository(
        recipeRepository: RecipeRepository
    ): IRecipeRepository
}
```

### 11.3 UseCaseModule.kt

```kotlin
package com.example.frigorecettes.di

import com.example.frigorecettes.domain.repository.IIngredientRepository
import com.example.frigorecettes.domain.repository.IRecipeRepository
import com.example.frigorecettes.domain.usecase.AnalyzeImageUseCase
import com.example.frigorecettes.domain.usecase.GetRecipeDetailsUseCase
import com.example.frigorecettes.domain.usecase.GetRecipeSuggestionsUseCase
import dagger.Module
import dagger.Provides
import dagger.hilt.InstallIn
import dagger.hilt.android.components.ViewModelComponent
import dagger.hilt.android.scopes.ViewModelScoped

@Module
@InstallIn(ViewModelComponent::class)
object UseCaseModule {
    
    @Provides
    @ViewModelScoped
    fun provideAnalyzeImageUseCase(
        repository: IIngredientRepository
    ): AnalyzeImageUseCase {
        return AnalyzeImageUseCase(repository)
    }
    
    @Provides
    @ViewModelScoped
    fun provideGetRecipeSuggestionsUseCase(
        repository: IRecipeRepository
    ): GetRecipeSuggestionsUseCase {
        return GetRecipeSuggestionsUseCase(repository)
    }
    
    @Provides
    @ViewModelScoped
    fun provideGetRecipeDetailsUseCase(
        repository: IRecipeRepository
    ): GetRecipeDetailsUseCase {
        return GetRecipeDetailsUseCase(repository)
    }
}
```

---

## 12. Application Class

### 12.1 FrigoRecettesApplication.kt

```kotlin
package com.example.frigorecettes

import android.app.Application
import dagger.hilt.android.HiltAndroidApp

@HiltAndroidApp
class FrigoRecettesApplication : Application() {
    
    override fun onCreate() {
        super.onCreate()
        // Initialisation globale si nécessaire
    }
}
```

---

## 13. Gradle Dependencies (Référence)

### 13.1 build.gradle.kts (app module)

```kotlin
plugins {
    id("com.android.application")
    id("org.jetbrains.kotlin.android")
    id("com.google.dagger.hilt.android")
    kotlin("kapt")
}

android {
    namespace = "com.example.frigorecettes"
    compileSdk = 34
    
    defaultConfig {
        applicationId = "com.example.frigorecettes"
        minSdk = 24
        targetSdk = 34
        versionCode = 1
        versionName = "1.0.0"
    }
    
    buildFeatures {
        compose = true
    }
    
    composeOptions {
        kotlinCompilerExtensionVersion = "1.5.8"
    }
}

dependencies {
    // Core Android
    implementation("androidx.core:core-ktx:1.12.0")
    implementation("androidx.lifecycle:lifecycle-runtime-ktx:2.7.0")
    implementation("androidx.activity:activity-compose:1.8.2")
    
    // Jetpack Compose
    implementation(platform("androidx.compose:compose-bom:2024.01.00"))
    implementation("androidx.compose.ui:ui")
    implementation("androidx.compose.ui:ui-graphics")
    implementation("androidx.compose.ui:ui-tooling-preview")
    implementation("androidx.compose.material3:material3")
    
    // Navigation Compose
    implementation("androidx.navigation:navigation-compose:2.7.6")
    
    // ViewModel Compose
    implementation("androidx.lifecycle:lifecycle-viewmodel-compose:2.7.0")
    
    // Hilt (Dependency Injection)
    implementation("com.google.dagger:hilt-android:2.50")
    kapt("com.google.dagger:hilt-android-compiler:2.50")
    implementation("androidx.hilt:hilt-navigation-compose:1.1.0")
    
    // Coroutines
    implementation("org.jetbrains.kotlinx:kotlinx-coroutines-android:1.7.3")
    
    // CameraX
    implementation("androidx.camera:camera-camera2:1.3.1")
    implementation("androidx.camera:camera-lifecycle:1.3.1")
    implementation("androidx.camera:camera-view:1.3.1")
    
    // Coil (Image loading)
    implementation("io.coil-kt:coil-compose:2.5.0")
    
    // Retrofit (Mock pour MVP, préparé pour V2)
    implementation("com.squareup.retrofit2:retrofit:2.9.0")
    implementation("com.squareup.retrofit2:converter-moshi:2.9.0")
    
    // Moshi (JSON parsing)
    implementation("com.squareup.moshi:moshi:1.15.0")
    implementation("com.squareup.moshi:moshi-kotlin:1.15.0")
    kapt("com.squareup.moshi:moshi-kotlin-codegen:1.15.0")
    
    // Room (optionnel pour cache local)
    // implementation("androidx.room:room-runtime:2.6.1")
    // kapt("androidx.room:room-compiler:2.6.1")
    // implementation("androidx.room:room-ktx:2.6.1")
}
```

---

## Récapitulatif

Ces exemples de code illustrent :

1. **Séparation claire des couches** : Domain / Data / Presentation
2. **Contrats d'interfaces** : Repositories abstraits
3. **Use Cases** : Logique métier isolée
4. **Mappers** : Conversion DTO ↔ Domain
5. **Mock API** : Service simulé avec délais réalistes
6. **Resource Wrapper** : Gestion d'états unifiée
7. **States immutables** : Pour chaque ViewModel
8. **Dependency Injection** : Hilt pour l'injection
9. **Navigation** : Routes sealed class type-safe

**Important** : Ne PAS implémenter ce code maintenant. Ces exemples servent uniquement de référence pour la PHASE 0 (cadrage).

L'implémentation réelle commencera en PHASE 1.
