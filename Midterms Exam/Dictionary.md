 - <span style="color:#77c5fd">fastest data structure</span>
- a set with operations such as:
	- <span style="color:#77c5fd">insert</span>
	- <span style="color:#77c5fd">delete</span>
	- <span style="color:#77c5fd">member</span>
- Implementations:
	- <span style="color:#77c5fd">Linked List</span>
	- <span style="color:#77c5fd">Array</span>
	- <span style="color:#77c5fd">Cursor-based</span>
	- <span style="color:#77c5fd">Hashing</span>

## *Purpose*

```c
colors { "red", "green", "blue" }
```

<img width="458" height="309" alt="image" src="https://github.com/user-attachments/assets/2f5e537b-b9ee-4c11-9b68-b0135b285630" />

## *Problem*

1. C is a structural language, not an object-oriented one.
2. Index access is only integer values in C.

## *Solution: Hashing*

- a function that generates a unique key by determining the:
	- <mark style="background: #5478C2A6;"><font color="white">location of the element</font></mark>
	- <mark style="background: #5478C2A6;"><font color="white">starting point in searching for the location of the element</font></mark>
	- <mark style="background: #5478C2A6;"><font color="white">generates the index</font></mark>
	- <mark style="background: #5478C2A6;"><font color="white">does not know if the index being returned has value</font></mark>

## *Hash( )*

<img width="638" height="360" alt="image" src="https://github.com/user-attachments/assets/9a7a6199-9512-41c4-92b0-029d234ddeff" />

## *Hash Context*

- the context of the hash( ) is dependent on the coding context
- Example: Hash( ) will return the digit of an integer in its ones place

```c
int Hash(int num) {
	return num % 10;
}
```

1. Hash returns a digit in its hundredths place
2. Hash accepts a last name and then it returns 0 if last name with A, 1 if B, ... , 25 if Z.
3. Hash accepts an RGB value and returns a digit constrained in a 64 palette size.

## *Two Types*

1. <mark style="background: #5478C2A6;"><font color="white">Open Hashing (External Hashing)</font></mark>
	- stores the set in potentially unlimited space
	- Dynamic Array, Linked List
2. <mark style="background: #5478C2A6;"><font color="white">Closed Hashing (Internal Hashing)</font></mark>
	- store the set in a fixed space
	- Static Array, Cursor-Based

## *Open Hashing*

Set A = {20, 47, 22, 5, 65, 72, 6, 91}

<img width="280" height="490" alt="image" src="https://github.com/user-attachments/assets/9dd12a3b-a02f-4dff-bf2f-11bf778ca693" />

<mark style="background: #5478C2A6;"><font color="white">hash( )</font></mark> - generates a value through % of 10
<mark style="background: #5478C2A6;"><font color="white">chaining</font></mark>
- solution to collisions
- uses linked list to chain values to its key
- array of linked list

Other Variations

<img width="468" height="465" alt="image" src="https://github.com/user-attachments/assets/81b74f92-6560-4b52-b3c5-f8b6f8f05ba3" />

## *Closed Hashing*

Set A = {20, 47, 22, 5, 65, 72, 6, 91

Dictionary D

<img width="77" height="461" alt="image" src="https://github.com/user-attachments/assets/fb802b5b-d56f-4849-ba4f-c7357d377f74" />

<mark style="background: #5478C2A6;"><font color="white">hash( )</font></mark> - generates a value through % of 10

Synonyms
- 2 or more elements with the same hash value

Solution
- Linear Hashing
- Progressive Overflow

## *Linear Hashing*

- the element is placed <mark style="background: #5478C2A6;"><font color="white">in the next available position if collision occurs</font></mark>
- using concept of <mark style="background: #5478C2A6;"><font color="white">circular arrays</font></mark>

<img width="595" height="270" alt="image" src="https://github.com/user-attachments/assets/1cb07353-d40b-4ddf-9f82-a1335ad77a30" />

## *Bucket*

- using a range of indexes to limit space use
- hash( ) - adjust for the range of the bucket

<img width="432" height="499" alt="image" src="https://github.com/user-attachments/assets/7c7acd87-d379-430f-a992-7b5366d1f3f2" />

## *Progressive Overflow*

- dividing the space used into half, one used as the primary storage and the other as the secondary storage

<img width="396" height="342" alt="image" src="https://github.com/user-attachments/assets/af715a3a-917e-4fe1-82e1-243eb90380cd" />

```c
#define MAX 10
#define Empty " "
#define Delete -1

typedef struct {
	int elem;
	int next;
} node;

typedef struct {
	node table[MAX];
	int Avail;
} Dictionary;
```

Set A = {20, 43, 22, 5, 65, 72, 6, 28, 91}

```c
#define MAX 5;
hash(x) == x % MAX;
```

<img width="457" height="409" alt="image" src="https://github.com/user-attachments/assets/f95256dc-6a08-4037-9ec4-811e10d77d70" />

<img width="442" height="411" alt="image" src="https://github.com/user-attachments/assets/319300b6-11e5-4bc8-a0b5-58c8b2a1330a" />

<img width="752" height="348" alt="image" src="https://github.com/user-attachments/assets/df217a8e-b64a-4fb9-95ff-56dad96ea87e" />

<mark style="background: #5478C2A6;"><font color="white">Perfect Hash</font></mark>
- when a hash function returns a unique value
- not possible to get a perfect hash

<mark style="background: #5478C2A6;"><font color="white">Packing Density</font></mark>
- ratio of num elements to be stored to number of available space
- perfect ratio = 70:30 (only for closed hashing)
