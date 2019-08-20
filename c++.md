# C++ theory

## General C++ concepts

* Plain old data (POD)
* Base class accessors and their effects
* References vs. pointers
* Polymorphism
* Full/partial template specialization
* Map vs. unordered_map vs. multimap vs. unordered_multimap
* Rule of three
* Functor objects
* Function pointer syntax
* Template syntax

## Important C++11 concepts

* `auto`
* `decltype()`
* Brace initialization
* Defaulted constructors
* `nullptr`
* Delegating constructors
* Move semantics
* Rvalue references
* Raw vs. weak vs. shared vs. unique pointers
* Placement new
* Override identifier
* Final identifier
* Futures and promises
* Variadic functions/structures

## Data structures

### STL deque

A deque is a double-ended queue.
Elements can be added to both its front and back in O(1).
Internally, deques are implemented as a vector of pointers to fixed-size vectors.
That way, if an element is added to the front of the queue, it can either be inserted into the first fixed-size vector, or a new fixed-size vector has to be allocated, in which case the pointers in the pointer vector have to be moved by one.
This is faster than moving all data elements, as would be the case for a vector.

Time complexity of common operations:

* Random access: O(1)
* Insertion or removal of elements at beginning or end: O(1)
* Random insertion or removal: O(n)

### STL array

STL arrays represent fixed-size containers.

### STL list

An STL list is implemented as a doubly-linked list.

Time complexity of common operations:

* Insertion: O(1)
* Deletion: O(1)
* Lookup: O(n)

### STL forward_list

An STL forward_list is implemented as singly-linked list.

Time complexity of common operations:

* Insertion: O(1)
* Deletion: O(1)
* Lookup: O(n)

### STL priority_queue

The STL implementation of a heap.
By default, a priority_queue is a max-heap.
This behavior can be changed by supplying a custom comparison function to the constructor.
