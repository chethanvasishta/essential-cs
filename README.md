# Essential Computer Science

The following is a list of questions aimed to test the understanding of basics of computer science required for every day application development. The questions are tagged with relevant topics that will provide answers. Some questions might seem absurd to someone who understand the fundamentals of the area, but it's designed to force the developers to test their understanding of the fundamentals

# Basic Programming

## Build and Launch

1. When you build a helloworld program (see below) in C++, what are the steps in converting the helloworld.cpp into a helloworld.exe?
```c++
int foo(int a, int b)
{
    int c = a + b;
    a++;
    b++;
    return c;
}
int main(int argc, char* argv[])
{
    int a = 10, b=12;
    int c = foo(a, b);
    std::cout << a << " + " << b << " = " c << std::endl;
    int *p = malloc(10); // allocate 10 bytes
    return 0;
}
```
2. What are the parts of an helloworld executable?
    - Where is the main() function located? Similarly, where is foo() located on the executable?
    - Where is malloc() located?
3. When you launch the helloworld.exe, what all happens?
    - Who calls the main() function?
    - How many threads are created when this program launches?
    - Where are these threads located in the memory? Are they part of any heap?
    - Is a heap created on program launch?
    - Where is the code for main() and foo() located in the memory? Can a program accidentally overwrite this memory location?
4. [Libraries] Suppose an application has a a set of dependent DLLs?
    - When are these DLLs loaded?
    - Are all the dependent DLLs loaded in the beginning of the program? Is it configurable?
5. [Function Calls] How does the main() function send a and b to foo()?
    - Are the a and b in the foo() located in the same space as main's a and b?
    - If yes, does changing a in foo() change the a in main too? If not, how are these variables located?
    - When is the space for a and b in foo() created and destroyed?
    - [Stack Frames] Who creates the stack frame foo()? Who destroys it?
    - Can you describe the stack frame structure for the main() calling foo()? What all does it contain?
6. [Recursion] Can you describe the stack frame for main() calling foo() calling foo()?
    - Are a and b of foo shared across recursion calls?
    - Can any function recursively call itself?
    - Is there a limit to the depth of recusion? If yes, what defines it?
7. [System Call] Let's say the program creates an array using malloc(). Who wrote the malloc implementation?    
    - Is malloc a system call? If yes, how does the program know how to call it? If no, what does malloc do?
    - Let's say there's a system call falloc(). Is making a system call same as calling foo()? If not, what's the difference?  
    - Describe how a system call works.

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
