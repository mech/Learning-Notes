# SwiftUI

* [About SwiftUI](https://github.com/Juanpe/About-SwiftUI)

Just like in design tools and React, SwiftUI is component-based.

## HStack and VStack

Container like a VStack can be extract into Subview to create more components.

No more Auto Layout constraints? The way you create layouts in SwiftUI is more akin to Flexbox with a few key differences.

```swift
ComponentView(props)
  .modifierOne(show ? Color.red : Color("myRed"))
  .modifierTow()
  .cornerRadius(10)
```

The direction of the stack is very clear. You can add alignment and additional styling later.

```swift
VStack {
  VStack {
    Text("UI")
      .font(.title)
      .fontWeight(.bold)
    Text("Design")
      .color(.white)
  }
  Image("Background")
}
.cornerRadius(10)
```

```js
<VStack
  cornerRadius={10}
  padding="horizontal"
  space="between"
  width="340"
  height="220"
  minWidth="100"
  gap={20}
>
  ...
</VStack>

<Text scale="title or headline"></Text>
```