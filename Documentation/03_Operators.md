# Operators in Kotlin: A Detailed Study

Operators are special symbols or keywords that perform operations on one or more operands (values or variables). Kotlin, like most programming languages, provides a rich set of operators to manipulate data, perform calculations, make comparisons, and control program flow.

One of Kotlin's strengths is its flexibility with operators: many operators are actually member functions or extension functions with special syntax, allowing for operator overloading and custom behavior for user-defined types.

## I.Assignment Operators

### Assignment operators are used to assign a value to a variable.

- = (Simple Assignment)
  - Assigns the value on the right to the variable on the left.

#### Example:

```Kotlin
var x = 10
val name = "Alice"
```

- Compound Assignment Operators (Shorthand)
  - Combine an arithmetic or bitwise operation with an assignment.
  - Syntax: variable op= value is equivalent to variable = variable op value

Operator Equivalent To Example Result

- +=
  - a = a + b var a = 5; a += 3 a is 8
- -=
  - a = a - b var a = 5; a -= 3 a is 2
- \_=
  - a = a \_ b var a = 5; a \*= 3 a is 15
- /=
  - a = a / b var a = 5; a /= 2 a is 2 (integer division)
- %=

  - a = a % b var a = 5; a %= 3 a is 2

- Bitwise Compound Assignments (for Int, Long, Short, Byte):

  - andAssign(other: T) -> &=

  - orAssign(other: T) -> |=

  - xorAssign(other: T) -> ^=

  - shlAssign(other: Int) -> <<=

  - shrAssign(other: Int) -> >>=

  - ushrAssign(other: Int) -> >>>= (unsigned right shift)

#### Example:

```Kotlin
var flags = 0b1010
flags = 0b1010 // 10
flags = 0b0011 // 3
flags andAssign 0b0101 // Equivalent to flags = flags.and(0b0101) -> flags is 0b0000 (0)
println(flags) // Output: 0

var num = 10 // 00001010
num shlAssign 1 // num becomes 20 (00010100)
println(num) // Output: 20
```

## II. Arithmetic Operators

Arithmetic operators perform mathematical calculations.

- - (Addition)
- - (Subtraction)
- - (Multiplication)
- / (Division)
  - For integers, / performs integer division (truncates the decimal part).
    - For floating-point numbers, it performs floating-point division.
- % (Modulo/Remainder)
  - Returns the remainder of a division.

#### Example:

```Kotlin
val a = 10
val b = 3

println("a + b = ${a + b}") // 13
println("a - b = ${a - b}") // 7
println("a * b = ${a * b}") // 30
println("a / b = ${a / b}") // 3 (integer division)
println("a % b = ${a % b}") // 1

val c = 10.0
val d = 3.0
println("c / d = ${c / d}") // 3.3333333333333335 (floating-point division)
```

- Unary Operators:
  - - (Unary Plus): No effect on the value.
  - - (Unary Minus): Negates the value.

#### Example:

```Kotlin
val positive = 5
val negative = -positive // -5
val anotherPositive = +negative // -5 (no change)
```

## III. Increment and Decrement Operators

These operators increase or decrease the value of a variable by 1.

- ++ (Increment)
- -- (Decrement)
- Prefix vs. Postfix:
  - Prefix (++variable, --variable): The operation is performed before the value is used in the expression.
  - Postfix (variable++, variable--): The operation is performed after the value is used in the expression.

#### Example:

```Kotlin
var counter = 0
println("Initial counter: $counter") // 0

val a = ++counter // counter becomes 1, then a gets 1
println("a: $a, counter: $counter") // a: 1, counter: 1

val b = counter++ // b gets 1, then counter becomes 2
println("b: $b, counter: $counter") // b: 1, counter: 2

var value = 10
val c = --value // value becomes 9, then c gets 9
println("c: $c, value: $value") // c: 9, value: 9

val d = value-- // d gets 9, then value becomes 8
println("d: $d, value: $d") // d: 9, value: 8
```

## IV. Comparison (Relational) Operators

Comparison operators compare two operands and return a Boolean result (true or false).

- == (Equality): Checks if two operands are equal in value.
- != (Inequality): Checks if two operands are not equal in value.
- > (Greater Than)
- < (Less Than)
- > = (Greater Than or Equal To)
- <= (Less Than or Equal To)
- Structural Equality (==):
  In Kotlin, == for objects (non-primitive types) translates to a call to the equals() method. This means it checks for structural equality (do they have the same content?), not referential equality (are they the same object in memory?).
- Referential Equality (===):
  To check if two references point to the exact same object in memory, use ===.

#### Example:

```Kotlin
val num1 = 10
val num2 = 20
val num3 = 10

println("num1 == num2: ${num1 == num2}")   // false
println("num1 == num3: ${num1 == num3}")   // true
println("num1 != num2: ${num1 != num2}")   // true
println("num1 > num2: ${num1 > num2}")     // false
println("num1 <= num3: ${num1 <= num3}")   // true

val str1 = "Hello"
val str2 = "Hello"
val str3 = String("Hello".toCharArray()) // Creates a new String object

println("str1 == str2: ${str1 == str2}")   // true (structural equality)
println("str1 === str2: ${str1 === str2}") // true (often true due to String interning)
println("str1 == str3: ${str1 == str3}")   // true (structural equality)
println("str1 === str3: ${str1 === str3}") // false (different objects in memory)
```

## V. Logical Operators

Logical operators combine boolean expressions and return a Boolean result.

- && (Logical AND):
  Returns true if both operands are true. Short-circuits (if the first operand is false, the second is not evaluated).

- || (Logical OR):
  Returns true if at least one operand is true. Short-circuits (if the first operand is true, the second is not evaluated).

- ! (Logical NOT):
  Inverts the boolean value of its operand.

#### Example:

```Kotlin
val isRaining = true
val hasUmbrella = false
val isSunny = false

println("Can go out (AND): ${isRaining && hasUmbrella}") // false (isRaining is true, but hasUmbrella is false)
println("Can stay dry (OR): ${isRaining || hasUmbrella}") // true (isRaining is true)
println("Is not raining: ${!isRaining}") // false
println("Is sunny AND not raining: ${isSunny && !isRaining}") // false (isSunny is false)
```

## VI. Bitwise Operators (Member Functions)

Kotlin does not have special bitwise operators like &, |, ^, <<, >>, >>>. Instead, bitwise operations are performed using named member functions of integer types (Int, Long, Short, Byte).

- and(other: T): Bitwise AND
- or(other: T): Bitwise OR
- xor(other: T): Bitwise XOR (exclusive OR)
- inv(): Bitwise Invert (unary operator)
- shl(bitCount: Int): Signed Shift Left
- shr(bitCount: Int): Signed Shift Right
- ushr(bitCount: Int): Unsigned Shift Right (fills with zeros)

#### Example:

```Kotlin
val a = 0b1100 // 12
val b = 0b0110 // 6

println("a.and(b) = ${a.and(b)}")   // 0b0100 (4)
println("a.or(b) = ${a.or(b)}")     // 0b1110 (14)
println("a.xor(b) = ${a.xor(b)}")   // 0b1010 (10)
println("a.inv() = ${a.inv()}")     // -13 (inverts all bits, including sign bit)

val num = 8 // 00001000
println("num.shl(2) = ${num.shl(2)}") // 32 (00100000)
println("num.shr(2) = ${num.shr(2)}") // 2 (00000010)

val signedNum = -16 // 11110000 (assuming 8-bit for simplicity)
println("signedNum.shr(2) = ${signedNum.shr(2)}")   // -4 (11111100) - preserves sign
println("signedNum.ushr(2) = ${signedNum.ushr(2)}") // 1073741820 (00111100...) - fills with zeros
```

## VII. Range Operators

Kotlin provides concise operators for creating ranges, primarily used with for loops and in checks.

- .. (Range To): Creates a closed range (inclusive of both start and end).
- until (Range Until): Creates a half-open range (inclusive of start, exclusive of end).
- downTo (Down To): Creates a range that counts downwards.
- step (Step): Used with ranges to define an increment/decrement step.

#### Example:

```Kotlin
for (i in 1..5) { // 1, 2, 3, 4, 5
    print("$i ")
}
println()

for (i in 1 until 5) { // 1, 2, 3, 4
    print("$i ")
}
println()

for (i in 5 downTo 1) { // 5, 4, 3, 2, 1
    print("$i ")
}
println()

for (i in 1..10 step 2) { // 1, 3, 5, 7, 9
    print("$i ")
}
println()

for (i in 10 downTo 1 step 3) { // 10, 7, 4, 1
    print("$i ")
}
println()
```

## VIII. Membership Operators

Used to check if an element is present within a range or collection.

- in (In): Checks if an element is present in a range, collection, or string.
- !in (Not In): Checks if an element is not present.

#### Example:

```Kotlin
val numbers = listOf(1, 2, 3, 4, 5)
val number = 3
val anotherNumber = 6

println("$number in numbers: ${number in numbers}")      // true
println("$anotherNumber in numbers: ${anotherNumber in numbers}") // false
println("$anotherNumber !in numbers: ${anotherNumber !in numbers}") // true

val range = 1..10
println("5 in range: ${5 in range}") // true
println("15 in range: ${15 in range}") // false

val text = "Hello Kotlin"
println("'K' in text: ${'K' in text}") // true
println("\"Kotlin\" in text: ${"Kotlin" in text}") // true
```

## IX. Elvis Operator (?:)

Definition: Provides a default value when a nullable expression is null.

- Syntax:
  - nullableExpression ?: defaultValue
- Behavior:
  - If nullableExpression is not null, its value is returned. Otherwise, defaultValue is returned.

#### Example:

```Kotlin
val name: String? = null
val displayName = name ?: "Guest"
println("Display name: $displayName") // Output: Guest

val actualName: String? = "John Doe"
val anotherDisplayName = actualName ?: "Unknown"
println("Another display name: $anotherDisplayName") // Output: John Doe
```

## X. Safe Call Operator (?.) and Non-null Asserted Call (!!)

These are crucial for Kotlin's null safety.

### ?. (Safe Call):

- Allows you to safely call a method or access a property on a nullable object.
- If the object is null, the entire expression evaluates to null without throwing a NullPointerException.

#### Example:

```Kotlin
val str: String? = null
val length = str?.length // length will be null
println("Length (safe call): $length") // Output: null

val strNonNull: String? = "Kotlin"
val lengthNonNull = strNonNull?.length // lengthNonNull will be 6
println("Length (non-null safe call): $lengthNonNull") // Output: 6
```

### !! (Non-null Asserted Call):

- Converts any nullable type to its non-nullable counterpart.
- Caution: If the value is null at runtime, it will throw a NullPointerException. Use only when you are absolutely certain the value will not be null.

#### Example:

```Kotlin
val nonNullableStr: String? = "I'm here!"
val len = nonNullableStr!!.length // This is safe, nonNullableStr is not null
println("Length (non-null asserted): $len") // Output: 9

val potentiallyNull: String? = null
// val riskyLen = potentiallyNull!!.length // This line would throw a NullPointerException at runtime!
```

## XI. Type Check and Cast Operators

Used for checking and converting types.

- is (Is): Checks if an object is an instance of a particular type. Returns Boolean.
- !is (Not Is): Checks if an object is not an instance of a particular type. Returns Boolean.
- as (Unsafe Cast): Performs an unsafe cast. If the cast is not possible, it throws a ClassCastException.
- as? (Safe Cast): Performs a safe cast. If the cast is not possible, it returns null instead of throwing an exception.

#### Example:

```Kotlin
val obj: Any = "Hello"

if (obj is String) {
    println("obj is a String. Length: ${obj.length}") // Smart-casted to String inside the block
} else {
    println("obj is not a String.")
}

if (obj !is Int) {
    println("obj is not an Int.")
}

val numObj: Any = 123
val stringValue: String = numObj as String // Throws ClassCastException at runtime
// val stringValue: String? = numObj as? String // Returns null safely
// println(stringValue)
```

## XII. Operator Overloading

Okay, let's dive into a detailed study of operators in Kotlin!

Operators in Kotlin: A Detailed Study
Operators are special symbols or keywords that perform operations on one or more operands (values or variables). Kotlin, like most programming languages, provides a rich set of operators to manipulate data, perform calculations, make comparisons, and control program flow.

One of Kotlin's strengths is its flexibility with operators: many operators are actually member functions or extension functions with special syntax, allowing for operator overloading and custom behavior for user-defined types.

I. Assignment Operators
Assignment operators are used to assign a value to a variable.

= (Simple Assignment)

Assigns the value on the right to the variable on the left.

Example:

Kotlin

var x = 10
val name = "Alice"
Compound Assignment Operators (Shorthand)

Combine an arithmetic or bitwise operation with an assignment.

Syntax: variable op= value is equivalent to variable = variable op value

Operator Equivalent To Example Result
+= a = a + b var a = 5; a += 3 a is 8
-= a = a - b var a = 5; a -= 3 a is 2
_= a = a _ b var a = 5; a \*= 3 a is 15
/= a = a / b var a = 5; a /= 2 a is 2 (integer division)
%= a = a % b var a = 5; a %= 3 a is 2

Export to Sheets
Bitwise Compound Assignments (for Int, Long, Short, Byte):

andAssign(other: T) -> &=

orAssign(other: T) -> |=

xorAssign(other: T) -> ^=

shlAssign(other: Int) -> <<=

shrAssign(other: Int) -> >>=

ushrAssign(other: Int) -> >>>= (unsigned right shift)

Example:

Kotlin

var flags = 0b1010
flags = 0b1010 // 10
flags = 0b0011 // 3
flags andAssign 0b0101 // Equivalent to flags = flags.and(0b0101) -> flags is 0b0000 (0)
println(flags) // Output: 0

var num = 10 // 00001010
num shlAssign 1 // num becomes 20 (00010100)
println(num) // Output: 20
II. Arithmetic Operators
Arithmetic operators perform mathematical calculations.

- (Addition)

* (Subtraction)

- (Multiplication)

/ (Division)

For integers, / performs integer division (truncates the decimal part).

For floating-point numbers, it performs floating-point division.

% (Modulo/Remainder)

Returns the remainder of a division.

Example:

Kotlin

val a = 10
val b = 3

println("a + b = ${a + b}") // 13
println("a - b = ${a - b}") // 7
println("a _ b = ${a _ b}") // 30
println("a / b = ${a / b}") // 3 (integer division)
println("a % b = ${a % b}") // 1

val c = 10.0
val d = 3.0
println("c / d = ${c / d}") // 3.3333333333333335 (floating-point division)
Unary Operators:

- (Unary Plus): No effect on the value.

* (Unary Minus): Negates the value.

Example:

Kotlin

val positive = 5
val negative = -positive // -5
val anotherPositive = +negative // -5 (no change)
III. Increment and Decrement Operators
These operators increase or decrease the value of a variable by 1.

++ (Increment)

-- (Decrement)

Prefix vs. Postfix:

Prefix (++variable, --variable): The operation is performed before the value is used in the expression.

Postfix (variable++, variable--): The operation is performed after the value is used in the expression.

Example:

Kotlin

var counter = 0
println("Initial counter: $counter") // 0

val a = ++counter // counter becomes 1, then a gets 1
println("a: $a, counter: $counter") // a: 1, counter: 1

val b = counter++ // b gets 1, then counter becomes 2
println("b: $b, counter: $counter") // b: 1, counter: 2

var value = 10
val c = --value // value becomes 9, then c gets 9
println("c: $c, value: $value") // c: 9, value: 9

val d = value-- // d gets 9, then value becomes 8
println("d: $d, value: $d") // d: 9, value: 8
IV. Comparison (Relational) Operators
Comparison operators compare two operands and return a Boolean result (true or false).

== (Equality): Checks if two operands are equal in value.

!= (Inequality): Checks if two operands are not equal in value.

> (Greater Than)

< (Less Than)

> = (Greater Than or Equal To)

<= (Less Than or Equal To)

Structural Equality (==): In Kotlin, == for objects (non-primitive types) translates to a call to the equals() method. This means it checks for structural equality (do they have the same content?), not referential equality (are they the same object in memory?).

Referential Equality (===): To check if two references point to the exact same object in memory, use ===.

Example:

Kotlin

val num1 = 10
val num2 = 20
val num3 = 10

println("num1 == num2: ${num1 == num2}") // false
println("num1 == num3: ${num1 == num3}") // true
println("num1 != num2: ${num1 != num2}") // true
println("num1 > num2: ${num1 > num2}") // false
println("num1 <= num3: ${num1 <= num3}") // true

val str1 = "Hello"
val str2 = "Hello"
val str3 = String("Hello".toCharArray()) // Creates a new String object

println("str1 == str2: ${str1 == str2}") // true (structural equality)
println("str1 === str2: ${str1 === str2}") // true (often true due to String interning)
println("str1 == str3: ${str1 == str3}") // true (structural equality)
println("str1 === str3: ${str1 === str3}") // false (different objects in memory)
V. Logical Operators
Logical operators combine boolean expressions and return a Boolean result.

&& (Logical AND): Returns true if both operands are true. Short-circuits (if the first operand is false, the second is not evaluated).

|| (Logical OR): Returns true if at least one operand is true. Short-circuits (if the first operand is true, the second is not evaluated).

! (Logical NOT): Inverts the boolean value of its operand.

Example:

Kotlin

val isRaining = true
val hasUmbrella = false
val isSunny = false

println("Can go out (AND): ${isRaining && hasUmbrella}") // false (isRaining is true, but hasUmbrella is false)
println("Can stay dry (OR): ${isRaining || hasUmbrella}") // true (isRaining is true)
println("Is not raining: ${!isRaining}") // false
println("Is sunny AND not raining: ${isSunny && !isRaining}") // false (isSunny is false)
VI. Bitwise Operators (Member Functions)
Kotlin does not have special bitwise operators like &, |, ^, <<, >>, >>>. Instead, bitwise operations are performed using named member functions of integer types (Int, Long, Short, Byte).

and(other: T): Bitwise AND

or(other: T): Bitwise OR

xor(other: T): Bitwise XOR (exclusive OR)

inv(): Bitwise Invert (unary operator)

shl(bitCount: Int): Signed Shift Left

shr(bitCount: Int): Signed Shift Right

ushr(bitCount: Int): Unsigned Shift Right (fills with zeros)

Example:

Kotlin

val a = 0b1100 // 12
val b = 0b0110 // 6

println("a.and(b) = ${a.and(b)}") // 0b0100 (4)
println("a.or(b) = ${a.or(b)}") // 0b1110 (14)
println("a.xor(b) = ${a.xor(b)}") // 0b1010 (10)
println("a.inv() = ${a.inv()}") // -13 (inverts all bits, including sign bit)

val num = 8 // 00001000
println("num.shl(2) = ${num.shl(2)}") // 32 (00100000)
println("num.shr(2) = ${num.shr(2)}") // 2 (00000010)

val signedNum = -16 // 11110000 (assuming 8-bit for simplicity)
println("signedNum.shr(2) = ${signedNum.shr(2)}") // -4 (11111100) - preserves sign
println("signedNum.ushr(2) = ${signedNum.ushr(2)}") // 1073741820 (00111100...) - fills with zeros
VII. Range Operators
Kotlin provides concise operators for creating ranges, primarily used with for loops and in checks.

.. (Range To): Creates a closed range (inclusive of both start and end).

until (Range Until): Creates a half-open range (inclusive of start, exclusive of end).

downTo (Down To): Creates a range that counts downwards.

step (Step): Used with ranges to define an increment/decrement step.

Example:

Kotlin

for (i in 1..5) { // 1, 2, 3, 4, 5
print("$i ")
}
println()

for (i in 1 until 5) { // 1, 2, 3, 4
print("$i ")
}
println()

for (i in 5 downTo 1) { // 5, 4, 3, 2, 1
print("$i ")
}
println()

for (i in 1..10 step 2) { // 1, 3, 5, 7, 9
print("$i ")
}
println()

for (i in 10 downTo 1 step 3) { // 10, 7, 4, 1
print("$i ")
}
println()
VIII. Membership Operators
Used to check if an element is present within a range or collection.

in (In): Checks if an element is present in a range, collection, or string.

!in (Not In): Checks if an element is not present.

Example:

Kotlin

val numbers = listOf(1, 2, 3, 4, 5)
val number = 3
val anotherNumber = 6

println("$number in numbers: ${number in numbers}")      // true
println("$anotherNumber in numbers: ${anotherNumber in numbers}") // false
println("$anotherNumber !in numbers: ${anotherNumber !in numbers}") // true

val range = 1..10
println("5 in range: ${5 in range}") // true
println("15 in range: ${15 in range}") // false

val text = "Hello Kotlin"
println("'K' in text: ${'K' in text}") // true
println("\"Kotlin\" in text: ${"Kotlin" in text}") // true
IX. Elvis Operator (?:)
Definition: Provides a default value when a nullable expression is null.

Syntax: nullableExpression ?: defaultValue

Behavior: If nullableExpression is not null, its value is returned. Otherwise, defaultValue is returned.

Example:

Kotlin

val name: String? = null
val displayName = name ?: "Guest"
println("Display name: $displayName") // Output: Guest

val actualName: String? = "John Doe"
val anotherDisplayName = actualName ?: "Unknown"
println("Another display name: $anotherDisplayName") // Output: John Doe
X. Safe Call Operator (?.) and Non-null Asserted Call (!!)
These are crucial for Kotlin's null safety.

?. (Safe Call):

Allows you to safely call a method or access a property on a nullable object.

If the object is null, the entire expression evaluates to null without throwing a NullPointerException.

Example:

Kotlin

val str: String? = null
val length = str?.length // length will be null
println("Length (safe call): $length") // Output: null

val strNonNull: String? = "Kotlin"
val lengthNonNull = strNonNull?.length // lengthNonNull will be 6
println("Length (non-null safe call): $lengthNonNull") // Output: 6
!! (Non-null Asserted Call):

Converts any nullable type to its non-nullable counterpart.

Caution: If the value is null at runtime, it will throw a NullPointerException. Use only when you are absolutely certain the value will not be null.

Example:

Kotlin

val nonNullableStr: String? = "I'm here!"
val len = nonNullableStr!!.length // This is safe, nonNullableStr is not null
println("Length (non-null asserted): $len") // Output: 9

val potentiallyNull: String? = null
// val riskyLen = potentiallyNull!!.length // This line would throw a NullPointerException at runtime!
XI. Type Check and Cast Operators
Used for checking and converting types.

is (Is): Checks if an object is an instance of a particular type. Returns Boolean.

!is (Not Is): Checks if an object is not an instance of a particular type. Returns Boolean.

as (Unsafe Cast): Performs an unsafe cast. If the cast is not possible, it throws a ClassCastException.

as? (Safe Cast): Performs a safe cast. If the cast is not possible, it returns null instead of throwing an exception.

Example:

Kotlin

val obj: Any = "Hello"

if (obj is String) {
println("obj is a String. Length: ${obj.length}") // Smart-casted to String inside the block
} else {
println("obj is not a String.")
}

if (obj !is Int) {
println("obj is not an Int.")
}

val numObj: Any = 123
val stringValue: String = numObj as String // Throws ClassCastException at runtime
// val stringValue: String? = numObj as? String // Returns null safely
// println(stringValue)
XII. Operator Overloading
Kotlin allows you to overload many of its operators for your custom classes. This means you can define what an operator (like +, -, \*, ==, [], etc.) does when applied to instances of your own classes. This is done by implementing specific named member functions or extension functions.

#### Example: Overloading + for a Point class

```Kotlin
data class Point(val x: Int, val y: Int) {
    // Overload the '+' operator
    operator fun plus(other: Point): Point {
        return Point(x + other.x, y + other.y)
    }

    // Overload the unary '-' operator
    operator fun unaryMinus(): Point {
        return Point(-x, -y)
    }
}

fun main() {
    val p1 = Point(1, 2)
    val p2 = Point(3, 4)

    val p3 = p1 + p2 // Calls p1.plus(p2)
    println("p1 + p2 = $p3") // Output: p1 + p2 = Point(x=4, y=6)

    val p4 = -p1 // Calls p1.unaryMinus()
    println("-p1 = $p4") // Output: -p1 = Point(x=-1, y=-2)
}
```

This extensive set of operators, combined with Kotlin's safety features and the ability to overload, makes the language powerful, expressive, and a pleasure to work with.
