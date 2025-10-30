# 📱👈🏻  Les Gestures en SwiftUI

[Slide Canva](https://www.canva.com/design/DAG3LQ15Xtc/cVccm4Gj2o4wZ7OMz8ts2Q/view?utm_content=DAG3LQ15Xtc&utm_campaign=designshare&utm_medium=link2&utm_source=uniquelinks&utlId=h9d4a6404e6)

Andrei, Edilene, Florian, Séverine, Stacy

<video width="720" height="340" controls>
    <source src="NotebookKLM.mov" type="video/mp4">
    Your browser does not support the video tag.
</video>  

Un Gesture en SwiftUI est une interaction `tactile` spécifique et intentionnelle faite par `l'utilisateur`.  

Elles permettent de détecter et de réagir aux interactions physiques de l'utilisateur avec les vues:  
- taps
- glissements
- pincements
- rotations
- etc...

*Le composant `Button` intègre déjà sa propre mécanique de gesture. (un seul tap)*.  

---

## 1. Fonctionnement
Le principe est d'**attacher** un objet `Gesture` à une vue à l'aide du modificateur de vue **`.gesture()`**.

L'approche de SwiftUI est **déclarative et réactive** : vous déclarez quel geste doit être reconnu, et la vue se met à jour automatiquement en modifiant une `@State`.

### Cycle de Vie du Geste
* **`onChanged`** : Déclenché de manière répétée pendant que le geste est en cours (utile pour suivre un mouvement comme un glissement).
* **`onEnded`** : Déclenché lorsque l'utilisateur met fin au geste (par exemple, en relâchant le doigt).

---
## 2. Les Types de Gestes Intégrés

SwiftUI fournit cinq gestes prédéfinis (`built-in`) pour couvrir les interactions les plus courantes :

| Type de Geste | Interaction Détectée | Description & Valeur de sortie |
| :--- | :--- | :--- |
| **`TapGesture`** | Un ou plusieurs taps (clics). | Simple reconnaissance, sans état continu. |
| **`LongPressGesture`** | Un tap maintenu pendant une durée spécifique. | Peut être utilisé pour afficher un menu contextuel. |
| **`DragGesture`** | Un glissement ou un déplacement continu. | Fournit la propriété clé `value.translation` pour le déplacement. |
| **`MagnificationGesture`** | Mouvement de pincement à deux doigts. | Fournit la propriété `value.scale` (facteur de zoom). |
| **`RotationGesture`** | Mouvement de rotation à deux doigts. | Fournit la propriété `value.rotation` (angle de rotation). |

---

## 3. Gestion des Interactions
Les possibilités des gestes sont étendues via des raccourcis pratiques et des mécanismes de composition.  

Pour les cas très simples, on utilise des modificateurs de vue qui encapsulent le geste :  

| Modificateur (Raccourci) | Équivalent `Gesture` Complet | Utilisation |
| :--- | :--- | :--- |
| **`.onTapGesture { ... }`** | Simplifie l'utilisation du `TapGesture`. | Tap simple. |
| **`.onTapGesture(count: 2) { ... }`** | Version simplifiée pour la détection. | Double-tap. |

### La Composition pour les Gestes Avancées
Le mécanisme de composition permet de combiner les gestes de base pour créer une logique d'interaction unique et plus complexe.

| Modificateur de Composition | But | Exemple |
| :--- | :--- | :--- |
| **`.simultaneously(with: )`** | **Reconnaissance Simultanée** | Permet de **Drag** (glisser) *et* de **Magnify** (pincer) un élément en même temps. |
| **`.sequenced(before: )`** | **Reconnaissance Séquentielle** | Exige un ordre précis : le Geste 1 doit réussir avant que le Geste 2 puisse commencer (ex: **Long Press** puis **Drag**). |
| **`.exclusively(before: )`** | **Reconnaissance Prioritaire** | Permet de donner la priorité au Geste 1. S'il ne réussit pas, le système tente le Geste 2. |

---

## 4. Exemple Pratique : 
## Rendre un Élément Déplaçable
L'exemple classique du **`DragGesture`** pour déplacer un élément à l'écran :

```swift

import SwiftUI

struct DraggableRectangle: View {
    @State private var offset: CGSize = .zero

    var body: some View {
        Rectangle()
            .fill(Color.blue)
            .frame(width: 100, height: 100)
            .offset(offset)
            .gesture(
                DragGesture()
                    .onChanged { value in
                        offset = value.translation
                    }
                    .onEnded { _ in
                        withAnimation {
                            offset = .zero 
                        }
                    }
            )
    }
}

#Preview {
    DraggableRectangle()
}

```

---

### 5.1. Exemples:

- [DrageGestureDemo](https://flourdau.github.io/GestureSwiftUI/pages/DrageGestureDemo)  
- [PinchDemo](https://flourdau.github.io/GestureSwiftUI/pages/PinchDemo)  
- [RotationDemo](https://flourdau.github.io/GestureSwiftUI/pages/RotationDemo)  
- [SimultaneousGestureExample](https://flourdau.github.io/GestureSwiftUI/pages/SimultaneousGestureExample)  
- [LongPressDemo](https://flourdau.github.io/GestureSwiftUI/pages/LongPressDemo)  
- [TapGestureDemo](https://flourdau.github.io/GestureSwiftUI/pages/TapGestureDemo)  

---

## 5. Ressources: 
- [Documentation Officielle Apple (Gestures API)](https://developer.apple.com/documentation/swiftui/gestures)  
- [Tutoriel Apple (Ajouter de l'Interactivité)](https://developer.apple.com/documentation/swiftui/adding-interactivity-with-gestures)  

---

<iframe width="560" height="315" src="https://www.youtube.com/embed/Kl_3xrZBEFY?si=672qP1lRQ8g4FysF&t=42" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>

---

## 6. Outils:
- Canva
- Gemini & co
- GitHub 
- NoteBookKLM
- VSCode 
