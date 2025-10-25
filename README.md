# 📱👈🏻 Maîtriser les Gestures (Gestes) en SwiftUI

Les **Gestures** (Gestes) sont un protocole fondamental en **SwiftUI** qui permet de détecter et de réagir aux interactions physiques de l'utilisateur avec les vues (taps, glissements, pincements, rotations, etc.).  
Le composant Button intègre déja toute la mécanique. Mais on peut gérer et paramétrer plus en détails...
## 1. Concept Fondamental et Fonctionnement

Le principe est d'**attacher** un objet `Gesture` à une vue à l'aide du modificateur de vue **`.gesture()`**.

L'approche de SwiftUI est **déclarative et réactive** : vous déclarez quel geste doit être reconnu, et la vue se met à jour automatiquement en modifiant une `@State`.

### Cycle de Vie du Geste

Un geste passe typiquement par trois états gérés par des closures :

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

## 3. Gestion des Interactions Avancées

Les possibilités des gestes sont étendues via des raccourcis pratiques et des mécanismes de composition.

### 3.1. Les Méthodes de Commodité (*Convenience Methods*)

Pour les cas très simples, on utilise des modificateurs de vue qui encapsulent le geste :

| Modificateur (Raccourci) | Équivalent `Gesture` Complet | Utilisation |
| :--- | :--- | :--- |
| **`.onTapGesture { ... }`** | Simplifie l'utilisation du `TapGesture`. | Tap simple. |
| **`.onTapGesture(count: 2) { ... }`** | Version simplifiée pour la détection. | Double-tap. |

### 3.2. La Composition pour les Gestes Complexes

Le mécanisme de composition permet de combiner les gestes de base pour créer une logique d'interaction unique et plus complexe.

| Modificateur de Composition | But | Exemple |
| :--- | :--- | :--- |
| **`.simultaneously(with: )`** | **Reconnaissance Simultanée** | Permet de **Drag** (glisser) *et* de **Magnify** (pincer) un élément en même temps. |
| **`.sequenced(before: )`** | **Reconnaissance Séquentielle** | Exige un ordre précis : le Geste 1 doit réussir avant que le Geste 2 puisse commencer (ex: **Long Press** puis **Drag**). |
| **`.exclusively(before: )`** | **Reconnaissance Prioritaire** | Permet de donner la priorité au Geste 1. S'il ne réussit pas, le système tente le Geste 2. |

---

## 4. Exemple Pratique : Rendre un Élément Déplaçable

L'exemple classique du **`DragGesture`** pour déplacer un élément à l'écran :

```swift

import SwiftUI

struct DraggableRectangle: View {
    // Variable d'état pour suivre la position du décalage
    @State private var offset: CGSize = .zero

    var body: some View {
        Rectangle()
            .fill(Color.blue)
            .frame(width: 100, height: 100)
            .offset(offset) // Applique le décalage (déplacement) à la vue

            // Définition du geste DragGesture
            .gesture(
                DragGesture()
                    .onChanged { value in
                        // En temps réel, on met à jour l'offset avec la translation du doigt
                        offset = value.translation
                    }
                    .onEnded { _ in
                        // À la fin du glissement, on réinitialise (ou on ancre l'élément)
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


### 5. Ressources pour Aller Plus Loin 🔗

Pour approfondir votre compréhension des gestes en SwiftUI, ces ressources techniques sont essentielles :

Liens: 
- [Documentation Officielle Apple (Gestures API)](https://developer.apple.com/documentation/swiftui/gestures)
- [Tutoriel Apple (Ajouter de l'Interactivité)](https://developer.apple.com/documentation/swiftui/adding-interactivity-with-gestures)
- [Vidéo](https://youtu.be/Kl_3xrZBEFY?si=GMxT4FDF2jc_AKO4&t=42)
