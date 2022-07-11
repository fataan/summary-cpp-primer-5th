# Chapter 2. Variables and Basic Types

## 2.1. Primitive Built-in Types
cpp defined two primitive type, that is arithmatic types and void(not return value)

### 2.1.1. Arithmetic Types
Arithmetic types devided two type, integral type(including character and boolean) and floating-point type

|type|meaning|size|
|--|--|--|
|short|short integer|16 bits|
|int|integer|32 bits|
|long| long integer|64 bits|
|float|single-precision floating-point|32 bits|
|double|double-precision floating-point|64 bits|
|char|charachter|8 bits|
|wchar_t|wide charachter|16 bits|
|char16_16|unicode|16 bits|
|char32_32|unicode|32 bits|
|bool|boolean|8 bits|

bool represents truht values true and false.

char is guaranteed to be big
enough to hold numeric values corresponding to thecharacters in the machine’s basic
character set.

wchar_t, char16_t, char_32 are used
for extended character sets

int type represent integer. short and long is smalled and extended integer type,respectively.

floating-point types represent single-, double-, and extended-precision values. The float and double types typically yield about 7 and 16 significant digits, respectively.

** signed and unsigned type **
Except for bool and the extended character types, the integral types may be signed
or unsigned. A signed type represents negative or positive numbers (including zero);
an unsigned type represents only values greater than or equal to zero.unsigned type not has bit for sign in binary, so this type represent only 0 and positive number.

### 2.1.2. Type Conversions
The type of an object defines the data that an object might contain and what operations that object can perform. Among the operations that many types support is the ability to convert objects of the given type to other, related types. Type conversions happen automatically when we use an object of one type where an object of another type is expected

```cpp
bool a = 42; // a is true
int i = a; // i has value 1
i = 3.15; // i has value 3
double pi = i; // pi has value 3.0
unsigned char c = -1; // c has 255
signed char c2 = 256; // undefined
```
> The rules for signed-to-unsigned conversion say that the value is reduced modulo UINT_MAX + 1, so -1will convert to UINT_MAX (which is probably 0xffffffff or 4294967295 if unsigned int is 32 bits).

```cpp 
signed char c2 = 256; // undefined
```
output undefined because signed char max value is 128

#### Expressions Involving Unsigned Types
```cpp
unsigned u = 10;
int i = -42;
std::cout << i + i << std::endl; // output: -84
std::cout << u + i << std::endl; // output: 4294967264
```
variable i will converts to unsigned before addition. according to the rules UINT_MAX + 1 for converts signed, so -42 will be 4,294,967,254.
4294967254 + 10 = 4294967264

```cpp
for (unsigned u = 10; u >= 0; --u)
 std::cout << u << std::endl
```
this code will be infinite loops, because conditional always be true. unsigned never negative!

### 2.1.3. Literals
A value, such as 42, is known as a literal becaus its value self-evident. Every literal has a type. The form and value of a literal determine its type. 

#### Integer Literals
```cpp
20 /* decimal */ 024 /* octal */ 0x14 /* hexadecimal */
```
Integer literals are expressed in two types i.e.,
1. Prefixes which indicates the base.
2. Suffixes which indicates the type.

Prefix represent four types:
1. Decimal-literal(base 10):- a non-zero decimal digit followed by zero or more decimal digits(0, 1, 2, 3, 4, 5, 6, 7, 8, 9). For example, 56, 78.

2. Octal-literal(base 8):- a zero followed by zero or more octal digits(0, 1, 2, 3, 4, 5, 6, 7). For example, 045, 076, 06210.

3. Hex-literal(base 16):- 0x or 0X followed by one or more hexadecimal digits(0, 1, 2, 3, 4, 5, 6, 7, 8, 9, a, A, b, B, c, C, d, D, e, E, f, F). For example, 0x23A, 0Xb4C, 0xFEA.

4. Binary-literal(base 2):- 0b or 0B followed by one or more binary digits(0, 1). For example, 0b101, 0B111.


|Suffix|Data Type|
|--|--|
||int|
|U or u|unsigned int|
|L or l|long int|
|UL or ul|unsigned long int|
|LL or ll|long long int|
|ULL or ull|unsigned long long int|

#### Floating-Point Literal
By default, floating-point literals have type double. We can override the default using
a suffix.

|suffix|type|
|--|--|
|F or f|float|
|L or l|long double|

### Character and Character String Literals.

```cpp
'a' // character literal
"b" // string literal
```
A character enclosed within single quotes is a literal of type char. Zero or more
characters enclosed in double quotation marks is a string literal
|prefix|type|
|--|--|
|u|chart_16|
|U|chart_32|
|L|wchart_t|

### Escape Sequences
we use an escape sequence to represent such characters. An escape sequence begins with a backslash. 
```cpp
cout << "\n"; // print a newline
cout << "\thalo!\n"; // print a tab followed halo! and a new line
```
We can also write a generalized escape sequence, hich is \x followed by one or more hexadecimal digits or a \ followed by one, two, or three octal digits. The value represents the numerical value of the character. 

```cpp 
// Latin-1
cout << '\115'; // print M
cout << '\x24'; // print $
```

## 2.2. Variables
A variable provides us with named storage that our programs can manipulate. Each
variable in C++ has a type. The type determines the size and layout of the variable’s
memory, the range of values that can be stored within that memory, and the set of
operations that can be applied to the variable. C++ programmers tend to refer to
variables as “variables” or “objects” interchangeably.

### 2.2.1. Variable Definitions
A simple variable definition consists of a type specifier, followed by a list of one or
more variable names separated by commas, and ends with a semicolon. Each name in
the list has the type defined by the type specifier. A definition may (optionally) provide
an initial value for one or more of the names it defines:
```cpp
int sum = 0, value, // sum, value, and units_sold have type int
units_sold = 0; // sum and units_sold have initia value 0
Sales_item item; // item has type Sales_item (see § 1.5.1 (p. 20))
// string is a library type, representing a variable-length sequence of characters
std::string book("0-201-78345-X"); // book initialized from string literal
```
#### Initializers
An object that is initialized gets the specified value at the moment it is created.

```cpp
//intialized var1 before it used for intialzed var2
int var1 = 12, int var2 = a;
```
> Initialization is not assignment. Initialization happens when a variable is given
a value when it is created. Assignment obliterates an object’s current value
and replaces that value with a new one.

#### Default Initialization
When we define a variable without an initializer, the variable is default initialized.
Such variables are given the “default” value. What that default value is depends on
the type of the variable and may also depend on where the variable is defined.

The value of an object of built-in type that is not explicitly initialized depends on
where it is defined. Variables defined outside any function body are initialized to zero. variables of built-in type
defined inside a function are uninitialized. The value of an uninitialized variable of
built-in type is undefined. It is an error to copy or otherwise try to
access the value of a variable whose value is undefined

```cpp
std::string empty; // empty implicitly initialized to the empty string
Sales_item item; // default-initialized Sales_item object
```
Most classes let us define objects without explicit initializers. Such classes supply an
appropriate default value for us. For example, as we’ve just seen, the library string
class says that if we do not supply an initializer, then the resulting string is the
empty string.

### 2.2.2. Variable Declarations and Definitions
A declaration makes a name known to the program. A file that wants to
use a name defined elsewhere includes a declaration for that name. A definition
creates the associated entity.

> A variable declaration specifies the type and name of a variable. A variable definition
is a declaration. In addition to specifying the name and type, a definition also allocates
storage and may provide the variable with an initial value.

To obtain a declaration that is not also a definition, we add the extern keyword
and may not provide an explicit initializer:
```cpp
extern int i; // declaration but no define i
int j; // declaration and define j
extern int k = 3; //declaration and define k. Any declaration that includes an explicit initializer is a definition.
```
It is an error to provide an initializer on an extern inside a function.

> Variables must be defined exactly once but can be declared many times.

more example:
```cpp
#include <iostream>

using namespace std;

void printN(int b); // declaration 

int main()
{
	printN(3);
}

void printN(int b) // declaration and define
{
	cout << b;
}
```
```cpp
// main.cpp
#include <iostream>

using namespace std;

int main()
{
	extern int a; // declaration
	cout << a;
}

// anotherfile.h (or .cpp)
extern int a = 3; // definition
```
### 2.2.3. Identifiers
Identifiers in C++ can be composed of letters, digits, and the underscore character.
The language imposes no limit on name length. Identifiers must begin with either a
letter or an underscore. Identifiers are case-sensitive; upper- and lowercase letters are
distinct:

```cpp
// defines four different int variables
int somename, someName, SomeName, SOMENAME;
```
The language reserves a set of names may not be used as identifiers. The standard also reserves a set of names for use in the standard library. The
identifiers we define in our own programs may not contain two consecutive
underscores, nor can an identifier begin with an underscore followed immediately by
an uppercase letter. In addition, identifiers defined outside a function may not begin
with an underscore.


## 2.3. Compound Types
A compound type is a type that is defined in terms of another type. 
generally, a declaration is a base type
followed by a list of declarators. Each declarator names a variable and gives the
variable a type that is related to the base type.

### 2.3.1. References
A reference defines an alternative name for an object. A reference type “refers to”
another type. We define a reference type by writing a declarator of the form &d,
where d is the name being declared:
```cpp
int ival = 1024;
int &refVal = ival; // refVal refers to (is another name for) ival
int &refVal2; // error: a reference must be initialized
```
When we define a reference, instead of copying the initializer’s
value, we bind the reference to its initializer. Once initialized, a reference remains
bound to its initial object. There is no way to rebind a reference to refer to a different
object. Because there is no way to rebind a reference, references must be initialized.
> reference not an object, so its not have a region of storage and address(altought its, initial object its)
#### A Reference Is an Alias
After a reference has been defined, all operations on that reference are actually
operations on the object to which the reference is bound.
```cpp                                    
int ival = 1024;
int &refVal = ival; // refVal refers to (is another name for) ival             
int i = refVal; // i = ival
```
#### Reference Definitions
We can define multiple references in a single definition. Each identifier that is a
reference must be preceded by the `&` symbol.
```cpp
int i = 1024, i2 = 2048; // i and i2 are both ints
int &r = i, &r2 = i2; // r and r2 both is reference
```
### 2.3.2. Pointers
A pointer is a compound type that “points to” another type. Like references, pointers
are used for indirect access to other objects. Unlike a reference, a pointer is an object
in its own right. Pointers can be assigned and copied; a single pointer can point to
several different objects over its lifetime. Unlike a reference, a pointer need not be
initialized at the time it is defined. Like other built-in types, pointers defined at block
scope have undefined value if they are not initialized.

#### Pointer Definitions
We define a pointer type by writing a declarator of the form `*d`, where d is the
name being defined. The `*` must be repeated for each pointer variable:
```cpp
int *ip1, *ip2; // both ip1 and ip2 are pointers to int
double dp, *dp2; // dp2 is a pointer to double; dp is a double
```
#### Taking the Address of an Object
A pointer holds the address of another object. We get the address of an object by using
the address-of operator (the `&` operator):
```cpp
int ival = 42;
int *p = &ival; // p holds the address of ival; p is a pointer to ival
```
The second statement defines p as a pointer to int and initializes p to point to the
int object named ival. Because references are not objects, they don’t have
addresses. Hence, we may not define a pointer to a reference.

#### Pointer Value
The value (i.e., the address) stored in a pointer can be in one of four states:
1. It can point to an object.
2. It can point to the location just immediately past the end of an object.(like array, last index +1)
3. It can be a null pointer, indicating that it is not bound to any object.
4. It can be invalid; values other than the preceding three are invalid.

Although pointers in cases 2 and 3 are valid, there are limits on what we can do
with such pointers. Because these pointers do not point to any object, we may not
use them to access the (supposed) object to which the pointer points. If we do
attempt to access an object through such pointers, the behavior is undefined.

#### Using a Pointer to Access an Object
When a pointer points to an object, we can use the dereference operator (the `*`
operator) to access that object.
```cpp
int ival = 42;
int *p = &ival; // p holds the address of ival; p is a pointer to ival
cout << *p; // * yields the object to which p points; prints 42
```
#### Null Pointers
A null pointer does not point to any object. Code can check whether a pointer is null
before attempting to use it. There are several ways to obtain a null pointer:
```cpp
int *p1 = nullptr; // equivalent to int *p1 = 0;
int *p2 = 0; // directly initializes p2 from the literal constant 0
```
> If possible, define a pointer only after the object to which it should
point has been defined. If there is no object to bind to a pointer, then
initialize the pointer to nullptr or zero. That way, the program can detect
that the pointer does not point to an object.

#### void Pointers 
```cpp                                            int ival = 2;
void *pval = &ival; // ok
float *p2val = &ival; // error type not matching.
```  
The type `void*` is a special pointer type that ca
n hold the address of any object. Like
any other pointer, a `void*` pointer holds an address, but the type of the object at  
that address is unknown. because address is unkno
we can't use dereference operator and operate on t
he object it addresses.                             
```cpp
char val = 'a';
char *pval = &val;
void *p2val = &val;      

++*pval; // ok: encode val + 1 become 'b'
++*p2val; // error
```

## 2.4. const Qualifier
A variable whose value we know cannot be changed. This variable should initialized after create it.
```cpp
const int bufSize = 512; // ok
bufSize = 500; // error: attemp assign bufSize
const int i; // error: must initialized
```
#### 2.4.1. References to const
a reference to const cannot be used to change the
object to which the reference is bound.
we can bind a reference to
const to a nonconst object, a literal, or a more general expression.
```cpp
const int val = 4;
const int &ref1 = val; // bind a const object

int dval = 5;
const int &ref2 = dval; // bind a nonconst object
```
#### 2.4.2. Pointers and const
As with references, we can define pointers that point to either const or nonconst
types. Like a reference to const, a pointer to const may not be
used to change the object to which the pointer points. We may store the address of a
const object only in a pointer to const.
```cpp
const int val = 2;
const int *dval = &val;
*dval = 4; // error: cannot change value of pointer points(i.e val)

int val2 = 15;
dval = &val2; // ok: can point to noconst object and the value pointer(i.e address) can change.
```

##### const pointer
we can have a pointer that is itself const. so we cannot change the value of pointer(i.e address).
```cpp
int errNumb = 0;
int *const curErr = &errNumb;
*dval = 4;// ok: the value of pointer points can chnage(i.e errNumb)

int errNumb2 = 5;
dval = &errNumb2 // error: cannot chage value of pointer(i.e address errNumb)

const int val = 3;
const int *const dval = &val; // dval is a const pointer to a const
object
```
> the easiest way to understand these declarations is to
read them from right to left.
In this case, the symbol closest to curErr is const,
which means that curErr itself will be a const object. The type of that object is
formed from the rest of the declarator. The next symbol in the declarator is `*`, which means that curErr is a const pointer. Finally, the base type of the declaration
completes the type of curErr, which is a const pointer to an object of type int.

### 2.4.3. Top-Level const
More generally, top-level const indicates that an object itself is const. Top-level
const can appear in any object type, i.e., one of the built-in arithmetic types, a class
type, or a pointer type. Low-level const appears in the base type of compound types
such as pointers or references. Note that pointer types, unlike most other types, can
have both top-level and low-level const independently.

```cpp
int i = 0;
int *const p1 = &i; // we can't change the value of p1; const is top-level
const int ci = 42; // we cannot change ci; const is top-level
const int *p2 = &ci; // we can change p2; const is low-level
const int *const p3 = p2; // right-most const is top-level, left-most is not
const int &r = ci; // const in reference types is always low-level
```

The distinction between top-level and low-level matters when we copy an object.
When we copy an object, top-level consts are ignored:
```cpp
i = ci; // ok: copying the value of ci; top-level const in ci is ignored
p2 = p3; // ok: pointed-to type matches; top-level const in p3 is ignored
```
low-level const is never ignored. When we copy an object,
both objects must have the same low-level const qualification or there must be a
conversion between the types of the two objects. In general, we can convert a
nonconst to const but not the other way round:
```cpp
int *p = p3; // error: p3 has a low-level const but p doesn't
p2 = p3; // ok: p2 has the same low-level const qualification as p3
p2 = &i; // ok: we can convert int* to const int*
int &r = ci; // error: can't bind an ordinary int& to a const int object
const int &r2 = i; // ok: can bind const int& to plain int
```

