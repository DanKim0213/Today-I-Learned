# Priority Queue 

Table of Content
- Heap vs Priority Queue
- Heap
- Priority Queue

> In computer science, a priority queue is an abstract data-type. Each element in a priority queue has an associated priority. In a priority queue, elements with high priority are served before elements with low priority. - [Wikipedia](https://en.wikipedia.org/wiki/Priority_queue)

A priority queue is a powerful tool that can solve problems as varied as writing an email scheduler, finding the shortest path on a map, or merging log files. 

## Heap vs Priority Queue

Heaps are concrete data structures, whereas priority queues are abstract data type. Heaps are commonly used to implement priority queues. They’re the most popular concrete data structure for implementing the priority queue abstract data type.

## Heap

### What is Heap?

In a heap tree, the value in a node is always smaller than both of its children. This is called the heap property. This is different from a binary search tree, in which only the left node will be smaller than the value of its parent.

The algorithms for both pushing and popping rely on temporarily violating the heap property, then fixing the heap property through comparisons and replacements up or down a single branch.

Similarly, when popping the smallest element, Python knows that, because of the heap property, the element is at the root of the tree. It replaces the element with the last element at the deepest layer and then checks if the heap property is violated down the branch.

### Does *heapify* sort?

```python
import heapq
a = [3, 5, 1, 2, 6, 8, 7]
heapq.heapify(a)
print(a) # [1, 2, 3, 5, 6, 8, 7]
```

No. As you can see, heapify() modifies the list in place but doesn’t sort it. A heap doesn’t have to be sorted to satisfy the heap property. However, since every sorted list does satisfy the heap property, running heapify() on a sorted list won’t change the order of elements in the list.

## Priority Queue

### What is Priority Queue?

The priority queue abstract data type, for example, supports three operations:
- `peek` peeks the root element which is the highest priority.
- `push` pushes an element to the queue.
- `pop` pops the element with the highest priority.

### Time Complexity

1. **Binary Heap**:
   - Insertion: O(log n)
   - Deletion (extract-min or extract-max): O(log n)
   - Search: O(n)

2. Fibonacci Heap:
   - Insertion: O(1)
   - Deletion (extract-min or extract-max): O(log n) amortized
   - Search: O(n)

3. Binary Search Tree (BST):
   - Insertion: O(log n) on average, O(n) in the worst case (unbalanced tree)
   - Deletion: O(log n) on average, O(n) in the worst case (unbalanced tree)
   - Search: O(log n) on average, O(n) in the worst case (unbalanced tree)

(Note that these time complexities are given in terms of the number of elements in the priority queue, represented by "n".) 

### What is the time complexity of heapify in priority queue?

The time complexity of the heapify operation in a priority queue implemented using a binary heap is O(n), where n is the number of elements in the heap.

Heapify is an operation that takes an array of elements and rearranges them to form a valid heap structure. It is typically used to build a heap from an unsorted array or to restore the heap property after an element has been removed or modified.

The heapify operation works by repeatedly "bubbling down" elements from the root node to their correct positions in the heap. Starting from the last non-leaf node and moving up to the root, each node is compared with its children and swapped if necessary to maintain the heap property.

In the worst case, each element may need to be compared with and potentially swapped with its children multiple times as it "bubbles down" through the heap. Since there are n/2 non-leaf nodes in a binary heap, the number of comparisons and swaps required by heapify is proportional to the number of elements in the heap, resulting in a time complexity of O(n).

It's important to note that the heapify operation is typically a one-time operation performed during the initialization of a priority queue or when rebuilding a heap structure. Once the heap is constructed, subsequent insertions and deletions can be performed in O(log n) time.

### As I know whenever insertion or deletion in priority queue built in binary heap is done, heapify is required. Thus, could the time complexity of insertion be O(n * logn)?

No, the time complexity of insertion in a binary heap-based priority queue is not O(n * log n). The time complexity of insertion in a binary heap is O(log n), where n is the number of elements in the heap.

When inserting an element into a binary heap, it is initially placed at the bottommost rightmost position in the heap (the next available leaf node). The element is then "bubbled up" or "percolated up" by comparing it with its parent and swapping if necessary to maintain the heap property.

The number of comparisons and swaps required during the insertion process is proportional to the height of the heap, which is logarithmic in the number of elements. Hence, the time complexity of insertion in a binary heap is O(log n).

After the insertion, if the heap property is violated, only a portion of the heap may need to be restructured by performing a "bubbledown" operation, not a full heapify operation. This operation has a time complexity of O(log n) as well.

It's worth mentioning that the overall time complexity of performing a series of insertions into a binary heap-based priority queue is determined by summing up the individual insertion complexities. For n insertions, the total time complexity would be O(n log n), not O(n * log n), as the logarithmic factor remains the same for each insertion operation.

## Furthermore

- [The Python heapq Module: Using Heaps and Priority Queus](https://realpython.com/python-heapq-module/)
- [Understanding Priority Queue in Python with Implementation](https://www.pythonpool.com/python-priority-queue/)
