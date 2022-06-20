# Topics 

1. [Introduction to C++]() 
2. [Scope and Namespace]() 
3. [EnuEnumerated Types]() 
4. [Pre Processor Directives]() 
5. [Data Types and Operators]() 
   1. [Numeric Data Types]() 
   2. [The Auto Keyword]() 
   3. [Value vs. Reference]() 
   4. [Constants]() 
   5. [Garbage Values]() 
   6. [I/O Streams]() 
   7. [Operations with different numeric types]() 
   8. [Binary Operations]() 
   9. [Unary Operations]() 
   10. [Comparing and Booleans]() 
   11. [Characters]() 
   12. [The Yoda Syntax]() 
   13. [The Ternary Operator]() 
   14. [The Switch Statement]() 
   15. [The For-Loop]() 
   16. []() 
   17. []() 
   18. []() 
   19. []() 
6. []() 
7. []() 
8. []() 
9. []() 
10. []() 
11. []() 
12. 

# 1. Introduction to C++ 

The `main()` function is the entry point of a program's execution. We can use `#include` to import a library, followed by the name of the library within either angle brackets if the library is in standard libraries, or double quotation marks if the library exists inside the project directory.  

`cout` is an object of the `ostream` class. Functions in this class are used to control the flow of bits to some destination. When we create an instance of `cout`, its destination is fixed as the output console. 
The insertion operator `<<` is the operator we use to push some bits from the memory into an object. 
`endl` is a manipulator we can use to create a new line in the output.  

At first, C++ had no library that shipped with it. It only had the C Runtime Library. Then the STL – Standard Template Library came along. It had a set of headers that offered functionality, collections, data structures and algorithms as templates. That, later grew into be the Standard Library. 
It’s controlled by the standards committee. The current C++ standard library is not necessarily in all headers. The vendors of the compiler can choose how to implement its own library. 
Everything of the standard library is in the std namespace. Those class names start with lower case letters.  

# 2. Scope and Namespace 

The scope resolution operator `::` is used to mention the scope.  

We can use the `using` keyword to declare a namespace. Functionality that comes with the standard library is all in the **std** namespace. Using this functionality, we can implement our version of the standard libraries. 

Take string for an example, we can either use ``std::string`` or we can write our own string class and with that namespace ``mylib::string`` can be used. It’s possible to mix and match them in the same application without any confusion. 

In C++, no words are really preserved, so string is available to name our class. We don’t actually have to mention the namespace each time we use anything from the standard library. We can declare the namespace using the using keyword. Usage of this keyword and mentioning the namespace is just a convenient way to tell the compiler, whenever I’m using cout, I mean ``std::cout``.  

```cpp
int main() {
    std::string word {“World”};
    std::cout << "Hello " << word << std::endl;
    return 0;
}
```
or  
```cpp
using std::cout;
using std::endl;

int main() {
    cout << "Hello world" << endl << "The next line" << endl;
    return 0;
}
```

When we’re using only one namespace or when we’re using a lot of things in the same namespace, we can tell the compiler that we’re using the entire namespace by using `using` keyword and committing to that namespace.  

```cpp
using namespace std;

int main() {
	cout << "Hello world" << endl << "The next line" << endl; 
	return 0;
}
```

If we’re using the entire std namespace like this, we should be careful not to mix our code with anything from the **std** namespace. It’s also strongly discouraged to use the entire **std** namespace in header files. 

# 3. Enums 

In C++, we can create an enum (usually in a header file) using the `enum` keyword, followed by open and close curly braces contained values and a semi-colon. They can contain few possible states (or values) a variable field can get.  
Special thing about C++ enums is that they can be referred only by the value, and without the enum name. So, all the values in a enum have to be unique and cannot be conflicted with values from another enum. 

```cpp
enum Status {
    Approved, Pending, Cancelled 
};

int main () {
    Status s = Pending;
    s = Approved;
    return 0;
}
```

# 4. Pre Processor Directives 

Anything that starts with a `#` is called a pre-processor directive. They are instructions for the compiler usually to combine files together, to include a library or for debugging purposes. We can create debug builds with more output than release builds. We can also use them for convenience, like include guards with `#ifendif`, `#endif` and `#define` that we can use to stop the same library from importing more than once.  

When we create a sub class, and in its definition,  we’ve included the super class, then whenever we’re working with those classes in a separate function, we only need to include the sub class. If we include both, we’ll get a compile time error. We can get around this by adding `#ifendif`, `#define` and `#endif` preprocessor directives in the class header file, so we don’t have to worry about that, the classes themselves will figure it out.  

`#define` keyword is used to define a constant arbitrary. We need to give it the same name as the file name, usually in upper or Camel case pre-fixed with an underscore. That will define the class, but to prevent it from being defined again, we can cover the whole definition with `#ifndef` – ‘if not defined’ and `#endif` pre-processor directives. 
This pattern is called an **include guard**. The name of the include guard must be unique for each class. 

```cpp
#ifndef CLASSNAME_H
#define CLASSNAME_H

class Classname { 
    /* everything*/ 
};

#endif CLASSNAME_H
```

We can also use the `#pragma once`  to tell the compiler to only include this only once. 

# 5. Data Types and Operators 

C++ is a strongly typed language. We must declare the type of a variable in its declaration. 

## 5.1. Numeric Data Types 

There are two main types of integers, signed and unsigned. Signed integers can hold positive and negative numbers. Unsigned integers can only hold positive numbers.  
We need to declare it using `signed` or `unsigned` keywords before the `int` keyword. If we just use int keyword, the default is signed integer. 
For real numbers there are float (4 bytes), double (8 bytes) and long double (10 bytes) types we could use. 
From C++ 11, it's recommended that we initialize a variable like given below, instead of using the `=` assignment operator. 

```cpp
double rate_of_interest {0.07};
```

## 5.2. The Auto Keyword 

There is also an `auto` keyword in C++. If we ever decided not to declare the data type and let the compiler decide it, we can use this keyword and pass in the value. 

```cpp
#include <iostream>
#include <typeinfo>

using namespace std;

int main() {
    auto myVar = 9.5;
    cout << "Type of myVar : " << typeid(myVar).name() << endl;
}
```

## 5.3. Value vs. Reference 

Reference variables in C++ are declared using an `&` sign before the variable name. We must initialize a reference variable in C++.  When we declare a reference variable, we must mention to which variable this is going to refer. 
Data type of the reference variable must be the same type as the variable it points to.  

## 5.4. Constants 

We can declare a global constant variable using the `const` keyword (right after the namespace declaration). It will be available for all the functions. 
```cpp
const int number = 5;
```

## 5.5. Garbage Values 

If we create a variable and not initialize it by giving it a value, initially it will be holding a garbage value. A garbage value is whatever the state of that point of the memory was. It was never initialized, neither was cleared. So, when we create a variable, the best thing to do is to initialize it to zero by using the equal sign, or empty curly braces.  `int var {};` 

## 5.6. I/O Streams 

`istream` is a class in the `iostream` library, and `cin` is a global object that we can use to take console keyboard input to the program. 
To extract a value from the keyboard using the `cin` object and assign that to a variable, we need to use `>>` extraction operator. This class is intelligent enough to extract the value accordingly to the type. 

## 5.7. Operations with different numeric types 

Once we apply some operation between two integers, the result is always going to be an integer. If we apply an operation between an integer and a double, the result is going to be a double. Operations between two different data types, the resulting data type is always going to be whichever is the highest precise. 
We can use explicit casting to covert between data types. We need to mention the casting type inside parenthesis, before the variable or value. 

## 5.8. Binary Operations 

Assigning a value to a variable using the `=` operator is a **binary operation**. It has two operands, the left-hand side and the right-hand side. The left-hand side is called the lvalue (target) and the right-hand side is called the rvalue (source). The operation is always pushing the rvalue to the lvalue. The lvalue is always going to be a variable. We cannot assign a value to a constant. 
All the operators (like `+`, `-` and even `=` ) returns a value. If we execute `int x=5`, `x` gets the value 1 and this assignment returns 5. If we push that into a Boolean variable, it’ll truncate into `True` (or 1). 

## 5.9. Unary Operations 

The operators that required to be applied on only one operand are called **unary operators**. The unary increment `++` and unary decrement `--` operators are the most commonly used unary operators. 
These two unary operators can be post-fixed or pre-fixed (either `x++` or `++x`). 
Unless there are more than one operator in the expression with the unary operator, there is no difference between the post-fixed and pre-fixed operators. But once there is more than one operator, the post-fixed operator will be executed after the other operator, and the pre-fixed operator will be executed before the other operator. 
In this example, the equals assignment happens before the increment. 

```cpp
#include <iostream>

using namespace std;

int main() {
    int x {10};
    int p;
    p = x++;
}
```

We cannot use the assignment operator and a unary increment or decrement operator with a constant, we'll get a compilation error. That's because, under the hood, this is what's happening.
```cpp
p = ++x; 	// ++x -> x = x + 1
p = ++5; 	// ++5 -> 5 = 5 + 1
```

## 5.10. Comparing and Booleans 

The result of any comparison in C++ is either `true` or `false`. It is a value of the `bool` data type. 
True in C++ is represented with 1 and false in C++ is represented with 0. 
Relational operators in C++ are `==`, `!=`, `>`, `>=`, `<`, `<=`.
Logical operators in C++ are logical AND `&&`, logical OR `||` and logical NOT `!`.
There also shortcut assignment operations in C++, like `+=`, `-=`, `*=` and `/=`. 

## 5.11. Characters 

The `char` or the character data type is used to hold a single character. We always have to assign the value in single quote marks. The default encoding is ASCII. We can cast the char variable or the value into an int data type to get the ascii code. 
But, there is no exponential (power of) operator in C++.

## 5.12. The Yoda Syntax 

Some programmers use (`3==i`) instead of (`i==3`) as the condition in if statements with binary equals operator, it’s called the **Yoda syntax**. They tend to use this because, if they leave off one equal sign in the operator, instead of doing an assignment operation, the compiler will return an error, because we can’t assign a new value to an integer literal.  
If we ever have anything to be checked if it’s not zero before pass it into a function (e.g.- modular operator, that will blow up if we pass in zero as the right-hand operand), C++ programmers tend to use this pattern extensively. 
`if (y && (x % y))`

## 5.13. The Ternary Operator 

The only **ternary operator** in C++ is the conditional operator. It's defined as,  
`(condition)?(expression if the condition is true):(expression if the condition is false)`  
We can nest these conditional operators to get an equivalent to an else if statement. This is also called the **immediate if** statement. 

## 5.14. The Switch Statement 

The main best thing about using a switch statement instead of if-else, is that the compiler doesn’t have to test the expression for each condition, so it’s much more efficient than using if-else statements over and over again. Using an enum or an integer value instead of an expression is very common in switch statements.  

The ordering of the cases is not mandatory. The values of cases always have to be constants. If we do not add the `break` keyword, once a case is executed, it's going to fall through all the next cases and execute them until it comes to the end of the statement, or it finds a break. We don't have to add a `break` to the last statement. 

```cpp
switch (n) {
    case 1 :    
        cout << "One" << endl;
        break;
    case 2 : 
        cout << "Two" << endl;
        break;
    case 3 : 
        cout << "Three" << endl;
        break;
    default : 
        cout << "Invalid number for this" << endl;
}
```

## 5.15. The For-Loop 

As the initializer for a for loop, we can either declare a variable inline, or we can use one that’s already been declared. If we declare one in the initializer, that variable will go out of scope at the end of the for loop.  

We can use the `rand` function of the `cstdlib` library to generate a pseudo random number. But this function will give us the same random number (or numbers) each time we execute the program. That's because, its algorithm depends on a random seed, in order to get a different number or a set of different numbers, we need to change that seed.  
We can do that using the `srand` function. We can pass it an integer as a parameter, which will be used as the seed. But then we have to change the seed every time we execute the code.  
The easiest way to get around this is to pass the time of the system as the seed to the rand function. We can include the `time.h` or `ctime` library and use their `time` function (both are the same) with `NULL` passed in as the parameter. 
We can use mod operation on the returned number to get it in a range.  

```cpp
#include <iostream>
#include <cstdlib>
#include <time.h>

using namespace std;

int main() {
    srand(time(NULL));
    for(int i=1; i<=10; ++i) {
        cout << rand() % 100 << endl;	// numbers till 100
    }
    return 0;
}
```

# Functions 

In C++, functions can only return one value. C++ allows us to overload functions (polymorphism). Function can be inside classes (member functions) or not (global/ free functions).  
When we pass in variables as parameters into a function in C++, the arguments we are passing inside parenthesis in the function call, are called **actual arguments**. 
The arguments we define in the function definition that reflect these actual arguments are called **formal arguments**.  

In C++, every time a function gets called, the process happening is, copy the values of actual arguments into formal arguments. When we pass in or return values to/from functions, the process of copying can be expensive. So, we should try to pass parameters and return values as references. But we should be careful not to get ourselves into a dangling pointer. We can pass reference variables into a function just by passing the variable name (don't need to add `&` in the function call, only add the in the definition and prototype). 

The process of compiling C++ starts from the beginning of our code and goes line by line. Its scope is whatever is written prior to the line currently compiling. But the process of execution starts from the `main()` function, and its flow depends on how our code is written.  
Because of the compilation starts from the top, if we call a function in our code before it appears in the code, the compiler will not compile the code. So, we need to mention that function's details prior to the calling. That is called a function prototype declaration. 

```cpp
#include <iostream>

using namespace std;

void swap(int &, int &);

int main() {
	int first = 13;
	int second = 53;
	swap (first, second);
	return 0;
}

void swap(int &a, int &b) {
	int temp = a;
	a = b;
	b = temp;
}
```

If we’ve correctly declared our function in a header file, and correctly passed in the arguments, we should not get any compile time errors.  
If we’ve not correctly implemented the function in the cpp file, we’ll get linker errors. Linker errors looks like  `Code.obj: error LNK ###`. If we get an error like this, we should probably look in the implementation.  
Usually, when we try to identify an error, it’s good practice to start from the first line of compilation output. 

# Pointers 

Integers (type `int`) in C++ takes 4 bytes space. For any variable, the byte number is the least significant byte, the starting byte of that particular value in primary memory. When we look at a pointer for a variable, it gives us the address of the first byte of that variable's value in memory. Then C++ runtime checks the data type and gets the number of bytes that data type takes, and gets that number of bytes from that starting address.  

`&` is called the **address of** operator, because it gives us the memory address of any variable. In C++, any value that starts with 0x is a hex (hexa-decimal) value. If we print out the pointer of a variable, we'll get a hex number. If we want the number to be an integer and not hexa-decimal, we can cast the pointer into unsigned.  

If the `&` operator is prefixed to a variable that means, *please take the address of this instance*. 
And if `&` is post fixed to a type that means, *this is a reference variable of this type*.  

We can also create pointer variables in C++. If we declare a variable `p`, with type `int*`, it's considered to be a pointer variable of an integer. We can put the `*` symbol (Asterix) after the data type or before the variable name (`double* k` or `double *k`).  
But if we want to declare multiple pointer variables in one declaration, post-fixing the data type would be the way to go. After the declaration, we can initialize it with the pointer of some variable in memory. Once we have a pointer variable, pointing to a variable in memory, the pointer variable only holds the address of the initial byte of that value. But we can use that pointer to manipulate the whole value. The `*` symbol is called the dereferencing operator. 

```cpp
int temp = 300;
int *p = &temp;
// now, the value is 300
*p = *p + 1
// now, it's 301
```

If we try to dereference a bad pointer, our program will crash in run time. To not let this, happen, we can immediately initialize pointers when we declare them. C++ 11, introduced a keyword `nullptr` we could use to initialize a pointer as null. Then before we access that pointer, we can use either an if statement or an error handling code to check if it is null, and use it only if it’s not null.  
References on the other hand, cannot be null. They always have to be initialized with something.  

If we declare an integer pointer like const `int* cpi` , that means the `cpi` points to a **constant integer**, of which we cannot change the value.  
Or if we declare it like `int * const cpi` , that means a **constant pointer**, which cannot be changed. We cannot change the address of a constant pointer, it has to be pointing to the same object.  
We can combine both of those functionalities and declare something like `const int* const crazyInt` of which we cannot perform each of those things, it can only access the data.  

The size of the memory that takes for a pointer depends on the architecture of the compiler we're using. If it's 32bit compiler, a pointer takes 32 bits in memory.  
We can use the sizeof function to see how much a memory a variable or a pointer take. In 32bit compiler, the size of a char pointer (`p`) is 4 bytes, while the size of the character itself (`*p`) takes 1 byte.  

The operating system allocates the variables of one code-block in memory, in a top to bottom stack. If we declare a few variables and check their pointers, we'll see that their pointer starts after the previous one's highest significant digit. There is a pointer add operator in C++, which will give us the address of the next variable within that block, once we +1 a pointer. Same way, if we subtract one from a pointer, it's going to get the value of the address of the previous variable in memory.  

Consider two integer values declared as `temp1` and `temp2` that are allocated at **7012088** and **7012084** (may vary from execution to execution), if we create two integer pointer variables `t1` and `t2`, if we do `t2 = 2t +1`, we'll get the value of `t1` (because it's top-down, the memory is allocated in descending order. `t2 +1 = t1`, even though `t2` is declared after `t1`).  

C++ do not allow us to assign a pointer to a different type of pointer (e.g.- int pointer to a char pointer). But we can use explicit casting to get around that. If we create an int pointer that holds some value, and we assign that pointer into a char pointer using explicit casting, once we print out the value of that char variable, we'll get the ascii character at whatever that integer's first byte's value is.  
We can also call function by pointers as well as references. 

```cpp
#include <iostream>

using namespace std;

void plusSome(int* value1, int* value2) {
	*value1 = *value1 + 10;
	*value2 = *value2 + 5;
}

int main() {
	int first = 13;
	int second = 53;
	plusSome (&first, &second);
	cout << "first : " << first << endl << "second : " << second << endl;
	return 0;
}
```

If a pointer points to an object, and we want to use a member function of that object, we have to cover the pointer variable with a bracket `(*p)` and then use the dot `.` character to call the member. Or we can use the arrow sign `->`. 

# Arrays 

Array is a contiguous data structure. Which means, all the elements are going to be allocated one after another in the primary memory.  

The name of the array always holds the first element's pointer. Whenever we're referring to an element with its index, the compiler uses pointer calculations to get the pointer of the given element. `a[1] -> (*&a +1)`  
Referring to an index as `4[a]` is also possible, because - `4[a] -> (*4 + &a)`  
To print out the elements, either these ways are allowed.  `a[i]`    `i[a]`   `*(a+i)`

* We can declare an integer arrays using - `int arrayName[10];` or `int arrayX[5] = {10,20,30,40,50};`. 
* If we declare an array, and not initialize it, all of its items will be holding garbage values. 
* If we declare an int array of 10 elements, and we initialize it using `{10,20}`, these items will be filled into the corresponding indexes of the array, and the rest of the array's elements would be initialized with zero. 
* If we initialize an array with `{0}`, all of its elements are going to be zero. 
* If we do not declare the array's length and initialize it with some values, the compiler's going to create the array with the given number of elements. 
* Multi-dimensional arrays are also allowed in C++.

In C++ 11, a range for loop was introduced. We can use it to traverse an array. The syntax is similar to for each loop 
`for(data_type_of_elements   identifier  :  collection)`
We can get a reference to variables in the for-range loop, and use the identifier to manipulate the elements of that array. We can also use auto type for simple things, so we can pass in different types of arrays. 

```cpp
int x[] = {10,20,30,40,50};
for (int &p: x) {
	p *= 2;
}
for (auto k: x) {
	cout << k << " ";
}
```

Special thing to note about arrays in C++ is, their variable name only holds the base address. It doesn't contain the number of elements. So, when we pass an array to a function, it's not easy to get around because, we cannot process it without its length. So usually, C++ recommends to receive a reference to the array in functions. 

```cpp
#include <iostream>

using namespace std;

const int size_of_array = 5;
void print_array (int (&x) [size_of_array]) {
	for (auto k:x) {
		cout << k << " " ;
	}
}

int main() {
	int x[] = {10,20,30,40,50};
	print_array(x);
}
```

Even though arrays can be very useful, most developers recommend not to use them, and to use a **vector** or another collection instead. That’s because of a few problems, that C-style arrays have.  

First is that they don’t know how big they are. Arrays do not allocate its length information anywhere. It’s okay to use them only if we know exactly how big our array is, and it is good practice to use a constant integer member variable for the length of each array, and pass that into the array, so when we need to know how big it is, we can just refer to that integer. If the array is allocated dynamically, on the heap, there’s literary no way of telling or even calculating how big the array actually is. This could lead into errors.  

Using pointer manipulation extensively to access elements of an array could lead into errors very easily. If the array is allocated dynamically, we could just increment the value and get any number of pseudo values that are actually not in the array. And more dangerously, we can actually write new elements to the array, past its boundaries. When we try to add an element beyond the boundaries of an array, if we’re using pointers, it would actually work, and overwrite some other point in memory, cause there’s no way for an array to be automatically resized just because we’ve added new elements to it. This error would not even be noticed by the compiler or runtime, and lead into a buffer overflow error or worse, without us even noticing.  

Collection implementations like **vector**, can handle all these problems. **Vectors** can even grow automatically as we add elements to it. So, we should only use an array, if we’re sure absolutely about what we’re doing.  

# Strings 

String class of the C++ standard library, which contains all the necessary functions needed for string processing. We can instantiate a string using `string var_name("This is a string");`  

But we can only call the constructor once for each string object. If we ever want to change the string, we can pass a string to that variable. We can also instantiate a string with the same character using this, it will give us a string made with 15 x s.
`string str3(15, 'x');`  

When we use `cin` to get input to a string variable, it only takes one word. Anything we type in after the first whitespace is going to be discarded by C++. We can use `cin` to get only one word input. But if we want a string with more than one word as input, we can use the global `getline` method. We need to pass in the input stream (`cin` object) and the string variable in which the string be saved to the `getline` function to get the whole string.  
`getline(cin, myline);`  

We can use the at function of string class and pass it the index of the character we want, to get a specific character of a string by its index. We can also do that by considering the string an array, and using square brackets. There is also a length function in string class.  
Characters are comparable, to check if a letter is in lower case we can use the comparison operators. To make a character upper case, we can subtract 32 from that character, because in ascii, the difference between a simple letter and its corresponding capital letter is 32. 

```cpp
string str = "Hello world";
for (char &p:str) {
	if (p >= 'a' && p <= 'z') {
		p -= 32;
	}
}
cout << str << endl;
```

We can use iterators to traverse through a string (or any other collection). In C++ we need to create an iterator object accordingly to the type of the collection. We need to use the scope resolution operator `::` to specify the type.  

The begin method of the string class returns the string iterator object, with the pointer placed at the beginning of the string. Same way, `str.end` function returns an iterator that's placed at the end of the string. We can use that to check if the iterator has come to the end of the string. When we traverse the collection, we need to use the dereferencing operator to get the element. In this case, the dereferencing operator is not about pointers, it's been overloaded for the iterator class. We also need to increment the iterator using unary operator, after we got the element.  

If we want to traverse a string in the reverse direction, we can use a reverse iterator. We can declare a reverse iterator using `string::reverse_iterator`. In reverse iterator, we need to call `str.rbegin` to get the reverse iterator object from the string. We can use the `str.rend` function to check if we've came to the beginning of the string. In reverse iterator, we need to use unary increment to traverse. 

```cpp
string str = "Hello world";
string::iterator it = str.begin();
while (it != str.end()) {
	cout << *it << " " ;
	++it;
}
string::reverse_iterator rit = str.rbegin();
while (rit != str.rend()) {
	cout << *rit << " ";
	++rit;
}
```

There is a clear method in the string class that we could use to clear all the characters of a string. To delete a specific portion of a string, we can use the erase method. We can call the erase method on the string and pass it the starting index position and the number of characters we want to erase. We can also use the (**str.begin()+number**) to indicate the starting position. Likewise, we can use (**str.end()-number**) to indicate the finishing position of the erasing.  

String class has `push_back`('char') method to add a character at the end of the string and `pop_back` method to pop a single character from the end of the string. The front method returns a reference to the first character, we can use it to change the first character.  
Likewise, back method returns a reference to the last character.  
There is also an `append` method, we can use to append another string literal to the end of a string. We can use the `insert`(pos, 'string slice') method to insert a string literal at a given position of a string.  
We can use the `find` method to search for a string inside another string. We can pass the search start position as a second parameter if we want. Whenever a match is found, it will return the index of the target as an unsigned integer. 

```cpp
string str ("You must know, first my no longer be first if second comes first!");
string target("first");
string::size_type index = str.find(target, 10);
while (index != string::npos) {
	cout << "Target string '" << target << "'' found at index : " index << endl;
	index = str.find(target, index +1);
}
```

**Size_type** is a general implementation of unsigned integer, we can use it to make compatible between systems.  
**npos** is the value that's going to be returned by find, if the target is not found till the end of the string.  
We can use the **find_first_of** method to find the first occurrence of any character of a given string, inside another string.  

There’s also a wstring class In the standard library for wide strings, which could be useful in a Unicode situation.  
String comparison in C++ is done based on their position in the dictionary. That's called lexicographical comparison.  
Lexicon is the dictionary and lexicography are the style of writing the dictionary. We can use comparison operators to compare strings. They are shortcuts to the compare method of the string class. If we want to, we can use that instead. String compare method returns an integer. If both strings are equal, it will return 0. If the string we compare on comes first in the dictionary, it will return -1. And if the augmented string appears first in the dictionary, it will return +1. 

We can use the `replace` method of the string class, to replace a part of a string with some other string. We need to pass in the replacement index as the first parameter, and the replacement length (size of the target we're looking for) as the second parameter, and the replacement string as the third parameter to the `replace` method. 

```cpp
string str ("first is the first would we like first");
string target("first");
string repl("second")
string::size_type pos = str.find(target);
while (pso != string::npos) {
	str.replace(pos, target.size(), repl);
	pos = str.find(target, pos + repl.size());
}
```

We can use the `substring` method to take out a portion of a string. We need to pass in the starting index position of the substring, and the length of the substring to the `substring` method. It returns a string.  

We can use the `istringstream` class of the header `sstream` to push a string to a stream. We need to pass in the source string to the `istringstream` object. We can use the extraction operator `>>` to extract each value from the stream.  
Default is to use spaces as delimiters. Otherwise we need to use the `peek` and `ignore` methods in `istringstream` to skip the delimiters.  
`Peek` method can check what the next character in the stream is, without making any disturbance. 

```cpp
string source = "10,20,30,40,50";
istringstream iss(source);
int k;
while(iss >> k) {
	cout << k << endl;
	if(iss.peek() == ',') {
	iss.ignore();
	}
}
```

We need to use the `getline` method with passed in the `istringstream` object and the token string object and the delimiter (the default delimiter for `getline` method is the new line character) to extract string tokens from a stream. With that, we can use it without the `peek` and `ignore`. We can nest this functionality to get more robust `istringstream`s.

```cpp
string source = "John:10,Tina:20,Robin:18";
istringstream iss (source);
string part;
while(getline(iss, part, ',')) {
	istringstream iss2 (part);
	string rec;
	while(getline(iss2, rec, ':')) {
		cout << rec << endl;
	}
	cout << endl;
}
```

To concatenate different types of data into a string, we can use the `ostringstream` class of the `sstream` header. We can use the insertion operator `<<` to insert different types of values into the `ostringstream` object. At the end, we can use the `str` method of the `ostringstream` class to get the stream into a string object.

We can use the `atoi` method on c-type strings (legacy - not string objects), to parse them into integers.  
We can use the `c_str` method to convert a string object into a c-type string.  
This way is commonly used in parsing integers read from files. 

```cpp
string m = "50";
int number = atoi(m.c_str());
```

# C-style Strings 

C-style strings are arrays of characters. Since arrays don’t carry around its length, a C-style string doesn’t know its length.  
The theory is, if we can put a special character at the end of an array, we can identify where it ends, and access it using its pointer. This special character is the null character ‘**\0**’ , it have the numeric value zero in it.  

So, if we want to put "**hello**" in a C-style string, the array actually has to be 6 characters long. We can use `strlen` function, that goes through the array, looking for this character, to know how long a C-style string is. This method is in the `<cstring>` header along with a lot more. Many of them are unintuitive and unsafe.  
So, we should take advantage of the modern `std::string` and `std::wstring` whenever we can. We can go back and forth between these by using the `.c_str()` and  `strcpy` methods. 

# File I/O 

We can use `fstream` header to handle file inputs and outputs in C++. We can use `ofsteam` class to output data into a file. 

```cpp
#include <iostream>
#include <fstream>
#include <cstdlib>

using namespace std;

int main () {
	ofstream fout;
	fout.open("myfile.txt");
	if (fout.fail()) {
		cout << "Error in opening file!" << endl;
		exit([1]);
	}
	fout << "Hello World!" << endl;
	int a = 35;
	double b = 	25.5 ;
	fout << "a = " << a << ", b = " << b << endl;
	fout.close();
	return 0;
}
```

If the given **myfile.txt** doesn't exist, it's going to be created. Otherwise it will be overwritten and all existing the content of the file will be lost.  
If the file fails to create or load, the fail method will return true.  
Finally, we need to execute the `close` method, that will flush (or dump) all the data into the file. 

We can use the `ifstream` class to read files. The eof method in `ifstream` class returns true if we've reached the end of the file.  

```cpp
#include <iostream>
#include <fstream>
#include <cstdlib>

using namespace std;

int main () {
	ifstream fin;
	fin.open("data1.txt");
	if (!fin) {
		cout << "Error in opening file!" << endl;
		exit([1]);
	}
	int val;
	while (!fin.eof()) {
		fin >> val;
		cout << val << " ";
	}
	fin.close();
	return 0;
}
```

We can use the `setw`(width) method to print data into cout with a better structure. This class is in `iomanip` header. There is other functionality given in C++ to make it easier. 

# Dynamic Memory Allocation 

Usually in C++, the compiler will write instructions for memory allocation during the compilation of a program. Then it actually uses the allocated memory in execution. This is called **compile-time allocation**.  

Take an **integer array x[100]** for an example. In this scenario, the compiler will write instructions to allocate 400 bytes for this array.  
It is a fixed-allocation which means, during the execution, we can't get more memory.  
That is one drawback of compile time allocation.  

But if we allocate memory in runtime, we can allocate exactly what we need, so there will be no shortage or wastage of memory. 
We can use the `new` keyword in C++ to dynamically allocate memory for a pointer. The `new` keyword should be followed by the data type. That memory will be allocated during the execution of the program.  
The compiler will not write any instructions for this memory allocation. The allocation will be arranged contiguously. The base address will be stored in the pointer.  

## Stack vs Heap Memory Allocation 

Whenever we allocate memory dynamically using the `new` keyword, that memory will be allocated in the **heap** memory.  
The **stack** area is used by the system to allocate compile time memory. So, all the local variables that are declared using compile time allocation, will be using the **stack**.  Once the operation is finished, the operating system de-allocate (or release) the memory implicitly from the stack.  

But with dynamic allocation, it's programmer’s responsibility to de-allocate the heap memory once the job is done, with `delete` keyword. The heap is also called the **free store**.  

Whenever we’re using dynamic memory allocation, we need to make sure that we’ve implemented the **copy constructor**, the copy assignment operator and the destructor.  

Whenever we dynamically allocate memory, there is a chance to have some memory leak if we fail to manage the memory efficiently.  
For an example, if we write a function that dynamically allocate an integer variable locally. Once the function is completed and the execution is returned to the caller, if we did not delete that memory explicitly, there will be a memory leak.  
The pointer for that memory will be lost within the program, but the allocated memory stays intact. So, it's no longer possible for us to reach that memory. The operating system will not be able to release that memory for later use. We also must never call return in a function, before a `delete` keyword.  

## Shallow vs Deep Copies 

There are two ways to copy a compile time allocated array into a dynamically allocated array. A **shallow copy** means, we're just copying the pointer. So, our dynamically allocated pointer would actually be pointing to the same array in stack area. If the program deletes the original array, the copied shallow array would still have a dangling pointer, that points to an invalid memory.  

To get around this, we need to use deep copying. We can implement that by creating an entirely new array dynamically using the new keyword, and copying each element from the source array using a for loop.  

# Vectors 

Vectors are dynamic containers and its implementation is available in the standard C++ library. Vector class comes with a lot of functions that we can use to process our data.  
We need to use the `vector` keyword to initialize a vector. It must be followed by the type of the elements in angle brackets and the vector variable name.  
We can use the `push_back`(value) method in the vector class to append an element at the end of the vector. We can also assign values like arrays using indexes. We can use a for loop to iterate through a vector. 

```cpp
vector <int> v;
v.push_back(10);
v[1] = 20;
for (int p:v) {
	cout << p << ", ";
}
```

The values of a vector, are actually contained within a dynamic array, inside the vector object that is abstracted from us. We can get the base address of that array using the data method of the vector class. We can capture that address into a pointer (the pointer's type should be the type of the elements), and using that we can manipulate the elements.

Vectors can grow automatically. We can add any number of elements, and still access them using their indexes, without worrying about the size of the vector. And we can check the size and the capacity using size and capacity methods of the vector at any time. 

Because of this functionality, memory allocation for each time we add a new element costs a bit much time. The vector class has a clever algorithm to have optimal balance between the execution time and memory utilization. When we're constantly adding elements to a vector, its capacity growth gets higher than its size. Vector class will allocate more memory, so when we add more elements, it can execute faster. So, at any time of a vector’s execution, it's capacity might be slightly higher than its size.  

If we don't want this extra space, we can use `shrink_to_fit` method. It will discard all the extra allocated elements at the end.  

There are many ways to create a vector. If we declare a vector like `v1` in this example, that means this `v1` vector has five elements, and each of those elements are initially set to -1. We can initialize a vector with an array. The first parameter is the array and the second parameter is the last element, in the `v2` vector, we're copying all 5 elements, and in `v3` we're copying only the second and the third elements. We can initialize a vector with another vector (`v5`), and it's going to be a deep copy. We can initialize a vector with an iterator like in `v6`, and it will be a deep copy.  
In that case, we can also use `rbegin`, `rend`, `begin` and `end` methods as iterators. 

```cpp
vector <int> v1(5, -1);
int x[] = {10,20,30,40,50};
vector <int> v2 (x, x+5);
vector <int> v3 (x+1, x+3);
vector <int> v5 (v4);
vector <int> v6 (v5.begin(), v5.begin() + 3)
```

There are methods like front and back in vector class, that gives us the first and the last element in the vector. We can use those methods to change the current first and last elements.  
We can use the `insert` method to insert a new element in a desired location within the vector. The new element will take that place, and the rest of the elements would be pushed back.  
There is an `erase` method in the vector class that we can use to remove a particular element from the vector. It accepts a single parameter, we can pass in end, front, etc. Or it also accepts a two parameter range for beginning and end of erasing. 

```cpp
vector <string> names {"Anthony", "Josh", "Mark", "Linda", "Carl"};
names.erase (names.begin(), names.size()-2;
```

# Map 

Map is a collection in the standard library. Things In a map are organized in key-value pairs. Just like vectors, it grows when it needs to. It keeps the sorted order, so we can access items using keys and speed search, but it costs a little to add items.  
We can use the key inside square brackets to access a value, or we can use the find method to look up.  
We can also use `pair` and `insert` functions to add pairs. 
Map iterators points to a pair, first and seconds. We need to dereference the pointer to get the key and the value. 

```cpp
map <int, string> mymap;
mymap [1] = “One”;
pair <int, string> p(2, “Two);
mymap.insert(p);
for (auto ip = mymap.begin(); ip != mymap.end(); ip++) {
	cout << ip->first << “ : “ << ip->second << endl;
}
auto found = find(2);
cout << found->first << “ : “ << found->second << endl;
```

The `find` method returns an iterator. We can get the found items by dereferencing it, or we could use square brackets to access the found item.  
In case of a map, there can be only one hit for each key, because they are unique.  
But there are other collections that can have more, and in those collections, find method returns an iterator with more than one item. 

# Other Collections 

There is also a **list** class in the standard library that implements a linked list. We can traverse a linked list just like we do with a standard vector. Each element of a linked list keeps two pointers, for the previous and next element. Adding elements is faster in linked lists, but it takes some time to access the elements.  

All these classes are declared in the standard library, so they can be used interchangeably. If we declare the type to be `auto`, we can change the collection type whenever we want to, it would still work because after all they have the same standards.  

There are classes that gives different behaviors to access elements, like pushing and popping. FIFO collections are available as *queues* and *dequeues* (double-ended queue).  
There is also a sub collection called **priority_queue** which lets us assign a priority to each element, and be ordered based on the given priority.  

There is also a **set** implementation, that has extra functionality for mathematical operations like union and difference. Unlike a vector, a set doesn’t need to re-organize itself whenever we add or remove an element, it allows us to keep iterators going while we’re messing with the elements, which we cannot do with a vector.  

We can use the **multimap**, if we want a map-like structure, but with more than one value per key. 

# Sorting and Searching 

Sorting and searching functions in C++ come externally to collections. They are in a header called `algorithm`. They take a collection or in most cases, a pair of iterators, so it can search from given beginning to the given end of the collection. We can use the same functions in any collection. 

The standard *for_each* function in the standard library, takes three arguments. A begin iterator, an end iterator and what to do when it gets to each element.  
Interestingly, as that third argument, we can implement our own function that takes an *auto* (or the actual type) argument and does something, and pass the name of that function (without parameters). That would be a functional call.  

The find_if method takes a start iterator, an end iterator, and a function which will return true for a certain value. Only the elements that got true returned from the given function will be returned as an iterator of the given type. 

```cpp
void print (int i) {
	cout << I << “ “ ;
}
bool odd (int i) {
	return i%2;
}
vector <int> v;
v.push_back(5);
v.push_back(2);
for_each (v.begin(), v.end(), print);
cout << “-----------” << endl;
auto o = find_if (v.begin(), v.end(), odd);
while (o != v.end()) {
	cout << *o << “ “;
	o = find_if (++o, v.end(), odd);
}
```

We can sort a collection by simply calling the `sort` function with start and end iterators passed to it. It actually has a lot of overloads that take different arguments.  
For example, if we wanted to sort based on a different factor, or if we want to use a different order. 

# Struct 

Struct comes from the **C** language, it allows us to create user-defined types in a fundamental way. We can do that using classes with object-oriented programming too. But struct is generally used for **POD** – ‘plain old data’ with little or no business logic.  

They can have member functions, constructors and destructors. The only difference is that in structs, the default access modifier is public, unlike in a class which is private by default.  

We can define our own structures using the `struct` keyword. Inside curly braces, we must define the members, and the braces must be closed with a semi-colon. Then we can create objects using this structure.  

We can use the member access operator (the dot . ) to access it's member variables. In the C way of defining types, there is no way to define the methods for the type within the type definition, so the operations for the structure are defined outside the struct block. 

```cpp
#include <iostream>
#include <string>

using namespace std;

struct Account {
	int accNo;
	string holderName;
	double balance;
};

Account readAccountData() {
	Account acc;
	cout << "Input account number: " ;
	cin >> acc.accNo;
	cout << "Holder's name: " ;
	cin >> acc.holderName;
	cout << "Initial balance: " ;
	cin >> acc.balance;
	return acc;
}

void printAccountData (Account& acc) {
	cout << "Account Details" << endl;
	cout << "-----------------------------" << endl;
	cout << "Account number: " << acc.accNo << endl;
	cout << "Holder's name: " << acc.holderName << endl;
	cout << "Balance: $" << acc.balance << endl;
}

bool accountDebit (Account& acc, double amount) {
	bool success = false;
	if (acc.balance >= amount) {
		acc.balance -= amount;
		success = true;
	}
	return success;
}

void accountCredit (Account& acc, double amount) {
	acc.balance += amount;
}

int main() {
	Account a;
	a = readAccountData();
	printAccountData(a);
	cout << "Input debit amount: " ;
	double amount;
	cin >> amount;
	bool success = accountDebit(a, amount);
	if (success) {
		cout << "Account debited with $" << amount << " successfully." << endl;
		cout << "Current balance: $" << a.balance << endl << endl;
	} else {
		cout << "Debit unsuccessful, make sure you have sufficient balance." << endl << endl;
	}
	return 0;
}
```

We can also access members of a struct type using **struct pointer**. In that case, we have to use the **arrow operator** to access the members, instead of the *dot operator*.  
If we allocate the object dynamically, we can use pointers and the arrow operator. Or we can use the dereferencing operator on the pointer to use the dot operator, but if we do that, we need to cover the dereferencing with parenthesis to separate it from the dot operator. 

```cpp
Account a;
Account* aptr = &a;
aptr->accNo = 5;
aptr->holderName = "Jonh";
a.balance = "500.00";
Account *b = new Account;
(*p).accNo = 45;
p->holderName = "Tom";
delete p;
```

# Object Oriented Programming 

Classes in C++ are defined using the `class` keyword followed by the name of the class and curly braces block ended with a semi-colon.  
A class typically have three sections, *private*, *public* and *protected*. These access modifiers must be followed with a colon, and then we can write the members in there. We can have multiple sections of access modifiers. If nothing is mentioned, the members are going to be considered as private. Protected members will be available in the scope of that same class and within the child classes.  

The methods can be implemented in-place, within the class right with the declaration. But in general practice, we usually implement the methods outside of the class. But if the methods are very simple (like setters/getters) we can write them in-place.  

Usually, the class declaration is written separately in a header file, and the method implementations are written in another cpp file.  

In order to write the implementations for the methods outside of the class, we need to use the '**belongs to**' operator (also known as the **scope resolution operator** `::`) and indicate the class in which this method is declared in.  

C++ allows us to overload any method of a class, as long as those methods have different method signatures.  

An object cannot be created if there is no constructer defined in the class. But, if we do not write a constructor, once we try to construct an object, the compiler writes a default constructor for us.  
The default constructor is an empty constructor block, with no parameters and no functionality within the constructor. But if we write a constructor with any signature, the compiler will not write the default constructor. We can implement the constructors outside of the class.  
In general practice, we implement the toString method in the class using an ostringstream object. 

```cpp
class Car{
    private:
        string color;
        int speed;
        bool isEngineOn;
    public:
        Car();
        Car(string c);
        void acceleration();
        void applyBreak();
        int getSpeed();
        void startEngine();
        void stopEngine();
        string toString();
};

string Car::toString(){
    ostringstream oss;
    oss << "Color of the Car: " << color << endl;
    oss << "Current Speed: " << speed << endl;
    if (isEngineOn)
        oss << "Engine is On" << endl;
    else
        oss << "Engine is Off" << endl;
    return oss.str();
}

Car::Car(string color){
    this->color = color;
    speed = 0;
    isEngineOn = false;
}

Car::Car(){
  this->color = "Gray";
  this->speed = 0;
  this->isEngineOn = false;
}

int Car::getSpeed(){
    return this->speed;
}

void Car::stopEngine(){
    if (this->isEngineOn){
        this->isEngineOn = false;
        this->speed = 0;
    }
}

void Car::acceleration(){
    if (this->isEngineOn)
        this->speed += 10;
}

void Car::applyBreak(){
    if (this->speed - 8 >= 0 )
        this->speed -= 8;
    else
        this->`speed = 0;
}

void Car::startEngine(){
    if (!this->isEngineOn){
        this->isEngineOn = true;
    }
}
```

In memory management, for each object the variable values are loaded to memory at each instance. But the methods are only loaded once. The methods will know on which object to work on, because we're calling them on each object, using the dot operator.  
So, as long as we call the methods from a method which contains the objects (e.g.- main) there will not be any confusion.  

Think about the control flow of a program. When we're calling a method on an object, the control will jump inside the method implementation. If the information, on which object the method is called on is not passed in to the method, the runtime will not be able to resolve the member variables for the method to work on. That information is not passed on to the methods explicitly by the programmer. But it's happening implicitly by the use of '*this pointer*'.  

Whenever we're making a reference to any instance member of a class, the compiler always rewrites the code with this pointers for every instance member of the class. This pointer is declared using `this` keyword followed by an arrow.  

This pointer holds the address of the current object by which the method has been called. The compiler always prefixes references of a class with this pointers.  
If we want, we can write them ourselves as well. If we use a parameter with the same name as a member variable in a method, we have to use the this pointer explicitly. 

```cpp
void Car::Car(string color) {
	this->color = color;
	this->speed = 0;
	this->isEngineOn = false;
}
```

When we want to access an object from a method outside the class, that's not going to change the object, we can use a constant pointer to pass in the object pointer as a parameter to the function. Using a pointer, increases the efficiency of the program's execution. By declaring the pointer constant, we can make sure there will be no side effects that affect the object. We can declare a constant using the `const` keyword. We also need to declare those methods as constant as well.  
The constant keyword comes after the parameter declaration in the method declaration. Once we add the const keyword to a method, that means that method will not change any instance member of the object.  
We can declare getters constant. Method declaration and implementation both must have const keyword between parenthesis and curly braces.  

After declaring a method constant, if we still want to perform an operation that may update or change a member variable, we will get a compilation error.  
But, we can still get around that using mutable variables. Once we declare a member variable mutable, any constant method can still change the variable's value, and the compiler is going to overlook that operation.  
We can declare a variable mutable using the `mutable` keyword.  
This is only used in such occasions as a simple operation for performance enhancement. 

When we write constructors in C++, we can use the general way to initialize variable just like in other languages, by taking arguments and assigning them into the member variables.  
But this costs a performance wastage. When a constructor like that is called, it first creates the member variables in memory and initialize them, and once the assignment takes place, those variable values are changed into them.  
This might not be a problem when we’re dealing with small objects that have int like members. But most of user defined types (like strings, etc) takes up a considerable amount of processing power, if we keep this up.  
So, it’s good practice to write constructors this way. 

```cpp 
MyClass {
private: 
	string mystring;
public:	
	MyClass(string s);
};

MyClass::MyClass (string s) : mystring(s) { 
	/* leave this empty */
}
```

Objects we create are instances of classes. They have a lifetime.  
When we call a constructor, memory is allocated for that particular object in stack.  
The object goes out of scope, usually at a `}`, and then the reserved memory is released.  

In C++ there is a saying **RAII – Resource Acquisition is Initialization**, that means if we have a resource that needs to be managed (e.g.- an opened file, a database connection or a windows cursor), the constructor will acquire the resource and once its lifetime ends, the destructor will be called to release the resource.  

Whenever if needed, we can use `{ }` to cover any code. If we cover an object with a pair of curly braces, once control reaches the end brace, the destructor will be called.  

# Make 

If we have a project with a class called testclass that's declare in `testclass.h` and implemented in `testclass.cpp` with a client named `main.cpp`, the command to compile all files looks like this.  
`g++ -o myprogram -Wall main.cpp testclass.cpp`  
Wall command enables show all warnings in the compilation. We don't need to mention the header files. 

In general practice, we don't usually compile multiple filed projects in the previous way. Instead we use the **make** utility in order to build the projects.  

Consider a project with three files, `testclass.h`, `testclass.cpp` and `main.cpp` in the same directory.  
We can write a **makefile** for that like this.  

```cmake
all: myprogram

myprogram: main.o testclass.o
	g++ -Wall -o myprogram main.o testclass.o

main.o: main.cpp
	g++ -c -Wall main.cpp

testclass.o: testclass.cpp
	g++ -c -Wall testclass.cpp

clean:
	rm testclass.o
	rm main.o
```

We need to save this file as '**makefile**' with no extension in the same folder. Once we execute the command `make` in that directory, the project will be built.  

These all, clean and others are called rules (or rule labels).  
`all` rule label indicates what the final executable is after the compilation. Then it tells how that executable is going to be created. Right after the colon, we have to indicate what objects required to create the executable. Then in the next line with one tab from the beginning, we need to write the command for the compilation of that executable, given those indicated object files exist.  
Then in the same way, we need to indicate how to build the required dependencies for that executable to be created. If they depend on others, we need to add rules for those too. And at the end, we can add some clean-up commands using the `clean` rule label. 

# Operator Overloading 

C++ allows us to overload operators. But this functionality can change the natural meaning of operators. That's why most languages don't allow operator overloading.  
Implicit data types and classes have operators defined in the compiler. But for explicit classes, we need to implement how those operators should work. That's what operator overloading is.  
When we apply an operation on two operands, compiler will call the implemented function regarding to that operator on the left-hand operand, and pass in the right-hand operand as the parameter. The compiler will look for the corresponding method within the class definition. Usual operator methods named `operator+`, `operator-` and so on.  

Some operators cannot be overridden. The scope resolution operator `::`, conditional operator `?:`, member access operator (the dot `.`) cannot be overloaded.  
In most cases, the return type is also the type of the same class.  

```cpp
Circle operator+ (const Circle& rho) {
	Circle result;
	result.radius = this->radius + rho.radius;
	return result;
}

Circle operator- (const Circle& rho) {
	Circle result;
	result.radius = abs(this->radius - rho.radius);	
	return result;
}
```

Unary operators like unary increment and unary decrement can be pre or post fixed. Consider [ c = ++c ], in pre-fixed increment, first the value will be incremented and then be applied to the variable. Consider [ c = C++ ], in post-fixed increment, the value will be applied to the variable first and then it will be incremented.  
For unary operators, we need to override two function for pre-fixed and post-fixed versions. In pre-fixed function, there will be no parameters. But the post-fixed function will take a dummy int parameter as recommended by C++.  
It is only used to make a difference between the pre-fixed and post-fixed unary operators. This dummy parameter is not a normal parameter. We wouldn't give it a name. It's declared only by the type. 

```cpp
Circle operator++ () {
	this->radius++;
	Circle result;
	result.radius = this->radius;
	return result;
}

Circle operator++ (int) {
	Circle result;
	result.radius = this->radius;
	this->radius += 1;
	return result;
}
```

We need to overload the insertion operator `<<`, for our objects to be able to output into a stream or printed out. Insertion operator is a binary operator. The left-hand operand can be `cout` or `fout`. And the right-hand operand is the object.  
The call would be like `cout.operator<<(object_instance)`. The operator function is called by the `cout` object. It's not our object which makes the call to the insertion operator function.  
We also cannot override the function in the ostream class. 
To get around this, we need to implement the insertion operator as a global function. Even though we overloaded all the previous operators as members of the class, they also can be implemented as global functions. 

```cpp
ostream& operator<< (ostream& sout, const Circle& c) {
	sout << "Radius: " << c.getRadius() << endl;
	return sout;
}
```

The return type would be a reference to an `ostream` object. The first parameter would be the left-hand operand, and the second parameter would be the right-hand operand. We cannot make a copy of the `cout` object that's been declared in the `std` namespace, so we have to take a reference to it.  

We can also write overloaded operators that take different arguments (like our class and an integer comparison), that will be useful sometimes. For an example, we might want to create a `Date` class and overload it’s plus operator so we can get another date object by adding an integer to the date.  
Take this comparison operator for an example. It would have `Date` to `Date` comparison and `Date` to integer comparison, `date1 < 5`  we can write a member function that overloads `operator<` .  
But, if the arguments are passed in like this `5 < date1` , we cannot include that function inside the class. We can implement it right outside of the class with the correct method signature. Their declarations would look like below as a free function, or we can declare it as a **friend function**. 

```cpp
Class Date {
	// rest of the class declaration
	public:
		bool operator< (Date& d);
	bool operator< (int i);
}

bool operator< (int i, Date& d);
```

# Friend Functions

In the above example, global method is accessing the private member `radius` through a getter function. But, having to access a private member from a global scope could get tedious sometimes.  
C++ have given the functionality for a short hand method called **friend functions** to solve this issue. We can use the `friend` keyword to declare the friend function of a class that's been implemented globally, but still need to be considered as a part of the class. 

```cpp
class Circle{
	//	everything
	friend ostream& operator<< (ostream&, const Circle&);
}

ostream& operator<<(ostream& sout, const Circle& c){
    sout << "Radius: " << c.radius << endl;
    return sout;
}
```

We have to return the `ostream` object because, otherwise multiple insertion `cout << c1 << c2`  will not be possible. If we had void in as the return in the `operator<<` function, we'll still be able to print out one `Circle` object, but not more than one.  

When we take `cout` as an input and return it back, when we have more than one objects to insert, those operations will be executed one by one. If we execute this `cout << c1 << c2` , first `cout << c1`  will be executed. After that operation, the `cout` object is returned back to that point. Then we'd have `cout << c2` . That's why we need to return the `ostream` reference back to the caller. 

Overloading extraction operator is just the same. We can implement a global method for `operator>>` and declare a friend function in the class. It should take and return an istream reference.  
These insertion and extraction operators work with `ifstream` `ofstream` objects as well.

```cpp
class Circle {
	//	everything
	friend istream& operator>> (istream&, const Circle&);
}

istream& operator>>(istream& sin, const Circle& c){
    sin >> c.radius;
    return sin;
}
```

There are six relational operators in C++. All those returns a boolean value. These operators will use the left-hand operand and apply the operator function on that object with the right-hand operand passed in as parameter. Inside our class, we can implement these operators just like we did with arithmetic operators. 

```cpp
bool operator> (const Circle& rho) {
	return this->radius > rho.radius;
}

bool operator== (const Circle& rho) {
	return this->radius == rho.radius;
}
```

The assignment operator (`=`) works without being overloaded. That's because, the compiler writes the task of the assignment operator by itself implicitly. We can overload it ourselves in a special situation. But the task of assignment is generally written by the compiler, because what it does is copying bit by bit from the right-hand operand to the corresponding left-hand operand. 

```cpp
class Circle {
	//	everything
	Circle& operator= (const Circle& rho);
}

Circle& Circle::operator= (const Circle& rho) {
	this->radius = rho.radius;
	return *this;
}
```

If there are multiple assignments in a single statement `a = b = c` , they are evaluated right to left.  
Whenever we're writing our own assignment operator, the compiler doesn't write its own version for that class.  
We have to overload the assignment operator when we have dynamic memory allocation in a class. But, if our class just have simple attributes, we don't need to overload the assignment operator.  

If someone accidently do  `obj1 = obj2` , this will lead to a crash. So, whenever we're overloading the assignment operator, we need to perform a check to see if it's the same object in memory by comparing the pointers.	 `if (this != &rho)` 

We also don't need to implement the copy constructor by ourselves. The copy constructor is used to copy an object's content to another object. It's done by copying every bit from the source object to the destination object. The compiler is able to do this by itself. We need to write this explicitly, when it comes to dynamic memory allocation for an attribute within our class. 

```cpp
class Circle {
	//	everything
	Circle (const Circle& rho) {
		this->radius = rho.radius;
	}
}
```

Note one thing: if we execute this `Circle c1, c2; c1 = c2;`  the assignment operator will be called upon the assignment. But if we do the assignment in line with the declaration like this  `Circle c1 = c2` , the compiler will call the copy constructor for that. That's because, there cannot be a chained assignment while the object is being created and the constructor does not return any value.  

If we create a class that behaves as a collection, we might have to overload the subscription operator `[]`. To do that, we need to write the overloaded method that takes an integer as an argument, with the return type of a pointer. Only thing the method needs to do is to return the element in the collection using the integer index.  
When we implement collection classes, we need to implement the insertion and extraction operators in such a way that is easier to identify as a collection. For an example, we can cover the set of elements with brackets and add commas in between each element.  

When we create a class with a dynamic member variable, we have to override the **destruct** method. The objects we create using that class will be stored in stack area while the dynamic member is allocated in the heap. When we instantiate objects inside another method, once that method is finished or the object goes out of scope, the object itself will be de-allocated from the stack. But that dynamic member will still exist as a dangling memory. This could lead into a lot of memory leaks.  
The destructor method will automatically be called, whenever the object goes beyond scope. The destructor for a class is just like a constructor. It has the same name as the class, except we need to prefix it with a tilde (`~`).  
Destructor methods take no argument and have no return type. Inside the method, we need to use the delete keyword to `delete` any dynamic member of the class. 

# Template 

Templates in C++ allows us to write generic code. We can write a function that's able to receive any type of parameters. We can write classes that can have instance members of generic type.  
In other languages like Java, C#, they have **generics** for this. But C++ **templates** are a little bit different. They are resolved at compile time, no runtime checks.  
Type safety is a huge part of C++ language, and this is how we achieve that.  
Most of old C++ collections and algorithms are rich in templates, even the old C++ standard library was called STL – Standard *Template* Library.  

We can declare a template using the `template` keyword, followed by the type declaration inside angle brackets. We declare the type placeholder using the `typename` keyword and we usually give the placeholder a capital letter like `T`.  
After the template declaration, we can use that type placeholder in our functions. It will replace the object type and give our function a generic independency from types.  

```cpp
template <typename T>
int compareTo(T a, T b){
    if (a < b){
        return -1;
    }
    else if(a > b){
        return +1;
    }
    else{
        return 0;
    }
}

int main() {
    int x = 10, y = 100, i;
    i =  compareTo(x, y);
    cout << "i = " << i << endl;
    return 0;
}
```

The compiler is clever enough to determine the type of the passed in arguments and replace `T` with integer. Or we can explicitly tell the compiler what type the parameters are, by pre-fixing the parameters with the type inside angle brackets. 
```cpp
compareTo <int> (x, y); 
```

The compareTo method with the template will still work fine for a class we implemented ourselves, as long as it's overridden the comparison operators.  

When we define our own generic class, that has a generic member, once we implement its method outside of the class, we need to specify a template and a type placeholder post-fixed with the class name in the scope resolution operator.  

```cpp
template<typename T>
class Test{
    private:
         T x, y;
    public:
        Test(T x, T y);
        T getSum();
};

template <typename T>
Test<T>::Test(T x, T y){
    this->x = x;
    this->y = y;
}

template<typename T>
T Test<T>::getSum(){
    return x + y;
}
```

There can be multiple type declarations in one template. 

When we declare our generic class with a *friend function*, that friend function would not be a part of the class. So, we need to declare a separate template for the friend function, and that template must contain a different type name to stop shadowing. And then we can pass that typename as the parameter for the friend function. 

```cpp
template <typename T>
class SimpleVector {
	// class declaration using T as the type
	template<typename U>
	friend ostream& operator << (ostream &, const SimpleVector<U>&);
}

template<typename U>
ostream& operator << (ostream &out, const SimpleVector<U>& sv){
    out << "[";
    for(int i = 0; i < sv.numElements; ++i){
        if (i == sv.numElements - 1)
            out << sv.item[i];
        else
            out << sv.item[i] << ", ";
    }
    out << "]";
    return out;
}
```

There could be some operations in a template implementation, that might not work for some objects. In that case, we could either write the missing operator, or we can write a specialized template.  
One of the special things about C++ templates is that they can be specially implemented for certain objects. At some times, template specialization is the only option for certain classes. 

```cpp
#pragma once

template <class T>
class MyGenericClass {
	// Class definition using T
};

template <>
class MyGenericClass <ForThisClass> {
	// Class definition using ForThisClass
};
```

# Inheritance 

We often have objects and entities which are bound hierarchically in parent-child relationships. And the best way to map them in programs is by using inheritance. The concept of inheritance remains same across all the programming languages. Inheritance uses the concept of **IS-A** relationship.  

Sub-types or sub-classes are extended from the general-type or the super-class to have all the general behaviors and features.  
We implement the super class just like we did with other classes and we use the `:` to declare the extension in the sub class.  

There are three different types of inheritance in C++. The first is public, that we use the most in general practice. And the others are protected and private.  
In **public** inheritance, all the public members of the super type will remain public in the sub type.  
Any member we've declared **private** in the super type will only be available exclusively inside the super class. To access them from the child classes, we can use getters & setters, and call them from the child class using the scope resolution operator pre-fixed with the super class.  
Anything we have declared as **protected** in the super class, will be available within the child classes.  

When we write constructors for the sub-class, we must call the constructor from the super class within it. If we do not implement a constructor for the sub class, it's going to call the DEFAULT (empty) constructor of the super class.  
If the default constructor for the super class does not exist, the compiler will give an error. Otherwise, we need to call the super class' constructor using the `:` symbol right after the parenthesis of the sub class' constructor.  
If we do not implement the sub class' constructor, the compiler will write this 
```cpp
SubCls():SuperCls() {} 
```

```cpp
#include <iostream>
#include <sstream>
#include <string>

using namespace std;

class SuperCls {
	private:
		string var1;
		int var2;
	public:
		SuperCls(string var1, int var2) {
			cout << "This will be executed first!" << endl;
			this->var1 = var1;
			this->var2 = var2;
		}
	int method1() {
	    cout << "This will be printed last!" << endl;
		return var2 * 5;
	}
};

class SubCls : public SuperCls {
	private:
		int specialVar;
	public:
		SubCls(string var1, int var2, int specialVar):SuperCls(var1, var2) {
			cout << "And then this will be printed!" << endl;
			this->specialVar = specialVar;
		}
	int method1() {		// overriding
		cout << "This will not be printed if I'm Super" << endl;
		int answer = SuperCls::method1();
		answer += specialVar;
		return answer;
	}
};

int main(){
	SubCls *p = new SubCls("Var1", 1, 5);
	int answer = p->method1();
	cout << "\nThis will be 5 in Sub, 10 in Super: " << answer << endl;
	return 0;
}
```

If we declare the `p` pointer as a `SuperCls` object, the `method1` from the `SuperCls` will be called, and the overridden method will never be executed.  
If we declare the `p` pointer `SubCls`, the `method1` from the `SubCls` will be executed, and within that we have called the `method1` from the `SuperCls`.  

If the developer of the super class implements a method as **virtual**, once we call the method, the sub class’ implementation will run. If it’s not declared as virtual, which is the default, the method of the super class will be executed, because it’s faster. This is a specialty in C++.   
The *virtual functions* are configured using the *virtual table*. This is happening behind the curtains, but if our class has a lot of virtual functions, this might cost a lot of memory and could take some time for our program to be executed.  

If we’re implementing a class that inherits another class, we can write the sub class’ constructor to call the super class’ constructor and then assign the member variables that are special to the sub class. In that way, when we instantiate the sub class, the constructor for the super class will be called (and finished executing) before the construction of the sub class ends.  
Likewise, when the destructor is called, the sub class’s destructor (the destructor of the innermost class) will be called first, and then the super class’ destructor will be called.  

# Pure Virtual Function 

If we have a function that's common among the child-classes, we can declare that in the parent class. But, what if we the behavior of that function is completely different among the child classes, and have no common behavior to implement on the parent class? Then we can declare a *purely virtual function*.  

It's a function declared in the super type, that has not implemented any behavior. So, the child types have the full responsibility of the implementation, but still, any object of that super class still can perform that function.  

We can declare a virtual method in the super type using the `virtual` keyword.
```cpp
virtual void printMyName() = 0;
```
Until we complete the implementation of a virtual function in the sub type, we cannot instantiate an object of that sub type. 

# Multiple Inheritance 

In C++, a class can inherit from multiple super classes. For an example, think about a flying video game, that has birds and air planes. We can't implement the flying functions in the Bird class. Then we'd have to repeat the code in the `AirPlane` class, and also not all birds can fly.  
What we can do is to create a `Flyable` class and declare flight methods as virtual.  
Then we should create parent class `Bird` and sub classes of different birds (e.g.- `Eagle`) that extends `Bird`.  
We also need to create an `AirPlane` class that extends the `Flyable` class, and implement the fly methods in that.  
We need to create the `Eagle` class that inherit both `Bird` and `Flyable` classes.  
If we create an `Ostrich` class, that only should extend from the `Bird` class. (In this case, the `Flyable` class has the same functionality as an Interface in Java).  
The `Flyable` must be declared as a **super most type**, so any child type can inherit from it. We can write extension from multiple classes by separating the parent types with commas after the `:` symbol. 

# Smart Pointers 

C++ have provided a collection of **smart pointers** that we could use instead of a pointer. They are objects (pointer wrappers) that would be allocated in the stack, and automatically delete the resource once it’s gone out of scope.  
This is not garbage collection, it’s deterministic destruction.  
They are generic, so we can use them with any kind of object.  

They handle copying in two ways.  
One is to prevent copying by making the copy constructor and the assignment operator private.  
The other way is by having a reference count. It keeps the count of copy increments, and decrement them when they destructed.  
They even have the overloaded operators for dereferencing and arrow operator.  

We can include the memory library of the standard library to use these pointer objects.  

### Shared Pointer 

If we’re having a resource that might get copied a few times, it’s good to use the `shared_ptr`. Shared pointers don’t have any flaws and will make sure no memory leak will happen. We don’t need to implement the copy constructor and the assignment operator anymore. We also don’t need to initialize it to `NULL` or `nullptr`, we also don’t need to worry about the deleting, which means we don’t need to write destructors in classes. We actually cannot use `delete` keyword on them. If we ever wanted to tell the `shared_ptr` to let go of the resource, we can use its member function `reset`.  
If we ever assign it to a new pointer, we cannot use the `new` keyword to dynamically allocate a new resource and assign it to the shared pointer. Instead, we need to call the `make_shared` function, declare the type and pass in the arguments to instantiate.  

```cpp
#include <memory>

std::shared_ptr<ObjectType> pMySPtr;

// use it
pMySPtr.reset();
pMySPtr = std::make_shared<ObjectType> ( /* arguments */ );
```
### Weak Pointer 

There’s also a `weak_ptr` in the memory library that works with shared pointers. Every time we copy a shared pointer, it bumps up the reference count. We can use weak pointers to keep a pointer of which existence doesn’t keep the original pointer alive, by increasing the reference count. If the object goes out of scope, weak pointer handles it nicely.  

### Unique Pointer 

There’s also a unique pointer (`unique_ptr`). This is fast and efficient. A unique pointer *exclusively owns* the object to which it points. That means, if it’s not null, it’s destructor is obligated to delete the object.  
It also cannot be copied. There is no copy constructor or copy assignment operator. There is a move method in the standard library, that we can use to move a reference into a unique pointer.  

Unique pointer provides move constructor and move assignment. With that functionality, we can implement the transfer of a pointer’s ownership, in and out of a function, which could not be done by classical C++.  
It also makes way to store pointers, elegantly and efficiently within a container.  
Smart pointers help to remove the explicit deletes. The make functions help to remove the explicit `new` keywords.  
When we use the default constructor of the `unique_ptr`, we’ll get a *null pointer*. We don’t explicitly assign it into a null pointer.  
We can get help from the `unique_ptr` class templates and use the `make_unique` function to create a unique pointer. This function even works with most user defined types, by forwarding parameters and creating them naturally and efficiently.  

```cpp
auto sp1 = unique_ptr<int> { new int { 123 } };
auto sp2 = make_unique<int>(345);
auto sp3 = movie(sp1);
```

The move function, makes the `sp1` pointer give up it’s ownership and release the object to be owned by `sp3`. We cannot use the assignment operator to do this.  

Unique pointers even allow Boolean conversion, so we could pass the pointer into a Boolean statement to check if it holds a non-null pointer.  

We can call the release method on our object, to release all the pointers attached to it. There’s also a reset method we could use to reset the ownership of an object.  

We can pass a unique pointer to a function by value. If we write a function that accepts a unique pointer of some kind by value, we need to call the move method inside the parameters when we call that function. 

```cpp
auto GetMyObj() -> unique_ptr<MyObj> {
	return make_unique<MyObj> ( /* construct */ );
}

auto TakeThisUPtr (unique_ptr<MyObj> up) -> unique_ptr<MyObj> {
	// code to update up
	return up;
}

auto main() -> int {
	auto p1 = GetMyObj();
	p1 = TakeThisUPtr (move(p1));
	return 0;
}
```

The unique pointer class allows us to override it implicit behavior of deletion. We can provide a custom implementation for the delete process. This class provides a template parameter called `deleter`. This is simply a function object that deletes the unique pointer.  

### COM Pointers 

**Windows SDK** provides the `ComPtr`, that we could use with the **COM** and *WinRT* interfaces. The Windows SDK ships with a *Visual C++ compiler*, and this com pointer is what we should use when we’re dealing directly with COM interfaces.  

*More On This To Come...*  
Advanced Microsoft Visual C++ and .Net Programming  

### Auto Pointer 

There was an *auto pointer* in the standard library, a previous attempt to make a smart pointer. It wasn’t as smart as it should be.  
It worked very poorly inside containers. The programmer had to delete each pointer explicitly when they create contained collections. Shared and unique pointers don’t have that problem. 
We can switch all the raw pointers we use into shared pointers, we can forget about memory management and just treat it like a normal object. 

### Void Pointers 

A void pointer is declared using `void*` and is very powerful, but also very dangerous functionality.  
They can point to anything. We can take any type of pointer and cast it into a void pointer, or we can cast a void pointer into any type of a pointer, without any runtime errors.  
This was used very commonly as a function parameter. But we should try to avoid it as much as we can.  

Void pointer gives up all the type safety in C++. For an example, when a function takes a void pointer as an argument, and then cast it into an integer, void pointers goes to the memory location and take the bits in that location and actually builds up an integer with it. No runtime errors or warnings are given.  

We should always try to use either polymorphism instead or a dynamic cast. With void pointers, developers have got flexibility to do almost anything with it, but they can cause errors very easily. There are no runtime checks, and even when an error is occurred, only a very little information is given by the runtime. 

### Pointers with Inheritance 

By using smart pointers in inheritance hierarchy, they would work just like raw pointers. So, we should not hesitate to use them.  
If we create a super class pointer and assign it a sub class object, when we call an overridden method, unless it’s virtual, we’d still get the super class’ implementation executed. If the function is virtual, even though we refer to it using a super class pointer, we’d get the overridden implementation executed.  
Once we use virtual functions, there will be a virtual table, which will result in a performance hit.  
If we create a super class pointer for a sub class object, and call delete, the destructor from the super class will be executed.  This could be a huge problem, if the class have any resources to close or a lock to release.  
So, some developers make all destructors virtual. But that’s not necessary, that could result in a virtual function overhead increasing even though that’s not needed.  
So, we should make the destructor virtual, if the class have any special closing up, or if there are other virtual functions already. 

If we have a sub class with more member variables than the super class, there will be slicing errors. An error could happen, when we copy a super class object into a sub class, or vice-versa. Either there will be no room to put the extra members in the super class (**slicing**), or there will be information missing in the derived class, if we try to copy an object. This is happened very commonly when objects are passed into functions.  
If we have a function that takes arguments by value and not by reference, when we pass in the wrong type, either the copy will fail or there will be a slicing.  

To avoid these errors, we need to use pointers or references. Among many solutions, using references (`&`) could keep polymorphism and still work easily with the derived members (using the dot `.`), when we try to refer to a sub class object as a super class object.  
We should not use pointers (`*`) instead, because we have to use the arrow operator to access members, and we cannot call the derived members of the sub class with it.  

# Casting 

We can use **C-style casting** to cast an object to another type. But this is very dangerous and could lead into a lot of potential errors.  
There are other types of casting in C++, that uses templates. They are relatively much safer than C style castings.  

**Static casting** is used as `static_cast<TypeToCast>` can be used instead of C style cast. They are checked at compile time. If the compiler doesn’t see a relation between two types, it’ll return an error or a warning saying the types are incompatible.  

**Dynamic cast** `dynamic_cast<TypeToCast>` has runtime checks. It relays on knowing what the type is at runtime. It only works with casting to pointer to a class that has a virtual table.  
The special thing about dynamic cast is, that it returns null if the cast fails. It’s slower to use dynamic casts, but it’s safer because it never misinterprets bits.  

There’s also a `const_cast`, that we could use to take a constant variable and cast it into a non-constant variable, so we could change it. This is not a beginner’s technique.  

There’s also a `reinterpret_cast` for bit twiddling, this involves knowing how long data types are and the pattern of bits inside the data type, and the bits and the meaning will be interpreted differently. This is really not for beginners. 

# Lambdas 

A lambda is an expression that represents some operation. We can use lambdas to improve generic work. They would be a great help when it comes to concurrency. They are extensively used for functional programming. The most common purpose is to eliminate small functions, and replace them with lambdas.  

In the `for_each` example code, we had to write a separate (tiny) print function to pass in as the third argument. It could be irritating to maintain these small functions. We can write the same `for_each` by using a lambda instead.  

```cpp
vector <int> v;
// add elements
for_each (
	v.begin(), 
	v.end(), 
	[] (int i) {cout << i << “ “ ;}
);
```

A lambda don’t necessarily have to be in a single line or a single statement. Here’s another lambda that has multiple statements. 

```cpp
vector <int> v;
// add elements
for_each (
	v.begin(), 
	v.end(), 
	[] (int i) {
		cout << i;
		if (i % 2 == 0) {
			cout << “ even” << endl;
		} else {
			Cout << “ odd“ << endl;
		}
	}
);
```

Lambdas can return a value. If the lambda is single lined, and that line is a return statement, then we do not have to specify the return type, the compiler can infer.  
But in most cases, they are multi-lined, and we’d have to specify the return type.   
`[] (int n) -> double { /* --- */ }`  This is a lambda that takes an integer, does an operation and return a double.  
The body of the lambda have to contain at least one return statement. 
For a single lined lambda, we don’t need to specify. `[] (int n) { return n*n }`

Lambdas are implemented in C++ as *anonymous function objects*. When we write a lambda, the compiler rewrites the anonymous function object for it, by overriding the bracket operators for parameters and `->` operator for return type and etc.  
The anonymous function object that’s generated for us by the compiler has member variables. These member variables hold all the values that are used inside the body of the lambda. A lambda has access to information from the calling scope, and that information is put into member variables in the anonymous function object.  
An anonymous function object is an instance of a class, and we can keep that instance in a variable, instead of passing that immediately into a function.  

The square brackets of the lambda are actually called the **capture clause**.  
Empty `[]` ones mean that the lambda doesn’t capture anything.  
If we put `[x,y]` that means, it’s capturing those by value, from the scope that’s local at the moment where the lambda is created, to be saved into the lambda’s object. Later when the lambda is executed, those member variables will be used. In that operation, copies are made for those members.  
So, even though the variables are gone out of scope, those values will be available inside the lambda. If we want to, we can capture those variables by reference.  
`[&x, &y]` When they are captured by reference, no copies are made.  
If we make a change to `x` and `y` in the lambda, that change will be reflected in the original calling scope where the values are originated. If those variables are out of scope, dangling reference issues will occur. By typing equal sign `[=]` inside the square brackets, specifies that it needs to capture everything (*the whole stack at the time*). The compiler will check to see what we actually need and write the object accordingly.  
Similarly, we can capture everything local to the calling scope by reference, by passing `[&]`.  
We can mix and match these two approaches. Some by value and some by reference.  
All these captured member variables are **constants** by default. If we want to make changes, we need to use `mutable` keyword. If the members are captured by value, the changes will only be made to the copies, and there will be no impact on the calling local scope. But if they were captured by reference, the lambda will change the original members. 

```cpp
vector <int> v;
int x = 3;
int y = 7;
// add elements
cout << “printing elements between 3 and 7” << endl;
for_each (
	v.begin(), 
	v.end(), 
	[x,y] (int n) {
		if (n >= x && n <= y) 
			cout << n << “ “; 
	}
);
```

In the below given example, we’re capturing the whole local scope by value. So, even though we’re using the `mutable` keyword, `x` and `y` will not be changed in the outer scope. Only their copies inside the anonymous function object will be changed. But since we’re taking `r` as an integer reference, the values inside the vector will be changed. 

```cpp
vector <int> v;
// add elements
x = 1;
y = 1;
for_each (
	v.begin(), 
	v.end(), 
	[=] (int& r) mutable {
		const int old = r;
		r *= 2;
		x = y;
		y = old;
	}
);
```

# Exceptions 

The simplest thing to do when we expect an error, just to perform a check before the error happens, instead using exception handling. But in some cases, the place where the problem occurs, is not the place where we could deal with it. One option is to return true if the operation succeeds and false if it doesn’t. But if there’s some value that function must return, we cannot do that. But, with the use of exceptions, we can handle expected errors without constant checks along the way.  
Once an exception is thrown, the transfer flow of the program’s execution jumps from the location where the problem occurred to the place where can handle it. The special thing is, that the intervening code is skipped. 

```cpp
try {
	vector <int> v;
	v.push_back(1);
	int j = v.at(99);
} catch (out_of_range& e) {
	cout << “out of range exception: “ << e.what();
} catch (exception& e) {
	cout << e.what();
}
```

The exception is handed to each `catch` block in turn. The first one that can handle it, gets it. The best practice is to order catch blocks by more specific exceptions first. Also, we must catch exceptions by reference, it’s great for catching derived exceptions.  

In C++, the programmer has a lot of flexibility. Back in the day, we could throw just about anything. An integer, a string or even an instance of any class could be thrown. And then we could have a catch block that catches integers or etc. So, it’s a great help to have an exceptions class in the standard library.  
The class `exception` is the base class of the hierarchy of exceptions. The commonly used exceptions are instances of classes that derived from this class.  

Standard exception is defined in the header `std::except`. It has a member function `what()` that returns a string which is useful for error messages and debugging.  
There are two main types of exceptions. 
* logic_error: domain_error, invalid_argument, length_error, out_of_range
* runtime_error: overflow_error, range_error, underflow_error 

All the derived classes of `exceptions` are just marker classes. They don’t add any new members. They have only changed the name, so we could catch them or identify them more specifically.  

To trigger (**throw**) an exception, we can use the `throw` keyword. When we caught an exception, or when we prevented an error, we could throw an exception up the stack to inform the caller. We should be as specific as we can, on our choice of what type of derived exception to throw. We can pass in a string with some information as the argument.  

If the thrown exception is caught by reference, the caller will get the benefit from our choice of being specific with the exception type. It will have information containing the given string and the type of the error. But if it was caught by value, the exception will suffer from slicing, and leave out the specified derived exception type. Even though it still has the given string information, this is very bad practice.  

There could be variable lifetime issues associated with unwinding the stack. When an exception happens, all the members that were local at that point tries go out of scope. If the exception is not handled carefully, this could lead into huge memory management errors.  

Anything inside the `try` block will go out of scope at the moment an exception is invoked. Which means, any members, constructed within the try block will be automatically destructed once an exception is thrown.  
We don’t actually need to deal with that in our catch blocks. But anything outside of the try block, will stay in the stack, even after control hits the exception.  

There are no `finally` blocks in C++. So, if we have anything dynamically allocated in the try block, we would not be able to delete it if an exception is thrown. We can’t even de-allocate it in the catch block.  
To get around this, C++ approach is to always allocate memory in the stack, so the destructor will automatically be invoked. The conclusion is to never use raw pointers in try blocks. We should always use smart pointers instead, so it would be an object, and we wouldn’t have to worry about deallocation.  

There is a cost on using exceptions. If no exception is thrown in a `try` block, it’s little to no cost. But if an exception is thrown, that could take more time to process than an `if` block. So, we should try to prevent errors using if clauses as much as we can, in small and very common inline errors and type checking kind of stuff. We should use exceptions, if it’s not a commonly identified error or if it is a rare case, or if the error handling should be passed way up the call stack, or if handling that in another way could cost just as much time. 

# Concurrency 

There are two approaches to concurrent programming.  
The first is **multiprocessing**. In this approach there are multiple processes, each process with a single thread, and the processes communicate with each other in preliminary ways such as files, pipes, message queues and etc. But it is usually slow and complicated to start a lot of processes. Also, processes take a considerable amount of overhead, so one process would not accidently step onto another process.  

The second method of concurrent programming is **multithreading**. In this approach, one process contains two or more threads, and those threads communicate with each other by using shared memory. A thread is considered to be a light weight process, so they are easy and fast to start. Threads also takes very lower overhead. Communicating through a shared memory is much faster than communicating through pipelines or files.  
The downsides of multithreading are, that they are difficult to implement, and they cannot run on distributed systems.  

```cpp
#include <iostream>
#include <thread>

using namespace std;

void function_1 () {
	std::cout << "Beauty is only skin-deep" << std::endl;
}

int main() {
	std::thread t1(function_1); 	// t1 starts running
	t1.join();						// main thread waits for t1 to finish
	return 0;
}
```

There is a `<thread>` header in `std` namespace.  
If the `t1` has a long running process, the `main` thread doesn’t need to wait for it. We can call `t1.detach();` instead of `t1.join();` . Then `t1` would run independently of the `main` thread. Then we call `t1` a '**daemon process**'.  
Some daemon processes keep running until the system shuts down. Since the *main* thread no longer have a connection with its child *t1* thread, once *t1* finishes it's execution, the runtime would have the responsibility to reclaim the resources that were allocated for *t1*.  
If the main thread finishes its execution before *t1*, we will no longer see the console output. So, if we ever have two or more threads sharing the same resource (in this case `cout`), we should keep the *main* thread running, until all the child processes finish their execution.  

Remember, we can only **join** or *detach* a thread only once. If we ever call the `join` method on a thread that is not joinable, or in other words, if the child thread object goes out of scope before we *join* or *detach* it, the program will crash.  
To avoid that, there is a `joinable()` method in thread, that returns a bool. We can check for that before we call *detach* or *join*. We still don't get do *detach* or *join* more than once, but at least in this way, the program would not crash.  
We could cover the parent process with *try-and-catch* block to make sure the child thread joins, with or without exception. Or we could use the **RAII** approach, and wrap the child thread object with a wrapper class, and have its destructor call join function. 

```cpp
class Fctor {
	public:
		void operator()(string& msg) {
			cout << "t1 says: " << msg << endl;
		}
};

int main() {
	string s = "Where there is no trust, there is no love";
	std::thread t1((Fctor()), std::move(s));
	t1.join();
	cout << "main says: " << s << endl;
	return 0;
}
```

If we're instantiating an object inside the instantiation of a thread, we need to pass the parameters to the object constructor as secondary parameters to the thread constructor. And we also need to cover the object's constructor with an additional pair of parentheses, to avoid c++ evaluating it to be a function call.  

Even if we have the object constructor asking for referenced parameters, when we pass something, it will be taken by value. Because, parameters to a thread is always taken by value.  
If we really need to pass arguments by reference, we can use `std::ref` to cover the argument (reference wrapper) that's been passed into the thread's object constructor.  

This is an example for parent and child threads sharing the same memory resource (in this case string `s`) by using references. We can achieve the same thing by using pointers. But, memory sharing could lead into data race problems.  

A better approach would be to use `std::move` function to wrap the resource. It will move the given resource from one thread to another. It's both safe and efficient. In c++ libraries, there are many things that can only be moved and cannot be copied. As a matter of fact, a thread object itself can only be moved. 
```cpp
std::thread t2 = std::move(t1);
```

Every thread has an associated id number with it. To get that we could call,
```cpp
std::this_thread::get_id()
```

This will return the id of the current thread (or the thread it's been called in). To get the id of another thread, we could call,
```cpp
t1.get_id()
```

### Over-Subscription 

We should use threads as much as we have calls. But if our hardware cannot support that much threads, our performance would degrade. This is called '**oversubscription**'. When we create more threads than available cpu cores, it would have to do a lot of contact switching. 
```cpp
std::thread::hardware_concurrency()
```
This would give us an indication of how many threads we could truly run on our hardware. 

### Race Conditions 

A **race condition** occurs when the outcome of a program depends on the relative execution order of two or more threads. We should try to avoid race conditions. One way to avoid this is by using **mutex** to synchronize the access of the common resource. 

```cpp
#include <iostream>
#include <string>
#include <thread>
#include <mutex>

using namespace std;

std::mutex mu;

void shared_print (string msg, int id) {
	mu.lock();
	cout << msg << id << endl;
	mu.unlock();
}

void function_1 () {
	for (int i=0; i>-100; i--) {
		shared_print(string("From t1: "), i);
	}
}

int main() {
	std::thread t1(function_1);
	for (int i=0; i<100; i++) {
		shared_print(string("From main: "), i);
	}
	t1.join();
	return 0;
}
```

By using mutex to synchronize a shared resource among threads, we can avoid race conditions. But, if an exception is thrown in between locking an unlocking, the resource might get locked forever. We could use a `lock_guard` to get around this.  
This is also a variant of **RAII** technique. Whenever the guard goes out of scope, the mutex will always be unlocked, with or without exception. 
```cpp
void shared_print (string msg, int id) {
	std::lock_guard<std::mutex> guard(mu);
	cout << msg << id << endl;
}
```

Still with all that, the shared resource might be available and be used from another thread, without going through the lock. To protect the resource completely, the mutex must be bundled together with the shared resource. 

```cpp
#include <iostream>
#include <string>
#include <thread>
#include <mutex>

using namespace std;

class Logfile {
	std::mutex m_mutex;
	ofstream f;
	public:
		Logfile() {
			f.open("log.txt");
		} // need a destructor to close the file, have not implemented here
		void shared_print (string id, int value) {
			std::lock_guard<mutex> locker(m_mutex);
			f << "From " << id << ": " << value << endl;
		} // we should never let f be available to the outside 
};

void function_1 (Logfile& log) {
	for (int i=0; i>-100; i--) {
		log.shared_print(string("From t1: "), i);
	}
}

int main() {
	Logfile log;
	std::thread t1(function_1, std::ref(log));
	for (int i=0; i<100; i++) {
		log.shared_print(string("From main: "), i);
	}
	t1.join();
	return 0;
}
```

### Deadlocks 

**Deadlock** is another problem that might arise, when dealing with thread synchronization with locks.  
Consider the below given code. We're using two mutexes (two locks) for the same resource for some reason. The `function_1` calls the `shared_print` method, that locks `_mu` first and then `_mu2`, and the main method calls the `shared_print2` which locks `_mu2` first and then `_mu`.  
There will be a time, in which `function_1` locks `_mu` and waiting for `_mu2` to be released, at the same time the `main` method locks `_mu2` and waiting for `_mu` to be released.  
This is a deadlock, and our program will hang from there. 

```cpp
class Logfile {
	std::mutex _mu;
	std::mutex _mu2;
	ofstream _f;
	public:
		Logfile() {
			_f.open("log.txt");
		} // need a destructor to close the file, have not implemented here
		void shared_print (string id, int value) {
			std::lock_guard<mutex> locker(_mu);
			std::lock_guard<mutex> locker2(_mu2);
			f << "From " << id << ": " << value << endl;
		}
		void shared_print2 (string id, int value) {
			std::lock_guard<mutex> locker2(_mu2);
			std::lock_guard<mutex> locker(_mu);
			f << "From " << id << ": " << value << endl;
		} 
};
```

To avoid deadlocks, we could make everything locking the mutexes in the same order. Or we could use the standard library's `standard_lock` function, which can be used to lock arbitrary number of lockable objects such as mutex, with the use of deadlock avoiding algorithms. 

```cpp
class Logfile {
	std::mutex _mu;
	std::mutex _mu2;
	ofstream _f;
	public:
		Logfile() {
			_f.open("log.txt");
		} // need a destructor to close the file, have not implemented here
		void shared_print (string id, int value) {
			std::lock(_mu, _mu2);
			std::lock_guard<mutex> locker(_mu, std::adopt_lock);
			std::lock_guard<mutex> locker2(_mu2, std::adopt_lock);
			f << "From " << id << ": " << value << endl;
		}
		void shared_print2 (string id, int value) {
			std::lock(_mu, _mu2);
			std::lock_guard<mutex> locker2(_mu2, std::adopt_lock);
			std::lock_guard<mutex> locker(_mu, std::adopt_lock);
			f << "From " << id << ": " << value << endl;
		} 
};
```

`std::adopt_lock` tells the locker, the mutex is already locked and to adopt to the ownership of that mutex, so when the locker goes out of scope, it should unlock the mutex.  

There is a `unique_lock`, which is similar to `lock_guard` but it gives more flexibility to implement a *finer-grained* lock.  
When we use a unique lock, instead of a lock guard, we can construct the locker, without actually locking the mutex. To do that, we need pass in a second parameter of `std::defer_lock`. When we do that, the given mutex is owned by the locker (unique lock), but the mutex is not locked. So, we're able to do something else, that doesn't use the shared resource.  
When we do need to lock it, we can call `locker.lock()` method. And if we need to do something else again, that doesn't use the shared resource, we can call `locker.unlock()` method. We can repeat locking and unlocking as much as we like. This functionality is not given by `lock_guard`. 

```cpp
class Logfile {
	std::mutex _mu;
	ofstream _f;
	public:
		Logfile() {
			_f.open("log.txt");
		} // need a destructor to close the file, have not implemented here
		void shared_print (string id, int value) {
			std::unique_lock<mutex> locker(_mu, std::defer_lock);
			// do something else
			locker.lock();
			f << "From " << id << ": " << value << endl;
			locker.unlock();
			// ...
		}
};
```

A wrapper class of a mutex cannot be copied. However, a unique lock can be moved. When we do move a unique lock, the ownership of the mutex transfers from one unique lock to another unique lock. But a lock guard can never be moved.  
But the downside of a unique lock is that it's a little bit heavier than a lock guard. So, if we have a concern on performance, we should use a lock guard instead.  

### Producer - Consumer Problems 

If there are two threads sharing a resource, there could be a *producer-consumer* problem even if we used mutex and unique locks.  
To get around that, we can use a condition variable and use its notify functions. 
`notify_one()` will wake up one thread, if there is any waiting on that condition. 

```cpp
std::deque<int> q;
std::mutex mu;
std::condition_variable cond;

void function_1() {
	int count = 10;
	while (count > 0) {
		std::unique_lock<mutex> locker(mu);
		q.push_front(count);
		locker.unlock();
		cond.notify_one();
		std::this_thread::sleep_for(chrono::seconds(1));
		cound--;
	}
}

void function_2() {
	int data = 0;
	std::unique_lock<mutex> locker(mu);
	cond.wait(locker, [](){return !q.empty();});
	data = q.back();
	q.pop_back();
	locker.unlock();
	cout << "t2 got the value from t1: " << data << endl;
}

int main() {
	std::thread t1(function_1);
	std::thread t2(function_2);
	t1.join();
	t2.join();
	return 0;
}
```

We're sending the locker into the `cond.wait` because, we don't need to lock something while that thread's obviously sleeping. This way, it will release the lock and go to sleep, and once it's been awakened by the other thread, it will again lock the mutex. Since we have to lock and unlock the mutex many times, we have to use unique lock.  

The lock could be awakened by itself while sleeping and waiting for the other thread to notify. That is called a '**spurious wake**'. If that happens, we don't need that thread to keep executing. To ensure that, we can pass a predicate to the wait function to check if the `q` is empty.  

### Fututre & Promise 

There is an `async` method in `std` that we could use in small occasions where we need a thread to do just a simple job. It doesn't return a thread, it returns a **future**. A future is a channel that we could use to receive data from a child thread. It's `get()` function will wait for the child thread to finish, and return the result. 

```cpp
#include <future>

using namespace std;

int factorial (int N) {
	int res = 1;
	for (int i=N; i>1; i--) {
		res *= i;
	}
	cout << "Result is: " << res << endl;
	return res;
}

int main() {
	int x;
	std::future<int> fu = std::async(factorial, 4);
	x = fu.get();
	return 0;
}
```

A **future** object represents an object by using which we can get something in the future. It can only call `get()` function once.  But the async function will not always kick off another thread. If we call it with this, 
```cpp
std::future<int> fu = std::async(std::launch::deferred, factorial, 4);
```
It will not create a thread. What it will do now is, it will defer the execution of the factorial function, until later when it actually asks for the result by calling `get()`. And it will be executed on the same thread.  

If we do this, 
```cpp
std::future<int> fu = std::async(std::launch::async, factorial, 4);
```
It will create another thread. We could also call both of those by doing, 
```cpp
std::future<int> fu = std::async(std::launch::async | std::launch::deferred, factorial, 4);
```
In this case, the implementation will determine whether it should kick off another thread or not. It is also what's happening by default.  
We can also use a future to pass a value from the parent thread to the child thread, not at the time of creating the thread, but at some point, in the future. For that we also need a **promise**.  

```cpp
#include <future>

using namespace std;

int factorial (std::future<int>& f) {
	int res = 1;
	int N = f.get();
	for (int i=N; i>1; i--) {
		res *= i;
	}
	cout << "Result is: " << res << endl;
	return res;
}

int main() {
	int x;
	std::promise<int> p;
	std::future<int> f = p.get_future();
	std::future<int> fu = std::async(std::launch::async, factorial, 4, std::ref(f));
	// do something
	std::this_thread::sleep_for(chrono::milliseconds(20));
	p.set_value(4);
	x = fu.get();
	return 0;
}
```

When we call `get_future()` on the *promise*, it will return a *future*. We can pass it by reference to the child thread, and when the child thread needs the promised value, it will wait for it to be set by the parent thread.  

If the parent thread do not set the promise, the `f.get()` function will get an exception: `std::future::errc::broken_promise`. And if we really cannot set a value, we can set an exception. 
```cpp
p.set_exception(std::make_exception_ptr(std::runtime_error("To err is human")));
```
So now, when the child thread calls the get function, it will get this runtime error, instead of the infamous `broken_promise` exception.  

Promises and futures can also only be moved. They cannot be copied.  

If we need to call this factorial function multiple times, on multiple threads, we can use a shared future, instead of creating multiple futures and multiple promises. Shared future can also be copied, so we don't have to pass it by reference. When parent set the value to be 4 on promise, all the children will get that value. 

```cpp
#include <future>

using namespace std;

int factorial (std::shared_future<int> sf) {
	int res = 1;
	int N = f.get();
	for (int i=N; i>1; i--) {
		res *= i;
	}
	cout << "Result is: " << res << endl;
	return res;
}

int main() {
	int x;
	std::promise<int> p;
	std::future<int> f = p.get_future();
	std::shared_future<int> sf = f.share();
	std::future<int> fu = std::async(std::launch::async, factorial, 4, sf);
	std::future<int> fu2 = std::async(std::launch::async, factorial, 4, sf);
	std::future<int> fu3 = std::async(std::launch::async, factorial, 4, sf);
	p.set_value(4);
	return 0;
}
```
