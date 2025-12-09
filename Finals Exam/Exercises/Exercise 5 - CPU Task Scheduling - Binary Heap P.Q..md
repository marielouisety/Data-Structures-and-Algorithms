Sample output:

```c
=============== OS SCHEDULER PRIORITY QUEUE MENU ===============
Select a Test Scenario to Run:
1. Enqueue Test (Demonstrates Max Heap build on insertion)
2. Dequeue Test (Demonstrates Max Heap extraction/scheduling)
3. Full Combination Test (Dynamic OS Scheduling Scenario)
==================================================================
Enter your choice (1, 2, or 3): 1

--- Scheduler Queue initialized with capacity 10. ---

--- Test 1: ENQUEUE (Process Arrival) ---
Inserting processes in various priority orders:
-> ENQUEUED: Process ID 10 (Priority: 5)
-> ENQUEUED: Process ID 20 (Priority: 8)
-> ENQUEUED: Process ID 30 (Priority: 3)
-> ENQUEUED: Process ID 40 (Priority: 9)
-> ENQUEUED: Process ID 50 (Priority: 7)

--- Current Ready Queue (Heap Order: Priority, PID) ---
| P40 (Pri:9) | P20 (Pri:8) | P30 (Pri:3) | P10 (Pri:5) | P50 (Pri:7) |
------------------------------------------------------
NOTE: The highest priority process (PID 40, Pri 9) is at the top of the heap (first in the list).

Program finished execution.

Sample Output 2

=============== OS SCHEDULER PRIORITY QUEUE MENU ===============
Select a Test Scenario to Run:
1. Enqueue Test (Demonstrates Max Heap build on insertion)
2. Dequeue Test (Demonstrates Max Heap extraction/scheduling)
3. Full Combination Test (Dynamic OS Scheduling Scenario)
==================================================================
Enter your choice (1, 2, or 3): 2

--- Scheduler Queue initialized with capacity 10. ---

--- Test 2: DEQUEUE (Scheduling Dispatch) ---
Pre-loading 5 processes for scheduling...
-> ENQUEUED: Process ID 100 (Priority: 4)
-> ENQUEUED: Process ID 200 (Priority: 1)
-> ENQUEUED: Process ID 300 (Priority: 6)
-> ENQUEUED: Process ID 400 (Priority: 3)
-> ENQUEUED: Process ID 500 (Priority: 5)

Ready Queue before dispatch:

--- Current Ready Queue (Heap Order: Priority, PID) ---
| P300 (Pri:6) | P500 (Pri:5) | P100 (Pri:4) | P200 (Pri:1) | P400 (Pri:3) |
------------------------------------------------------

Dispatching processes in order of priority (Max Heap extraction):
<- DEQUEUED: SCHEDULING Process ID 300 (Priority: 6)

--- Current Ready Queue (Heap Order: Priority, PID) ---
| P500 (Pri:5) | P400 (Pri:3) | P100 (Pri:4) | P200 (Pri:1) |
------------------------------------------------------
<- DEQUEUED: SCHEDULING Process ID 500 (Priority: 5)

--- Current Ready Queue (Heap Order: Priority, PID) ---
| P100 (Pri:4) | P400 (Pri:3) | P200 (Pri:1) |
------------------------------------------------------
<- DEQUEUED: SCHEDULING Process ID 100 (Priority: 4)

--- Current Ready Queue (Heap Order: Priority, PID) ---
| P400 (Pri:3) | P200 (Pri:1) |
------------------------------------------------------
<- DEQUEUED: SCHEDULING Process ID 400 (Priority: 3)

--- Current Ready Queue (Heap Order: Priority, PID) ---
| P200 (Pri:1) |
------------------------------------------------------
<- DEQUEUED: SCHEDULING Process ID 200 (Priority: 1)
Current Ready Queue: [Empty]

Queue is now empty.

Program finished execution.

Sample Output 3

=============== OS SCHEDULER PRIORITY QUEUE MENU ===============
Select a Test Scenario to Run:
1. Enqueue Test (Demonstrates Max Heap build on insertion)
2. Dequeue Test (Demonstrates Max Heap extraction/scheduling)
3. Full Combination Test (Dynamic OS Scheduling Scenario)
==================================================================
Enter your choice (1, 2, or 3): 3

--- Scheduler Queue initialized with capacity 10. ---

--- Test 3: COMBINATION (Dynamic OS Scheduling) ---

--- STEP 1: Process Arrival (Enqueuing Tasks) ---
-> ENQUEUED: Process ID 101 (Priority: 9)
-> ENQUEUED: Process ID 205 (Priority: 3)
-> ENQUEUED: Process ID 312 (Priority: 5)
-> ENQUEUED: Process ID 400 (Priority: 2)

--- Current Ready Queue (Heap Order: Priority, PID) ---
| P101 (Pri:9) | P205 (Pri:3) | P312 (Pri:5) | P400 (Pri:2) |
------------------------------------------------------

--- STEP 2: Scheduler Dispatch (Dequeuing Highest Priority) ---
<- DEQUEUED: SCHEDULING Process ID 101 (Priority: 9)

New critical process arrives:
-> ENQUEUED: Process ID 550 (Priority: 10)

--- Current Ready Queue (Heap Order: Priority, PID) ---
| P550 (Pri:10) | P312 (Pri:5) | P400 (Pri:2) | P205 (Pri:3) |
------------------------------------------------------
<- DEQUEUED: SCHEDULING Process ID 550 (Priority: 10)

--- STEP 3: Scheduling Remaining Tasks ---
<- DEQUEUED: SCHEDULING Process ID 312 (Priority: 5)
<- DEQUEUED: SCHEDULING Process ID 205 (Priority: 3)
<- DEQUEUED: SCHEDULING Process ID 400 (Priority: 2)

All processes have been scheduled and executed in priority order.

Program finished execution.
```

main.c

```c
#include <stdio.h>
#include <stdlib.h>
#include "types.h"

/**
 * @brief Prints the current processes in the queue (in heap order, not sorted).
 * @param pq Pointer to the PriorityQueue.
 */
void printQueue(PriorityQueue *pq) {
    if (pq->size == 0) {
        printf("Current Ready Queue: [Empty]\n");
        return;
    }

    printf("\n--- Current Ready Queue (Heap Order: Priority, PID) ---\n");
    for (int i = 0; i < pq->size; i++) {
        printf("| P%d (Pri:%d) ", pq->heap[i].pid, pq->heap[i].priority);
    }
    printf("|\n------------------------------------------------------\n");
}

int main() {
    int choice;

    printf("=============== OS SCHEDULER PRIORITY QUEUE MENU ===============");
    printf("\nSelect a Test Scenario to Run:");
    printf("\n1. Enqueue Test (Demonstrates Max Heap build on insertion)");
    printf("\n2. Dequeue Test (Demonstrates Max Heap extraction/scheduling)");
    printf("\n3. Full Combination Test (Dynamic OS Scheduling Scenario)");
    printf("\n==================================================================");
    printf("\nEnter your choice (1, 2, or 3): ");

    if (scanf("%d", &choice) != 1) {
        printf("\n\n--- INVALID INPUT: Please enter a number (1-3). Exiting. ---\n");
        return 1;
    }

    switch (choice) {
        case 1:
            runEnqueueTest();
            break;
        case 2:
            runDequeueTest();
            break;
        case 3:
            runCombinationTest();
            break;
        default:
            printf("\n\n--- INVALID CHOICE: Please selected 1, 2, or 3. Exiting. ---\n");
            break;
    }

    printf("\nProgram finished execution.\n");

    return 0;
}
```

tests.c

```c
#include <stdio.h>
#include <stdlib.h>
#include "types.h"

// =================================================================
//                 TEST SCENARIOS IMPLEMENTATION
// =================================================================

/**
 * @brief Test Scenario 1: Focuses solely on Enqueuing processes.
 * Demonstrates how the Max Heap is built upon insertion.
 */
void runEnqueueTest() {
    PriorityQueue schedulerQueue;
    initQueue(&schedulerQueue);

    printf("\n--- Test 1: ENQUEUE (Process Arrival) ---\n");
    printf("Inserting processes in various priority orders:\n");

    insertProcess(&schedulerQueue, (Process){.pid = 10, .priority = 5});
    insertProcess(&schedulerQueue, (Process){.pid = 20, .priority = 8}); // Higher priority than 10
    insertProcess(&schedulerQueue, (Process){.pid = 30, .priority = 3});
    insertProcess(&schedulerQueue, (Process){.pid = 40, .priority = 9}); // Highest priority
    insertProcess(&schedulerQueue, (Process){.pid = 50, .priority = 7});

    printQueue(&schedulerQueue);
    printf("NOTE: The highest priority process (PID 40, Pri 9) is at the top of the heap (first in the list).\n");
}

/**
 * @brief Test Scenario 2: Focuses solely on Dequeuing processes.
 * Requires pre-loading data to demonstrate extraction behavior.
 */
void runDequeueTest() {
    PriorityQueue schedulerQueue;
    initQueue(&schedulerQueue);

    printf("\n--- Test 2: DEQUEUE (Scheduling Dispatch) ---\n");
    printf("Pre-loading 5 processes for scheduling...\n");

    // Pre-load data
    insertProcess(&schedulerQueue, (Process){.pid = 100, .priority = 4});
    insertProcess(&schedulerQueue, (Process){.pid = 200, .priority = 1});
    insertProcess(&schedulerQueue, (Process){.pid = 300, .priority = 6});
    insertProcess(&schedulerQueue, (Process){.pid = 400, .priority = 3});
    insertProcess(&schedulerQueue, (Process){.pid = 500, .priority = 5});

    printf("\nReady Queue before dispatch:\n");
    printQueue(&schedulerQueue);

    printf("\nDispatching processes in order of priority (Max Heap extraction):\n");
    while (schedulerQueue.size > 0) {
        Process dispatched = extractMax(&schedulerQueue);
        if (dispatched.pid != -1) {
            printf("<- DEQUEUED: SCHEDULING Process ID %d (Priority: %d)\n", dispatched.pid, dispatched.priority);
            printQueue(&schedulerQueue); // Show state after each dispatch
        }
    }
    printf("\nQueue is now empty.\n");
}


/**
 * @brief Test Scenario 3: The original combination of Enqueue and Dequeue,
 * demonstrating a dynamic scheduling environment.
 */
void runCombinationTest() {
    PriorityQueue schedulerQueue;
    initQueue(&schedulerQueue);

    printf("\n--- Test 3: COMBINATION (Dynamic OS Scheduling) ---\n");

    printf("\n--- STEP 1: Process Arrival (Enqueuing Tasks) ---\n");

    // Scenario: High priority interactive task arrives
    insertProcess(&schedulerQueue, (Process){.pid = 101, .priority = 9}); // High priority
    // Scenario: Background job arrives
    insertProcess(&schedulerQueue, (Process){.pid = 205, .priority = 3}); // Low priority
    // Scenario: Medium-priority system task
    insertProcess(&schedulerQueue, (Process){.pid = 312, .priority = 5}); // Medium priority
    // Scenario: Another background job arrives (lower priority than previous one)
    insertProcess(&schedulerQueue, (Process){.pid = 400, .priority = 2}); // Lowest priority

    printQueue(&schedulerQueue);

    printf("\n--- STEP 2: Scheduler Dispatch (Dequeuing Highest Priority) ---\n");

    // The scheduler picks the task with the highest priority (PID 101, Pri 9)
    Process dispatched1 = extractMax(&schedulerQueue);
    printf("<- DEQUEUED: SCHEDULING Process ID %d (Priority: %d)\n", dispatched1.pid, dispatched1.priority);

    // Scenario: A new critical process arrives while others are waiting
    printf("\nNew critical process arrives:\n");
    insertProcess(&schedulerQueue, (Process){.pid = 550, .priority = 10}); // NEW Highest priority

    printQueue(&schedulerQueue);

    // The scheduler picks the next task. It should be PID 550 (Pri 10) now.
    Process dispatched2 = extractMax(&schedulerQueue);
    printf("<- DEQUEUED: SCHEDULING Process ID %d (Priority: %d)\n", dispatched2.pid, dispatched2.priority);

    // Continue scheduling the remaining tasks
    printf("\n--- STEP 3: Scheduling Remaining Tasks ---\n");

    while (schedulerQueue.size > 0) {
        Process dispatched = extractMax(&schedulerQueue);
        printf("<- DEQUEUED: SCHEDULING Process ID %d (Priority: %d)\n", dispatched.pid, dispatched.priority);
    }

    printf("\nAll processes have been scheduled and executed in priority order.\n");
}
```

types.h

```c
#ifndef TYPES_H
#define TYPES_H

// Maximum number of processes the scheduler can hold
#define MAX_PROCESSES 10

// Process Structure
// A structure representing a task/process in the operating system.
typedef struct {
    int pid;      // Process ID (Unique Identifier)
    int priority; // Priority level (Higher number = Higher priority)
} Process;

// Priority Queue Structure (Max Heap Implementation)
// The heap array will store the processes.
typedef struct {
    Process heap[MAX_PROCESSES]; // Array to store the heap elements
    int size;                    // Current number of processes in the queue
    int capacity;                // Maximum capacity of the queue
} PriorityQueue;

void initQueue(PriorityQueue *pq);
void swap(Process *a, Process *b);
void heapifyDown(PriorityQueue *pq, int index);
void insertProcess(PriorityQueue *pq, Process newProcess);
Process extractMax(PriorityQueue *pq);
void printQueue(PriorityQueue *pq);
void runEnqueueTest(void);
void runDequeueTest(void);
void runCombinationTest(void);

#endif
```

pq.c

```c
#include <stdio.h>
#include <stdlib.h>
#include "types.h"

// write your functions here
```