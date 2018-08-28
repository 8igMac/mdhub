Effective C++ Note
===
[TOC]

# Deducing Type
## Item 1: Understand Template Type Deduction
```c++
template <typename T>
void f(ParamType param);

f(expr); // deduce T and ParamType from expr
```
1. Param type is a reference or pointer, but not a universal reference
    - If _expr_'s type is a reference, ignore the reference part.
    - Then pattern-match _expr_'s type against _ParamType_ to determin T.

For example:
```c++
// this is our template
template<typename T>
void f(T& param); // param is a reference

// and we have these variable declarations
int x = 27; // x is an int
const int cx = x; // cx is a const int
const int& rx = x; // rx is a reference to x as a const int

// the deduced types for param and T in various calls are as follows:
f(x); // T is int, param's type is int&
f(cx); // T is const int, param's type is const int&
f(rx); // T is const int, param's type is const int&
// rx’s reference-ness is ignored during type deduction.
```

2. Param type is universal reference
    - If _expr_ is an lvalue, both T and _ParamType_ are deduced to be lvalue references. That’s doubly unusual. First, it’s the only situation in template type deduction where T is deduced to be a reference. Second, although ParamType is declared using the syntax for an rvalue reference, its deduced type is an lvalue reference.
    - If expr is an rvalue, the “normal” (i.e., Case 1) rules apply.
    
For example:
```c++
template<typename T>
void f(T&& param); // param is now a universal reference
int x = 27;
const int cx = x;
const int& rx = x; 

f(x); // x is lvalue, so T is int&, param's type is also int&
f(cx); // cx is lvalue, so T is const int&, param's type is also const int&
f(rx); // rx is lvalue, so T is const int&, param's type is also const int&
f(27); // 27 is rvalue, so T is int, param's type is therefore int&&
```
3. Param type is neither a pointer nor a reference
    - As before, if expr’s type is a reference, ignore the reference part.
    - If, after ignoring expr’s reference-ness, expr is **const**, ignore that, too. If it’s **volatile**, also ignore that.

For example:
```c++
template<typename T>
void f(T param); // param is now passed by value

int x = 27;
const int cx = x;
const int& rx = x; // as before

f(x); // T's and param's types are both int
f(cx); // T's and param's types are again both int
f(rx); // T's and param's types are still both int
```
:::info
If the argument passed is of type **const char * const** and param is case 3, the result will be **const char\***
:::

4. Array argument
Array types are different from pointer
types, even though they sometimes seem to be interchangeable.
```c++
const char name[] = "J. P. Briggs"; // name's type is const char[13]
const char * ptrToName = name; // array decays to pointer
```
Here, the const char* pointer ptrToName is being initialized with name, which is a const char[13]. These types (const char* and const char[13]) are not the same, but because of the **array-to-pointer decay rule**, the code compiles.

Consider the following example:
```c++

```