# Linux System Calls and Library Functions
![AI](https://github.com/nu11secur1ty/Linux-System-Calls-and-Library-Functions/blob/master/photo/System-Call-and-Library-Function.png)

Computer software are developed to either automate some tasks or solve some problems. Either way, a software achieves the goal with the help of the logic that the developer of that software writes. Every logic requires some services like computing the length of a string, opening a file etc. Standard services are catered by some functions or calls that are provided for this purpose only.

Like for calculating string length, there exists a standard function like strlen(), for opening a file, there exists functions like open() and fopen(). We call these functions as standard functions as any application can use them.

These standard functions can be classified into two major categories :


  1    Library function calls.
  2    System function calls.


In this article, we will try to discuss the concept behind the system and library calls in form of various points and wherever required, I will provide the difference between the two.

# 1. Library functions Vs System calls

The functions which are a part of standard C library are known as Library functions. For example the standard string manipulation functions like strcmp(), strlen() etc are all library functions.

The functions which change the execution mode of the program from user mode to kernel mode are known as system calls. These calls are required in case some services are required by the program from kernel. For example, if we want to change the date and time of the system or if we want to create a network socket then these services can only be provided by kernel and hence these cases require system calls. For example, socket() is a system call.

# 2. Why do we need system calls?

System calls acts as entry point to OS kernel. There are certain tasks that can only be done if a process is running in kernel mode. Examples of these tasks can be interacting with hardware etc. So if a process wants to do such kind of task then it would require itself to be running in kernel mode which is made possible by system calls.


# 3. Types of library functions

Library functions can be of two types :

   . Functions which do not call any system call.
   . Functions that make a system call.

There are library functions that do not make any system call. For example, the string manipulation functions like strlen() etc fall under this category. Also, there are library functions that further make system calls, for example the fopen() function which a standard library function but internally uses the open() sytem call.



# 4. Interaction between components

The following diagram to depict how Library functions, system calls, application code interact with each other.

![AI](https://github.com/nu11secur1ty/Linux-System-Calls-and-Library-Functions/blob/master/photo/system-library-call.png)


The diagram above makes it clear that the application code can interact with Library functions or system calls. Also, a library function can also call system function from within. But only system calls have access to kernel which further can access computer hardware.


# 5. fopen() vs open()

Some of us may argue that why do we have two functions for the same operation ie opening a file?

Well, the answer to this is the fact that fopen() is a library function which provides buffered I/O services for opening a file while open() is a system call that provides non-buffered I/O services. Though open() function is also available for applications to use but application should avoid using it directly.

In general, if a library function corresponding to a system call exists, then applications should use the library function because :

    . Library functions are portable which means an application using standard library functions will run on all systems. While on the other hand an application relying on the corresponding system call may not run on every system as system call interface may vary from system to system.
    . Sometimes the corresponding library function makes the load to system call lesser resulting in non-frequent switches from user mode to kernel mode. For example if there is an application that reads data from file very frequently, then using fread() instead of read() would provide buffered I/O which means that not every call to fread() would result in a call to system call read(). The fread() may read larger chunk of data(than required by the user) in one go and hence subsequent fread() will not require a call to system function read().


# 6. Is malloc() a system call?

This is one of the very popular misconception that people have. Lets make it clear that malloc() is not a system call. The function call malloc() is a library function call that further uses the brk() or sbrk() system call for memory allocation.


# 7. System calls : Switching execution modes

Traditionally, the mechanism of raising an interrupt of ‘int $0x80’ to kernel was used. After trapping the interrupt, kernel processes it and changes the execution mode from user to kernel mode. Today, the systenter/sysexit instructions are used for switching the execution mode.


# 8. Some other differences

Besides all the above, here are a few more differences between a system and library call :

    . A library function is linked to the user program and executes in user space while a system call is not linked to a user program and executes in kernel space.
    . A library function execution time is counted in user level time while a system call execution time is counted as a part of system time.
    . Library functions can be debugged easily using a debugger while System calls cannot be debugged as they are executed by the kernel.




