---
toc: true
comments: false
layout: post
title: Lab notebook 10
description: This shows planning and notes from hacks.
type: tangibles
courses: { compsci: {week: 10} }
---

# Learnings:
- Developing procedures team lesson notes:
    - A procedure is a named group of programming instructions:
        - Procedure Parameters: variables that are defined within the procedure's parentheses and serve as placeholders for values that can be passed to the procedure when it is called, allowing the procedure to operate on different data or values each time it is executed.
        - Procedure Algorithms: a step-by-step set of instructions that defines a specific task or operation to be performed within a computer program
        - Procedure Return Values: data or results that a procedure can send back to the part of the program that called it, allowing the procedure to provide information or perform a specific task and then share the outcome with the rest of the program.

- Libraries team lesson notes:
    - In Python, a library is a collection of pre-written code, functions, and modules that extend the language's capabilities.
        - Examples of third-party Python libraries: NumPy, Pandas, Matplotlib, TensorFlow, Django, Flask, Random.
        - To install a library, run the `pip install [library name]` command.
            - To use a library in a program, one must first import it using `import [library name]` at the beginning of the program.
    - Libraries and APIs:
        - A file that contains procedures that cane be used in a program is called a <strong>library</strong>
        - An <strong>Application Program Interface (API)</strong> provides specifications for how procedures in a library behave and can be used. 
        - APIs define the methods and functions that are available for developers to interact with a library. They specify how to make requests, provide inputs, and receive outputs, creating a clear and consistent way to use library features.

# Errors:
- We were initially unable to connect our `nav.basics` files, which were our menus, to our `.md` files which contained our genre information and JavaScript code that connected our API to our JavaScript DOM tables. To fix this, we needed to include a `{include nav_[filename].html}` line at the top of each file.