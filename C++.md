# C++

## 1. C++ Basics

### 1.4 Variable assignment and initialization

There are **6 basic ways** to initialize variables in C++:

```c++
int a;         // no initializer (default initialization)
int b = 5;     // initial value after equals sign (copy initialization)
int c( 6 );    // initial value in parenthesis (direct initialization)

// List initialization methods (C++11) (preferred)
int d { 7 };   // initial value in braces (direct list initialization)
int e = { 8 }; // initial value in braces after equals sign (copy list initialization)
int f {};      // initializer is empty braces (value initialization)
```

### 1.6 Uninitialized variables and undefined behavior

Unlike some programming languages, C/C++ does not automatically initialize most variables to a given value (such as zero). The default value of a variable that is not initialized is whatever (garbage) value happens to already be in that memory address.A variable that has not been given a known value (through initialization or assignment) is called an **uninitialized variable**.





## 2. C++ Basics: Functions and Files

### 2.1 Introduction to functions

***Definition***: 

- A **function** is a resuable sequence of statements designed to do a particular job.

- A **function call** is an expression that tells the CPU to interrupt the current function and execute another function.

All user-defined functions will take the following form:

```c++
returnType functionName() // This is the function header (tells the compiler about the existence of the function)
{
    // This is the funciton body (tells the compiler what the function does)
}
```

### 2.3 Void functions



### 2.11 Header files

#### The #include order of header files

To maximize the chance that missing includes will be flagged by compiler, order your #includes as follows:

1. The paired header file
2. Other headers from your project
3. Third party library headers
4. Standard library headers

The header for each grouping should be sorted alphabetically (unless the documentation for a 3rd party library instructs you to do otherwise).

#### A few recommendations for creating and using header files

- Always include header guards.
- Do not define variables and functions in header files.
- Give a header file the same name as the source file it's associated with (e.g. `grades.h` is paired with `grades.cpp`).
- Each header file should have a specific job, and be as independent as possible.
- Be mindful of which headers you need to explicitly include for the functionality that you are using in your code files, to avoid inadvertent transitive includes.
- A header file should #include any other headers containing functionality it needs. Such a header should compile successfully when #included into a .cpp file by itself.
- Only #include what you need (don't include everything just because you can).
- Do not #include .cpp files.
- Prefer putting documentation on what something does or how to use it in the header. It's more likely to be seen there. Documentation describing how something works should remain in the source files.



### 2.12 Header guards

**Header guards** (also called **include guards**) are conditional compilation directives that take the following form:

```c++
#ifndef SOME_UNIQUE_NAME_HERE
#define SOME_UNIQUE_NAME_HERE

// your declarations (and certain types of definitions) here

#endif
```

*SOME_UNIQUE_NAME_HERE* can be any name you want, but by convention is set to **the full filename of the header file, typed in all caps**, using underscores for spaces or punctuation.

In large programs, it's possible to have two separate header files (included from different directories) that end up having the same filename (e.g. direcotryA\config.h and directoryB\config.h). Considering this, some good suggestions are a naming convention of PROJECT_PATH_FILE_H, FILE_LARGE-RANDOM-NUMBER_H, or FILE_CREATION-DATA_H.

#### #pragma once

Modern compilers support a simpler, alternate form of header guards using the `#pragma` preprocessor directive.

There is one known case where `#pragma once` will typically fail. If a header file is copied so that it exists in multiple places on the file system, if somehow both copies of the header get included, header guards will successfully de-dupe the identical headers, but `#pragma once` won’t (because the compiler won’t realize they are actually identical content).



### 2.13 How to design your first programs



### 2.14 Chapter review

- 



## 3. Debugging C++ Programs

### 3.1 Syntax and semantic errors







## 4. Fundamental Data Types

### 4.1 Data types

Because all data on a computer is just a sequence of bits, we use a **data type** (often called a "type" for short) to tell the compiler how to interpret the contents of memory in some meaningful way.

C++'s **fundamental data types**, or informally called **basic types**, **primitive types**, or **built-in types**.

| Types                                                        | Category             | MEANING                                          | EXAMPLE |
| ------------------------------------------------------------ | -------------------- | ------------------------------------------------ | ------- |
| float<br />double<br />long double                           | Floating Point       | a number with a fractional part                  | 3.14159 |
| bool                                                         | Integral (Boolean)   | true or false                                    | true    |
| char<br />wchar_t<br />char8_t (C++20)<br />char16_t (C++11)<br />char32_t (C++11) | Integral (Character) | a single character of text                       | 'c'     |
| short int<br />int<br />long int<br />long long int (C++11)  | Integral (Integer)   | positive and negative whole numbers, including 0 | 64      |
| std::nullptr_t (C++11)                                       | Null Pointer         | a null pointer                                   | nullptr |
| void                                                         | Void                 | no type                                          | n/a     |

**The string type**

In C++, strings aren't a fundamental type (they're a compound type).

**The _t suffix**

Many of the types defined in newer versions of C++ (e.g. std::nullptr_t) use a _t suffix. This suffix means "type", and it's a common nomenclature applied to modern types.



### 4.2 Void

**Void** is an **incomplete type**.

An **incomplete type** is a type that has been declared but not yet defined. The compiler knows about the existence of such types, but does not have enough information to determine how much memory to allocate for objects of that type.

Void is intentionally incomplete since it represents the lack of a type, and thus cannot be defined.

Incomplete types can not be instantiated:

```c++
void value; // won't work, variables can't be defined with incomplete type void
```

Most commonly, *void* is used to indicate that a function does not return a value.



### 4.3 Object sizes and the sizeof operator

| CATEGROY       | Type           | Minimum size | typical size       | note                  |
| -------------- | -------------- | ------------ | ------------------ | --------------------- |
| Boolean        | bool           | 1 byte       | 1 byte             |                       |
| character      | char           | 1 byte       | 1 byte             | always exactly 1 byte |
|                | wchar_t        | 1 byte       | 2 or 4 bytes       |                       |
|                | char8_t        | 1 byte       | 1 byte             |                       |
|                | char16_t       | 2 bytes      | 2 bytes            |                       |
|                | char32_t       | 4 bytes      | 4 bytes            |                       |
| integer        | short          | 2 bytes      | 2 bytes            |                       |
|                | int            | 2 bytes      | 4 bytes            |                       |
|                | long           | 4 bytes      | 4 or 8 bytes       |                       |
|                | long long      | 8 bytes      | 8 bytes            |                       |
| floating point | float          | 4 bytes      | 4 bytes            |                       |
|                | double         | 8 bytes      | 8 bytes            |                       |
|                | long double    | 8 bytes      | 8, 12, or 16 bytes |                       |
| pointer        | std::nullptr_t | 4 bytes      | 4 or 8 bytes       |                       |

**The sizeof operator**

The **sizeof operator** is a unary operator that takes either a type or a variable, and returns its size in bytes.

```c++
#include <iomanip> // for std::setw (which sets the width of the subsequent output)
#include <iostream>

int main()
{
    std::cout << std::left; // left justify output
    std::cout << std::setw(16) << "bool:" << sizeof(bool) << " bytes\n";
    std::cout << std::setw(16) << "char:" << sizeof(char) << " bytes\n";
    std::cout << std::setw(16) << "short:" << sizeof(short) << " bytes\n";
    std::cout << std::setw(16) << "int:" << sizeof(int) << " bytes\n";
    std::cout << std::setw(16) << "long:" << sizeof(long) << " bytes\n";
    std::cout << std::setw(16) << "long long:" << sizeof(long long) << " bytes\n";
    std::cout << std::setw(16) << "float:" << sizeof(float) << " bytes\n";
    std::cout << std::setw(16) << "double:" << sizeof(double) << " bytes\n";
    std::cout << std::setw(16) << "long double:" << sizeof(long double) << " bytes\n";

    return 0;
}
```

Result in windows:

```
bool:           1 bytes
char:           1 bytes
short:          2 bytes
int:            4 bytes
long:           4 bytes
long long:      8 bytes
float:          4 bytes
double:         8 bytes
long double:    8 bytes
```

Trying to use `sizeof` on an incomplete type (such as `void`) will result in a compilation error.



### 4.4 Signed integers

C++ has 4 primary fundamental integer types available for use:

| Type          | Minimum size | note                                      |
| ------------- | ------------ | ----------------------------------------- |
| short int     | 16 bits      |                                           |
| int           | 16 bits      | Typically 32 bits on modern architectures |
| long int      | 32 bits      |                                           |
| long long int | 64 bits      |                                           |

**Overflow** will result in undefined behavior.



### 4.5 Unsigned integers, and why to avoid them

To define an unsigned integer, we use the *unsigned* keyword.

```c++
unsigned shrot us;
unsigned int ui;
unsigned long ul;
unsigned long long ull;
```

**Unsigned integer overflow**

If an unsigned value is out of range, it is divided by one greater than the largest number of the type, and only the remainder kept.

The number `280` is too big to fit in our 1-byte range of 0 to 255. 1 greater than the largest number of the type is 256. Therefore, we divide 280 by 256, getting 1 remainder 24. The remainder of 24 is what is stored.

An example using 2-byte shorts:

```c++
#include <iostream>

int main()
{
    unsigned short x{ 65535 }; // largest 16-bit unsigned value possible
    std::cout << "x was: " << x << '\n';

    x = 65536; // 65536 is out of our range, so we get modulo wrap-around
    std::cout << "x is now: " << x << '\n';

    x = 65537; // 65537 is out of our range, so we get modulo wrap-around
    std::cout << "x is now: " << x << '\n';

    return 0;
}
```

The output is:

```c++
x was: 65535
x is now: 0
x is now: 1
```

The other result:

```c++
#include <iostream>

int main()
{
    unsigned short x{ 0 }; // smallest 2-byte unsigned value possible
    std::cout << "x was: " << x << '\n';

    x = -1; // -1 is out of our range, so we get modulo wrap-around
    std::cout << "x is now: " << x << '\n';

    x = -2; // -2 is out of our range, so we get modulo wrap-around
    std::cout << "x is now: " << x << '\n';

    return 0;
}
```

The output is:

```c++
x was: 0
x is now: 65535
x is now: 65534
```

**Why to avoid unsigned integers**

Because of two behaviors that can cause problems, developers should generally avoid unsigned integers:

1. With unsigned numbers, it is much easier to overflow the bottom of the range, because the bottom of the range is 0, which is close to where the majority of our values are.

2. Unexpected behavior can result when you mix signed and unsigned integers. In C++, if a mathematical operation has one signed integer and one unsigned integer, the signed integer will usually be converted to an unsigned integer. And the result will thus be unsigned.

   One example:

   ```c++
   #include <iostream>
   
   // assume int is 4 bytes
   int main()
   {
   	unsigned int u{ 2 };
   	signed int s{ 3 };
   
   	std::cout << u - s << '\n'; // 2 - 3 = 4294967295
   
   	return 0;
   }
   ```

   Another example:

   ```c++
   #include <iostream>
   
   // assume int is 4 bytes
   int main()
   {
       signed int s { -1 };
       unsigned int u { 1 };
   
       if (s < u) // -1 is implicitly converted to 4294967295, and 4294967295 < 1 is false
           std::cout << "-1 is less than 1\n";
       else
           std::cout << "1 is less than -1\n"; // this statement executes
   
       return 0;
   }
   ```

**When should you use unsigned numbers?**

1. Unsigned numbers are preferred when dealing with bit manipulation.
2. Array indexing.
3. When developing for an embedded system or some other processor/memory limited context.



### 4.6 Fixed-width integers and size_t

**Why isn't the size of the integer variables fixed?**

The short answer is that this goes back to the early days of C, when computers were slow and performance was of the utmost concern. C opted to intentionally leave the size of an integer open so that the compiler implementers could pick a size for int that performs best on the target computer architecture.

**Fixed-width integers**

To address the above issues, C99 defined a set of **fixed-width integers** (in the stdint.h header) that are guaranteed to be the same size on any architecture.

These are defined as follows:

| Name          | TYPE            | RANGE                                                  | NOTES                                          |
| ------------- | --------------- | ------------------------------------------------------ | ---------------------------------------------- |
| std::int8_t   | 1 byte signed   | -128 to 127                                            | Treated like a signed char on many systems.    |
| std::uint8_t  | 1 byte unsigned | 0 to 255                                               | Treated like an unsigned char on many systems. |
| std::int16_t  | 2 byte signed   | -32,768 to 32,767                                      |                                                |
| std::uint16_t | 2 byte unsigned | 0 to 65,535                                            |                                                |
| std::int32_t  | 4 byte signed   | -2,147,483,648 to 2,147,483,647<br />$-2.1e^9 -2.1e^9$ |                                                |
| std::uint32_t | 4 byte unsigned | 0 to 4,294,967,295<br />$0 - 4.2e^9$                   |                                                |
| std::int64_t  | 8 byte signed   | $-9.2e^{18} - 9.2e^{18}$                               |                                                |
| std::uint64_t | 8 byte unsigned | $0 - 1.8e^{19}$                                        |                                                |

C++ officially adopted these fixed-width integers as part of C++11. They can be accessed by including the `<cstdint>` header, where they are defined inside the *std* namespace.

```c++
#include <cstdint> // for fixed-width integers
#include <iostream>

int main()
{
    std::int16_t i{5};
    std::cout << i << '\n';
    return 0;
}
```

The fixed-width integers have two downsides that are typically raised.

1. The fixed-width integers are not guaranteed to be defined on all architectures. However, given that most modern architectures have standardized around 8/16/32/64-bit variables, this is unlikely to be a problem unless your program needs to be portable to some exotic mainframe or embedded architectures.
2. If you use a fixed-width integer, it may be slower than a wider type on some architectures.For example, if you need an integer that is guaranteed to be 32-bits, you might decide to use std::int32_t, but your CPU might actually be faster at processing 64-bit integers.

**Fast and least integers**

To help address the above downsides, C++ also defines two alternative sets of integrs that are guaranteed to be defined.

- **The fast types (std::int_fast#\_t and std::uint_fast#\_t)** provide the fastest signed/unsigned integer type with a width of at least # bits (where # = 8, 16, 32, 64).
- **The least types (std::int\_least#\_t and std::uint\_least#\_t)** provide the smallest signed/unsigned integer type with a width of at least # bits (where # = 8, 16, 32 or 64).

An example:

```c++
#include <cstdint> // for fast and least types
#include <iostream>

int main()
{
	std::cout << "least 8:  " << sizeof(std::int_least8_t) * 8 << " bits\n";
	std::cout << "least 16: " << sizeof(std::int_least16_t) * 8 << " bits\n";
	std::cout << "least 32: " << sizeof(std::int_least32_t) * 8 << " bits\n";
	std::cout << '\n';
	std::cout << "fast 8:  " << sizeof(std::int_fast8_t) * 8 << " bits\n";
	std::cout << "fast 16: " << sizeof(std::int_fast16_t) * 8 << " bits\n";
	std::cout << "fast 32: " << sizeof(std::int_fast32_t) * 8 << " bits\n";

	return 0;
}
```

```
least 8:  8 bits
least 16: 16 bits
least 32: 32 bits

fast 8:  8 bits
fast 16: 32 bits
fast 32: 32 bits
```

However, these fast and least integers have their own downsides:

1. Not many programmers actually use them, and a lack of familiarity can lead to errors.

2. The fast types can lead to memory wastage, as their actual size may be larger than indicated by their name.

3. Because the size of the fast/least integers can vary, it's possible that your  program may exhibit different behaviors on architectures where they resolve to different sizes.

   ```c++
   #include <cstdint>
   #include <iostream>
   
   int main()
   {
       std::uint_fast16_t sometype { 0 };
       sometype = sometype - 1; // intentionally overflow to invoke wraparound behavior
   
       std::cout << sometype << '\n';
   
       return 0;
   }
   ```

**Best practice**

- Prefer `int` when the size of integer doesn't matter and the variable is short-lived.
- Prefer `std::int#_t` when storing a quantity that needs a guaranteed range.
- Prefer `std::uint#_t` when doing bit manipulation or where well-defined wrap-around behavior is required.

**Avoid the following when possible**

- `short` and `long` integers -- use a fixed-width type instead.
- Unsigned types for holding quantities.
- The 8-bit fixed-width integer types.
- The fast and least fixed-width types.
- Any compiler-specific fixed-width integers.

**The std::size_t**

The `sizeof` operator returns a value of type `std::size_t`, which is defined as an unsigned implementation-defined integral type, and it is typically used to represent the size or length of objects.

`std::size_t` is defined in a number of different headers.  <cstddef> is the best one to include, as it contains the least number of other defined identifiers.

`sizeof` must be able to return the size of an object (in bytes) using a value of type `std::size_t`. Therefore, the largest object creatable on a system has a size (in bytes) equal to the largest value `std::size_t` can hold. If it were possible to create a larger object, `sizeof` would not be able to return its size, as it would overflow the range of `std::size_t`.



### 4.7 Floating point numbers

There are three different floating point data types: **float**, **double**, and **long double**.

| category       | Type        | minimum size | typical size       |
| -------------- | ----------- | ------------ | ------------------ |
| floating point | float       | 4 bytes      | 4 bytes            |
|                | double      | 8 bytes      | 8 bytes            |
|                | long double | 8 bytes      | 8, 12, or 16 bytes |

```c++
int x{5};      // 5 means integer
double y{5.0}; // 5.0 is a floating point literal (no suffix means double type by default)
float z{5.0f}; // 5.0 is a floating point literal, f suffix means float type
```

==Note==: By default, floating point literals default to type double. An *f* suffix is used to denote a literal of type float.

**Printing floating point numbers**

```c++
#include <iostream>

int main()
{
	std::cout << 5.0 << '\n';
	std::cout << 6.7f << '\n';
	std::cout << 9876543.21 << '\n';

	return 0;
}
```

The results:

```
5
6.7
9.87654e+06
```

**Floating point range**

| size                                    | Range                                                        | precision                              |
| --------------------------------------- | ------------------------------------------------------------ | -------------------------------------- |
| 4 bytes                                 | $\pm1.18\times10^{-38 }- \pm3.4\times10^{38} and\ 0.0$       | 6-9 significant digits, typically 7    |
| 8 bytes                                 | $\pm 2.23 \times10^{-308 }- \pm 1.80 \times10^{308} and\ 0.0$ | 15-18 significant digits, typically 16 |
| 80-bits (typically uses 12 or 16 bytes) | $\pm 3.36 \times10^{-4392 }- \pm 1.18 \times10^{4392} and\ 0.0$ | 18-21 significant digits               |
| 16 bytes                                | $\pm 3.36 \times10^{-4392 }- \pm 1.18 \times10^{4392} and\ 0.0$ | 33-36 significant digits               |

The **precision** of a floating point type defines how many significant digits it can represent without information loss.

A floating point type can only precisely represent a certain number of significant digits. Using a value with more significant digits than the minimum may result in the value being stored inexactly.

**Outputing floating point values**

When outputting floating point numbers, std::cout has a default precision of 6 -- that is, it assumes all floating point variables are only significant to 6 digits (the minimum precision of a float), and hence it will truncate anything after that.

An example:

```c++
#include <iostream>

int main()
{
    std::cout << 9.87654321f << '\n';
    std::cout << 987.654321f << '\n';
    std::cout << 987654.321f << '\n';
    std::cout << 9876543.21f << '\n';
    std::cout << 0.0000987654321f << '\n';

    return 0;
}
```

The output is:

```
9.87654
987.654
987654
9.87654e+006
9.87654e-005
```

Also note that std::cout will switch to outputting numbers in scientific notation in some cases. Depending on the compiler, the exponent will typically be padded to a minimum number of digits, which is compiler-specific (Visual Studio uses 3, some others use 2 as per the C99 standard).

 We can override the default precision that `std::cout` shows by using an `output manipulator` function named `std::setprecision()`.

**Output manipulators** alter how data is output, and are defined in the *iomanip* header.

An example:

```c++
#include <iomanip> // for output manipulator std::setprecision()
#include <iostream>

int main()
{
    std::cout << std::setprecision(17); // show 17 digits of precision
    std::cout << 3.33333333333333333333333333333333333333f <<'\n'; // f suffix means float
    std::cout << 3.33333333333333333333333333333333333333 << '\n'; // no suffix means double

    return 0;
}
```

Outputs:

```
3.3333332538604736
3.3333333333333335
```

Precision issues don't just impact fractional numbers, they impact any number with too many significant digits. When precision is lost because a number can't be stored precisely, this is called a **rounding error**.

```c++
#include <iomanip> // for std::setprecision()
#include <iostream>

int main()
{
    float f { 123456789.0f }; // f has 10 significant digits
    std::cout << std::setprecision(9); // to show 9 digits in f
    std::cout << f << '\n';

    return 0;
}
```

Output:

```
123456792
```

Consequently, one has to be careful when using floating point numbers that require more precision than the variables can hold.

**Rounding errors make floating point comparisons tricky**

An example:

```c++
#include <iomanip> // for std::setprecision()
#include <iostream>

int main()
{
    std::cout << std::setprecision(17);

    double d1{ 1.0 };
    std::cout << d1 << '\n';

    double d2{ 0.1 + 0.1 + 0.1 + 0.1 + 0.1 + 0.1 + 0.1 + 0.1 + 0.1 + 0.1 }; // should equal 1.0
    std::cout << d2 << '\n';

    if (d1 == d2) {
        std::cout << 1 << '\n';
    } else {
        std::cout << 0 << '\n';
    }

    return 0;
}
```

Outputs:

```
1
0.99999999999999989
0
```

Rounding errors occur when a number can’t be stored precisely. This  can happen even with simple numbers, like 0.1. Therefore, rounding  errors can, and do, happen all the time. Rounding errors aren’t the  exception -- they’re the norm. Never assume your floating point numbers  are exact.

A corollary of this rule is: be wary of using floating point numbers for financial or currency data

**NaN and Inf**

There are two special categories of floating point numbers. The first is **Inf**, which represents infinity. Inf can be positive or negative. The second is **NaN**, which stands for “Not a Number”. Both are platform specific.

An example:

```c++
#include <iostream>

int main()
{
    double zero {0.0};
    double posinf { 5.0 / zero }; // positive infinity
    std::cout << posinf << '\n';

    double neginf { -5.0 / zero }; // negative infinity
    std::cout << neginf << '\n';

    double nan { zero / zero }; // not a number (mathematically invalid)
    std::cout << nan << '\n';

    return 0;
}
```

Outputs:

```
inf
-inf
-nan
```



### 4.8 Boolean values

Boolean variables are variables that can have only two possible values: *true*, and *false*.

```c++
bool b;
```

To initialize or assign a *true* or *false* value to a Boolean variable, we use the keywords **true** and **false**.

```c++
bool b1 {true};
bool b2 {false};
b1 = false;
bool b3{}; // default initialize to false
```

Boolean values are stored as integers and are considered an integral type (true becomes the integer 1, and false becomes the integer 0).

**Printing Boolean values**

When we print Boolean values, std::cout prints *0* for *false*, and *1* for *true*:

```c++
#include <iostream>

int main()
{
    std::cout << true << '\n'; // true evaluates to 1
    std::cout << !true << '\n'; // !true evaluates to 0

    bool b {false};
    std::cout << b << '\n'; // b is false, which evaluates to 0
    std::cout << !b << '\n'; // !b is true, which evaluates to 1
    return 0;
}
```

Outputs:

```
1
0
0
1
```

If you want std::cout to print “true” or “false” instead of 0 or 1, you can use *std::boolalpha*. Here’s an example:

```c++
#include <iostream>

int main()
{
    std::cout << true << '\n';
    std::cout << false << '\n';

    std::cout << std::boolalpha; // print bools as true or false

    std::cout << true << '\n';
    std::cout << false << '\n';
    return 0;
}
```

Outputs:

```
1
0
true
false
```

You can use *std::noboolalpha* to turn it back off.

**Integer to Boolean conversion**

When using uniform initialization, you can initialize a variable using integer literals `0` (for `false`) and `1` (for `true`) (but you really should be using `false` and `true` instead). Other integer literals cause compilation errors:

```c++
#include <iostream>

int main()
{
	bool bFalse { 0 }; // okay: initialized to false
	bool bTrue  { 1 }; // okay: initialized to true
	bool bNo    { 2 }; // error: narrowing conversions disallowed

	std::cout << bFalse << bTrue << bNo << '\n';

	return 0;
}
```

However, in any context where an integer can be converted to a Boolean, the integer `0` is converted to `false`, and any other integer is converted to `true`.

```c++
#include <iostream>

int main()
{
	std::cout << std::boolalpha; // print bools as true or false

	bool b1 = 4 ; // copy initialization allows implicit conversion from int to bool
	std::cout << b1 << '\n';

	bool b2 = 0 ; // copy initialization allows implicit conversion from int to bool
	std::cout << b2 << '\n';


	return 0;
}
```

Outputs:

```
true
false
```

If we comment out line 5, the output will be:

```
1
0
```

**Inputting Boolean values**

An example:

```c++
#include <iostream>

int main()
{
	bool b{}; // default initialize to false
	std::cout << "Enter a boolean value: ";
	std::cin >> b;
	std::cout << "You entered: " << b << '\n';

	return 0;
}
```

Output:

```
Enter a Boolean value: true
You entered: 0
```

It turns out that *std::cin* only accepts integers for Boolean variables: 0 for false and others for true. 

In this case, because we entered *true*, *std::cin* silently failed. A failed input will also zero-out the variable, so *b* also gets assigned value *false*. Consequently, when *std::cout* prints a value for *b*, it prints 0.

To allow *std::cin* to accept “false” and “true” as inputs, the *std::boolalpha* option has to be enabled:

```c++
#include <iostream>

int main()
{
	bool b{};
	std::cout << "Enter a boolean value: ";

	// Allow the user to enter 'true' or 'false' for boolean values
	// This is case-sensitive, so True or TRUE will not work
	std::cin >> std::boolalpha;
	std::cin >> b;

	std::cout << "You entered: " << b << '\n';

	return 0;
}
```

However, when *std::boolalpha* is enabled, “0” and “1” will no longer be interpreted as Booleans inputs (they both resolve to “false” as does any non-“true” input).

==Note==: Enabling `std::boolalpha` will only allow lower-cased “false” or “true” to be accepted. Variations with capital letters will not be accepted.



### 4.9 Chars

The **char** data type was designed to hold a single `character`. A **character** can be a single letter, number, symbol, or whitespace.

The char data type is an integral type, meaning the underlying value is stored as an integer. Similar to how a Boolean value `0` is interpreted as `false` and non-zero is interpreted as `true`, the integer stored by a `char` variable are intepreted as an `ASCII character`.

**Char size, range, and default sign**

Char is defined by C++ to always be 1 byte in size. By default, a  char may be signed or unsigned (though it’s usually signed). If you’re  using chars to hold ASCII characters, you don’t need to specify a sign  (since both signed and unsigned chars can hold values between 0 and  127).

If you’re using a char to hold small integers (something you  should not do unless you’re explicitly optimizing for space), you  should always specify whether it is signed or unsigned. A signed char  can hold a number between -128 and 127. An unsigned char can hold a  number between 0 and 255.

**Avoid multicharacter literals**

For backwards compatibility reasons, many C++ compilers support multicharacter literals, which are char literals that contain multiple characters (e.g. `'56'`). If supported, these have an implementation-defined value (meaning it varies depending on the compiler). Because they are not part of the C++ standard, and their value is not strictly defined, multicharacter literals should be avoided.

An example:

```c++
#include <iostream>

int add(int x, int y)
{
	return x + y;
}

int main()
{
	std::cout << add(1, 2) << '/n';

	return 0;
}
```

Output:

```
312142
```

The issue here is that the programmer accidentally used `'/n'` (a multicharacter literal consisting of a forward slash and an 'n' character) instead of `'\n'` (the escape sequence for a newline). The program first prints 3 (the result of add(1, 2)) correctly. But then it prints the value of `'/n'`, which on the author’s machine had the implementation-defined value `12142`.

**The other char types, `wchar_t`, `char8_t`, `char16_t`, and `char32_t`**

`wchar_t` should be avoided in almost all cases (except when interfacing with the Windows API). Its size is implementation defined, and is not reliable. It has largely been deprecated.

`char16_t` and `char32_t` were added to C++11 to provide explicit support for 16-bit and 32-bit Unicode characters. These char types have the same size as `std::uint_least16_t` and `std::uint_least32_t` respectively (but are distinct types). `char8_t` was added in C++20 to provide support for 8-bit Unicode (UTF-8). It is a distinct type that uses the same representation as `unsigned char`.

### 4.10 Intorduction to type conversion and static_cast

**Implicit type conversion**

In most cases, C++ will allow us to convert values of one fundamental type to another fundamental type. The process of converting a value from one type to another type is called **type conversion**.

When the compiler does type conversion on our behalf without us explicitly asking, we call this **implicit type conversion**.

**Type conversion produces a new value**

Even though it is called a conversion, a type conversion does not actually change the value or type of the value being converted. Instead, the value to be converted is used as input, and the conversion results in a new value of the target type (via direct initialization).

**An introduction to explicit type conversion via the static_cast operator**

==Note:==  The `static_cast` operator will produce undefined behavior if the value being converted doesn’t fit in range of the new type.

**Explicit type conversion** allow us (the programmer) to explicitly tell the compiler to convert a value from one type to another type, and that we take full responsibility for the result of that conversion.

To perform an explicit type conversion, in most cases we’ll use the `static_cast` operator. The syntax for the `static cast` looks a little funny:

```c++
static_cast<new_type>(expression)
```

An example:

```c++
#include <iostream>

void print(int x)
{
	std::cout << x << '\n';
}

int main()
{
	print( static_cast<int>(5.5) ); // explicitly convert double value 5.5 to an int

	return 0;
}
```

**Using static_cast to convert char to int**

An example:

```c++
#include <iostream>

int main()
{
    char ch{ 97 }; // 97 is ASCII code for 'a'
    std::cout << ch << " has value " << static_cast<int>(ch) << '\n'; // print value of variable ch as an int

    return 0;
}
```

Output:

```
a has value 97
```

**std::int8_t and std::uint8_t likely behave like chars instead of integers**

An example:

```c++
#include <cstdint>
#include <iostream>

int main()
{
    std::int8_t myInt{65};      // initialize myInt with value 65
    std::cout << myInt << '\n'; // you're probably expecting this to print 65

    return 0;
}
```

Because `std::int8_t` describes itself as an int, you might be tricked into believing that the above program will print the integral value `65`. However, on most systems, this program will print `A` instead (treating `myInt` as a `signed char`). However, this is not guaranteed (on some systems, it may actually print `65`).

If you want to ensure that a `std::int8_t` or `std::uint8_t` object is treated as an integer, you can convert the value to an integer using `static_cast`:

```c++
#include <cstdint>
#include <iostream>

int main()
{
    std::int8_t myInt{65};
    std::cout << static_cast<int>(myInt) << '\n'; // will always print 65

    return 0;
}
```

In cases where `std::int8_t` is treated as a char, input from the console can also cause problems:

```c++
#include <cstdint>
#include <iostream>

int main()
{
    std::cout << "Enter a number between 0 and 127: ";
    std::int8_t myInt{};
    std::cin >> myInt;

    std::cout << "You entered: " << static_cast<int>(myInt) << '\n';

    return 0;
}
```

A sample run of this program:

```
Enter a number between 0 and 127: 35
You entered: 51
```

Here’s what’s happening. When `std::int8_t` is treated as a char, the input routines interpret our input as a sequence of characters, not as an integer. So when we enter `35`, we’re actually entering two chars, `'3'` and `'5'`. Because a char object can only hold one character, the `'3'` is extracted (the `'5'` is left in the input stream for possible extraction later). Because the char `'3'` has ASCII code point 51, the value `51` is stored in `myInt`, which we then print later as an int.



## 5. Constants and Strings

### 5.1 Constant variables (named constants)

In programming, a **constant** is a value that may not be changed during the program's execution.

C++ supports two different kinds of constants:

- **Named constants** are constant values that are associated with an identifier. These are also sometimes called **symbolic constants**, or occasionally just **costants**.
- **Literal constants** are constant values that are not associated with an identifier.

**Types of named constants**

There are three ways to define a named constant in C++:

- Constant variables.
- Object-like macros with substitution text.
- Enumerated constants.

**Declaring a const variable**

To declare a constant variable, we place the `const` keyword (called a “const qualifier”) adjacent to the object’s type:

```c++
const double gravity { 9.8 };  // preferred use of const before type
int const sidesInSquare { 4 }; // "east const" style, okay but not preferred
```

**Const variables must be initialized**

Const variables *must* be initialized when you define them, and then that value can not be changed via assignment:

```c++
int main()
{
    const double gravity; // error: const variables must be initialized
    gravity = 9.9;        // error: const variables can not be changed

    return 0;
}
```

Note that const variables can be initialized from other variables (including non-const ones):

```c++
#include <iostream>

int main()
{
    std::cout << "Enter your age: ";
    int age{};
    std::cin >> age;

    const int constAge { age }; // initialize const variable using non-const value

    age = 5;      // ok: age is non-const, so we can change its value
    constAge = 6; // error: constAge is const, so we cannot change its value

    return 0;
}
```

**Const function parameters**

Function parameters can be made constants via the `const` keyword:

```c++
#include <iostream>

void printInt(const int x)
{
    std::cout << x << '\n';
}

int main()
{
    printInt(5); // 5 will be used as the initializer for x
    printInt(6); // 6 will be used as the initializer for x

    return 0;
}
```

Note that we did not provide an explicit initializer for our const parameter `x` -- the value of the argument in the function call will be used as the initializer for `x`.

Making a function parameter constant enlists the compiler’s help to ensure that the parameter’s value is not changed inside the function. However, in modern C++ we don’t make value parameters `const` because we generally don’t care if the function changes the value of the parameter (since it’s just a copy that will be destroyed at the end of the function anyway). The `const` keyword also adds a small amount of unnecessary clutter to the function prototype.

It's better not to use `const` when passing by value.

**Const return values**

A function's return value may also be made const:

```c++
#include <iostream>

const int getValue()
{
    return 5;
}

int main()
{
    std::cout << getValue() << '\n';

    return 0;
}
```

- For fundamental types, the `const` qualifier on a return type is simply ignored (your compiler may generate a warning).

- For other types (which we’ll cover later), there is typically little point in returning const objects by value, because they are temporary copies that will be destroyed anyway. Returning a const value can also impede certain kinds of compiler optimizations (involving move semantics), which can result in lower performance.

It's better not to use `const` when returning by value.

**Object-like macros with substitution text**

```c++
#include <iostream>

#define MY_NAME "Alex"

int main()
{
    std::cout << "My name is: " << MY_NAME << '\n';

    return 0;
}
```

When the preprocessor processes the file containing this code, it will replace `MY_NAME` (on line 7) with `"Alex"`. Note that `MY_NAME` is a name, and the substitution text is a constant value, so object-like macros with substitution text are also named constants.

**Prefer constant variables to preprocessor macros**

Three major problems for using preprocessor macros for named constants:

1. The biggest issue is that macros don’t follow normal C++ scoping rules. 
   Once a macro is #defined, all subsequent occurrences of the macro’s name in the current file will be replaced. If that name is used elsewhere, 
   you’ll get macro substitution where you didn’t want it. This will most 
   likely lead to strange compilation errors. For example:

   ```c++
   #include <iostream>
   
   void someFcn()
   {
   // Even though gravity is defined inside this function
   // the preprocessor will replace all subsequent occurrences of gravity in the rest of the file
   #define gravity 9.8
   }
   
   void printGravity(double gravity) // including this one, causing a compilation error
   {
       std::cout << "gravity: " << gravity << '\n';
   }
   
   int main()
   {
       printGravity(3.71);
   
       return 0;
   }
   ```

2. Second, it is often harder to debug code using macros. Although your 
   source code will have the macro’s name, the compiler and debugger never see the macro because it has already been replaced before they run. Many debuggers are unable to inspect a macro’s value, and often have limited capabilities when working with macros.

3. Third, macro substitution behaves differently than everything else in C++. Inadvertent mistakes can be easily made as a result.

Constant variables have none of these problems: they follow normal scoping rules, can be seen by the compiler and debugger, and behave consistently.

It's better to prefer constant variables over object-like macros with substitution text.

**Type qualifiers**

A **type qualifier** (sometimes called a **qualifier** for short) is a keyword that is applied to a type that modifiers how that type behaves.The `const` used to declare a constant variable is called a `const type qualifier` (or `const qualifier` for short).

As of C++23, C++ only has two type qualifiers: `const` and `volatile`.

The `volatile` qualifier is used to tell the compiler that an object may have its value changed at any time. This rarely-used qualifier disables certain types of optimizations.



### 5.2 Literals

**Literals** are values that are inserted directly into the code. For example:

```c++
return 5;                     // 5 is an integer literal
bool myNameIsAlex { true };   // true is a boolean literal
double d { 3.4 };             // 3.4 is a double literal
std::cout << "Hello, world!"; // "Hello, world!" is a C-style string literal
```

Literals are sometimes called **literal constants** because their meaning cannot be redefined (`5` always means the integral value 5).

**The type of a literal**

The type of a literal is deduced from the literal’s value. For example, a literal that is a whole number (e.g. `5`) is deduced to be of type `int`.

By default:

| Literal value        | Examples        | Default literal type |
| -------------------- | --------------- | -------------------- |
| integer value        | 5, 0, -3        | int                  |
| boolean value        | true, false     | bool                 |
| floating point value | 1.2, 0.0, 3.4   | double (not float!)  |
| character            | 'a', '\n'       | char                 |
| C-style string       | "Hello, world!" | const char[14]       |

**Literal suffixes**

If the default type of a literal is not as desired, you can change the type of a literal by adding a suffix:

| Data type      | suffix                                 | meaning                                   |
| -------------- | -------------------------------------- | ----------------------------------------- |
| integral       | u or U                                 | unsigned int                              |
|                | l or L                                 | long                                      |
|                | ul, uL, Ul, UL, lu, lU, Lu, LU         | unsigned long                             |
|                | ll or LL                               | long long                                 |
|                | ull, uLL, Ull, ULL, llu, llU, LLu, LLU | unsigned long long                        |
|                | z or Z                                 | The signed version of std::size_t (C++23) |
|                | uz, uZ, Uz, UZ, zu, zU, Zu, ZU         | std::size_t (C++23)                       |
| floating point | f or F                                 | float                                     |
|                | l or L                                 | long double                               |
| string         | s                                      | std::string                               |
|                | sv                                     | std::string_view                          |

Most of the suffixes are not case sensitive. The exceptions are:

- `s` and `sv` must be lower case.
- Two consecutive `l` or `L` characters must have the same casing.

Excepting the `f` suffix, suffixes are most often used in cases where type deduction is involved.

**String literals**

For historical resons, strings are not a fundamental type in C++. Rather, they have a strange, complicated type that is hard to work with. Such strings are often called **C strings** or **C-style strings**, as they are inherited from the C-language.

There are two non-obvious things worth knowing about C-style string literals.

1. All C-style string literals have an implicit null terminator. 

   Consider a string such as `"hello"`. While this C-style string appears to only have five characters, it actually has six: `'h'`, `'e'`, `'l`‘, `'l'`, `'o'`, and `'\0'` (a character with ASCII code 0).  This trailing ‘\0’ character is a special character called a **null terminator**, and it is used to indicate the end of the string. A string that ends with a null terminator is called a **null-terminated string**.

2. Unlike most other literals (which are values, not objects), C-style 
   string literals are const objects that are created at the start of the 
   program and are guaranteed to exist for the entirety of the program.

### 5.3 Numeral systems (decimal, binary, hexadecimal, and octal)

| number system | prefix    |
| ------------- | --------- |
| Decimal       | No prefix |
| Octal         | 0         |
| Hexadecimal   | 0x or 0X  |

**Binary literals**

Prior to C++14, there is no support for binary literals. However, hexadecimal literals provide us with a useful workaround (that you may still see in existing code bases):

```c++
#include <iostream>

int main()
{
    int bin{};    // assume 16-bit ints
    bin = 0x0001; // assign binary 0000 0000 0000 0001 to the variable
    bin = 0x0002; // assign binary 0000 0000 0000 0010 to the variable
    bin = 0x0004; // assign binary 0000 0000 0000 0100 to the variable
    bin = 0x0008; // assign binary 0000 0000 0000 1000 to the variable
    bin = 0x0010; // assign binary 0000 0000 0001 0000 to the variable
    bin = 0x0020; // assign binary 0000 0000 0010 0000 to the variable
    bin = 0x0040; // assign binary 0000 0000 0100 0000 to the variable
    bin = 0x0080; // assign binary 0000 0000 1000 0000 to the variable
    bin = 0x00FF; // assign binary 0000 0000 1111 1111 to the variable
    bin = 0x00B3; // assign binary 0000 0000 1011 0011 to the variable
    bin = 0xF770; // assign binary 1111 0111 0111 0000 to the variable

    return 0;
}
```

In C++14 onward, we can use binary literals by using the 0b prefix:

```c++
#include <iostream>

int main()
{
    int bin{};        // assume 16-bit ints
    bin = 0b1;        // assign binary 0000 0000 0000 0001 to the variable
    bin = 0b11;       // assign binary 0000 0000 0000 0011 to the variable
    bin = 0b1010;     // assign binary 0000 0000 0000 1010 to the variable
    bin = 0b11110000; // assign binary 0000 0000 1111 0000 to the variable

    return 0;
}
```

**Digit separators**

Because long literals can be hard to read, C++14 also adds the ability to use a quotation mark (') as a digit separator.

```c++
#include <iostream>

int main()
{
    int bin { 0b1011'0010 };  // assign binary 1011 0010 to the variable
    long value { 2'132'673'462 }; // much easier to read than 2132673462

    return 0;
}
```

Also note that the separator can not occur before the first digit of the value:

```c++
int bin { 0b'1011'0010 };  // error: ' used before first digit of value
```

Digit separators are purely visual and do not impact the literal value in any way.

**Outputting values in decimal, octal, or hexadecimal**

By default, C++ outputs values in decimal. However, you can change the output format via use of the `std::dec`, `std::oct`, and `std::hex` I/O manipulators:

```c++
#include <iostream>

int main()
{
    int x { 12 };
    std::cout << x << '\n'; // decimal (by default)
    std::cout << std::hex << x << '\n'; // hexadecimal
    std::cout << x << '\n'; // now hexadecimal
    std::cout << std::oct << x << '\n'; // octal
    std::cout << std::dec << x << '\n'; // return to decimal
    std::cout << x << '\n'; // decimal

    return 0;
}
```

This prints:

```
12
c
c
14
12
12
```

Note that once applied, the I/O manipulator remains set for future output until it is changed again.

**Outputting values in binary**

Outputting values in binary is a little harder, as `std::cout` doesn’t come with this capability built-in. Fortunately, the C++ standard library includes a type called `std::bitset` that will do this for us (in the <bitset> header).

To use `std::bitset`, we can define a `std::bitset` variable and tell `std::bitset` how many bits we want to store. The number of bits must be a compile-time constant. `std::bitset` can be initialized with an integral value (in any format, including decimal, octal, hex, or binary).

```c++
#include <bitset> // for std::bitset
#include <iostream>

int main()
{
	// std::bitset<8> means we want to store 8 bits
	std::bitset<8> bin1{ 0b1100'0101 }; // binary literal for binary 1100 0101
	std::bitset<8> bin2{ 0xC5 }; // hexadecimal literal for binary 1100 0101

	std::cout << bin1 << '\n' << bin2 << '\n';
	std::cout << std::bitset<4>{ 0b1010 } << '\n'; // create a temporary std::bitset and print it

	return 0;
}
```

This prints:

```
11000101
11000101
1010
```

In C++20 and C++23, we have better options available via the new Format Library (C++20) and Print Library (C++23):

```c++
#include <format> // C++20
#include <iostream>
#include <print> // C++23

int main()
{
    std::cout << std::format("{:b}\n", 0b1010);  // C++20
    std::cout << std::format("{:#b}\n", 0b1010); // C++20

    std::println("{:b} {:#b}", 0b1010, 0b1010);  // C++23

    return 0;
}
```

This prints:

```
1010
0b1010
1010 0b1010
```

### 5.4 Constant expressions and compile-time optimization

**The as-if rule**

In C++, compilers are given a lot of leeway to optimize programs. The **as-if rule**
says that the compiler can modify a program however it likes in order to produce more optimized code, so long as those modifications do not affect a program’s “observable behavior”.

**Compile-time evaluation of expressions**

Modern C++ compilers are able to evaluate some expressions at compile-time. When this occurs, the compiler can replace the expression with the result of the expression.

**Constant expressions**

One kind of expression that can always be evaluated at compile time is called a “constant expression”. A **constant expression** is an expression that contains only compile-time constant and operators/functions that support compile-time evaluation.

A **compile-time constant** is a constant whose value *must be* known at compile time. This includes:

- Literals (e.g. '5', '1.2')
- Constexpr variables
- Const integral variables with a constant expression initializer (e.g. `const int x { 5 };`). This is a historical exception -- in modern C++, constexpr variables are preferred.
- Non-type template parameters.
- Enumerators

Const variables that are not compile-time constants are sometimes called **runtime constants**. Runtime constants cannot be used in a constant expression.

==Note:== Const non-integral variables are always runtime constants (even if they 
have a constant expression initializer). If you need such variables to be compile-time constants, define them as constexpr variables instead.

The most common type of operators and functions that support compile-time evaluation include:

- Arithmetic operators with operands that are compile-time constants (e.g. `1 + 2`)
- Constexpr and consteval functions.

Example:

```c++
#include <iostream>

int getNumber()
{
    std::cout << "Enter a number: ";
    int y{};
    std::cin >> y;

    return y;
}

int main()
{
    // Non-const variables:
    int a { 5 };                 // 5 is a constant expression
    double b { 1.2 + 3.4 };      // 1.2 + 3.4 is a constant expression

    // Const integral variables with a constant expression initializer
    // are compile-time constants:
    const int c { 5 };           // 5 is a constant expression
    const int d { c };           // c is a constant expression
    const long e { c + 2 };      // c + 2 is a constant expression

    // Other const variables are runtime constants:
    const int f { a };           // a is not a constant expression
    const int g { a + 1 };       // a + 1 is not a constant expression
    const long h { a + c };      // a + c is not a constant expression
    const int i { getNumber() }; // getNumber() is not a constant expression

    const double j { b };        // b is not a constant expression
    const double k { 1.2 };      // 1.2 is a constant expression

    return 0;
}
```

**Why we care about constant expressions**

Constant expressions are useful for two reasons:

- Constant expressions are *always* eligible for compile-time evaluation, meaning they are more likely to be optimized at compile-time.
- Certain C++ features require constant expressions.

A few common cases where a constant expression is required:

- The initializer of a constexpr variable.
- A non-type template argument.
- The defined length of a `std::array` or a C-style array.

**When are constant expressions evaluated?**

The compiler is only *required* to evaluate constant expressions at compile-time in contexts that require a constant expression (such as the initializer of a compile-time constant). In contexts that do not require a constant expression, the compiler may choose whether to evaluate a constant expression at compile-time or at runtime.

```c++
const int x { 3 + 4 }; // constant expression 3 + 4 must be evaluated at compile-time
int y { 3 + 4 };       // constant expression 3 + 4 may be evaluated at compile-time or runtime
```

Because variable `x` has type `const int` and a constant expression initializer, it is a compile-time constant. Its initializer must be evaluated at compile-time (otherwise the value of `x` wouldn’t be known at compile-time, and `x` wouldn’t be a compile-time constant).

Because variable `y` does not require a constant expression initializer, the compiler can choose whether to evaluate `3 + 4` at compile-time or runtime.

Even when not required to do so, modern compilers will *usually* evaluate a constant expression at compile-time because it is an easy optimization and more performant to do so.

**Partial optimization of constant subexpressions**

```c++
#include <iostream>

int main()
{
	std::cout << 3 + 4 << '\n';

	return 0;
}
```

Compilers have long been able to optimize constant subexpressions, even 
when the full expression is a runtime expression. This optimization process is called “constant folding”, and is allowed under the as-if rule.

The resulting optimized code would look like this:

```c++
#include <iostream>

int main()
{
	std::cout << 7 << '\n';

	return 0;
}
```



### 5.5 Constexpr variables

When using `const`, our variables could end up as either a compile-time const or a runtime const, depending on whether the initializer is a constant expression or not. In some cases, it can be hard to tell whether a const variable is a compile-time constant (and thus usable in a constant expression) or a runtime constant (and thus not usable in a constant expression).

For example:

```c++
int a { 5 };       // not const at all
const int b { a }; // obviously a runtime const (since initializer is non-const)
const int c { 5 }; // obviously a compile-time const (since initializer is a constant expression)

const int d { obj };        // not obvious whether this is a runtime or compile-time const
const int e { getValue() }; // not obvious whether this is a runtime or compile-time const
```

In the above example, both `d` and `e` could be either a runtime or a compile-time const depending on how `obj` and `getValue()` are defined. It’s not clear until we hunt down the definitions for those identifiers.

**The `constexpr` keyword**

Fortunately, we can enlist the compiler’s help to ensure we get a compile-time constant variable where we desire one. To do so, we use the `constexpr` keyword instead of `const` in a variable’s declaration. A **constexpr** (which is short for “constant expression”) variable must be initialized with a constant expression, otherwise a compilation error will result.

For example:

```c++
#include <iostream>

int five()
{
    return 5;
}

int main()
{
    constexpr double gravity { 9.8 }; // ok: 9.8 is a constant expression
    constexpr int sum { 4 + 5 };      // ok: 4 + 5 is a constant expression
    constexpr int something { sum };  // ok: sum is a constant expression

    std::cout << "Enter your age: ";
    int age{};
    std::cin >> age;

    constexpr int myAge { age };      // compile error: age is not a constant expression
    constexpr int f { five() };       // compile error: return value of five() is not a constant expression

    return 0;
}
```

Note that non-integral types can be made constexpr.

**Const vs constexpr**

For variables, const means that the value of an object cannot be changed after initialization. Constexpr means that an object must have a value that is known at compile-time.

Constexpr variables are implicitly const. Const variables are not implicitly constexpr (except for const integral variables with a constant expression initializer).

**Best practice**

- Any constant variable whose initializer is a constant expression should be declared as `constexpr`.
- Any constant variable whose initializer is not a constant expression should be declared as `const`.

**Const and constexpr function parameters**

Normal function calls are evaluated at runtime, with the supplied arguments being used to initialize the function’s parameters. Because the initialization of function parameters happens at runtime, this leads to two consequences:

1. `const` function parameters are treated as runtime constants (even when the supplied argument is a compile-time constant).
2. Function parameters cannot be declared as `constexpr`, since their initialization value isn’t determined until runtime.

**Nomenclature recap**

| TERM                  | definition                                                   |
| --------------------- | ------------------------------------------------------------ |
| Compile-time constant | An object whose value must be known at compile time (e.g. literals and constexpr variables). |
| Constexpr             | Keyword that declares variables as compile-time constants (and functions that can be evaluated at compile-time).<br />Informally, shorthand for "constant expression". |
| Constant expression   | An expression that contains only compile-time constants and operators/functions that support compile-time evaluation. |
| Runtime expression    | An expression that is not a constant expression.             |
| Runtime constant      | An constant object that is not a compile-time constant.      |



### 5.6 The conditional operator

**The conditional operator evaluates as an expression**

For example, when initializing a variable:

```c++
#include <iostream>

int main()
{
    constexpr bool inBigClassroom { false };
    constexpr int classSize { inBigClassroom ? 30 : 20 };
    std::cout << "The class size is: " << classSize << '\n';

    return 0;
}
```

There’s no direct if-else replacement for this. You might think to try something like this:

```c++
#include <iostream>

int main()
{
    constexpr bool inBigClassroom { false };

    if (inBigClassroom)
        constexpr int classSize { 30 };
    else
        constexpr int classSize { 20 };

    std::cout << "The class size is: " << classSize << '\n';;

    return 0;
}
```

However, this won’t compile, and you’ll get an error message that `classSize`
isn’t defined. Much like how variables defined inside functions die at the end of the function, variables defined inside an if-statement or else-statement die at the end of the if-statement or else-statement. Thus, `classSize` has already been destroyed by the time we try to print it.

**Parenthesizing the conditional operator**

Because C++ prioritizes the evaluation of most operators above the evaluation of the conditional operator, it’s quite easy to write expressions using the conditional operator that don’t evaluate as expected.

For this reason, the conditional operator should be parenthesized as follows:

- Parenthesize the entire conditional operator when used in a compound expression (an expression with other operators).
- For readability, consider parenthesizing the condition if it contains any operators (other than the function call operator).

```c++
return isStunned ? 0 : movesLeft;           // not used in compound expression, condition contains no operators
int z { (x > y) ? x : y };                  // not used in compound expression, condition contains operators
std::cout << (isAfternoon() ? "PM" : "AM"); // used in compound expression, condition contains no operators (function call operator excluded)
std::cout << ((x > y) ? x : y);             // used in compound expression, condition contains operators
```

**The type of the expressions must match or be convertible**

To comply with C++'s type checking rules, one of the following must be true:

- The type of the second and third operand must match.
- The compiler must be able to find a way to convert one or both of the second and third operands to matching types. The conversion rules the compiler uses are fairly complex and may yield surprising results in some cases.

An example:

```c++
#include <iostream>

int main()
{
    std::cout << (true ? 1 : 2) << '\n';    // okay: both operands have matching type int

    std::cout << (false ? 1 : 2.2) << '\n'; // okay: int value 1 converted to double

    std::cout << (true ? -1 : 2u) << '\n';  // surprising result: -1 converted to unsigned int, result out of range

    return 0;
}
```

Assuming 4 byte integers, the above prints:

```
1
2.2
4294967295
```

In general, it’s okay to mix operands with fundamental types (excluding 
mixing signed and unsigned values). If either operand is not a fundamental type, it’s generally best to explicitly convert one or both operands to a matching type yourself so you know exactly what you’ll get.

If the compiler can’t find a way to convert the second and third operands to a matching type, a compile error will result:

```c++
#include <iostream>

int main()
{
    constexpr int x{ 5 };
    std::cout << ((x != 5) ? x : "x is 5"); // compile error: compiler can't find common type for constexpr int and C-style string literal

    return 0;
}
```

In the above example, one of the expressions is an integer, and the  other is a C-style string literal. The compiler will not be able to find  a matching type on its own, so a compile error will result.

In such cases, you can either do an explicit conversion, or use an if-else statement:

```c++
#include <iostream>
#include <string>

int main()
{
    int x{ 5 }; // intentionally non-constexpr for this example

    // We can explicitly convert the types to match
    std::cout << ((x != 5) ? std::to_string(x) : std::string{"x is 5"}) << '\n';

    // Or use an if-else statement
    if (x != 5)
        std::cout << x << '\n';
    else
        std::cout << "x is 5" << '\n';

    return 0;
}
```

**When to use the conditional operator?**

The conditional operator is most useful when doing one of the following:

- Initializing an object with one of two values.
- Assigning one of two values to an object.
- Passing one of two values to a function.
- Returning one of two values from a function.
- Printing one of two values.

Complicated expressions should generally avoid use of the conditional operator, as they tend to be error prone and hard to read.



### 5.7 Inline functions and variables

```c++
#include <iostream>

int min(int x, int y)
{
    return (x < y) ? x : y;
}

int main()
{
    std::cout << min(5, 6) << '\n';
    std::cout << min(3, 2) << '\n';
    return 0;
}
```

For functions that are large and/or perform complex tasks, the overhead of the function call is typically insignificant compared to the amount of time the function takes to run. However, for small functions (such as `min()` above), the overhead costs can be larger than the time needed to actually execute the function’s code! In cases where a small function is called often, using a function can result in a significant performance penalty over writing the same code in-place.

**Inline expansion**

**Inline expansion** is a process where a function call is replaced by the code from the called function’s definition.

For example, if the compiler expanded the `min()` calls in the above example, the resulting code would look like this:

```c++
#include <iostream>

int main()
{
    std::cout << ((5 < 6) ? 5 : 6) << '\n';
    std::cout << ((3 < 2) ? 3 : 2) << '\n';
    return 0;
}
```

**The performance of inline code**

Beyond removing the cost of function call, inline expansion can also allow the compiler to optimize the resulting code more efficiently -- for example, because the expression `((5 < 6) ? 5 : 6)` is now a constant expression, the compiler could further optimize the first statement in `main()` to `std::cout << 5 << '\n';`.

However, inline expansion has its own potential cost: if the body of the function being expanded takes more instructions than the function call being replaced, then each inline expansion will cause the executable to grow larger. Larger executables tend to be slower (due to not fitting as well in memory caches).

Inline expansion is best suited to simple, short functions (e.g. no more than a few statements), especially cases where a single function call can be executed more than once (e.g. function calls inside a loop).

**The inline keyword, historically**

Historically, compilers either didn’t have the capability to determine whether inline expansion would be beneficial, or were not very good at it. For this reason, C++ provided the keyword `inline`, which was originally intended to be used as a hint to the compiler that a function would (probably) benefit from being expanded inline.

A function that is declared using the `inline` keyword is called an **inline function**.

An example:

```c++
#include <iostream>

inline int min(int x, int y) // inline keyword means this function is an inline function
{
    return (x < y) ? x : y;
}

int main()
{
    std::cout << min(5, 6) << '\n';
    std::cout << min(3, 2) << '\n';
    return 0;
}
```

However, in modern C++, the `inline` keyword is no longer used to request that a function be expanded inline. There are quite a few reasons for this:

- Using `inline` to request inline expansion is a form of premature optimization, and misuse could actually harm performance.
- The `inline` keyword is just a hint -- the compiler is completely free to ignore a request to inline a function. This is likely to be the result if you try to inline a lengthy function! The compiler is also free to perform inline expansion of functions that do not use the `inline` keyword as part of its normal set of optimizations.
- The `inline` keyword is defined at the wrong level of granularity. We use the `inline` keyword on a function definition, but inline expansion is actually determined per function call. It may be beneficial to expand some function calls and detrimental to expand others, and there is no syntax to influence this.

Modern optimizing compilers are typically good at determining which function calls should be made inline -- better than humans in most cases. As a result, the compiler will likely ignore or devalue any use of `inline` to request inline expansion for your functions.

It's better not to use the `inline` keyword to request inline expansion for your functions.

**The inline keyword, modernly**

In modern C++, the term `inline` has evolved to mean “multiple definitions are allowed”. Thus, an inline function is one that is allowed to be defined in multiple translation units (without violating the ODR).

Inline functions have two primary requirements:

- The compiler needs to be able to see the full definition of an inline 
  function in each translation unit where the function is used (a forward 
  declaration will not suffice on its own). The definition can occur after
  the point of use if a forward declaration is also provided. Only one 
  such definition can occur per translation unit, otherwise a compilation 
  error will occur.
- Every definition for an inline function must be identical, otherwise undefined behavior will result.

The linker will consolidate all inline function definitions for an identifier into a single definition (thus still meeting the requirements of the one definition rule).

Here's an example:

main.cpp

```c++
#include <iostream>

double circumference(double radius); // forward declaration

inline double pi() { return 3.14159; }

int main()
{
    std::cout << pi() << '\n';
    std::cout << circumference(2.0) << '\n';

    return 0;
}
```

math.cpp

```c++
inline double pi() { return 3.14159; }

double circumference(double radius)
{
    return 2.0 * pi() * radius;
}
```

Inline functions are typically defined in header files, where they can be #included into the top of any code file that needs to see the full definition of the identifier. This ensures that all inline definitions for an identifier are identical.

**Best practice**

Avoid the use of the `inline` keyword unless you have a specific, compelling reason to do so (e.g. you’re defining those functions or variables in a header file).

**Why not make all functions inline and defined in a header file?**

- It can increase your compile times. When a function in a code file 
  changes, only that code file needs to be recompiled. When an inline 
  function in a header file changes, every code file that includes that 
  header (either directly or via another header) needs to recompiled. On 
  large projects, this can have a drastic impact.
- It can lead to more naming collisions since you’ll end up with more code in a single code file.

**Inline variables C++17**

C++17 introduces **inline variables**, which are variables that are allowed to be defined in multiple files. Inline variables work similarly to inline functions, and have the same requirements (the compiler must be able to see an identical full definition everywhere the variable is used).

### 5.8 Constexpr and consteval functions

```c++
#include <iostream>

int greater(int x, int y)
{
    return (x > y ? x : y); // here's our expression
}

int main()
{
    constexpr int x{ 5 };
    constexpr int y{ 6 };

    std::cout << greater(x, y) << " is greater!\n"; // will be evaluated at runtime

    return 0;
}
```

By using a function (which is good for modularity and documentation) we’ve lost our ability for that code to be evaluated at compile-time (which is bad for performance).

**Constexpr functions can be evaluated at compile-time**

A **constexpr function** is a function whose return value may be computed at compile-time. To make a function a constexpr function, we simply use the `constexpr` keyword in front of the return type.

```c++
#include <iostream>

constexpr int greater(int x, int y) // now a constexpr function
{
    return (x > y ? x : y);
}

int main()
{
    constexpr int x{ 5 };
    constexpr int y{ 6 };

    // We'll explain why we use variable g here later in the lesson
    constexpr int g { greater(x, y) }; // will be evaluated at compile-time

    std::cout << g << " is greater!\n";

    return 0;
}
```

When a function call is evaluated at compile-time, the compiler will calculate the return value of the function call at compile-time, and then replace the function call with the return value.

To be eligible for compile-time evaluation, a function must have a constexpr return type, and a call to the function must have arguments that are known at compile time (e.g. are constant expressions).

**Constexpr functions can alse be evaluated at runtime**

Functions with a constexpr return value can also be evaluated at runtime, in which case they will return a non-constexpr result. For example:

```c++
#include <iostream>

constexpr int greater(int x, int y)
{
    return (x > y ? x : y);
}

int main()
{
    int x{ 5 }; // not constexpr
    int y{ 6 }; // not constexpr

    std::cout << greater(x, y) << " is greater!\n"; // will be evaluated at runtime

    return 0;
}
```

In this example, because arguments `x` and `y` are not constant expressions, the function cannot be resolved at compile-time. However, the function will still be resolved at runtime, returning the expected value as a non-constexpr `int`.

**When is a constexpr function evaluated at compile-time?**

A constexpr function must be evaluated at compile-time if the return value is used where a constant expression is required. Otherwise, compile-time evaluation is not guaranteed.

Thus, a constexpr function is better thought of as “can be used in a constant expression”, not “will be evaluated at compile-time”.

Put another way, we can categorize the likelihood that a constexpr  function will actually be evaluated at compile-time as follows:

Always (required by the standard):

- Constexpr function is called where constant expression is required.
- Constexpr function is called from other function being evaluated at compile-time.

Probably (there’s little reason not to):

- Constexpr function is called where constant expression isn’t required, all arguments are constant expressions.

Possibly (if optimized under the as-if rule):

- Constexpr  function is called where constant expression isn’t required, some  arguments are not constant expressions but their values are known at  compile-time.

Never (not possible):

- Constexpr  function is called where constant expression isn’t required, some  arguments have values that are not known at compile-time.

**What about `std::is_constant_evaluated` or `if consteval`?**

Introduced in C++20, `std::is_constant_evaluated()` (defined in the <type_traits> header) was intended to allow differentiation of behavior when a function is evaluating at runtime vs compile-time, so you could do something like this:

```c++
#include <type_traits> // for std::is_constant_evaluated()

constexpr int someFunction()
{
    if (std::is_constant_evaluated()) // if evaluating at compile-time
        // do something
    else // runtime evaluation
        // do something else
}
```









## 6. Operators







## 7. Scope, Duration, and Linkage

### 7.1 Compound statements (blocks)

A **compound statement** (also called a **block**, or **block statement**) is a group of *zero or more* statements that is treated by the compiler as if it were a single statement.

Blocks *can be* nested insider other blocks:

```c++
int add(int x, int y)
{ // block
    return x + y;
} // end block

int main()
{ // outer block

    // multiple statements
    int value {};

    { // inner/nested block
        add(3, 4);
    } // end inner/nested block

    return 0;

} // end outer block
```



### 7.2 User-defined namespaces and the scope resolution operator

**Defining own namespaces**

C++ allows us to define our own namespaces via the `namepsace` keyword.

The syntax for a namespace is as follows:

```c++
namespace namespaceIdentifier
{
    // content of namespace here
}
```

It's recommended starting namespace names with a capital letter.

**Accessing a namespace with the scope resolution operator (::)**

The **scope resolution operator** tells the compiler that the identifier specified by the right-hand operand should be looked for in the scope of the left-hand operand.

An example:

```c++
#include <iostream>

namespace Foo // define a namespace named Foo
{
    // This doSomething() belongs to namespace Foo
    int doSomething(int x, int y)
    {
        return x + y;
    }
}

namespace Goo // define a namespace named Goo
{
    // This doSomething() belongs to namespace Goo
    int doSomething(int x, int y)
    {
        return x - y;
    }
}

int main()
{
    std::cout << Foo::doSomething(4, 3) << '\n'; // use the doSomething() that exists in namespace Foo
    std::cout << Goo::doSomething(4, 3) << '\n'; // use the doSomething() that exists in namespace Goo
    return 0;
}
```



**Using the scope resolution operator with no name prefix**

The scope resolution operator can also be used in front of an identifier without providing a namespace name (e.g. `::doSomething`). In such a case, the identifier is looked for in the global namespace.

An example:

```c++
#include <iostream>

void print() // this print() lives in the global namespace
{
	std::cout << " there\n";
}

namespace Foo
{
	void print() // this print() lives in the Foo namespace
	{
		std::cout << "Hello";
	}
}

int main()
{
	Foo::print(); // call print() in Foo namespace
	::print();    // call print() in global namespace (same as just calling print() in this case)

	return 0;
}
```

In this example, use of the scope resolution operator is superfluous. The next example show a case where the scope resolution operator with no namespace can be useful.

**Identifier resolution from within a namespace**

If an identifier inside a namespace is used and no scope resolution is provided, the compiler will:

1. First try to find a matching declaration in that same namespcae.
2. If no matching identifier is found, then check each containing namespace in sequence to see if a match is found, with the global namespace being checked last.

An example:

```c++
#include <iostream>

void print() // this print() lives in the global namespace
{
	std::cout << " there\n";
}

namespace Foo
{
	void print() // this print() lives in the Foo namespace
	{
		std::cout << "Hello";
	}

	void printHelloThere()
	{
		print();   // calls print() in Foo namespace
		::print(); // calls print() in global namespace
	}
}

int main()
{
	Foo::printHelloThere();

	return 0;
}
```

`::print()` is used to explicitly call the global version of `print()`.

**Forward declaration of content in namespaces**

For identifiers inside a namespace, those forward declarations need to be inside the same namespace.

An example:

add.h

```c++
#ifndef ADD_H
#define ADD_H

namespace BasicMath
{
    // function add() is part of namespace BasicMath
    int add(int x, int y);
}

#endif
```

add.cpp

```c++
#include "add.h"

namespace BasicMath
{
    // define the function add() inside namespace BasicMath
    int add(int x, int y)
    {
        return x + y;
    }
}
```

main.cpp

```c++
#include "add.h" // for BasicMath::add()

#include <iostream>

int main()
{
    std::cout << BasicMath::add(4, 3) << '\n';

    return 0;
}
```

Both the declaration for `add()` in add.h and definition of function `add()` need to be put inside the same namespace `BasicMath`.

**Multiple namespace blocks are allowed**

It's legal to declare namespace blocks in multiple locations (either across multiple files, or multiple places within the same file). All declarations within the namespace are considered part of the namespace.

An example:

circle.h

```c++
#ifndef CIRCLE_H
#define CIRCLE_H

namespace BasicMath
{
    constexpr double pi{ 3.14 };
}

#endif
```

growth.h

```c++
#ifndef GROWTH_H
#define GROWTH_H

namespace BasicMath
{
    // the constant e is also part of namespace BasicMath
    constexpr double e{ 2.7 };
}

#endif
```

main.cpp

```c++
#include "circle.h" // for BasicMath::pi
#include "growth.h" // for BasicMath::e

#include <iostream>

int main()
{
    std::cout << BasicMath::pi << '\n';
    std::cout << BasicMath::e << '\n';

    return 0;
}
```

**Nested namespaces**

Namespaces can be nested inside other namespaces.

An example:

```c++
#include <iostream>

namespace Foo
{
    namespace Goo // Goo is a namespace inside the Foo namespace
    {
        int add(int x, int y)
        {
            return x + y;
        }
    }
}

int main()
{
    std::cout << Foo::Goo::add(1, 2) << '\n';
    return 0;
}
```

Since C++17, nested namespace can also be declared this way:

```c++
#include <iostream>

namespace Foo::Goo // Goo is a namespace inside the Foo namespace (C++17 style)
{
    int add(int x, int y)
    {
        return x + y;
    }
}

int main()
{
    std::cout << Foo::Goo::add(1, 2) << '\n';
    return 0;
}
```

**Namespace aliases**

C++ allows to create **namespace aliases**, which allow us to temporarily shorten a long sequence of namespaces into something shorter:

```c++
#include <iostream>

namespace Foo::Goo
{
    int add(int x, int y)
    {
        return x + y;
    }
}

int main()
{
    namespace Active = Foo::Goo; // active now refers to Foo::Goo

    std::cout << Active::add(1, 2) << '\n'; // This is really Foo::Goo::add()

    return 0;
} // The Active alias ends here
```

One nice advantage of namespace aliases:

If you ever want to move the functionality within `Foo::Goo` to a different place, you can just update the `Active` alias to reflect the new destination, rather than having to find or replace every instance of `Foo::Goo`.

```c++
#include <iostream>

namespace Foo::Goo
{
}

namespace V2
{
    int add(int x, int y)
    {
        return x + y;
    }
}

int main()
{
    namespace Active = V2; // active now refers to V2

    std::cout << Active::add(1, 2) << '\n'; // We don't have to change this

    return 0;
}
```



### 7.3 Local variables

Local variables are variables that are defined inside a function (including function parameters).

**Local variables have block scope**

Local variables have **block scope**, which means they are *in scope* from their point of definition to the end of the block they are defined within.

**All variable names within a scope must be unique**

Variable names must be unique within a given scope, otherwise any reference to the name will be ambiguous.

**Local variables have automatic storage duration**

A variable's **storage duration** (usually just called **duration**) determines what rules govern when and how a variable will be created and destroyed.

Local variables have **automatic storage duration**, which means they are created at the point of definition and destroyed at the end of the block they are defined in.

For this reason, local variables are sometimes called **automatic variables**.

**Local variables in nested blocks**

Nested blocks are considered part of the scope of the outer block where they are defined. Consequently, variables defined in the outer block *can* be seen inside a nested block:

```c++
#include <iostream>

int main()
{ // outer block

    int x { 5 }; // x enters scope and is created here

    { // nested block
        int y { 7 }; // y enters scope and is created here

        // x and y are both in scope here
        std::cout << x << " + " << y << " = " << x + y << '\n';
    } // y goes out of scope and is destroyed here

    // y can not be used here because it is out of scope in this block

    return 0;
} // x goes out of scope and is destroyed here
```

**Local variables have no linkage**

Identifiers have another property named **linkage**. An identifier's *linkage_* determines whether a declaration of that same identifier in a different scope refers to the same object (or function).

Local variables have no linkage. Each declaration of an identifier with no linkage refers to a unique object or function.

For example:

```c++
int main()
{
    int x { 2 }; // local variable, no linkage

    {
        int x { 3 }; // this declaration of x refers to a different object than the previous x
    }

    return 0;
}
```



### **7.4 Introduction to global variables**

In C++, variables can also be declared *outside* of a function. Such variables are called **global variables**.

**The scope of global variables**

Identifiers declared in the global namespace have **global namespace scope** (commonly called **global scope**, and sometimes informally called **fle scope**), which means they are visible from the point of the declaration until the end of the *file* where they are declared.

Global variables can also be defined inside a user-defined namespace.

```c++
#include <iostream>

namespace Foo // Foo is defined in the global scope
{
    int g_x {}; // g_x is now inside the Foo namespace, but is still a global variable
}

void doSomething()
{
    // global variables can be seen and used everywhere in the file
    Foo::g_x = 3;
    std::cout << Foo::g_x << '\n';
}

int main()
{
    doSomething();
    std::cout << Foo::g_x << '\n';

    // global variables can be seen and used everywhere in the file
    Foo::g_x = 5;
    std::cout << Foo::g_x << '\n';

    return 0;
}
```

**Global variable initialization**

Unlike local variables, which are uninitialized by default, variables with static duration are zero-initialized by default.

Non-constant global variables can be optionally initialized:

```c++
int g_x;       // no explicit initializer (zero-initialized by default)
int g_y {};    // value initialized (resulting in zero-initialization)
int g_z { 1 }; // list initialized with specific value
```

**Constant global variables**

Just like local variables, global variables can be constant. As with all constants, constant global variables must be initialized.

```c++
// Const global variables
const int g_y;           // error: const variables must be initialized
const int g_y { 2 };     // defines initialized global const

// Constexpr global variables
constexpr int g_y;       // error: constexpr variables must be initialized
constexpr int g_y { 3 }; // defines initialized global constexpr
```



### 7.5 Variable shadowing (name hiding)

When we have a variable inside a nested block that has the same name as a variable in an outer block, the nested variable "hides" the outer variable in areas where they are both in scope. This is called **name hiding** or **shadowing**.

An example:

```c++
#include <iostream>

int main()
{ // outer block
    int apples { 5 }; // here's the outer block apples

    { // nested block
        // apples refers to outer block apples here
        std::cout << apples << '\n'; // print value of outer block apples

        int apples{ 0 }; // define apples in the scope of the nested block

        // apples now refers to the nested block apples
        // the outer block apples is temporarily hidden

        apples = 10; // this assigns value 10 to nested block apples, not outer block apples

        std::cout << apples << '\n'; // print value of nested block apples
    } // nested block apples destroyed


    std::cout << apples << '\n'; // prints value of outer block apples

    return 0;
} // outer block apples destroyed
```

Outputs:

```
5
10
5
```

**Shadowing of global variables**

Similar to how variables in a nested block can shadow variables in an outer block, local variables with the same name as a global variable will shadow the global variable wherever the local variable is in scope:

```c++
#include <iostream>
int value { 5 }; // global variable

void foo()
{
    std::cout << "global variable value: " << value << '\n'; // value is not shadowed here, so this refers to the global value
}

int main()
{
    int value { 7 }; // hides the global variable value until the end of this block

    ++value; // increments local value, not global value

    std::cout << "local variable value: " << value << '\n';

    foo();

    return 0;
} // local value is destroyed
```

However, because global variales are part of the global namespace, we can use the scope operator (::) with no prefix to tell the compiler we mean the global variable instead of the local variale.

```c++
#include <iostream>
int value { 5 }; // global variable

int main()
{
    int value { 7 }; // hides the global variable value
    ++value; // increments local value, not global value

    --(::value); // decrements global value, not local value (parenthesis added for readability)

    std::cout << "local variable value: " << value << '\n';
    std::cout << "global variable value: " << ::value << '\n';

    return 0;
} // local value is destroyed
```

### 7.6 Internal linkage

Global variable and functions identifiers can have either **internal linkage** or **external linkage**.

An identifier with **internal linkage** can be seen and used within a single translation unit, but it is not accessible from other translation units (that is, it is not exposed to the linker).

This means that if two source files have identically named identifiers with internal linkage, those identifiers will be treated as independant (and do not result in an ODR violation for having duplicate definitions).

**Global variables with internal linkage**

Global variables with internal linkage are sometimes called **internal variables**.

To make a non-constant global variable internal, we use the `static` keyword.

```c++
#include <iostream>

static int g_x{}; // non-constant globals have external linkage by default, but can be given internal linkage via the static keyword

const int g_y{ 1 }; // const globals have internal linkage by default
constexpr int g_z{ 2 }; // constexpr globals have internal linkage by default

int main()
{
    std::cout << g_x << ' ' << g_y << ' ' << g_z << '\n';
    return 0;
}
```

Const and constexpr global variables have internal linkage by default (and thus don't need the `static` keyword -- if it is used, it will be ignored).

Here's an example of multiple files using internal variales:

a.cpp

```c++
[[maybe_unused]] constexpr int g_x { 2 }; // this internal g_x is only accessible within a.cpp
```

main.cpp

```c++
#include <iostream>

static int g_x { 3 }; // this separate internal g_x is only accessible within main.cpp

int main()
{
    std::cout << g_x << '\n'; // uses main.cpp's g_x, prints 3

    return 0;
}
```

**Functions with internal linkage**

Functions default to external linkage, but can set to internal linkage via the `static` keyword:

add.cpp

```c++
// This function is declared as static, and can now be used only within this file
// Attempts to access it from another file via a function forward declaration will fail
[[maybe_unused]] static int add(int x, int y)
{
    return x + y;
}
```

main.cpp

```c++
#include <iostream>

static int add(int x, int y); // forward declaration for function add

int main()
{
    std::cout << add(3, 4) << '\n';

    return 0;
}
```

This program won't link, because function `add` is not accessible outside of `add.cpp`.

**`static` vs unnamed namespaces**

In modern C++, use of the `static` keyword for giving identifiers internal linkage is falling out of favor. Unnamed namespaces can give internal linkage to a wider range of identifiers (e.g. type identifiers), and they are better suited for giving many identifiers internal linkage.



### 7.7 External linkage and variable forward declarations









## 8. Contorl Flow





## 14. Introduction to Classes

### 14.1 Procedural programming versus object-oriented programming

In programming, properties are represented by **objects**, and behaviors are represented by **functions**.

In **procedual programming**, the functions and the data those functions operate on are separate entities. The programmer is responsible for combining the functions and the data together to produce the desired result. And thus, procedural programming represents reality fairly poorly.

In **object-oriented programming** (often abbreviated as OOP), the focus is on creating program-defined data types that contain both properties and a set of well-defined behaviors. The term "object" in OOP refers to the objects that we can instantiate from such types.



### 14.2 Intorduction to classes

