
#   DrageGestureDemo

<video width="320" height="240" controls>
    <source src="DragGestureDemo.mov" type="video/mp4">
    Your browser does not support the video tag.
</video>  

```Swift

import SwiftUI

struct DragGestureDemo: View {
    @State private var position = CGSize.zero
    @State private var estEnTrainDeGlisser = false

    var body: some View {
        VStack {
            Text("Glissez le cercle")
                .font(.headline)

            Spacer()

            Circle()
                .fill(estEnTrainDeGlisser ? Color.orange : Color.blue)
                .frame(width: 100, height: 100)
                .offset(x: position.width, y: position.height)
                .gesture(
                    DragGesture()
                        .onChanged { valeur in
                            estEnTrainDeGlisser = true
                            position = valeur.translation
                        }
                        .onEnded { valeur in
                            estEnTrainDeGlisser = false
                            position = .zero

                        }
                )

            Spacer()

            Text("X: (Int(position.width)), Y: (Int(position.height))")
                .foregroundColor(.gray)
        }
    }
}

#Preview {
    DragGestureDemo()
}
```