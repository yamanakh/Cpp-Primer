### Setting up C++ on Windows

[Configure VS Code for Microsoft C++](https://code.visualstudio.com/docs/cpp/config-msvc)

### Setting up C++ on Linux

TBA

**255**? why? please look at [this](http://www.tldp.org/LDP/abs/html/exitcodes.html)

## Exercises Section 1.2
### Exercise 1.3
> Write a program to print Hello, World on the standard output.

```cpp
#include <iostream>

int main()
{
    std::cout << "Hello, World" << std::endl;
    return 0;
}
```

### Exercise 1.4
> Our program used the addition operator, +, to add two numbers. Write a program that uses the multiplication operator, *, to print the product instead.

```cpp
#include <iostream>

int main()
{
    std::cout << "Enter two numbers:" << std::endl;
    int v1 = 0, v2 = 0;
    std::cin >> v1 >> v2;
    std::cout << "The product is " << v1 * v2 << std::endl;
    return 0;
}
```

### Exercise 1.5

> We wrote the output in one large statement. Rewrite the program to use a separate statement to print each operand.

```cpp
#include <iostream>

int main()
{
    std::cout << "Enter two numbers:" << std::endl;
    int v1 = 0, v2 = 0;
    std::cin >> v1 >> v2;
    std::cout << "The product of ";
    std::cout << v1;
    std::cout << " and ";
    std::cout << v2;
    std::cout << " is ";
    std::cout << v1 * v2;
    std::cout << std::endl;
    return 0;
}
```

### Exercise 1.6
> Explain whether the following program fragment is legal.

It is illegal because no object class was defined beforehand. If we compile it we get the following error message:

**[Error] expected primary-expression before '<<' token**

Solution 1: remove the spare semicolons.
```cpp
std::cout << "The sum of " << v1 << " and " << v2 << " is " << v1 + v2 << std::endl;
```
Solution 2: insert _std::cout_ in front of each line as done in excercise

## Exercises Section 1.3
### Exercise 1.7

> Compile a program that has incorrectly nested comments.

Example:
```cpp
/*
* comment pairs /* */ cannot nest.
* ''cannot nest'' is considered source code,
* as is the rest of the program
*/
int main()
{
    return 0;
}
```

Compiling this code results in several warning and error codes.

### Exercise 1.8

> Indicate which, if any, of the following output statements are legal:
```cpp
std::cout << "/*";
std::cout << "*/";
std::cout << /* "*/" */;
std::cout << /* "*/" /* "/*" */;
```
> After you’ve predicted what will happen, test your answers by compiling a
program with each of these statements. Correct any errors you encounter.

Compiled result:
```cpp
std::cout << "/*";  /* -> Compilation successfull. */
std::cout << "*/";  /* -> Compilation successfull. */
```
1) These two lines are fine as the syntax for the start and end of a comment is within quotation marks, thus read as a string.

```cpp
std::cout << /* "*/" */;    /* -> Compilation unsuccessfull. */
```
2) This line is problematic. The first comment pair is fine /* "\*/ but the second " and \*/ are on their own.

```cpp
std::cout << /* "*/" /* "/*" */;    /* -> Compilation successfull. */
```
3) This line looks similar to the previous case but The middle part, " /* ", is read as a string and thus fine.

To **correct the mistake** just add an additional quotation mark on line 3:
```cpp
std::cout << "/*";
std::cout << "*/";
std::cout << /* "*/" */";
std::cout << /* "*/" /* "/*" */;
```

Output:

    /**/ */ /* 

## Exercises Section 1.4.1
### Exercise 1.9
> Write a program that uses a while to sum the numbers from 50 to 100.

```cpp
#include <iostream>
int main()
{
    int sum = 0, val = 50;
    while (val <= 100) {
        sum += val;
        ++val;
    }
    std::cout << "The sum of all numbers from 50 to 100 inclusive is " << sum << std::endl;
    return 0;
}
```

### Exercise 1.10
Use the decrement operator (--) to write a while that prints the numbers from ten down to zero.

```cpp
#include <iostream>
int main()
{
    int val = 10;
    while (val >= 0) {
        std::cout << val << std::endl;
        --val;
    }
    return 0;
}
```

### Exercise 1.11
Write a program that prompts the user for two integers.Print each number in the range specified by those two integers.

```cpp
#include <iostream>
int main()
{
    std::cout << "Enter two numbers:" << std::endl;
    int v1 = 0, v2 = 0;
    std::cin >> v1 >> v2;

    if (v1 > v2) {
        int temp = v1;
        v1 = v2;
        v2 = temp;
    }

    while (v1 <= v2) {
        std::cout << v1 << std::endl;
        ++v1;
    }
    return 0;
}
```

## Exercises Section 1.4.2
### Exercise 1.12
> What does the following for loop do? What is the final value
of sum?
```cpp
int sum = 0;
for (int i = -100; i <= 100; ++i)
    sum += i;
```

Answer: The for loop sums all numbers from -100 to 100 inclusive. The result is 0.

### Exercise 1.13
> Rewrite the exercises from § 1.4.1 (p. 13) using for loops.

Ex1.9:
```cpp
#include <iostream>
int main()
{
    int sum = 0;
    for (int val = 50; val <= 100; ++val)
        sum += val;
    std::cout << "The sum of all numbers from 50 to 100 inclusive is " << sum << std::endl;
    return 0;
}
```

Ex1.10:
```cpp
#include <iostream>
int main()
{
    for (int val = 10; val >= 0; --val)
        std::cout << val << std::endl;
    return 0;
}
```

Ex1.11:
```cpp
#include <iostream>
int main()
{
    std::cout << "Enter two numbers:" << std::endl;
    int v1 = 0, v2 = 0;
    std::cin >> v1 >> v2;

    if (v1 > v2) {
        int temp = v1;
        v1 = v2;
        v2 = temp;
    }

    for (int small = v1; small <= v2; ++small)
        std::cout << small << std::endl;
    return 0;
}
```

### Exercise 1.14
> Compare and contrast the loops that used a for with those using a while. Are there advantages or disadvantages to using either form?

[Answer to a similar question on Stack Overflow](http://stackoverflow.com/questions/2950931/for-vs-while-in-c-programming)

Short summary:
*A while loop will always evaluate the condition first.
A do/while loop will always execute the code in the do{} block first and then evaluate the condition.
A for loop allows you to initiate a counter variable, a check condition, and a way to increment your counter all in one line.
At the end of the day, they are all still loops, but they offer some flexibility as to how they are executed.*

### Exercise 1.15
> Write programs that contain the common errors discussed in the box on page 16. Familiarize yourself with the messages the compiler generates.

**Syntax Errors**:
```c++
int main(){
    std::cout << "Hello World!" << std::endl // semicolon missing 
    return 0;
}
```

**Type errors**:
```c++
int main(){
    char s = "Hello World!"; // Here char should be std::string
    std::cout << s << endl;
    return 0;
}
```

**Declaration errors**:
```c++
int main(){
    int k = 0;
    std::cout << K << std::endl; // use of undeclared identifier 'K'
    return 0;
}
```

## Exercises Section 1.4.3
### Exercise 1.16

```cpp
#include <iostream>
int main()
{
    int sum = 0;
    for (int val; std::cin >> val; sum += val);
    std::cout << sum << std::endl;

    return 0;
}
```
## Exercises Section 1.4.4
### Exercise 1.17

> What happens in the program presented in this section if the input values are all equal? What if there are no duplicated values?

If the input values are all equal, it will print a line which shows the count of the number you input.

If there are no duplicated values, when different values input, a new line will be printed if you click `Enter`.

### Exercise 1.18

> Compile and run the program from this section giving it only equal values as input. Run it again giving it values in which no number is repeated.

![run](https://db.tt/F38zExnq)

## Exercise 1.19

> Revise the program you wrote for the exercises in § 1.4.1 (p. 13) that printed a range of numbers so that it handles input in which the first number is smaller than the second.

[code](https://github.com/pezy/Cpp-Primer/blob/master/ch01/ex1_11.cpp)

## Exercise 1.20

> http://www.informit.com/title/032174113 contains a copy of Sales_item.h in the Chapter 1 code directory. Copy that file to your working directory. Use it to write a program that reads a set of book sales transactions, writing each transaction to the standard output.

[Here](ex1_20.cpp) is the code.

Note : C++11 flag need to enable.
For GCC and Clang, this can be done with the `-std=c++11`

## Exercise 1.21
> Write a program that reads two Sales_item objects that have the same ISBN and produces their sum.

The program should check whether the objects have the same ISBN.

[Code](ex1_21.cpp)

## Exercise 1.22

> Write a program that reads several transactions for the same ISBN. Write the sum of all the transactions that were read.

Tips: this program will appear in the section 1.6.

[Here](ex1_22.cpp) is the code.

![run](https://db.tt/UlkuvpAS)

## Exercise 1.23
> Write a program that reads several transactions and counts
how many transactions occur for each ISBN.

Tip: please review the `1.4.4`.

[Here](ex1_23.cpp) is the code.

## Exercise 1.24
> Test the previous program by giving multiple transactions
representing multiple ISBNs. The records for each ISBN should be grouped
together.

`data/book.txt` may be used as the records.

![run](https://db.tt/EeDI7lvN)

## Exercise 1.25
> Using the Sales_item.h header from the Web site,
compile and execute the bookstore program presented in this section.

It is the same as Exercise 1.22.

![run](https://db.tt/C6OOPuzA)
