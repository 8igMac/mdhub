Effective C++ Note
===

## Item 1: Understand Template Type Deduction
```cpp
template<typename T>
void f(ParamType param);

f(expr);
```

### Case 1: _ParamType_ is a Reference or Pointer, But Not a Universal Reference
1. If _expr_’s type is a reference/pointer, ignore the reference/pointer part.
2. Then pattern-match _expr_’s type against _ParamType_ to determine T.
> Note: passing a const object to a template taking a T& parameter is safe: the 
constness of the object becomes part of the type deduced for T.

### Case 2: _ParamType_ is a Universal Reference
- If _expr_ is an lvalue, both T and ParamType are deduced to be lvalue references.
That’s doubly unusual. First, it’s the only situation in template type deduction
where T is deduced to be a reference. Second, although ParamType is declared
using the syntax for an rvalue reference, its deduced type is an lvalue reference.
- If _expr_ is an rvalue, the “normal” (i.e., Case 1) rules apply.

### Case 3: _ParamType_ is Neither a Pointer nor a Reference
1. As before, if expr’s type is a reference, ignore the reference part.
2. If, after ignoring expr’s reference-ness, expr is const, ignore that, too. 
If it’s volatile, also ignore that.

> Note: 
1. array passed by value in the function _param_ is deduced as pointer
2. array passed by reference in the function _param_ is deduced as reference to array

> Note: Interestingly, the ability to declare references to arrays enables 
creation of a template that deduces the number of elements that an array contains:
```cpp
// return size of an array as a compile-time constant. (The
// array parameter has no name, because we care only about
// the number of elements it contains.)
template<typename T, std::size_t N>
constexpr std::size_t arraySize(T (&)[N]) noexcept 
{
    return N;
}
```

> Note: Arrays aren’t the only things in C++ that can decay into pointers. Function types can
decay into function pointers, and everything we’ve discussed regarding type deduc‐
tion for arrays applies to type deduction for functions and their decay into function
pointers.
```cpp
void someFunc(int, double); // someFunc is a function;
                            // type is void(int, double)
template<typename T>
void f1(T param); // in f1, param passed by value

template<typename T>
void f2(T& param); // in f2, param passed by ref

f1(someFunc); // param deduced as ptr-to-func;
              // type is void (*)(int, double)

f2(someFunc); // param deduced as ref-to-func;
              // type is void (&)(int, double)
```

## Item 2: Understand auto type deduction
**With only one curious exception, auto type deduction is template type
 deduction.**
- Think of **auto** as **T**
- Thind of type specifier as __ParamType__

### different then template type deduction
When the initializer for an auto-declared variable is enclosed in braces, 
the deduced type is a std::initializer_list. If such a type can’t be deduced
 (e.g., because the values in the braced ini‐tializer are of different types), 
the code will be rejected:
```cpp
auto x1 = 27; // type is int, value is 27

auto x2(27); // ditto

auto x3 = { 27 }; // type is std::initializer_list<int>,
                  // value is { 27 }

auto x4{ 27 }; // ditto
```
```cpp
auto x5 = { 1, 2, 3.0 }; // error! can't deduce T for
                         // std::initializer_list<T>
```
So the only real difference between auto and template type deduction is that auto
assumes that a braced initializer represents a std::initializer_list, but template
type deduction doesn’t.

> Note: auto in a function return type or a lambda parameter implies template type
deduction, not auto type deduction.
