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