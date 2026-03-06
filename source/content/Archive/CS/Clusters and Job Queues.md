The core message is that while clusters offer immense power, they introduce significant
complexity and should only be used after optimizing code on a single machine.


  1. When to Move to a Cluster
  The authors define a cluster as a group of computers working together and suggest
  scaling out only when:
   * Resource Limits: You’ve reached the CPU or memory limits of a single machine.
   * High Availability: You need reliability and redundancy for production systems.
   * Data Volume: Your data is too large to fit on one disk or in one machine's RAM.


  2. Key Technologies and Tools
  The chapter explores three primary ways to implement clustering in Python:
   * IPython Parallel (`ipyparallel`): Best for research and interactive work. It uses a
     "Hub and Spoke" model with ZeroMQ, allowing you to easily push/pull data and run
     functions asynchronously across remote engines.
   * Dask: Focused on scaling data science workloads (NumPy, Pandas, Scikit-Learn). It
     provides high-level abstractions that mimic familiar APIs but executes them across
     a distributed task scheduler.
   * NSQ (Job Queues): Recommended for robust production systems. Unlike interactive
     tools, NSQ is a message-passing queue that ensures "at-least-once" delivery, making
     it ideal for independent tasks processed by a pool of workers.


  3. Infrastructure and Deployment
   * Docker: The authors emphasize Docker as critical for ensuring identical
     environments across all nodes, eliminating "it works on my machine" bugs and
     simplifying dependency management.
   * Lessons from Failure: The chapter cites high-profile cases like Knight Capital and
     Skype to warn about the risks of poorly managed clusters, emphasizing simplicity,
     monitoring, and robust deployment.


  4. Practical "Avoid the Pain" Strategy
  The chapter concludes with these best practices:
   5. Optimize locally first: Use Cython, Numba, or multiprocessing before going
      distributed.
   6. Minimize data movement: Moving data between machines is often the biggest
      bottleneck; keep computation close to the data.
   7. Expect failure: Design your system to handle nodes going offline or tasks timing
      out.
   8. Use mature tools: Don't build your own cluster management; use established
      libraries like Dask or Celery.