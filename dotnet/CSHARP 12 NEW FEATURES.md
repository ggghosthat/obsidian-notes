C# 12 includes the following new features:
- Primary Constructors
- Collection expressions
- Inline arrays
- Optional parameters in lambda expressions
- ref readonly parameters
- Alias and types
- Experimental attribute
- Interceptors

## Primary constructors
We can now create primary constructors in any `class` and `struct`. Primary constructors are not longer restricted to `record` types. Primary constructors are in scope for the entire body of the class. To ensure that all primary constructor parameters are definitely assigned, all explicitly declared constructors must call the primary constructor using `this` syntax. Adding a primary constructor to a `class` prevents the compiler from declaring an implicit parameterless constructor. In a `struct`, the implicit parameterless constructor initializes all fields, including primary constructor parameters to the 0-bit pattern. 

The compiler generates public properties from primary constructor parameters only in `record` types, either `record class` or `record struct` types. Nonrecord classes and structs might not always want this behavior for primary constructor parameters.

Example:
``` csharp
namespace Entities;

//classic constructor
public class Person
{
	public Person(string name)
	{
		//do something
	}
}

//primary constructor for class,
//does not assign to any property
public class User(string name)
{
	//do somethin
}

//primary constructor for struct,
//does not assign to any property
public struct User(string name)
{
	//do somethin
}

//record constructor, assign to property "Name"
public record Visitor(string Name);
```

## Collection expressions
Collection expressions introduce a new terse syntax to create common collection values. inlining other collections into these values is possible using a spread element `..e`. 
Several collection-like types can be created without requiring external BCL support. These types are:
- Array types, such as `int[]`
- `System.Span<T>` and `System.ReadOnlySpan<T>`
- Types that support collection initializers, such as `System.Collections.Generic.List<T>`

The following examples show uses of collection expressions:

```csharp
//create an array:
int[] a = [1, 2, 3, 4, 5, 6, 7];

//create a list:
List<string> b = ["one", "two", "three"];

//create a span:
Span<char> c = ['a', 'b', 'c', 'd', 'e', 'f', 'h', 'i'];

//create a jagged 2d array:
int[][] twoD = [[1, 2, 3], [4, 5, 6], [7, 8, 9]];

//create a jagged 2D array from variables:
int[] row0 = [1, 2, 3];
int[] row1 = [4, 5, 6];
int[] row2 = [7, 8, 9];
int[][] twoDFromVariables = [row0, row1, row2];
```

The spread element, `..e` in a collection expression adds all the elements in that expression. The argument must be a collection type. The following examples show how the spread element works:

``` csharp
int[] row0 = [1, 2, 3];
int[] row1 = [4, 5, 6];
int[] row2 = [7, 8, 9];

int[] single = [..row0, ..row1, ..row2];

foreach(var element in single)
	Console.WriteLine(element);

// output:
// 1, 2, 3, 4, 5, 6, 7, 8, 9,
```

The spread element evaluates each element of the enumerations expression. Each element is included in the output collection.

We can use collection expressions anywhere we need a collection of elements. They can specify the initial value for a collection or be passed as arguments to methods that take collection types.

## `ref readonly` parameters
C# added `in` parameters as a way to pass readonly references. `in` parameters allow both variables and values, and can be used without any annotation on arguments. 

The additional of `ref readonly` parameters enables more clarity for APIs that might be using `ref` parameters or `in` parameters:
- APIs created before `in` was introduced might use `ref` even though the argument isn't modified. Those APIs can be updated with `ref readonly`. It won't be a breaking change for caller, as would be if the `ref` parameter was changed to `in`
- APIs that take an `in` parameter, but logically require a variable. A value expression doesn't work
- APIs that use `ref` because they require a variable, but don't mutate that variable.

``` csharp
var example = new Example()

var age = 30;

example.Test(ref age);

Console.WriteLine($"The age is: {age}");

class Example()
{
	public void Test(ref readonly int age)
	{
		Console.WriteLine($"The age is: {age}");
		age++; //throw error, because it's not allowed
	}
}
```

## Default lambda parameters (optional parameters in lambda expressions)
We can now define default values for parameters on lambda expressions. The syntax and rules are the same as adding default values for arguments to any methods or local function. 

Example:
``` csharp
//before c# 12
var lambda = (int age) => $"He is {age} years old";

//starting with c# 12
var lambda = (int age = 30) => $"He is {age} years old";

lambda(30);
lambda(50);
```

## Alias any type
We can use the `using` alias directive to alias any type, not just named types. That means we can create semantic aliases for tuple types, array types, pointerr types, or other unsafe type.

Example:
``` csharp
//declaring alias 
using Point2d = (int X, int Y);

//use alias as a variable
var point2D = new Point2d(6, 9);

//deconstruct it to tuple
(int X, int Y) point = new Point2d(1, 2);
```

## Inline arrays
inline arrays are used by the .NET runtime team and other library authors to improve performance in our apps. Inline arrays enable a developer to create an array of a fixed size in a struct type. A struct with an inline buffer should provide performance characteristics similar to an unsafe fixed size buffer. We likely won't declare our inline arrays, but we can use them transparently when they're exposed as `Span<T>` or `ReadOnlySpan<T>` objects from runtime APIs.  (Hmm, that means a `Span<T>` use inline arrays under the hood)

An inline array is declared similar to the following `struct`:

``` csharp
[System.Runtime.CompilerServices.InlineArray(10)]
public struct Buffer
{
	private int _element0;
}
```

We use them like any other array:

``` csharp
var buffer = new Buffer();

for (int i = 0 ; i < 10; i++)
	buffer[i] = i;

foreach (var i in buffer)
	Console.WriteLine(i);
```

The difference is that the compiler can take advantage of known information about inline array.  We likely consume it as we would any other array.

## Experimental attribute
Types, methods, or assemblies can be marked with the `System.System.Diagnostics.CodeAnalysis.ExperimentalAttribute` to indicate an experimental features. The compiler issues a warning if you access a method or type annotated with the `ExperimentalAttribute`. All types included in an assembly marked with the `Experimental` attribute are experimental.

``` csharp
[Experimental("RiskyId")]
public class RiskyFeature
{
}
...
//warn about experimental type
var risky = new RiskyFeature();
```

## Interceptors
An interceptor is a method that can declaratively substitute a cal to an interceptable method with a call to itself at compile time. This substitution occurs by having the interceptor declare the source location of the calls that it intercepts. interceptors provide a limited facility to change the semantics of existing code by adding new code to a compilation, for example in a source generator. 

We use it as part of a source generator to modify, rather than add code to an existing source compilation. The source generator substitutes calls to an interceptable method with a call to interceptor method.

``` csharp
public class Example
{
	public void Method1()
	{
		Console.WriteLine("Method 1");
	}
	
	public void Method2()
	{
		Console.WriteLine("Method 2");
	}
}

public static class Interception
{
	[InterceptsLocation(
		filePath: "path to file with interceptable method",
		line: 6 //should be a number of line with interceptable method
		character: 9 //should be a character from starting of line with interceptable method
		)]
	public static void InterceptMethod1(this Example example)
	{
		Console.WriteLine("Hello from interceptor");		
	}
}
```