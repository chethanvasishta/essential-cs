These are the topics we touched upon during discussions that require extra reading

1. Base and bound registers

1. CPU Privileges

1. Super fetch

1. Thread over-subscription

1. C++ references

1. Move semantics

1. Return value optimization

1. Realloc tables

1. Thunk

1. Trampoline

1. Address Space Layout Randomization – prevents vulnerabilities that can be exploited with the process's preferred base address

1. Debugger - ptrace

1. Translation units

1. [Mixing malloc and delete](https://isocpp.org/wiki/faq/freestore-mgmt#mixing-malloc-and-delete)

1. [Detect buffer overflows with canaries](https://manybutfinite.com/post/epilogues-canaries-buffer-overflows/)

1. [How the stack works](https://manybutfinite.com/post/journey-to-the-stack/)

1. [DEADBEEF and other memory fill patterns](https://stackoverflow.com/questions/127386/what-are-the-debug-memory-fill-patterns-in-visual-studio-c-and-windows)

1. [Linkers and loaders – Eli Bendersky](https://eli.thegreenplace.net/tag/linkers-and-loaders)

1. [Illegally access deallocated memory](https://stackoverflow.com/questions/6441218/can-a-local-variables-memory-be-accessed-outside-its-scope?noredirect=1&lq=1)

1. [Distributed build strategies](https://moderncppdevops.com/2024/06/24/distributing-builds/ )

1. [Protection against stack smashing with random guard values](https://www.redhat.com/en/blog/security-technologies-stack-smashing-protection-stackguard#:~:text=Limitations%20of%20StackGuard%3A&text=This%20would%20allow%20an%20attacker,prevent%20heap%2Dbased%20buffer%20overflows.)

1. [glibc heap implementation](https://azeria-labs.com/heap-exploitation-part-1-understanding-the-glibc-heap-implementation/)

1. [How debuggers work](http://www.alexonlinux.com/how-debugger-works)

1. Super pages

1. Radix page table

1. Streaming algorithms can't efficiently use the locality assumptions of the cache. How does it optimize?

1. Kmalloc

1. Related to page fault

1. - Swap
1. - Access violation
1. - Committed vs reserved memory

1. Data breakpoints

1. Memory leaks

1. mmap

1. Shared memory

1. DLL/code sharing

1. Alloc buckets

1. Debuggers

1. virtual_protect()

1. Stack watcher in the C run time

1. Guard bytes
	- Canaries: https://manybutfinite.com/post/epilogues-canaries-buffer-overflows/

1. System calls for virtual_alloc() and valloc()

1. Application Binary Interface (ABI)

1. Region based allocators 

1. [HOARD](https://dl.acm.org/doi/pdf/10.1145/378995.379232)

1. [What every programmer should know about memory](https://people.freebsd.org/~lstewart/articles/cpumemory.pdf)

1. Stack smashing

1. Symbol files

1. int3

1. PDB checksum

1. Endianness

1. Fast stack walk

1. Precise stack

1. Alignment and padding

1. Natural word size

1. #pragma pack
	- Pack1
	- Pack2

1. Loading and patching DLLs

1. Import Address Table of DLLs

1. Dllmain

1. Loader lock

1. Decoration on DLL names

1. User-defined conversions 

1. RTTI 

1. std::type_info
