---
toc: true
comments: false
layout: post
title: Lab notebook 8
description: This shows planning and notes from hacks.
type: tangibles
courses: { compsci: {week: 8} }
---

# Learnings:
- Algorithms team lesson notes:
    - Algorithms are step-by-step procedures or sets of rules used to solve problems or perform tasks
    - Example of CollegeBoard pseudo code for addition:
        ```
        num1 --> 5
        num2 --> 10
        sum --> num1 + num2
        display(sum)
        ```
    - Selection:
        - Decision to make based on a given circumstance
        - Ex: is it raining? If so, bring an umbrella outside
    - Iteration
        - Also referred to as repetition
        - After performing steps of a procedure/problem, iteration means checking to see if a task is completed
        - Refers back accordingly
    - Algorithms can be represented using flowcharts, Pseudo Code, or programming languages
    - Conditional statements
        - Conditional statements (if-else statements) allow a program to make decisions based on certain conditions
        - Enable different code branches to be executed depending on whether a condition is true or false
    - Loops
        - Loops (for loops, while loops) enable repetitive execution of code
        - They are used when a set of instructions needs to be repeated multiple times.
    - Strings
        - A string is a data type used to represent text or sequences of characters
        - Strings are commonly used in programming for tasks like input/output and text processing
    - A Fibonacci sequence is a series of numbers in which each number is the sum of the two preceding ones. It commonly starts with 0 and 1, and the sequence continues infinitely.
        - Code example:  
                ```
                def fibonacci(n):
                if n <= 0:
                    return []
                elif n == 1:
                    return [0]
                elif n == 2:
                    return [0, 1]
                else:
                    fib_sequence = [0, 1]
                    while len(fib_sequence) < n:
                        next_number = fib_sequence[-1] + fib_sequence[-2]
                        fib_sequence.append(next_number)
                    return fib_sequence

                    n = 10
                    result = fibonacci(n)
                    print(result)
                ```

# Errors:
- No errors of note.