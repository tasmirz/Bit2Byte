## Looking Back into Arrays

Array is indeed a great tool for iterative programming. However, would it have been enough, we needn't have to study the whole realm of Data Structures. 
Let's review array find out  where it lacks behind.

Array is a collection of **same sized data**, stored **consecutively** in computer memory. The highlighted property makes array very fast to access $O(1)$ . Let's watch some simulation which will give us insights on design limitations of array.

### Insertion at random position in array
As array elements are stored in consecutive order. Inserting a new one in $k$ position requires shifting all element from $k$ to $n$ by one position. 
 
![[gif-output-Sat02Nov2024044729GMT.gif]]
In this example , reader may find some limitations, 
* The last element (in case it's a filled array) gets lost.
* A vast amount of data exchange is required
#### Removing from random position in array
The next elements are shifted up to  
![[download.gif]]

#### The Array Simulator
![[Array.html]]
## What is a linked list ?
Linked list a data structure* holding a data element and one or more references (addresses). It's a referential structure. 

It can be a struct/object holding at least two members data and reference. Conventionally such an object/struct is called a **Node**.  Here reference is usually the memory address of the next node.

```cpp
struct Node {
	type data;
	Node next = null; //next is the reference to next node
}
```

> Every byte stored in memory has a specific address which allows random access. Variables are names of memory addresses. Variables containing address of another variable are called pointers.

![[Linked List.excalidraw]]

The initial node is called root. The last node is called tail. Usually these two node's addresses are available to the user.

```cpp
Node * root = new Node();
Node * tail;
root->next = new Node();
root->next->next = new Node();


// Or
Node * root = new Node();
Node * a = new Node();
Node * b = new Node();
root->next = a;
a->next = b;
```

It is visible that ,
* node *a* is not accessible from *b*
* *b* is also not directly accessible from  *root*
So in the mentioned example traversal is only possible from one direction. And only one advancement per iteration. 

**Question to the reader** : 
* Is it possible to traverse in both ways? If yes, can it be achieved with one reference only?
* Does this structure allow peeking into $i$<sup>th</sup> element in  single iteration?
* How to support different data types?

Array achieves $O(1)$ access time by keeping two constraints same size and consecutive memory. However in case of a linked list both size of element and memory location are not bound to any specified factors. 
### Traversing a Linked List

Traversing a linked list means visiting each node in the list exactly once. This can be done using a simple loop.

```cpp
Node* current = root;
while (current != nullptr) {
	// Process the current node
	current = current->next;
}
```
 Searching
 ![[search.mp4.gif]]
**Task** : 
* Try finding a specific element
* Compare this with array traversal and array accessing
### Insertion
There can be 3 types of insertion
1. Before current root
   ![[insert at root.excalidraw]]
3. In k<sup>th</sup> position
   ![[insert at mid.excalidraw]]
1. After tail
   ![[insert at tail.excalidraw]]
### Deletion
1. Current root
   ![[delete from root.excalidraw]]
2. From k<sup>th</sup> position
   ![[insert at mid.excalidraw]]
3. The tail - self study
   Hint: modify mid to update tail
### Merging

Array merging can be done in $O(1)$ if tail is known

![[merge.excalidraw]]

Exercise : 
* You are given two sorted list, now join these in  a single list such that the new list is sorted and no extra space is used
* Try implementing merge sort (node swapped) and analyze its complexity
## Why do we need linked lists
Reader may wonder, some extra modifications in array may achieve 
## Use cases

1. Maximum insertion deletion at front/end. Does not require array copy like array.
2. Sequential traversal
3. Regular merging
4. High data size : reference size ratio
5. Where nodes are referenced multiple times, swapping in list does not affect the other processes as address remains same. (imagine having a large binary data which are referenced by multiple processes and one linked list any swapping in the linked list does not affect others. And any updates are momentarily done )
### As underlying data structures
Linked list is often used as core structure of various data structures like deque, stack and queues as it support $O(1)$ insertion and deletion at front and back (doubly). These structures are used for **undo/redo**,  **pagination** , **task scheduling** / **task queue management**, **dfs path**, **graph list** etc. 
### Large file saving
Imagine saving a size in a sequentially filled file system. To maximize performance chunk size of 4KB is used.
![[filesave.excalidraw]]
### Chunked Array
Arrays can be chunked. Instead of resizing a new next node can be added to improve cache locality without requiring copying. this can be used for ranged counting sort.
### Chained Tasks
![[Pasted image 20241102234804.png]]
#### CRON Like
![[chainedtasks.excalidraw]]
#### State Management
![[states.excalidraw]]

#### Effect list
![[matrix.mp4.gif]]
![[house.mp4.gif]]
## Limitations
* Very low cache hit rate
  After registers, cache is the fastest memory. As major number of elements of an array is loaded into cache, sequential access is way faster than linked list.
* Extra space taken
* Slow random access
* Insertion deletion can slower than array
## ToDo
- [ ] Linked list Merge - in simulator