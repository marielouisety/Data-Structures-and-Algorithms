Recap of
- <span style="color:#77c5fd">Data Types</span>
- <span style="color:#77c5fd">Functions</span>
- <span style="color:#77c5fd">Pointers</span>
- <span style="color:#77c5fd">Arrays</span>
- <span style="color:#77c5fd">Dynamic Memory Allocation</span>
- <span style="color:#77c5fd">Structures</span>
- <span style="color:#77c5fd">Linked List</span>

## *Primitive Data Types*

- <mark style="background: #5478C2A6;"><font color="white">char</font></mark> - whole number (4 bytes)
- <mark style="background: #5478C2A6;"><font color="white">char</font></mark> - single character (1 byte)
- <mark style="background: #5478C2A6;"><font color="white">float</font></mark> - decimal number (4 bytes)
- <mark style="background: #5478C2A6;"><font color="white">double</font></mark> - larger decimal number (8 bytes)
- <mark style="background: #5478C2A6;"><font color="white">char</font></mark> - holds no value
- <mark style="background: #5478C2A6;"><font color="white">int*, float*, char*</font></mark> - pointer type (8 bytes)

## *Derived Data Types*

- <mark style="background: #5478C2A6;"><font color="white">Arrays</font></mark> - sequence of data items with same type of values
- <mark style="background: #5478C2A6;"><font color="white">Pointers</font></mark> - accesses the memory and deals with the addresses of which it is pointed to

## *User-Defined Data Types*

- <mark style="background: #5478C2A6;"><font color="white">structure</font></mark> - a package of different types of variables under one name, defined by keyword "struct"
- <mark style="background: #5478C2A6;"><font color="white">union</font></mark> - allows storing of varying data types in the same memory location that can be defined with different members but only a single member can contain a value at any given time
- <mark style="background: #5478C2A6;"><font color="white">enum</font></mark> - consists of integral constants

```c
#include <studio.h>

int addNum(int, int);            // Function Prototype
void displayNum(int);

int main() {
	int x = 5, y = 7, z;
	z = addNum(x,y);             // Function Call

	printNum(z);
	return 0;
}

int addNum(int a, int b) {       // Function Definition
	int sum;
	sum = a + b;            
	return sum;
}

void printNum(int g) {
	printf("The sum is %d", g);
}
```

## *Pointers*

- Value: address of another variable
- datatype: any
- Declaration: ```datatype *variableName;```

| variable | stores | returns | syntax |
|----------|--------|---------|--------|
| ptr | address | address | ptr = &x |
|   *ptr    | value | value | *ptr = x; |

## *Arrays*

- a fixed-size collection of elements of the same data type 
- stores multiple values in a single variable for easy data manipulation
  
  ```c
int array[6];
```

![[Pasted image 20250918235038.png]]

- Declaration
```c
datatype variableName[size];
```

- Initialization
  ```c
int array[6] = {2, 4, 8, 12, 16, 18};
```

- Accessing the Array
  ```c
  variableName[index];

int array[6] = {2, 4, 8, 12, 16, 18};
array[4] // accessing the 5th index	
```

- Passing Arrays to Functions
- Function Definition
  ```c
void sort(int arr[]) {
  	// code
  }

// or

void sort(int *arr) {
	// code
}
```

- Function Prototype
	- ```void sort(int[]);```
	- ```void sort(int*);```

- Function Call
  ```c
sort(arr);
```

## *Dynamic Memory Allocation*

- allocating memory during runtime program

| <span style="color:#77c5fd">malloc()</span> | allocates a single block of memory and returns pointer to the first byte of allocated space |
|----------|---|
| <span style="color:#77c5fd">calloc()</span> | allocates a specified number of blocks of memory and initializes all bytes to zero |
| <span style="color:#77c5fd">realloc()</span> | modifies the size of a previously allocated memory space |
| <span style="color:#77c5fd">free()</span> | de-allocates the memory allocated |

- Syntax
  
| <span style="color:#77c5fd">malloc()</span> | ptr = (cast-type*)malloc(byte-size); |
|----------|---|
| <span style="color:#77c5fd">calloc()</span> | ptr = (cast-type*)calloc(n, element-size); |
| <span style="color:#77c5fd">realloc()</span> | ptr = malloc(ptr, newSize); |
| <span style="color:#77c5fd">free()</span> | free(ptr); |

## *Structure*

- collection of one or more variables which can be of different data types stored contiguously in memory
- Syntax
  ```c
struct tagName {
       datatype variableName;
  } variableList;

// Example

struct Fraction {
	int numerator;
	int denominator;
} A, B;
```

- using typedef
  ```c
typedef struct tagName {
       datatype variableName;
  } NewType;

// Example

typedef struct Fraction {
	int numerator;
	int denominator;
} Frac;
```

## *Pointer to Structure*

![[Pasted image 20250919001621.png]]

## *Accessing Structures*

- Access the variable numerator in three ways:
	- ```A.numerator;```
	- ```(*ptr).numerator;```
	- ```ptr->numerator;```

## *Structures*

![[Pasted image 20250919004952.png]]

```c
typedef struct {
	char LName[16];
	char Fname[24];
	char Mi;
} Nametype;

typedef struct {
	Nametype name;
	unsigned int ID;
	char Course[8];
	int YrLvl;
} Studtype;

Studtype StudArray[size];
```

![[Pasted image 20250919005056.png]]

```c
typedef struct {
	char LName[16];
	char Fname[24];
	char Mi;
} Nametype;

typedef struct {
	Nametype name;
	unsigned int ID;
	char Course[8];
	int YrLvl;
} Studtype;

typedef struct {
	Studtype StudArray[size];
	int count;
} StudList;

StudList List;
```

![[Pasted image 20250919005839.png]]

## *Linked List*

- a linear data structure that isn't stored in a contiguous location
- linked with pointers
- <span style="color:#77c5fd">self-referencing structure</span>

```c
typedef struct node {
	char data;
	struct node *link;
} celltype, *LIST;

List L;
L = (LIST)malloc(sizeof(celltype));
L->data = 'M';
L->link = (LIST)malloc(sizeof(celltype));
L->link->data = 'B';
L->link->link = NULL;
```

![[Pasted image 20250919005657.png]]

```c
typedef struct {
	char LName[16];
	char FName[24];
	char Mi;
} Nametype;

typedef struct node {
	Nametype name;
	struct node *link;
} celltype, *LIST;
```

![[Pasted image 20250919020332.png]]

## *Linked-List Traversal*

<span style="color:#77c5fd">Pointer to Data (access only)</span>

```c
#include <stdio.h>
#include <stdlib.h>

typedef struct node {
    char data;
    struct node *link;
} cellType, *LIST;

int main() {
    
    LIST L, trav;
    
    L = (LIST)malloc(sizeof(cellType));
    L->data = 'M';
    L->link = (LIST)malloc(sizeof(cellType));
    L->link->data = 'A';
    L->link->link = (LIST)malloc(sizeof(cellType));
    L->link->link->data = 'A';
    L->link->link->link = NULL;
    
    printf("List: ");
    trav = L;
    while (trav != NULL){
        printf("%c -> ", trav->data);
        trav = trav->link;
    }
    printf("NULL\n");

    return 0;
    
}
```

![[Pasted image 20250919020755.png]]
![[Pasted image 20250919021133.png]]
![[Pasted image 20250919021154.png]]
![[Pasted image 20250919021212.png]]

<span style="color:#77c5fd">Pointer to Data Pointer (modifying pointer list)</span>

```c
#include <stdio.h>
#include <stdlib.h>

typedef struct node {
    char data;
    struct node *link;
} cellType, *LIST;

int main() {
    
    LIST L, trav;
    
    L = (LIST)malloc(sizeof(cellType));
    L->data = 'M';
    L->link = (LIST)malloc(sizeof(cellType));
    L->link->data = 'A';
    L->link->link = (LIST)malloc(sizeof(cellType));
    L->link->link->data = 'A';
    L->link->link->link = NULL;
    
    printf("Original list: ");
    trav = L;
    while (trav != NULL){
        printf("%c -> ", trav->data);
        trav = trav->link;
    }
    printf("NULL\n");
    
    printf("Modified list: ");
    trav = L->link;
    LIST newNode;
    newNode = (LIST)malloc(sizeof(cellType));
    newNode->data = 'Y';
    newNode->link = trav->link;
    trav->link = newNode;
    
    trav = L;
    while (trav != NULL) {
        printf("%c -> ", trav->data);
        trav = trav->link;
    }
    printf("NULL\n");

    return 0;
    
}
```

![[Pasted image 20250919021503.png]]
![[Pasted image 20250919021522.png]]
![[Pasted image 20250919021430.png]]
![[Pasted image 20250919021600.png]]



