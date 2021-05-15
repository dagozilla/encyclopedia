# C++ Header Files

## Table of Contents
- [Background](#background)
- [Header Files](#header-files)
- [Pragma Once](#pragma-once)
- [Difference Between Using Angle Brackets and Using Quotes in An Include Statement](#difference-between-using-angle-brackets-and-using-quotes-in-an-include-statement)
- [References](#references)

## Background
Header file is a file that contains function or data type declarations which other source files will include it into their source codes. Header file is useful when we want to write the same forward declaration statements to many source codes. To understand this more, let's write some codes.

Create a main file named `main.cpp`. In `main.cpp`, we create a function named `log` that will receive `const char*` (some kind of a `string` or `array of char`) and print it to the shell.

```c++
// main.cpp

#include <iostream>

void log(const char* message) {
    std::cout << message << std::endl;
}

int main() {
    log("Program started");
    log("Program finished");
}
```
Compile the source code then run the executable file. It will works just fine.

```sh
g++ main.cpp -o main
./main
# Program started
# Program finished
```

Now let's create another source file named `foobar.cpp`. Implement an empty function called `foo` that only calls the `log` function.

```c++
// foobar.cpp

void foo() {
    log("foo function is called");
}
```

Try to compile the source codes.

```sh
g++ main.cpp foobar.cpp -o main # compilation failed
```

The source codes will not be able to be compiled because the compiler doesn't know what the `log` function is in the `foobar.cpp` source file. So, we must add a forward declaration statement in the `foobar.cpp` source file.

```c++
// foobar.cpp

void log(const char* message);

void foo() {
    log("foo function is called");
}
```

The above source codes will be compiled successfully because the compiler know what the `log` function in `foobar.cpp` source file is and know the implementation of it from the `main.cpp` source file.

But, what happens if we have many source files like `foobar.cpp` that call `log` function? We need to write the same forward declaration statement to every source files. To overcome this problem, we need a `header file`.

## Header Files

Create a header file named `log.hpp` and write a forward declaration statement for the `log` function here.

```c++
// log.hpp

void log(const char* message);
```

Edit the `foobar.cpp` to include the `log.hpp` instead of write the forward declaration statement.

```c++
// foobar.cpp

#include "log.hpp"

void foo() {
    log("foo function is called");
}
```
Eventhough we have implemented the `log` function in the `main.cpp`. We'll include the `log.hpp` to the `main.cpp` file just to show it to you that it works.

```c++
// main.cpp

#include "log.hpp"
#include <iostream>

void log(const char* message) {
    std::cout << message << std::endl;
}

int main() {
    log("Program started");
    log("Program finished");
}
```

Compile the source codes and run the executable file. It will works just fine.

```sh
g++ main.cpp foobar.cpp -o main
./main
# Program started
# Program finished
```

To make it more make sense, let's create a header file named `log.cpp` where the implementation of the log function is located.

```c++
// log.cpp

#include <iostream>

void log(const char* message) {
    std::cout mstd::cout << message << std::endl;
}
```

Create a header file named `foobar.cpp` where the forward declaration of the `foo` function is located.

```c++
// foobar.hpp

void foo();
```

Then, edit the `main.cpp` to calls the `foo` function. Remove the implementation of the `log` function in the `main.cpp` because we will use the implementation from the `log.cpp`.

```c++
// main.cpp

#include "log.hpp"
#include "foo.hpp"

int main() {
    log("Program started");
    foo();
    log("Program finished");
}
```

Compile the source codes and run the executable file. It will works just fine.

```sh
g++ main.cpp log.cpp foobar.cpp -o main
./main
# Program started
# foo function is called
# Program finished
```

## Pragma Once
Now we have this files in our current project directory.
```
-
|- log.hpp
|- log.cpp
|- foobar.hpp
|- foobar.cpp
|- main.cpp
```

```c++
// log.hpp
void log(const char* message);
```

```c++
// log.cpp

#include <iostream>

void log(const char* message) {
    std::cout mstd::cout << message << std::endl;
}
```
```c++
// foobar.hpp

void foo();
```

```c++
// foobar.cpp

#include "log.hpp"

void foo() {
    log("foo function is called");
}
```

```c++
// main.cpp

#include "log.hpp"
#include "foo.hpp"

int main() {
    log("Program started");
    foo();
    log("Program finished");
}
```

Now, let's define an empty struct named `bar` in `log.hpp`.
```c++
// log.hpp

void log(const char* message);

struct bar {};
```

Edit the `foobar.hpp` to also include the `log.hpp` for the sake of this demo.
```c++
// foobar.hpp

#include "log.hpp"

void foo();
```

The source codes will not be able to be compiled. In the `log.hpp` file we initialize the `bar` struct. The `foobar.hpp` include the `log.hpp` file. The `main.cpp` include both `log.hpp` and `foobar.hpp` files. Because the compiler preprocess the `#include` statements, the `bar` struct defined multiple times in the same translation unit and that's forbidden. This is also said that you can implement many same forward declarations in a translation unit.

```sh
g++ main.cpp log.cpp foobar.cpp -o main
# In file included from foobar.hpp:1,
#                  from main.cpp:2:
# log.hpp:3:8: error: redefinition of ‘struct bar’
#     3 | struct bar {};
#       |        ^~~
# In file included from main.cpp:1:
# log.hpp:3:8: note: previous definition of ‘struct bar’
#     3 | struct bar {};
#       |        ^~~
```

To overcome this problem, we used to define a symbol using `ifndef`, `define`, and `endif` statements in the header files. The combination of this preprocess statements tell the compiler not to add a header file content into a translation unit if a symbol already defined. Let's use this method in `log.hpp` by define a symbol named `_LOG_HPP`.

```c++
// log.hpp

#ifndef _LOG_HPP
#define _LOG_HPP

void log(const char* message);

struct bar {};

#endif  // _LOG_HPP
```

Compile the source codes and run the executable file. It will works just fine.
```sh
g++ main.cpp log.cpp foobar.cpp -o main
./main
# Program started
# foo function is called
# Program finished
```

But now there is a simpler preprocess statement called `#pragma once`. This statement tells the compiler to only include the header file only once in a translation unit. Let's use this in `log.hpp`.

```c++
// log.hpp

#pragma once

void log(const char* message);

struct bar {};
```

Compile the source codes and run the executable file. It will works just fine.

## Difference Between Using Angle Brackets and Using Quotes in An Include Statement
- `#include "header_file"` search the header file both relative to the current file where the statement is stated and in the compiler includes directories.
- `#include <header_file>` search the header file only in the compiler includes directories.

## References
1. ["C++ Header Files"](https://youtu.be/9RJTQmK0YPI). *The Cherno*. Retrieved 12 May 2021.
