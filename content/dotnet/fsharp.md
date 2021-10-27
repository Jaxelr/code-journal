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

