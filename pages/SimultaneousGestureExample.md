
#   SimultaneousGestureExample

<video width="320" height="240" controls>
    <source src="SimultaneousGestureExample.mov" type="video/mp4">
    Your browser does not support the video tag.
</video>

```Swift
import SwiftUI

struct SimultaneousGestureExample: View {
    @State private var currentScale: CGFloat = 1.0
    @State private var currentRotation: Angle = .zero

    var body: some View {
        
        RoundedRectangle(cornerRadius: 20)
            .fill(Color.blue)
            .frame(width: 200, height: 200)
            .scaleEffect(currentScale)
            .rotationEffect(currentRotation)
            .gesture(
                MagnificationGesture()
                    .onChanged { value in
                        self.currentScale = value
                    }
                    .simultaneously(with:
                    
                    RotationGesture()
                        .onChanged { value in
                            self.currentRotation = value
                        }
                )
//                .onEnded { _ in }
            )
    }
}

#Preview {
    SimultaneousGestureExample()
}

```