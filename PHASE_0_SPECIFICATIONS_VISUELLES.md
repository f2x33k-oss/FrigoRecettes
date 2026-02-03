# PHASE 0 - Spécifications Visuelles et Flux UX

## 1. Flux utilisateur détaillé

### 1.1 Parcours complet utilisateur

```
┌─────────────────────────────────────────────────────────────────┐
│                      LANCEMENT DE L'APP                         │
│                                                                 │
│  - Splash screen (optionnel)                                   │
│  - Vérification permission caméra                              │
└──────────────────────────┬──────────────────────────────────────┘
                           │
                           ↓
┌─────────────────────────────────────────────────────────────────┐
│                    ÉCRAN 1 : CAMÉRA                             │
│                                                                 │
│  ┌───────────────────────────────────────────────────┐         │
│  │                                                   │         │
│  │          [PREVIEW CAMÉRA EN TEMPS RÉEL]          │         │
│  │                                                   │         │
│  │                                                   │         │
│  │                                                   │         │
│  │                    📷                            │         │
│  │              [Bouton Capture]                    │         │
│  │                                                   │         │
│  └───────────────────────────────────────────────────┘         │
│                                                                 │
│  Actions utilisateur :                                         │
│  - Pointer caméra vers frigo                                   │
│  - Tap bouton capture                                          │
└──────────────────────────┬──────────────────────────────────────┘
                           │
                           │ [Photo capturée]
                           ↓
┌─────────────────────────────────────────────────────────────────┐
│                  ÉCRAN 2 : ANALYSE                              │
│                                                                 │
│  ┌───────────────────────────────────────────────────┐         │
│  │                                                   │         │
│  │        [PHOTO DU FRIGO CAPTURÉE]                 │         │
│  │                                                   │         │
│  └───────────────────────────────────────────────────┘         │
│                                                                 │
│  🔄 Analyse en cours... (1-2 secondes)                         │
│                                                                 │
│  ──────────────────────────────────────────────────            │
│                                                                 │
│  Ingrédients détectés :                                        │
│  ┌─────────┐ ┌──────────┐ ┌──────┐ ┌────────┐                │
│  │ Tomate  │ │Courgette │ │ Oeuf │ │  Lait  │    [+ Ajouter] │
│  │    ✓    │ │    ✓     │ │  ✓   │ │   ✓    │                │
│  └─────────┘ └──────────┘ └──────┘ └────────┘                │
│                                                                 │
│  ──────────────────────────────────────────────────            │
│                                                                 │
│  [↻ Reprendre photo]    [🔍 Trouver des recettes →]           │
└──────────────────────────┬──────────────────────────────────────┘
                           │
                           │ [Validation]
                           ↓
┌─────────────────────────────────────────────────────────────────┐
│              ÉCRAN 3 : LISTE RECETTES                           │
│                                                                 │
│  Filtres :                                                     │
│  ┌─────────┐ ┌──────┐ ┌─────────┐ ┌────────┐                 │
│  │  Tous   │ │ Plat │ │ Entrée  │ │Dessert │                 │
│  └─────────┘ └──────┘ └─────────┘ └────────┘                 │
│                                                                 │
│  12 recettes trouvées                                          │
│                                                                 │
│  ┌───────────────────────────────────────────────┐             │
│  │ [Image]  Omelette aux légumes       🟢 95%   │             │
│  │          Facile • 25 min                     │ ←           │
│  └───────────────────────────────────────────────┘             │
│                                                                 │
│  ┌───────────────────────────────────────────────┐             │
│  │ [Image]  Ratatouille              🟡 75%     │             │
│  │          Moyen • 65 min                      │             │
│  └───────────────────────────────────────────────┘             │
│                                                                 │
│  ┌───────────────────────────────────────────────┐             │
│  │ [Image]  Quiche aux légumes       🟡 60%     │             │
│  │          Facile • 45 min                     │             │
│  └───────────────────────────────────────────────┘             │
│                                                                 │
│  ... (scroll vertical)                                         │
└──────────────────────────┬──────────────────────────────────────┘
                           │
                           │ [Tap sur recette]
                           ↓
┌─────────────────────────────────────────────────────────────────┐
│              ÉCRAN 4 : DÉTAIL RECETTE                           │
│                                                                 │
│  ┌───────────────────────────────────────────────────┐         │
│  │                                                   │         │
│  │     [IMAGE HEADER FULL WIDTH DE LA RECETTE]      │         │
│  │                                                   │         │
│  └───────────────────────────────────────────────────┘         │
│                                                                 │
│  Omelette aux légumes                                          │
│  ⭐⭐⭐⭐⭐ Facile • 25 min • 2 personnes                       │
│                                                                 │
│  ──────────────────────────────────────────────────            │
│                                                                 │
│  📋 INGRÉDIENTS (6)                                            │
│                                                                 │
│  ✅ 4 oeufs                                                    │
│  ✅ 2 tomates moyennes                                         │
│  ✅ 1 courgette                                                │
│  ✅ 50ml de lait                                               │
│  ❌ 1 pincée de sel (manquant)                                │
│  ❌ 1 pincée de poivre (manquant)                             │
│                                                                 │
│  ──────────────────────────────────────────────────            │
│                                                                 │
│  👨‍🍳 PRÉPARATION (5 étapes)                                   │
│                                                                 │
│  1️⃣ Laver et couper les tomates et la courgette...           │
│     ⏱️ 5 min                                                   │
│                                                                 │
│  2️⃣ Dans un bol, battre les oeufs avec le lait...            │
│     ⏱️ 2 min                                                   │
│                                                                 │
│  ... (scroll vertical)                                         │
│                                                                 │
│  [← Retour aux recettes]                                       │
└─────────────────────────────────────────────────────────────────┘
```

---

## 2. Spécifications détaillées par écran

### 2.1 Écran Caméra

#### Layout
```
╔═════════════════════════════════════════════════╗
║  [<]                                      [i]   ║  ← TopBar
╠═════════════════════════════════════════════════╣
║                                                 ║
║                                                 ║
║                                                 ║
║           PREVIEW CAMÉRA                        ║
║           (Plein écran)                         ║
║                                                 ║
║                                                 ║
║                                                 ║
║                                                 ║
║                                                 ║
║                   ┌─────┐                       ║
║                   │  📷  │                       ║  ← Bouton capture
║                   └─────┘                       ║
║                                                 ║
╚═════════════════════════════════════════════════╝
```

#### Composants
- **TopBar** :
  - Bouton retour (si navigation depuis autre écran)
  - Bouton info (guide utilisateur optionnel)
- **Preview** : CameraX preview en plein écran
- **Bouton capture** :
  - FAB (Floating Action Button) centré en bas
  - Icône appareil photo
  - Animation au clic
- **Indicateur** : Loader lors de l'analyse (overlay)

#### Comportements
- Au lancement : demande permission caméra si non accordée
- Tap bouton : capture photo → overlay loading → navigation vers Analyse
- Gestion erreurs caméra : dialog avec message explicatif

---

### 2.2 Écran Analyse

#### Layout
```
╔═════════════════════════════════════════════════╗
║  [<] Analyse                                    ║  ← TopBar
╠═════════════════════════════════════════════════╣
║  ┌─────────────────────────────────────────┐   ║
║  │                                         │   ║
║  │      [Photo capturée]                   │   ║  ← Image preview
║  │      (Aspect ratio 4:3 ou 16:9)         │   ║
║  │                                         │   ║
║  └─────────────────────────────────────────┘   ║
║                                                 ║
║  ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━   ║
║                                                 ║
║  Ingrédients détectés (4)                      ║  ← Section titre
║                                                 ║
║  ┌─────────┐┌──────────┐┌──────┐┌────────┐   ║  ← Chips modifiables
║  │ Tomate ✗││Courgette✗││Oeuf ✗││Lait   ✗│   ║
║  └─────────┘└──────────┘└──────┘└────────┘   ║
║                                                 ║
║  ┌─────────────┐                               ║  ← Bouton ajout
║  │ + Ajouter   │                               ║
║  └─────────────┘                               ║
║                                                 ║
║  ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━   ║
║                                                 ║
║  [↻ Reprendre photo]                           ║  ← Actions
║                                                 ║
║  ┌─────────────────────────────────────────┐   ║
║  │  🔍 Trouver des recettes               │   ║  ← Bouton principal
║  └─────────────────────────────────────────┘   ║
║                                                 ║
╚═════════════════════════════════════════════════╝
```

#### Composants
- **Image** : Photo capturée (cliquable pour zoom optionnel)
- **Chips ingrédients** :
  - FlowRow (wrap automatique)
  - Chaque chip avec icône ✗ pour supprimer
  - Badge avec score de confiance (optionnel)
- **Bouton ajout** : Ouvre dialog avec recherche/sélection manuelle
- **Boutons action** :
  - Secondaire : "Reprendre photo"
  - Primaire : "Trouver des recettes"

#### Comportements
- Au chargement : animation d'analyse (1-2s)
- Chips : swipe ou tap ✗ pour supprimer
- Ajout manuel : dialog avec autocomplete
- Validation : minimum 1 ingrédient requis
- Navigation : CTA principal vers liste recettes

---

### 2.3 Écran Liste Recettes

#### Layout
```
╔═════════════════════════════════════════════════╗
║  [<] Recettes                        [⚙]       ║  ← TopBar
╠═════════════════════════════════════════════════╣
║  ┌─────┐┌─────┐┌─────────┐┌────────┐          ║  ← Filtres
║  │Tous ││Plat ││Entrée   ││Dessert │          ║
║  └─────┘└─────┘└─────────┘└────────┘          ║
║                                                 ║
║  12 recettes trouvées                          ║  ← Compteur
║                                                 ║
║  ┏━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━┓   ║
║  ┃ ┌────┐                                  ┃   ║  ← Recipe Card
║  ┃ │IMG │  Omelette aux légumes           ┃   ║
║  ┃ │    │  ⭐ Facile • ⏱️ 25 min          ┃   ║
║  ┃ └────┘  🟢 95% compatible              ┃   ║
║  ┗━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━┛   ║
║                                                 ║
║  ┏━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━┓   ║
║  ┃ ┌────┐                                  ┃   ║
║  ┃ │IMG │  Ratatouille                    ┃   ║
║  ┃ │    │  ⭐ Moyen • ⏱️ 65 min           ┃   ║
║  ┃ └────┘  🟡 75% compatible              ┃   ║
║  ┗━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━┛   ║
║                                                 ║
║  ┏━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━┓   ║
║  ┃ ┌────┐                                  ┃   ║
║  ┃ │IMG │  Quiche aux légumes             ┃   ║
║  ┃ │    │  ⭐ Facile • ⏱️ 45 min          ┃   ║
║  ┃ └────┘  🟡 60% compatible              ┃   ║
║  ┗━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━┛   ║
║                                                 ║
║  ...                                           ║
╚═════════════════════════════════════════════════╝
```

#### Composants
- **Filtres** : HorizontalScrolling chips (sélection unique)
- **Recipe Card** :
  - Image miniature (ratio 1:1, 80x80dp)
  - Titre de la recette (max 2 lignes)
  - Métadonnées : difficulté + temps
  - Match score avec indicateur couleur :
    - 🟢 Vert : 80-100%
    - 🟡 Jaune : 50-79%
    - 🟠 Orange : <50%
- **LazyColumn** : Liste scrollable avec placeholders

#### Comportements
- Filtre : tap pour sélectionner catégorie (reload liste)
- Tri : par match_score décroissant par défaut
- Tap card : navigation vers détail recette
- Pull-to-refresh : recharge suggestions (optionnel MVP)
- État vide : illustration + message "Aucune recette trouvée"

---

### 2.4 Écran Détail Recette

#### Layout
```
╔═════════════════════════════════════════════════╗
║  [<]                              [♡] [⋮]      ║  ← TopBar transparent
╠═════════════════════════════════════════════════╣
║  ┏━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━┓   ║
║  ┃                                         ┃   ║  ← Hero Image
║  ┃      [IMAGE RECETTE HEADER]            ┃   ║
║  ┃      (Full width, ~250dp height)       ┃   ║
║  ┃                                         ┃   ║
║  ┗━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━┛   ║
║                                                 ║
║  Omelette aux légumes                          ║  ← Titre (H1)
║  ⭐ Facile • ⏱️ 25 min • 👥 2 personnes        ║  ← Metadata
║                                                 ║
║  Une omelette simple et savoureuse avec des    ║  ← Description
║  légumes frais, parfaite pour un repas...      ║
║                                                 ║
║  ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━   ║
║                                                 ║
║  📋 INGRÉDIENTS (6)                            ║  ← Section
║                                                 ║
║  ✅  4 oeufs                                   ║  ← Liste ingrédients
║  ✅  2 tomates moyennes                        ║    avec status
║  ✅  1 courgette                               ║
║  ✅  50ml de lait                              ║
║  ❌  1 pincée de sel                           ║
║  ❌  1 pincée de poivre                        ║
║                                                 ║
║  ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━   ║
║                                                 ║
║  👨‍🍳 PRÉPARATION (5 étapes)                    ║  ← Section
║                                                 ║
║  ┌─────────────────────────────────────────┐   ║
║  │ 1  Laver et couper les tomates et la    │   ║  ← Step card
║  │    courgette en petits dés               │   ║
║  │    ⏱️ 5 min                              │   ║
║  └─────────────────────────────────────────┘   ║
║                                                 ║
║  ┌─────────────────────────────────────────┐   ║
║  │ 2  Dans un bol, battre les oeufs avec   │   ║
║  │    le lait, le sel et le poivre          │   ║
║  │    ⏱️ 2 min                              │   ║
║  └─────────────────────────────────────────┘   ║
║                                                 ║
║  ...                                           ║
║                                                 ║
║  ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━   ║
║                                                 ║
║  🔥 INFORMATIONS NUTRITIONNELLES               ║  ← Section (bonus)
║  245 kcal • 18g protéines • 8g glucides        ║
║                                                 ║
╚═════════════════════════════════════════════════╝
```

#### Composants
- **Hero Image** : Image pleine largeur avec overlay gradient
- **TopBar transparent** : Apparaît au scroll
- **Metadata Row** : Icônes + texte pour infos clés
- **Ingrédients** :
  - Checkbox (✅ disponible / ❌ manquant)
  - Quantité + nom
- **Steps** : Cards numérotées avec durée optionnelle
- **ScrollView** : Contenu entier scrollable

#### Comportements
- Scroll : TopBar apparaît progressivement
- Ingrédients manquants : affichés en rouge
- Boutons header :
  - ♡ Favoris (désactivé MVP)
  - ⋮ Menu (partage, etc. - désactivé MVP)
- Pas d'action finale dans MVP (bouton "Commencer" grisé)

---

## 3. Design System (Guidelines)

### 3.1 Palette de couleurs

**Couleurs principales** :
```
Primary       : #4CAF50  (Vert - nourriture fraîche)
Primary Dark  : #388E3C
Primary Light : #C8E6C9

Secondary     : #FF9800  (Orange - chaleur cuisine)
Secondary Dark: #F57C00
Secondary Light:#FFE0B2

Background    : #FFFFFF  (Blanc)
Surface       : #F5F5F5  (Gris très clair)
Error         : #F44336  (Rouge)
Success       : #4CAF50  (Vert)
Warning       : #FFC107  (Jaune)
```

**Couleurs texte** :
```
Text Primary   : #212121  (Noir quasi pur)
Text Secondary : #757575  (Gris moyen)
Text Disabled  : #BDBDBD  (Gris clair)
```

### 3.2 Typographie

**Scale de texte** :
```
H1 (Titres principaux)    : 24sp, Bold
H2 (Sous-titres)          : 20sp, SemiBold
H3 (Sections)             : 18sp, SemiBold
Body (Texte standard)     : 16sp, Regular
Caption (Métadonnées)     : 14sp, Regular
Button                    : 16sp, Medium, ALL CAPS
```

**Police** : Roboto (système Android par défaut)

### 3.3 Espacements

**Padding/Margin** :
```
XXS : 4dp
XS  : 8dp
S   : 12dp
M   : 16dp  ← Standard pour la plupart des cas
L   : 24dp
XL  : 32dp
XXL : 48dp
```

### 3.4 Composants UI

**Boutons** :
- **Primary** : Fond Primary, texte blanc, elevation 2dp
- **Secondary** : Outlined, texte Primary, no elevation
- **Text Button** : Texte Primary, no background

**Cards** :
- Background Surface
- Border radius : 12dp
- Elevation : 2dp
- Padding interne : 16dp

**Chips** :
- Height : 32dp
- Border radius : 16dp
- Padding horizontal : 12dp

**Images** :
- Border radius : 8dp (cards) / 12dp (large)
- Placeholder : couleur Surface avec icône centrée

---

## 4. États et transitions

### 4.1 États de chargement

**Loading states** :
- **Skeleton screens** : préféré pour liste recettes
- **Circular progress** : pour actions ponctuelles (analyse)
- **Linear progress** : pour top bar (upload futur)

**Messages** :
```
Analyse en cours...
Recherche de recettes...
Chargement...
```

### 4.2 États d'erreur

**Types d'erreurs** :
- **Erreur réseau** : "Impossible de charger les données"
- **Erreur caméra** : "Permission caméra requise"
- **Aucun résultat** : "Aucune recette trouvée avec ces ingrédients"
- **Erreur analyse** : "Impossible d'analyser l'image"

**Affichage** :
- Snackbar pour erreurs temporaires
- Full screen error state pour échecs majeurs
- Bouton "Réessayer"

### 4.3 Animations

**Transitions d'écrans** :
- Slide horizontal (navigation standard)
- Fade + Scale (dialog/modal)

**Micro-interactions** :
- Ripple effect sur boutons/cards
- Scale animation sur chips au tap
- Fade in pour images chargées
- Slide up pour bottom sheets

---

## 5. Gestion des permissions

### 5.1 Permission caméra

**Flow** :
```
1. App launch
   ↓
2. Check permission
   ↓
   ├─ Accordée → Afficher preview
   │
   └─ Non accordée
      ↓
      3. Afficher rationale (si déjà refusée)
         ↓
         4. Request permission
            ↓
            ├─ Accordée → Afficher preview
            │
            └─ Refusée définitivement
               ↓
               5. Afficher état bloqué avec bouton "Paramètres"
```

**UI état bloqué** :
```
╔═════════════════════════════════════════════════╗
║                                                 ║
║              📷                                 ║
║                                                 ║
║         Permission requise                      ║
║                                                 ║
║  Cette application a besoin d'accéder à        ║
║  votre caméra pour scanner votre frigo.        ║
║                                                 ║
║  ┌─────────────────────────────────────────┐   ║
║  │      Ouvrir les paramètres             │   ║
║  └─────────────────────────────────────────┘   ║
║                                                 ║
╚═════════════════════════════════════════════════╝
```

---

## 6. Scénarios d'usage

### 6.1 Scénario nominal (Happy Path)

**Contexte** : Utilisateur veut cuisiner avec ce qu'il a dans son frigo

**Steps** :
1. Lance l'app
2. Voit l'écran caméra directement
3. Pointe vers le frigo, prend photo
4. Voit 4 ingrédients détectés automatiquement
5. Ajoute "sel" manuellement
6. Tape "Trouver des recettes"
7. Voit 12 recettes suggérées, triées par compatibilité
8. Filtre sur "Plat" → reste 8 recettes
9. Sélectionne "Omelette aux légumes" (95% match)
10. Consulte la recette complète
11. Note qu'il manque juste du poivre
12. Commence à cuisiner

**Durée estimée** : < 2 minutes

---

### 6.2 Scénario avec correction

**Contexte** : IA détecte mal certains ingrédients

**Steps** :
1. Lance l'app et prend photo
2. Voit 5 ingrédients, mais 1 est incorrect ("Aubergine" détectée au lieu de "Poivron")
3. Supprime "Aubergine" (tap sur ✗)
4. Ajoute "Poivron" manuellement
5. Continue normalement

**Apprentissage** : L'utilisateur peut corriger facilement

---

### 6.3 Scénario échec analyse

**Contexte** : Photo floue ou frigo vide

**Steps** :
1. Prend photo de frigo vide ou floue
2. Analyse retourne 0 ingrédients
3. Voit message : "Aucun ingrédient détecté. Assurez-vous que la photo est nette."
4. Bouton "Reprendre photo"
5. Re-tente avec meilleure photo
6. Succès cette fois

**Résilience** : L'app gère les échecs gracefully

---

## 7. Accessibilité (A11y)

### 7.1 Checklist MVP

**Minimum requis** :
- ✅ Content descriptions sur toutes les images/icônes
- ✅ Contraste texte/fond ≥ 4.5:1 (WCAG AA)
- ✅ Taille tactile minimum 48dp x 48dp
- ✅ Labels sur tous les champs
- ✅ États focus clairement visibles
- ✅ Support TalkBack (lecteur d'écran Android)

**Exemples** :
```kotlin
// Image avec content description
Image(
    painter = painterResource(R.drawable.recipe),
    contentDescription = "Photo d'une omelette aux légumes"
)

// Bouton accessible
Button(
    onClick = { },
    modifier = Modifier.semantics {
        contentDescription = "Trouver des recettes avec ces ingrédients"
    }
) {
    Text("Trouver des recettes")
}
```

---

## 8. Performance

### 8.1 Métriques cibles

**App startup** : < 2 secondes (cold start)
**Navigation** : < 300ms entre écrans
**Analyse image** : 1-2 secondes (mock)
**Chargement liste** : < 1 seconde
**Scroll liste** : 60 FPS constant

### 8.2 Optimisations

**Images** :
- Compression JPEG/WebP
- Tailles multiples (thumbnails vs full)
- Cache mémoire + disque (Coil)
- Lazy loading

**Listes** :
- LazyColumn avec keys
- Item recomposition minimale
- Placeholders pendant chargement

---

## 9. Cas limites (Edge Cases)

### 9.1 Données

| Cas | Comportement |
|-----|--------------|
| 0 ingrédient détecté | Message erreur + bouton reprendre |
| 1 seul ingrédient | Affiche recettes (même avec low match score) |
| 20+ ingrédients | Scroll horizontal pour chips |
| 0 recette trouvée | État vide avec illustration |
| 100+ recettes | Pagination (ou limit 50 pour MVP) |
| Nom recette très long | Ellipsis après 2 lignes |
| Image recette manquante | Placeholder avec icône |

### 9.2 Réseau

| Cas | Comportement |
|-----|--------------|
| Pas de connexion | MVP : pas d'impact (tout mock local) |
| Timeout API | Dialog erreur + retry |
| Réponse malformée | Log error + message générique |

### 9.3 Appareil

| Cas | Comportement |
|-----|--------------|
| Pas de caméra | Message + bouton "Importer depuis galerie" |
| Stockage plein | Message erreur lors capture photo |
| Batterie faible | Pas de comportement spécial (MVP) |
| Rotation écran | États préservés (ViewModel) |

---

## 10. Checklist de validation Phase 0

Avant de passer à l'implémentation :

- ✅ Architecture MVVM définie et validée
- ✅ Structure de dossiers claire
- ✅ 4 écrans détaillés avec wireframes
- ✅ Modèles de données spécifiés
- ✅ Contrats API mockés (JSON)
- ✅ Flux utilisateur complet
- ✅ Design system défini (couleurs, typo, espacements)
- ✅ États UI et erreurs anticipés
- ✅ Permissions identifiées
- ✅ Edge cases listés
- ✅ Accessibilité considérée
- ✅ Scope MVP respecté (pas de features V2)

---

## Prochaine étape

**Phase 1** : Initialisation du projet Android Studio avec :
- Configuration Gradle (Kotlin DSL)
- Dépendances (Hilt, Compose, CameraX, etc.)
- Structure de packages selon architecture définie
- Theme Compose avec couleurs/typos
- Navigation skeleton

**Prêt à démarrer le développement ! 🚀**
