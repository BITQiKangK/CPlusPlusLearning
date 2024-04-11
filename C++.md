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

An identifier with **external linkage** can be seen and used both from the file in which it is defined, and from other code files (via a forward declaration).

**Functions have external linkage by default**

**Global variables with external linkage**

Global variables with external linkage are sometimes called **external variables**. To make a global variable external (and thus accessible by other files), we can use the `extern` keyword to do so:

```c++
int g_x { 2 }; // non-constant globals are external by default

extern const int g_y { 3 }; // const globals can be defined as extern, making them external
extern constexpr int g_z { 3 }; // constexpr globals can be defined as extern, making them external (but this is pretty useless, see the warning in the next section)

int main()
{
    return 0;
}
```

Non-const global variables are external by default (if used, the `extern` keyword will be ignored).

**Variable forward declarations via the extern keyword**

To actually use an external global variable that has been defined in another file, you also must place a `forward declaration` for the global variable in any other files wishing to use the variable. For variables, creating a forward declaration is also done via the `extern` keyword (with no initialization value).

An example:

a.cpp

```c++
// global variable definitions
int g_x { 2 }; // non-constant globals have external linkage by default
extern const int g_y { 3 }; // this extern gives g_y external linkage
```

main.cpp

```c++
#include <iostream>

extern int g_x; // this extern is a forward declaration of a variable named g_x that is defined somewhere else
extern const int g_y; // this extern is a forward declaration of a const variable named g_y that is defined somewhere else

int main()
{
    std::cout << g_x << ' ' << g_y << '\n'; // prints 2 3

    return 0;
}
```

==Note:== 

1. If you want to define an uninitialized non-const global variable, do not use the extern keyword, otherwise C++ will think you're trying to make a forward declaration for the variable.
2. Although constexpr variables can be given external linkage via the `extern` keyword, they can not be forward declared as constexpr. This is because the compiler needs to know the value of the constexpr variable (at compile time). If that value is defined in some other file, the compiler  has no visibility on what value was defined in that other file. However, you can forward declare a constexpr variable as const, which the compiler will treat as a runtime const.

**Summary**

```c++
// External global variable definitions:
int g_x;                       // defines non-initialized external global variable (zero initialized by default)
extern const int g_x{ 1 };     // defines initialized const external global variable
extern constexpr int g_x{ 2 }; // defines initialized constexpr external global variable

// Forward declarations
extern int g_y;                // forward declaration for non-constant global variable
extern const int g_y;          // forward declaration for const global variable
extern constexpr int g_y;      // not allowed: constexpr variables can't be forward declared
```



### 7.8 Why (non-const) global variables are evil

**The reasons**

1. Global variables make the program's state unpredictable.

    Every function call becomes potentially dangerous, and the programmer has no easy way of knowing which ones are dangerous and which ones aren't. Local variables are much safer because other functions can not affect them directly.

2. Global variables also make your program less modular and less flexible.

   A function that utilizes nothing but its parameters and has no side effects is perfectly modular. Modularity helps both in understanding what a program does, as well as with reusability. Global variables reduce modularity significantly.

In particluar, avoid using global variables for important "decision-point" variables.

**The initialization order problem of global variables**

Initialization of static variables (which includes global variables) happens as part of program startup, before execution of the `main` function. This proceeds in two phases:

1. `static initialization`: In the static initialization phase, global variables with constexpr initializers (including literals) are initialized to those values. Also, global variables without initializers are zero-initialized.
2. `dynamic initialization`: Global variables with non-constexpr initializers are initialized.

Within a single file, for each phase, global variables are generally initialized in order of definition. Given this, you need to be careful not to have variables dependent on the initialization value of other variables that won't be initialized until later.

An example:

```c++
#include <iostream>

int initX();  // forward declaration
int initY();  // forward declaration

int g_x{ initX() }; // g_x is initialized first
int g_y{ initY() };

int initX()
{
    return g_y; // g_y isn't initialized when this is called
}

int initY()
{
    return 5;
}

int main()
{
    std::cout << g_x << ' ' << g_y << '\n';
}
```

Any use of a global variable should meet at least the following two criteria:

1. There should only ever be one of the thing the variable represents in your program.
2. And its use should be ubiquitous throughout your program.

**Some advice**

1. Prefix all non-namespaced global variables with "g" or "g_", or better yet, put them in a namespace, to reduce the chance of naming collisions.

2. Instead of allowing direct access to the global variable, it's a better practice to "encapsulate" the variable.

   Make sure the variable can only be accessed from within the file it's declared in, e.g. by making the variable static or const, then provide external global "access functions" to work with the variable.

3. When writing an otherwise standalone function that uses the global variable, don't use the variable directly in your function body. Pass it in as an argument instead.



### 7.9 Sharing global constants across multiple files (using inline variables)

**Global constants as internal variables**

Prior to C++17

**Global constants as external variables**





### 7.10 Static local variables





### 7.11 Scope, duration, and linkage summary

**Scope summary**

An identifiers's *scope* determines where the identifier can be accessed within the source code.







### 7.12 Using declarations and using directives



### 7.13 Unnamed and inline namespaces







## 8. Contorl Flow





## 10. Type Conversion, Type Aliases, and Type Deduction

### 10.1 Implicit type conversion

**Introduction to type conversion**

The value of an object is stored as a sequence of bits, and the data type of the object tells the compiler how to interpret those bits into meaningful values.

Different data types may represent the "same" number differently. The integer value `3` might be stored as binary `0000 0000 0000 0000 0000 0000 0000 0011`, whereas floating point value `3.0` might be stored as binary `0100 0000 0100 0000 0000 0000 0000 0000`.

When we do this:

```c++
float f{ 3 }; // initialize floating point variable with int 3
```

In such a case, the compiler can't just copy the bits representing the `int` value `3` into the memory allocated for `float` variable `f`. Instead, it needs to convert the integer value `3` to the equivalent floating point value `3.0`, which can then be stored in the memory allocated for `f`.

The process of producing a new value of some type from a value of a different type is called a `conversion`.

Type conversion can be invoked in one of two ways: either **implicitly** (as needed by the compiler), or **explicitly** (when requested by the programmer).

**Implicit type conversion**

**Implicit type conversion** (also called **automatic type conversion** or **coercion**) is performed automatically by the compiler when one data type is required, but a different data type is supplied

**What happens when a type conversion is invoked**

When a type conversion is invoked (whether implicitly or explicitly), the compiler will determine whether it can convert the value from the current type to the desired type.





## 11. Function Overloading and Function Templates

### 11.1 Introduction to function overloading

**Function overloading** allows us to create multiple functions with the same name, so long as each individually named function has different parameter types (or the functions can be otherwise differentiated).

An example:

```c++
int add(int x, int y) // integer version
{
    return x + y;
}

double add(double x, double y) // floating point version
{
    return x + y;
}

int main()
{
    return 0;
}
```

**Introduction to overload resolution**

When a function call is made to a function that has been overloaded, the compiler will try to match the function call to the appropriate overload based on the arguments used in the function call. This is called **overload resolution**.

**Making it compile**

In order for a program using overloaded functions to compile, two things have to be true:

1. Each overloaded function has to be differentiated from the others.
2. Each call to an overloaded function has to resolve to an overloaded function.

If an overloaded function is not differentiated, or if a function all to an overloaded function can not be resolved to an overloaded function, then a compile error will result.



### 11.2 Function overload differentiation

**How overloaded functions are differentiated**

| Function property    | Used for differentiation | Notes                                                        |
| -------------------- | ------------------------ | ------------------------------------------------------------ |
| Number of parameters | Yes                      |                                                              |
| Type of parameters   | Yes                      | Excludes typedefs, type aliases, and const qualifier on value parameters. Include ellipses. |
| Return type          | No                       |                                                              |

**Overloading based on number of parameters**

An overloaded function is differentiated so along as each overloaded function has a different number of parameters.

An example:

```c++
int add(int x, int y)
{
    return x + y;
}

int add(int x, int y, int z)
{
    return x + y + z;
}
```

**Overloading based on type of parameters**





## 12. Compound Types: References and Pointers

### 12.1 Introduction to compound data types

**Compound data types**

**Compound data types** (also sometimes called **composite data types**) are data types that can be constructed from fundamental data types (or other compound data types).

C++ supports the following compound types:

- Functions

- Arrays

- Pointer types:

  - Pointer to object
  - Pointer to function

- Pointer to member types:

  - Pointer to data member
  - Pointer to member function

- Referece types:

  - L-value references
  - R-value references

- Enumerated types:

  - Unscoped enumerations
  - Scoped enumerations

- Class types:

  - Structs
  - Classes
  - Unions

  

### 12.2 Value categories (lvalues and rvalues)

**The properties of an expression**

To help determine how expressions should evaluate and where they can be used, all expressions in C++ have two properties: a **type** and a **value category**.

**The type of an expression**

The type of an expression is equivalent to the type of the value, object, or function that results from the evaluated expression.

An example:

```c++
int main()
{
    auto v1 { 12 / 4 }; // int / int => int
    auto v2 { 12.0 / 4 }; // double / int => double

    return 0;
}
```

The compiler can use the type of an expression to determine whether an expression is valid in a given context. For example:

```c++
#include <iostream>

void print(int x)
{
    std::cout << x << '\n';
}

int main()
{
    print("foo"); // error: print() was expecting an int argument, we tried to pass in a string literal

    return 0;
}
```

Note that the type of an expression must be determinable at compile time (other type checking and type deduction wouldn't work) -- however, the value of an expression may be determined at either compile time (if the expression is constexpr) or runtime (if the expression is not constexpr).

**The value category of an expression**

Consider the following program:

```c++
int main()
{
    int x{};

    x = 5; // valid: we can assign 5 to x
    5 = x; // error: can not assign value of x to literal value 5

    return 0;
}
```

The **value category** of an expression (or subexpression) indicates whether an expression resolves to a value, a function, or an object of some kind.

Prior to C++11, there were only two possible value categories: `lvalue` and `rvalue`.

In C++11, three additional value categories (`gvalue`, `prvalue`, and `xvalue`) were added to support a new feature called `move semantics`.

**Lvalue and rvalue expressions**

An **lvalue** is an expression that evaluates to an identifiable object or function (or bit-field).

Since the introduction of constants into the language, lvalues come in two subtypes:

1. **Modifiable lvalue**: Lvalue whose value can be modified.
2. **Non-modifiable lvalue**: Lvalue whose value can't be modified (because the lvalue is const or constexpr).

An **rvalue** is an expression that is not an lvalue. Rvalue expressions evaluate to a value. Commonly seen rvalues include **literals** (except C-style string literals, which are lvalues) and **the return value of functions** and **operators that return by value**.

Rvalues aren't identifiable (meaning they have to be used immediately), and only exist within the scope of the expression in which they are used.

An assignment operation requires the left operand of the assignment to be a modifiable lvalue expression, and the right operand to be an rvalue expression.

==Tip==

`operator&` requires its operand to be an lvalue. If `&(expression);` compiles, `expression` must be an lvalue:

```c++
int foo()
{
    return 5;
}

int main()
{
    int x { 5 };
    &x; // compiles: x is an lvalue expression
    &5; // doesn't compile: 5 is an rvalue expression
    &foo(); // doesn't compile: foo() is an rvalue expression
}
```

A C-style string literal is an lvalue because C-style strings (which are C-style arrays) decay to a pointer. The decay process only works if the array is an lvalue (and thus has an address that can be stored in the pointer).

**Lvalue to rvalue conversion**

Look at this example:

```c++
int main()
{
    int x { 5 };
    int y { x }; // x is an lvalue expression

    return 0;
}
```

Lvalue expressions will implicitly convert to rvalue expressions in contexts where an rvalue is expected but an lvalue is provided.



### 12.3 Lvalue references

In C++, a **reference** is an alias for an existing object. Once a reference has been defined, any operation on the reference is applied to the object being referenced.

Modern C++ contains two types of references: `lvalue references`, and `rvalue references`.

**Lvalue reference types**

An **lvalue reference** (commonly just called a `reference` since prior to C++11 there was only one type of reference) acts as an alias for an existing lvalue (such as a variable).

To declare an lvalue reference type, we use an ampersand (&) in the type declaration:

```c++
int      // a normal int type
int&     // an lvalue reference to an int object
double&  // an lvalue reference to a double object
```

**Lvalue reference variables**

An **lvalue reference variable** is a variable that acts as a reference to an lvalue (usually another variable).

To create an lvalue reference variable, we simply define a varable with an lvalue reference type:

```c++
#include <iostream>

int main()
{
    int x { 5 };    // x is a normal integer variable
    int& ref { x }; // ref is an lvalue reference variable that can now be used as an alias for variable x

    std::cout << x << '\n';  // print the value of x (5)
    std::cout << ref << '\n'; // print the value of x via ref (5)

    return 0;
}
```

**Modifying values through an lvalue reference**

We can also use a reference to modify the value of the object being referenced:

```c++
#include <iostream>

int main()
{
    int x { 5 }; // normal integer variable
    int& ref { x }; // ref is now an alias for variable x

    std::cout << x << ref << '\n'; // print 55

    x = 6; // x now has value 6

    std::cout << x << ref << '\n'; // prints 66

    ref = 7; // the object being referenced (x) now has value 7

    std::cout << x << ref << '\n'; // prints 77

    return 0;
}
```

**Initialization of lvalue references**

Much like constants, all references must be initialized.

```c++
int main()
{
    int& invalidRef;   // error: references must be initialized

    int x { 5 };
    int& ref { x }; // okay: reference to int is bound to int variable

    return 0;
}
```

When a reference is initialized with an object (or function), we say it is **bound** to that object (or function). 

The process by which such a reference is bound is called **reference binding**. 

The object (or function) being referenced is sometimes called **referent**.

Lvalue references must be bound to a *modifiable* lvalue.

```c++
int main()
{
    int x { 5 };
    int& ref { x }; // valid: lvalue reference bound to a modifiable lvalue

    const int y { 5 };
    int& invalidRef { y };  // invalid: can't bind to a non-modifiable lvalue
    int& invalidRef2 { 0 }; // invalid: can't bind to an rvalue

    return 0;
}
```

Lvalue references **cant't** be bound to non-modifiable lvalues or rvalues (otherwise you'd be able to change those values through the refernece, which could be a violation of their const-ness).

For this reason, lvalue references are occasionally called **lvalue references to non-const** (sometimes shortened to **non-const reference**).

In most cases, the type of the reference must match the type of the referent.

```c++
int main()
{
    int x { 5 };
    int& ref { x }; // okay: reference to int is bound to int variable

    double y { 6.0 };
    int& invalidRef { y }; // invalid; reference to int cannot bind to double variable
    double& invalidRef2 { x }; // invalid: reference to double cannot bind to int variable

    return 0;
}
```

**References can't be reseated (changed to refer to another object)**

Once initialized, a reference in C++ cannot be **reseated**, meaning it cannot be changed to reference another object.

```c++
#include <iostream>

int main()
{
    int x { 5 };
    int y { 6 };

    int& ref { x }; // ref is now an alias for x

    ref = y; // assigns 6 (the value of y) to x (the object being referenced by ref)
    // The above line does NOT change ref into a reference to variable y!

    std::cout << x << '\n'; // user is expecting this to print 5, whereas it prints 6

    return 0;
}
```

When a reference is evaluated in an expression, it resolves to the object it's referencing. 

So `ref = y` doesn't change `ref` to new reference `y`. Rather, because `ref` is an alias for `x`, the expression evaluates as if it was written `x = y`.

**Lvalue reference scope and duration**

Reference variables follow the same scoping and duration rules that normal variables do:

```c++
#include <iostream>

int main()
{
    int x { 5 }; // normal integer
    int& ref { x }; // reference to variable value

     return 0;
} // x and ref die here
```

**References and referents have independent lifetimes**

With one exception, the lifetime of a reference and the lifetime of its referent are independent. In other words, both of the following are true:

- A reference can be destroyed before the object it is referencing.
- The object being referenced can be destroyed the reference.

When a reference is destroyed before the referent, the referent is not impacted. For example:

```c++
#include <iostream>

int main()
{
    int x { 5 };

    {
        int& ref { x };   // ref is a reference to x
        std::cout << ref << '\n'; // prints value of ref (5)
    } // ref is destroyed here -- x is unaware of this

    std::cout << x << '\n'; // prints value of x (5)

    return 0;
} // x destroyed here
```

Results:

```
5
5
```

**Dangling references**

When an object being referenced is destroyed before a reference to it, the reference is left referencing an object that no longer exists. Such a reference is called **dangling reference**.

Accessing a dangling reference leads to undefined behavior.

**References aren't objects**

References are not objects in C++. A reference is not required to exist or occupy storage.

If possible, the compiler will optimize references away by replacing all occurrences of a reference with the referent. However, this isn't always possible, and in such cases, references may require storage.

Because references aren't objects, they can't be used anywhere an object is required (e.g. you can't have a reference to a reference, since an lvalue reference must reference an identifiable object).

In cases where you need a reference that is an object or a reference that can be reseated, `std::reference_wrapper` provides a solution.

Considering the following variables:

```c++
int var{};
int& ref1{ var };  // an lvalue reference bound to var
int& ref2{ ref1 }; // an lvalue reference bound to var
```

Because `ref1` is a reference to `var`, when used in an expression, `ref1` evaluates to `var`. So `ref2` is just a normal lvalue reference (as indicated by its type `int&`), bound to `var`.

A reference to a reference would have syntax `int&&` -- but since C++ doesn't support references to references, this syntax was repurposed in C++11 to indicate an rvalue.



### 12.4 Lvalue references to const

**Lvalue reference to const**

By using `const` keyword when declaring an lvalue reference, we tell an lvalue reference to treat the object it is referencing as const.

Such a reference is called an **lvalue reference to a const value** (sometimes called a **reference to const** or a **const reference**).

Because lvalue references to const treat the object they are referencing as const, they can be used to access but not modify the value being referenced:

```c++
#include <iostream>

int main()
{
    const int x { 5 };    // x is a non-modifiable lvalue
    const int& ref { x }; // okay: ref is a an lvalue reference to a const value

    std::cout << ref << '\n'; // okay: we can access the const object
    ref = 6;                  // error: we can not modify an object through a const reference

    return 0;
}
```

**Initializing an lvalue reference to const with a modifiable lvalue**

Lvalue references to const can also bind to modifiable lvalues. In such a case, the object being referenced is treated as const when accessed through the reference (even though the underlying object is non-const):

```c++
#include <iostream>

int main()
{
    int x { 5 };          // x is a modifiable lvalue
    const int& ref { x }; // okay: we can bind a const reference to a modifiable lvalue

    std::cout << ref << '\n'; // okay: we can access the object through our const reference
    ref = 7;                  // error: we can not modify an object through a const reference

    x = 6;                // okay: x is a modifiable lvalue, we can still modify it through the original identifier

    return 0;
}
```

**Initializing an lvalue reference to const with an rvalue**

Lvalues references to const can also bind to rvalues:

```c++
#include <iostream>

int main()
{
    const int& ref { 5 }; // okay: 5 is an rvalue

    std::cout << ref << '\n'; // prints 5

    return 0;
}
```

When this happens, a temporary object is created and initialized with the rvalue, and the reference to const is bound to that temporary object.

**Initializing an lvalue reference to const with a value of a different type**

Lvalue references to const can even bind to values of a different type, so long as those values can be implicitly converted to the reference type:

```c++
#include <iostream>

int main()
{
    // case 1
    const double& r1 { 5 };  // temporary double initialized with value 5, r1 binds to temporary

    std::cout << r1 << '\n'; // prints 5

    // case 2
    char c { 'a' };
    const int& r2 { c };     // temporary int initialized with value 'a', r2 binds to temporary

    std::cout << r2 << '\n'; // prints 97 (since r2 is a reference to int)

    return 0;
}
```

**Const references bound to temporary objects extend the lifetime of the temporary object**

Temporary objects are normally destroyed at the end of the expression in which they are created. 

To avoid dangling references in such cases, C++ has a special rule: When a const lvalue reference is *directly* bound to a temporary object, the lifetime of the temporary object is extended to match the lifetime of the reference.

```c++
#include <iostream>

int main()
{
    const int& ref { 5 }; // The temporary object holding value 5 has its lifetime extended to match ref

    std::cout << ref << '\n'; // Therefore, we can safely use it here

    return 0;
} // Both ref and the temporary object die here
```

Lifetime extension only works when a const reference is directly bound to temporary. Temporaries returned from a function (even ones returned by const reference) are not elligible for lifetime extension.

**Constexpr lvalue references**

When applied to a reference, `constexpr` allows the reference to be used in a constant expression.

Constexpr references hava a particular limitation: they can only be bound to objects with static duration (either globals or static locals). This is because the compiler knows where static objects will be instantiated in memory, so it can treat that address as a compile-time constant.

```c++
int g_x { 5 };

int main()
{
    [[maybe_unused]] constexpr int& ref1 { g_x }; // ok, can bind to global

    static int s_x { 6 };
    [[maybe_unused]] constexpr int& ref2 { s_x }; // ok, can bind to static local

    int x { 6 };
    [[maybe_unused]] constexpr int& ref3 { x }; // compile error: can't bind to non-static object

    return 0;
}
```

When defining a constexpr reference to a const variable, we need to apply both `cosntexpr` (which applies to the reference) and `const` (which applies to the type being referenced).

```c++
int main()
{
    static const int s_x { 6 }; // a const int
    [[maybe_unused]] constexpr const int& ref2 { s_x }; // needs both constexpr and const

    return 0;
}
```



### 12.5 Pass by lvalue reference

**Pass by reference**

One way to avoid making an expensive copy of an argument when calling a function is to use `pass by reference` instead of `pass by value`.

When using **pass by reference**, we declare a function parameter as a reference type (or const reference type) rather than as a normal type. 

When the function is called, each reference parameter is bound to the appropriate argument. Because the reference acts as an alias for the argument, no copy of the argument is made.

**Pass by reference allows us to change the value of an argument**

A reference acts identically to the object being referenced, when using pass by reference, any changes made to the reference parameter *will* affect the argument:

```c++
#include <iostream>

void addOne(int& y) // y is bound to the actual object x
{
    ++y; // this modifies the actual object x
}

int main()
{
    int x { 5 };

    std::cout << "value = " << x << '\n';

    addOne(x);

    std::cout << "value = " << x << '\n'; // x has been modified

    return 0;
}
```

Outputs:

```c++
value = 5
value = 6
```

**Pass by reference can only accept modifiable lvalue arguments**

Because a reference to a non-const value can only bind to a modifiable lvalue (essentially a non-const variable), this means that pass by reference only works with arguments that are modifiable lvalues.

```c++
#include <iostream>

void printValue(int& y) // y only accepts modifiable lvalues
{
    std::cout << y << '\n';
}

int main()
{
    int x { 5 };
    printValue(x); // ok: x is a modifiable lvalue

    const int z { 5 };
    printValue(z); // error: z is a non-modifiable lvalue

    printValue(5); // error: 5 is an rvalue

    return 0;
}
```



### 12.6 Pass by const lvalue reference

Unlike a reference to non-const (which can only bind to modifiable ivalues), a reference to const can bind to modifiable lvalues, non-modifiable lvalues, and rvalues.

```c++
#include <iostream>

void printRef(const int& y) // y is a const reference
{
    std::cout << y << '\n';
}

int main()
{
    int x { 5 };
    printRef(x);   // ok: x is a modifiable lvalue, y binds to x

    const int z { 5 };
    printRef(z);   // ok: z is a non-modifiable lvalue, y binds to z

    printRef(5);   // ok: 5 is rvalue literal, y binds to temporary int object

    return 0;
}
```

Passing by const reference offers the same primary benefit as pass by reference (avoiding making a copy of the argument), while also guaranteeing that function can *not* change the value being referenced.

**Passing values of a different type to a const lvalue reference parameter**

A const lvalue reference can bind to an value of a different type, as long as that value is convertable to the type of the reference.

The primary motivation for allowing this is so that we can pass a value as an argument to either a value parameter or a const reference parameter in exactly the same way.

```c++
#include <iostream>

void printVal(double d)
{
    std::cout << d << '\n';
}

void printRef(const double& d)
{
    std::cout << d << '\n';
}

int main()
{
    printVal(5); // 5 converted to temporary double, copied to parameter d
    printRef(5); // 5 converted to temporary double, bound to parameter d

    return 0;
}
```

**When to pass by (const) reference**

Because class types can be expensive to copy (sometimes significantly so):

- Class types are usually passed by const reference instead of by value to avoid making an expensive copy of the argument.
- Fundamental types are cheap to copy, so they are typically passed by value.

**The cost of pass by value vs pass by reference**

There are two key points that will help us understand when we should pass by value vs pass by reference:

**First**, the cost of copying an object is generally proportional to two things:

- The size of the object. Objects that use more memory take more time to copy.
- Any additional setup costs. Some class types do additional setup when they are instantiated (e.g. such as opening a file or database, or allocating a certain amount of dynamic memory to hold an object of a variable size). These setup costs must be paid each time an object is copied.

On the other hand, binding a reference to an object is always fast (about the same speed as copying a fundamental type).

**Second**, accessing an object through a reference is slightly more expensive than accessing an object through a normal variable identifier.

With a reference, there usually is an extra step: the program must first access the reference to determine which object is being referenced, and only then can it go to that memory address for that object and access the value.

The compiler can also sometimes optimize code using objects passed by value more highly than code using objects passed by reference. This means code generated to access objects passed by reference is typically slower than the code generaged for objects passed by value.

**Why we dont't pass everything by reference**

- For objects that are cheap to copy, the cost of copying is similar to the cost of binding, so we favor pass by value so the code generated will be faster.
- For objects that are expensive to copy, the cost of the copy dominates, so we favor pass by (const) reference to avoid making a copy.

**For function parameters, prefer `std::string_view` over `const std::string&` in most cases**

Im most cases, `std::string_view` is the better choice, as it can handle a wider range of argument types efficiently.

There are a few cases where using a `const std::string&` parameter may be more appropirate:

- If you're using C++14 or older, `std::string_view` isn't available
- If your function needs to call some other function that takes a C-style or `std::string` parameter, then `const std::string&` may be a better choice, as `std::string_view` is not guaranteed to be null-terminated (something that C-style string functions expect) and does not efficiently convert back to a `std::string`.



### 12.7 Introduction to pointers

**The address-of operator (&)**

The **address-of operator (&)** returns the memory address of its operand.

An example:

```c++
#include <iostream>

int main()
{
    int x{ 5 };
    std::cout << x << '\n';  // print the value of variable x
    std::cout << &x << '\n'; // print the memory address of variable x

    return 0;
}
```

Outputs:

```
5
0027FEA0
```

**The dereference operator (*)**

The **dereference operator (*)** (also occassionally called the **indirection operator**) returns the value at a given memory address as an lvalue:

```c++
#include <iostream>

int main()
{
    int x{ 5 };
    std::cout << x << '\n';  // print the value of variable x
    std::cout << &x << '\n'; // print the memory address of variable x

    std::cout << *(&x) << '\n'; // print the value at the memory address of variable x (parentheses not required, but make it easier to read)

    return 0;
}
```

**Pointers**

A **pointer** is an object that holds a *memory address* (typically of another variable) as its value.

In modern C++, the pointers we are talking about here are sometimes called "raw pointers" or "dumb pointers", to help differentiate them from "smart pointers".

**Pointer initialization**

Like normal variables, pointers are *not* initialized by default.

A pointer that has not been initialized is sometimes called a **wild pointer**. Wild pointers contain a garbage address, and dereferencing a wild pointer will result in undefined behavior. Because of this, you should always initialize your pointers to a known value.

Once we have a pointer holding the address of another object, we can then use the dereference operator (*) to access the value at that address. For example:

```c++
#include <iostream>

int main()
{
    int x{ 5 };
    std::cout << x << '\n'; // print the value of variable x

    int* ptr{ &x }; // ptr holds the address of x
    std::cout << *ptr << '\n'; // use dereference operator to print the value at the address that ptr is holding (which is x's address)

    return 0;
}
```

The type of the pointer has to match the type of the object being pointed to:

```c++
int main()
{
    int i{ 5 };
    double d{ 7.0 };

    int* iPtr{ &i };     // ok: a pointer to an int can point to an int object
    int* iPtr2 { &d };   // not okay: a pointer to an int can't point to a double object
    double* dPtr{ &d };  // ok: a pointer to a double can point to a double object
    double* dPtr2{ &i }; // not okay: a pointer to a double can't point to an int object

    return 0;
}
```

With one exception, initializing a pointer with a literal value is disallowed:

```c++
int* ptr{ 5 }; // not okay
int* ptr{ 0x0012FF7C }; // not okay, 0x0012FF7C is treated as an integer literal
```

**Pointers and assignment**

We can use assignment with pointers in two different ways:

1. To change what the pointer is pointing at (by assigning the pointer a new address)
2. To change the value being pointed at (by assigning the dereferenced pointer a new value)

**Differences between pointers and references**

| references                                        | pointers                         |
| ------------------------------------------------- | -------------------------------- |
| the address-of and dereference happens implicitly | happens explicitly               |
| must be initialized                               | are not required (but should be) |
| are not objects                                   | are objects                      |
| can not be reseated                               | can be reseated                  |
| must always be bound to an object                 | can point to nothing             |
| are "safe" (outside of dangling references)       | are inherently dangerous         |

**The address-of operator returns a pointer**

The address-of operator (&) doesn't return the address of its operand as a literal. Instead, it returns a pointer containing the address of the operand, whose type is derived from the argument (e.g. taking the address of an `int` will return the address in an `int` pointer).

```c++
#include <iostream>
#include <typeinfo>

int main()
{
	int x{ 4 };
	std::cout << typeid(&x).name() << '\n'; // print the type of &x

	return 0;
}
```

On Visual Studio, this printed:

```
int *
```

**The size of pointers**

The size of a pointer is dependent upon the architecture the executable is compiled for -- a 32-bit executable uses 32-bit memory addresses -- consequently, a pointer on a 32-bit machine is 32 bits (4 bytes). With a 64-bit executable, a pointer would be 64 bits (8 bytes). Note that this is true regardless of the size of the object being pointed to:

```c++
#include <iostream>

int main() // assume a 32-bit application
{
    char* chPtr{};        // chars are 1 byte
    int* iPtr{};          // ints are usually 4 bytes
    long double* ldPtr{}; // long doubles are usually 8 or 12 bytes

    std::cout << sizeof(chPtr) << '\n'; // prints 4
    std::cout << sizeof(iPtr) << '\n';  // prints 4
    std::cout << sizeof(ldPtr) << '\n'; // prints 4

    return 0;
}
```

**Dangling pointers**

Much like a dangling reference, a **dangling pointer** is a pointer that is holding the address of an object that is no longer valid.

Dereferencing an invalid pointer will lead to undefined behavior. Any other use of an invalid pointer value is implementation-defined.



### 12.8 Null pointers

**Null pointers**

A **null value** (often shortened to **null**) is a special value that means something has no value.

When a pointer is holding a null value, it means the pointer is not pointing at anything. Such a pointer is called a **null pointer**.

The easiest way to create a null pointer is to use value initialization:

```c++
int main()
{
    int* ptr {}; // ptr is now a null pointer, and is not holding an address

    return 0;
}
```

**The nullptr keyword**

Much like the keywords `true` and `false` represent Boolean literal values, the **nullptr** represents a null pointer literal.

We can use `nullptr` to explicitly initialize or assign a pointer a null value.

```c++
int main()
{
    int* ptr { nullptr }; // can use nullptr to initialize a pointer to be a null pointer

    int value { 5 };
    int* ptr2 { &value }; // ptr2 is a valid pointer
    ptr2 = nullptr; // Can assign nullptr to make the pointer a null pointer

    someFunction(nullptr); // we can also pass nullptr to a function that has a pointer parameter

    return 0;
}
```

**Dereferencing a null pointer results in undefined behavior**

Much like dereferencing a dangling (or wild) pointer leads to undefined behavior, dereferencing a null pointer also leads to undefined behavior.

**Checking for null pointers**

We can use a conditional to test whether a pointer has value `nullptr` or not:

```c++
#include <iostream>

int main()
{
    int x { 5 };
    int* ptr { &x };

    if (ptr == nullptr) // explicit test for equivalence
        std::cout << "ptr is null\n";
    else
        std::cout << "ptr is non-null\n";

    int* nullPtr {};
    std::cout << "nullPtr is " << (nullPtr==nullptr ? "null\n" : "non-null\n"); // explicit test for equivalence

    return 0;
}
```

Pointers will implicitly convert to Boolean values: a null pointer converts to Boolean value `false`, and a non-null pointer converts to Boolean value `true`.

The following program is equivalent to the prior one:

```c++
#include <iostream>

int main()
{
    int x { 5 };
    int* ptr { &x };

    // pointers convert to Boolean false if they are null, and Boolean true if they are non-null
    if (ptr) // implicit conversion to Boolean
        std::cout << "ptr is non-null\n";
    else
        std::cout << "ptr is null\n";

    int* nullPtr {};
    std::cout << "nullPtr is " << (nullPtr ? "non-null\n" : "null\n"); // implicit conversion to Boolean

    return 0;
}
```

==Note==: 

- Conditionals can only be used to differentiate null pointers from non-null pointers.
- There is no convenient way to determine whether a non-null pointer is pointing to a valid object or dangling (pointing to an invalid object).

**Use nullptr to avoid dangling pointers**

Dereferencing a pointer that is either null or dangling will result in undefined behavior.

We can easily avoid dereferencing a null pointer by using a conditional to ensure a pointer is non-null before trying to dereference it.

But there is no way to detect whether a pointer is dangling, we need to avoid having any dangling pointers in our program in the first place. We do that by ensuring that any pointer that is not pointing at a valid object is set to `nullptr`.

A pointer should either hold the address of a valid object, or be set to nullptr. That way we only need to test pointers for null, and can assume any non-null pointer is valid.

```c++
// Assume ptr is some pointer that may or may not be a null pointer
if (ptr) // if ptr is not a null pointer
    std::cout << *ptr << '\n'; // okay to dereference
else
    // do something else that doesn't involve dereferencing ptr (print an error message, do nothing at all, etc...)
```

**Legacy null pointer literals: 0 and NULL**

In older code, there are two other literal values used instead of `nullptr`.

1. The literal `0`:

   In the context of a pointer, the literal `0` is specially defined to mean a null value, and is the only time you can assign an integral literal to a pointer.

   ```c++
   int main()
   {
       float* ptr { 0 };  // ptr is now a null pointer (for example only, don't do this)
   
       float* ptr2; // ptr2 is uninitialized
       ptr2 = 0; // ptr2 is now a null pointer (for example only, don't do this)
   
       return 0;
   }
   ```

   On modern architectures, the address `0` is typically used to represent a null pointer. However, this value is not guaranteed by the C++ standard, and some architectures use other values. The literal `0`, when used in the context of a null pointer, will be translated into whatever address the architecture uses to represent a null pointer.

2. `NULL`:

   Additionally, there is a preprocessor macro named `NULL` (defined in the <cstddef> header).  This macro is inherited from C.

   ```c++
   #include <cstddef> // for NULL
   
   int main()
   {
       double* ptr { NULL }; // ptr is a null pointer
   
       double* ptr2; // ptr2 is uninitialized
       ptr2 = NULL; // ptr2 is now a null pointer
   
       return 0;
   }
   ```

Both `0` and `NULL` should be avoided in modern C++ (use `nullptr` instead).

**Favor references over pointers whenever possible**

```c++
int main()
{
    int* ptr { };

    {
        int x{ 5 };
        ptr = &x; // assign the pointer to an object that will be destroyed (not possible with a reference)
    } // ptr is now dangling and pointing to invalid object

    if (ptr) // condition evaluates to true because ptr is not nullptr
        std::cout << *ptr; // undefined behavior

    return 0;
}
```

Since references can’t be bound to null, we don’t have to worry about null references. And because references must be bound to a valid object upon creation and then can not be reseated, dangling references are harder to create.

Because they are safer, references should be favored over pointers, unless the additional capabilities provided by pointers are required.



### 12.9 Pointers and const

With normal (non-const) pointers, we can change both what the pointer is pointing at (by assigning the pointer a new address to hold) or change the value at the address being held (by assigning a new value to the dereferenced pointer).

We can't set a normal pointer to point at a const varibale.

```c++
int main()
{
    const int x { 5 }; // x is now const
    int* ptr { &x };   // compile error: cannot convert from const int* to int*

    return 0;
}
```

**Pointer to const value**

A **pointer to a const value** (sometimes called a `pointer to const` for short) is a (non-const) pointer that points to a constant value.

To declare a pointer to a const value, use the `const` keyword before the pointer's data type:

```c++
int main()
{
    const int x{ 5 };
    const int* ptr { &x }; // okay: ptr is pointing to a "const int"

    *ptr = 6; // not allowed: we can't change a const value

    return 0;
}
```

However, because a pointer to const is not const itself (it just points to a const value), we can change what the pointer is pointing at by assigning the pointer a new address:

```c++
int main()
{
    const int x{ 5 };
    const int* ptr { &x }; // ptr points to const int x

    const int y{ 6 };
    ptr = &y; // okay: ptr now points at const int y

    return 0;
}
```

Just like a reference to const, a pointer to const can point to non-const variables too.

A pointer to const treats the value being pointed to as constant, regradless of whether the object at that address was initially defined as const or not:

```c++
int main()
{
    int x{ 5 }; // non-const
    const int* ptr { &x }; // ptr points to a "const int"

    *ptr = 6;  // not allowed: ptr points to a "const int" so we can't change the value through ptr
    x = 6; // allowed: the value is still non-const when accessed through non-const identifier x

    return 0;
}
```

**Const pointers**

We can also make a pointer itself constant. A **constant pointer** is a pointer whose address can not be changed after initialization.

To decalre a const pointer, use the `const` keyword after the asterisk in the pointer declaration:

```c++
int main()
{
    int x{ 5 };
    int* const ptr { &x }; // const after the asterisk means this is a const pointer

    return 0;
}
```

Just like a normal const variable, a const pointer must be initialized upon definition, and this value can't be changed via assignment:

```c++
int main()
{
    int x{ 5 };
    int y{ 6 };

    int* const ptr { &x }; // okay: the const pointer is initialized to the address of x
    ptr = &y; // error: once initialized, a const pointer can not be changed.

    return 0;
}
```

However, because the *value* being pointed to is non-const, it is possible to change the value being pointed to via dereferencing the const pointer:

```c++
int main()
{
    int x{ 5 };
    int* const ptr { &x }; // ptr will always point to x

    *ptr = 6; // okay: the value being pointed to is non-const

    return 0;
}
```

**Const pointer to a const value**

```c++
int main()
{
    int value { 5 };
    const int* const ptr { &value }; // a const pointer to a const value

    return 0;
}
```

A const pointer to a const value can not have its address changed, nor can the value it is pointing to be changed through the pointer. It can only be ereferenced to get the value it is pointing at.

**Pointer and const recap**

To summarize, only to remember 4 rules:

1. A non-const pointer can be assigned another address to change what it is pointing at.
2. A const pointer always point to the same address, and this address can not be changed.
3. A pointer to a non-const value can change the value it is pointing to. These can not point to a const value.
4. A pointer to a const value treats the value as const when accessed through the pointer, and thus can not change the value it is pointing to.  These can be pointed to const or non-const l-values (but not r-values, which don't have an address).

Keeping the declaration syntax straight can be a bit challenging:

- A `const` before the asterisk is associated with the  type being pointed to. Therefore, this is a pointer to a const value,  and the value cannot be modified through the pointer.
- A `const` after the asterisk is associated with the pointer itself. Therefore, this pointer cannot be assigned a new address.

```c++
int main()
{
    int v{ 5 };

    int* ptr0 { &v };             // points to an "int" but is not const itself, so this is a normal pointer.
    const int* ptr1 { &v };       // points to a "const int" but is not const itself, so this is a pointer to a const value.
    int* const ptr2 { &v };       // points to an "int" and is const itself, so this is a const pointer (to a non-const value).
    const int* const ptr3 { &v }; // points to a "const int" and is const itself, so this is a const pointer to a const value.

    // if the const is on the left side of the *, the const belongs to the value
    // if the const is on the right side of the *, the const belongs to the pointer

    return 0;
}
```



### 12.10 Pass by address

 **Pass by address**

C++ provides a third way to pass values to a function (besides by reference or by value), called **pass by address.**

With  **pass by address**, instead of providing an object as an argument, the caller provides an object's *address* (via a pointer).

```c++
void printByAddress(const std::string* ptr)
{
    std::cout << *ptr << '\n'; // print the value via the dereferenced pointer
}
```

**Null checking**

In most cases, it is more effective to test whether the function parameter is null as a precondition and handle the negative case immediately.

```c++
#include <iostream>

void print(int* ptr)
{
    if (!ptr) // if ptr is a null pointer, early return back to the caller
        return;

    // if we reached this point, we can assume ptr is valid
    // so no more testing or nesting required

    std::cout << *ptr << '\n';
}

int main()
{
	int x{ 5 };

	print(&x);
	print(nullptr);

	return 0;
}
```

If a null pointer should never be passed to the function, an `assert` can be used instead (or also) (as asserts are intended to document things that should never happen):

```c++
#include <iostream>
#include <cassert>

void print(const int* ptr) // now a pointer to a const int
{
	assert(ptr); // fail the program in debug mode if a null pointer is passed (since this should never happen)

	// (optionally) handle this as an error case in production mode so we don't crash if it does happen
	if (!ptr)
		return;

	std::cout << *ptr << '\n';
}

int main()
{
	int x{ 5 };

	print(&x);
	print(nullptr);

	return 0;
}
```

**Prefer pass by (const) reference**

Pass by const reference has a few advantages over pass by address/

1. Because an object being passed by address must have an address, only lvalues can be passed by address (as rvalues don't have addresses). Pass by const reference is more flexible, as it can accept lvalues and rvalues:

   ```c++
   #include <iostream>
   
   void printByValue(int val) // The function parameter is a copy of the argument
   {
       std::cout << val << '\n'; // print the value via the copy
   }
   
   void printByReference(const int& ref) // The function parameter is a reference that binds to the argument
   {
       std::cout << ref << '\n'; // print the value via the reference
   }
   
   void printByAddress(const int* ptr) // The function parameter is a pointer that holds the address of the argument
   {
       std::cout << *ptr << '\n'; // print the value via the dereferenced pointer
   }
   
   int main()
   {
       printByValue(5);     // valid (but makes a copy)
       printByReference(5); // valid (because the parameter is a const reference)
       printByAddress(&5);  // error: can't take address of r-value
   
       return 0;
   }
   ```

2. The syntax for pass by reference is natural, as we can just pass in literals or objects. With pass by address, our code ends up littered with ampersands (&) and asterisks (*).

Prefer pass by reference to pass by address unless you have a specific reason to use pass by address.

**Pass by address for "optional" arguments**









## 14. Introduction to Classes

### 14.1 Procedural programming versus object-oriented programming

In programming, properties are represented by **objects**, and behaviors are represented by **functions**.

In **procedual programming**, the functions and the data those functions operate on are separate entities. The programmer is responsible for combining the functions and the data together to produce the desired result. And thus, procedural programming represents reality fairly poorly.

In **object-oriented programming** (often abbreviated as OOP), the focus is on creating program-defined data types that contain both properties and a set of well-defined behaviors. The term "object" in OOP refers to the objects that we can instantiate from such types.



### 14.2 Intorduction to classes

