1. Create a C program that inserts, deletes, and searches the RGB value in an open hashing dictionary.
	a. The hash function accepts an RGB value and returns a digit constrained in a 64-palette size.
	b. Given this structure, formulate this into an open hashing dictionary:
```c
typedef struct {
	String colorName;
	int RGBval[3];
} Color;
```