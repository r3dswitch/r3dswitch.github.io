1. The Bottleneck: Memory Fragmentation
  The authors use a "Diffusion Equation" (a grid-based simulation) to show why pure
  Python is slow for math.
   * The Problem: Python lists store pointers to objects scattered in memory. This leads
     to cache misses, where the CPU wastes time waiting for data from RAM because it
     isn't in the fast L1/L2 caches.
   * The Result: In their tests, pure Python had over 50% cache misses, making it
     impossible for the CPU to use its advanced "pipelining" and "vectorization"
     features.


  2. Enter NumPy: Vectorization and Locality
  NumPy solves these problems by storing data in contiguous chunks of memory using
  low-level C types.
   * Vectorized Operations: Instead of explicit for loops in Python, you use "implied
     loops" (e.g., A + B). This allows NumPy to use specialized CPU instructions (like
     SIMD) to process multiple numbers in a single clock cycle.
   * Speed Gain: For a vector norm-square calculation, NumPy was found to be nearly 90x
     faster than pure Python.
   * Performance Insight: Using perf showed that NumPy reduced cache misses from 53% to
     20% and significantly lowered the total number of CPU instructions required.


  3. Memory Management: In-Place Operations
  A common trap with NumPy is the creation of temporary arrays.
   * Implicit Allocation: The operation res = A * B + C first creates a temporary array
     for A * B, then another for the sum. This wastes memory and time on allocations.
   * In-Place Solutions: Using operators like += or *= (e.g., A *= B, then A += C)
     modifies the data in its existing memory "bucket," avoiding the overhead of new
     allocations. This is crucial for large grids that push the limits of available RAM.


  4. Advanced Optimization with numexpr
  Even with NumPy, the CPU still has to make multiple passes over the data (one for
  multiplication, one for addition).
   * `numexpr`: This module compiles entire mathematical expressions into optimized
     kernels.
   * Cache Awareness: It breaks large arrays into "tiles" that fit perfectly into the
     CPU's L1/L2 caches, further reducing cache misses.
   * Multi-core Support: It can automatically parallelize calculations across multiple
     CPU cores using OpenMP.
   * When to Use: It is most effective for large datasets that exceed the CPU cache
     size. For small grids, the overhead of "compiling" the expression string can
     actually make it slower than standard NumPy.


  5. Specialized Tools: array module
  The built-in array module is mentioned as a middle ground: it provides contiguous
  memory storage like NumPy but lacks vectorization. Since it has to convert data to
  Python objects on every access, it can actually be slower than a regular list for
  mathematical loops. Its primary use is memory-efficient storage of primitive types,
  not high-speed calculation.


  Core Takeaway: To make math fast in Python, move your data into contiguous NumPy
  arrays and replace Python loops with vectorized operations. For very large problems,
  use in-place updates and numexpr to minimize memory allocation and maximize CPU cache
  hits.