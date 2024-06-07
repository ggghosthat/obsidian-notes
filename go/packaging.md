## Packages 

Every Go program is made up of packages.
Programs start running in package `main`. 
Example:

```Go
package main

import (
	"fmt"
	"math/rand"
)

func main() {
	fmt.Println("Hello world!")
}
```

This program is using the packages with import path `"fmt"` and `"math/rand"`

By convention, the package name is the same as the last element of the import path. For instance, the `"math/rand"` package comprises files that begin with the statement `package rand`.

## Exported names
In Go, a name is exported if it begins with a capital letter. For example, `Pizza` is an exported name, as is `Pi`, which is exported from the `math` package.

`pizza` and `pi` do not start with capital letter, so they are not exported.

When importing a package, you can refer only to its exported names. Any "unexported" names are not accessible from outside  the package.

```Go
package main

import (
	"fmt"
	"math"
)

func main() {
	//GOOD
	fmt.Println(math.Pi)
	//ERROR use Pi instead of `Pi`
	fmt.Println(math.pi)
}
```

## Functions
A function can take zero or more arguments.

```Go
package main

import "fmt"

func add(x int, y int) int {
	return x + y
}

func main() {
	fmt.Println(add(12, 12)) //24
}
```

In this example, `add` takes two parameters of type `int`.

**Notice** that the type comes after the variable name.

When two or more consecutive named function parameters share a type, you can omit the type from all but the last.

```Go
package main

import "fmt"

func add(x, y int) int {
	return x + y
}

func main() {
	fmt.Println(add(14, 13)) //27
}
```

In this example, we shortened
`x int, y int` to `x, y int`

Also function can return any number of results. 

```Go
package main

import "fmt"

func swap(x, y string) (string, string) {
	return y, x
}

func main() {
	a, b := swap("hello", "world") //hello, world
	fmt.Println(a, b) //world, hello
}
```

## Named return values
Go's return values maybe named. If so, they are treated as variables defined at the top of the function.

These names should be used to document the meaning of the return values.

A `reutn` statement without arguments returns the named return values. This is known as a "naked" return.

Naked return statements should be used only in short function as with the example shown here. They can harm readability in longer functions.

For example:
```Go
package main

import "fmt"

func split(sum int) (x, y int) {
	x = sum * 4 / 9
	y = sum - x
	return
}

func main() {
	y, x := split(17)
	fmt.Println(y, x)
}
```

## Variables
The `var` statement declares a list of variables, as infunction arguments lists, the  type is last.

A `var` statement can be at package or function level. We see both in this example below: 

```Go
package main

import "fmt"

var c, python, java, bool

func main() {
	var i int
	fmt.Println(i, c, python, java)
}
```

## Variables with initializers

A `var` declaration can include initializers, one per variable.

If an initializer is present, the type can be omitted, the variable will rake the type of the initializer.

```Go
package main

import "fmt"

var i, j int = 1, 2

func main() {
	var c, python, java = true, false, "no!"
	fmt.Println(i, j, c, python, java)
}
```

## Short variable declarations
Inside a function. the `:=` short assignment statement can be used in place of a `var` declaration with implicit type.

Outside a function, every statement begins with a keyword (`var`, `func` and so on) and so the `:=` construct is not variable.

```Go
package main

import "fmt"

func main() {
	var i, j int = 1, 2
	k := 3
	c, python, java := true, false, "no!"
	
	fmt.Println(i, j, k, c, python, java)
}
```

## Basic types
Go's basic types are 
```Go
bool

string

int  int8  int16  int32  int64
uint uint8 uint16 uint32 uint64 uintptr

byte // alias for uint8

rune // alias for int32
     // represents a Unicode code point

float32 float64

complex64 complex128
```

The example shows variables of several type and also that variable declarations may be "factored" into blocks, as with import statements. 

The `int`, `uint`, `uintptr` types are usually 32 bits wide on 32-bit systems and 64 bits wide on 64-bit systems. When you need an integer value you should use `int` unless you have a specific reason to use a sized or unsigned integer type.

Example:
``` Go
package main

import (
	"fmt"
	"math/cmplx"
)

var (
	ToBe   bool       = false
	Maxint uint64     = 1<<64 - 1
	z      complex128 = cmplx.Sqrt(-5 + 12i)
)

func main() {
	fmt.Printf("Type: %T Value: %v\n", ToBe, ToBe)
	fmt.Printf("Type: %T Value: %v\n", MaxInt, MaxInt)
	fmt.Printf("Type: %T Value: %v\n", z, z)
}
```

## Zero values
Variables declared without an explicit initial value are given their zero zero value.

the zero value is:
- `0` for numeric types
- `false` for the boolean type, and
- `""` (the empty string) got strings

``` Go
package main

import "fmt"

func main() {
	var i int
	var f float64
	var b bool
	var s string
	fmt.Printf("%v %v %v %q\n", i, f, b, s)
}
```

## Type conversions
The expression `T(v)` converts the value `v` to the type `T`.

Some numeric conversions:
``` Go
var i int = 42
var f float64 = float64(i)
var u uint = uint(f)
```

Or, put more smiply:
```Go
i := 42
f := float64(j)
u := uint(f)
```

Unlike in C, in Go assignment between items of different type requires an explicit conversion.

Example:
``` Go
package main
import (
	"fmt"
	"math"
)

func main() {
	var x, y int 3, 4
	var f float64 = math.Sqrt(float64(x*x + y*y))
	var z uint = uint(f)
	fmt.Println(x, y, z)
}
```

## Type inference
When declaring a variable without specifying an explicit type (either by using the `:=` syntax or `var =` expression syntax), the variable's type is inferred from the value in the right hand side.

When th right hand side of the declaration is typed, the new variable is of that same type:

``` Go
var i int
j := i // j is an int
```

but when the right hand side contains an untyped numeric constant, the new varible may bt an `int`, `float64` or `complex128` depending on the precision of the constant:
``` Go
i := 42           // int
f := 3.142        // float64
g := 0.867 + 0.5i // complex128
```

Example:
``` Go
package main

import "fmt"

func main() {
	v := 42 // change me!
	fmt.Printf("v is of type %T\n", v)
}
```

## Constants
Constants are declared like variables, but with the `const` keyword.

Constants can be character, string, boolean, or numeric values.

Constants cannot be declared using the `:=` syntax.

``` Go
package main

import "fmt"

const Pi = 3.14

func main() {
	const World = "世界"
	fmt.Println("Hello", World)
	fmt.Println("Happy", Pi, "Day")

	const Truth = true
	fmt.Println("Go rules?", Truth)
}
```

## Numeric constants
Numeric constants are high-precision values.

An untyped constant takes the type needed by its context

Example:
``` Go
package main

import "fmt"

const (
	// Create a huge number by shifting a 1 bit left 100 places.
	// In other words, the binary number that is 1 followed by 100 zeroes.
	Big = 1 << 100
	// Shift it right again 99 places, so we end up with 1<<1, or 2.
	Small = Big >> 99
)

func needInt(x int) int { return x*10 + 1 }
func needFloat(x float64) float64 {
	return x * 0.1
}

func main() {
	fmt.Println(needInt(Small))
	fmt.Println(needFloat(Small))
	fmt.Println(needFloat(Big))
}

```