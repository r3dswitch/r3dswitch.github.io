Core Philosophy
   * Performance via Cache: Reducing RAM usage keeps data closer to the CPU (L1/L2/L3        caches), resulting in significant speedups compared to accessing main memory (RAM).
   * Object Overhead: Standard Python objects are "heavy" because they store extensive       metadata. High-performance code requires switching to leaner, specialized data
     structures.

  ---

  Key Techniques and Strategies


  1. Specialized Data Structures
   * __slots__: By defining __slots__ in a class, you prevent the creation of a
     per-instance __dict__. This can reduce memory usage by 40–70% when creating
     millions of objects.
   * array.array: For large collections of primitive numbers (integers, floats), the
     built-in array module is much more compact than a standard Python list because it
     stores data in a contiguous C-style array.
   * NumPy Arrays: Use NumPy for numerical data and explicitly set the bit-depth (e.g.,
     float32 instead of the default float64) to halve memory consumption immediately.


  2. Lazy Evaluation
   * Generators and Iterators: Use yield and generator expressions to process data one
     item at a time. This keeps the memory footprint constant (O(1)) regardless of the
     total dataset size.
   * Itertools: Leverage the itertools library for efficient, memory-friendly data
     manipulation.


  3. Efficient Text and String Storage
   * Tries and DAWGs: For storing millions of strings (like dictionaries or URLs), use a
     Trie or Directed Acyclic Word Graph (DAWG). These structures compress common
     prefixes and suffixes, often reducing memory usage by 90% or more.
   * Unicode vs. Bytes: Python 3 strings are Unicode. If your data is purely ASCII,
     storing it as bytes objects can save significant space.


  4. Handling Large Datasets (Out-of-Core)
   * mmap (Memory Mapping): Use memory-mapped files to treat data on disk as if it were
     in RAM. The operating system handles loading only the necessary chunks into memory.
   * Sparse Matrices: Use scipy.sparse for datasets where most values are zero, which
     avoids storing empty cells.
   * Vaex & Dask: For data that physically cannot fit in RAM, these libraries use lazy
     evaluation and memory mapping to process "Big Data" on a single machine.


  5. Probabilistic Data Structures
   * Bloom Filters: Used to check if an item might be in a set. They use a fraction of
     the memory of a standard set by allowing a tiny, tunable probability of false
     positives.
   * HyperLogLog: An algorithm for counting unique elements (cardinality) in massive
     streams using almost no RAM compared to a standard set.

  ---


  Recommended Profiling Tools
   * memory_profiler: For line-by-line RAM usage analysis.
   * Pympler: For deep inspection of how much memory complex Python objects are truly
     consuming.
   * sys.getsizeof(): For a quick check of an object's size (though it does not recurse
     into container contents).