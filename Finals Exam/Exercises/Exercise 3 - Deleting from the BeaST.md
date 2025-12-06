Practice deleting elements from BST

Steps (iterative):

1. Find the node to delete ('current') and its parent ('parent')
2. Handle case 3: Node with 2 children  
    1. Find the in-order successor (minimum node in the right subtree) and its parent
    2. Copy successor's key to the current node (replacement)
    3. Update 'current' and 'parent' for the remaining logic to delete the successor's original location.
3. Case 1 & 2: Node with 0 or 1 child (or the successor after Case 3)

Also try:
- Recursive and iterative delete function

Sample output:

```c
--- Building BST for Deletion Test ---
Inserted: "Mango"
Inserted: "Apple"
Inserted: "Pineapple"
Inserted: "Banana"
Inserted: "Grape"
Inserted: "Orange"
Inserted: "Kiwi"

Initial In-Order Traversal:
   "Apple" "Banana" "Grape" "Kiwi" "Mango" "Orange" "Pineapple"

--- Test 1: Delete Leaf Node (Kiwi) ---
Resulting Traversal: "Apple" "Banana" "Grape" "Mango" "Orange" "Pineapple"

--- Test 2: Delete Node with 1 Child (Apple) ---
Resulting Traversal: "Banana" "Grape" "Mango" "Orange" "Pineapple"

--- Test 3: Delete Node with 2 Children (Mango - the Root) ---
Resulting Traversal: "Banana" "Grape" "Orange" "Pineapple"

--- Test 4: Delete Non-Existent Key (Zebra) ---
Key "Zebra" not found for deletion.
No change expected: "Banana" "Grape" "Orange" "Pineapple"

Tree destroyed and memory freed.
```

main.c

```c
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#include "types.h"

/**
 * @brief Deletes a node with the given key from the BST.
 * @param root The current root of the BST.
 * @param key_data The string key to delete.
 * @return BST The new root of the BST after deletion.
 */
BST deleteNode(BST root, const char *key_data) {
    // TO DO
    
    // tried nested helper function
    BST findMinLocal(BST node) {
        while (node && node->LC != NULL)
            node = node->LC;
        return node;
    }

    if (root == NULL) {
        printf("Key \"%s\" not found for deletion.\n", key_data);
        return NULL;
    }

    int cmp = strcmp(key_data, root->key);

    if (cmp < 0) {
        root->LC = deleteNode(root->LC, key_data);
    }
    else if (cmp > 0) {
        root->RC = deleteNode(root->RC, key_data);
    }
    else {
        if (root->LC == NULL) {
            BST temp = root->RC;
            free(root->key);
            free(root);
            return temp;
        }
        else if (root->RC == NULL) {
            BST temp = root->LC;
            free(root->key);
            free(root);
            return temp;
        }

        BST temp = findMinLocal(root->RC);

        free(root->key);
        root->key = strdup(temp->key);

        root->RC = deleteNode(root->RC, temp->key);
    }

    return root;
}

int main() {
    // 1. Create and initialize the tree
    BST myTree = NULL;

    printf("--- Building BST for Deletion Test ---\n");
    // Keys: Apple, Banana, Grape, Kiwi, Mango(ROOT), Orange, Pineapple
    insert(&myTree, "Mango");      // Root
    insert(&myTree, "Apple");      // Left of Mango
    insert(&myTree, "Pineapple");  // Right of Mango
    insert(&myTree, "Banana");     // Right of Apple
    insert(&myTree, "Grape");      // Left of Pineapple
    insert(&myTree, "Orange");     // Right of Grape
    insert(&myTree, "Kiwi");       // Left of Orange

    printf("\nInitial In-Order Traversal:\n   ");
    inorderTraversal(myTree);
    printf("\n");

    // --- Deletion Tests ---

    printf("\n--- Test 1: Delete Leaf Node (Kiwi) ---\n");
    // Kiwi is a leaf node (0 children)
    myTree = deleteNode(myTree, "Kiwi");
    printf("Resulting Traversal: ");
    inorderTraversal(myTree);
    printf("\n");

    printf("\n--- Test 2: Delete Node with 1 Child (Apple) ---\n");
    // Apple has 1 child (Banana)
    myTree = deleteNode(myTree, "Apple");
    printf("Resulting Traversal: ");
    inorderTraversal(myTree);
    printf("\n");

    printf("\n--- Test 3: Delete Node with 2 Children (Mango - the Root) ---\n");
    // Mango is replaced by its successor (Orange)
    myTree = deleteNode(myTree, "Mango");
    printf("Resulting Traversal: ");
    inorderTraversal(myTree);
    printf("\n");

    printf("\n--- Test 4: Delete Non-Existent Key (Zebra) ---\n");
    myTree = deleteNode(myTree, "Zebra");
    printf("No change expected: ");
    inorderTraversal(myTree);
    printf("\n");

    // 2. Clean up memory
    destroyTree(myTree);
    printf("\nTree destroyed and memory freed.\n");

    return 0;
}
```

types.h

```c
#ifndef TYPES_H
#define TYPES_H

// Define a maximum length for the key
#define MAX_KEY_LEN 100

// 1. Structure Definition
typedef struct node {
   char *key;          // The string element used for comparison and storage
   struct node* LC;   // Left Child pointer
   struct node* RC;   // Right Child pointer
} Node, *BST;

#endif
```

