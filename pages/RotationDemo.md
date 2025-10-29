
#   RotationDemo

<video width="320" height="240" controls>
    <source src="RotationDemo.mov" type="video/mp4">
    Your browser does not support the video tag.
</video>

```Swift

import SwiftUI

struct RotationDemo: View {
    @State private var angle = Angle.zero
    @State private var dernierAngle = Angle.zero
    
    var body: some View {
        VStack {
            Text("Rotation: \(String(format: "%.0f", angle.degrees))°")
                .font(.headline)
                .padding()
            
            RoundedRectangle(cornerRadius: 20)
                .fill(
                    LinearGradient(
                        colors: [.purple, .pink],
                        startPoint: .topLeading,
                        endPoint: .bottomTrailing
                    )
                )
                .frame(width: 200, height: 200)
                .rotationEffect(angle)
                .shadow(radius: 10)
                .gesture(
                    RotationGesture()
                        .onChanged { valeur in
                            angle = dernierAngle + valeur
                        }
                        .onEnded { valeur in
                            dernierAngle = angle
                        }
                )
            
            Button("Réinitialiser") {
                withAnimation(.spring()) {
                    angle = .zero
                    dernierAngle = .zero
                }
            }
            .buttonStyle(.bordered)
            .padding()
        }
    }
}

#Preview {
    RotationDemo()
}

```