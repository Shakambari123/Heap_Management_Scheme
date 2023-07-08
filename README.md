# Heap_Management_Scheme
I have implemented Allocation and Deallocation of memory and garbage
collection that takes place inside a heap using Doubly linked lists using C
language.


1. The code begins with the definition of a structure called `Node_tag`. This structure represents a node in the doubly linked list. It contains several fields:
   - `tag` is an integer value representing the identifier or tag assigned to a particular block of memory.
   - `size` is an integer representing the size of the memory block.
   - `data` is an integer representing the user-input data associated with the memory block.
   - `next` is a pointer to the next node in the linked list.
   - `prev` is a pointer to the previous node in the linked list.
   - `isFree` is a boolean flag indicating whether the memory block is free (1) or allocated (0).

2. The `Node` type is defined as a typedef of `struct Node_tag`. It provides a convenient way to refer to instances of this structure.

3. The variable `head` is declared as a pointer to a `Node` and is initially set to `NULL`. It will point to the first node in the linked list.

4. The variable `tag_id` is declared and initialized to 1. It will be used to assign unique tags to memory blocks.

5. The `allocate` function takes an integer parameter `c`, which represents the desired size of the memory block to be allocated. It searches for a free node in the linked list with sufficient size to accommodate `c`.

6. Inside the `allocate` function, a pointer `ptr` is created and initialized with the `head` pointer, which points to the first node in the linked list.

7. A while loop is used to iterate through the linked list until either a free node with sufficient size or the end of the list is reached.

8. If a suitable node is found, indicated by `(ptr->isFree)&&(c<=ptr->size)`, the loop breaks.

9. After the loop, if `ptr` is not `NULL`, it means a free node with sufficient size was found. Further operations are performed to allocate the memory block:
   - Pointers `next_ptr` and `prev_ptr` are initialized with the next and previous pointers of `ptr`.
   - If `c` is not equal to `ptr->size`, a new node is created using `malloc` to represent the remaining free space after allocating the desired block. This new node is inserted into the linked list after `ptr`.
   - The `size`, `prev`, `next`, and `isFree` fields of the new node and `ptr` are updated accordingly.
   - The `tag` field of `ptr` is assigned the `tag_id` value and `tag_id` is incremented.
   - Finally, the `isFree` field of `ptr` is set to `FALSE` to mark the memory block as allocated.

10. If `ptr` is `NULL`, it means a suitable free node was not found, and a message "no suff. space" is printed to indicate insufficient space.

11. The `free_node` function is responsible for freeing a previously allocated memory block based on its tag.

12. Inside the `free_node` function, a pointer `ptr` is created and initialized with the `head` pointer.

13. A while loop is used to iterate through the linked list until either a node with the given tag or the end of the list is reached.

14. If a node with the desired tag is found, indicated by `delete_tag==ptr->tag`, the loop breaks.

15. After the loop, if `ptr` is not `NULL`, it means a node with the specified tag was found, and it can be freed:
   - Pointers `next_ptr` and `prev_ptr` are initialized with the next and previous pointers of `ptr`.
   - The `isFree` field of `ptr` is set to `TRUE` to mark the memory block as free.
   - If the next node `next_ptr` exists and is also free, the two nodes are merged by updating the `size` and `next` pointers of `ptr` and freeing the `next_ptr`.
   - Similarly, if the previous node `prev_ptr` exists and is also free, the two nodes are merged by updating the `size` and `prev` pointers of `ptr` and freeing the `prev_ptr`.
   - If `prev_ptr` is the `head` node, the `head` pointer is updated to `ptr`.
   - Finally, the `tag` field of `ptr` is set to `-1` to indicate that it is no longer associated with any tag.

16. If `ptr` is `NULL`, it means a node with the specified tag was not found, and a message "No such tag_id exist" is printed.

This code provides a basic memory allocation and deallocation mechanism using a doubly linked list, allowing the user to allocate and free memory blocks of various sizes.
