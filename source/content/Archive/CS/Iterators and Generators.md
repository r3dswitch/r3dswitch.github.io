1. The Core Concept: Lazy Evaluation
  Generators and iterators allow for lazy evaluation, meaning data is produced only when
  requested rather than being precomputed and stored in memory.
   * Memory Efficiency: A generator that calculates 100 million Fibonacci numbers uses
     the same amount of memory as one that calculates 10, because it only ever holds the
     current value and the state necessary to calculate the next one.
   * CPU Efficiency: By avoiding massive allocations (like list.append overhead) and
     immediate full-sequence processing, generators can often be twice as fast as
     list-based counterparts for large datasets.


  2. Iterators vs. Generators
   * Iterators: Objects that implement the __next__ and __iter__ methods. They are the
     mechanism behind Python's for loops.
   * Generators: A simpler way to create iterators using the yield keyword. A function
     with yield returns a generator object that can be "polled" for values until it hits
     a StopIteration exception.
   * Built-in Support: Many Python functions like range, map, zip, filter, and enumerate
     are implemented as generators to minimize memory footprint.


  3. Workflow: Generation vs. Transformation
  The authors advocate for a paradigm shift in how you structure code:
   * Generation: Use generators/iterators to produce data (e.g., reading lines from a
     massive file).
   * Transformation: Use functions to act on that data one item at a time.
   * Benefit: This separation makes code more modular, easier to debug, and ready for
     parallelization (e.g., using multiprocessing's map function).


  4. Advanced Tooling with itertools
  The standard library itertools module provides highly optimized "building blocks" for
  complex generator workflows:
   * `islice`: Slice an infinite generator.
   * `chain`: Connect multiple generators into one sequence.
   * `takewhile`: Stop a generator based on a condition.
   * `cycle`: Repeat a finite sequence infinitely.


  5. The Trade-offs
   * Single-Pass Only: Generators are "one-time use." Once you consume a value, it's
     gone. If you need to reference the same data multiple times, a list
     (precomputation) might be faster despite the memory cost.
   * State Management: Converting a complex algorithm to a generator requires carefully
     managing the state between yield calls.
   * Common Mistake: Wrapping a generator in len() or list() immediately consumes it and
     allocates all that memory, negating the generator's benefits. Use sum(1 for x in
     gen) for counting instead.


  Core Takeaway: Use generators by default for large or infinite datasets. They shift
  the burden from RAM to CPU, enabling "online" or "single-pass" algorithms that can
  process data far larger than your available memory.