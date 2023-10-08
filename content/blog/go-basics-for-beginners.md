---
title: "Go Essentials: A Beginner's Guide to the world of Golang"
date: 2023-09-29T20:06:49+05:30
description: "In this blog, we will learn about the basics of Golang. Join me in this journey to learn about the amazing world of Go."
---

Hello everyone 👋, Today I have something interesting for you.

I was recently contributing to [Porter](https://getporter.org/) - a CNCF sandbox
project and Once I fixed the
[issue](https://github.com/getporter/porter/issues/2885) and was done with the
[pull request](https://github.com/getporter/porter/pull/2897), I was motivated
to make more contributions to the project. And, since the project was mainly
written in Golang, I thought this is a good opportunity to learn Golang.

While learning Golang myself, I made some notes which are more than sufficient
to get familiar with the syntax and necessary concepts of Golang. So, Let's get
started.

## History of Golang

- [Golang](https://go.dev) was created by Engineers at Google motivated by their
  shared dislike for C++.
- Multicore processors were becoming universal and most programming languages
  like Java offered very little to get the most out of them.
- Go was created to keep useful features and combine the -
  - easy and readable syntax of python
  - efficiency of statically typed compiled languages like C,C++.
  - support for modern, networked and multicore programming.

## How is memory allocated in Golang?

When Go starts a program, It requests a block of memory from operating system,
cuts it into small chunks and manages it itself.

The basic unit of Go memory management is the `mspan`, which consists of several
pages, each `mspan` can allocate a specific size of object.

Go's memory allocator allocates objects in three categories based on their size:

- Small objects(less than or equal to 16B)
- General objects (greater than 16B, less than or equal to 32KB)
- Large objects (greater than 32KB).

## Data types in Golang

Go has a concept of types that is either explicitly declared or implicitly
inferred.

It is a fast, statically typed, compiled language that feels like dynamically
typed, interpreted language.

- **Number**
  - **Integer** - Integer types are based on the amount of memory they acquire,
    `uint` stands for unsigned integer and `int` for signed integer.
    | Data Type | Memory |
    | --------- | ------ |
    | uint8 | 8 bits or 1 byte |
    | uint16 | 16 bits or 2 bytes |
    | uint32 | 32 bits or 4 bytes |
    | uint64 | 64 bits or 8 bytes |
    | int8 | 8 bits or 1 byte |
    | int16 | 16 bits or 2 bytes |
    | int32 | 32 bits or 4 bytes |
    | int64 | 64 bits or 8 bytes |
    | int | 4 bytes for 32-bit machines, 8 bytes for 64-bit machines |
  - **Float** - Go supports `float32` and `float64` data types, also referred to
    as single precision and double precision respectively.
    | Data Type | Memory |
    | --------- | ------ |
    | float32 | 32 bits or 4 byte |
    | float64 | 64 bits or 8 bytes |
- **Rune** - An item represented by a single value in single quotes which can
  take 1 to 4 bytes.
- **String** - It is a read-only slice of bytes and occupies 16 bytes of memory.
- **Boolean** - A boolean is either `true` or `false` which represent 0 or 1 and
  occupies 1 byte of memory.

## Variables

Now, Let's talk about how we can use variables inside Golang.

Variables are declared using `var` keyword followed by `variable_name` and its
`type` such as int, string etc.

```go
// The syntax for declaring a variable is :
// var <variable_name> <data_type>
var str string

// After declaring we can initialise variables like this

str = "Hello World!"
```

### Declaring + Initialising Variables

- Standard way

```go
// The syntax for declaring and initialising a variable is :
// var <variable_name> <data_type> = <value>

var str string = "Hello"
var num int = 10
var b bool = true
var decimal float64 = 69.420
```

- Shorthand way

```go
// Variables of same data type can be declared together like this
var f,b string = "foo","bar"

// Variables of different data type can also be declared together like this
var (
    str string = "foo"
    num int = 10
)
```

We can also use the **walrus** operator `:=` to declare and initialise variables. We
do not explicitly mention type of variable, It is implicitly assigned a type by
the compiler.

```go
str := "foo"
```

### Constants

Constants are variables whose value is initialised once and can never be changed
again. They are **untyped** unless explicitly given a type at the time of
declaration, which allows flexibility.

Constants need to be initialised at the time of declaration as the
[concept of zero value](#concept-of-zero-value) doesn't apply to constants. And,
they can not be initialised using the `:=` operator.

```go
// const <const_name> <data_type> = value

const PI float64 = 3.14

// const <const_name> = value

const PI = 3.14
```

### Printing Variables

Variables can be printed to console by using methods provided by `fmt`
package such as `Print`,`Printf`,`Println` etc.
Code to print a variable in go :

```go
package main
import "fmt"

func main() {
  var hello string = "Hello"
  var money float64 = 69.420

  fmt.Print(str , " World")
  fmt.Println(str , " World")
  // Difference between Print and Println is that Print method doesn't add
  // newline after printing a statement while Println does.

  fmt.Printf("%s World! I have $ %f in my account.", hello, money);
  // Printf stands for Print Formatter and it takes a template string with
  // format specifiers and Object args(s).
}
```

#### Printf Format specifiers

Format specifiers are prefixed with a % symbol. There are different types
of format specifiers for printing different types of variables.

| Verb  | Description                            |
| ----- | -------------------------------------- |
| %v    | default format                         |
| %T    | type of the value                      |
| %d    | integers                               |
| %c    | character                              |
| %q    | quoted characters/string               |
| %s    | plain string                           |
| %t    | true or false                          |
| %f    | floating numbers                       |
| %0.2f | floating numbers upto 2 decimal places |

### Variable Scope

Scopes are defined using Blocks which are declared using braces `{` `}`.

```go
{
  //outer block
  {
    //inner block
  }
}
```

Inner block can access variables declared in Outer block but vice versa is not
true.
e.g:-

```go
func main() {
  city := "Tokyo"
  {
    country := "Japan"
    fmt.Println(country)
    fmt.Println(city)
  }
  // fmt.Println(country) // this line will give error as Outer block cannot
  // access variable `country` defined in inner block
  fmt.Println(city)
}
```

### Local vs Global Variables

- **Local Variables**

Local variables are declared inside a function or a block, also inside loops
or conditional statements. These are only available inside and are not
accessible outside the function or block.

```go
package main
func main() {
  name := "Zoro" // `name` is a local variable only available inside main func
}
```

- **Global Variables**

Global variables are declared outside of a function/block and are available
throughout the lifetime of a program. These variables are declared at the top of
the program outside of any function or block and cannot be declared using the
walrus `:=` operator, these have to be declared in the standard way.

```go
package main
import "fmt"

var name string = "Zoro"
// `name` is a global variable available for use anywhere in the program

func main() {
  fmt.Println(name)
}
```

### Concept of Zero Value

When you declare a variable and do not initialise it, It is given a default
value by the compiler known as `zero value` which is different for different
data types.
e.g:-

| Data Types | Zero values |
| ---------- | ----------- |
| bool       | true        |
| int        | 0           |
| float64    | 0.0         |
| string     | ""          |
| etc.       | ...         |

## How to take user input?

`fmt` package provides a function `Scanf` which is used to take input from user.

- It takes a format string containing format specifiers, along with a variable
  number of arguments prefixed with ampersand `&` operator which means the
  address of the variable.

- Taking a single Input

  ```go
  package main
  import "fmt"

  func main() {
    var name string
    fmt.Print("Enter your name: ")
    fmt.Scanf("%s", &name)
    fmt.Println("Hello ",name)
  }
  ```

- Taking Multiple Inputs

  ```go
  package main
  import "fmt"

  func main() {
    var name string
    var is_student bool
    fmt.Print("Enter your name and Are you a student?: ")
    fmt.Scanf("%s %t", &name, &is_student)
    fmt.Println(name, is_student)
  }
  ```

- Scanf returns two values `count` and `err` which stands for the number of
  arguments that the function writes to and any error thrown during the
  execution of scanf function.

  ```go
  package main
  import "fmt"

  func main() {
    var str string
    var num int
    fmt.Print("Enter a string and a variable: ")

    count, err := fmt.Scanf("%s %d", &str, &num)

    fmt.Println("count: ",count)
    fmt.Println("error: ",err)
    fmt.Println(str, num)
  }
  ```

  ```bash
  ❯ go run main.go
  Enter a string and a variable: hello world
  count:  1
  error:  expected integer
  hello 0
  ```

  Here, if we enter string two times then we will get an error. And the value of
  count is 1 as only the first input was handled successfully by Scanf which was
  `str` and It was assigned the value **"hello"** . But, `num` variable couldn't
  be assigned the given value as It was expecting an integer, So, It was
  assigned the zero value which is **0** for integers.

## More on Types

### Checking Types

We can check data types of variable using `%T` or `reflect.TypeOf` provided by
reflect package.

- Using `%T`

  We can use `%T` format specifier to check the type of any variable

  ```go
  fmt.Printf("Variable Type of %v is %T", variable_name)
  ```

- Using `reflect.TypeOf()`

  ```go
  package main
  import (
    "fmt"
    "reflect"
  )
  func main() {
    var sanji int = 3
    var quote string = "My hands are only for cooking."

    fmt.Printf("Variable sanji=%d is type of %v\n", sanji,reflect.TypeOf(sanji))
    fmt.Printf("Variable quote=%d is type of %v\n", quote,reflect.TypeOf(quote))
  }
  ```

### Type Casting/Conversion

The process of converting one data type to another is called Type Casting or
Conversion. However, It does not guarantee that the value will remain intact.

```go
package main
import "fmt"

func main() {
    var f float64 = 69.420
    var i int = int(f)
    fmt.Println("Integer Value: ",i)
}
```

```bash
❯ go run main.go
Integer Value: 69
```

Here the decimal value got truncated while converting float to integer.

Type Conversion can also be done by methods provided by a package `strconv`

- `Itoa()` - Converts integer to string and returns the value.

  ```go
  package main
  import (
    "fmt"
    "strconv"
  )

  func main() {
      var i int = 69
      var s string = strconv.Itoa(i) // convert int to string
      fmt.Println("String: ",s)
  }
  ```

  It will print "69" as string.

- `Atoi()` - Convert string to integer and returns two values - integer, error

  ```go
  package main
  import (
    "fmt"
    "strconv"
  )

  func main() {
      var s string = "69"
      i, err := strconv.Atoi(s) // convert string to int
      fmt.Println("Integer: ",i);
      fmt.Println("Error: ",err);
  }
  ```

  Since the string contains "69", It is correctly converted to string and the
  error is nil.
  If it contained any character such as a-z,A-z,symbols etc, Then It would have
  given an error.

## Conditionals

### If-else and else if

```go
if condition_1 { // parenthesis () around the condition is optional
    // execute when condition_1 is true
} else if condition_2 { // else should start from the same line where if block ends
    // execute when condition_2 is true
} else {
    // if none of the condition is true
}
```

### Switch Case

The expression doesn't need to be in parenthesis and break; statement is also
not needed.

```go
switch expression {
  case value_1:
    // execute when expression equals to value_1
  case value_2, value_3:
    // execute when expression equals to value_2 or value_3
  default:
    // execute when no matches found
}
```

#### the `fallthrough` keyword

It is used to force the execution flow of switch case.

```go
switch expression {
  case value_1:
    // execute when expression equals to value_1
  case value_2:
    // execute when expression equals to value_2
    fallthrough // It forces to execute the successive(next) case block
  case value_3:
    // execute when expression equals to value_3 or value_2 since fallthrough is
    // used
  default:
    // execute when no matches found
}
```

#### Switch with conditions

We don't give expression to switch statement and instead we can give conditions
for each cases.

```go
switch {
  case condition_1:
    // execute when condition_1 is true
  case condition_2:
    // execute when condition_2 is true
  default:
    // execute when no conditions are true
}
```

## Looping in Go

There is only one loop in Go that is `for` loop.

```go
for initialisation; condition; post {
  // statement(s)
}
```

First initialisation happens, then if condition is true, statements inside loop
are executed and after execution is completed, post statement (mostly increment
of decrement) is executed.

- **Infinite Loop** - If the condition of For Loop is omitted (not provided)
  then it becomes an infinite Loop.

- **Break and Continue**
  <br/>`break` statement ends the loop immediately when it is encountered inside
  loop.
  <br/>`continue` statement skips the current iteration and goes to the next one.

## Arrays in Go

An Array is a collection of similar data elements stored at contiguous memory
locations.

In Golang, Arrays are of fixed length, And since, we have [pointers](#pointers)
in Go, we can get the address of any element of array.

```go
// Array Declaration
// var <array_name> [<size_of_array>] <data_type>

var num [5]int

// Array Declaration and Initialisation
// var <array_name>[<size_of_array>]<data_type> = [<size_of_array>]<data_type>{<values>}

var num [5]int = [3]int{6,9,4,2,0}

// Shorthand
// <array_name> := [<size_of_array>]<data_type>{<values>}

num := [3]int{6,9,4,2,0}

// Shorthand using ellipsis(...)
// <array_name> := [...]<data_type>{<values>}

num := [...]int{6,9,4,2,0}
```

### Length of Array

To calculate length of an Array, we can use builtin `len()` function.

```go
fruits := [4]string { "this", "is", "a", "test" }
fmt.Println(len(fruits))
```

### Looping through Array

- Basic for loop

```go
arr := [3]int {6,9,4,2,0}

for i := 0; i < len(arr[i]); i++ {
  fmt.Println(arr[i]);
}
```

- using range keyword

```go
arr := [3]int {6,9,4,2,0}

for index, element := range arr {
  fmt.Println(index, "->", element)
}

// If we don't need index, we can replace it with underscore `_`
for _, element := range arr {
  fmt.Println(element)
}
```

### MultiDimensional Array

```go
// 2D Array
arr := [3][2]int {{1, 2}, {3, 4}, {5, 6}}

fmt.Println(arr[2][1]) // This will print 6
```

## Slices

A Slice is a continous segment of an underlying array, which offer more
flexibility as they are variable typed (elements can be added or removed).

Slices have three major components

- **pointer** - It points to the first element of array accessible through the
  slice.
- **length** - It is the number of elements in slice, can be accessed using
  `len()` function.
- **capacity** - It is the number of elements in the underlying array counting
  from the first element of the slice, can be accessed using `cap()` function.

### Creating a Slice

```go
// <slice_name> := []<data_type>{<values>}
grades := []int{10, 20, 30}
```

Creating slice from an array from `start_index` till the `end_index`
(`end_index` is not included).

```go
// array[start_index : end_index]
arr := [8]int{2, 3, 4, 5, 6, 7, 8, 9}

arr[1:5] // [3, 4, 5, 6]
// array -> | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 |
//                ^
//                Slice Pointer
// slice -> | 3 | 4 | 5 | 6 | -> length = 4, capacity = 7
```

If we omit the `start_index`, it will be 0 by default and if we omit the
`end_index`, it will be the length of array by default.

```go
// array[start_index : end_index]
arr := [5]int{11, 12, 13, 14, 15}

arr[ :3] // [11, 12, 13]
arr[2: ] // [13, 14, 15]
arr[ : ] // [11, 12, 13, 14, 15]
```

Using `make` function

```go
// slice := make([]<data_type>, length, capacity)
slice := make([]int, 5, 8)
```

Since Slices are references to the original array, If we mutate the slice it
will aslo mutate the original array from which the slice was created.

```go
arr := [5]int{11, 12, 13, 14, 15}

slice = arr[ :3] // [11, 12, 13]
slice[1] = 1000

// Now the slice will become, slice - [11, 1000, 13]
// And, the original array, arr - [11, 1000, 13, 14, 15]
```

### Appending to Slice

`append` function is used to append a slice or values of the same type as that
of the slice to the slice.

If the number of total values after appending become more than the capacity of
the slice, then the slice's capacity will be doubled.

- Appending values to slice

  ```go
  // slice = append(slice, element_1, element_2)

  new_slice = append(slice, 10, 20, 30)
  ```

- Appending slice to slice

  ```go
  // slice = append(slice, anotherSlice...)

  new_slice := append(slice_1, slice_2...)
  ```

### Deleting from Slice

To delete an element from a slice, we can just create a new slice which doesn't
contain the element to be deleted.

```go
arr := [5]int {10, 20, 30, 40, 50}

i := 2 // index of element to be deleted

slice_1 := arr[:i] // [10, 20]
slice_2 := arr[i+1:] // [40, 50]

new_slice := append(slice_1, slice_2...)
// Now new_slice consists of [10, 20, 40, 50] and the element at index 2 got
// deleted
```

### Copy from a Slice

```go
// func copy(dst, src []Type) int
// num := copy(dest_slice, src_slice)

src_slice := []int{10, 20, 30, 40, 50}
dest_slice := make([]int, 3)

num := copy(dest_slice, src_slice)
```

## Maps in Go

Maps are unordered collection of key-value pairs, implemented using hash tables.

- Zero value of a map is `nil`.
- Length of a map can be calculated using `len()` function.

```go
// var <map_name> map[<key_data_type>]<value_data_type>
var my_map map[string]int // creates a nil map

// <map_name> := map[<key_data_type>]<value_data_type>{<key_value_pairs>}
my_map := map[string]string{"h": "ello", "w": "orld"}

// <map_name> := make(map[<key_data_type>]<value_data_type>, <initial_capacity>)
my_map := make(map[string]int)
```

### Access Items of Map

- Access value using key

```go
my_map := map[string]string{"h": "ello", "w": "orld"}

fmt.Println(my_map["h"]) // Output : ello
```

- Getting a key

```go
// value, found := map_name[key]
my_map := map[string]string{"h": "ello", "w": "orld"}

value, found := my_map["h"]
fmt.Println(found, value) // Output: true, ello
```

### Adding/Deleting a key-value pair

```go
my_map := map[string]string{"h": "ello", "w": "orld"}

my_map["t"] = "est" // adds a key-value pair

fmt.Println(my_map) // Output: map[h:ello w:orld t:est]

delete(my_map, "w") // deletes a key-value pair

fmt.Println(my_map) // Output: map[h:ello t:est]
```

### Clearing/Truncating a map

Items can be removed one by one using a for loop or Reinitializing the map can
also clear all items from the map.

```go
my_map := map[string]string{"h": "ello", "w": "orld"}
my_map := make(map[string]string) // reinitializing with make truncates the map
```

## Functions

Functions are self-contained units of code which do a certain task, and help us
divide a program into organisable and reusable chunks.

```go
// func <function_name>(<params>) <return_type> {
//   function body
// }

func addNumbers(a int, b int) int {
  sum := a + b
  return sum;
}

addNumbers(10, 20)
```

**Return Type** - A function can or can not have return value(s).

```go
// standard return values
func operation(a int, b int) (int, int) {
  sum := a + b
  diff := a - b
  return sum, diff
}

// named return values
func operation(a int, b int) (sum int, diff int) {
  sum := a + b
  diff := a - b
  return
}

func main() {
  sum, difference := operation(20, 10)
  fmt.Println(sum, " ", difference)
}
```

### Variadic functions

Variadic functions have variable number of parameters.

```go
// func <function_name>(param1 type, param2 type, param3 ...type) <return type>

func sumNumbers(numbers ...int) int

func sumNumbers(str string, numbers ...int) int
```

The Variadic parameter numbers is a slice of all the arguments passed to the
function.

```go
func printDetails(student string, subjects ...string) string {
  fmt.Println("hi ", student, " /n Here are your subjects - ")
  for _, sub := range subjects {
    fmt.Println(sub, " ")
  }
  return sum
}

func main() {
  fmt.Println(printDetails("Rohan", "English"))
  fmt.Println(printDetails("Sohan", "Mathematics", "English", "Science"))
}
```

### Anonymous function

Anonymous functions are functions declared without any named indentifier to
refer to it.

```go
func main() {
  x := func(l int, b int) int { // Anonymous function
    return l * b
  }
  fmt.Printf("%T , %v", x, x(20, 50))
}

// Output: func(int, int) int, 1000
```

**Defer Statement** - A defer statement delays the execution of a function until
the surrounding function returns.

```go
func printString(str string) {
  fmt.Println(str)
}
func printNumber(int num) {
  fmt.Println(num)
}

func main() {
  defer printNumber(101) // delays the function execution
  printString("GoLang")
}

// Output:
// GoLang
// 101
```

## Pointers

A _Pointer_ is a variable that holds the memory address of another variable. It
points to the address where the memory is allocated and provides ways to find
or even change the value located at that address.

### Address and Dereference operator

- `&` operator
  The ampersand `&` or address-of operator is used to get the address of a
  variable by prefixing the variable name with this operator.

- `*` operator
  The asterisk `*` or dereference operator is used to get the value at a memory
  location by prefixing the address with this operator.

```go
// Declaring a Pointer
// var <pointer_name> *<data_type>
var ptr_i *int
var ptr_s *string

// Initialising a Pointer
// var <pointer_name> *<data_type> = &<variable_name>
i := 10
var ptr_i *int = &i // ptr is a pointer which holds the address of variable i

// Shorthand
s := "hello"
ptr_s = &s
```

We can get or modify the value of a variable using `*` operator on a pointer
that holds the address of that variable.

```go
s := "hello"
ps := &s

fmt.Println(s, *ps)

*ps := "world"

fmt.Println(s, *ps)

// Output:
// hello hello
// world world
```

### Passing by value

Function is called directly passing the value of variable as argument, so
modifying the variable inside the function doesn't affect the original variable
as the parameter is copied into another location of memory.

All basic data types such as int, bool, string etc are Pass by value by default.

```go
func modify(n int) {
  n += 10
}

func main() {
  num := 15
  fmt.Println(num)
  modify(num)
  fmt.Println(num)
}

// Output:
// 15
// 15
```

### Passing by Reference

By using pointers, we can pass the references of variables as arguments and when
their value is modified the value of original variable is also modified as the
memory address of the original variable is passed using pointer.

Slices are references to an underlying Array so they are Pass by reference, Maps
are also Pass by reference by default.

```go
func modify(n *int) {
  *n += 10
}

func main() {
  num := 15
  fmt.Println(num)
  modify(&num)
  fmt.Println(num)
}

// Output:
// 15
// 25
```

## Structs

Structs are used to create custom data types by grouping various data elements
together and referencing them through a single variable name.

> Note: Structs are also Pass by value by default, so to modfiy values on Struct
> use pointer to follow Pass by reference.

### Declaration and Initialisation

```go
// Declaration
// type <struct_name> struct {
//   list of fields
// }

type Student struct {
  name string
  rollNo int
  marks []int
  grades map[string]int
}

// Initialising
// var <variable_name> <struct_name>
var s Strudent

// Initialising using new keyword
// <variable_name> := new(<struct_name>)
st := new(Strudent)

st := Student{
  name: "Rohan",
  rollNo: 10,
  marks: {80, 74, 96}
}
```

### Accessing Fields

```go
// <variable_name>.<field_name>

type Student struct {
  name string
  rollNo int
  marks []int
  grades map[string]int
}

var st Student

st.name = "Sohan"
fmt.Println(st.name, st.rollNo)
```

> Equality : Two structs will be equal only if they are created from same Struct definition
> and they also have same values.

## Method

A Method is a function that has a defined reciever (extra parameter after func
keyword).

```go
func (s Student) getMarks() float64 {
  // code
}
func (s *Student) getMarks() float64 {
  // code
}
```

Example:

```go
type Circle struct {
  radius float64
  area float64
}

func (c *Circle) calcArea() {
  c.area = 3.14 * c.radius * c.radius
}

func main() {
  c := Circle{radius: 5}
  c.calcArea()
  fmt.Printf("%+v", c)
}

// Output: {radius:5 area:78.5}
```

### Method sets

A set of methods that are available to a data type and are useful to encapsulate
functionality.

```go
type Student struct {
  name string
  grades []int
}

func (s *Student) displayName() {
  fmt.Println(s.name)
}

func (s *Student) calculatePercentage() float64 {
  sum := 0
  for _, v := range s.grades {
    sum += v
  }
  return float64(sum*100) / float64(len(s.grades)*100)
}

func main() {
  s := Student{name: "Rohan", grades: []int{90, 75, 84}}
  s.displayName()
  fmt.Printf("%.2f%%", s.calculatePercentage())
}
```

## Interfaces

An interface is like a blueprint for a method set. It specifies a method set and
is a powerful way to introduce modularity in Go. It describes all the methods of
a method set by providing the function signature for each method but does not
implement them.

```go
// type <interface_name> interface {
//  method signatures
// }

type FixedDeposit interface {
  getRateOfInterest() float64
  calcReturn() float64
}
```

### Implementing Interface

```go
type shape interface {
  area() float64
  perimeter() float64
}

type square struct {
  side float64
}

func (s square) area() float64 {
  return s.side * s.side
}

func (s square) perimeter() float64 {
  return 4 * s.side
}

type rect struct {
  length, breadth float64
}

func (r rect) area() float64 {
  return r.length * r.breadth
}

func (r rect) perimeter() float64 {
  return 2*(r.length+r.breadth)
}

func printData(s shape) {
  fmt.Println(s)
  fmt.Println(s.area())
  fmt.Println(s.perimeter())
}

func main() {
  r := rect{length: 3, breadth: 4}
  s := square{side: 5}
  printData(r)
  printData(c)
}
```

## Final Remarks

So, These were the important concepts of Golang, And I know this was a lot but
if you made it till here, then Congrats 🥳.

If you liked this blog, found any mistakes or just want to say Hi, feel free to
send an [email](mailto:zelfroster@gmail.com) or personal message me on
[X/Twitter](https://twitter.com/zelfroster).

Now, I will see you in the next blog. Until then keep learning and take care,
Bye.
