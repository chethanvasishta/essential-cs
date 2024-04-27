# Essential Computer Science
TODO: Add a description

# Basic Programming

## Build and Launch

1. When you build a helloworld program in C++, what are the steps in converting the helloworld.cpp into a helloworld.exe?
2. What are the parts of an helloworld executable?
3. When you launch the helloworld.exe, what all happens?
4. Let's say the program creates an array using malloc(). Who wrote the malloc implementation?
    a. Is malloc a system call? If yes, how does the program know how to call it? If no, what does malloc do?
5. Describe how a system call works

Rough: Context switching, sending pointers across processes, threads, 

### Exercises:



## Memory Management (OS)

Topics: Virtual Memory, Paging, Address Space, Reserved vs. Committed memory, Swap Disk

### Basics

1. What happens under the hood when you get an out-of-memory exception?
2. Can increasing your RAM (orimary memory) overcome the out-of-memory exception?
3. If I have a 32-bit process, what's the maximum memory I can allocate for the process?
4. If I have a machine with 1 GB RAM, can I allocate more than 1 GB in the process?
5. If I allocate a 10 MB array on a typical windows machine, how is the array placed on the primary memory?
    a. If it is contiguous, what happens when there's enough space in the RAM but no contiguous space for the 10 MB array?
    b. If it is not contiguous, i.e. placed in chunks, how does the system figure out which chunk a memory access like arr[i] should fetch?
6. 
   

### Intermediate

1. What's a kernel address space and a user address space? Why is this needed?
2. What are page tables? Why do you need them?
3. Where are the page tables stored?

Rough: TLB, Shootdown, Context Switch, ASID?

## Compile vs. Link





# C++

1. 
