# Stationary_Queue

It is a sequential data structure, a Circular Queue. Unlike most implementations, it is fixed size. This means insertion/deletion only, is not supported, however, pushing one and and popping the other end can be done with 1 main memory access.When the offset is 0, the content is layed out in memory exactly as it is interpreted.
It has an underlying simple std::vector,called Data, and an offset. The offset marks the 0the element, and the rest is layed out in order.
When the end of Data is reached, the data starts again at it's beginning. With n sized Data and n elements, almost always, the first and the last element will be next to each other, meaning the "after last" is the first element, causing popping at the beginning and pushing to the end, be a simple in place overwrite, and similarly, the last element being the "before first" causes the same  speedup to be the case.
Example of a layout with 10 elements and an offset of 7:
4 5 6 7 8 9 0 1 2 3.    OFFSET:7
Pushing_front x would make it:
4 5 6 7 8 x 0 1 2 3.    OFFSET:6   
Such pushing also returns the overwritten value, in this case, 9.
