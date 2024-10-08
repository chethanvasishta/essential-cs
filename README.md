# Essential Computer Science

The following is a list of questions aimed to test the understanding of basics of computer science required for every day application development. The questions are tagged with relevant topics that will provide answers. Some questions might seem absurd to someone who understands the fundamentals of the area, but it's designed to force the developers to test their understanding of the fundamentals.

# Basic Programming

## Build and Launch

### Single Process

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
	p[0] = 42;
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
	- Where are they loaded in the virtual address space?
	- Who is responsible for loading the DLLs?
	- If I allocate memory (through malloc) in one DLL of an EXE, can I deallocate it in another?
	- If I allocate memory (through valloc or some system call instead of malloc) in one DLL of an EXE, can I deallocate it in another?
	- Does this work?
		```
		main()
		{
			struct x;
			dll_foo(&x);
		}

		dll_foo(struct *x)
		{
			print(x->a, x->b);
		}
		```

5. [Function Calls] How does the main() function send a and b to foo()?
	- Are the a and b in the foo() located in the same space as main's a and b?
	- If yes, does changing a in foo() change the a in main too? If not, how are these variables located?
	- When is the space for a and b in foo() created and destroyed?
	- Recommended Concepts: Calling Conventions
6. [Stack Frames] Who creates the stack frame foo()? Who destroys it?
	- Can you describe the stack frame structure for the main() calling foo()? What all does it contain?
	- Can you intentionally overwrite any arbitrary address location inside a thread stack?
		- If not, who prevents it? What's the mechanism to prevent it?
	- Where exactly is the thread stack located in memory?
	- Is there a limit to the number of threads that can be created by a process?
	- Is there a limit to the number of stack frames that can be created for a thread?
	- [Bonus] Can main access/read the variable c in foo() after foo() is over? Note: It's not as straightforward as you think!
7. [Recursion] Can you describe the stack frame for main() calling foo() calling foo()?
	- Are a and b of foo shared across recursion calls?
	- Can any function recursively call itself?
	- Is there a limit to the depth of recusion? If yes, what defines it?
8. [System Call] Let's say the program creates an array using malloc(). Who wrote the malloc implementation?    
	- Is malloc a system call? If yes, how does the program know how to call it? If no, what does malloc do? How is it implemented?
	- Let's say there's a system call falloc(). Is making a system call same as calling foo()? If not, what's the difference?  
	- Describe how a system call works.
9. [Compatibility] Can you call a DLL compiled with a different compiler? For e.g. helloworld.exe compiled with MSVC-14 that wants to use a function bar() in dep.dll compiled with Intel C++ compiler? Other scenarios:
	- Helloworld.exe -MSVC-14, dep.dll - MSVC-19?
	- Helloworld.exe - 32-bit MSVC-14, dep.dll 64-bit MSVC-14? If that works, how? If not, why not?
	- Is there a run a program compiled for Intel x86 processor on a AMD processor? What about ARM processors?
		- Can a program compiled for a Intel x86 processor run on any Intel x86 processor?
10. [Heaps]
	- When malloc() allocates a new memory allocation, say 100 bytes, is a new heap created always?
	- If not, is an existing heap reused? Can two allocations share a heap? If so, who does the bookkeeping?
	- Can multiple heaps exist inside a process?
	- When an allocation is freed, what happens inside the heap?
	- new vs. malloc
		- What the difference between new and malloc
		- Can you call free on a memory allocation created by the new operator
		- Can there be multiple malloc() in the same program? If yes, can a free() deallocate memory created by either of the malloc()
		- What happens if you free a pointer twice?
		- Can you call delete[] on an allocation created by new? (Not new[])
	- Exercise:
		- [Basic] Fix memory leaks in TODO program
		- [Intermediate] Write your memory allocator
11. [Stack vs. Heap]
	- Where are a and b allocated? Where is the allocation pointed by p allocated?
	- What's the scope and lifetime of a and b inside main? Similarly, a, b and c inside foo()? What's the scope of
12. [Initialization order]
	- TODO: Globals, singletons, etc.
	- Can you rely on the initialization order of globals across files?
13. [Crash]
	- What does it mean for a program to crash?
	- What happens after a program crashes? What happens to the state of the threads, heaps, loaded DLLs, etc. on program crash?
		- If the above program crashes because of some reason after the malloc() call completes (p is assigned), will the system lose the memory allocated for p?
		- Do the threads apart from the crashed thread continue to run after the crash?
	- Enumerate the reasons why a program could crash. Are all crashes irrecoverable?
	- Can a program crash, crash the entire system?
14. [Threads]
	- In a process with 2 threads, how many stacks are created?
	- Do threads share the virtual address space?
	- Can a thread access the memory of another thread?
	- Can a thread access the stack of another thread?
15. [Stack]
	- Can you write beyond a stack frame?
16. [Compatibility]
	- If I build a main.exe in a Windows machine, can I run it on Linux? Why not?
		- What if the loader was also ported to Linux? Can I run it then?
			- How are system calls handled in Windows vs Linux?
17. If I copy-paste main.exe to any other machine with a different Windows OS, would it be able to run?
	- What if the machines had the same version of OS? 
		- What if the machines all had x86 architecture? (x86, but different processors)
18. What happens when I run a 32-bit process on a 64-bit machine?
19. [Exceptions]
	- If an exception is thrown somewhere in the call stack, how does a function much below the current function frame catch and handle that exception?
20. [Stack]
	- What happens in the following code? What does cout print when the called function returns nothing, but the caller expects it to return an int?

		```
		// -- Main.cpp --

		int foo(int a, int b);

		int main()
		{
			int x = foo(10, 20);
			cout << x;
		}
		

		// -- helper.cpp --

		void foo(int a, int b)
		{

			// do something with a and b
			cout << a << b;
		}
		```
### Multiple-Processes

1. Can you launch multiple instances of an application in a system simultaneously? If  yes,
	- What gets shared between the instances?
	- How many copies of the dependent DLLs are in memory?
	- In the above example, can another instance dereference the pointer p and read p[0]? Can another instance write to that?
1. If I run two instances of the same application, how does the loader write the addresses to function calls in each instance? Because they would be sharing the code on RAM.
2. If two different applications running simultaneously refer to a same DLL, are there two copies of the DLL in memory? If no,
	- What happens to the state inside the DLL? Is it accessible across processes?
	- If there's a function bar() inside the DLL, can it be called by both processes simultaneously? What happens if bar() modifies a global state inside a DLL?
	- Exercise: Create the above scenario, attach a debugger like Visual Studio and see what gets loaded and shared?
3. [Security] If two programs allocate two 10 MB arrays in RAM, can one access the array of another? If not, who prevents this from happening?
   - What's the mechanism to prevent one process accessing memory of another process?
4. [Context-Switching] What is context switching?
	- What happens during a context switch?
	- If a process was running on core 0 is switched out and scheduled on core 1, what happens to the data it had on core 0? Will it cause any functional issues?
5. What's the difference between threads and processes?
	- When would you create threads vs. processes?
	- What's shared and not shared across threads of the same process?
	- What's shared and not shared across multiple processes?

### Exercises:

### Recommended Reading


## Memory Management

Topics: Virtual Memory, Paging, Address Space, Reserved vs. Committed memory, Swap Space

### Basics

1. [Out of Memory] What happens under the hood when you get an out-of-memory exception?
	- Can increasing your RAM (primary memory) overcome the out-of-memory exception?
	- Can killing other processes temporarily help you fix the out-of-memory exception?
2. If I have a 32-bit process, what's the maximum memory I can allocate for the process?
	- What's the maximum on a 64-bit process?
	- Can I allocate an array of 3.5 GB on a 32-bit process? Assuming I haven't allocated anything on this process yet?
		- If not, why? What's the maximum I can allocate on a Windows machine? What about Linux?    
3. If I have a machine with 1 GB RAM, can I allocate more than 1 GB in the process?
4. If I allocate a 10 MB array on a typical windows machine, how is the array placed on the primary memory?
	- If it is contiguous, what happens when there's enough space in the RAM but no contiguous space for the 10 MB array?
	- If it is not contiguous, i.e. placed in chunks, how does the system figure out which chunk a memory access like arr[i] should fetch?
	- Does the physical page have to be contiguous?
5. If I allocate a pointer p with 4 bytes of allocation at location 0x100 of process P1, what's preventing another process P2 from accessing location 0x100 and read the values of P1?
6. How does the operating system allocate stack space for a new thread?

#### Memory layout
1. What happens when memory is misaligned?
1. What is the size of this struct?
	```
	struct
	{
		int a;
		int b;
		char c;
	}
	```
1. How much space would this take? What is the object layout?
	```
	class Base
	{
		int x;
		char c;
	}

	class Derived::public Base
	{
		int p;
		int q;
	}
	```

1. Can you do this?
	```
	foo(Base b)
	{ ... }

	Derived d;
	foo(d);
	```

1. Can you construct a base class object from a derived class object?
1. What is the size of D? What is the object layout? 
	```
    class A {int a, int b} 
    class B: public A {int c, int d} 
    class C: public A {int e, int f} 
    class D: public B, C {int p, int q}
	```

1. What does aptr point to in the above object? (d is the object of class D)
	```
	A* aptr = static_cast<A*>(d)
	```

1. What does aptr->a give?
1. What does bptr point to? 
	```
    B* bptr = static_cast<B*>(d)
	```

1. What does cptr point to? 
	```
    C* cptr = static_cast<C*>(d)
	```

1. What about when we have: 
	```
    void *v = static_cast<void*>(d); 
    C* cptr = static_cast<C*>(v);
	```
1. Can I do this?
	```
	Base *b;
	B = static_cast<Base*>(d);
	```

1. Why do we need virtual functions?
1. What would be the code generated for the last two lines?
	```
	class Base
	{ foo() { print("Base"); } }

	class Derived
	{ foo() { print("Derived"); } }

	Base b;
	Derived d;

	b.foo();
	d.foo();
	```

1. What is the code generated for the last line of code?
	```
	class Base
	{ virtual foo() { print("Base"); } }

	class Derived
	{ virtual foo() override { print("Derived"); } }

	Base *bptr = &d;

	bptr->foo();
	```

1. In the above question, how does bptr know that it's an object of derived class?
1. Is there one vtable per class or per object instance?
1. When is the object layout created and when is the actual vtable created?
1. How does the compiler know about private vs public virtual functions?
1. What gets printed when the following code is run?
	```
	class B
	{
		B() { foo(); }
	public:
		virtual void foo() { print("B foo"); }
	}

	class D
	{
		D() { foo(); }
	private:
		virtual void foo() { print("D foo"); }
	}

	Base *b = new D();
	b->foo(); // What gets printed here?
	```

1. What are all the steps that happen when you construct a derived object?
1. If we define only one of the following, do the other ones get automatically generated by the compiler?
	- ctor
	- dtor
	- copy ctor
	- assignment
1. What is the rule of 3 and the rule of 5?
1. Does the compiler give an error if we define only one of the 3 (see rule of 3)?
1. Write an assignment operator and a user-defined operator.
1. What is the difference between the following pieces of code? Which one of them is preferred?
	```
	B::B():name(" ") { }
	```

	```
	B::B() { name = " "; }
	```

1. Can you have virtual constructors and virtual destructors?
1. Which destructor gets called here when `b` is deleted?
	- Why?
	- What is the code generated for `delete b;`?
	- Is this compile-time binding or run-time binding?
	- If the destructor in Base was also virtual, what would be the code generated for `delete b;`?
	```
	class Base
	{
		~Base() { ... }
	}

	class Derived: public Base
	{
		virtual ~Derived() { ... }
	}

	main()
	{
		Base *b = new Derived();
		delete b;
	}
	```
1. What is compile-ime binding and run-time binding?
1. Is this compile-time binding?
	```
	const B &bref = *b;
	bref.foo();
	```
1. Can I get the address of a reference? Is it equal to the address of the object it refers to?
1. There is no private/public at runtime. How are they distinguished?
1. What happens to the object layout when we have private inheritance?
	```
	class D
	{
		int x;
	private:
		int y;
	}
	```

1. In the above example, would this work even if the second int is private?
	```
	D d;
	int *p = reinterpret_cast<int*>(&d);
	*p = 1;
	*(p+1) = 42;
	```

1. What are the checks that the compiler does for generating code for a function call?
1. Write C++ in C:
	- Virtual functions
	- Overload resolution

### Intermediate

#### Virtual Memory, Paging, Swap Space

1. What is virtualization of memory (virtual memory)?
   - Why is it necessary to virtualize memory?
   - How does virtualization help with security of data across processes? Answer question 5 in memory basics above.
   - Does virtualization help reduce the implications of limited RAM? [Swap space]
2. [Fragmentation] What is memory fragmentation?
	- How does virtualization help with fragmentation?
3. [Address Space] What's an address space?
	- What's the size of address space for a 32-bit process? 64-bit process?
	- Is the address space of a process contiguous?
	- Does the address space always start from 0?
	- Is the address space private to a process?     
	- What's a kernel address space and a user address space? Why is this needed?
		- What gets allocated in the kernel space vs. user space?
		- When can a process access user space? When can it access kernel space?
		- What is the difference between user mode and kernel mode?
	- What's the difference between virtual address and a physical address?
	- Can a process ever issue loads/stores to a physical address?
4. [Implementation]
	- How is a virtual address converted to a physical address?
	- What are page tables? Why do you need them?
		- Is there a page table per process or is there one system-wide page table?
		- Can you brief the pros and cons of major page table implementations - radix, inverted?
		- Does each process carry its own page table?
	- Where are the page tables stored?
		- Is it part of the user space?
		- Can a process ever access a page table directly?
		- What are the hardware support mechanisms for speeding up page table walks?
			- How do these mechanisms work during a process context switch? 
		- Where is the page table stored? How/when is it brought into main memory?
4. What's the concept of reserved vs. committed memory?
	- What are page faults?
	- How does the OS handle page faults?
	- What are the different reasons a page can fault?
	- Can you access invalid memory access violation using page fault?
	- When the OS "fetches" from the hard disk on a page fault, how does it get the coressponding disk address for a given virtual address?
5. [Swap Space] What's a swap space?
	- Why is it needed? Where is it situated?
	- How does the OS know that a page is in a swap space?
	- [Windows] What's the working set of a process? Does it show the total memory taken up by a process?
	- Exercise: Open the SysInternal VMMap and check out the memory allocation of a process?
		- Allocate a few thousand byte sized allocations and delete them. What part of the memory grows? Does it always shrink after deallocation?
6. Answer the basic programming questions (single and multi-process) now that you know about virtual memory.
7. What exactly is a memory leak?
   - Is it a memory leak if you don't delete an allocation when the program is being shutdown?
   - Describe how a memory leak in the heap segment can affect a running process.
   - What happens to the physical pages allocated to the process if the process crashes?
8. How can virtual memory contribute to improving the performance of I/O operations?
1. How is a stack overflow detected?
	- When we usually write past an allocated memory of data, we are likely to cause memory corruptions, but how is stack overflow specifically detected as opposed to memory corruptions that go undetected?
9. What mechanisms do operating systems use to prevent stack overflow?
10. What is the difference between paging and segmenting?
11. Why can't we access a memory location outside the address space of a process? Who is stopping us from doing so?
12. What is wrong with the concept of 1-1 memory mapping from virtual memory to physical memory?
13. How do you split a segment across pages? Or how do you split the process across the virtual address space? Are the pages contiguously allocated in the address space or are they random?
14. If there's a 1GB virtual page, does this 1GB have to be contiguous in the physical memory?
15. If an array allocated spans more than a page, would the pages be contiguous in the address space?
16. What are the types of memory access violations?
How does the operating system manage segment resizing and dynamic memory allocation within segments?
17. Can page size and physical frame size be different?
18. TLB has about 32 entries while page table could have 10^6 entries. How is this ever helpful with this kind of a ratio? 
	- Same question for cache. The L1 cache holds about 32 KB, while DRAM has 64 GB, how does such a small cache even help with speedup?
19. What happens to the TLB at context switch?
	- TLB shootdown
	- ABID (Address Base Identifier) / ASID (Address Space Identifier)
20. In what scenarios does a page fault occur?
21. How is a page fault handled? (For all scenarios in the previous question)
22. If I allocate more memory in a process, do the number of virtual pages increase or would RAM increase? Or both?
23. What is the working set memory of a process?

  
Sharing DLLs, memory mapping, working set      

Rough: TLB, Shootdown, Context Switch, ASID? [Move to architecture]

## Compile, Link and Load

Consider the following the program split into three components. The main program contains the main() function, that calls a foo() in a static library and bar in a dynamic library. 

```C++
// main program -- main.cpp
#include <iostream>
int foo(int);
void bar(a);
void zee(int y) {
	foo(y);
	bar();
}
int main(int argc, char *argv[]) {
	int a = 10;
	foo(a);
	bar(a);
	std::cout << a << std::endl;
}
// -- static library static.lib --
void foo(int x) {
	// do something with x
}
// -- dynamic library dyn.dll --
void bar(int y) {
	// do something
}
// Compile the program as g++ -o main.exe main.cpp -lstatic -ldyn
```
1. When I compile main.cpp, a main.o object file is produced
	- What all does main.o contain?
	- What functions does main.o contain? Does it contain foo()? Does it contain bar()?
	- What's the granularity at which the compiler operates? Or what are compilation units?
	- What are the steps in compiling this program to main.exe
	- What does the compiler do when it sees a header file include?
	- Would the compile of main.cpp fail if the static library didn't have the definition of foo()?
	- How is main() linked to foo()?
		- Is the parameter passed to foo() the same way a simple function call happens?
		- How many copies of foo() are there in the main.exe?
		- How many copies of foo() are there i the main program after it it loaded?
	- How is main() linked to bar()?
		- Answer the same questions as foo()
2. What's the difference between compile and link?
	- Can you get a link error and compile error in the same build?
1. Do we actually need a linker or is a compiler enough?
3. What is a static library?
	- Why would one write a static library?
	- Are there any disadvantages by using a static library? Think in terms of maintanability, sharing, memory, etc.
	- What all does a static library contain?
	- Can you run a static library as a program by itself? If not, what's missing?
	- Can you see all the static libraries loaded in a program if you attach a debugger?
	- When a linker sees a static library, can it see all the functions inside a static library?
	- Can there be multiple copies of the same static library in a given process?
		- If there's a global in the static library, will there be copies of the global too?
		- In the above example, if the static library was present two times in the process, how does main know which foo to call?
	- Can you link to static libraries compiled by a different compiler?
	- Why not directly use source files instead of a static lib, since the static lib is anyway a zip of .o files of its source files?
4. What is a dynamic library?
	- Think of the same questions as the static library.
	- When is a dynamic library loaded in memory? Are there multiple ways to load a dynamic library?
	- Are DLL sections contiguous in the virtual address space?
	- Can you call any function that's present inside a dynamic library?
	- Can you modify/rebuild a DLL that's loaded in a running process?
	- What does the callstack for a call to a dll look like?
	- Can you call DLLs that are built by a different compiler?
	- Can a DLL function take a std::string as a parameter? Or for that sake, a bool or a struct? Justify.
	- How does the processor get the address of the DLL loaded by a process?
	- If two or more processes attempt to load the same DLL, what happens?
	- If a process has loaded about a 100 DLLs, how does it keep track of all of these?
	- Does this compile?
		```
		main.cpp
		foo();

		DLL
		int foo(int);
		```
	- What exactly does extern "C" do?

5. How do distributed builds work?
	- Does the compile job gets distributed? If yes, how does the compiler on another machine get the header files for this machine?
	- Does the linker job gets distributed across machines? If yes, how does it work?
	- Why do you sometimes see an out-of-memory during the link stage of the compilation process?
6. How does incremental link work?
7. Classes defined in C++ get converted to C this way. If I make A(int) private, how does the compiler know?

	__Source code__
	```
	class A
	{
		A() {}
		A(int) {}
	private:
		int x;
		int y;
	}
	```

	__Generated code__
	```
	struct
	{
		int x
		int y

		A_A1(A* this)
		A_A2(A* this, int)
	}
	```
8. Should this compile? Or does it compile and give a run-time error?
	```
	class A
	{
		A::A() {foo()}

	public:
		virtual void foo() { print("A") } 
	}

	class B : A
	{
		B:::B() {foo()}

	private:
		virtual void foo() override { print("B") }
	}

	int main()
	{
		A* aptr = new B();
		aptr->foo();
	}
	```

	Alternatively,

	```
	A* getFactory()
	{
		if (day == "Sunday")
			return new B();
		else
			return new A();
	}

	int main()
	{

		A* aptr = getFactory();
		aptr->foo();
	}
	```

9. The following code works in C, and not in C++. Why? How?
	```
	// -- Main.cpp --

	int foo(int a, int b);

	int main()
	{
	  int x = foo(10, 20);
	  cout << x;
	}

	// -- helper.cpp --

	void foo(int a, int b)
	{
	  // do something with a and b
	  cout << a << b;
	}
	```
[Compiler]

1. What happens if we have multiple forward declarations?
1. What happens if we have multiple definitions? 
1. What is the difference/recommendation between #pragma once and #ifndef...#define...#endif header guards?

[Linker]

1. How does a linker resolve function addresses when we have function overloading?
1. 
1. 

[Functions]
1. Which of these overloads gets called?
	```
	EXE
	foo(x)

	DLL
	int foo(int) { ... }
	int foo(int, int) { ... }
	```
1. What is the code generated for these?
	- int foo(double x) { ... }
	- int foo(int a) { ... }
	- int foo(int, int) { ... }
	- int main() { int x = foo(2); }

[User-defined conversions]
1. What is operator overloading?
1. What are user-defined conversions?

[Casting]
1. Can I convert doublt to int? Does it throw warning/error?
	- What happens with C-style cast vs static_cast?
1. Can I convert int* to int?
1. Why do we need static_cast?
1. Can I convert Derived* to Base*?
1. Can I convert Base* to Derived*?
1. How do you legally convert C to B? Is there a chain of casts to do it?
1. Does dynamic_cast work on non-polymorphic types? Why?
1. How does dynamic_cast work?
1. Does void* work with dynamic_cast?
	- How do we know if each void* object has a vtable?
1. What is you static_cast an object to void* and then use dynamic_cast to some derived object type? Would it work? Would it be able to get the vtable?
1. What is the output of this program?
	```
	const int x = 10;
	int *p = const_cast<int*>(&x);
	std::cout << x << *p << std::endl;
	*p = 20;
	std::cout << x << *p << std::endl;
	```
1. What is the output of this program?
	```
	const char* str = "Hello";
	char *x = const_cast<char*>(str);
	std::cout << x[4];
	x[4] = 'p';
	std::cout << x[4];
	```
1. What is the difference between volatile and regular variables?
1. Can I do this?
	```
	const int* p = new const int[100];
	delete[] p;
	p = nullptr;
	```
1. Can I do this?
	```
	int* const p = new const int[100];
	delete[] p;
	p = nullptr;
	```
1. What is the difference between nullptr and NULL?

Intermediate:

1. Relocation, patching, delay load
   
	
## Debugging

1. For what reasons would a program crash?
2. How can a debugger see values of the other program? Isn't it a violation of the security?
1. How exactly does the debugger get this "special privilege" to ask the OS to reveal data pertaining to another process? 
	- Can I write my own debugger and ask the OS to go read some other process data for me? 
3. How do breakpoints work? If you'd like, take a specific example. Like how does a visual studio breakpoint work?
4. When a breakpoint is hit, we see a call stack. How does the debugger get the callstack?
5. When can you trust callstacks? Can a callstack ever be corrupted?
	- If yes, what are the reasons a debugger might be lying about the callstack? 
7. What are symbol files? How do they work? Is there a difference between the symbol files on MSVC vs. gcc?
	- What are symbol servers? Why do you need to set one up? How do you populate one?
8. How do you debug memory leaks?
	- How do you identify that there's a leak?
	- How do you fix the exact leak? And how do you verify that the leak is fixed?
9. How do you debug a memory corruption to the code space of the process?
10. What's a segmentation fault? Who is responsible for checking it? Why is it called so (reveals a lot of useful history :))
11. What's a memory corruption? Shouldn't the OS complain about writing to a memory beyond bounds? Do you remember seeing access violation exceptions? Why don't you see these during memory corruptions?
	- How does one find a memory corruption?
12. What's the difference between release and debug binaries? Can you debug a release binary?
13. Does copying debug binaries to a clean VM with the product installed work? Why?
14. When can you say with confidence that an intermittently appearing bug/crash is fixed?
15. What are data breakpoints? How do they work internally?
16. Can you execute functions in the watch window?
	- If yes, which thread are they executed? What happens when there's an exception or a crash in the function called by the watch window?
17. How does a debugger access another program's memory? For e.g., visual studio debugger when attached to helloworld.
	- How is this process able to read the variables of the other program? Isn't it security violation?
	- Also, each variable in the helloworld has a virtual address. How is this translated by the debugger to the helloworld's physical address? Does it access to the program's page tables?
	  - Is the hardware page walker involved in this conversion?
	- Does the watch window work in the same way?
18. In what situations does staring at the code without blinking reveal the bug?
19. In what situations does repeatedly running the same experiment without any changes reveal the bug?
20. What are memory fill patterns?
21. If a debugger actually overwrites the binary while placing breakpoints, how does it work when there are two instances of the same process running? Why would the second instance that is not being debugged not pause at the breakpoint?


Bugs to add: access violation, race condition, reinterpret cast to larger storage space pointer, 

## Pointer Arithmetic

1. Is there anything wrong with the code below?

```c++

struct ParamInfo
{
	char* name;
	char* type;
};

void FillParamInfo(ParamInfo *info)
{
	info = new ParamInfo();
	info->name = "Hello";
	info->type = "World";
}

int main()
{
	ParamInfo *info = nullptr;
	FillParamInfo(info);
	std::cout << info->name << " " << info->type << std::endl;
	return 0;
}
```
- Trace the code in terms of the following
  - Where are the pointers info located?
  - Where does new allocate memory for info, name and type
  - How is the info passed on the stack
  - Free?
  - Where are the "Hello" and "World" strings located?
	- Can I delete the pointer to the "Hello" string using delete info->name?

2. Different datatype pointer increments
3. reinterpret_cast a intptr_t pointer to a int32 pointer?
4. 

# C++


---

Rough Topics:

static vs dynamic lib, load vs link time, val vs. ref passing, c++ ref, lvalue and rvalue, c++ constr and destr, virtual functions, vtables, pointer artihmetic, vectors across DLL boundaries, interop,
