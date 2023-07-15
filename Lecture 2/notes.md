# Lecture 2: Data Structures and Dynamic Arrays

## Data Structure and Interfaces

- An interface is a collection of supported operations (API)
- A data structure is a way to store data
- and interface is a specification: what operations are supported (the problem !)
- a data structure is a representation: how operations are supported (the solution !)

## Sequence Interface

- maintain a sequence of items(order is extrinsic)
- Ex: (xo,x1,x2....xn+1)(zero indexing)
- (use _n_ to denote the number of items stored in the data structure)

## Static Arrays

- Key: Word RAM model of computation
  - memory = array of w-bit works
  - RAM: random access memory
  - "array" = consecutive chunk of memory
  - array[i] === memory [address(array)+i]
  - aray access is O(1) time (constant time)

## Linked List Sequence

- Pointer data structure
- Each item stored in a **node** which contains a pointer to the next node in sequence
- Each node has two fields: node.item and node.next
- Can manipulate pointers to the first node in sequence (Called the head)
- Can now insert and delete from the front in theta(1) time! YAY!
- inersting/ deleting efficiently from back is also possible
- But now get_at(i) and set_at(i, x) each take O(n) time

## Dynamic Arrays

- make an array efficient for **last** dynamic operations
- (Python Lists is a dynamic array)
- relax constraint that the size(array) = n -> n # of items
- enforce size = theta(n) & >= n
- maintain A[i]=xi
- **Idea!** Allocate extra space so reallocation does not occur with every dynamic operation
- **Fill ratio** 0<= r <= 1 the ration of items to space
- whenever array is full (r=1), allocate theta(n) extra space at end to fill ratio ri (eg., 1/2)
- Will have to insert theta(n) items before the next reallocation
- A single operation can take theta(n) time for reallocation
- A single operation can take theta(n) time for reallocatino
- Hoever, any sequence of theta(n) operations takes theta(n) time
- So each operation takes theta(1) time "on average"

## Amortized Analysis

- Data structure analysis technique to distribute cost over many operations
- Operation has amortized cost T(n) if _k_ operations cost at mose <=kT(n)
- "T(n) amortized" roughly means T(n) "on average" over many operations
- inserting into a dynamic array takes theta(1) amortized time
- more ammortization analysis techniques in 6.046

## Dynamic Array Deletion

- Delete from back? theta(1) time without effort, yay!
- However, can be very wasteful in space. Want size of data structure to stay theta(n)
- **Attempt:** if empty, resize to r =1. Alternation insertion and deletion could be bad.
- **Idea!** When r < rd, resize array to ratio r, where rd < ri
- Then theta(n) cheap operations must be made before next expensive resize
- Can limit extra space usage to (1+E)n for any E > 0
- Dynamic arrays only support dynamic last operations in theta(1)
- Python List append and pop are amortized O(1) time, other operations can be O(n)!
- (inserting/deleting efficiently from front is also possible)
