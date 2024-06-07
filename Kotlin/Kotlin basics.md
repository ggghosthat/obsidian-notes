## Hello World!

Each Kotlin program like other programming languages starts with the `main()`  function.

``` Kotlin
fun main()
{
	println("Hello World")
}
```

In Kotlin:
- `fun` is used to declare a function 
- the `main()` function is place where Kotlin starts from
- the body of a function is written within curly braces `{}`
- `println()` and `print()` functions print their arguments to standard output


### Variables
As an other programing languages Kotlin need to store data, and  variable here come in handy to do just that. In we can declare:
- **read-only** variables with `val`
- **mutable** variables with `var`
To assign a value, use the assignment operator `=`.

Example:
```Kotlin
val popcorn = 5 //There are 5 boxes of popcorn
val hotdog = 7 //There are 7 hotdogs
var customers - 10 //There are 10 customers in the queue

//Some customers leave the queue
customers = 8
println(customers)
//8
```

JetBrains recommend to declare all variables as read-only `val` by default. Declare mutable variables `var` only if necessary.

### String templates
It's useful to know how to print contents of variables to standard output. You can do this with **string templates**. You can use template expression to access data stored in variables and other objects, and convert them into strings. A string value is a sequence of characters in double quotes `"`. Template expressions always start with a dollar sign `$`.

To evaluate a piece of code in a template expression, place the code within curly braces `{}` after the dollar sign `$`.

Example:
```Kotlin
val customers = 10
println("There are $customers customers")
//There are 10 customers

println("There are ${customers + 1} customers")
//There are 11 customers
```


## Basic types
Every variable and data structure in Kotlin has a data type. Data types are important because they tell the compiler what you are allowed to do with that variable or data structure. In other words, what functions and properties it has.

In previous chapter we used `customers` variable, which has type: `Int`. Kotlin's ability to **infer** the data type is called **type inference**. `customers` is assigned an integer value. From this, Kotlin infers that `customers` has numerical data type: `Int`. As a result, the compiler knows that you can perform aithmetic operations with `customers`. 

Example:
```Kotlin
var customers = 10

//some customers leave the queue
customers = 8

customers = customers + 3 //Example of addition: 11
cusotmers += 7  //Example of addition: 18
customers -= 3  //Example of subtraction 15
customers ** 2  //Example of multiplication: 30
customers /= 3  //Example of devision: 10

println(customers)
```

In total, Kotlin has the following basic types:

| Category | Basic types |
| ---- | ---- |
| Integers | `Byte`, `Short`, `Int`, `Long` |
| Unsigned integers | `UByte`, `UShort`, `UInt`, `ULong` |
| Floating-point numbers | `Float`, `Double` |
| Booleans | `Boolean` |
| Characters | `Char` |
| Strings | `String` |
Also we Kotlin allow us declare variables and initialize them later. Kotlin can manage this as long as variable are initialized before the first read.

To declare a variable without initializing it, specify its type with `:`. It look similar with Python, however there is a deference in syntax of these programming languages.

```Kotlin
val age: Int = 10
```

```Python
age: int = 10
```

Example:
```Kotlin
//Variable declared without initialization
val d: Int
//Variablr initialized
d = 3

//Variable explicitly typed and initialized
val e: String = "hello"

//Variables can be read because they have been initialized 
println(d) //3
println(e) //hello
```



## Collections
While programming, it's very useful to be able to group data into structures for later processing. Kotlin provides collections for exactly this purpose.

There are following collections in Kotlin for grouping items:

| Collection type | Description |
| ---- | ---- |
| **Lists** | Ordered collections of items |
| Sets | Unique unordered collections of items |
| Maps | Sets of key-value pairs where keys are unique and map to only one value |
Each collection type can be **mutable** or **read only**.

### Lists
Lists store items in the order that they are added, and allow for duplicate items. 
To create a read-only list (`List`) use the `listOf()` function. 
To create a mutable list (`MutableList`) use the `mutableListOf()` function.

When creating lists, Kotlin can infer the type of items stored. To declare the type explicitly, add the type within angled brackets `<>` after the list declaration:

```Kotlin
val readOnlyShapes = listOf("triangle", "square", "circle")
println(readOnlyShapes)
//["triangle", "square", "circle"]

val shapes: MutableList<String> = mutableListOf("triangle", "square", "circle")
println(shapes)
//["triangle", "square", "circle"]
```

if you want to avoid unwanted modification, you can obtain read-only views of mutable lists by assigning them to a `List`:

```Kotlin
val shapes: MutableList<String> = mutableListOf("triangle", "square", "circle")
val shapesLocked: List<String> = shapes
```

Lists are ordered so to access an item in a list, use the **indexed access operator** `[]`:

```Kotlin
val readOnlyShapes = listOf("triangle","square","circle")
println("The first item in the list is: ${readOnlyShapes[0]}")
//The first item in the list is: triangle
```

To get the **first** or **last** item in a list use `.first()` and `.last()` functions respectively:

```Kotlin
val readOnlyShapes = listOf("triangle","square","circle")
println("The first item in the list is: ${readOnlyShapes.first()}")
//The first item in the list is: triangle
```

To get the number of items in a list, use the `.count()` function:

```Kotlin
val readOnlyShapes = listOf("triangle","square","circle")
println("This list has ${readOnlyShapes.count()} items.")
//The list has 3 items.
```

To check that an item is in a list, use the `in` operator:

```Kotlin
val readOnlyShapes = listOf("triangle","square","circle")
println("circle" in readOnlyShapes)
//true
```

To **add** or **remove** items from a **mutable** list use `.add()` and `.remove()` functions respectively: 

```Kotlin
val shapes: MutableList<String> = mutableListOf("triangle", "square", "circle")
//Add "pentagon" to the list
shapes.add("pentagon")
println(shapes)
//["triangle", "square", "circle", "pentagon"]

//Remove the first "pentagon" from the list
shapes.remove("pentagon")
println(shapes)
//["triangle", "square", "circle"]
```

### Set
Whereas lists are ordered and allow duplicate items, sets are **unordered** and only store **unique** items.
To create a read-only set (`Set`), use the `setOf()` function.
To create a mutable set (`MutableSet`), use the `mutableSetOf()` function.
Like with lists case, Kotlin can infer the type of items stored in set. If you want to declare the type explicitly add the type within angled brackets `<>` after the set declaration. 

```Kotlin
//Read-only set
val readOnlyFruit = setOf("apple", "banana", "chery", "chery")
//Mutable set with explicit type declaration
val fruit: MutableSet<String>  = mutableSetOf("apple", "banana", "chery", "chery")

println(readOnlyFruit)
//[apple, banana, chery]
```

As we can see, in the above example the duplicate `cherry` item is dropped, that because sets only contains unique elements.

Also, we can prevent unwanted modifications, obtain read-only views of mutable sets by casting them to `Set`:

``` Kotlin
val fruit: MutableSet<String> = mutableSetOf("apple", "banana", "cherry", "cherry")
val fruitLocked: Set<String> = fruit
```

As in List case we can access items by index accession operator `[]`:

```Kotlin
val readOnlyFruit = setOf("apple", "banana", "cherry", "cherry")
println("This set has ${readOnlyFruit.count()} items")
// This set has 3 items
```

To check that an item in a set, use the `in` operator:

```Kotlin
val readOnlyFruit = setOf("apple", "banana", "cherry", "cherry")
println("banana" in readOnlyFruit)
// true
```

To add or remove items from a mutable set, use `.add()` and `.remove()` functions respectively:

```Kotlin
val fruit: MutableSet<String> = mutableSetOf("apple", "banana", "cherry", "cherry")
fruit.add("dragonfruit")    // Add "dragonfruit" to the set
println(fruit)              // [apple, banana, cherry, dragonfruit]

fruit.remove("dragonfruit") // Remove "dragonfruit" from the set
println(fruit)              // [apple, banana, cherry]
```


### Maps
Maps store items in key-value pairs. You access the value by referencing the key. You can imagine a map like a food menu. You can find the price (**value**), by finding the food (**key**) you want to eat. Maps are useful if you want to look up a value without using a numbered index, like in a list.

- Every key in a map must be unique so that Kotlin can understand which value you want to get.
- You can have duplicate value in a map

To create a read-only map (`Map`), use the `mapOf()` function.
To create a mutable map (`MutableMap`, use the `mutableMapOf()` function.

Kotlin infers the type of items stored in map. To declare type explicitly, add the types of key and value within angled brackets `<>` after the map declaration. (`MutableMap<String, Int>`, where keys have `String` type and values have `Int` type). The easiest way to create maps is to use `to` between each key and its related value:

```Kotlin
// Read-only map
val readOnlyJuiceMenu = mapOf("apple" to 100, "kiwi" to 190, "orange" to 100)
println(readOnlyJuiceMenu)
// {apple=100, kiwi=190, orange=100}

// Mutable map with explicit type declaration
val juiceMenu: MutableMap<String, Int> = mutableMapOf("apple" to 100, "kiwi" to 190, "orange" to 100)
println(juiceMenu)
// {apple=100, kiwi=190, orange=100}
```

To prevent unwanted modifications, obtain read-only views of mutable maps by casting them to `Map`:

```Kotlin
val juiceMenu: MutableMap<String, Int> = mutableMapOf("apple" to 100, "kiwi" to 190, "orange" to 100)
val juiceMenuLocked: Map<String, Int> = juiceMenu
```

To access a value in a map, use the indexed access operator `[]` with its key:

``` Kotlin
// Read-only map
val readOnlyJuiceMenu = mapOf("apple" to 100, "kiwi" to 190, "orange" to 100)
println("The value of apple juice is: ${readOnlyJuiceMenu["apple"]}")
// The value of apple juice is: 100
```

To get the number of items in a map, use the `.count()` function:

```Kotlin
// Read-only map
val readOnlyJuiceMenu = mapOf("apple" to 100, "kiwi" to 190, "orange" to 100)
println("This map has ${readOnlyJuiceMenu.count()} key-value pairs")
// This map has 3 key-value pairs
```

To add or remove items from a mutable map, use `.put()` and `.remove()` functions respectively:

```Kotlin
val juiceMenu: MutableMap<String, Int> = mutableMapOf("apple" to 100, "kiwi" to 190, "orange" to 100)
juiceMenu.put("coconut", 150) // Add key "coconut" with value 150 to the map
println(juiceMenu)
// {apple=100, kiwi=190, orange=100, coconut=150}

juiceMenu.remove("orange")    // Remove key "orange" from the map
println(juiceMenu)
// {apple=100, kiwi=190, coconut=150}
```

To check if a specific key is already included in a map, use the `.containsKey()` function:

```Kotlin
val readOnlyJuiceMenu = mapOf("apple" to 100, "kiwi" to 190, "orange" to 100)
println(readOnlyJuiceMenu.containsKey("kiwi"))
// true
```

To obtain a collection of the keys or values of a map, use the `keys` and `values` properties respectively:

```Kotlin
val readOnlyJuiceMenu = mapOf("apple" to 100, "kiwi" to 190, "orange" to 100)
println(readOnlyJuiceMenu.keys)
// [apple, kiwi, orange]
println(readOnlyJuiceMenu.values)
// [100, 190, 100]
```

To check that a key or value is in a map, use the `in` operator:

```Kotlin
val readOnlyJuiceMenu = mapOf("apple" to 100, "kiwi" to 190, "orange" to 100)
println("orange" in readOnlyJuiceMenu.keys)
// true
println(200 in readOnlyJuiceMenu.values)
// false
```


## Control flow
Kotlin like other programming languages has control flow (**Conditional expressions** and **Loops**) to manage program execution scenario.

### Conditional Expressions
Kotlin provides `if` and `when` for checking conditional expressions.
#### if
To use `if`, add the conditional expression within parentheses `()` and the action to take if the result is true within curly braces `{}`:

```Kotlin
val d: Int
val check = true

if (check) {
	d = 1
} else {
	d = 2
}

println(d)
//1
```

Kotlin does not contains ternary operator `condition ? then : else`, instead you can use `if` as an expression. When using `if` as an expression, there are no curly braces `{}`:

```Kotlin
val a = 1
val b = 2

println(if (a > b) a alse b) //Returns a value: 2
```


#### When 
Use `when` when you have a conditional expression with multiple branches. `when` can be used either as a statement or as an expression.

Here is an example of using `when` as a statement:
- Place the conditional expression within parentheses `()` and the actions to take within curly braces `{}` .
- Use `->` in each branch to separate each condition from each action.

```Kotlin
val obj = "Hello"

when (obj) {
	//Checks whether obj equals to "1"
	"1" -> println("One")
	//Checks whether obj equals to "Hello"
	"Hello" -> println("Greeting")
	//Default statement
	else -> printlb("Unknown")
}
//Greeting
```

Here is an example of using `when` as an expression. The `when` syntax is assigned immediately to a variable:

```Kotlin
val obj = "Hello"

val result = when(obj) {
	//Checks whether obj equals to "1"
	"1" -> "One"
	//Checks whether obj equals to "Hello"
	"Hello" -> "Greeting"
	//Default statement
	else -> "Unknown"
}

println(result)
//Greeting
```

Previous example showed that `when` is useful for matching a variable. `when` is also useful when you need to check a chain of Boolean expressions:

```Kotlin
val temp = 18

val description = when {
	// If temp < 0 is true, sets description to "very cold"
    temp < 0 -> "very cold"
    // If temp < 10 is true, sets description to "a bit cold"
    temp < 10 -> "a bit cold"
    // If temp < 20 is true, sets description to "warm"
    temp < 20 -> "warm"
    // Sets description to "hot" if no previous condition is satisfied
    else -> "hot"             
}
prnintln(description)
//warm
```

### Ranges 
Before talking about loops, it's useful to know how to construct ranges for loops to iterate over.

The most common way to create a range in Kotlin is to use the `..` operator. For example, `1..4` is equivalent to `1, 2, 3, 4`.

To declare a range without end value, use the `..<` operator. For example, `1..<4` is equivalent to `1,2,3`.

To declare reversed range, use `downTo`. For example, `4 downTo 1` is equivalent to `4, 3, 2, 1`. 

To declare a range that increments in a step that isn't `1`,  use `step` and your desired increment value. For example, `1..5 step 2` is equivalent to `1,3,5`.

We can also do the same with `Char` ranges:
- `'a'..'d'` is equivalent to `'a', 'b', 'c', 'd'` 
- `'z' downTo 's' step 2`  is equivalent to `'z', 'x', 'v', 't'` 

### Loops 
Using our knowledge about Kotlin ranges now we can play with loops. There are 2 most common loop structures in programming. They are `for` and `while`. Use `for` to iterate over a range of values and perform an action. Use `while` to continue an action until a particular condition is satisfied.

**For** - using it we can iterate over numbers and print the number each time. Place the iterator and range within parentheses `()` with `in` keyword. Place your action to perform within curly braces `{}`:

```Kotlin
	 for (number in 1..5) {
		 //number is the iterator and 1..5 is the range
		 print(number)
	 }
	 //12345
```

Also we can iterate over collection:

```Kotlin
	val cakes = listOf("carrot", "cheese", "chocolate")

	for (cake in cakes) {
		println("Yummy, it's a $cake cake!")
	}
	
	// Yummy, it's a carrot cake!
	// Yummy, it's a cheese cake!
	// Yummy, it's a chocolate cake!
```

**While** - this loop can be used in ways:
- to execute a code  block while a conditional expression is true. (`while)
- to execute the code block first and then the conditional expression. (`do-while`)

In the first use case (`while`):
- Declare the conditional expression for your while loop to continue within parentheses `()`.    
- Add the action you want to complete within curly braces `{}`.

```Kotlin
var cakesEaten = 0
while (cakesEaten < 3) {
    println("Eat a cake")
    cakesEaten++
}
// Eat a cake
// Eat a cake
// Eat a cake
```

In the second use case (`do-while`):
- Declare the conditional expression for your while loop to continue within parentheses `()`.    
- Define the action you want to complete within curly braces `{}` with the keyword `do`.

```Kotlin
var cakesEaten = 0
var cakesBaked = 0
while (cakesEaten < 3) {
    println("Eat a cake")
    cakesEaten++
}
do {
    println("Bake a cake")
    cakesBaked++
} while (cakesBaked < cakesEaten)
// Eat a cake
// Eat a cake
// Eat a cake
// Bake a cake
// Bake a cake
// Bake a cake
```

