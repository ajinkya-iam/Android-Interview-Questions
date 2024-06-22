# Android-Interview-Questions

## Kotlin 

### 1. Advantage of `const` keyword ? 
- Const value replaced at complie time, there is no overhead at runtime.
- Const values are immutable, ensuring that they cannot be modified, which can prevent bugs.
- Const values can be accessed from anywhere in the codebase without the need for object instantiation.
- Using `const` for fixed values like API endpoints or configuration settings makes the code more readable and easier to understand.
  
  ### Disadvantage
- Const can only be used with primitive types and string literals. It cannot be used with complex data types or custom objects.
- Const can only be declared at the top level or inside objects, not inside functions or classes.
- The value assigned to const must be known at compile-time, which limits its use cases.

  ### Example

   `const val MAX_USER_COUNT = 100`
  

### 2. `lateinit` keyword ?
  - `lateinit` in kotlin is useful scenario when we do not want to initialize a variable at the time of the declaration and want to
    initialize it at some later point in time, but we make sure that we initialize it before use.
  - `private lateinit var hello: HelloWorld`
  - `lateinit` is non-nullable


### 3. `lazy` keyword ?
 - `lazy` in Kotlin is useful in a scenario when we want to create an object inside a class, but that object creation is expensive and
   that might lead to a delay in the creation of the object that is dependent on that expensive object.
 - `private val mentor: Mentor by lazy { Mentor() }`
 - Object will get initialized only when it is accessed for the first time, else it will not get initialized.
 - Can be only used with the val keyword, hence read-only property

### 4. `inline` function ?
In Kotlin, the inline keyword is used to optimize higher-order functions by reducing the overhead associated with function calls, particularly for lambda expressions. 
When a function is marked with the inline modifier, the compiler replaces the function call with the actual code of the function, thus eliminating the call overhead and potentially enabling further optimizations.

When the function code is very small, it's a good idea to make the function inline.

```kotlin
fun guide() {
    print("guide start")
    teach()
    print("guide end")
}

inline fun teach() {
    print("teach")
}
```

### 4. Sealed Class ?
- `sealed class` is a class that restricts the inheritance hierarchy. It can have a limited set of subclasses defined within the same file.
- A sealed class itself is always an abstract class, and as a result

``` kotlin
sealed class SealedExample<T> {
    data class Success<T>(val data: T) : SealedExample<T>()
    data class Error<T>(val error: T) : SealedExample<T>()
}

class SealedExampleHandler {

    fun <T> handleExample(example: SealedExample<T>) {
        when (example) {
            is SealedExample.Success -> {
                println("Success with data: ${example.data}")
            }
            is SealedExample.Error -> {
                println("Error with message: ${example.error}")
            }
        }
    }
}

fun main() {
    val successExample: SealedExample<String> = SealedExample.Success("Operation successful")
    val errorExample: SealedExample<String> = SealedExample.Error("Something went wrong")

    val handler = SealedExampleHandler()
    handler.handleExample(successExample)
    handler.handleExample(errorExample)
}
```

