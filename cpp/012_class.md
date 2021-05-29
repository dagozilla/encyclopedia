# Class in C++

## Table of Contents
- [Definition](#definition)
- [Class](#class)
- [Visibility](#visibility)
- [Struct](#struct)
- [Constructor](#constructor)
- [Destructor](#destructor)
- [Copy Constructor](#copy-constructor)
- [Operator Overloading](#operator-overloading)
- [Static](#static)
- [References](#references)

## Definition
> A **Class** is a user-defined data type, which holds its own data members and member functions. This primarily used to encapsulate data of an object and grouped them together

## Class
Let's say we want to implement a simple robot that has position X, Y and also Speed. We can implement this normally and it will works completely fine.

```c++
// main.cpp

#include <iostream>

#define LOG(x) std::cout << x << std::endl

int main() {
    int X, Y, Speed;
    X = 2;
    Y = 3;
    LOG(X); // 2
}
```

But if you want to make another robot you need the same property (X, Y, Speed) and need to duplicate the previous code.

```c++
// main.cpp

#include <iostream>

#define LOG(x) std::cout << x << std::endl

int main() {
    int r1X, r1Y, r1Speed;
    r1X = 2;
    r1Y = 3;

    int r2X, r2Y, r2Speed;
    r2X = 4;
    r2Y = 5;

    LOG(r1X); // 2
}
```

Suddenly you have a block of code that can actually be simplified, you can use array however but if the number of property is huge the same problem will occur. So what's the solution? here is where class comes in, you can conceptualize what a group of data will be (in this case a robot) and define the property of that group.

```c++
// main.cpp

#include <iostream>

#define LOG(x) std::cout << x << std::endl

class Robot {
    int X, Y, Speed;
};

int main() {
    Robot r1, r2;
    r1.X = 2;
    r1.Y = 3;
    r2.X = 4;
    r2.Y = 5;

    LOG(r1.X); // compile error
}
```

This looks more tidy and can be understood relatively easier by human readers than the previous code. However if you run this code you would meet an error, that will be disscussed in the next section.

## Visibility
It is useful to define beforehand which attributes can be accessed by who, in C++ this is implemented by a few keywords which is ***private***, ***public*** and ***protected***. ***private*** means only the class where it defined can access those attributes and ***public*** as the name suggest everyone can access the attributes. We will come back to ***protected*** later on.

```c++
// main.cpp

#include <iostream>

#define LOG(x) std::cout << x << std::endl

class Robot {
public:
    int X, Y, Speed;
};

int main() {
    Robot r1, r2;
    r1.X = 2;
    r1.Y = 3;
    r2.X = 4;
    r2.Y = 5;

    LOG(r1.X); // 2
}
```

Now the attributes are declared as ***public*** it can be accessed outside of the class itself. Class by default declare attributes as ***private*** if not specified. This implementation is not frequently used by other people because it's not good to have public attributes, people usually declare attributes as ***private*** and then make what's called `getter` and `setter`. What's the difference? for example if i update the speed of the robot, it probably logical to update the position of the robot, instead of updating manually every time the speed is updated we can set a `SpeedSetter` function that automatically update the position.


Now we have the class we can make as many robot as we want, though it's not very useful because there is no functionality to this class. Let's add a new functionality called `Move` that will move the robot position according to the input. 

```c++
// main.cpp

#include <iostream>

#define LOG(x) std::cout << x << std::endl

class Robot {
public:
    int X, Y, Speed;

    void Move(int x, int y) {
        X += x;
        Y += y;
    }
};

int main() {
    Robot r;
    r.X = 2;
    r.Y = 3;

    r.Move(5, 5);

    LOG(r.X); // 7
}
```

This code will work as expected and add the input to the attributes of the object.

## Struct
Struct is another keyword in C++ that is equivalent to keyword `class` with only 1 difference that is while `class` declare property as `private` by default, `struct` declare property as `public` by default.

```c++
// main.cpp

#include <iostream>

#define LOG(x) std::cout << x << std::endl

struct Robot {
    int X, Y, Speed;

    void Move(int x, int y) {
        X += x;
        Y += y;
    }
};

int main() {
    Robot r;
    r.X = 2;
    r.Y = 3;

    r.Move(5, 5);

    LOG(r.X); // 7
}
```

Exactly the same code as before but replacing `class` with `struct` and removing the `public` keyword and this will work just fine. A lot of people discuss about how and when you should use each of them but it's just a matter of style and personal preferences, codewise it will function the same.

## Constructor
Defining the attributes line by line after instantiating a class is inefficient because you can have a lot of attributes in a class. To solve this problem C++ has a solution that's called ***Constructor*** constructor is a special type of method that will get called everytime a new object is instantiated.

```c++
// main.cpp

#include <iostream>

#define LOG(x) std::cout << x << std::endl

class Robot {
public:
    int X, Y, Speed;

    Robot() {
        X = 0;
        Y = 0;
    }
};

int main() {
    Robot r;

    LOG(r.X); // 0
}
```

We can see that even without assigning value `x` in `main` the value is automatically set to 0 because the constructor is automatically called everytime a new object is created. We can also add parameters to the constructor to initialize it with value and not only that we can actually have more than one constructor that has different parameters (concept of overloading).

```c++
// main.cpp

#include <iostream>

#define LOG(x) std::cout << x << std::endl

class Robot {
public:
    int X, Y, Speed;

    Robot() {
        LOG("normal");
        X = 0;
        Y = 0;
    }

    Robot(int x, int y) {
        LOG("overloading");
        X = x;
        Y = y;
    }
};

int main() {
    Robot r1;       // normal
    LOG(r1.X);      // 0

    Robot r2(2, 3); // overloading
    LOG(r2.X);      // 2
}
```

We can see that this two instantiation calls different constructor in this example. There is actually a syntax that can simplify more if you want to change the member of the class.

```c++
// main.cpp

#include <iostream>

#define LOG(x) std::cout << x << std::endl

class Robot {
public:
    int X, Y, Speed;

    Robot(): X(0), Y(0) {
        LOG("normal");
    }

    Robot(int x, int y): X(x), Y(y) {
        LOG("overloading");
    }
};

int main() {
    Robot r1;       // normal
    LOG(r1.X);      // 0

    Robot r2(2, 3); // overloading
    LOG(r2.X);      // 2
}
```

## Destructor
Similiarly to how constructor is called when you instantiate a new object, ***Destructor*** is called whenever you destroy an object. Constructor is where you initialize that you need to do and destructor is where you destroy what you has initialize (for example cleaning the memory).

```c++
// main.cpp

#include <iostream>

#define LOG(x) std::cout << x << std::endl

class Robot {
public:
    int X, Y, Speed;

    Robot(): X(0), Y(0) {
        LOG("normal");
    }

    Robot(int x, int y): X(x), Y(y) {
        LOG("overloading");
    }

    ~Robot() {
        LOG("Destructor");
    }
};

int main() {
    Robot r1;       // normal
    LOG(r1.X);      // 0

    Robot r2(2, 3); // overloading
    LOG(r2.X);      // 2
}
```

Even though this doesn't look that helpful, this is something that will be need implemented if you manually declare something in the constructor like pointers. If a data members need to call `delete` then this is the place where you would call them.

## Copy Constructor
Copy constructor is a whole new different concept in OOP and can be useful in many scenarios. This often very useful when you need to copy a whole internal structures of the object that you want to copy.

```c++
// main.cpp

#include <iostream>

#define LOG(x) std::cout << x << std::endl

class Robot {
public:
    int X, Y, Speed;

    Robot(): X(0), Y(0) {
        LOG("normal");
    }

    Robot(int x, int y): X(x), Y(y) {
        LOG("overloading");
    }

    Robot(const Robot& other): X(other.X), Y(other.Y) {
        LOG("copy constructor");
    }

    ~Robot() {
        LOG("Destructor");
    }
};

int main() {
    Robot r1(2, 3); // overloading
    Robot r2 = r1;  // copy constructor
    LOG(r2.X);
}
```

This might seem unhelpful at first because we've done nothing in the copy contructor but again this is helpful when you need to manually initialize something on the constructor. For example if you initialize list of data manually in the constructor, it's a good idea to copy them one by one inside copy constructor because you don't want them to have the same memory address.

## Operator Overloading
This is something special on C++ compared to other high-level language. Other language don't give you this much control but C++ does, even though giving more controls doesn't necessarily a good thing. So what's ***Operator Overloading***? as the name suggest it overload an operator. What's operator? operator are special symbol like `+`, `-`, `*`, `&` and many more. List of available operators are linked in references below. To use operator overloading you need to write the operator you want to overload after the keyword `operator`. Let's use a new struct called Vec2 to demonstrate operatorr overloading.

```c++
// main.cpp

#include <iostream>

#define LOG(x) std::cout << x << std::endl

struct Vec2 {
    int X, Y;

    Vec2(): X(0), Y(0) {}

    Vec2(int x, int y): X(x), Y(y) {}

    Vec2 operator+(const Vec2& other) {
        return Vec2(X + other.X, Y + other.Y);
    }
};

int main() {
    Vec2 V1(5,5), V2(1,2);
    Vec2 V3 = V1 + V2;
    LOG(V3.X);  // 6
    LOG(V3.Y);  // 7
}
```

This opens up a lot of possibility for implementation (and also for bugs).

## Static
Static is another keyword in C++ that has different application, but here we only going to talk about the usage of the word `static` inside a class. `static` property in a class means there is only one property across all instances. For example if i have 2 instances of `Robot` that has `static` attributes of `type` this `count` is shared across all instances.

```c++
// main.cpp

#include <iostream>

#define LOG(x) std::cout << x << std::endl

class Robot {
public:
    static int count;
    int X, Y, Speed;

    Robot() {
        count++;
    }
};

int Robot::count = 0;  // initialize static members

int main() {
    Robot r1, r2;

    LOG(r2.count); // 2
}
```

Here we access the `count` of r2 without declaring it but it prints `2`, this is because `count` is a static attributes that is it shares through all instances so assigning value on it on r1 will also set the value on r2. This code will works fine but it actually more precise to access the `count` as a member of its class not a variable from each instances.

```c++
// main.cpp

#include <iostream>

#define LOG(x) std::cout << x << std::endl

class Robot {
public:
    static int count;
    int X, Y, Speed;
};

int main() {
    Robot r1, r2; // not needed
    Robot::count = 2;

    LOG(Robot::count); // 2
}
```

This works exactly the same as before and you can actually delete the instances because we only accessing the count. `static` can also be used for methods to share it across all instances.


```c++
// main.cpp

#include <iostream>

#define LOG(x) std::cout << x << std::endl

class Robot {
public:
    static int count;
    int X, Y, Speed;

    static void PrintCount() {
        std::cout << count << std::endl;
    }
};

int Robot::count;  // initialize static members

int main() {
    Robot::count = 10;

    Robot::PrintCount();  // 10
    // LOG(Robot::count); // 10
}
```

But you can't access non-static attributes from inside a `static` method and it's pretty obvious if you think about it, because non-static attributes are not shared therefore there are a different one from each instances and the methods wouldn't be able to know which one to use in the implementation.


```c++
// main.cpp

#include <iostream>

#define LOG(x) std::cout << x << std::endl

class Robot {
public:
    static int count;
    int X, Y, Speed;

    static void PrintCount() {
        std::cout << X << ", " << Y << " " count << std::endl;  // compile error
    }
};

int Robot::count;  // initialize static members

int main() {
    Robot::count = 10;

    Robot::PrintCount();  // 10
    // LOG(Robot::count); // 10
}
```

`static` actually can be used more in different context, but for this we only use `static` in the context of `class`.

## References

1. ["CLASSES in C++"](https://youtu.be/2BP8NhxjrO0). *The Cherno*. Retrieved 27 May 2021.
2. ["CLASSES vs STRUCTS in C++"](https://youtu.be/fLgTtaqqJp0). *The Cherno*. Retrieved 27 May 2021.
3. ["Constructors in C++"](https://youtu.be/FXhALMsHwEY). *The Cherno*. Retrieved 27 May 2021.
4. ["Destructors in C++"](https://youtu.be/D8cWquReFqw). *The Cherno*. Retrieved 27 May 2021.
5. ["Visibility in C++"](https://youtu.be/6OVQ8nh3KP0). *The Cherno*. Retrieved 27 May 2021.
6. ["Static for Classes and Structs in C++"](https://youtu.be/V-BFlMrBtqQ). *The Cherno*. Retrieved 27 May 2021.
7. ["Copying and Copy Constructors in C++"](https://youtu.be/BvR1Pgzzr38). *The Cherno*. Retrieved 28 May 2021.
8. ["OPERATORS and OPERATOR OVERLOADING in C++"](https://youtu.be/mS9755gF66w). *The Cherno*. Retrieved 29 May 2021.
9. ["operator overloading"](https://en.cppreference.com/w/cpp/language/operators). *cppreference*. Retrieved 29 May 2021.
