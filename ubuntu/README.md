# Ubuntu

## Table of Contents
- [About Ubuntu](#about-ubuntu)
  - [What is GNU/Linux?](#what-is-gnu/linux)
  - [What is Debian?](#what-is-debian)
  - [What is Ubuntu?](#what-is-ubuntu)
  - [What is the relationship between Unix, Linux, Debian, and Ubuntu?](#what-is-the-relationship-between-unix-linux-debian-and-ubuntu?)
- [Installation](#installation)
  - [Dual Boot (Windows 10 x Ubuntu)](#dual-boot-(Windows-10-x-Ubuntu))
  - [Virtual Machine (Oracle VirtualBox)](#virtual-machine-(oracle-virtualbox))
- [References](#references)

## About Ubuntu

### What is GNU/Linux?
- First released by Linus Torvalds, Linux is an operating system: a series of programs that let you interact with your computer and run other programs.
- An operating system consists of various fundamental programs which are needed by your computer so that it can:
  - communicate and receive instructions from users
  - read and write data to hard disks, tapes, and printers
  - control the use of memory, and
  - run other software
- The most important part of an operating system is the kernel. In a GNU/Linux system, Linux is the kernel component. The rest of the system consists of other programs, many of which were written by or for the GNU Project.
- Because the Linux kernel alone does not form a working operating system, some people prefer to use the term “GNU/Linux” to refer to systems that many people casually refer to as “Linux”.

### What is Debian?
- Debian is an all-volunteer organization dedicated to developing free software and promoting the ideals of the Free Software community.
- Debian Project began in 1993, when Ian Murdock issued an open invitation to software developers to contribute to a complete and coherent software distribution based on the relatively new Linux kernel.
- Ubuntu and Debian are distinct but parallel and closely linked systems. The Ubuntu project seeks to complement the Debian project.

### What is Ubuntu?
- Ubuntu is a Linux distribution based on Debian that mainly used for the enterprise server, desktop, cloud, and IoT.
- Ubuntu is released every six months, with long-term support (LTS) releases every two years.
  - Non-LTS releases: 9 months support
  - LTS releases: 5 years support

### What is the relationship between Unix, Linux, Debian, and Ubuntu?
- Unix: An old Operating System which the Linux kernel loosely based on
- Linux: Kernel (Still in active development)
- Debian: Early Operating System to Ubuntu (Still in active development)
- Ubuntu: Newer Operating System based on Debian (Still in active development)

## Installation
There are several ways to install Ubuntu into your laptop/PC. It is recommended to install it in dual boot mode since it gives better performance to your installed Ubuntu.

### Dual Boot (Windows 10 x Ubuntu)
Follow the installation process from this [post](https://www.itzgeek.com/post/how-to-install-ubuntu-20-04-alongside-with-windows-10-in-dual-boot/) but please read some notes below before begin the installation process.
- Make sure your laptop is in charging mode while installing ubuntu.
- It is recommended to allocate around 100GB (1GB = 1024MB) disk space for Ubuntu.
- It is recommended to do automatic partitioning instead of manual partitioning when partitioning the disk at ubuntu installation process.
- If you're still in doubt to do it by yourself (especially in the Disk Partitioning step), ask a friend who is experienced in this kind of process to assist you.

### Virtual Machine (Oracle VirtualBox)
Follow the installation process from this [post](https://www.lifewire.com/install-ubuntu-linux-windows-10-steps-2202108) but please read some notes below before begin the installation process.
- Please remember that since it uses virtualization, it might not performed as good as the one that directly installed to the machine.
- This supposed to be worked on VirtualBox for Mac but please do your own research since new MacBooks using Apple silicon and the new macOS is made to optimize the potential of this silicon.

## References
1. ["What is Ubuntu?"](https://help.ubuntu.com/lts/installation-guide/s390x/ch01s01.html). *Official Ubuntu Documentation*. Retrieved 24 April 2021.
2. ["What is Debian?"](https://help.ubuntu.com/lts/installation-guide/s390x/ch01s02.html). *Official Ubuntu Documentation*. Retrieved 24 April 2021.
3. ["What is GNU/Linux?"](https://help.ubuntu.com/lts/installation-guide/s390x/ch01s03.html). *Official Ubuntu Documentation*. Retrieved 24 April 2021.
4. ["What is the relationship between Unix, Linux, Ubuntu, Debian and Android?"](https://superuser.com/questions/816018/what-is-the-relationship-between-unix-linux-ubuntu-debian-and-android). *superuser*. Retrieved 24 April 2021.
5. ["How To Install Ubuntu 20.04 Alongside With Windows 10 in Dual Boot"](https://www.itzgeek.com/post/how-to-install-ubuntu-20-04-alongside-with-windows-10-in-dual-boot/). *IT'zGeek*. Retrieved 24 April 2021.
6. ["How to Install Ubuntu Linux on Windows 10 With VirtualBox"](https://www.lifewire.com/install-ubuntu-linux-windows-10-steps-2202108). *Lifewire*. Retrieved 24 April 2021.
