
#   TapGestureDemo

<video width="320" height="240" controls>
    <source src="TapGestureDemo.mov" type="video/mp4">
    Your browser does not support the video tag.
</video>

```Swift

import SwiftUI

struct TapGestureDemo: View {
    @State private var compteur = 0
    @State private var message = "Touchez l'écran"
    
    var body: some View {
        VStack(spacing: 30) {
            Text(message)
                .font(.title)
            
            Text("Touches: (compteur)")
                .font(.headline)
            
            Rectangle()
                .fill(Color.blue)
                .frame(width: 150, height: 150)
                .onTapGesture {
                    compteur += 1
                    message = "Toucher simple!"
                }
            
            Rectangle()
                .fill(Color.green)
                .frame(width: 150, height: 150)
                .onTapGesture(count: 2) {
                    compteur += 2
                    message = "Double toucher!"
                }
        }
    }
}

#Preview {
    TapGestureDemo()
}

```