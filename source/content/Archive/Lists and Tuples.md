1. Underlying Architecture
  Both lists and tuples are implemented as arrays—flat lists of data with intrinsic
  ordering.
   * Memory Layout: Python stores data in "consecutive buckets" in system memory. These
     buckets store references (pointers) to the actual objects, allowing them to hold
     mixed types.
   * $O(1)$ Lookup: Because data is stored in consecutive buckets, looking up an element
     by index is a simple calculation ($M + i$, where $M$ is the start address) and
     takes constant time regardless of the array's size.


  2. Lists vs. Tuples: The Performance Trade-off
  The primary difference lies in mutability and how Python manages their memory:
   * Lists (Dynamic Arrays): Mutable and resizable. To make append operations efficient,
     Python overallocates memory. For example, if you create a list of size 4, Python
     might actually allocate 8 buckets. This avoids a full memory reallocation on every
     append but results in higher memory overhead.
   * Tuples (Static Arrays): Immutable and fixed-size.
       * Memory Efficiency: They use exactly the amount of memory needed.
       * Caching: Python caches small tuples. When a tuple is no longer needed, its
         memory isn't always returned to the kernel immediately but is kept in a "free
         list" for reuse. This makes creating new tuples faster than creating new lists.


  3. Search Performance
  Searching for a value (not an index) in an unordered list/tuple is a Linear Search
  ($O(n)$). To optimize this:
   * Sorting: Python uses Timsort ($O(n \log n)$ worst case, $O(n)$ best case), a hybrid
     of insertion and merge sort.
   * Binary Search ($O(\log n)$): Once sorted, you can use binary search to find
     elements or the `bisect` module to maintain a sorted list while inserting new
     elements.
   * Recommendation: If you frequently search a large dataset, a dictionary ($O(1)$) is
     faster, but the $O(n)$ cost of converting a list to a dictionary may only be worth
     it if you perform many lookups.


  4. Practical Guidelines
   * Use Tuples for: Unchanging data ("multiple properties of one thing"). They are
     lighter on memory and faster to instantiate.
   * Use Lists for: Collections of disparate objects that grow or change over time.
   * Generic vs. Specific: The authors note that "generic code will be much slower than
     code specifically designed to solve a particular problem." If your data is all of
     the same primitive type (e.g., all integers), consider using the array module or
     NumPy for even better performance.


  Core Takeaway: Pick the right structure based on whether your data is static or
  dynamic. If using lists, be mindful of the "hidden" memory cost of overallocation and
  the $O(n)$ cost of linear searches.