# C Programming Notes

This repository contains **well-structured theoretical notes with practical C programs** covering **C fundamentals, data types, operators, control flow, arrays, strings, pointers, pointer arithmetic, functions, recursion, structures, unions, dynamic memory allocation, file handling, and preprocessor concepts**.

The content is designed for:

- 📘 University exams  
- 🧠 Concept revision  
- 💻 Viva & interviews  
- 🧪 Practice and future reference  

---

## 📚 Table of Contents (Click to Navigate)

| Chapter | Topic |
|------|------|
| 1 | [C Basics & Fundamentals](#c-basics--fundamentals) |
| 2 | [Variables & Data Types](#variables--data-types) |
| 3 | [Operators](#operators) |
| 4 | [Control Statements](#control-statements) |
| 5 | [Arrays](#arrays) |
| 6 | [Strings](#strings) |
| 7 | [Pointers](#pointers) |
| 8 | [Functions & Recursion](#functions--recursion) |
| 9 | [Structures & Unions](#structures--unions) |
| 10 | [Dynamic Memory Allocation](#dynamic-memory-allocation) |
| 11 | [File Handling](#file-handling) |
| 12 | [Preprocessor Directives](#preprocessor-directives) |
| 13 | [Common Mistakes & Exam Traps](#common-mistakes--exam-traps) |

---

## C Basics & Fundamentals

- Structure of a C program  
- Compilation process  
- Keywords, identifiers, constants  

---

## Variables & Data Types

- Primitive data types  
- Size of data types  
- Type conversion  

---

## Operators

- Arithmetic operators  
- Relational operators  
- Logical operators  
- Bitwise operators  
- Assignment operators  

---

## Control Statements

- `if`, `if-else`, `else-if`
- `switch`
- Loops (`for`, `while`, `do-while`)
- `break`, `continue`

---

## Arrays

- One-dimensional arrays  
- Array initialization  
- Array traversal  

---

## Strings

- Character arrays  
- String functions  
- Difference between char array and string literal  

---

## Pointers

## 📌 Topics Covered

* Pointer definition and fundamentals
* Address-of (`&`) and dereferencing (`*`)
* Pointer to pointer
* Pointer arithmetic
* Arrays and pointer relationships
* Array traversal using pointers
* Array of pointers
* Complex pointer declarations
* Common mistakes and exam traps

---

## 🔹 Definition

A **pointer** is a variable that stores the **memory address of another variable**.

```c
int *ptr;
```

* The pointer type determines how many bytes are accessed during dereferencing
* Pointers must be **initialized before dereferencing**

---

## 🔹 Dereferencing

**Dereferencing** means accessing the **value stored at the memory address held by a pointer**.

```c
int x = 10;
int *p = &x;

printf("%d", *p); // Output: 10
```

---

## 📁 Programs Included

---

## 📄 1.c – Pointer and Pointer to Pointer

```c
#include<stdio.h>

int main(){
    int x = 10; // Assume address of x is 1000

    int *ptr1;   // pointer to int (assume address 2000)
    int **ptr2;  // pointer to pointer to int

    ptr1 = &x;
    ptr2 = &ptr1;

    printf("%u\n", x);       // 10
    printf("%u\n", &x);      // 1000
    printf("%u\n", ptr1);    // 1000
    printf("%u\n", *ptr1);   // 10
    printf("%u\n", &ptr1);   // 2000
    printf("%u\n", ptr2);    // 2000
    printf("%u\n", *ptr2);   // 1000
    printf("%u\n", **ptr2);  // 10
    
    return 0;
}
```

### 🔍 Key Concepts

* `ptr1` stores the address of `x`
* `ptr2` stores the address of `ptr1`
* Each `*` removes **one level of indirection**

---

## 📄 2.c – Pointer Arithmetic with Arrays

```c
#include <stdio.h>

int main()
{
    int arr[] = {1, 2, 3, 4, 5};
    int *ptr1 = &arr[0];

    *(ptr1 + 4) *= 10; // Updates arr[4] = 50

    ptr1 += 2; // ptr1 now points to arr[2]

    int size = sizeof(arr) / sizeof(arr[0]);

    for (int i = 0; i < size; i++)
    {
        printf("%d\t", arr[i]);
        printf("%d\t", *(arr + i));
    }

    while (ptr1 < arr + size)
    {
        printf("%d\n", *ptr1);
        ptr1++;
    }

    return 0;
}
```

### 🔍 Key Concepts

* `arr == &arr[0]`
* Pointer arithmetic moves by `sizeof(data_type)`
* Pointer traversal must stay **within array bounds**

---

## 📄 3.c – Array Indexing vs Pointer Notation

```c
#include<stdio.h>

int main() {
    int arr[] = {1,2,3,4,5};

    printf("%d %d\n", arr[0], *(arr)); 
    printf("%d %d\n", arr[1], *(arr + 1)); 
    printf("%d %d\n", arr[2], *(arr + 2)); 
    printf("%d %d\n", arr[3], *(arr + 3)); 
    printf("%d %d\n", arr[4], *(arr + 4));

    int *ptr[] = {arr + 1, arr + 3, arr + 5, arr, arr + 4};

    printf("%d %d\n", *(arr + 3), **(ptr + 1));

    return 0;
}
```

### 🔍 Key Concepts

* `arr[i] == *(arr + i)`
* Array of pointers stores addresses of array elements
* `**(ptr + 1)` follows the address chain

---

## 📄 5.c – Complex Pointer Declarations

```c
#include<stdio.h>

int main() {
    int *(p1[3]);        // array of 3 pointers to int
    int (*p2)[3];        // pointer to array of 3 integers
    int *p3(int, int);   // function returning pointer to int

    return 0;
}
```

### 🔍 Key Concepts

* Parentheses change binding order
* Use **clockwise / spiral rule** to read declarations
* `int *p1[3]` is NOT the same as `int (*p2)[3]`

---

## Functions & Recursion

* Function declaration and definition
* Call by value vs call by reference
* Recursive functions

---

## Structures & Unions

* Structure definition and access
* Difference between structure and union
* Nested structures

---

## Dynamic Memory Allocation

* `malloc()`
* `calloc()`
* `realloc()`
* `free()`

---

## File Handling

* File modes
* `fopen()`, `fclose()`
* Reading and writing files

---

## Preprocessor Directives

* `#define`
* `#include`
* Macros
* Conditional compilation

---

## Common Mistakes & Exam Traps

| Mistake                             | Result             |
| ----------------------------------- | ------------------ |
| Dereferencing uninitialized pointer | Undefined behavior |
| Pointer out of array bounds         | Undefined behavior |
| Using `NULL` with int arrays        | Logical error      |
| Confusing pointer declarations      | Wrong answer       |

---

## 🧠 One-Line Exam Summary

> **Pointers store addresses, dereferencing accesses values, pointer arithmetic depends on data type size, arrays decay to pointers, and pointer operations must always stay within valid memory bounds.**

---

## ✅ Usage

This repository can be used for:

* Exam preparation
* Interview revision
* Understanding low-level C concepts
* Quick reference for developers

---

## 📌 Author Notes

These notes are written with a focus on **clarity, correctness, and exam-readiness**, using practical examples and commonly tested concepts.

Happy Learning 🚀
