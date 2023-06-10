## LinkedList using Python

### Code

```python
class Node:
    def __init__(self, data):
        self.data = data
        self.next = None

class LinkedList:
    def __init__(self):
        self.head = None

    def insert_at_beginning(self, data):
        """
        Inserts a node at the beginning of the linked list.
        Time complexity: O(1)
        Space complexity: O(1)
        """
        new_node = Node(data)
        new_node.next = self.head
        self.head = new_node

    def insert_at_end(self, data):
        """
        Inserts a node at the end of the linked list.
        Time complexity: O(n), where n is the number of nodes in the linked list
        Space complexity: O(1)
        """
        new_node = Node(data)
        if not self.head:
            self.head = new_node
        else:
            current = self.head
            while current.next:
                current = current.next
            current.next = new_node

    def insert_after(self, prev_node, data):
        """
        Inserts a node after a given node in the linked list.
        Time complexity: O(1)
        Space complexity: O(1)
        """
        if not prev_node:
            print("Previous node is not in the list.")
            return
        new_node = Node(data)
        new_node.next = prev_node.next
        prev_node.next = new_node

    def insert_at_nth_position(self, position, data):
        """
        Inserts a node at a specified position in the linked list.
        Time complexity: O(n), where n is the number of nodes in the linked list
        Space complexity: O(1)
        """
        if position == 0:
            self.insert_at_beginning(data)
        else:
            new_node = Node(data)
            current = self.head
            count = 1
            while current and count < position:
                current = current.next
                count += 1

            if not current:
                print("Position out of range.")
                return

            new_node.next = current.next
            current.next = new_node

    def delete_node(self, data):
        """
        Deletes a node with the given data from the linked list.
        Time complexity: O(n), where n is the number of nodes in the linked list
        Space complexity: O(1)
        """
        if not self.head:
            print("List is empty.")
            return

        if self.head.data == data:
            self.head = self.head.next
            return

        current = self.head
        prev = None

        while current:
            if current.data == data:
                break
            prev = current
            current = current.next

        if not current:
            print("Node not found.")
            return

        prev.next = current.next

    def delete_at_position(self, position):
        """
        Deletes a node at the specified position in the linked list.
        Time complexity: O(n), where n is the number of nodes in the linked list
        Space complexity: O(1)
        """
        if not self.head:
            print("List is empty.")
            return

        if position == 0:
            self.head = self.head.next
            return

        current = self.head
        prev = None
        count = 0

        while current and count != position:
            prev = current
            current = current.next
            count += 1

        if not current:
            print("Position out of range.")
            return

        prev.next = current.next

    def search(self, data):
        """
        Searches for a node with the given data in the linked list.
        Time complexity: O(n), where n is the number of nodes in the linked list
        Space complexity: O(1)
        """
        if not self.head:
            return False

        current = self.head
        while current:
            if current.data == data:
                return True
            current = current.next

        return False

    def search_position(self, data):
        """
        Searches for a node with the given data and returns its position.
        Time complexity: O(n), where n is the number of nodes in the linked list
        Space complexity: O(1)
        """
        if not self.head:
            return -1

        current = self.head
        position = 0
        while current:
            if current.data == data:
                return position
            current = current.next
            position += 1

        return -1

    def reverse(self):
        """
        Reverses the linked list.
        Time complexity: O(n), where n is the number of nodes in the linked list
        Space complexity: O(1)
        """
        current = self.head
        prev = None

        while current:
            next_node = current.next
            current.next = prev
            prev = current
            current = next_node

        self.head = prev

    def print_list(self):
        """
        Prints the elements of the linked list.
        Time complexity: O(n), where n is the number of nodes in the linked list
        Space complexity: O(1)
        """
        current = self.head
        while current:
            print(current.data, end=" -> ")
            current = current.next
        print()
```

### Explanation

1. Node Class:
    - The `Node` class represents a single node in the linked list.
    - It has two attributes: `data` to store the value of the node and `next` as a reference to the next node in the list.
    - When a new node is created, the `__init__` method sets the `data` attribute to the provided value and `next` to None.
2. LinkedList Class:
    - The `LinkedList` class serves as the container for the linked list.
    - It has one attribute, `head`, which points to the first node in the list. Initially, it is set to None.
    - The `__init__` method initializes the `head` attribute as None.
3. Insertion Methods:
    - `insert_at_beginning(data)`:
        - Creates a new node with the provided `data` value.
        - Sets the `next` of the new node to the current head of the list.
        - Updates the `head` of the list to point to the new node, making it the new first node.
    - `insert_at_end(data)`:
        - Creates a new node with the provided `data` value.
        - If the list is empty (head is None), sets the new node as the head.
        - Otherwise, traverses to the last node using a while loop.
        - Sets the `next` of the last node to the new node, making it the new last node.
    - `insert_after(prev_node, data)`:
        - Checks if the `prev_node` exists (not None) in the list.
        - Creates a new node with the provided `data` value.
        - Sets the `next` of the new node to the `next` of `prev_node`.
        - Sets the `next` of `prev_node` to the new node, effectively inserting it after `prev_node`.
    - `insert_at_nth_position(position, data)`:
        - Handles the special case of inserting at position 0 (beginning) by calling `insert_at_beginning`.
        - Creates a new node with the provided `data` value.
        - Traverses the list using a while loop, stopping at the node preceding the desired position.
        - Adjusts the pointers to insert the new node at the desired position.
4. Deletion Methods:
    - `delete_node(data)`:
        - Handles the special case when the node to be deleted is the head node.
        - Traverses the list using a while loop to find the node to be deleted and its previous node.
        - Adjusts the pointers of the previous node to skip the node to be deleted.
    - `delete_at_position(position)`:
        - Handles the special case when the position to be deleted is 0 (head node).
        - Traverses the list using a while loop to find the node at the desired position and its previous node.
        - Adjusts the pointers of the previous node to skip the node at the desired position.
5. Search Methods:
    - `search(data)`:
        - Traverses the list using a while loop to check if any node contains the given `data` value.
        - Returns `True` if found, otherwise `False`.
    - `search_position(data)`:
        - Traverses the list using a while loop to check if any node contains the given `data` value.
        - Returns the position (index) of the node if found, otherwise -1.
6. Reverse Method:
    - `reverse()`:
        - Traverses the list using a

while loop, starting from the head node.
- Uses three pointers, `current`, `prev`, and `next_node`, to reverse the links between nodes.
- Iteratively updates the `next` pointer of each node to point to the previous node.
- Finally, updates the `head` to the last node encountered, effectively reversing the list.

1. Print Method:
    - `print_list()`:
        - Traverses the list using a while loop, starting from the head node.
        - Prints the `data` value of each node, separated by an arrow "->".

### Complexity

1. Node Class:
    - No methods, only attributes.
2. LinkedList Class:
    - No methods, only attributes.
3. Insertion Methods:
    - `insert_at_beginning(data)`:
        - Time Complexity: O(1) - Insertion at the beginning of the list takes constant time.
        - Space Complexity: O(1) - No additional space is required.
    - `insert_at_end(data)`:
        - Time Complexity: O(N) - Insertion at the end requires traversing the entire list.
        - Space Complexity: O(1) - No additional space is required.
    - `insert_after(prev_node, data)`:
        - Time Complexity: O(1) - Insertion after a specific node takes constant time.
        - Space Complexity: O(1) - No additional space is required.
    - `insert_at_nth_position(position, data)`:
        - Time Complexity: O(N) - In the worst case, when inserting at the end or beyond the end, traversal of the list is required.
        - Space Complexity: O(1) - No additional space is required.
4. Deletion Methods:
    - `delete_node(data)`:
        - Time Complexity: O(N) - In the worst case, when the node to be deleted is at the end, traversal of the list is required.
        - Space Complexity: O(1) - No additional space is required.
    - `delete_at_position(position)`:
        - Time Complexity: O(N) - In the worst case, when deleting the last node or beyond the end, traversal of the list is required.
        - Space Complexity: O(1) - No additional space is required.
5. Search Methods:
    - `search(data)`:
        - Time Complexity: O(N) - In the worst case, when the value is not found, traversal of the entire list is required.
        - Space Complexity: O(1) - No additional space is required.
    - `search_position(data)`:
        - Time Complexity: O(N) - In the worst case, when the value is not found, traversal of the entire list is required.
        - Space Complexity: O(1) - No additional space is required.
6. Reverse Method:
    - `reverse()`:
        - Time Complexity: O(N) - Reversing the linked list requires traversing the entire list once.
        - Space Complexity: O(1) - No additional space is required.
7. Print Method:
    - `print_list()`:
        - Time Complexity: O(N) - Printing all the nodes requires traversing the entire list.
        - Space Complexity: O(1) - No additional space is required.