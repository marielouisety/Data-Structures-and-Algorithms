## *Structures*

Reference the following structures, answer the following prompts with two variations: firstly access the data without a pointer and secondly access with a pointer.

```c
typedef struct {
    char LName[16];
    char FName[24];
    char Mi;
} Nametype;

typedef struct {
    Nametype name;
    unsigned int ID;
    char Course[8];
    int YrLvl;
} Studtype, *studPtr;

typedef struct {
    Studtype StudArray[size];
    int count;
} StudList, *listPtr;
```

<span style="color:#77c5fd">A. Given the following: </span>
```c
Studtype stud; 
studPtr ptr = &stud;
``` 

1. Input from Keyboard the ID Number 
   ```c
scanf("%u", &stud.ID);
scanf("%u", &ptr->ID);
```

2. Display on screen the last name
   ```c
printf("%s", stud.name.LName);
printf("%s", ptr->name.LName);
```

3. Change the course to BSCS
   ```c
strcpy(stud.Course, "BSCS");
strcpy(ptr->Course, "BSCS");
```

4. Display the first letter of the first name
      ```c
printf("%c", stud.name.FName[0]);
printf("%c", ptr->name.FName[0]);
```

<span style="color:#77c5fd">B. Given the following: </span>
```c
Studtype studList[50]; 
studPtr pointedTo = studList;
```

1. Input from keyboard the ID number of the 5th student in the array
   ```c
scanf("%u", &studList[4].ID);
scanf("%u", &pointedTo[4]->ID);   
```

2. Display on screen the first name of the 20th student in the array 
   ```c
printf("%s", studList[19].name.FName);
printf("%s", pointedTo[19]->name.FName);
```

3. Change the course of the 1st student in the array to BSCS 
   ```c
strcpy(studList[0].Course, "BSCS");
strcpy(pointedTo[0]->Course, "BSCS");
```
   
4. Print on screen the first letter of the first name of the first student in the array
   ```c
printf("%c", studList[0].name.FName[0]);
printf("%c", pointedTo[0]->name.FName[0]);
```

<span style="color:#77c5fd">C. Given the following:</span>
```c
#define size 50
studList List;
listPtr pointList = &List;
```

1. Input from keyboard the ID number of the 5th student in the array 
   ```c
scanf("%u", &List.StudArray[4].ID);
scanf("%u", &pointList->StudArray[4].ID);
```

2. Display on the screen the first name of the 20th student in the array 
   ```c
printf("%s", List.StudArray[19].name.FName);
printf("%s", pointList->StudArray[19].name.FName);
```
   
3. Change the course of the 1st student in the array to BSCS 
   ```c
strcpy(List.StudArray[0].Course, "BSCS");
pointList->StudArray[0].Course, "BSCS");
```
   
4. Print on screen the first letter of the last name of the last student in the array
   ```c
printf("%s", List.StudArray[List.count-1].name.LName[0]);
printf("%s", pointList->StudArray[List.count-1].name.LName[0]);
```

## *Arrays*

1. Given an array of integers of size n, the function will return 1 if all the integers in the array are unique. If not, the function will return 0. 
   
   a. Code of the Function 
   ```c
int checkUnique(int arr[], int n){
	int i, j, retval = 1;
    for (i = 0; i < n; i++){
        for (j = i+1; j < n; j++){
            if (arr[i] == arr[j]){
                retval = 0;
            } 
        }
    }
    return retval;
}
```
   
   b. Function Call 
   ```c
checkUnique(arr, n);
```

   c. Main Code
   ```c
#include <stdio.h>

int main() {
    
    int arr[] = {1, 2, 3, 5, 5};
    int n = sizeof(arr);
    
    int result = checkUnique(arr, n);
    
    printf("%d", result);
}
```

2. Bonus: Given an array of studtype of size p and a string variable of r, the function will delete all occurrences of a specified course.
   
   Note: I changed p to SIZE
   a. Function Definition
   ```c
void deleteCourse(Studtype StudArray[], int *count, char r[]) {
    int i = 0;
    while (i < *count) {
        if (strcmp(StudArray[i].Course, r) == 0) {
            // shift left
            for (int j = i; j < *count - 1; j++) {
                StudArray[j] = StudArray[j+1];
            }
            (*count)--;  // shrink size
        } else {
            i++;
        }
    }
}

void displayStudents(Studtype StudArray[], int count) {
    for (int i = 0; i < count; ++i) {
        printf("%s, %s %c | %u | %s - %d\n",
               StudArray[i].name.LName,
               StudArray[i].name.FName,
               StudArray[i].name.Mi,
               StudArray[i].ID,
               StudArray[i].Course,
               StudArray[i].YrLvl);
    }
}
```
   
   b. Function Call
   ```c
deleteCourse(list.StudArray, &list.count, r);
displayStudents(list.StudArray, list.count);
```
   
   c. Main Function
   ```c
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#define SIZE 10

typedef struct {
    char LName[16];
    char FName[24];
    char Mi;
} Nametype;

typedef struct {
    Nametype name;
    unsigned int ID;
    char Course[5];
    int YrLvl;
} Studtype, *studPtr;

typedef struct {
    Studtype StudArray[SIZE];
    int count;  // how many students are actually stored
} StudList, *listPtr;

void deleteCourse(Studtype StudArray[], int *count, char r[]);
void displayStudents(Studtype StudArray[], int count);

int main() {
    
    // Initialize list with 5 students
    StudList list = {
        {
            { {"Ty", "Marie", 'M'}, 23101494, "BSIT", 3 },
            { {"Colaljo", "Chelsea", 'J'}, 23101495, "BSIT", 3 },
            { {"Derama", "Jeskha", 'B'}, 23101496, "BSCS", 3 },
            { {"Delgado", "Jio", 'B'}, 23101497, "BSCS", 3 },
            { {"Ouano", "Cheska", 'D'}, 23101498, "BSIT", 3 },
        },
        5 // count
    };

    printf("Original Array: \n");
    displayStudents(list.StudArray, list.count);

    char r[5] = "BSCS";

    printf("\nModified Array (after deleting %s): \n", r);
    deleteCourse(list.StudArray, &list.count, r);
    displayStudents(list.StudArray, list.count);

    return 0;
}
```

Explanation for the Solution:
1. Design data structures
2. Initialize the StudList
   ```c
StudList list = {
    { { {"Ty","Marie",'M'}, ... }, ... },
    5
};
```
3. Create a function that displays the students in the array
   ```c
void displayStudents(Studtype StudArray[], int count) {
    for (int i = 0; i < count; ++i) {
        printf("%s, %s %c | %u | %s - %d\n",
               StudArray[i].name.LName,
               StudArray[i].name.FName,
               StudArray[i].name.Mi,
               StudArray[i].ID,
               StudArray[i].Course,
               StudArray[i].YrLvl);
    }
}
```
4. Implement deleteCourse using delete-by-shifting
   - use a ```while (i < *count)*``` loop, not a for, so you can stay at the same index after a deletion.
   - compare strings with ```strcmp(...) == 0```
   - shift elements left with assignment `StudArray[j] = StudArray[j+1];`
   - decrement `(*count)--;` when you remove an element.
   - example loop structure
     ```c
int i = 0;
while (i < *count) {
    if (strcmp(StudArray[i].Course, r) == 0) {
        for (int j = i; j < *count - 1; j++)
            StudArray[j] = StudArray[j+1];
        (*count)--;
    } else {
        i++;
    }
}
```
5. Use `list.StudArray` and `list.count` in `main`
   ```c
displayStudents(list.StudArray, list.count);
deleteCourse(list.StudArray, &list.count, r);
```

## *Linked Lists*

1. Given a sorted linked list of characters, the function will insert a character in its proper position.
   
   a. Function Definition
   
   
   b. Function Call
   
   
   c. Main Function


Explanation for the Solution:
1. Function Header
   ```c
void insertSorted(Node **head, char item);
```
	- We pass `Node **head` (pointer to the head pointer) so the function can update the head when insertion is at the front.
	- `item` is the character to insert.
	- 