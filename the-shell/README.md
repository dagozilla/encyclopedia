# The Shell

```bash
dagozilla:~$ pwd
/home/dagozilla
dagozilla:~$ cd /home
dagozilla:/home$ pwd
/home
dagozilla:/home$ cd ..
dagozilla:/$ pwd
/
dagozilla:/$ cd ./home
dagozilla:/home$ pwd
/home
dagozilla:/home$ cd dagozilla
dagozilla:~$ pwd
/home/dagozilla
dagozilla:~$ ../../bin/echo hello
hello
```
## Table of Contents
- [Background](#background)
- [What is the shell?](#what-is-the-shell?)
- [What is a terminal](#what-is-a-terminal?)
- [Course](#course)
- [References](#references)

## Background
- Computers these days have a variety of interfaces for giving them commands; fancyful graphical user interfaces, voice interfaces, and even AR/VR are everywhere.
- These are great for 80% of use-cases, but they are often fundamentally restricted in what they allow you to do — you cannot press a button that isn’t there or give a voice command that hasn’t been programmed.
- To take full advantage of the tools your computer provides, we have to go old-school and drop down to a textual interface: The Shell.

## What is the shell?
- The shell is a program that takes commands from the keyboard and gives them to the operating system to perform.
- In the old days, it was the only user interface available on a Unix-like system such as Linux. Nowadays, we have *graphical user interfaces (GUIs)* in addition to *command line interfaces (CLIs)* such as the shell.
- On most Linux systems a program called **bash** (which stands for Bourne Again SHell, an enhanced version of the original Unix shell program, **sh**, written by Steve Bourne) acts as the shell program. Besides **bash**, there are other shell programs available for Linux systems. These include: **ksh**, **tcsh** and **zsh**.

## What is a terminal?
- *Terminal emulator* is a program that opens a window and lets you interact with the shell.
- Examples: **gnome-terminal**, **konsole**, **xterm**, **rxvt**, **kvt**, **nxterm**, and **eterm**.
- Your device probably shipped with one installed, or you can install one fairly easily.

## Course
The shell course from [The Missing Semester of Your CS Education](https://missing.csail.mit.edu/2020/course-shell/) (a class from **MIT**) provides good explanations about the usage of the shell and some exercises for it.

## References
1. ["Course overview + the shell"](https://missing.csail.mit.edu/2020/course-shell/). *The Missing Semester of Your CS Education*. Retrieved 24 April 2021.
2. ["What is "the Shell"?"](https://linuxcommand.org/lc3_lts0010.php). *LinuxCommand*. Retrieved 24 April 2021.
