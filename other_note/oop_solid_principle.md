OOP - SOLID principles
===
{%youtube VUvEDg30FyY %}
[Toc]

## Single responsibility 
 **_Code should be one and only one reason to change_**
 
Big fat class problem:
- When you update code, you run higher risk to break the module
- Hard to test
- If we're talking about collaboration, the problems above will just be more serious.

It is better to separte big class into small class upon their "single responsibility."
 

## Open close
**_Code should open to extension but closed to modification_**

While you scale up the program(add new functions or classes), you shouldn't have to change the old code. This is for better scalability.

## Liskov subtitutability
**_Anywhere you use a base class you should able to use a subclass and not know it_**

When you replace the subclass, the base class should not feel it, i.e. **interface consistency**.

## Interface Segregation 
**_Don't force client to use interface they don't need_**

Example: It is only reasonable to tell the computer screen to display(output) content but to implement a input method on it is wierd. That is, the input method of a computer screen is undefined. So it is better to  **separate I/O interface into I and O.**

## Dependency Inversion
**_High level modules shouldn't rely on low level modules, both should rely on abstract_**

Example: Online music stream should be separate out the low level modules that handle sound cards and net stream.

Example: C++ implement a middle abstract class iterator to connect hight level STL algorithms and low level STL containers.

## Extra - Tell Don't Ask
**_Tell objects to do the work. Don't ask them for their data_**

Example: Instead of asking for data of the object members(**bill.item**) and sum them up, we should implement a method on that object that does the job and we can just call the object method(**bill.sum()**).
