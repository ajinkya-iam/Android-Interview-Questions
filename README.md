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
