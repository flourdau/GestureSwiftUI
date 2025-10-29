
#   PinchDemo

<video width="320" height="240" controls>
    <source src="PinchDemo.mov" type="video/mp4">
    Your browser does not support the video tag.
</video>

```Swift
import SwiftUI

struct PinchDemo: View {
    @State private var scale: CGFloat = 1.0
    
    var body: some View {
        Image("image") //Ajouter votre image dans les asset...
            .resizable()
            .scaledToFit()
            .frame(width: 300, height: 300)
            .scaleEffect(scale)
            .gesture(
                MagnificationGesture()
                    .onChanged { value in
                        self.scale = value
                    }
                    .onEnded { _ in
                        // garder le facteur actuel ou le remettre à 1.0
                        // self.scale = 1.0
                    }
            )
            .border(Color.gray, width: 1)
    }
}

struct PinchDemo_Previews: PreviewProvider {
    static var previews: some View {
        PinchDemo()
            .previewLayout(.sizeThatFits)
            .padding()
    }
}

```