# Control Flow in Kotlin: A Detailed Study

Control flow statements determine the order in which instructions are executed in a program. Kotlin provides powerful and expressive constructs for decision-making, looping, and branching, often with enhancements over traditional languages.

## I. Conditional Expressions (if and when)

Kotlin treats if and when not just as statements but also as expressions. This means they can return a value, making your code more concise and functional.

### A. if Expression

The if expression evaluates a condition and executes a block of code accordingly.

- Basic if:

```Kotlin
val temperature = 25

if (temperature > 30) {
    println("It's hot outside!")
}
```

- if-else:

```Kotlin
val isRaining = true

if (isRaining) {
    println("Bring an umbrella.")
} else {
    println("Enjoy the sunshine!")
}
```

- if-else if-else Chain:

```Kotlin
val score = 85

if (score >= 90) {
    println("Grade: A")
} else if (score >= 80) {
    println("Grade: B")
} else if (score >= 70) {
    println("Grade: C")
} else {
    println("Grade: F")
}

```

- if as an Expression (Returning a Value):
  The last expression in an if or else block is the value that the if expression returns.

```Kotlin
val num = 10
val result = if (num % 2 == 0) {
    println("Even number detected.") // This line is executed
    "Even" // This value is returned by the if expression
} else {
    println("Odd number detected.")
    "Odd"
}
println("The number is $result.") // Output: Even number detected. The number is Even.

// Shorter form for single-expression blocks:
val max = if (a > b) a else b
```

### B. when Expression (Kotlin's Enhanced switch)

The when expression is a powerful and flexible replacement for the switch statement in other languages. It can be used both as a statement and an expression.

- Basic when (as a statement):

```Kotlin
val dayOfWeek = 3

when (dayOfWeek) {
    1 -> println("Monday")
    2 -> println("Tuesday")
    3 -> println("Wednesday")
    4 -> println("Thursday")
    5 -> println("Friday")
    6, 7 -> println("Weekend") // Multiple branches for the same action
    else -> println("Invalid day") // Mandatory if used as an expression, optional otherwise
}
```

- when as an Expression (Returning a Value):

When used as an expression, when must be exhaustive (cover all possible cases) or include an else branch.

```Kotlin
val statusCode = 200

val message = when (statusCode) {
    200 -> "OK"
    400 -> "Bad Request"
    401 -> "Unauthorized"
    404 -> "Not Found"
    500, 502, 503 -> "Server Error" // Multiple values in a single branch
    else -> "Unknown Status" // Required for exhaustiveness when used as an expression
}
println("Status message: $message") // Output: Status message: OK
```

- when with Arbitrary Expressions (instead of constant values):

```Kotlin
val x = 10
when (x) {
    in 1..10 -> println("x is in the range 1 to 10")
    is Int -> println("x is an integer") // Type check (smart cast happens here)
    else -> println("None of the above")
}
```

- when without an Argument:

This allows when to act like a more flexible if-else if chain, evaluating boolean conditions. The first branch whose condition is true is executed.

```Kotlin
val age = 25

val category = when {
    age < 13 -> "Child"
    age in 13..19 -> "Teenager"
    age in 20..64 -> "Adult"
    else -> "Senior"
}
println("Age category: $category") // Output: Age category: Adult
```

## II. Loop Constructs

The for loop iterates over anything that provides an iterator. This is commonly used for collections, ranges, and arrays.

- Iterating over a range:

```Kotlin
for (i in 1..5) { // 1, 2, 3, 4, 5 (inclusive)
    print("$i ")
}
println() // Output: 1 2 3 4 5

for (i in 1 until 5) { // 1, 2, 3, 4 (exclusive of 5)
    print("$i ")
}
println() // Output: 1 2 3 4

for (i in 5 downTo 1) { // 5, 4, 3, 2, 1
    print("$i ")
}
println() // Output: 5 4 3 2 1

for (i in 1..10 step 2) { // 1, 3, 5, 7, 9
    print("$i ")
}
println() // Output: 1 3 5 7 9
```

- Iterating over collections (Lists, Sets, etc.):

```Kotlin
val fruits = listOf("Apple", "Banana", "Cherry")
for (fruit in fruits) {
    println(fruit)
}
// Output:
// Apple
// Banana
// Cherry
```

- Iterating with index:

```Kotlin
for (index in fruits.indices) { // Loop over indices (0, 1, 2)
    println("Fruit at $index is ${fruits[index]}")
}
// Output:
// Fruit at 0 is Apple
// Fruit at 1 is Banana
// Fruit at 2 is Cherry

// Preferred way for both element and index:
for ((index, fruit) in fruits.withIndex()) {
    println("Fruit at $index is $fruit")
}
```

- Iterating over Maps:

```Kotlin
val ages = mapOf("Alice" to 30, "Bob" to 24, "Charlie" to 35)
for ((name, age) in ages) { // Destructuring declaration
    println("$name is $age years old.")
}
// Output:
// Alice is 30 years old.
// Bob is 24 years old.
// Charlie is 35 years old.
```

### B. while Loop

The while loop repeatedly executes a block of code as long as its condition is true.

```Kotlin
var i = 0
while (i < 5) {
    println("While loop: $i")
    i++
}
// Output:
// While loop: 0
// While loop: 1
// While loop: 2
// While loop: 3
// While loop: 4
```

### C. do-while Loop

The do-while loop executes its block of code at least once, and then repeatedly as long as its condition is true.

```Kotlin
var j = 0
do {
    println("Do-while loop: $j")
    j++
} while (j < 5)
// Output:
// Do-while loop: 0
// Do-while loop: 1
// Do-while loop: 2
// Do-while loop: 3
// Do-while loop: 4

var k = 10
do {
    println("This will print at least once: $k")
    k++
} while (k < 5) // Condition is false from the start, but runs once
// Output:
// This will print at least once: 10
```

## III. Jump Expressions

ump expressions alter the normal sequential flow of execution within loops or functions.

### A. break

The break expression terminates the innermost loop immediately. Execution continues from the statement immediately following the loop.

```Kotlin
for (i in 1..10) {
    if (i == 5) {
        break // Exits the loop when i is 5
    }
    print("$i ")
}
println() // Output: 1 2 3 4
```

### B. continue

The continue expression skips the rest of the current iteration of the innermost loop and proceeds to the next iteration (if any).

```Kotlin
for (i in 1..5) {
    if (i == 3) {
        continue // Skips printing 3
    }
    print("$i ")
}
println() // Output: 1 2 4 5
```

### C. Labels for break and continue

Kotlin allows you to label expressions (including loops) to control the flow when dealing with nested loops. A label is an identifier followed by @.

```Kotlin
loop@ for (i in 1..3) {
    for (j in 1..3) {
        if (i == 2 && j == 2) {
            break@loop // Exits the outer loop (labeled 'loop')
        }
        println("i = $i, j = $j")
    }
}
// Output:
// i = 1, j = 1
// i = 1, j = 2
// i = 1, j = 3
// i = 2, j = 1

println("--- Using continue with label ---")

outerLoop@ for (i in 1..3) {
    for (j in 1..3) {
        if (i == 2 && j == 1) {
            continue@outerLoop // Skips to the next iteration of 'outerLoop'
        }
        println("i = $i, j = $j")
    }
}
// Output:
// i = 1, j = 1
// i = 1, j = 2
// i = 1, j = 3
// i = 3, j = 1
// i = 3, j = 2
// i = 3, j = 3
```

### D. return

The return expression terminates the execution of the function (or lambda/anonymous function) it is called within and returns a value to the caller.

- Basic return from a function:

```Kotlin
fun greet(name: String) {
    if (name.isBlank()) {
        println("Name cannot be empty.")
        return // Exits the function early
    }
    println("Hello, $name!")
}

fun add(a: Int, b: Int): Int {
    return a + b // Returns the sum
}

fun main() {
    greet("Alice")    // Output: Hello, Alice!
    greet("")         // Output: Name cannot be empty.
    val sum = add(5, 3)
    println("Sum: $sum") // Output: Sum: 8
}
```

- Labeled Returns for Lambdas:
  When returning from a lambda expression, return by default returns from the enclosing function. To return from the lambda itself, you use a label.

```Kotlin
fun performAction(numbers: List<Int>) {
    numbers.forEach { // forEach is an inline function that takes a lambda
        if (it == 3) {
            // return // This would return from performAction()
            return@forEach // This returns from the forEach lambda only
        }
        print("$it ")
    }
    println("\nFinished iterating.")
}

fun findFirstEven(numbers: List<Int>): Int? {
    numbers.forEach returnBlock@ {
        if (it % 2 == 0) {
            return@returnBlock it // Returns from the findFirstEven function
        }
    }
    return null // If no even number found
}

fun main() {
    performAction(listOf(1, 2, 3, 4, 5))
    // Output: 1 2
    // Finished iterating. (This line is printed because return@forEach only exited the lambda, not the function)

    val evenNumber = findFirstEven(listOf(1, 3, 5, 7, 2, 9))
    println("First even: $evenNumber") // Output: First even: 2

    val noEvenNumber = findFirstEven(listOf(1, 3, 5, 7, 9))
    println("First even: $noEvenNumber") // Output: First even: null
}
```

### IV. When to Choose Which Control Flow

- if: Best for simple true/false conditions or a short chain of else if for distinct conditions. Use it as an expression for assigning values based on conditions.

- when: Ideal for multiple distinct conditions, pattern matching (types, ranges), and situations where if-else if becomes unwieldy. It's often more readable and concise. Always prefer when over chained if-else if for more than a couple of branches.

- for: Use when you need to iterate over a collection, array, or a sequence of numbers (ranges).

- while/do-while: Use when the number of iterations is unknown, and you need to repeat a block of code based purely on a condition. do-while is for cases where the block must execute at least once.

- break/continue: Use sparingly within loops to handle specific edge cases or optimize performance. Overuse can make code harder to read and debug. Labels are for precise control in nested loops.

- return: Essential for exiting functions and lambdas, returning results, and handling early exit conditions. Labeled returns are key for precise control within lambdas and anonymous functions.

Mastering these control flow mechanisms is fundamental to writing effective and efficient Kotlin programs. They allow you to dictate the logic and behavior of your applications with clarity and precision.
