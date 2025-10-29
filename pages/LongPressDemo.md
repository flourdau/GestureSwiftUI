
#   LongPressDemo

<video width="320" height="240" controls>
    <source src="LongPressDemo.mov" type="video/mp4">
    Your browser does not support the video tag.
</video>

```Swift
import SwiftUI

struct LongPressDemo: View {
    @State private var progres = 0.0
    @State private var complete = false
    
    var body: some View {
        VStack {
            Circle()
                .fill(complete ? Color.green : Color.blue)
                .frame(width: 200, height: 200)
                .scaleEffect(complete ? 1.2 : 1.0)
                .overlay(
                    Text(complete ? "Complet!" : "Appuyez")
                        .foregroundColor(.white)
                        .font(.title)
                )
                .onLongPressGesture(
                    minimumDuration: 2.0,
                    pressing: { enCoursDePression in
                        if enCoursDePression {
                            withAnimation(.linear(duration: 2.0)) {
                                progres = 1.0
                            }
                        } else {
                            progres = 0.0
                        }
                    },
                    perform: {
                        withAnimation {
                            complete = true
                        }
                        DispatchQueue.main.asyncAfter(deadline: .now() + 1) {
                            withAnimation {
                                complete = false
                            }
                        }
                    }
                )
            
            ProgressView(value: progres)
                .padding()
        }
        .padding()
    }
}

#Preview {
    LongPressDemo()
}

```