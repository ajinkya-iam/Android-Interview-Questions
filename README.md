# Android-Interview-Questions

## Basic Of Kotlin

### 1. Variables
Kotlin has two types of variables:

- `val`: Immutable (read-only) variables. You can’t reassign them.
- `var`: Mutable variables that can be changed.

``` kotlin
val name = "Kotlin"  // Read-only
var age = 10         // Can be reassigned
```

### 2. Functions
In Kotlin, functions are defined using the `fun` keyword.

``` kotlin
fun greet() {
    println("Hello, Kotlin!")
}

fun add(a: Int, b: Int): Int {
    return a + b
}
```

### 3. Control Flow
Kotlin uses standard control flow structures like `if`, `when`, `for`, and `while`.

- `if-else`:

```kotlin
val max = if (a > b) a else b
```
- `when`: Kotlin’s alternative to `switch` statements.
```kotlin
when (x) {
    1 -> print("One")
    2 -> print("Two")
    else -> print("Unknown")
}
```

### 4. Null Safety
Kotlin's type system is designed to eliminate null pointer exceptions by distinguishing between nullable and non-nullable types.

- Use `?` to mark a variable as nullable.
- Use `?.` to safely access nullable types.
- Use `!!` to force a nullable type to a non-null type (may cause crash if null).


```kotlin
var name: String? = "Kotlin"  // Nullable
name = null

println(name?.length)  // Safe call
println(name!!.length) // Throws exception if name is null

```

### 5. Classes and Objects
Kotlin supports object-oriented programming with classes and objects.

```kotlin
class Person(val name: String, var age: Int) {
    fun display() {
        println("$name is $age years old.")
    }
}

val person = Person("John", 25)
person.display()  // John is 25 years old.
```

### 6. Data Classes
Data classes are used to hold data and automatically generate useful methods like `toString()`, `equals()`, and `hashCode()`.

```kotlin
data class User(val name: String, val age: Int)

val user = User("Alice", 30)
println(user)  // User(name=Alice, age=30)
```
### 7. Collections
Kotlin has powerful collection types like `List`, `Set`, and `Map`.

```kotlin
val numbers = listOf(1, 2, 3, 4)
val mutableNumbers = mutableListOf(1, 2, 3)

val userMap = mapOf("name" to "Alice", "age" to 30)
```

### 8. Lambdas
Kotlin supports functional programming with lambda expressions.

```kotlin
val sum = { a: Int, b: Int -> a + b }
println(sum(10, 20))  // 30
```

### 9. Extension Functions
You can add functions to existing classes without modifying them.

```kotlin
fun String.print() {
    println(this)
}

"Hello, World!".print()  // Prints: Hello, World!
```

-----------------------------------------------------------------------------------------------------------------------------------

## 1. Data Class
A data class in Kotlin is a class specifically designed to hold data. Kotlin provides several automatically generated functions for data classes, which helps reduce boilerplate code. These include methods like `toString()`, `equals()`, `hashCode()`, and `copy()`.
### Key Features of a Data Class:

1. Primary Constructor with Parameters: A data class must have at least one parameter in its primary constructor. These parameters define the properties of the data class.

2. Automatically Generated Methods:
- `toString()`: Provides a string representation of the object for easier debugging.
- `equals()`: Checks if two objects are equal based on their property values.
- `hashCode()`: Provides a unique code based on the property values, used for hash-based collections.
- `copy()`: Creates a copy of the object with the option to modify some properties.

### Example : 

```kotlin
data class User(val name: String, val age: Int)
```

With this simple definition, Kotlin automatically provides useful methods for this class:

```kotlin
val user1 = User("Alice", 30)
val user2 = User("Alice", 30)

// toString()
println(user1)  // Output: User(name=Alice, age=30)

// equals()
println(user1 == user2)  // Output: true

// copy()
val user3 = user1.copy(age = 35)
println(user3)  // Output: User(name=Alice, age=35)
```

### Use Case:
Data classes are ideal when you need to store simple data structures like user details, configuration settings, or any other group of values where you care more about storing data than behavior.

They reduce boilerplate code while ensuring the class has useful, predefined functionality!




-----------------------------------------------------------------------------------------------------------------------------------

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

### 5. `init` block ?
- In Kotlin, an init block is used to initialize an object. It runs as part of the primary constructor and allows you to perform setup operations when an instance of a class is created.
- You can have multiple init blocks in a class, and they will be executed in the order they appear in the class body.
- `init` block run after primary constructor and before secondary constructor. 

``` kotlin
  class Person(val name: String, val age: Int) {
    init {
        println("Person's name is $name and age is $age")
    }
  }
```

