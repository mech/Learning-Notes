# Kotlin

```kotlin
// Unlike class, object can't have any constructor
object Singleton {
  var s: String? = null
}

fun String.lengthIsEven(): Boolean = length % 2 == 0

var isEven = "someString".lengthIsEven()

// Group object initialization statement like Ruby's code block
val textView = TextView(this).apply {
  visibility = View.VISIBLE
  text = "test"
}

// when() replaces switch
fun parseResponse(response: Response?) = when (response?.code()) {
  null -> throw HTTPException("Something bad happened")
  200, 201 -> parse(response.body())
  in 400..499 -> throw HTTPException("Invalid request")
  in 500..599 -> throw HTTPException("Server error")
  else -> throw HTTPException("Error! Code ${response.code()}")
}
```

For comparison, Swift function is like so:

```swift
func greet(name: String? = "Unnamed") -> String {
}
```