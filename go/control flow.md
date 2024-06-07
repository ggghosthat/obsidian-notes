## For
Go has only one looping construct, the `for` loop.
The basic `for` loop has three components separated by semicolons:
 - the init statement: executed before the first iteration
 - the condition expression: evaluated before every iteration
 - the post statement: executed at the end of every iteration

The init statement will often be a short variable declaration, and the variables declared  there are visible only in the scope of the `for` statement

The loop will stop iterating once the boolean condition evaluates to `false`.

**Note** Unlike other languages like C, Java, or JavaScript there are no parentheses surrounding the three components of the `for` statement and the braces `{}` are always required. 

Example:
```Go
package main

import "fmt"

func main() {
	sum := 0
	for i:= 0; i < 10; i++ {
		sum += i
	}
	fmt.Println(sum)
}
```

Moreover, here we should say about the fact , that init and post statements are optional. See example below:

``` Go
package main

import "fmt"

func main() {
	sum := 1
	for ; sum < 1000; {
		sum += sum
	}
	fmt.Println(sum)
}
```

## While in Go
Also we can drop out the semicolon: C's `while` is spelled `for` in Go. See example below:
``` Go
package main

import "fmt"

func main() {
	sum := 1
	for sum < 100 {
		sum += sum
	}
	fmt.Println(sum)
}
```

### forever loop
If we omit the condition it loops forever, so an infinite loops compactly expressed:

``` Go
package main

func main() {
	for{
	}
}
```

## If
Go's `if` statement is needn't be surrounded by parentheses `()`, but the braces `{}` are required.

``` Go
package main

import (
	"fmt"
	"math"
)

func sqrt(x float64) string {
	if x <  0 {
		return sqrt(-x) + "i"
	}
	return fmt.Sprint(math.Sqrt(x)) 
}

func main() {
	fmt.Println(sqrt(2), sqrt(-4))
}
```

## If with a short statement
Like `for`, the `if` statement can start with a short statement to execute before the condition. 
Variables declared by the statement are only in scope until the end of the `if`

``` Go
package main 

import (
	"fmt"
	"math"
)

func pow(x, n, lim float64) float64 {
	if v := math.Pow(x, n); v < lim {
		return v
	}
	return lim
}

func main() {
	fmt.Println(
		pow(3, 2, 10),
		pow(3, 3, 20),
	)
}
```

## If and else
Variables declared inside an `if` short statement are also available inside any of the `else` blocks.

``` Go
package main

import (
	"fmt"
	"math"
)

func pow(x, n, lim float64) float64 {
	if v := math.Pow(x, n); v < lim {
		return v
	} else {
		fmt.Printf("%g >= %g'n", v, lim)
	}
	
	return lim
}

func main() {
	fmt.Println(
		pow(3, 2, 10),
		pow(3, 3, 20),
	)
}
```

## Switch
A `switch` statement is a shorter way to write a sequence if `if - else` statements. It runs the first case whose value is equal to the condition expression. 
Go's `switch` is like the one in C, C++, Java, JavaScript, and PHP, except that Go only runs the selected case, not all the cases that follow in effect, the `break` statement that is needed at the end of each case in those languages is provided automatically in Go. Another important difference is that Go's switch cases need not be constants, and the values involved need not be integers

``` Go
package main

import (
	"fmt"
	"runtime"
)

func main() {
	fmt.Println("Go runs on")
	switch os := runtime.GOOS; os {
		case "darwin":
			fmt.Println("OS X.")
		case "linux":
			fmt.Println("Linux.")
		default:
			fmt.Println("%s. \n", os)
	}
}
```

## Switch evaluation order
Switch cases evaluate cases from top to bottom, stopping when a case succeds.

``` Go
switch i {
case 0:
case f()
}
```

does not call `f` if `i==0`

``` Go
package main

import (
	"fmt"
	"time"
)

func main() {
	fmt.Println("When's Saturday?")
	today := time.Noww().Weekday()
	switch time.Saturday {
	case today + 0:
		fmt.Println("Today.")
	case today + 1:
		fmt.Println("Tomorrow.")	
	case today + 2:
		fmt.Println("In two days.")
	default:
		fmt.Println("Too far away.")
	}
}
```

## Switch with no condition
Switch without  a condition is the same as `switch true`.
This construct can be a clean way to write long if-then-else chains.

``` Go
package main

import (
	"fmt"
	"time"
)

func main() {
	t := time.Now()
	switch {
		case t.Hour() < 12:
			fmt.Println("Good morning!")
		case t.Hour() < 17:
			fmt.Println("Good afternoon!")
		default:
			fmt.Println("Good evening!")
	}
}
```

## Defer
A defer statement defers the execution of a function until the surrounding functions returns. (Call deferred function while returning surrounding one (in the end of function))
The deferred call's arguments are evaluated immediately, but the function call is not executed until the surrounding function returns.

``` Go
package main

import "fmt"

func main() {
	defer fmt.Println("world")
	
	fmt.Println("Hello")
}
```

## Stacking defers
Deferred function calls are pushed onto a stack. When a function returns, its deferred calls are executed in last-in-first-out order.

``` Go
package main

import "fmt"

func main() {
	fmt.Println("counting")
	for i:= 0; i < 10; i++ {
		defer fmt.Println(i)
	}
	
	fmt.Println("done")
	//counting
	//done
	//9
	//8
	//7
	//6
	//5
	//4
	//3
	//2
	//1
	//0
}
```