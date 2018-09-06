Modern C++
===

# stream
- istream <- ifstream, istringstream
- ostream <- ofstream, ostringstream

# constexpr
- object: const and its value can be known in compile time.
- function: 'can' produce compile time known result if its argument are also compile time known.
- constexpr permit cout, can use non-type template function to print

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
