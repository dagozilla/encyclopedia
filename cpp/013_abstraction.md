# Abstraction in C++

## Table of Contents
- [Inheritance](#inheritance)
- [Virtual Functions](#virtual-functions)
- [Polymorphism](#polymorphism)
- [Abstract](#abstract)
- [References](#references)

## Inheritance
Inheritance between objects are fundamental concepts in OOP. Inheritance allows us to have a hierarchy of classes which relate to each other. In other words it allows us to have a base class which contains common functionality among the children or subclasses. The primary reason why this is useful is to avoid code duplication, code duplication refers to when we have a same code multiple times doing ***slightly*** different things. Instead of repeating the same code we can make a class which have all those common functionality and the other subclass just have to use them or maybe slightly change them according to its need.

```c++
// main.cpp

#include <iostream>

#define LOG(x) std::cout << x << std::endl

class Robot {
public:
    int X, Y, Speed;

    Robot(): X(0), Y(0) {}

    Robot(int x, int y): X(x), Y(y) {}

    void Move(int x, int y) {
        X += x;
        Y += y;
    }
};

class Robot3Wheeled {
public:
    const int type = 3;
    int X, Y, Speed;

    Robot3Wheeled(): X(0), Y(0) {}

    Robot3Wheeled(int x, int y): X(x), Y(y) {}

    void Move(int x, int y) {
        X += x;
        Y += y;
    }

    int GetType() {
        return type;
    }
};

int main() {
    Robot3Wheeled r;
    LOG(r.GetType()); // 3
}
```

This already look super messy, first of all the `Robot3Wheeled` class has basically the same structure as the `Robot` class only subtle changes such as a new static type and method. We can avoid this by using inheritance.

```c++
// main.cpp

#include <iostream>

#define LOG(x) std::cout << x << std::endl

class Robot {
public:
    int X, Y, Speed;

    Robot(): X(0), Y(0) {}

    Robot(int x, int y): X(x), Y(y) {}

    void Move(int x, int y) {
        X += x;
        Y += y;
    }
};

class Robot3Wheeled : public Robot {
public:
    const int type = 3;

    Robot3Wheeled(): Robot() {}

    Robot3Wheeled(int X, int Y): Robot(X,Y) {}

    int GetType() {
        return type;
    }
};

int main() {
    Robot3Wheeled r;
    LOG(r.GetType());   // 3
    r.X = 1;            // can access parent attributes
}
```

This not only make it more tidy it also make more sense because 3 wheeled robot is just another type of robot (base class). You can imagine it like completely copy and paste the whole property of `Robot` into `Robot3Wheeled`. There is a special type of visibility called ***protected*** which means the attribute are accessible for itself and also it's children. You might realize there is a `public` keyword, this is because C++ actually provide some mode of inheritance.
Mode of inheritance:
> ***public inheritance*** makes `public` members of the base class `public` in the derived class, and the `protected` members of the base class remain `protected` in the derived class.
> ***protected inheritance*** makes the `public` and `protected` members of the base class `protected` in the derived class.
> ***private inheritance*** makes the `public` and `protected` members of the base class `private` in the derived class.

## Virtual Functions
this concept allow us to override methods in subclasses. If we declare `GetType` as ***Virtual Functions*** we have the choice to override that method in the subclass to add simple change or even completely change it. To keep it simple all you need to know is that you need to declare `virtual` on the base class if you want to override it in the subclasses.

```c++
// main.cpp

#include <iostream>

#define LOG(x) std::cout << x << std::endl

class Robot {
public:
    int X, Y, Speed;

    Robot(): X(0), Y(0) {}

    Robot(int x, int y): X(x), Y(y) {}

    int GetType() {
        return -1;
    }
};

class Robot3Wheeled : public Robot {
public:
    const int type = 3;

    Robot3Wheeled(): Robot() {}

    Robot3Wheeled(int X, int Y): Robot(X,Y) {}

    int GetType() {
        return type;
    }
};

void PrintType(Robot* r) {
    LOG(r->GetType());
}

int main() {
    Robot* r = new Robot();
    PrintType(r);  // -1

    Robot3Wheeled* r3 = new Robot3Wheeled();
    PrintType(r3);  // -1 and not 3

    delete r, r3;
}
```

`PrintType` will not override the parent method because we dont declare it as `virtual`.

```c++
// main.cpp

#include <iostream>

#define LOG(x) std::cout << x << std::endl

class Robot {
public:
    int X, Y, Speed;

    Robot(): X(0), Y(0) {}

    Robot(int x, int y): X(x), Y(y) {}

    virtual int GetType() {
        return -1;
    }
};

class Robot3Wheeled : public Robot {
public:
    const int type = 3;

    Robot3Wheeled(): Robot() {}

    Robot3Wheeled(int X, int Y): Robot(X,Y) {}

    int GetType() override {    // override keyword is optional
        return type;
    }
};

void PrintType(Robot* r) {
    LOG(r->GetType());
}

int main() {
    Robot* r = new Robot();
    PrintType(r);  // -1

    Robot3Wheeled* r3 = new Robot3Wheeled();
    PrintType(r3);  // 3

    delete r, r3;
}
```

Now the code work as expected. Another useful use case of `virtual` is on destructor, it's probably a good idea to declare destructor as `virtual` so the child will also get destroyed.

## Polymorphism
***Polymorphism*** is the idea of having multiple type for a single type. If that doesn't make sense let's look at some example.

```c++
// main.cpp

#include <iostream>

#define LOG(x) std::cout << x << std::endl

class Robot {
public:
    int X, Y, Speed;

    Robot(): X(0), Y(0) {}

    Robot(int x, int y): X(x), Y(y) {}

    virtual int GetType() {
        return -1;
    }

    void Move(int x, int y) {
        X += x;
        Y += y;
    }
};

class Robot3Wheeled : public Robot {
public:
    const int type = 3;

    Robot3Wheeled(): Robot() {}

    Robot3Wheeled(int X, int Y): Robot(X,Y) {}

    int GetType() override {
        return type;
    }
};

class Robot4Wheeled : public Robot {
public:
    const int type = 4;

    Robot4Wheeled(): Robot() {}

    Robot4Wheeled(int X, int Y): Robot(X,Y) {}

    int GetType() override {
        return type;
    }
};

void PrintType(Robot* r) {
    LOG(r->GetType());
}

int main() {
    Robot3Wheeled* r3 = new Robot3Wheeled();
    PrintType(r3);  // 3

    Robot4Wheeled* r4 = new Robot4Wheeled();
    PrintType(r4);  // 4

    Robot* r;
    r = r3; // Polymorphism
    PrintType(r);  // 3

    r = r4; // Polymorphism
    PrintType(r);  // 4

    delete r3, r4, r;
}
```

Even though r1 is a `Robot` we can assign r3 which is a `Robot3Wheeled` and not get compile error, because essentially `Robot3Wheeled` is ***also*** a `Robot` 

## Abstract
***Abstract*** is a special `class` that contain unimplemented method. This can be achieved using what's called ***Pure Virtual Function*** some people might call this an ***Interface***. Sometimes it doesn't make sense for the parent class to implement a certain method (For example our `GetType`), this can be fixed using abstract class.

```c++
// main.cpp

#include <iostream>

#define LOG(x) std::cout << x << std::endl

class Robot {
public:
    int X, Y, Speed;

    Robot(): X(0), Y(0) {}

    Robot(int x, int y): X(x), Y(y) {}

    virtual int GetType() = 0;
};

class Robot3Wheeled : public Robot {
public:
    const int type = 3;

    Robot3Wheeled(): Robot() {}

    Robot3Wheeled(int X, int Y): Robot(X,Y) {}

    int GetType() override {    // override keyword is optional
        return type;
    }
};

void PrintType(Robot* r) {
    LOG(r->GetType());
}

int main() {
    Robot3Wheeled* r3 = new Robot3Wheeled();
    PrintType(r3);  // 3

    Robot* r = new Robot(); // compile error
    r = r3; // Polymorphism
    PrintType(r);  // 3

    delete r3, r;
}
```

One thing to note about abstract class is you can't instantiate an abstract class. This is because abstract class doesn't have implementation for certain methods, so abstract class can only be inherited but can't be instantiated.

## References
1. ["Inheritance in C++"](https://youtu.be/X8nYM8wdNRE). *The Cherno*. Retrieved 28 May 2021.
2. ["Virtual Functions in C++"](https://youtu.be/oIV2KchSyGQ). *The Cherno*. Retrieved 29 May 2021.
3. ["How to CREATE/INSTANTIATE OBJECTS in C++"](https://youtu.be/Ks97R1knQDY). *The Cherno*. Retrieved 29 May 2021.
4. ["Interfaces in C++ (Pure Virtual Functions)"](https://youtu.be/UWAdd13EfM8). *The Cherno*. Retrieved 29 May 2021.
