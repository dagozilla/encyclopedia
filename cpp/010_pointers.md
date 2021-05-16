# Pointers in C++

## Table of Contents
- [The Importance of Memory in Programming](#the-importance-of-memory-in-programming)
- [Definition](#definition)
- [Null Pointer](#null-pointer)
- [Pointer Manipulation](#pointer-manipulation)
- [Pointer of Pointer](#pointer-of-pointer)
- [Dynamic Memory Allocation](#dynamic-memory-allocation)
- [References](#references)

## The Importance of Memory in Programming
- When you launch an application, that entire application will be loaded into memory. All of the instructions in the code that you've written also will be loaded into memory.
- That's how the CPU can access your program and start executing it's instructions.
- **Pointers** are important to managing and manipulating that memories.

## Definition
> A **Pointer** is a number which represents a memory address.

## Null Pointer
Let's create a source code named `main.cpp` and paste this codes in it.

```c++
// main.cpp

#include <iostream>

#define LOG(x) std::cout << x << std::endl

int main() {
    // void* ptr = nullptr;
    void* ptr = 0;
    LOG(ptr);  // 0x0
}
```

Here, we initialized a pointer of void (a pure pointer) named `ptr` with a memory address `0`. The `0` itself is not a valid memory address but a pointer with invalid memory address is acceptable. This `0` value can be changed to `nullptr` in C++. The `ptr` variable will initialize a random number (not a null pointer) if not specified.

```c++
// main.cpp

#include <iostream>

#define LOG(x) std::cout << x << std::endl

int main() {
    void* ptr;
    LOG(ptr); // 0x7ffee89765d8 (a random number)
    LOG((ptr == nullptr)); // 0, means it's false
}
```

## Pointer Manipulation
Now, create an integer variable named `foo` with a value of `9` then store the `foo` memory address to `ptr`.

```c++
// main.cpp

#include <iostream>

#define LOG(x) std::cout << x << std::endl

int main() {
    int foo = 9;
    void* ptr = &foo;
    LOG(&foo); // 0x7ffee29fa5bc
    LOG(ptr);  // 0x7ffee29fa5bc (the foo memory address)
}
```

The `&` symbol (**address-of operator**) is used to retrieve a variable memory address. As you can see, `ptr` stores the memory address of `foo`.

Now, let's say we know the memory address of a variable. To access the value of the variable from a pointer, put an  `*` symbol at the front of the pointer variable. This operation is called **indirection** or **dereferencing**.

```c++
// main.cpp

#include <iostream>

#define LOG(x) std::cout << x << std::endl

int main() {
    int foo = 9;
    void* ptr = &foo;
    LOG(*ptr);  // compile error
}
```

The code above will not be able to be compiled. Although it is possible to store a memory address of any variable type in a pointer of void (`void *`), it is forbidden to do indirection on operand of type `void *`. The compiler doesn't know which variable type the pointer points to. The compiler must know the size and the type of a variable (4 bytes? 8 bytes? int? long?) to be able to process it correctly. To fix this, change the pointer type to `int`, the same type as the variable type the pointer points to. It will be compiled and run successfully.

```c++
// main.cpp

#include <iostream>

#define LOG(x) std::cout << x << std::endl

int main() {
    int foo = 9;
    int* ptr = &foo;
    LOG(*ptr);  // 9
}
```

You can change the value of the variable a pointer points to by dereferencing it. As you can see from the code below, the `foo` value changed by dereferencing the `ptr`.

```c++
// main.cpp

#include <iostream>

#define LOG(x) std::cout << x << std::endl

int main() {
    int foo = 9;
    int* ptr = &foo;

    LOG(foo);   // 9
    LOG(*ptr);  // 9

    *ptr = 10;

    LOG(foo);   // 10
    LOG(*ptr);  // 10
}
```

It is possible to cast a pointer to a different pointer type but be careful about the difference of the variable type and size. The code below shows a pointer of integer (`int*`) points to a `long` variable which stores `MAX_INT + 2`. It prints different values because `foo` stores a value that exceed `int` maximum capacity. This phenomenon is called `integer overflow`.

```c++
// main.cpp

#include <iostream>

#define LOG(x) std::cout << x << std::endl

int main() {
    long foo = 2147483649;  // MAX_INT + 2
    int* ptr = (int*) &foo;

    LOG(sizeof(long));  // 8 bytes
    LOG(sizeof(int));   // 4 bytes

    LOG(foo);   // 2147483649
    LOG(*ptr);  // -2147483647
}
```

## Pointer of Pointer
The pointer itself is also a variable, which means it also has a memory address. So, you can create a pointer that points to another pointer.

```c++
// main.cpp

#include <iostream>

#define LOG(x) std::cout << x << std::endl

int main() {
    int foo = 8;
    int* ptr1 = &foo;
    int** ptr2 = &ptr1;
    int*** ptr3 = &ptr2;

    LOG(foo);   // value of foo
    LOG(&foo);  // memory address of foo

    LOG(ptr1);  // memory address of foo (value of ptr1)
    LOG(&ptr1); // memory address of ptr1

    LOG(ptr2);  // memory address of ptr1 (value of ptr2)
    LOG(&ptr2); // memory address of ptr2

    LOG(ptr3);  // memory address of ptr2 (value of ptr3)
    LOG(&ptr3); // memory address of ptr3
}
```

## Dynamic Memory Allocation
To allocate a variable to the heap, use `new` operator. To deallocate it, use `delete` operator. **Always `delete` the variables that allocated with `new`**. We won't discuss about stack and heap memory allocation here in detail. The size of a memory address is 8 bytes on 64-bit machines.

```c++
// main.cpp

#include <iostream>

#define LOG(x) std::cout << x << std::endl

int main() {
    int* foo = new int(9);  // allocate sizeof(int) bytes of memory, stores 8 in it, then return the allocated memory address to the foo

    LOG(foo);   // the item's memory address
    LOG(&foo);  // foo's memory address
    LOG(*foo);  // 9, the value that we set

    LOG(sizeof(foo));   // 8 bytes, the size of the item's memory address
    LOG(sizeof(&foo));  // 8 bytes, the size of foo's memory address
    LOG(sizeof(*foo));  // 4 bytes, the size of the item

    delete foo; // deallocate foo
}
```

For dynamic array, we use `delete[]` to deallocate the memory. We won't discuss about array here in detail.

```c++
// main.cpp

#include <iostream>

#define LOG(x) std::cout << x << std::endl

int main() {
    int* foo = new int[3];  // allocate 3 x sizeof(int) bytes of memory then return the first item's memory address to the foo

    foo[0] = 111;   // set the first item's value
    foo[1] = 222;   // set the second item's value
    foo[2] = 333;   // set the third/last item's value

    LOG(foo);           // the value of foo (the first item memory address)
    LOG(&foo);          // the memory address of foo
    LOG(*foo);          // the value the variable pointer points to (the first item)
    LOG(sizeof(foo));   // 8 bytes, the size of the pointer, not the size of the array
    LOG(sizeof(&foo));  // 8 bytes, the size of foo's memory address
    LOG(sizeof(*foo));  // 4 bytes, the size of the variable the pointer points to (the first item's size)

    LOG(foo[0]);            // 111, the value of the first item in foo
    LOG(&foo[0]);           // the memory address of the first item, the same as the value of foo
    LOG(sizeof(foo[0]));    // 4 bytes, the size of the first item
    LOG(sizeof(&foo[0]));   // 8 bytes, the size of the first item's memory address

    LOG(foo[1]);            // 222, the value of the second item in foo
    LOG(&foo[1]);           // the memory address of the second item
    LOG(sizeof(foo[1]));    // 4 bytes, the size of the second item
    LOG(sizeof(&foo[1]));   // 8 bytes, the size of the second item's memory address

    LOG(foo[2]);            // 333, the value of the third/last item in foo
    LOG(&foo[2]);           // the memory address of the third/last item
    LOG(sizeof(foo[2]));    // 4 bytes, the size of the third/last item
    LOG(sizeof(&foo[2]));   // 8 bytes, the size of the third/last item's memory address

    delete[] foo;   // deallocate the array, add [] at the end of the delete operator
}
```

## References

1. ["POINTERS in C++"](https://youtu.be/DTxHyVn0ODg). *The Cherno*. Retrieved 15 May 2021.
