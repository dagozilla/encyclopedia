# References in C++

## Definition
> A **reference** is an alias of an existing variable.

## Demo
A reference act as an alias of an existing variable. To initialized a reference, add the `&` symbol after the reference's variable type and assigned it with an existing variable. It doesn't allocate memory. The way to access a reference is the same as a normal variable, without additional operator.

```c++
// main.cpp

#include <iostream>

#define LOG(x) std::cout << x << std::endl

int main() {
    int foo = 9;
    int& ref = foo;
    
    LOG(foo);   // the value of foo
    LOG(&foo);  // the memory address of foo

    LOG(ref);   // the value of ref, the same as foo's
    LOG(&ref);  // the memory address of ref, the same as foo's

    ref = 10;
    LOG(ref);   // the value changed
    LOG(foo);   // the value also changed because ref act as an alias for foo
}
```

But, you can't create an empty reference. A reference always has to be initialized with an existing variable.

```c++
// main.cpp

#include <iostream>

#define LOG(x) std::cout << x << std::endl

int main() {
    int& ref;   // compile error
}
```

A reference also can't change the variable it refer to.

```c++
// main.cpp

#include <iostream>

#define LOG(x) std::cout << x << std::endl

int main() {
    int foo = 9;
    int bar = 10;
    int& ref = foo;

    LOG(ref);   // 9
    LOG(foo);   // 9
    LOG(bar);   // 10

    ref = bar;  // Here we change the value of foo, not the variable the ref refer

    LOG(ref);   // 10
    LOG(foo);   // 10
    LOG(bar);   // 10
}
```

References can be used as parameters of a function (**pass-by-reference**) besides using pointers (**pass-by-pointer**). In order to be able to modify parameters in a function and keep the changes outside the scope of the function, we define the parameters of the function to be passed by pointer or passed by reference instead of just pass it by value.

```c++
// main.cpp

#include <iostream>

#define LOG(x) std::cout << x << std::endl

void incPassByValue(int val) {
    val++;
}

void incPassByPointer(int* ptr) {
    (*ptr)++;
}

void incPassByReference(int& ref) {
    ref++;
}

int main() {
    int foo = 9;
    LOG(foo);   // 9

    incPassByValue(foo);
    LOG(foo);   // stil 9, since we pass it by value

    incPassByPointer(&foo);
    LOG(foo);   // 10

    incPassByReference(foo);
    LOG(foo);   // 11
}
```

## References
1. ["REFERENCES in C++"](https://youtu.be/IzoFn3dfsPA). *The Cherno*. Retrieved 15 May 2021.
