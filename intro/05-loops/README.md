# Loops, for, while and goto

A loop is a control flow statement that allows you to repeat a block of code. 

# while loop

This loop is used when you want to execute a block of code an unknown number of times, as long as a certain condition is true. It has the following syntax:

Syntax:
```c++
while (condition) {
    // code block to be executed
}
```
Example:
```c++
int nums = 10;
while (nums>=0) {
    cout << nums << endl;
    nums--;
}
```

If the block is only one statement, it can be expressed without `{}`s.

Syntax:
```c++
while (condition) 
    // statement goes here
```
Example:
```c++
int nums = 10;
while (nums>=0) 
    cout << nums-- << endl;
```

# do-while loop

This is similar to the `while` loop, but it is guaranteed to execute at least once.

Syntax: 

```c++
do {
    // code block to be executed
} while (condition);
```

Example:
```c++
int x = 0;
do{
    cout << x << endl;
    x++;
} while(x<10);
```

If the block is only one statement, it can be expressed without `{}`s.

Syntax:
```c++
do
    // single statement goes here
while (condition);    
```
Example:
```c++
int x = 0;
do 
    cout << x++ << endl;
while (x<=10);
```

# for loop

This loop is used when you know in advance how many times you want to execute a block of code.

- The initialization part is executed only once, at the beginning of the loop. It is used to initialize any loop variables.
- The condition is evaluated at the beginning of each iteration of the loop. If the condition is true, the code block inside the loop is executed. If the condition is false, the loop is terminated.
- The increment part is executed at the end of each iteration of the loop. It is used to update the loop variables.

Syntax:
```c++
for (initialization; condition; step_iteration) {
    // code block to be executed
}
```

Example:
```c++
for(int i=10; i<=0; i--){
    cout << i << endl; 
}
```

If the block is only one statement, it can be expressed without `{}`s.

Syntax:
```c++
for (initialization; condition; step_iteration)
    // single statement goes here
```
Example:
```c++
for(int i=10; i<=0; i--)
    cout << i << endl;
```

# range based loops

A range-based loop is a loop that iterates over a range of elements. The declaration type should follow the same type of the elements in the range. 

Syntax:
```c++
for (declaration : range) {
    // code block to be executed
}
```
or
```c++
for (declaration : range)
    // single statement
```

To avoid explaining arrays and vectors now, assume `v` as an iterable container that can hold multiple elements. I am going to use auto here to avoid explaining this topic any further.
```c++
auto v = {1, 2, 3, 4, 5}; // an automatically inferred iterable container with multiple elements
for (int x : v) {
    cout << x << " ";
}
```

It is possible to automatically generate ranges  
```c++
#include <ranges>
#include <iostream>
using namespace std;
int main() {  
    // goes from 0 to 9. in iota, the first element is inclusive and the last one is exclusive.
    for (int i : views::iota(0, 10))  
        cout << i << ' ';
}
```

# Loop Control Statements

## `break`

`break` keyword defines a way to break the current loop and end it immediately.

```c++
// check if it is prime
int num; 
cin >> num; // read the number to be checked if is prime or not
bool isPrime = true;
for(int i=2; i<num; i++){
    if(num%i==0){ // check if i divides num
        isPrime = false;
        break; // this will break the loop and prevent further precessing
    }
}
```

## `continue`

`continue` keyword is used to skip the following statements of the loop and move to the next iteration.

```c++
// print all even numbers
for (int i = 1; i <= 10; i++) {
    if (i % 2 == 1)
        continue;
    cout << i << " "; // this statement is skipped if odd numbers
}
```

## `goto`

[You should avoid `goto` keyword](https://isocpp.github.io/CppCoreGuidelines/CppCoreGuidelines#Res-goto). PERIOD. The only acceptable usage is to break multiple nested loops at the same time. But even in this case, is better to use `return` statement and `functions` that you're going to see later in this course.  

The `goto` keyword allows you to transfer control to a labeled statement elsewhere in your code. 

Example on how to create a loop using labels and goto. You can create a loop just using labels(anchors) and goto keywords. But this syntax is hard to debug and read. Avoid it at all costs:

```c++
#include <iostream>
using namespace std;
int main() {
    int i=0;
    start: // this a label named as start.
    cout << i << endl;
    i++;
    if(i<10)
        goto start; // jump back to start
    else
        goto finish; // jump to finish
    finish: // this a label named as finish.
    return 0;
}
```

Example on hov to jump over and skip statements:
```c++
#include <iostream>

int main() {
    int x = 10;

    goto jump_over_this;  // control jumps to the label below

    x = 20;  // this line of code is skipped

    jump_over_this:  // label for goto statement
    std::cout << x << std::endl;  // outputs 10

    return 0;
}
```

Example of an arguably acceptable use of `goto`. Here you can see the usage of a way to break both loops at the same time. If you use `break`, you will only break the inner loop. In this situation it is better to break your code into functions to reduce complexity and nesting. 
```c++
for (int i = 0; i < imax; ++i)
    for (int j = 0; j < jmax; ++j) {
        if (i + j > elem_max) goto finished;
        // ...
    }
finished:
// ...
```

# Loop nesting

You can nest loops by placing one loop inside another. The inner loop will be executed completely for each iteration of the outer loop. Here is an example of nesting a for loop inside another for loop:

```c++
for (int i = 0; i < 10; i++) {
  for (int j = 0; j < 5; j++) {
    cout << "i: " << i << " j: " << j << endl;
  }
}
```

# Infinite loops

A infinite loop is when the code loops indefinitely without having a way out. Here goes some examples:

```c++
while(true)
    cout << "Hello World!" << endl; 
```

```c++
for(;;)
    cout << "Hello World!" << endl; 
```

```c++
int i = 0;
while(i<10); // note the ';' here, it will run indefinitely an empty statement because it won't reach the scope.
{
    cout << i << endl;
    i++;
}
```

# Homework

Do all exercises up to this topic here https://www.w3schools.com/cpp/exercise.asp

In this activity, you will have to solve Fibonacci sequence. You should implement using loops, and variables. Do not use arrays nor closed-form formulas.

- [Easy Fibonacci](https://www.beecrowd.com.br/judge/en/problems/view/1151)

Optional Readings on [Fibonacci Sequence](https://en.wikipedia.org/wiki/Fibonacci_number);

Hint: Create two variables, one to store the current value and the previous value. Each iteration step calculate the sum of both and store and put into a temp variable. Copy the current into the previous and set the current with the temporary you calculated before. 