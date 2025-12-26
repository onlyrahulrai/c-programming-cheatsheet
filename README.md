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

# Pointers

Pointers are one of the **most powerful and challenging concepts in C**.
They form the foundation for **arrays, strings, functions, dynamic memory allocation, and data structures**.

---

## 📚 Topics Covered

* Pointer definition and fundamentals
* Address-of (`&`) and dereferencing (`*`)
* Pointer to pointer (multiple indirection)
* Pointer arithmetic rules
* Arrays and pointers relationship
* Array traversal using pointers
* Array of pointers
* Complex pointer declarations
* Common mistakes and exam traps

---

## 🔹 What is a Pointer?

A **pointer** is a variable that stores the **memory address of another variable**.

```c
int *ptr;
```

### Key Notes

* Pointer type defines:

  * Size of data accessed
  * Behavior of pointer arithmetic
* Pointers **must be initialized before dereferencing**

❌ Undefined Behavior

```c
int *p;
printf("%d", *p);
```

✅ Correct Usage

```c
int x = 10;
int *p = &x;
```

---

## 🔹 Address-of (`&`) Operator

* Returns the **memory address** of a variable
* Applicable only to **lvalues**

```c
int x = 10;
int *p = &x;
```

---

## 🔹 Dereferencing (`*`) Operator

Dereferencing means **accessing the value stored at the address held by a pointer**.

```c
printf("%d", *p);  // prints 10
```

Each `*` removes **one level of indirection**.

---

# 📄 1.c – Pointer and Pointer to Pointer

```c
#include<stdio.h>

int main(){
    int x = 10; // Assume address of x is 1000

    int *ptr1;   // pointer to integer (assume address 2000)
    int **ptr2;  // pointer to pointer to integer

    ptr1 = &x;
    ptr2 = &ptr1;

    printf("%u\n", x);
    printf("%u\n", &x);
    printf("%u\n", ptr1);
    printf("%u\n", *ptr1);
    printf("%u\n", &ptr1);
    printf("%u\n", ptr2);
    printf("%u\n", *ptr2);
    printf("%u\n", **ptr2);

    return 0;
}
```

---

## 🧠 Memory Diagram

```
Memory Layout:

Address     Value        Variable
---------------------------------
1000        10           x
2000        1000         ptr1
3000        2000         ptr2
```

### Access Flow

```
ptr2  ──▶  ptr1  ──▶  x  ──▶  10
  *          *          *
```

### Explanation Table

| Expression | Meaning           |
| ---------- | ----------------- |
| `ptr1`     | Address of `x`    |
| `*ptr1`    | Value of `x`      |
| `ptr2`     | Address of `ptr1` |
| `*ptr2`    | Address of `x`    |
| `**ptr2`   | Value of `x`      |

---

## 📄 2.c – Pointer Arithmetic with Arrays

```c
#include <stdio.h>

int main()
{
    int arr[] = {1, 2, 3, 4, 5};
    int *ptr1 = &arr[0];

    *(ptr1 + 4) *= 10; // arr[4] = 50

    ptr1 += 2; // points to arr[2]

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

---

## 🧠 Memory Diagram (Array + Pointer)

```
Address     Value
-----------------
1000        1   ← arr[0]
1004        2   ← arr[1]
1008        3   ← arr[2]
1012        4   ← arr[3]
1016        50  ← arr[4]
```

```
ptr1 initially → 1000
ptr1 + 1       → 1004
ptr1 + 2       → 1008
```

### Key Rules

* `arr == &arr[0]`
* Pointer arithmetic moves by `sizeof(data_type)`
* Traversal must stay **within array bounds**

---

## ✔ Allowed vs ❌ Not Allowed

| Expression  | Valid |
| ----------- | ----- |
| `ptr + 1`   | ✅     |
| `ptr++`     | ✅     |
| `ptr - 1`   | ✅     |
| `ptr + ptr` | ❌     |
| `ptr * 2`   | ❌     |

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

---

## 🧠 Memory Diagram (Array of Pointers)

```
ptr array:

ptr[0] → &arr[1]
ptr[1] → &arr[3]
ptr[2] → &arr[2] 
ptr[3] → &arr[0]
ptr[4] → &arr[4]
```

```
**(ptr + 1)
 → *(ptr[1])
 → *( &arr[3] )
 → arr[3]
```

---

## 📄 4.c – Complex Pointer Declarations

```c
#include<stdio.h>

int main() {
    int *(p1[3]);        // array of 3 pointers to int
    int (*p2)[3];        // pointer to array of 3 integers
    int *p3(int, int);   // function returning pointer to int

    return 0;
}
```

---

## 🧠 Declaration Reading (Spiral Rule)

1. Start from variable name
2. Move right → left
3. Respect parentheses

### VERY IMPORTANT DIFFERENCE

```c
int *p1[3];    // Array of pointers
int (*p2)[3];  // Pointer to array
```

❗ **These are NOT the same**

---

## ⚠️ Common Mistakes & Exam Traps

* Dereferencing uninitialized pointers
* Accessing array out of bounds
* Confusing `arr` with `&arr`
* Incorrect pointer arithmetic
* Ignoring parentheses in declarations

---

## ✅ Final Summary

* Pointer stores **address**
* Dereferencing gives **value**
* Arrays and pointers are related but **not identical**
* Pointer arithmetic depends on **data type size**
* Parentheses change meaning completely

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

# Dynamic Memory Allocation

Dynamic Memory Allocation (DMA) allows a program to **request memory at runtime** instead of compile time.  
This memory is allocated from the **Heap**, unlike local variables which are stored on the stack.

DMA is useful when:
- The size of data is **not known at compile time**
- Large memory blocks are required
- Memory needs to be **resized dynamically**

---

## 📚 Header File Required

```c
#include <stdlib.h>
````

This header provides:

* `malloc()`
* `calloc()`
* `realloc()`
* `free()`

---

## 🔹 1. `malloc()` – Memory Allocation

### 📌 Description

* Allocates a **single block of memory**
* Memory is **uninitialized** (contains garbage values)
* Faster than `calloc`
* Returns `NULL` if memory allocation fails

### 📄 Example (malloc)

```c
int *arr = malloc(n * sizeof(int));
```

### ✔ Safe Usage Pattern

```c
int *arr = malloc(n * sizeof(int));

if (arr == NULL) {
    printf("Memory allocation failed!\n");
    return 1;
}
```

### 🧠 Key Points

* Memory is allocated from heap
* Programmer must initialize values manually
* Must be freed using `free()`

---

## 🔹 2. `calloc()` – Contiguous Allocation

### 📌 Description

* Allocates memory for **multiple elements**
* Memory is **initialized to zero**
* Slightly slower than `malloc`
* Takes **two arguments**

### 📄 Example (calloc)

```c
int *arr = calloc(n, sizeof(int));
```

### 🧠 Key Points

* Safer when default zero values are required
* Useful for arrays
* Must be freed using `free()`

---

## 🔹 `malloc()` vs `calloc()`

| Feature        | `malloc()` | `calloc()` |
| -------------- | ---------- | ---------- |
| Initialization | ❌ No       | ✅ Yes (0)  |
| Speed          | Faster     | Slower     |
| Arguments      | 1          | 2          |
| Memory Content | Garbage    | Zero       |

📌 **Exam Tip**
Use `calloc()` when memory must be initialized.

---

## 🔹 3. `realloc()` – Reallocate Memory

### 📌 Description

* Used to **resize previously allocated memory**
* Can increase or decrease memory size
* Preserves existing data (up to min(oldSize, newSize))

### 📄 Example (realloc)

```c
int *temp = realloc(arr, newSize * sizeof(int));
```

### ⚠️ Important Rule (EXAM FAVORITE)

❌ Wrong (causes memory leak):

```c
arr = realloc(arr, newSize * sizeof(int));
```

✅ Correct:

```c
int *temp = realloc(arr, newSize * sizeof(int));
if (temp != NULL)
    arr = temp;
```

### 🧠 How `realloc()` Works Internally

* If adjacent memory is available → extends same block
* Otherwise:

  1. Allocates new block
  2. Copies old data
  3. Frees old block
  4. Returns new address

---

## 🔹 Printing All Elements After `realloc()`

After reallocation:

* Update the **size variable**
* Read input for newly allocated memory
* Loop till **new size**, not old size

```c
if (newSize > oldSize) {
    for (int i = oldSize; i < newSize; i++)
        scanf("%d", &arr[i]);
}
```

---

## 🔹 4. `free()` – Deallocate Memory

### 📌 Description

* Releases dynamically allocated memory
* Prevents **memory leak**
* Pointer becomes **dangling** after free

### 📄 Example

```c
free(arr);
arr = NULL;
```

---

## ⚠️ Memory Leak

### 📌 What is a Memory Leak?

Memory allocated on heap but **never released**.

### ❌ Example

```c
int *p = malloc(100);
// no free()
```

### ✔ Correct

```c
free(p);
```

### 🚨 Why Memory Leak is Dangerous?

* Heap memory gets exhausted
* Program slows down or crashes
* Wastes system resources

---

## ❌ Common Mistakes (Exam Traps)

| Mistake                         | Result             |
| ------------------------------- | ------------------ |
| Not checking `NULL`             | Crash              |
| Ignoring `realloc` return       | Memory leak        |
| Using old size after realloc    | Garbage values     |
| Forgetting `free()`             | Memory leak        |
| Accessing memory after `free()` | Undefined behavior |

---

## 🧠 Stack vs Heap (Quick Comparison)

| Stack                | Heap              |
| -------------------- | ----------------- |
| Automatic allocation | Manual allocation |
| Fixed size           | Dynamic size      |
| Faster               | Slower            |
| Limited memory       | Large memory      |

---

## 📝 One-Line Exam Definitions

* **Dynamic Memory Allocation**: Allocation of memory at runtime using heap.
* **Memory Leak**: Memory allocated but not released.
* **Dangling Pointer**: Pointer pointing to freed memory.
* **Heap**: Memory area used for dynamic allocation.

---

## ✅ Summary

* `malloc()` → Fast, uninitialized memory
* `calloc()` → Zero-initialized memory
* `realloc()` → Resize memory safely
* `free()` → Prevent memory leaks
* Always check for `NULL`
* Always free allocated memory

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
