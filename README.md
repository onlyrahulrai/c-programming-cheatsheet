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
| 9 | [Dynamic Memory Allocation](#dynamic-memory-allocation) |
| 10 | [Structure](#structure) |
| 11 | [Union](#union) |
| 12 | [File Handling](#file-handling) |
| 13 | [Preprocessor Directives](#preprocessor-directives) |
| 14 | [Common Mistakes & Exam Traps](#common-mistakes--exam-traps) |

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

# Strings

A **string** is a sequence of characters terminated by a **null character (`'\0'`)**.  
Strings can be handled using:
- Character arrays
- Pointers to string literals
- Standard string library functions (`<string.h>`)

---

## 📚 Header File Required

```c
#include <string.h>
````

Provides commonly used string functions like:

* `strlen()`
* `strcpy()`
* `strcmp()`
* `strcat()`

---

## 🔹 1. Character Array vs Pointer to String Literal

### 📄 Example

```c
char str1[] = "Pankaj";   // Writable
char str2[] = "Neeraj";   // Writable
char *str3 = "Sharma";   // Read-only
```

### 🧠 Key Differences

| Feature              | `char arr[]`     | `char *p = "text"`    |
| -------------------- | ---------------- | --------------------- |
| Memory               | Stack / writable | Read-only section     |
| Content modification | ✅ Allowed        | ❌ Not allowed         |
| Reassignment         | ❌ Not allowed    | ✅ Allowed             |
| Pointer arithmetic   | Limited          | ✅ Allowed (read-only) |

❌ Invalid:

```c
str1 = "Change";   // array name cannot be reassigned
```

✔ Valid:

```c
str3 = "Hello World";
```

---

## 🔹 Pointer Arithmetic on Strings

Pointer arithmetic on strings is **allowed for reading only**.

```c
str3 += 3;
printf("%s\n", str3);   // prints from 3rd index
```

Example:

```
"Hello World"
   ^
Output: lo World
```

---

## 🔹 String Literal Expressions

```c
printf("%s\n", "Hello World" + 5);   // prints " World"
printf("%c\n", *("Hello" + 1));      // prints 'e'
```

✔ Allowed because:

* String literal decays to `char *`
* Only read operation is performed

---

## 🔹 String Pooling (Compiler Optimization)

```c
char *p = "Hello";
char *q = "Hello";
```

* Compiler **may** store only one copy of `"Hello"`
* `p` and `q` **may point to the same address**
* This behavior is **implementation-dependent**

❌ Wrong comparison:

```c
&p == &q   // compares pointer variables
```

✔ Correct comparison:

```c
p == q     // compares string literal addresses
```

---

## 🔹 2. Array of Strings vs Array of Pointers

### 📄 Example

```c
char str1[][256] = {
    "Hi",
    "How'r you?",
    "How's going?",
    "I hope you are doing going good"
};

char *str2[] = {
    "Hi",
    "How'r you?",
    "How's going?",
    "I hope you are doing going good"
};
```

### 🧠 Memory Difference

| Aspect             | `char str1[][256]` | `char *str2[]`    |
| ------------------ | ------------------ | ----------------- |
| Memory             | Continuous block   | Array of pointers |
| Modifiable strings | ✅ Yes              | ❌ No              |
| Memory usage       | More               | Less              |
| Flexibility        | Less               | More              |

---

### 🔹 Correct Access Patterns

| Expression    | Meaning                   |
| ------------- | ------------------------- |
| `str1[i]`     | i-th string               |
| `str1[i][j]`  | j-th character            |
| `str2[i]`     | pointer to string literal |
| `str2[i] + k` | string from index k       |

Example:

```c
printf("%s\n", *(str2 + 1) + 4);   // prints "r you?"
```

---

## 🔹 3. Standard String Functions (`<string.h>`)

---

### 🔸 `strlen()`

```c
strlen(str);
```

* Returns number of characters
* Does NOT count `'\0'`

Example:

```
"HelloWorld" → 10
```

---

### 🔸 `strcpy()`

```c
strcpy(dest, src);
```

* Copies string including `'\0'`
* Destination must be large enough

❌ Dangerous if buffer is small

---

### 🔸 `strcmp()`

```c
strcmp(str1, str2);
```

Returns:

* `0` → strings are equal
* `<0` → str1 < str2
* `>0` → str1 > str2

---

### 🔸 `strcat()`

```c
strcat(dest, src);
```

* Appends `src` to `dest`
* Destination must have enough free space

❌ **Most common buffer overflow error**

---

## ⚠️ Common String Mistakes (Exam Traps)

| Mistake                              | Result             |
| ------------------------------------ | ------------------ |
| Modifying string literal             | Undefined behavior |
| Using `%s` with wrong type           | Runtime error      |
| Buffer too small for `strcpy/strcat` | Memory corruption  |
| Forgetting `'\0'`                    | Incorrect output   |
| Comparing strings using `==`         | Logical error      |

---

## 🧠 Best Practices

* Use `char arr[]` if modification is required
* Use `char *` for constant strings
* Always ensure enough buffer size
* Prefer safe variants when possible:

  * `strncpy()`
  * `strncat()`

---

## 📝 One-Line Exam Definitions

* **String**: A character array terminated by `'\0'`
* **String Literal**: A constant string stored in read-only memory
* **String Pooling**: Compiler optimization that reuses identical string literals

---

## ✅ Summary

* Strings can be handled via arrays or pointers
* Arrays → writable, fixed size
* Pointers → flexible, read-only content
* `<string.h>` provides essential string functions
* Buffer size management is critical

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

# Structure

---

## 🔹 1. What is a Structure?

A **structure** in C is a **user-defined data type** that allows grouping **variables of different data types** under a single name.

It is used to represent a **real-world entity** that consists of multiple related attributes.

### Example (Real World)

A **Student** has:

* Name
* Age
* Date of Birth

All these belong to **one entity**, so we group them using a structure.

---

## 🔹 2. Why Do We Need Structures?

Without structures:

```c
char name[50];
int age;
int day, month, year;
```

Problems:

* Data is scattered
* Hard to manage multiple records
* Poor readability

With structures:

```c
struct Student {
    char name[50];
    int age;
};
```

### ✅ Advantages

✔ Logical grouping of data
✔ Easy handling of large records
✔ Essential for databases, OS, compilers, APIs
✔ Improves readability and maintainability

---

## 🔹 3. Structure Declaration Syntax

```c
struct structure_name {
    data_type member1;
    data_type member2;
    ...
};
```

### Example:

```c
struct Student {
    char name[50];
    int age;
};
```

⚠ **Semicolon (`;`) after structure definition is mandatory**

---

## 🔹 4. Declaring Structure Variables

### Method 1: After Declaration

```c
struct Student s1, s2;
```

### Method 2: During Declaration

```c
struct Student {
    char name[50];
    int age;
} s1, s2;
```

---

## 🔹 5. Accessing Structure Members

Use the **dot (`.`) operator**.

```c
s1.age = 20;
printf("%d", s1.age);
```

---

## 🔹 6. Structure Initialization

### 6.1 Positional Initialization

```c
struct Student s1 = {"Rahul", 21};
```

⚠ Order must match structure definition

---

### 6.2 Member-wise Assignment

```c
strcpy(s1.name, "Rahul");
s1.age = 21;
```

---

## 🔹 7. Nested Structures (Structure within Structure)

### Example: `Date` inside `Student`

```c
struct Date
{
    int day;
    int month;
    int year;
};

typedef struct
{
    char name[256];
    int age;
    struct Date dob;
} Student;
```

✔ Improves modularity
✔ Represents hierarchical data

---

## 🔹 8. Designated Initialization (C99 Feature)

### Example:

```c
Student s1 = {
    .name = "John Doe",
    .age = 21,
    .dob = {
        .day = 1,
        .month = 1,
        .year = 2025
    }
};
```

### ✅ Advantages

✔ Order independent
✔ Highly readable
✔ Prevents logical mistakes

---

## 🔹 9. Accessing Nested Members

```c
printf("%s\n", s1.name);
printf("%02d-%02d-%d\n",
       s1.dob.day,
       s1.dob.month,
       s1.dob.year);
```

---

## 🔹 10. Array of Structures

Used to store **multiple records**.

```c
Student students[2] = {
    {.name="Alice", .age=20, .dob={10,5,2004}},
    {.name="Bob", .age=22, .dob={15,8,2002}}
};
```

Access:

```c
students[0].age;
students[1].dob.year;
```

---

## 🔹 11. Structure and Functions

### 11.1 Passing Structure (Call by Value)

```c
void display(Student s)
{
    printf("%s %d\n", s.name, s.age);
}
```

❌ Copies entire structure
✔ Suitable for small structures

---

### 11.2 Passing Structure (Call by Reference – Recommended)

```c
void display(Student *s)
{
    printf("%s %d\n", s->name, s->age);
}
```

✔ Efficient
✔ No data copy

---

## 🔹 12. Pointer to Structure

### Declaration

```c
Student *ptr;
```

### Access Members

```c
ptr->age = 22;
```

`->` is called the **arrow operator**
Equivalent to:

```c
(*ptr).age
```

---

## 🔹 13. Dynamic Memory Allocation with Structures

### Single Structure

```c
Student *s = malloc(sizeof(Student));
```

### Multiple Structures

```c
Student *students = malloc(n * sizeof(Student));
```

Always check:

```c
if (students == NULL) {
    printf("Memory allocation failed");
}
```

---

## 🔹 14. Updating Structure Data

```c
s1.age++;
s1.dob.year = 2026;
```

---

## 🔹 15. Typedef with Structures

### Without typedef

```c
struct Student s1;
```

### With typedef

```c
typedef struct {
    char name[50];
    int age;
} Student;

Student s1;
```

✔ Cleaner syntax
✔ Professional coding style

---

## 🔹 16. Size of Structure

```c
printf("%lu", sizeof(Student));
```

Depends on:

* Data types
* Padding & alignment

---

## 🔹 17. Structure Padding & Alignment

Example:

```c
struct Example {
    char a;
    int b;
};
```

Memory layout:

```
a -> 1 byte
padding -> 3 bytes
b -> 4 bytes
Total = 8 bytes
```

✔ Done for faster CPU access

---

## 🔹 18. Common Mistakes ❌

❌ Forgetting semicolon after structure
❌ Using `.` instead of `->` with pointer
❌ Not allocating memory for pointer members
❌ Not freeing dynamically allocated memory
❌ Incorrect initializer order

---

## 🔹 19. Best Practices ✅

✔ Use `typedef struct`
✔ Prefer designated initialization
✔ Pass structures by reference
✔ Keep nested structures logical
✔ Always free allocated memory

---

## 🔹 20. Complete Example Program

```c
#include <stdio.h>

struct Date {
    int day, month, year;
};

typedef struct {
    char name[50];
    int age;
    struct Date dob;
} Student;

int main()
{
    Student s1 = {
        .name = "John Doe",
        .age = 21,
        .dob = {1, 1, 2025}
    };

    printf("Name: %s\n", s1.name);
    printf("Age: %d\n", s1.age);
    printf("DOB: %02d-%02d-%d\n",
           s1.dob.day,
           s1.dob.month,
           s1.dob.year);

    return 0;
}
```

---

## 🔹 21. Summary

* Structures group **heterogeneous data**
* Essential for real-world modeling
* Support nesting, arrays, pointers, functions
* Widely used in **DSA, OS, DBMS, Networking**

# Union

---

## 🔹 1. What is a Union?

A **union** in C is a **user-defined data type** similar to a structure, but **all members share the same memory location**.

👉 This means **only one member can store a value at a time**.

---

## 🔹 2. Why Do We Need Unions?

Unions are used when:

* Multiple variables **do not need to exist at the same time**
* Memory usage needs to be **optimized**
* We want to store **different data types in the same memory space**

### Example Use Cases

* Compiler design
* Operating systems
* Embedded systems
* Protocol parsing
* Memory-constrained programs

---

## 🔹 3. Difference Between Structure and Union (Quick Overview)

| Feature           | Structure                | Union                     |
| ----------------- | ------------------------ | ------------------------- |
| Memory Allocation | Separate for each member | Shared                    |
| Total Size        | Sum of all members       | Size of largest member    |
| Value Storage     | All members at once      | Only one member at a time |
| Memory Efficiency | Less                     | More                      |
| Use Case          | Records                  | Variants                  |

---

## 🔹 4. Syntax of Union Declaration

```c
union union_name {
    data_type member1;
    data_type member2;
    ...
};
```

### Example:

```c
union Data {
    int i;
    float f;
    char c;
};
```

⚠ Semicolon (`;`) is **mandatory**

---

## 🔹 5. Declaring Union Variables

### Method 1: After Declaration

```c
union Data d1;
```

### Method 2: During Declaration

```c
union Data {
    int i;
    float f;
} d1;
```

---

## 🔹 6. Accessing Union Members

Same as structure → **dot (`.`) operator**

```c
d1.i = 10;
printf("%d", d1.i);
```

⚠ Writing to one member **overwrites** the previous value.

---

## 🔹 7. Union Memory Behavior (Most Important Concept)

```c
union Data {
    int i;
    float f;
    char c;
};
```

Memory layout:

* All members start at **same address**
* Size = **max(sizeof(int), sizeof(float), sizeof(char))**

```c
printf("%lu", sizeof(union Data));
```

---

## 🔹 8. Example: Demonstrating Memory Overwrite

```c
#include <stdio.h>

union Data {
    int i;
    float f;
};

int main()
{
    union Data d;

    d.i = 10;
    printf("i = %d\n", d.i);

    d.f = 3.14;
    printf("f = %.2f\n", d.f);

    printf("i after writing f = %d\n", d.i);

    return 0;
}
```

### Output Explanation

* Assigning `f` **overwrites** `i`
* Only **last written member** is valid

---

## 🔹 9. Union Initialization

### At Declaration Time

```c
union Data d = {10};
```

✔ Initializes **first member only**

---

## 🔹 10. Union with `typedef`

```c
typedef union {
    int id;
    float salary;
} Info;

Info emp;
emp.id = 101;
```

✔ Cleaner syntax
✔ Professional usage

---

## 🔹 11. Union Inside Structure (Very Common)

Used when a structure field can store **different types of values**.

```c
struct Student {
    int roll;
    union {
        int marks;
        float percentage;
    } result;
};
```

Usage:

```c
struct Student s;
s.result.marks = 85;
```

---

## 🔹 12. Structure Inside Union

```c
union Container {
    int id;
    struct {
        int day, month, year;
    } date;
};
```

---

## 🔹 13. Pointer to Union

```c
union Data *ptr;
ptr->i = 20;
```

`->` operator works same as structure.

---

## 🔹 14. Array of Unions

```c
union Data arr[3];
```

Each element has **independent memory**, but inside each element, members share memory.

---

## 🔹 15. Size of Union

```c
printf("%lu", sizeof(union Data));
```

✔ Size equals **largest member**
✔ Padding may apply for alignment

---

## 🔹 16. Union vs Structure (Detailed Comparison)

| Aspect           | Structure | Union            |
| ---------------- | --------- | ---------------- |
| Memory           | Separate  | Shared           |
| Multiple values  | Allowed   | Not allowed      |
| Safety           | Safer     | Risky if misused |
| Memory efficient | ❌         | ✔                |
| Typical use      | Records   | Variant data     |

---

## 🔹 17. When to Use Union?

✔ When only **one value is needed at a time**
✔ When **memory optimization is critical**
✔ When implementing **tagged data types**

---

## 🔹 18. Tagged Union (Best Practice)

To track which member is valid:

```c
enum Type { INT, FLOAT };

struct Value {
    enum Type type;
    union {
        int i;
        float f;
    } data;
};
```

Usage:

```c
struct Value v;
v.type = INT;
v.data.i = 10;
```

✔ Safe
✔ Industry-grade design

---

## 🔹 19. Common Mistakes ❌

❌ Assuming all members hold values simultaneously
❌ Reading a member that was not last written
❌ Forgetting which member is active
❌ Using union where structure is needed

---

## 🔹 20. Best Practices ✅

✔ Use union only when necessary
✔ Track active member using `enum`
✔ Comment clearly which member is active
✔ Prefer structure if memory is not a concern

---

## 🔹 21. Complete Example Program

```c
#include <stdio.h>

union Data {
    int i;
    float f;
};

int main()
{
    union Data d;

    d.i = 100;
    printf("Integer: %d\n", d.i);

    d.f = 5.5;
    printf("Float: %.2f\n", d.f);

    return 0;
}
```

---

## 🔹 22. Summary

* Union shares **one memory location**
* Only **one member is valid at a time**
* Saves memory
* Used in **low-level and system programming**

## 🔹 Structure vs Union

| Feature | Structure                | Union               |
| ------- | ------------------------ | ------------------- |
| Memory  | Separate for each member | Shared              |
| Size    | Sum of members           | Largest member      |
| Usage   | Multiple values          | One value at a time |

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
