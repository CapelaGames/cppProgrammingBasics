## What is C++
- C++ is a programming language that focuses on run speed & functionality
- C++ is a compiled language
- C++ is a mid-level programming languge
    - High level = Python
    - Low level = Assembly

## Advantages of C++
- Very widely used / supported
- Many libraries available
- Resulting code can be very fast
- Syntax is similar to Java/C#
- Jobs
- Code is highly customizable
- C++ will be around for a long time

## Disadvantages of C++
- Easy to write unsafe code / crashes
- Must manage your own memory
(RAII will save us from these downsides)
- Syntax can be a little confusing
- Can be hard to read others' code due to custom definitions / op overloading
- Compiler/linker errors can be hard to interpert 

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
