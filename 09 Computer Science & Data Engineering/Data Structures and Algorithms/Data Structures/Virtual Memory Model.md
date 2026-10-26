---
title: "Virtual Memory Model"
domain: "Computer Science & Data Engineering"
course: "Data Structures and Algorithms"
unit: "Data Structures"
level: BSc
status: drafted
confidence: 0
tags: [data-structures-algorithms]
---
The Virtual Memory Model is a model that describes how an operating system organizes and presents physical memory to each program. Instead of working directly with the physical memory, each process receives a job that looks like a continuous block. Inside this space, there is:
1. The code segment: saves the code instructions
2. The data segment: saves the global and static variables
3. The stack, which saves local variables and function calls. Grows downwards.
4. The heap: grows upwards and dynamically saves created data. 