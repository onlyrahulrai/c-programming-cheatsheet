# Linked List

---

## 🔹 What is a Linked List?

**Linked List** एक **dynamic data structure** है जिसमें data elements (nodes) **linear order** में होते हैं,
लेकिन **contiguous memory** (array की तरह) में store नहीं होते।

हर element को **Node** कहते हैं, और हर node में दो भाग होते हैं:

```
[data | link]
```

* `data` → actual information
* `link` → अगले (या पिछले) node का address

👉 Nodes एक-दूसरे से **pointers** के माध्यम से जुड़े होते हैं।

---

## 🔹 Why Linked List?

Arrays की कुछ limitations होती हैं:

* Fixed size
* Insertion / deletion costly
* Memory wastage or overflow

👉 Linked List इन समस्याओं को solve करता है।

---

## 🔹 Advantages of Linked List

✔ Dynamic size (runtime में बढ़/घट सकती है)
✔ Insertion & deletion आसान (no shifting)
✔ Better memory utilization
✔ No need for contiguous memory

---

## 🔹 Disadvantages of Linked List

❌ Direct access possible नहीं (no indexing)
❌ Extra memory required (pointer storage)
❌ Traversal slower than array
❌ Cache friendly नहीं

---

## 🔹 Basic Terminology

* **Node** → Linked list का single element
* **Head** → First node का address
* **Tail** → Last node
* **NULL** → List का end

---

# 🔹 Types of Linked List

Linked List को structure और linking के आधार पर कई प्रकारों में बाँटा जाता है।

---

## 1️⃣ Singly Linked List

### 🔸 Description

* हर node में **data + next pointer** होता है
* Traversal केवल **one direction (forward)** में possible

```
Head → [10 | ] → [20 | ] → [30 | NULL]
```

### 🔸 Node Structure

```c
struct Node {
    int data;
    struct Node *next;
};
```

### 🔸 Features

✔ Simple & memory efficient
✔ Easy insertion & deletion
❌ Backward traversal possible नहीं

### 🔸 Use Cases

* Stack
* Queue
* Polynomial representation

[Complete Singly Linked List Program](#complete-singly-linked-list-program)

---

## 2️⃣ Doubly Linked List

### 🔸 Description

* हर node में **three parts** होते हैं:

  * previous pointer
  * data
  * next pointer
* Traversal **forward & backward** दोनों direction में possible

```
NULL ← [10] ⇄ [20] ⇄ [30] → NULL
```

### 🔸 Node Structure

```c
struct Node {
    int data;
    struct Node *prev;
    struct Node *next;
};
```

### 🔸 Features

✔ Two-way traversal
✔ Deletion आसान
❌ Extra memory overhead

### 🔸 Use Cases

* Browser navigation (Back/Forward)
* Undo/Redo operations
* Music playlist

---

## 3️⃣ Circular Singly Linked List

### 🔸 Description

* Last node का `next` → first node (head) को point करता है
* `NULL` pointer नहीं होता

```
Head → [10] → [20] → [30]
   ↑___________________|
```

### 🔸 Node Structure

```c
struct Node {
    int data;
    struct Node *next;
};
```

### 🔸 Features

✔ Efficient traversal
✔ No NULL reference
✔ Suitable for looping structures

### 🔸 Use Cases

* CPU scheduling (Round Robin)
* Multiplayer games
* Circular buffers

---

## 4️⃣ Circular Doubly Linked List

### 🔸 Description

* Doubly linked list + circular structure
* Last node का `next` → head
* Head का `prev` → last node

```
[10] ⇄ [20] ⇄ [30]
 ↑________________↓
```

### 🔸 Node Structure

```c
struct Node {
    int data;
    struct Node *prev;
    struct Node *next;
};
```

### 🔸 Features

✔ Bi-directional circular traversal
✔ No NULL pointers
❌ Most complex structure

### 🔸 Use Cases

* Advanced scheduling systems
* OS memory management

---

## 🔹 Comparison Table

| Feature           | Singly  | Doubly  | Circular Singly | Circular Doubly    |
| ----------------- | ------- | ------- | --------------- | ------------------ |
| Pointers per node | 1       | 2       | 1               | 2                  |
| Traversal         | One-way | Two-way | Circular        | Circular + two-way |
| Memory usage      | Low     | High    | Low             | Highest            |
| Complexity        | Simple  | Medium  | Medium          | High               |

---

## 🔹 When to Use Linked List?

✔ Frequent insertions/deletions
✔ Dynamic data size
✔ No need for random access

❌ When fast indexing is required → use Array

---

## 🎯 Interview One-Liner

> **“A linked list is a dynamic data structure where elements are stored in nodes connected via pointers rather than contiguous memory.”**

---

## 🧠 Memory Hook (Remember Forever)

> **Array = Index Based**
> **Linked List = Address Based**

---

## Complete Singly Linked List Program

Below is a complete, working, and exam-safe implementation of a Singly Linked List in C.

---

## 📌 Program Objective

इस program का उद्देश्य **Singly Linked List** पर निम्न operations perform करना है:

* Insert at Beginning
* Insert at End
* Insert at Specific Position
* Delete from Beginning
* Delete from End
* Display Linked List

यह program **menu-driven** है और dynamic memory allocation का उपयोग करता है।

---

## 🔹 Complete Program

```c
#include <stdio.h>
#include <stdlib.h>

typedef struct Node {
    int data;
    struct Node *next;
} Node;

/* Create a new node */
Node *createNode(int data) {
    Node *newNode = malloc(sizeof(Node));

    if (newNode == NULL) {
        printf("Memory allocation failed\n");
        exit(1);
    }

    newNode->data = data;
    newNode->next = NULL;
    return newNode;
}

/* Insert at beginning */
void insertAtBeg(Node **head, int data) {
    Node *newNode = createNode(data);
    newNode->next = *head;
    *head = newNode;
}

/* Insert at end */
void insertAtEnd(Node **head, int data) {
    Node *newNode = createNode(data);

    if (*head == NULL) {
        *head = newNode;
        return;
    }

    Node *temp = *head;
    while (temp->next != NULL) {
        temp = temp->next;
    }
    temp->next = newNode;
}

/* Insert at specific position (0-based) */
void insertAtPosition(Node **head, int data, int pos) {
    if (pos < 0) {
        printf("Invalid position\n");
        return;
    }

    if (pos == 0) {
        insertAtBeg(head, data);
        return;
    }

    Node *temp = *head;
    int i = 0;

    while (temp != NULL && i < pos - 1) {
        temp = temp->next;
        i++;
    }

    if (temp == NULL) {
        printf("Position out of range\n");
        return;
    }

    Node *newNode = createNode(data);
    newNode->next = temp->next;
    temp->next = newNode;
}

/* Delete from beginning */
void deleteAtBeg(Node **head) {
    if (*head == NULL) {
        printf("List is empty\n");
        return;
    }

    Node *temp = *head;
    *head = (*head)->next;
    free(temp);
}

/* Delete from end */
void deleteAtEnd(Node **head) {
    if (*head == NULL) {
        printf("List is empty\n");
        return;
    }

    if ((*head)->next == NULL) {
        free(*head);
        *head = NULL;
        return;
    }

    Node *temp = *head;
    while (temp->next->next != NULL) {
        temp = temp->next;
    }

    free(temp->next);
    temp->next = NULL;
}

/* Display list */
void display(Node *head) {
    while (head != NULL) {
        printf("%d -> ", head->data);
        head = head->next;
    }
    printf("NULL\n");
}

/* Main function */
int main() {
    Node *head = NULL;
    int choice, val, pos;

    while (1) {
        printf("\n1.Insert Beg\n2.Insert End\n3.Insert Pos\n4.Delete Beg\n5.Delete End\n6.Display\n7.Exit\n");
        scanf("%d", &choice);

        switch (choice) {
        case 1:
            scanf("%d", &val);
            insertAtBeg(&head, val);
            break;
        case 2:
            scanf("%d", &val);
            insertAtEnd(&head, val);
            break;
        case 3:
            scanf("%d %d", &val, &pos);
            insertAtPosition(&head, val, pos);
            break;
        case 4:
            deleteAtBeg(&head);
            break;
        case 5:
            deleteAtEnd(&head);
            break;
        case 6:
            display(head);
            break;
        case 7:
            exit(0);
        }
    }
}
```

---

## 🔹 Program Explanation (Step-by-Step)

### 🔸 1. `createNode()`

**Purpose:**
Heap memory में नया node बनाना और initialize करना।

**Explanation:**

* `malloc()` से memory allocate होती है
* NULL check memory failure से बचाता है
* `next = NULL` list का end दर्शाता है

---

### 🔸 2. `insertAtBeg()`

**Purpose:**
Linked list के शुरुआत में node insert करना।

**Why `Node **head`?**
👉 क्योंकि नया node **head बन जाता है**।

**Logic:**

```
newNode->next = old head
head = newNode
```

---

### 🔸 3. `insertAtEnd()`

**Purpose:**
List के last node के बाद नया node जोड़ना।

**Explanation:**

* Empty list → new node ही head बनता है
* Otherwise → last node तक traverse
* Last node का `next` नए node से link

---

### 🔸 4. `insertAtPosition()`

**Purpose:**
किसी specific position पर node insert करना (0-based index)।

**Steps:**

1. Position validate करें
2. `(pos - 1)` node तक traverse
3. Proper linking करें

---

### 🔸 5. `deleteAtBeg()`

**Purpose:**
First node को delete करना।

**Explanation:**

* Old head को temporary pointer में रखें
* Head को next node पर shift करें
* Old node को `free()` करें

---

### 🔸 6. `deleteAtEnd()`

**Purpose:**
Last node को delete करना।

**Special Case:**

* अगर सिर्फ 1 node है → head = NULL

**Logic:**

* Second-last node तक traverse
* Last node को free करें

---

### 🔸 7. `display()`

**Purpose:**
पूरी linked list को print करना।

**Explanation:**

* Head से traversal शुरू
* `NULL` मिलने पर stop

---

## 🔹 Sample Execution

```
Insert Beg: 10
Insert End: 20
Insert Pos (1): 15

Output:
10 -> 15 -> 20 -> NULL
```

---

## 🧠 MEMORY RULE (Golden Concept)

| Situation        | Use           |
| ---------------- | ------------- |
| Head change      | `Node **head` |
| Traversal / Read | `Node *head`  |

> 🧠 **Head भी एक variable है —
> उसे change करना है तो उसका address भेजो**

---

## ⏱ Time Complexity

| Operation           | Time |
| ------------------- | ---- |
| Insert at Beginning | O(1) |
| Insert at End       | O(n) |
| Delete at Beginning | O(1) |
| Delete at End       | O(n) |
| Traversal           | O(n) |

---

## ❌ Common Mistakes (Very Important)

❌ Using `Node *head` when head changes
❌ Forgetting `free()` after delete
❌ Dereferencing NULL pointer
❌ Ignoring `malloc()` failure
