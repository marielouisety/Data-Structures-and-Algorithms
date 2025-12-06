1. Create a C program that inserts, deletes, and searches the RGB value in an open hashing dictionary.
	a. The hash function accepts an RGB value and returns a digit constrained in a 64-palette size.
	b. Given this structure, formulate this into an open hashing dictionary:
```c
typedef struct {
	String colorName;
	int RGBval[3];
} Color;
```

```c
// RGB_hash.c

#include <stdio.h>
#include <stdlib.h>
#include <string.h>

#define TABLE_SIZE 64

typedef struct {
	char colorName[50];
	int RGBval[3]; // R, G, B
} Color;

typedef struct Node {
	Color data;
	struct Node* next;
} Node;

// Hash Table (array of pointers to linked lists)
Node* hashTable[TABLE_SIZE];


```
