Modern C++
===

### TOC
- [Template Metaprogramming - Metafuntion](#meta_func)
- [Concept](#concept)

<a name="meta_func"></a>
# Template Metaprogramming - Metafuntion
- C++ template is a turing complete sublaguage of C++
- compile-time evaluate
- accept types and compile-time constants as prameter and return **types/constants**
- usually impl as class template with specialization
- [Boost::MPL](https://www.boost.org/doc/libs/1_68_0/libs/mpl/doc/index.html) provides a large collection of metafunction and compile-time data
structure to simplify C++ template metaprogramming.

example code 1:
```cpp
template <bool, class L, class R>
struct IF
{
  typedef R type; 
};

template <class L, class R>
struct IF<true, L, R>
{
  typedef L type; 
};

IF<false, int, long>::type i; // is equivalent to long i;
IF<true,  int, long>::type i; // is equivalent to int i;

```
example code 2:
```cpp
template <int N>
struct Factorial 
{
    enum { value = N * Factorial<N - 1>::value };
};
 
template <>
struct Factorial<0> 
{
    enum { value = 1 };
};
 
// Factorial<4>::value == 24
// Factorial<0>::value == 1
void foo()
{
    int x = Factorial<4>::value; // == 24
    int y = Factorial<0>::value; // == 1
}
```

<a name="concept"></a>
# Concepts
- because compiler can generate a bounch of nested error message 
for template deduction error, concept introduce a safe guard
upan template parameter, and let the compiler produce a more readable
error message.
- type contrain for type
- will be implemented in c++20

# stream
- istream <- ifstream, istringstream
- ostream <- ofstream, ostringstream

# constexpr
- object: const and its value can be known in compile time.
- function: 'can' produce compile time known result if its argument are also compile time known.
- constexpr permit cout, can use non-type template function to print
example code 1:

# lambda function

# Namespace
Namespaces provide a method for preventing name conflicts in large projects. 
- namespace alias: define an alternate name for deep-nested namespace

# Rvalue reference
Rvalue refernce 是C++11之後才有的物件，他的存在是為了解決以下兩個問題
- move sematic
- fastfowarding

## move sematic
move assignment operator
move constructor

## std::move
將lvalue轉成rvalue

## if-it-has-a-name 原則
- Rvalue reference 屬於lvalue如果他有名子
- Rvalue reference 屬於rvalue如果他沒有名子

# STL
## Container
### sequence container v.s associative container
What is the difference between sc and ac?

### set v.s map
- map seems redundent to store an extra 'key' than set. Why do we need map?

key value is always immutable.
