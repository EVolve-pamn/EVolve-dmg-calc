# Evolve - Pokémon damage calculator

Android app, developed in Kotlin.

## Main Screens & Scope
1. **Pokémon Box (Colección):** Implements local storage imitating the official games' PC storage. Loads data and sprites from a remote API *on first launch* and caches them locally using Room.
2. **Teambuilder:** Allows creating a team of up to 6 Pokémon, computing and displaying type weaknesses, resistances, and offensive attack coverage dynamically.
3. **Damage Calculator:** Selects two Pokémon (attacker and defender) from the box/team to calculate detailed damage output based on stats, types, and moves.

## Technical Stack
- **Language:** Kotlin 2.2.10
- **UI:** Jetpack Compose + Material 3, Navigation Compose 2.9.8
- **Build System:** AGP 9 with Kotlin built-in, Gradle 9.6.0
- **Architecture:** MVVM (Model-View-ViewModel) + StateFlow, Lifecycle 2.10.0
- **Persistence:** Room 2.8.5 with KSP 2.3.x (Strictly no KAPT)
- **Image Loading:** Coil 3.3.0 (coordinates: `io.coil-kt.coil3`, imports `coil3.compose.*`)
- **Base Package:** `com.pamn.evolve`

---

## Rules and Constraints for AI Agents

To ensure code quality, maintainability, and alignment with academic evaluation criteria (especially regarding personal comprehension and defense), AI assistants must strictly follow these rules:

### 1. Architectural Integrity (MVVM & Clean Boundaries)
- **Strict Separation of Concerns:** ViewModels must not contain Android UI framework references (`android.*` contexts, Composables, etc.). Composables must remain stateless where possible (state hoisting).
- **Data Flow:** UI observes state exclusively via `StateFlow`. UI events must trigger ViewModel functions cleanly.
- **No Direct DB Access from UI:** All database interactions (Room) and network calls must be abstracted through Repository classes.

### 2. Room & Database Guidelines
- **KSP Compliance:** Never suggest or write code using KAPT; always use KSP (`ksp(...)`) for Room compiler dependencies.
- **Entities & DTOs:** Keep database entities clean. Handle API-to-Entity mapping explicitly using extension functions or mapper classes.
- **Offline-First Strategy:** Database queries must run on Dispatchers.IO (handled via Room's built-in suspend functions or Flows).

### 3. Jetpack Compose Best Practices
- **Recomposition Control:** Avoid unnecessary recompositions by using immutable data structures or stable state holders.
- **Navigation:** Use type-safe navigation arguments where applicable in Navigation Compose 2.9.8.
- **Material 3 Consistency:** Respect M3 color schemes, typography, and component guidelines.

### 4. Code Generation & Explanation Constraints
- **Explanations Required:** Whenever the AI generates complex logic (such as type-effectiveness multipliers in the damage calculator or coverage algorithms in the teambuilder), it must provide a brief technical breakdown explaining *how* it works so the team can defend it during the oral presentation.
- **No Mock Magic without Fallbacks:** If generating API integration code (e.g., PokeAPI), include robust error handling (try/catch, loading states, empty states) since offline execution without prior cache must be safely handled.
- **Dependency Versions:** Never introduce third-party libraries outside the defined stack without explicit team approval and justification for the memory report.
