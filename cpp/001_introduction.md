# Introduction to C++

## Table of Contents
- [Preface](#preface)
- [Programming Language Properties](#programming-language-properties)
- [The Features of (Modern) C++ as a Language](#the-features-of-modern-c++-as-a-language)
- [A Brief History of C++](#a-brief-history-of-c++)
- [References](#references)

## Preface
- Computers are capable to automate many processes that would be tedious or boring to perform otherwise.
- However, computers are not as "intelligent" as we are.
  - They have to be told in no uncertain terms about what they're supposed to do.
  - Their native languages are quite unlike anything we speak.
- Thus, in order to better communicate to our computers what exactly it is we want them to do, many **programming languages** developed to make the communication process easier.

## Programming Language Properties

### Compiled, Interpreted, or JIT-compiled
- **Compiled languages**
  - The codes are translated to the target machine's native language by a program called a **compiler**.
  - This can result in a very fast program
  - However, the compiled programs may not port well across operating systems and the compilation process may take a while.
- **Interpereted languages**
  - The codes are read by a program called **interpreter** and are executed by it.
  - They're  usually portable and have no long compile times but usually run slower than the compiled one.
- **JIT-compiled (just-in-time compiled) languages**
  - The codes quickly compiled when programs in them need to be run (usually with very little optimization).

### High or Low Level
It refers to how similar the language is to a computer's native language. The higher the level, the *less* similar it is.
- **Low-level Language**
  - Generally, the term is reserved for machine code itself and assembly languages, though many languages offer low-level elements.
- **High-level language**
  - It usually is easier to understand than a low-level language, and it usually takes less time to develop a program in a high-level language than it does in a low-level language.

### Type System
A **type system** refers to the rules that the different types of variables of a language have to follow. There are some typing characteristics but they're not necessarily mutually exclusive, and some languages mix them.

#### Type Strength: Strong or Weak
- **Strong typing system**: Puts restrictions on how different types of variables can be converted to each other without any converting statements.
  - An ideal strong typing system would forbid implicit "casts" to types that do not make any sense, such as an integer to a Fruit object.
- **Weak typing system**: Try to find some way to make the cast work.

#### Type Expression: Manifest or Inferred
- **Manifest typing**: Require variables' types to be explicitly defined.
- **Inferred typing**: Will infer the type of the variable based on the contexts in which it is used.

#### Type Checking: Static or Dynamic
- **Statically typed**: The compiler/interpreter does the type checking once before the program runs/is compiled.
- **Dynamically typed**: The types are checked at run-time.

#### Type Safety: Safe or Unsafe
- **Safe language**: Will do more to ensure that operations on typed variables that might lead to undefined behavior or errors do not occur.
- **Unsafe language**: Will give more responsibility to the users to check their code behaviours.

### Supported Paradigms
A programming paradigm is a methodology or way of programming that a programming language supports. Below are some of the paradigms:
- Declarative
- Functional
- Generic
- Imperative
- Structured
- Procedural
- Object-oriented

### Standardization
- This can be very important to ensure that programs written to work with one compiler/interpreter will work with another.
- Some languages standardized by an organization.
  - ANSI (American National Standards Institute)
  - ISO (International Organization for Standardization)
- Some languages have an informal but de-facto standard not maintained by any standards organization.

## The Features of (Modern) C++ as a Language
- **C++ is an open ISO-standardized language.**
  - Since 1998, C++ is standardized by a committee of the ISO.
- **C++ is a compiled language.**
  - C++ compiles directly to a machine's native code.
- **C++ is a strongly-typed unsafe language.**
  - C++ is a language that expects the programmer to know what he or she is doing, but allows for incredible amounts of control as a result.
- **C++ supports both manifest and inferred typing.**
  - As of the latest C++ standard, C++ supports both manifest and inferred typing, allowing flexibility and a means of avoiding verbosity where desired.
- **C++ supports both static and dynamic type checking.**
  - C++ allows type conversions to be checked either at compile-time or at run-time, again offering another degree of flexibility.
  - Most C++ type checking is, however, static.
- **C++ offers many paradigm choices.**
  - C++ offers remarkable support for procedural, generic, and object-oriented programming paradigms, with many other paradigms being possible as well.
- **C++ is *portable*.**
  - If your C++ code exclusively uses C++'s standard library, it will run on many platforms with few to no changes. This possible because many C++ compilers run on many different platforms.
- **C++ is upwards compatible with C.**
  - C++ can use C libraries with few to no modifications of the libraries' code.
- **C++ has incredible library support.**
  - Since the language is widely used for a long time, it has many libraries made by many communities.s

## A Brief History of C++
- Initially developed by **Bjarne Stroustrup** in 1979 for his Ph.D thesis.
- His goal was to add object-oriented programming into the C language (C with Classes).
- In 1983, the name of the language was changed from C with Classes to C++.
- In 1985, Stroustrup's reference to the language entitled *The C++ Programming Language* was published. The language was not officially standardized yet, making the book a very important reference.
- In 1998, the C++ standards committee published the first international standard which would be informally known as C++98. The Standard Template Library, which began its conceptual development in 1979, was also included.
- In mid-2011, the new C++ standard was finished. The Modern C++ era began since this standard release.

## References
1. ["A Brief Description"](https://www.cplusplus.com/info/description/). *cplusplus.com*. Retrieved 8 May 2021.
2. ["History of C++"](https://www.cplusplus.com/info/history/). *cplusplus.com*. Retrieved 8 May 2021.
