
The following is a list of questions aimed to test the understanding of basics of c++ required for every day application development. The questions are tagged with relevant topics that will provide answers. Some questions might seem absurd to someone who understands the fundamentals of the area, but it's designed to force the developers to test their understanding of the fundamentals.

# Objects and Layout

## Introduction

1. Consider the following code snippet:

    ```cpp
    class Base {
    public:
        int a;
        char b;
        double c;

        int add(int a, int b) { return a + b; }
    };
    ```

    - What's the size of the object in memory? 
      - Is the always the cumulative size of the data members?
      - Can it be more?
    - What's the size of an object of an empty class?
    - Is the object layout always the same across different compilers?
      - What about different versions of the same compiler?
    - Can I safely send a struct across DLL boundaries? If not, why?
      - What about static library boundaries?
    - Does the add() function take up any space?
  
2. Consider the derived class below.

    ```cpp
    class Derived : public Base {
    public:
        int d;
        char e;
        double f;
    };
    ```

    - What's the size of the object in memory?
      - Is it the cumulative size of the data members?
      - Where is the information about the inheritance relationship stored 'in the object'? How much space does it take?
  
3. What's the difference between a struct and a class in C++?
    - Are there any differences in the way they are laid out in memory?
4. Consider the above 'Base' class
   - 
    
## Intermediate

1. [Padding] Why is padding required? 
    - Who decides the padding layout?
    - Can padding be avoided?
      - In what scenarios would you want to avoid padding?
      - How does one avoid padding?
    - What happens if members are not padded? What are the consequences? Do all machines allow unalgined access?
      - What are the performance implications?
      - Is it just the performance that is affected?

2. Consider the following code snipped (diamond hierarchy):
    
    ```cpp
    class A {
    public:
        int a;
    };

    class B : public A {
    public:
        int b;
    };

    class C : public A {
    public:
        int c;
    };

    class D : public B, public C {
    public:
        int d;
    };
    ```
    - What's the size of the object of D in memory?
    - How many copies of A are there in the object of D?
    - How is the layout of the object in memory?
    - How is the layout of the object in memory different from the layout of the object of B or C?
    - Can I pass a pointer to an object of D to a function that expects a pointer to an object of A?
      - Can I pass a reference to an object of D to a function that expects a pointer to an object of B or C?
      - 

3. **Object Layout**
    - **Object Layout**: The layout of an object in memory is defined by the compiler. The layout of an object is determined by the compiler and is not specified by the C++ standard. The layout of an object is compiler dependent.
    - **Object Size**: The size of an object is compiler dependent. The size of an object is determined by the compiler and is not specified by the C++ standard.
    - **Empty Class**: An empty class has a size of 1 byte. An empty class is a class that has no data members.
    - **Padding**: The compiler may add padding to an object to ensure that the object is properly aligned in memory. Padding is compiler dependent.
    - **Alignment**: The alignment of an object is compiler dependent. The alignment of an object is determined by the compiler and is not specified by the C++ standard.
    - **Inheritance**: The layout of an object in memory is determined by the compiler. The layout of an object is compiler dependent. The layout of an object is determined by the compiler and is not specified by the C++ standard.
    - **Object Slicing**: Object slicing occurs when a derived class object is assigned to a base class object. Object slicing occurs when the derived class object is copied to the base class object, and the derived class data members are sliced off.
    - **Virtual Memory**: Virtual memory is a memory management technique that provides an abstraction of the physical memory. Virtual memory allows the operating system to manage the memory more efficiently.
    - **Virtual Table**: A virtual table is a table of function pointers that is used to implement dynamic dispatch in C++. A virtual table is used to implement polymorphism in C++.
    - **Virtual Pointer**: A virtual pointer is a pointer that points to the virtual table of an object. A virtual pointer is used to implement dynamic dispatch in C++.
    - **RTTI**: Run-time type information (RTTI) is a mechanism that allows the type of an object to be determined at run-time. RTTI is used to implement dynamic_cast and typeid in C++.


Rough Book

Object layout (padding), constructors and destructors, polymorphism (overloaded function picking) inheritance rules, object slicing, virtual memory, exception (unwinding, catch by const reference), overriding, size of empty class, vtable, vptr, RTTI, typeid, dynamic_cast, static_cast, const_cast, reinterpret_cast, placement new, new/delete, malloc/free, new[]/delete[], operator new/delete, operator new[]/delete[], operator overloading, copy constructor, copy assignment operator, move constructor, move assignment operator, copy and swap idiom, RAII, smart pointers, shared_ptr, unique_ptr, weak_ptr, auto_ptr, enable_shared_from_this, deletion of pointers inside a contained structure (TypeInfo .net inteface)