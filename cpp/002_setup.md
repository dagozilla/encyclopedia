# C++ Development Environment Setup

## Linux
Open a terminal and execute this commands to install and ensure that the `g++` compiler and `gdb` debugger have installed on your computer.

```sh
# Update the package lists.
sudo apt update

# Install all the libraries which are required to compile, run, and debug a C++ program.
sudo apt install build-essential gdb

# Check the g++ and gdb installation.
g++ --version
gdb --version
```

Create a new file named `main.cpp` and paste in the following source code:
```c++
#include <iostream>

int main() {
    std::cout << "DAGOZILLA ITB" << std::endl;
}
```

Open a terminal to the project directory and compile the source code with `g++` compiler. The following command will output an executable file named `main`.
```sh
g++ main.cpp -o main
```

Run the executable file from your terminal. It will print a text to the terminal.
```sh
./main
# DAGOZILLA ITB
```

Your ready to develop C++ programs in Linux environment.

## References
1. ["Setting up C++ Development Environment"](https://www.geeksforgeeks.org/setting-c-development-environment/). *GeeksforGeeks*. Retrieved 12 May 2021.
2. ["Using C++ on Linux in VS Code"](https://code.visualstudio.com/docs/cpp/config-linux). *Visual Studio Code*. Retrieved 12 May 2021.
