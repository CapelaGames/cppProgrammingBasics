## What is C++
- C++ is a programming language that focuses on run speed & functionality
- C++ is a compiled language
- C++ is a mid-level programming languge
    - High level = Python
    - Low level = Assembly

### Advantages of C++
- Very widely used / supported
- Many libraries available
- Resulting code can be very fast
- Syntax is similar to Java/C#
- Jobs
- Code is highly customizable
- C++ will be around for a long time

### Disadvantages of C++
- Easy to write unsafe code / crashes
- Must manage your own memory
(RAII will save us from these downsides)
- Syntax can be a little confusing
- Can be hard to read others' code due to custom definitions / op overloading
- Compiler/linker errors can be hard to interpert 

### In browser tutorial
[cplusplus turoial (code in browser)](https://cplusplus.com/doc/tutorial/)


## Hello world

```
#include <iostream>

int main(int argc, char * argv[])
{
    std::cout << "Hello, world!\n";
    return 0;
}
```
If your using something like Unity or Unreal to program you might not realise that when programs runs, your system calls your "main" function is what gets called. When your main function exits, your program exits. In c++ the main function can return an int, this is used to check for errors. 0 means no errors.
std is a namespace
<p>
<< operator 'pipes' the string to cout
<p>
While we are not going to use these, its good to know: \
int argc and char * argv[] are there to handle "command-line arguments".

When running a program you might run in in command line/ CMD/ bash like this.

```
make-toast
```
But you can also pass values to the program like this 

```
make-toast 2 medium
```
argc is the count of how many arguments there are \
argv is an array with those values
<p>

## Program Code and Header files

C++ is usually splits classes into two files, 
- A program code file (normally with the extension .cpp) These is where your functions will exist (Called the implementation)
- A header file (normally with .h) this is use for function and class declarations (More on this later)

### Declaration:
Notice the semicolon at the end. This is telling the compiler that this function exists somewhere. Kind of like a placeholder.
```
int sum (int x, int y);
```
### Definition:
A normal looking function, what it actually does / its actually implemented.
```
int sum (int x, int y)
{
    return x + y;
}
```

But why? \
C++ Requires you to declare all classes functions and variables before use. If you look at your code from top to bottom, if you use a function, it must have been declared or defined it literally above it.

C++ compiler is dumb, it goes from top to bottom, without going backwards to fill gaps in its knowledge
```
void function()
{
    FooClass class;
    class.anotherFunction();
}

// you can not define "FooClass" here, because function() won't see it

```

So using things like headers we can include definitions for our classes before we use it.
```
#include "FooClass.h"

void function()
{
    FooClass class;
    class.anotherFunction();
}
```

You can think of #include literally copying all of FooClass.h, and pasting it above. At the end of the ""Preprocessing" stage, you end up with 1 big file.

### Compilation Process
[look at graph](./img/GCC_CompilationProcess.png)


But why is it good? \

You can see the whole class at a glance.

Separates design from implementation / functionality

When is it bad? \

More going back and forth between .h and .cpp files

Cyclic dependencies (includes) can be hard to deal with.

## Classes

Class syntax
```
// This would be in the .h file
class Example
{
    int m_x = 0; //private by default
    int m_y = 0; 
public:
    int count;
    Example(int x, int y);
    ~Example();
    AFunction(int x);
    int getY();
};
// Don't for that ;
```


```
// This would be in the .cpp file
// Notice the Class name before the function name
Example::AFunction(int x)
{
    m_x = x;
    m_y = x * 5;
}
```

```
// Constructor
Example::Example()
{
    // Set up the class
}

// Destructor
Example:~Example()
{
    // clean-up here
}
```

## Standard Template Library (STL)

CPP provides a standard library which includes a of things you would expect CPP to have. \
Most Commonly: \
- std::vector<T> - vector of type T
In C# this would be a List<T>, confusignly not a vector 
(T must have a default constructor)
- std::set<T> - ordered set
(T must have a < operator defined)
In C# this would be a Dictionary (more accurately an OrderedDictionary)
- std::map<T1,T2> - map from T1 to T2 



## Basic Variables

int
float
bool - bools are 0 and 1
char - a character (single letter of a string)
std::string (an array of chars - char[])

using namespace std;


#include <vector>
std::vector<T> 

Note if you go out of bounds with a vector, it will just return what random data was there.


if you just use int to loop through you will get an error.

So use size_t instead. It changes size depending on which system your using it on. 


```
#include <vector>
#include <iostream>

int main(int argc, char * argv[])
{
    std::vector<int> vec;
    vec.push_back(42);
    vec.push_back(10);
    vec.push_back(11);

    for (size_t i=0; i < vec.size() ; i++)
    {
	std::cout << vec[i] << "\n";
    }

    for (auto& a : vec)
    {
	std::cout << a << "\n";
    }

    return 0;
}

```

### Class (without const correctness)

```
#include <vector>
#include <iostream>

class Student
{
    std::string m_first = "First";
    std::string m_last = "Last";
    int m_id = 0;
    float m_avg = 0;

public:

    Student() {}

    Student(std::string first, std::string, int id, float avg)
	: m_first (first)
	, m_last (last)
	, m_id (id)
	, n_avg (avg)
    {
    }

    int getAvg()
    {
	return m_avg;
    }

    int getID()
    {
	return m_id;
    }

    std::string getFirst()
    {
	return m_first;
    }

    std::string getLast()
    {
	return m_last;
    }

    void print() 
    {
	std::cout << m_first << " " << m_last << " ";
	std::cout << m_id << " " << m_avg << "\n";
    }
};

int main(int argc, char * argv[])
{
    Student s1;
    Student s2("Andrew", "Capela", 1, 3.14);
    Student s3("Jane", "Doe", 2022, 99.9);

    std::cout << s3.getLast() << "\n";

    s3.print();

    return 0;
}

```


### const correctness


```
#include <vector>
#include <iostream>

class Student
{
    std::string m_first = "First";
    std::string m_last = "Last";
    int m_id = 0;
    float m_avg = 0;

public:

    Student() {}

    Student(std::string first, std::string, int id, float avg)
	: m_first (first)
	, m_last (last)
	, m_id (id)
	, n_avg (avg)
    {
    }

    int getAvg() const
    {
	return m_avg;
    }

    int getID() const
    {
	return m_id;
    }

    std::string getFirst() const
    {
	return m_first;
    }

    std::string getLast() const
    {
	return m_last;
    }

    void print() const
    {
	std::cout << m_first << " " << m_last << " ";
	std::cout << m_id << " " << m_avg << "\n";
    }
};


int main(int argc, char * argv[])
{
    Student s1;
    Student s2("Andrew", "Capela", 1, 3.14);
    Student s3("Jane", "Doe", 2022, 99.9);

    std::cout << s3.getLast() << "\n";

    s3.print();

    return 0;
}

```


### Pass as reference

```
 
...

class Course
{
    std::string m_name = "Course";
    std::vector<Student> m_students;

public:
    Course() {}

    Couse(const std::string& name)
	: m_name(name)
    {
    }
}

...

```



### Using the class 

```
 
...

class Course
{
    std::string m_name = "Course";
    std::vector<Student> m_students;

public:
    Course() {}

    Couse(const std::string& name)
	: m_name(name)
    {
    }

    void addStudent(const Student& s)
    {
	m_students.push_back(s);
    }

    const std::vector<Student>& getStudents() const
    {
	return m_students;
    }

    void print() const
    {
	for (const auto& s : m_students)
	{
	    s.print();
	}
    }
}

int main(int argc, char * argv[])
{
    Student s1;
    Student s2("Andrew", "Capela", 1, 3.14);
    Student s3("Jane", "Doe", 2022, 99.9);

    Course XLD("XLD");
    XLD.addStudent(s1);
    XLD.addStudent(s2);
    XLD.addStudent(s3);
    XLD.addStudent(Studentt("Billy", "Bob", 3, 50.0));

    return 0;
}

```

### Loading from file

```
#include<fstream>

...

void loadFromFile(const std::string& filename)
{
    std::ifstream fin(filename); 
    std::string first, last;
    int id;
    float avg;

    while (fin >> first)
    {
	fin >> last >> id >> avg;

	addStudent(Student(first, last, id, avg));
    }

    
    
}

...

```

file to read
```

```



### Memory Management

There are two types of memory to store data.

Main differences are,
- The size of aviable memory
- The way memory is found/allocated
- The speed of the memory allocation
- The way we request memory in our code
- Stack memory dellocated when leaves scope

```
int main()
{
    int val = 5;	    // stack
    int* hval = new int;    // heap
    *hval = 5;

    int a[5];		    // stack
    int* ha = new int[5];   // heap
    ha[3] = 10;

    MyClass c(args);	    // stack
    MyClass * hc = new MyClass(args) // heap
}
```

#### Stack Memory
- Has predefined size (few megabytes)
- Very easy to run out of stack memory (stack overflow)
- Local variables (without 'new') are allocated on the stack by default
- Program function calls / return addresses are also allocated on the stack
- They get deallocated automatically when they leave scope
- Stack memory is a stack


#### Heap Memory
- Much more space avaiable than stack
- Allocation via the 'new' keyword
- OS finds a contiguous chunch of memory and returns a pointer to it
    - This is very complicated and expensive
- In c++ we can access it again via a pointer

```
int main()
{
    int i = 6;
    int j = 10;
    MyClass* p = new MyClass(5,4);
    int arr[2] = {3,4};
    // delete p;
}
```

| Heap                          |
| ------------- | ------------- |
| 0x1           | 5             |
| 0x2           | 4             |
| 0x3           |               |
| 0x4           |               |
| 0x5           |               |

 
| Stack         |
| ------------- |
| 4             |
| 3             |
| 0x1           |
| 10            |
| 6             |


Managing memory can be annoying, if we don't do it correctly we can have memory leaks.

Just remember: 
    - Stack = Fast, Limited
    - Heap = Slow, Larger

### Pointers

Now for the star of the show. Pointers. \

What is a pointer? It stores a memory address! \

If you modify a pointer variable, your changing the address. \

If you want to modify the value of the data, we need to dereference! \

'Raw' pointers can be very unsafe. \
Imagine you had key to a house, but you can just change the address the key unlocks to any address.

```
int main()
{
    int i = 6;	    // local int var
    int* p;	    // pointer to int , this is bad practice
    p = &i;	    // & = 'address of'
    *p = 7;	    // * = 'dereference'
}
```

| Stack				|
| ------------- | ------------- |
| 0x1           |               |
| 0x2           |               |
| 0x3           |               |
| 0x4           | ? -> 0x5      |
| 0x5           | 6 -> 7        |

This can be confusing, the symbols are overloaded for no good reason. They can mean different things in different locations

* can be multiplication, creating a pointer, and deferencing a pointer \
& can be bitwise operator, and operator and address of a pointer \

Luckily, we don't need to do this stuff anymore (even if it can be quite powerful)

### Arrays and pointers

```
int main()
{
    // int arr[3] // static array
    int * arr = new int[3];
    arr[0] = 5;
    arr[1] = 10;
    *(arr+2) = 20;
    // arr[n] == *(arr+n)
    // n[arr] == *(n+arr)
    // (arr+n) == &(arr[n])
}
```


| Heap                          |
| ------------- | ------------- |
| 0x1           | 5             |
| 0x2           | 10            |
| 0x3           | 20            |
| 0x4           |               |
| 0x5           |               |

 
| Stack         |
| ------------- |
|               |
|               |
|               |
|               |
| 0x1           |


This example is really silly. But the important thing to know is arrays, ints and pointers can be the same thing. 🤯 \
In fact, so are bools, and strings, and floats, everything is just binary deep down, it just depends on how you treat it. \

### Why use pointers?

1. Must use pointer for polymorphism 
    - Base * ptr = new Derived();
    - There is something called a reference we can use too
2. Pass by value vs. by reference
    - Modifying variable passed into function
3. Pointing to large data
    - Large data can't live on the stack

### References

Now, pointers are unsafe, so c++ introduced references. References kind of like a 'safe pointers'

Here comes another use of the & symbol.

To make a reference we use a & instead of a *.

A reference must point to existing data, and can never point to nothing/nullptr
    - This makes them (almost) always safe.

We Prefer using references to pointers wherever possible in our code.

### Pass By Value / Reference

By default all variables get passed by VALUE.

Passing by value has a cost when copying large data.

Also we might want to modify values pass to a function.

We can use pointers to pass by reference, but ideally we use references instead.

Note: the difference between a "&" 'reference' and a 'reference to data'

```
void tennify(int a) { a = 10; }

int main()
{
    int i = 12;
    tennify(i);
    std::cout << i << "\n";
}
```
What gets printed out?


```
void tennify(int* a) { a = 10; } 
// careful: pointer may be a null!
// careful: if the address is 0 (called a nullptr)
// careful: if the address needs by accessable by your program!
// careful: is the data sent an int?

int main()
{
    int i = 12;
    tennify(&i);
    std::cout << i << "\n";
}
```
What gets printed out?

```
void tennify(int& a) { a = 10; }
// reference will always* be valid

int main()
{
    int i = 12;
    tennify(i);
    std::cout << i << "\n";
}
```
What gets printed out?


### const reference

Whenever we pass a variable to a function that we don't want to be modified, use a const reference.

const declares that the variable cannot be modified inside the called function.

We only have to pass the 8-byte reference, which may be far less data than the data we are passing into the function.


```
void machineLearn(const BigData & d);


int main()
{
    BigData data(args);
    machineLearn(data);
}

```

#### Exceptions
Pass primitive data types by value.
~~int add(const int & a, const int & b);~~
int add(const int a, const int b);

Reference has an extra 'deference' step which is slower than using primitives. Primitives will be the same size(more or less) than pa pointer/reference anyway.

We havn't talked about this yet, but pass "smart pointers" by value
    - Copy constructor does counter inc/dec

Ensuring you use const correctly is called "const correctness" and is very important.


### RAII

The magic that makes everything okay!

Stands for: Resource Acquisition is Initialisation

Binds the life cycle of a resource that must be acquired before use to the lifetime of an object.
    - What does that mean? How does it help?

Makes life easier by automatically managing memory/resources within an object! 

It's almost like garbage collection without the overhead.


#### Implementation

- Encapsulate each resource into a class.
- The class constructor acquires the resource and initializes it accordingly. 
- The destructor releases the resource.
- The class ifself should be instantiated such that it has either automatic storage duration or in another RAII object.


```
//This is so we can have an int[] that can be on the heap instead of stack
class IntArray
{
    int * array;
public:
    IntArray(size_t size) { array = new int[size];}
    ~IntArray() { delete [] array; }
    int & operator [] (size_t i) { return array[i]; }
}
```


```
# include "IntArray.h"

int main()
{
    IntArray arr(10); // mem allocated
    arr[5] = 21;
    // arr destructs, mem deallocated
}
```

This is much faster than a garbage collected language.

### Smart pointers

But that can be troublesome to do create an RAII class for every data type we want to store a pointer to.

So c++ contains different 'smart pointers'

To start off with, always use std::shared_ptr<T>. At least when it comes to normal c++.

Unreal engine has their own smart pointers.

- TSharedPtr
- TSharedRef
- TWeakPtr
- TUniquePtr

We are not going to look at these now.

C++ smart points are:

- auto_ptr<T>
- shared_ptr<T>
- weak_ptr<T>
- unique_ptr<T>


Smart pointers works pretty much the same way as the IntArray we made above. But they can also do extra things.


Smart points handles RAII for a given pointer / type.


### Shared Pointer

It is a Reference Counted Pointer.


This smart pointer keeps a counter of every class referencing the smart pointer, and only clear memory if there are no references left.

```
#include <memory>

void func(std::shared_ptr<MyClass> p) // counter++ (= 2)
{
    p->doSomething();
    // counter-- (=1)
} 

int main()
{
    // std::shared_ptr<MyClass> p(new MyClass(args)); // old syntax 
    auto p = std::make_shared<MyClass>(); // counter = 1
    someOtherThings();

    // counter-- (= 0), deallocate
}

```


### How to allocate and pass data

After all is said and done, what should I do?

1. If possible, use the stack
    - Small, local variables
    - Pass variables by const reference if size > 8 bytes

2. If you need heap memory, use smart ptr
    - std::shared_ptr<T> myBigData;
    - std::shared_ptr<Base> = std::make_shared<Derived>();

3. Only when ABSOLUTELY NECESSARY use raw pointers / new




```
    int a;
    cout << a << &a;
    cout << sizeof(a);

    void print(int & x) cout<< &x <<x<< sizeof(x);

    int arr[10]; // = {};
    for(size_t i=0; i<10;i++)
	print(i);

   //look at address, 4 bytes away from eachother

    int * harr = new int[10];
    //loop print
    //memory leak

```



```
    int a = 10;
    int b = 25;
    int* pa = &a;
    int* pb = &b;

    //*pa = 17;
    //*(&a) = 17;

    // *(pb) = 17
    // *(pb-1) = 17

    print(a);
    print(b);
    print(pa); // error
    print(&pa);
```



```
//This is so we can have an int[] that can be on the heap instead of stddack
class IntArray
{
    size_t m_size;
    int * m_arr;

public:
    IntArray(size_t size)
	    : m_size (size)
	    , m_arr (new int[size])
    {
	std::cout << "Array Constructor\n";
    }

    int get(size_t index) const
    {
	return m_arr[index];
    }
    
    void set(size_t index, int val)
    {
	m_arr[index] = val;
    }

    void print() cost
    {
	for(size_t i=0;i < m_size; i++)
	{
	    std::cout << i << " " << m_arr[i] << "\n";
	}
    }

    ~IntArray()
    {
	delete [] arr; 
	std::cout << "Array Destructor\n";
    }
    //T & operator [] (size_t i) const { return arr[i]; }
    //const T & operator [] (size_t i) const { return arr[i]; }
}
```


```
# include "IntArray.h"

int main()
{
    IntArray myArray(10); 

    myArray.set(4,7);
    myArray.set(2,134);

    myArray.print();
}
```

```
template <typename T>
class DynamicArray
{
    T * m_arr
    //etc
...


//const DynamicArray<float> myArray(10);
//myArray[3] = 3.14159;
// std::cout << myArray[3] << "\n";
```
