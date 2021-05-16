# How C++ Works?

## Table of Contents
- [Preface](#preface)
- [The Build Pipeline](#the-build-pipeline)
- [Preprocessing](#preprocessing)
- [Compiling](#compiling)
- [Linking](#linking)
- [References](#references)

## Preface
- This article will explain how the C++ works from the source code files into an executable binary file.
- Basically, your source codes will be passed to the compiler which will be compiled to a binary. That binary can be some sort of library or the actual executable program.
- This article will be focused on the executable binary compilation.

## The Build Pipeline
```
Preprocessing -> Compiling -> Linking
```
- **Preprocessing**: Preprocess the `source codes` just before the actual compilation started to become the `translation units`.
- **Compiling**: Compile the `translation units` to become the `object files`.
- **Linking**: Link the `object files` to become an `executable binary file`.

## Preprocessing
In preprocessing, the `source codes` will be translated into `translation units` that will be compiled later. Let's write some codes to understand how the preprocessing works.

Create a new file named `math.hpp` (we'll talk more about the header files later) and implement the addition math function in it.

```c++
// math.hpp

int add(int a, int b) {
    return a + b;
}
```

Then, create a new file named `main.cpp` and use the `add` function in the `main` function. The `main` function is a special function as an entry point where the program will be started. The compiler will assumed the function will return zero if not specified.

```c++
// main.cpp

int main() {
    int result = add(1, 2);
}
```

If you compile it, it will be failed because the compiler doesn't know what the `add` function is. 

```sh
g++ main.cpp -o main
# main.cpp: In function ‘int main()’:
# main.cpp:2:18: error: ‘add’ was not declared in this scope
#     2 |     int result = add(1, 2);
#       |                  ^~~
```

To make it works, let's include the `math.hpp` into the `main.cpp` so that the compiler will know what the `add` function is.

```c++
// main.cpp

#include "math.hpp"

int main() {
    int result = add(1, 2);
}
```

It will be compiled successfully. The `-o` option is there to specify the output file name.

```sh
g++ main.cpp -o main
./main # no output since we don't print anything yet in the codes but the program exited successfully
```
The `#include` statement that written before is called a **preprocess statement**. The compiler will create a translation unit, paste the `main.cpp` content in it, then do the preprocessing (every statements that start with `#`). The `#include` statement is one of the preprocess statement that will paste all the given file content to the current file. In this case, because the `#include "math.hpp"` statement exists, it will paste the `math.hpp` content to the translation unit where the statement is located.

To see how it works, let's generate the translation unit with `-E` option to output an translation unit instead of an executable binary file and save the output to a file named `main.ii` with `-o` option.

```sh
g++ -E main.cpp -o main.ii
```

The translation unit file will looks like this. The compiler literally copy the `math.hpp` and `main.cpp` content and paste it into the translation unit in order.

```c++
// math.ii

# 1 "main.cpp"
# 1 "<built-in>"
# 1 "<command-line>"
# 1 "/usr/include/stdc-predef.h" 1 3 4
# 1 "<command-line>" 2
# 1 "main.cpp"
# 1 "math.hpp" 1
int add(int a, int b) {
    return a + b;
}
# 2 "main.cpp" 2

int main() {
    int result = add(1, 2);
}
```

## Compiling
In compiling, the `translation units` will be compiled to become `object files` that will be linked later. Let's write some codes to understand how the compilation works.

Rewrite our `main.cpp` to be like this. This time, we use `std::cout` from `iostream` library to print the result of `add(1, 2)` then print a new line (`std::endl`) to the console. Remove the `#include "math.hpp"` statement to simulate the compile error. Also, add `int add(int a, int b);` to the file.

```c++
// main.cpp

#include <iostream>

int add(int a, int b);

int main() {
    std::cout << add(1, 2) << std::endl;
}
```

If we compile the above `main.cpp` to an executable binary file, it will be failed because even though the compiler know the `add` function exists, the compiler doesn't know the implementation of the `add` function. But if we generate only the object files, it will be compiled successfully.

To demonstrate it, let's generate the object file with `-c` option to output an object file instead of an executable binary file and save the output to a file named `main.o` with `-o` option. As you can see, the `main.o` file generated successfully without any error.

```sh
g++ -c main.cpp -o main.o # the main.o file generated successfully
```

The `int add(int a, int b);` line is called the **forward declaration**. The forward declaration tells the compiler that the specified symbol or function exists. The compiler will believes then compiles it to an object file. This object file then will be linked to the other object file at the linking stage where the implementation of the function exists, generate an executable binary file.

## Linking
In linking, the `object files` will be linked, generate an `executable binary file`. Let's write some codes to understand how the linking works.

To make it works and clean, let's create a header file that contains the forward declaration and a source file that contains the implementation/definition.

```c++
// math.hpp

int add(int a, int b);
```

```c++
// math.cpp

int add(int a, int b) {
    return a + b;
}
```

Then, remove the previous written forward declaration in `main.cpp` and include the header file (`math.hpp`).

```c++
// main.cpp

#include <iostream>
#include "math.hpp"

int main() {
    std::cout << add(1, 2) << std::endl;
}
```

Generate the object files for `math.cpp` and `main.cpp`. Then, linked it.
```sh
g++ -c math.cpp -o math.o
g++ -c main.cpp -o main.o
g++ main.o math.o -o main
```

If you execute it, it will print `3` to the console.
```sh
./main
# 3
```

## References
1. ["How C++ Works: Understanding Compilation"](https://www.toptal.com/c-plus-plus/c-plus-plus-understanding-compilation). *Toptal*. Retrieved 12 May 2021.
2. ["How C++ Works"](https://youtu.be/SfGuIVzE_Os). *The Cherno*. Retrieved 12 May 2021.
3. ["How the C++ Compiler Works"](https://youtu.be/3tIqpEmWMLI). *The Cherno*. Retrieved 12 May 2021.
4. ["How the C++ Linker Works"](https://youtu.be/H4s55GgAg0I). *The Cherno*. Retrieved 12 May 2021.
