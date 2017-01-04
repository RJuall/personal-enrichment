# How Linux Works:

## What Every Superuser Should Know

### by Brian Ward

Ward, Brian. *How Linux Works: What Every Superuser Should Know.* San Francisco: No Starch Press, 2015. Print.

***

## Chapter 1 - "The Big Picture"

#### p.1

An operating system works through abstraction - a method by which many of the details involved in building and/or running a computer system can be ignored.

There are many terms for an abstracted sub-division in computer software, i.e. *subsystem*, *module*, *package*, *component*

When building a component a software developer typically doesn't think about the internal structure of other components, just which components can be used and how.

#### 1.1 Levels and Layers of Abstraction in a Linux System, p.2

Components are arranged into *layers* or *levels*, a classification of a component according to where that component sits between the user and the hardware \(the 0's and 1's\).

The operating system occupies most of the layers in between the hardware and the user.

###### A Linux system has three main levels:  

**Hardware**  

 * Processor \(CPU\)
 * Main Memory \(RAM\)
 * Disks
 * Network Ports
 * etc.  
 
**Linux Kernel**  

 * System Calls
 * Process Management
 * Memory Management
 * Device Drivers
 * etc.  
 
**User Processes**  

 * Graphical User Interface
 * Servers
 * Shell
 * etc.

The Linux kernel runs in *kernel mode* & user processes run in *user mode*.

Code running in kernel mode has unrestricted access to the processor and main memory & the area that only the kernel can access is called *kernel space*.

User mode restricts access to a relatively quite small subset of memory and safe CPU operations - *User space* are the parts of main memory that the user processes can access, meaning the consequences are limited should a user process crash, etc.

How much 'damage' a user process can cause varies, however.

#### 1.2 Hardware: Understanding Main Memory, p.4

"A CPU is just an operator on memory; it reads its instructions and data from the memory and writes data back out to the memory."

*State* is a term referring to a particular arrangement of bits in memory.

*Image* is a term referring to a particular physical arrangement of bits.

*Main memory* is the most important hardware in a computer system, arguably.

In its raw form, main memory is simply a large storage area for bits, 1's and 0's.

#### 1.3 The Kernel, p.4

"Nearly everything that the kernel does revolves around main memory."

The 4 general system areas that the kernel is in charge of:  
 * **Processes** - Determining which processes are allowed to use the CPU
 * **Memory** - Keeping track of all memory, where and to whom it is allocated, what might be shared, and what is free
 * **Device Drivers** - Interfacing between hardware \(i.e. the Disk\) and processes
 * **System Calls and Support** - Using system calls to communicate with the kernel
 
Two texts detailing the workings of a kernel:
 * *Operating System Concepts, 9th Edition* by Abraham Silberschatz, Peter B. Galvin, and Greg Gagne \(Wiley, 2012\)
 * *Modern Operating Systems, 4th Edition* by Andrew S. Tanenbaum and Herbert Bos \(Prentice Hall, 2014\)
 
##### 1.3.1 Process Management p.5

*Process Management* is the starting, pausing, resuming, and terminating of processes.

In a modern OS, many processes will run 'simultaneously', though usually those processes do not run *exactly* at the same time

Using a one-core CPU, for example, only one process may use the CPU at any given moment

Each process is given a *time slice*, an extremely tiny amount of time a process is given access to a CPU in order for it to be able to complete some work

The time slices are so small that processes appear to be running simultaneously

###### Context switching steps (quoted):  
 1. The CPU \(the actual hardware\) interrupts the current process based on an internal timer, switches into kernel mode, and hands control back to the kernel.
 2. The kernel records the current state of the CPU and memory, which will be essential to resuming the process that was just interrupted.
 3. The kernel performs any tasks that might have come up during the preceding time slice \(such as collecting data from input and output, or I/O, operations\).
 4. The kernel is now ready to let another process run. The kernel analyzes the list of processes that are ready to run and chooses one.
 5. The kernel prepares the memory for this new process, and then prepares the CPU.
 6. The kernel tells the CPU how long the time slice for the new process will last.
 7. The kernel switches the CPU into user mode and hands control of the CPU to he process.
 
Based on this list it is clear when the kernel runs: *between* processes

Multi-CPU systems are more complicated because the kernel does not necessarily need to relinquish control of its current CPU to allow a process to run on a different CPU, but usually this is what happens so that CPU usage is maximized.

##### 1.3.2 Memory Management, p.6

The kernel's job of memory management is complicated by the fact that it must do its job during a context switch

This is further complicated because of certain conditions that must be true (quoted):  
 * The kernel must have its own private area in memory that user processes can't access.
 * Each user process needs its own section of memory.
 * One user process may not access the private memory of another process.
 * User processes can share memory.
 * Some memory in user processes can be read-only.
 * The system can use more memory than is physically present by using disk space as auxiliary.
 
Modern CPUs include a *memory management unit \(MMU\)* that enables a memory access scheme called *virtual memory*

Virtual memory is a system by which processes do not directly access physical memory, but, by the use of a *memory address map* \(page table\), the kernel acts as though each process has an entire machine to itself.

##### 1.3.3 Device Divers and Management, p.7

"Device drivers have traditionally been part of the kernel, and they strive to present a uniform interface to user processes in order to simplify the software developer's job.

"A device is typically accessible only in kernel mode because improper access...could crash the machine."

##### 1.3.4 System Calls and Support, p.7

*System calls* or *syscalls* perform specific tasks that a user process cannot do well or at all - i.e. opening, reading, or writing files.

`fork()` and `exec()` are important to understanding how processes start up:  
 * `fork()` - when called the kernel creates a nearly identical copy of a process
 * `exec()` - when `exec(*program*)` is called, the kernel starts `*program*`, which replaces the current process
 
All user processes on a Linux system start as a result of `fork()`, disregarding `init`

Similarly `exec()` is normally used to start a new program instead of running a copy of an existing process

*Pseudodevices* look like devices to user processes, but they are purely implemented in software. Because of this they do not need to be in the kernel, but usually are for practical reasons. */dev/random* is an example of this.

#### 1.4 User Space, p.8

User space is the main memory that the kernel allocates for user processes and also the memory for the entire collection of running processes.

There is a rudimentary service level/layer structure to the kinds of components that user processes represent:  
 * Basic services at the bottom near the kernel \(i.e. network configuration, communication bus, diagnostic logging, etc.\)
 * Utility services in the middle \(i.e. mail, print, or database services, etc.\)
 * Applications closest to the user \(i.e. user interface, web browser, etc.\)
 
Components use other components. Generally if one component wants to use another, the second component is either at the same service level or below.

"In reality, there are no rules in user space."

#### 1.5 Users, p.9

The Linux kernel supports the traditional concept of a Unix user, an entity that can run processes and own files.

The kernel identifies users by numeric identifiers called *userids*, not by *username*

"Users exist primarily to support permissions and boundaries."

A Linux system normally has a number of users in addition to the ones that correspond to the real human beings who use the system, the most important of which being *root*

*Root* also known as the *superuser* is different in that it does not adhere to any restrictions and is the administrator on a traditional Unix system

As powerful as the root user is it still runs in the operating system's user mode - not kernel mode

"System designers constantly try to make root access as unnecessary as possible..."

A *group* is a set of users, a group's main purpose is to allow a user to share file access with other users in a group
