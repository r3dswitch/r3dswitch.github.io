1. Hash Tables: The Engine of $O(1)$ Performance
  Dictionaries and sets achieve constant-time $O(1)$ lookups and insertions by using
  hash tables.
   * Hashing: A key (like a string) is passed through a hash function to generate an
     integer. This integer is then "masked" to fit within the currently allocated
     memory, effectively turning the key into a list index.
   * Dictionaries vs. Sets: They are almost identical under the hood. The main
     difference is that a dictionary stores a key-value pair, while a set only stores
     unique keys.


  2. Collisions and Probing
  Because multiple keys can hash to the same index (a collision), Python must resolve
  these conflicts:
   * Probing: If a bucket is already occupied, Python uses a "probing" algorithm (a
     linear function of the hash) to find the next available slot.
   * Deletion: When an item is deleted, Python doesn't leave a NULL. Instead, it writes
     a "dummy" sentinel value. This ensures that probing for other keys that might have
     collided at that index doesn't stop prematurely.


  3. Memory Optimization (Compact Dictionaries)
  Since Python 3.6/3.7, dictionaries are compact:
   * They store the actual data (hash, key, value) in a dense array and use a separate,
     sparse "indices" array to map hashes to that dense array.
   * Memory Savings: This reduces memory usage by 30–95% compared to older versions.
   * Ordering: A side effect of this optimization is that dictionaries now guarantee
     insertion order.


  4. Namespaces: Python’s Internal Dictionary
  Python's core is powered by dictionaries. Every time you look up a variable or a
  function, you are performing a dictionary lookup:
   * Namespace Hierarchy: Python searches in this order: Local $\rightarrow$ Non-local
     $\rightarrow$ Global $\rightarrow$ Built-in.
   * Performance Tip: Looking up a global variable or a function in a module (e.g.,
     math.sin) is slower than looking up a local variable. For tight loops, assigning a
     global function to a local variable (e.g., sin = math.sin inside the function) can
     provide a noticeable speedup by bypassing the dictionary lookup on every iteration.


  5. Performance Costs & Trade-offs
   * Memory Overhead: Dictionaries and sets are memory-hungry compared to lists because
     they must maintain a sparse hash table to keep collision rates low.
   * Hashing Speed: The speed of $O(1)$ operations depends on the speed of the __hash__
     function. If hashing a key is expensive, the dictionary itself will feel slow.
   * Over Lists: For unique element checks, a set provides an $O(n)$ solution compared
     to a list's $O(n^2)$ approach, often yielding 250x-500x speedups for large
     datasets.


  Core Takeaway: Use dictionaries and sets when you need fast, index-independent lookups
  and can afford the memory overhead. To maximize speed in high-performance loops,
  "localize" your global lookups to minimize repeated hash table traversals in Python's
  namespaces.