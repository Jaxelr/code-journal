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

## Discriminated Unions

```fsharp
type Tree<'T> =
    | Node of Tree<'T> * 'T * Tree<'T>
    | Leaf


let rec depth input =
    match input with
    | Node(l, _, r) -> 1 + max (depth l) (depth r)
    | Leaf -> 0

///Option<T>
let optionPatternMatch input =
    match input with
    | Some i -> printfn "input is an int=%d" i
    | None -> printfn "input is missing"

///Single case dus are type safe abstractions 
///that support pattern matching
type OrderId = Order of string

// Create a DU value
let orderId = Order "12"

// Use pattern matching to deconstruct single-case DU
let (Order id) = orderId
```

## Exceptions

```fsharp
let divideFailwith x y =
    if y = 0 then 
        failwith "Divisor cannot be zero."  ///Throws type `Exception`
        else x / y 

///try/with
let divide x y =
    try
        Some (x / y)
    with :? System.DivideByZeroException -> 
        printfn "Division by zero!"
        None

///try/with/finally
exception InnerError of string
exception OuterError of string
  
let handleErrors x y =
   try 
       try 
           if x = y then raise (InnerError("inner"))
           else raise (OuterError("outer"))
       with InnerError(str) -> 
          printfn "Error1 %s" str
   finally
       printfn "Always print this."
```

## Classes and Interfaces

```fsharp
///Defining a class
type Vector(x: float, y: float) =
    let mag = sqrt(x * x + y * y)               // (1) - local let binding

    member this.X = x                           // (2) property
    member this.Y = y                           // (2) property
    member this.Mag = mag                       // (2) property

    member this.Scale(s) =                       // (3) method
        Vector(x * s, y * s)

    static member (+) (a : Vector, b : Vector) = // (4) static method
        Vector(a.X + b.X, a.Y + b.Y)

///Calling a base class from a derived one
type Animal() =
    member _.Rest() = ()
           
type Dog() =
    inherit Animal()
    member _.Run() =
        base.Rest()

///Defining an interface and implementation
type IVector =
    abstract Scale : float -> IVector

type Vector(x, y) =
    interface IVector with
        member __.Scale(s) =
            Vector(x * s, y * s) :> IVector
            
    member __.X = x
    
    member __.Y = y

///Another alternative using object expressions
type ICustomer =
    abstract Name : string
    abstract Age : int

let createCustomer name age =
    { new ICustomer with
        member __.Name = name
        member __.Age = age }
```

## Active Patterns

```fsharp
///Complete active pattern
let (|Even|Odd|) i = 
  if i % 2 = 0 then Even else Odd

let testNumber i =
    match i with
    | Even -> printfn "%d is even" i
    | Odd -> printfn "%d is odd" i

///Parameterized, partial active pattern
let (|DivisibleBy|_|) divisor n = 
  if n % divisor = 0 then Some DivisibleBy else None

let fizzBuzz input =
    match input with
    | DivisibleBy 3 & DivisibleBy 5 -> "FizzBuzz" 
    | DivisibleBy 3 -> "Fizz" 
    | DivisibleBy 5 -> "Buzz" 
    | i -> string i
```

## Functions

Useful functions for daily usage

### Mapping Functions

```fsharp
///Map - shape items from one collection into another collection
// [2; 4; 6; 8; 10; 12; 14; 16; 18; 20]
[1 .. 10] |> List.map (fun n -> n * 2)

type Person = { Name : string; Town : string }

let persons =
    [
        { Name = "Isaak"; Town = "London" }
        { Name = "Sara"; Town = "Birmingham" }
        { Name = "Tim"; Town = "London" }
        { Name = "Michelle"; Town = "Manchester" }
    ]

// ["London"; "Birmingham"; "London"; "Manchester"]
persons |> List.map (fun person -> person.Town)

///Map2, Map3 - Map for multiple lists
let list1 = [1; 2; 3]
let list2 = [4; 5; 6]
let list3 = [7; 8; 9]

// [5; 7; 9]
(list1, list2) ||> List.map2 (fun x y -> x + y)

// [12; 15; 18]
(list1, list2, list3) |||> List.map3 (fun x y z -> x + y + z) 

///Mapi - Map and include the index
let list1 = [9; 12; 53; 24; 35]

// [(0, 9); (1, 12); (2, 53); (3, 24); (4, 35)]
list1 |> List.mapi (fun x i -> (x, i))

// [9; 13; 55; 27; 39]
list1 |> List.mapi (fun x i -> x + i)

let list1 = [9; 12; 3]
let list2 = [24; 5; 2]

// [0; 17; 10]
(list1, list2) ||> List.mapi2 (fun i x y -> (x + y) * i) 
```

```fsharp
///indexed - return the collection along with the index position of each element
let list1 = [23; 5; 12]

// [(0, 23); (1, 5); (2, 12)]
let result = list1 |> Array.indexed
```

```fsharp
///iter - apply a unit returning function over each element
let list1 = [1; 2; 3]
let list2 = [4; 5; 6]

// Prints: 1; 2; 3; 
list1 |> List.iter (fun x -> printf "%d; " x)

// Prints: (1 4); (2 5); (3 6);
(list1, list2) ||> List.iter2 (fun x y -> printf "(%d %d); " x y)

// Prints: ([0] = 1); ([1] = 2); ([2] = 3);
list1 |> List.iteri (fun i x -> printf "([%d] = %d); " i x)

// Prints: ([0] = 1 4); ([1] = 2 5); ([2] = 3 6);
(list1, list2) ||> List.iteri2 (fun i x y -> printf "([%d] = %d %d); " i x y) 
```

```fsharp 
///collect - apply a function to each element then collect them into a new collection

// [0; 1; 0; 1; 2; 3; 4; 5; 0; 1; 2; 3; 4; 5; 6; 7; 8; 9; 10]
let list1 = [1; 5; 10]
let list2 = [1; 2; 3]

list1 |> List.collect (fun elem -> [0 .. elem])

// [1; 2; 3; 2; 4; 6; 3; 6; 9]
list2 |> List.collect (fun x -> [for i in 1..3 -> x * i])

// Example 3
type Customer =
    {
        Id: int
        OrderId: int list
    }

let c1 = { Id = 1; OrderId = [1; 2]}
let c2 = { Id = 2; OrderId = [43]}
let c3 = { Id = 5; OrderId = [39; 56]}
let customers = [c1; c2; c3]

// [1; 2; 43; 39; 56]
let orders = customers |> List.collect(fun c -> c.OrderId)
```

```fsharp
///pairwise - returns a new list of tuples of adjacent items
let list1 = [1; 30; 12; 20]

//  [(1, 30); (30, 12); (12, 20)]
list1 |> List.pairwise

// [31.0; 11.0; 21.0]
[ DateTime(2010,5,1)
  DateTime(2010,6,1)
  DateTime(2010,6,12)
  DateTime(2010,7,3) ]
|> List.pairwise
|> List.map(fun (a, b) -> b - a)
|> List.map(fun time -> time.TotalDays)
```

```fsharp
///windowed - returns a list of sliding windows from the input list
// [['a'; 'b'; 'c']; ['b'; 'c'; 'd']; ['c'; 'd'; 'e']]
['a'..'e'] |> List.windowed 3
```

### Grouping Functions

```fsharp
///groupby - the output is a collection of tuples
type Person =
    {
        Name: string
        Town: string
    }

let persons =
    [ { Name = "Isaak"; Town = "London" }
      { Name = "Sara"; Town = "Birnmingham" }
      { Name = "Tim"; Town = "London" }
      { Name = "Michelle"; Town = "Manchester" } ]

// [("London", [{ Name = "Isaak"; Town = "London" }; { Name = "Tim"; Town = "London" }]);
//  ("Birnmingham", [{ Name = "Sara"; Town = "Birnmingham" }]);
//  ("Manchester", [{ Name = "Michelle"; Town = "Manchester" }])]
persons |> List.groupBy (fun person -> person.Town)
```

```fsharp
///countby - the output is a tuple with the field + the number of items on the collection
type Person = { Name: string; Town: string }

let persons =
    [
        { Name = "Isaak"; Town = "London" }
        { Name = "Sara"; Town = "Birnmingham" }
        { Name = "Tim"; Town = "London" }
        { Name = "Michelle"; Town = "Manchester" }
    ]

// [("London", 2); ("Birnmingham", 1); ("Manchester", 1)]
persons |> List.countBy (fun person -> person.Town)
```

```fsharp
///partition - using the predicate return 2 lists
// Tupled result in two lists
let londonPersons, otherPersons =
    persons |> List.partition(fun p -> p.Town = "London")
```

```fsharp
///chunkBySize - group elements into chunks of n size
let list1 = [33; 5; 16]

// int list list = [[33; 5]; [16]]
let chunkedLst = list1 |> List.chunkBySize 2
```

```fsharp
///splitAt - split the collection into 2 parts on the index indicated

let xs = [| 1; 2; 3; 4; 5 |]

let left1, right1 = xs |> Array.splitAt 0   // [||] and [|1; 2; 3; 4; 5|]
let left2, right2 = xs |> Array.splitAt 1   // [|1|] and [|2; 3; 4; 5|]
let left3, right3 = xs |> Array.splitAt 5   // [|1; 2; 3; 4; 5|] and [||]
let left4, right4 = xs |> Array.splitAt 6   // InvalidOperationException
```

```fsharp
///splitInto - splits the collection into n of chunks
// [[1; 2; 3; 4]; [5; 6; 7]; [8; 9; 10]]
// note that the first chunk has four elements
[1..10] |> List.splitInto 3

// [[1; 2; 3]; [4; 5; 6]; [7; 8]; [9; 10]]
[1..10] |> List.splitInto 4

// [[1; 2]; [3; 4]; [5; 6]; [7; 8]; [9]; [10]]
[1..10] |> List.splitInto 6
```

### Aggregate Functions

```fsharp
let numbers = [1.0 .. 10.0]

let total = numbers |> List.sum         // 55.0
let average = numbers |> List.average   // 5.5
let max = numbers |> List.max           // 10.0
let min = numbers |> List.min           // 1.0
```

### Other Functions

```fsharp
///Find - finds the first element that matches a condition
let isDivisibleBy number elem = elem % number = 0

let input = [1 .. 10]

input |> List.find (isDivisibleBy 5)    // 5
input |> List.find (isDivisibleBy 11)   // KeyNotFoundException
```

```fsharp
/// findBack - finds the last element that matches a condition
let isDivisibleBy number elem = elem % number = 0

let input = [1 .. 10]

input |> List.findBack (isDivisibleBy 4)    // 8
input |> List.findBack (isDivisibleBy 11)   // KeyNotFoundException
```

```fsharp
///findIndex - finds the first index that matches a condition
let isDivisibleBy number elem = elem % number = 0

let input = [1 .. 10]

input |> List.findIndex (isDivisibleBy 5)   // 4
input |> List.findIndex (isDivisibleBy 11)  // KeyNotFoundException
```

```fsharp
let isDivisibleBy number elem = elem % number = 0

let input = [1..10]

input |> List.findIndexBack (isDivisibleBy 3)   // 8
input |> List.findIndexBack (isDivisibleBy 11)  // KeyNotFoundException
```

```fsharp
/// returns the first (head), last (last) and all but first item (tail) functions
let input = [15..22]

input |> List.head    // 15
input |> List.last    // 22
input |> List.tail    // [16; 17; 18; 19; 20; 21; 22]
```

```fsharp
///item - gets the element at a given index
let input = [1..7]

input |> List.item 5      // 6
input |> List.item 8      // ArgumentException
```

```fsharp
///take - returns the elements up to the specified count
let input = [1..10]

input |> List.take 5        // [1; 2; 3; 4; 5]
input |> List.take 11       // InvalidOperationException
```

```fsharp
///truncate - returns at most N elements
let input = [1..10]

input |> List.truncate 5    // [1; 2; 3; 4; 5]
input |> List.truncate 11   // [1; 2; 3; 4; 5; 6; 7; 8; 9; 10]
```

```fsharp
///takeWhile - give me items until the criteria isnt met
let input = [1..10]

input |> List.takeWhile (fun x -> x / 7 = 0)   // [1; 2; 3; 4; 5; 6]
input |> List.takeWhile (fun x -> x / 17 = 0)     // [1; 2; 3; 4; 5; 6; 7; 8; 9; 10]
```

```fsharp
///skipWhile - skips elements until the predicate is true
let mySeq = seq { for i in 1 .. 10 -> i * i }    // 1 4 9 16 25 36 49 64 81 100

mySeq |> Seq.skipWhile (fun elem -> elem < 10)   // 16 25 36 49 64 81 100
mySeq |> Seq.skipWhile (fun elem -> elem < 101)  // Empty seq
```

```fsharp
///exists - tests if any element satisfies a predicate
let inputs = [0..3]

inputs |> List.exists (fun elem -> elem = 3)      // true
inputs |> List.exists (fun elem -> elem = 10)     // false
```

```fsharp
///exists2 - tests the pair of elements of each list to satisfy the predicate
/// The collections must have equal lengths, except for Seq where extra elements are ignored.
let list1to5 = [1 .. 5]           // [1; 2; 3; 4; 5]
let list0to4 = [0 .. 4]           // [0; 1; 2; 3; 4]
let list5to1 = [5 .. -1 .. 1]     // [5; 4; 3; 2; 1]
let list6to1 = [6 .. -1 .. 1]     // [6; 5; 4; 3; 2; 1]

(list1to5, list5to1) ||> List.exists2 (fun i1 i2 -> i1 = i2)    // true
(list1to5, list0to4) ||> List.exists2 (fun i1 i2 -> i1 = i2)    // false
(list1to5, list6to1) ||> List.exists2 (fun i1 i2 -> i1 = i2)    // ArgumentException
```

```fsharp
///forall - tests all elements on the predicate
let inputs = [2; 4; 6; 8; 10]

inputs |> List.forall (fun i -> i % 2 = 0)    // true
inputs |> List.forall (fun i -> i % 2 = 0)    // false
```
```fsharp
///forall2 - tests the elements of the predicate pairwise 
let lst1 = [0; 1; 2]
let lst2 = [0; 1; 2]
let lst3 = [2; 1; 0]
let lst4 = [0; 1; 2; 3]

(lst1, lst2) ||> List.forall2 (fun i1 i2 -> i1 = i2)    // true
(lst1, lst3) ||> List.forall2 (fun i1 i2 -> i1 = i2)    // false
(lst1, lst4) ||> List.forall2 (fun i1 i2 -> i1 = i2)    // ArgumentException
```

```fsharp
///contains - returns true if a collection contains the item
let rushSet = ["Dirk"; "Lerxst"; "Pratt"]
let gotSet = rushSet |> List.contains "Lerxst"      // true
```

```fsharp
///filter, where - returns a new collection with the elements satisfied by the predicate
let data =
    [("Cats",4)
     ("Tiger",5)
     ("Mice",3)
     ("Elephants",2) ]

// [("Cats", 4); ("Mice", 3)]
data |> List.filter (fun (nm, x) -> nm.Length <= 4)
data |> List.where (fun (nm, x) -> nm.Length <= 4)
```

```fsharp
///length - length of the collection
[ 1 .. 100 ] |> List.length         // 100
[ ] |> List.length                  // 0
[ 1 .. 2 .. 100 ] |> List.length    // 50
```

```fsharp
///distinctBy - using the keys returned by the projection returns no duplicate entries
let inputs = [-5 .. 10]

// [-5; -4; -3; -2; -1; 0; 6; 7; 8; 9; 10]
inputs  |> List.distinctBy (fun i -> abs i)
```

```fsharp
///distinct - returns a collection that contains no dupes acording to equality comparisons
[1; 3; 9; 4; 3; 1] |> List.distinct    // [1; 3; 9; 4]
[1; 1; 1; 1; 1; 1] |> List.distinct     // [1]
[ ] |> List.distinct                    // error FS0030: Value restriction
```

```fsharp
///sortBy - sorts using keys given by the projection
[1; 4; 8; -2; 5] |> List.sortBy (fun x -> abs x)    // [1; -2; 4; 5; 8]
```

```fsharp
///sort - using Operators.compare
[1; 4; 8; -2; 5] |> List.sort    // [-2; 1; 4; 5; 8] 
```

```fsharp
///sortByDescending - sorts descending using keys given by the projection
[-3..3] |> List.sortByDescending (fun x -> abs x)   // [-3; 3; -2; 2; -1; 1; 0]
```

```fsharp
///sortDescending - self explanatory
[0..5] |> List.sortDescending    // [5; 4; 3; 2; 1; 0]
```

```fsharp
///sortWith - sorts using the function provider as predicate
let lst = ["<>"; "&"; "&&"; "&&&"; "<"; ">"; "|"; "||"; "|||"]

let sortFunction (str1: string) (str2: string) =
    if (str1.Length > str2.Length) then
        1
    else
        -1

// ["|"; ">"; "<"; "&"; "||"; "&&"; "<>"; "|||"; "&&&"]
lst |> List.sortWith sortFunction
```

```fsharp
///allPairs - takes 2 collections and returns all possible pair of elements
let arr1 = [| 0; 1 |]
let arr2 = [| 4; 5 |]

(arr1, arr2) ||> Array.allPairs arr1 arr2    // [|(0, 4); (0, 5); (1, 4); (1, 5)|]
```

```fsharp
///append - combine 2 collections into 1
let list1 = [33; 5; 16]
let list2 = [42; 23; 18]

List.append list1 list2     // [33; 5; 16; 42; 23; 18]
```

```fsharp
///averageBy - takes a func and uses it to calculate an average
// val avg1 : float = 2.0
[1..3] |> List.averageBy (fun elem -> float elem)

// val avg2 : float = 4.666666667
[| 1..3 |] |> Array.averageBy (fun elem -> float (elem * elem))
```

```fsharp
///choose - select and transform elements at the same time
let list1 = [33; 5; 16]

// [34; 6; 17]
list1 |> List.choose (fun elem -> Some(elem + 1))
```

```fsharp
///compareWith - compare 2 collections and stops when it encounters the first unequal pair
let sq1 = seq { 1; 2; 4; 5; 7 }
let sq2 = seq { 1; 2; 3; 5; 8 }
let sq3 = seq { 1; 3; 3; 5; 2 }

let compareSeq seq1 seq2 =
    (seq1, seq2 ||> Seq.compareWith (fun e1 e2 ->
        if e1 > e2 then 1
        elif e1 < e2 then -1
        else 0)

let compareResult1 = compareSeq sq1 sq2     // int = 1
let compareResult2 = compareSeq sq2 sq3     // int = -1
```

```fsharp
///concat - join n number of collections
// int list = [1; 2; 3; 4; 5; 6; 7; 8; 9]
List.concat [[1; 2; 3]; [4; 5; 6]; [7; 8; 9]]
```

```fsharp
///Array.copy - creates new array that contains the elements of an existing array
/// The copy is a shallow copy, elements using reference, only the reference is copied.
let firstArray : StringBuilder array = Array.init 3 (fun index -> new StringBuilder(""))
let secondArray = Array.copy firstArray
// Two arrays: [|; ; |]

firstArray.[0] <- new StringBuilder("Test1")
// firstArray: [|Test1; ; |]
// secondArray: [|; ; |]

firstArray.[1].Insert(0, "Test2") |> ignore
// firstArray: [|Test1; Test2; |]
// secondArray: [|; Test2; |]
```