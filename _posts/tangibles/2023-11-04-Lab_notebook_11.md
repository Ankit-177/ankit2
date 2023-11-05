---
toc: true
comments: false
layout: post
title: Lab notebook 11
description: This shows planning and notes from hacks.
type: tangibles
courses: { compsci: {week: 11} }
---

# Learnings:
- Simulations team lesson notes:
    - A simulation, in context of computer science, is a digital representation of a situation in the real world.
    - Algorithmic efficiency:
        - A problem is a general description of a task that can (or cannot) be solved algorithmically
        - A decision problem is a problem with a yes/no answer
        - An optimization problem is a problem with the goal of finding the "best" solution among many
        - Efficiency is an estimate of the amount of computational resources used by an algorithm
        - An algorithm's efficiency is determined through formal or mathematically reasoning
    - Sorting methods:
        - Bubble Sort: Bubble sort is a simple sorting algorithm that repeatedly steps through the list, compares adjacent elements, and swaps them if they are in the wrong order. The pass through the list is repeated until no swaps are needed, which means the list is sorted.
        - Quick Sort: Quick sort is a popular divide-and-conquer sorting algorithm. It divides the array into smaller sub-arrays and recursively sorts them. It's generally more efficient than Bubble Sort for larger lists.

# Errors:
- The rating system for our books failed to work as we had an unresolved `fetch` error when the stars were clicked in the "Ratings" column.