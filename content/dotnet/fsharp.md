# F# syntax cheet

This is taken from the following [github repo](https://github.com/adelarsq/fsharp-cheatsheet)


## Comments

```fsharp
// These is a line comments

(* These are 
    block comment *)

/// the `let` keyword defines a value
let result = 1 + 1 = 2
```

## Strings

```fsharp
// Create a string concatenating
let hello = "Hello " + "World"

//Use verbatim string preceded by @ to avoid escaping control characters
let verbatimXml = @"<book title=""Paradise Lost"">"

//We don't have to escape `"` with triple quoted strings
let tripleXml = """<book title="Paradise Lost">"""

//Backlash strings
let poem = 
    "Lorem ipsum dolor sit amet,\n\
    consectetur adipiscing elit,\n\
    sed do eiusmod tempor incididunt\n\
    ut labore et dolore magna aliqua."

//Interpolated strings
let name = "Dude"
let age = 22

printfn $"Name: {name}, Age: {age}"
```

## Basic Types

```fsharp
///`uy` for unsigned 8 bit int
///`L` for signed 64 bit integer
///`UL` for unsigned 64 bit integer
let a, b, c, d = 80uy, 80, 80L, 80UL

// val a: byte = 80uy
// val b: int = 80
// val c: int64 = 80L
// val d: uint64 = 80UL

///For floats, decimals and integers
let e, f, g, h = 4.14F, 4.14, 0.7833M, 9999I

// [val e: float32 = 4.14f]
// [val f: float = 4.14]
// [val g: decimal = 0.7833M]
// [val h: System.Numerics.BigInteger = 9999]
```

## Format

```fsharp
printfn "Hello, World"
printfn $"The time is {System.DateTime.Now}"

///With formatting
let data = [1..10]

printfn $"The numbers %d{1} to %d{10} are %A{data}"

///Or

printfn "The numbers %d to %d are %A" 1 10 data
```

## Loops
```fsharp
///For loops

let list1 = [1; 5; 100; 450; 788]

for i in list1 do
    printf "%d" i

let seq1 = seq { for i in 1 .. 10 -> (i, i * i) }

for (a, asqr) in seq1 do
    printfn "%d squared is %d" a asqr

for i in 1 .. 10 do
    printf "%d " i

for i = 10 downto 1 do
    printf "%i " i

for i in 1 .. 2 .. 10 do
    printf "%d " i

for c in 'a' .. 'z' do
    printf "%c " c

// Using of a wildcard character (_)
// when the element is not needed in the loop.
let mutable count = 0

for _ in list1 do
    count <- count + 1

///While loops
let mutable mutVal = 0
while mutVal < 10 do
    mutVal <- mutVal + 1
```
## Functions

```fsharp
///Define functions with the `let` keyword

let pi () = 3.14159 // func with no arguments
pi ()               // use () to call the func

let negate x = x * -1 
let square x = x * x 
let print x = printfn $"The number is: %d{x}"

let squareNegateThenPrint x = 
    print (negate (square x)) 

///Pipe operator |> is used to chain funcs
let squareNegateThenPrint x = 
    x |> square |> negate |> print

///Composition operator >> is used to compose funcs
let squareNegateThenPrint = 
    square >> negate >> print
```

## Pattern Matching

```fsharp
///Using match keyword
let rec fib n =
    match n with
    | 0 -> 0
    | 1 -> 1
    | _ -> fib (n - 1) + fib (n - 2)

///Use when to create filters
let sign x = 
    match x with
    | 0 -> 0
    | x when x < 0 -> -1
    | x -> 1

///Use func
let rec fib2 = function
    | 0 -> 0
    | 1 -> 1
    | n -> fib2 (n - 1) + fib2 (n - 2)
```

## Collections

### Lists

```fsharp
/// Lists use square brackets and `;` delimiter
let list1 = ["a"; "b"]

// :: is prepending
let list2 = "c" :: list1

// @ is concat    
let list3 = list1 @ list2   

// Recursion on list using (::) operator
let rec sum list = 
    match list with
    | [] -> 0
    | x :: xs -> x + sum xs

//Generating lists
[ 1; 3; 5; 7; 9 ]
[ 1..2..9 ]
[ for i in 0..4 -> 2 * i + 1 ]
List.init 5 (fun i -> 2 * i + 1)
```
### Arrays

```fsharp
/// Arrays use square brackets with bar
let array1 = [| "a"; "b" |]

// Indexed access using dot
let first1 = array1.[0]   
let first2 = array1[0]    // F# 6

//Generating arrays
[| 1; 3; 5; 7; 9 |]
[| 1..2..9 |]
[| for i in 0..4 -> 2 * i + 1 |]
Array.init 5 (fun i -> 2 * i + 1)
```

### Sequences

```fsharp
/// Sequences can use yield and contain subsequences
seq {
    // "yield" adds one element
    yield 1
    yield 2

    // "yield!" adds a whole subsequence
    yield! [5..10]
}

// Sequences can use yield and contain subsequences
seq {
    1
    2
    yield! [5..10]
}
```

### Dictionaries

```fsharp
open System.Collections.Generic

let inventory = Dictionary<string, float>()

//Add key/values
inventory.Add("Apples", 0.33)
inventory.Add("Oranges", 0.5)

//Remove key/values
inventory.Remove "Oranges"

// Read the value. If not exists - this throws.
let bananas1 = inventory.["Apples"]
let bananas2 = inventory["Apples"]   // F# 6

// Generic type inference with Dictionary
let inventory = Dictionary<_,_>()   // or let inventory = Dictionary()

inventory.Add("Apples", 0.33)

//Immutable Dictionaries
let inventory : IDictionary<string, float> =
    ["Apples", 0.33; "Oranges", 0.23; "Bananas", 0.45]
    |> dict

let bananas = inventory.["Bananas"]     // 0.45
let bananas2 = inventory["Bananas"]     // 0.45, F# 6

inventory.Add("Pineapples", 0.85)       // System.NotSupportedException
inventory.Remove("Bananas")             // System.NotSupportedException
```

### Map

```fsharp
///Map
let inventory =
    Map ["Apples", 0.33; "Oranges", 0.23; "Bananas", 0.45]

let apples = inventory.["Apples"]
let pineapples = inventory.["Pineapples"]   // KeyNotFoundException

let newInventory =              // Creates new Map
    inventory
    |> Map.add "Pineapples" 0.87
    |> Map.remove "Apples"
```

## Tuples and Records

### Tuples

```fsharp
// Tuple construction
let x = (1, "Hello")

// Triple
let y = ("one", "two", "three") 

// Tuple deconstruction / pattern
let (a', b') = x

/// Get the first and second elements
let c' = fst (1, 2)
let d' = snd (1, 2)
  
let print' tuple =
    match tuple with
    | (a, b) -> printfn "Pair %A %A" a b
```

### Records

```fsharp
// Declare a record type
type Person = { Name : string; Age : int }

// Create a value via record expression
let paul = { Name = "Paul"; Age = 28 }

// 'Copy and update' record expression
let paulsTwin = { paul with Name = "Jim" }

/// Records are immutable and have pattern matching support
let isPaul person =
    match person with
    | { Name = "Paul" } -> true
    | _ -> false
```

## Recursive Functions

```fsharp
///The `rec` keyword is used along with the `let` 
///keyword to define a recursive function:

let rec fact x =
    if x < 1 then 1
    else x * fact (x - 1)

///use `and` to call mutually recursive functions
let rec even x =
   if x = 0 then true 
   else odd (x - 1)

and odd x =
   if x = 0 then false
   else even (x - 1)
```