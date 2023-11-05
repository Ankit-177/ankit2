---
toc: true
comments: false
layout: post
title: Lab notebook 9
description: This shows planning and notes from hacks.
type: tangibles
courses: { compsci: {week: 9} }
---

# Learnings:
- Lists and searches team lesson notes:
    - Basic list operations:
        ```
        #Defining the List
        aList= [1,4,2,6,7,3,]
        #Accessing Elements in a list
        print(aList[1])


        #Storing Element at an Index to a variable
        Element = aList[3]
        print(Element)


        #Setting an Element at an Index to a variable
        element = 4
        aList[5]= element
        print(aList[5])

        #Insert a value at a certain index
        aList.insert(3, 10)
        print(aList[3])

        #Adding another value to the list (append)
        aList.append(5)
        print(aList)

        #Removing a value from the List at a specific Index
        aList.remove(2)
        print(aList)

        #Accessing the Length of a list
        print(len(aList))
        ```
    - Steps to performing a binary search:
        - index: organizing the data by assigning a reference value to each element
        - Put the number is order either ascending or descending
        - Search starts with middle number first which is found by adding the highest and lowest index number and dividing it by 2
        - This divides the range by 2
        - Repeat this process by shrinking the range each time till the desired target is found
        - Every time the process is repeated and leads to a target it is considered a comparison
    - Steps to performing a sequential search:
        - Each element in a list is examined in the order of the first element till the desired target
        - Order doesn’t matter

# Errors:
- No errors of note.