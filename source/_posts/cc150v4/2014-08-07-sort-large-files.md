---
layout: post
title: "[CC150v4] 9.4 Sort Large Files"
comments: true
category: CC150v4

---

### Question 

> If you have a 2 GB file with one string per line, which sorting algorithm would you use to sort the file and why?

### Solution

__External Sorting__ and N-way merge. 

1. Divide the file into K chunks, where X * K = 2 GB Bring each chunk into memory and sort the lines as usual using any O(n log n) algorithm Save the lines back to the file
1. Now bring the next chunk into memory and sort
1. Once we’re done, merge them one by one

### Details

[Wiki example](http://en.wikipedia.org/wiki/External_sorting#External_merge_sort) of sorting 900 megabytes of data using only 100 megabytes of RAM:

1. __Read 100 MB of the data in main memory and sort__ by some conventional method, like quicksort.
1. Write the sorted data to disk.
1. Repeat steps 1 and 2 until all of the data is in sorted 100 MB chunks (there are 900MB / 100MB = 9 chunks), which now need to be merged into one single output file.
1. __Read the first 10 MB (= 100MB / (9 chunks + 1)) of each sorted chunk__ into input buffers in main memory and allocate the remaining 10 MB for an output buffer. (In practice, it might provide better performance to make the output buffer larger and the input buffers slightly smaller.)
1. __Perform a 9-way merge__ and store the result in the output buffer. Whenever the output buffer fills, write it to the final sorted file and empty it. Whenever any of the 9 input buffers empties, fill it with the next 10 MB of its associated 100 MB sorted chunk until no more data from the chunk is available. __This is the key step that makes external merge sort work externally__ -- because the merge algorithm only makes one pass sequentially through each of the chunks, each chunk does not have to be loaded completely; rather, sequential parts of the chunk can be loaded as needed.

### Similar Question

[link](http://www.glassdoor.com/Interview/Sort-a-million-32-bit-integers-using-only-2MB-of-RAM-QTN_120936.htm)

> [Google] Sort a million 32 bit integers using only 2MB of RAM.

1 million integers = 4MB which is > 2MB RAM.

Solution: external sort - divide and conquer

1. read half the list into 2MB ram and sort using quicksort (quicksort uses logn space - however 0.5m integers is less than 2MB (2000kb v 2048kb) so this should be okay).
2. write sorted data to disk
3. repeat for next chunk
4. merging results: we need an output buffer. lets say this is 1MB. then we read 512KB from each of your chunks into input buffers. we then perform a 2-way merge of the data. when an input buffer becomes empty we can pull in the remainder of the chunk.
5. when the output buffer is full we write this to disk.
6. when the process completes we are left with 2x 1MB files sorted in the correct order.
