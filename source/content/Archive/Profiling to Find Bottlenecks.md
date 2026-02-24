1. The Profiling Philosophy
  The chapter emphasizes that you should never guess where a bottleneck is. Profiling
  provides empirical evidence that allows you to spend your time optimizing the 10% of
  code that actually causes 90% of the slowdown. The authors use a "Julia Set"
  calculation as a running example of a CPU-bound problem to demonstrate these tools.


  2. Basic Timing Tools
   * Unix `time` command: A simple way to measure the total "Wall clock" time, "User"
     time (CPU time), and "System" time (kernel overhead).
   * `timeit` module: Ideal for micro-benchmarking small snippets of code (e.g.,
     comparing list vs generator performance).
   * Custom Decorators: Using time.time() inside a decorator to wrap functions and print
     execution times for specific blocks.


  3. Systematic Profilers
   * `cProfile` (Built-in): The standard tool for function-level profiling. It provides
     a table showing the number of calls (ncalls), total time spent in a function
     (tottime), and cumulative time (cumtime).
       * Caveat: It adds overhead and doesn't show which lines inside a function are
         slow.
   * `line_profiler`: A critical tool that requires a @profile decorator on functions.
     It provides a line-by-line breakdown of execution time, making it the authors'
     favorite for deep-dive optimization.


  4. Specialized & Visual Tools
   * `PySpy`: A sampling profiler that can introspect an already-running process without
     changing the code. It has very low overhead and can generate Flame Graphs.
   * `SnakeViz`: A web-based visualizer for cProfile data. It uses "sunburst" or
     "icicle" diagrams where box width represents time, making it easy to see which call
     stacks are dominant.
   * `memory_profiler`: Similar to line_profiler but measures RAM usage over time. It is
     useful for finding memory leaks or inefficient object creation but is significantly
     slower than CPU profilers.


  5. Inspecting Bytecode (dis module)
  The authors introduce the dis module to disassemble Python code into the bytecode run
  by the CPython virtual machine. This helps programmers understand:
   * The "hidden" costs of Python's stack-based operations.
   * Why certain constructs (like local variables vs. global lookups) are faster.
   * How to build a mental model for what tools like Cython or Numba will eventually
     optimize.


  Core Takeaway: Effective profiling follows a hierarchy: start with coarse-grained
  tools (like time or cProfile) to find the "hot" functions, then use fine-grained tools
  (line_profiler) to identify the exact lines to rewrite or compile.