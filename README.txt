Names: Dylan Cancelliere, Jaden Seaton
Project Choice : Mark-Sweep Garbage Collector for uScheme
Time spent on assignment : 22 hours
Additional Collaborators : None

1. Solution

Our solution leveraged the lazy mark and sweep implementation that was
discussed during lecture. Our modifications center around the
allocation function, as is necessary to reap the benefits of amortizing
the sweep phase.

In further detail, during allocation we first sweep to find an available
space on the heap. Eventually, the program will reach the end of the
heap and the program begins garbage collection. Our implementation
leverages the provided visit functions to go through and mark each
reachable piece of data.

Then, the heap pointer will be reset to the start of the heap (ie
pagelist). Going forward, each sweep phase will increment the heap
pointer until it finds a space that's not marked as live, which it will
return to be reallocated. This continues until either the program
terminates, or if every memory space is marked.

Once every space is marked, the program adds a new page (a standardized
capacity grouping) to the heap and moves the heap pointer to the start
of the new page. At this point, the garbage collector is fully
developed, and this loop will continue in perpetuity.

It's also worth noting on an implementation specific note, when the
program reaches the end of a page, that it has not necessarily reached
the end of the heap. So, the pagelist functions as a linked list that
points to the next page to be used. When the program reaches the end of
a page, it checks to see if there are more pages, and if there are it
adjusts the heap pointer and limit appropriately.

2. Testing

... description of how you tested your submission ...
... ( why are you convinced that it works correctly ) ...

3. Functionality

To the best of my knowledge, the project works as intended. Despite
this, I'm not super confident in my approach to mark. From my
understanding of the algorithm the visit procedures (ie visitroots)
should accomplish marking everything reachable from the roots. However,
question 7 in the textbook that the assignment is based off of says
to create a separate mark procedure that calls visit as needed, which
I have not found to be necessary. Because of this, it feels like I'm
missing an important piece to the project despite everything seeming
to work as intended.

Likewise, question 8 references a function called growheap, but again
it appears that this functionality has already been written in via the
addpage function. This example particularly makes me think that perhaps
the source code I'm working with is already augmented compared to what
the book expects, but nonetheless it is potentially cause for concern.