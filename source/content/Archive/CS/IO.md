1. The Core Problem: Waiting for I/O
  I/O-bound tasks (like network requests or database queries) spend most of their time
  waiting for external responses. In a traditional "serial" program, the CPU sits idle
  during this wait. Asynchronous programming allows the CPU to switch to other tasks
  while waiting for I/O to complete, effectively "hiding" the latency.


  2. The Mechanism: Event Loops and Coroutines
   * Event Loop: A central coordinator that manages all pending tasks. It keeps track of
     which tasks are waiting for I/O and which are ready to resume.
   * Coroutines (`async def`): Functions that can be paused and resumed. When a
     coroutine hits an await statement, it yields control back to the event loop.
   * Cooperative Multitasking: Unlike threads (where the OS forces switches), coroutines
     must explicitly yield control. If a coroutine never awaits, it will block the
     entire program.


  3. Key Libraries
   * `asyncio` (Standard Library): Provides the foundational infrastructure for event
     loops and task management. It is lower-level and powerful.
   * `aiohttp`: The most popular library for asynchronous HTTP clients and servers. It
     allows for high-concurrency scraping and API calls. In the authors' tests, it was
     slightly faster than other methods due to its efficient coroutine resumption.
   * `gevent`: An alternative that uses "monkey patching" to make standard synchronous
     libraries asynchronous. It is useful for legacy projects but less explicit than
     asyncio.
   * `tornado`: A mature framework originally from Facebook, now fully compatible with
     asyncio and optimized for high-performance web applications.


  4. Handling Mixed CPU-I/O Workloads
  A major challenge is when a program needs to do both heavy calculation and I/O.
   * The Blocking Problem: CPU-bound code doesn't naturally await. To prevent it from
     "starving" I/O tasks, you must manually yield control using await asyncio.sleep(0).
   * Rule of Thumb: Insert a "zero-second sleep" in long loops every 50-100ms. This
     allows the event loop to process pending network responses or handle new incoming
     requests.
   * Full Async Solution: By interleaving CPU work with sleep(0) and queuing I/O tasks
     (via asyncio.create_task), the authors achieved a 7.3x speedup over serial code, as
     the I/O occurred in the background during CPU processing.


  5. Performance Tips
   * Semaphores: When making thousands of requests, use asyncio.Semaphore to limit
     concurrent connections. This prevents overwhelming the server or hitting OS file
     descriptor limits.
   * Connection Caching: Use persistent sessions (like aiohttp.ClientSession) to reuse
     TCP connections, significantly reducing the overhead of repeated requests to the
     same server.


  Core Takeaway: Use asyncio and aiohttp to maximize throughput for network-heavy
  applications. To keep your app responsive, ensure CPU-bound segments occasionally
  yield back to the event loop using await asyncio.sleep(0), allowing I/O operations to
  overlap with calculations.