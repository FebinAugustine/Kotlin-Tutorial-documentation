# Data Types in Kotlin

Kotlin's data types are largely similar to those found in Java, but with some key differences in how they are handled (e.g., no primitive types in the typical Java sense; everything is an object). However, for performance optimization, Kotlin's compiler often compiles these types down to Java's primitive types when possible.

## A. Numeric Types

Kotlin provides various numeric types to represent different kinds of numbers.

#### Type Bit Width Range Example

- Byte 8 -128 to 127 val b: Byte = 10
- Short 16 -32768 to 32767 val s: Short = 1000
- Int 32 -2,147,483,648 to 2,147,483,647 val i: Int = 100000
- Long 64 -9,223,372,036,854,775,808 to 9,223,372,036,854,775,807 val l: Long = 1234567890123L (note L suffix)
- Float
  32 Approx. pm3.4 times10raiseto38 (7 decimal digits precision)
  val f: Float = 3.14f (note f or F suffix)
  - Double 64
    Approx. pm1.8 times10raiseto308 (15-16 decimal digits precision)
    val d: Double = 3.14159

### Integer Literals:

- Decimal: 123
- Long: 123L
- Hexadecimal: 0x0F
- Binary: 0b00001011

### loating-point Literals:

- By default, floating-point literals are Double.
- To specify a Float, append f or F: 3.14f.

### Underscores in Numeric Literals:

You can use underscores to make large numbers more readable.

```Kotlin

val oneMillion = 1_000_000
val creditCardNumber = 1234_5678_9012_3456L
val hexBytes = 0xFF_EC_DE_5E
```

## B. Boolean Type

- Definition: Represents logical values.
- Values: true or false.
- Use Cases: Conditional statements (if, when), loops (while, for), logical operations.

#### Example:

```Kotlin

val isRaining: Boolean = true
val isLoggedIn = false // Type inferred
```

## C. Character Type

- Definition: Represents a single character.
- Syntax: Enclosed in single quotes.

#### Example:

```Kotlin

val grade: Char = 'A'
val newLine = '\n' // Special character (newline)
```

## D. String Type

- Definition: Represents a sequence of characters. String is an immutable class in Kotlin (like in Java).
- Syntax: Enclosed in double quotes.

- String Literals:

  - Escaped Strings:
    Standard strings that can have escape sequences (e.g., \n for newline, \t for tab, \\ for backslash, \" for double quote).

```Kotlin
val escapedString = "Hello, world!\nHow are you?"
println(escapedString)
```

- Raw Strings (Triple-quoted Strings):
  Enclosed in triple quotes ("""..."""). They can contain newlines and arbitrary text without escaping characters. Useful for multi-line text, regex patterns, or paths.

```Kotlin
val rawString = """
This is a multi-line string.
It preserves
all whitespace and
special characters like \t and "quotes".
No need for escaping.
""".trimIndent() // trimIndent() removes leading whitespace from all lines
println(rawString)
```

- String Templates:
  A powerful feature that allows you to embed expressions inside string literals.

- Using $variableName:

```Kotlin
val name = "Alice"
val age = 30
println("My name is $name and I am $age years old.")
// Output: My name is Alice and I am 30 years old.
```

- Using ${expression} for more complex expressions:

```Kotlin
val num1 = 10
val num2 = 5
println("The sum of $num1 and $num2 is ${num1 + num2}.")
// Output: The sum of 10 and 5 is 15.

val greeting = "Hello"
println("The length of the greeting is ${greeting.length}.")
// Output: The length of the greeting is 5.
```

## E. Array Type

Definition: Represents an ordered collection of elements of the same type. Arrays are mutable in Kotlin.

### Creation:

Using library functions like arrayOf(), intArrayOf(), doubleArrayOf(), etc.

Using the Array constructor with a size and a lambda function to initialize elements.

Accessing Elements: Using the index operator ([]).

#### Example:

```Kotlin
val numbers = arrayOf(1, 2, 3, 4, 5) // Inferred type Array<Int>
println(numbers[0]) // Output: 1

numbers[0] = 10 // Arrays are mutable
println(numbers[0]) // Output: 10

val names = arrayOf("Alice", "Bob", "Charlie")
println(names[1]) // Output: Bob

val squares = Array(5) { i -> i \* i } // Creates an array [0, 1, 4, 9, 16]
println(squares.contentToString()) // Output: [0, 1, 4, 9, 16]

// Primitive type arrays for performance (e.g., IntArray, BooleanArray)
val intArray = intArrayOf(1, 2, 3)
val booleanArray = booleanArrayOf(true, false, true)
```

## F. Collection Types (Brief Introduction)

While not "primitive" data types, collections are fundamental for storing and manipulating groups of data. Kotlin provides a rich set of collection types, distinguishing between immutable and mutable versions.

### Lists:

Ordered collections that can contain duplicate elements.

- Immutable List:
  listOf()

```Kotlin
val immutableList = listOf("Apple", "Banana", "Cherry")
// immutableList.add("Date") // Compilation error
```

- Mutable List: mutableListOf()

```Kotlin
val mutableList = mutableListOf("Red", "Green", "Blue")
mutableList.add("Yellow")
println(mutableList) // Output: [Red, Green, Blue, Yellow]
```

### Sets:

Unordered collections that contain unique elements.

- Immutable Set: setOf()

- Mutable Set: mutableSetOf()

### Maps (Dictionaries): Collections of key-value pairs. Keys are unique.

- Immutable Map: mapOf()

- Mutable Map: mutableMapOf()

# III. Type Conversions

Kotlin generally does not perform implicit type conversions for numeric types to prevent unexpected data loss. You must explicitly convert types using helper functions.

#### To convert to a wider type (safe):

```Kotlin
val i: Int = 10
val l: Long = i.toLong() // Converts Int to Long
val d: Double = l.toDouble() // Converts Long to Double
```

### To convert to a narrower type (potential data loss):

```Kotlin
val largeLong: Long = 10000000000L
val smallInt: Int = largeLong.toInt() // Potential data loss if largeLong exceeds Int.MAX_VALUE
println(smallInt) // Output: 1410065408 (due to overflow)

val piFloat: Float = 3.14159f
val piInt: Int = piFloat.toInt() // Truncates decimal part
println(piInt) // Output: 3
```

## IV. Conclusion

Understanding variables and data types in Kotlin is the bedrock of writing effective and safe code. By leveraging val for immutability, var for mutability, taking advantage of type inference, and embracing Kotlin's robust null safety features, you can write expressive, concise, and bug-resistant applications. Furthermore, a solid grasp of the available numeric, character, string, and collection types empowers you to model your data accurately and efficiently. Remember to prioritize val and consider null safety in all your variable declarations.
