* Process-based Parallelism: Unlike multithreading, which is limited by the GIL,
     multiprocessing spawns separate Python instances (one per core). This allows for
     true parallel execution, providing significant speedups for compute-intensive
     operations.
   * The `Pool` and `Process` Objects: The chapter introduces the Pool object as the
     primary way to manage a collection of worker processes. It covers how to map
     functions over data sets efficiently and discusses optimal pool sizing (usually
     matching the number of physical or logical CPU cores).
   * Interprocess Communication (IPC): Since processes do not share memory like threads
     do, the chapter details various ways to pass data between workers:
       * Queues and Pipes: For simple message passing.
       * Shared Memory: Using Value and Array for primitive types.
       * Managers: Using multiprocessing.Manager() to share more complex Python objects
         like lists and dictionaries.
   * Managing Large Datasets: For scientific computing, it explores techniques like
     using NumPy with mmap (memory-mapped files) to allow multiple processes to access
     large arrays without duplicating them in RAM.
   * Simplified Parallelism with Joblib: The authors recommend Joblib as a higher-level
     alternative for scientific tasks, highlighting its ability to cache results and
     provide a cleaner syntax for parallel loops.
   * "Embarrassingly Parallel" Problems: A central theme is identifying tasks that
     require little to no communication between processes, as these yield the best
     performance gains with minimal complexity.


  The chapter emphasizes that while multiprocessing is powerful, it carries overhead for
  process creation and data serialization (pickling). Therefore, the goal should be to
  maximize the amount of work done per process relative to the cost of communication.