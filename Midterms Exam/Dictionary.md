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

![[Pasted image 20251028192914.png]]

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

![[Pasted image 20251029170913.png]]

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

![[Pasted image 20251029172146.png]]

<mark style="background: #5478C2A6;"><font color="white">hash( )</font></mark> - generates a value through % of 10
<mark style="background: #5478C2A6;"><font color="white">chaining</font></mark>
- solution to collisions
- uses linked list to chain values to its key
- array of linked list

Other Variations

![[Pasted image 20251029172327.png]]
## *Closed Hashing*

Set A = {20, 47, 22, 5, 65, 72, 6, 91

Dictionary D
![[Pasted image 20251029172421.png]]

<mark style="background: #5478C2A6;"><font color="white">hash( )</font></mark> - generates a value through % of 10

Synonyms
- 2 or more elements with the same hash value

Solution
- Linear Hashing
- Progressive Overflow

## *Linear Hashing*

- the element is placed <mark style="background: #5478C2A6;"><font color="white">in the next available position if collision occurs</font></mark>
- using concept of <mark style="background: #5478C2A6;"><font color="white">circular arrays</font></mark>

![[Pasted image 20251029173231.png]]

## *Bucket*

- using a range of indexes to limit space use
- hash( ) - adjust for the range of the bucket

![[Pasted image 20251029173335.png]]

## *Progressive Overflow*

- dividing the space used into half, one used as the primary storage and the other as the secondary storage

![[Pasted image 20251029173437.png]]

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

![[Pasted image 20251029191429.png]]

![[Pasted image 20251029191452.png]]

![[Pasted image 20251029191622.png]]

<mark style="background: #5478C2A6;"><font color="white">Perfect Hash</font></mark>
- when a hash function returns a unique value
- not possible to get a perfect hash

<mark style="background: #5478C2A6;"><font color="white">Packing Density</font></mark>
- ratio of num elements to be stored to number of available space
- perfect ratio = 70:30 (only for closed hashing)
