1. The Core Philosophy: Dropping Down to C
  Python is slow for tight loops because it is an interpreted, dynamic language. To get
  near-native speeds, you must convert "hot" sections of your code into C. The authors
  explore several ways to do this, ranging from fully automatic to manually managing
  memory.


  2. Cython: The Bridge to C
  Cython is a compiler that converts Python code (with optional C-like type annotations)
  into C code, which is then compiled into a machine-code module.
   * Pure Python Conversion: Simply compiling unmodified Python code with Cython can
     give a ~2x speedup by removing some interpreter overhead.
   * Static Type Annotations: By adding types (e.g., cdef int i), Cython can bypass
     Python's dynamic lookup entirely. For the Julia Set example, this reduced runtime
     from 8.3s to 0.5s.
   * NumPy Integration: Cython can use the Buffer Protocol (via memoryview) to access
     NumPy arrays directly in memory, avoiding the overhead of Python object
     dereferencing.


  3. Numba: Just-In-Time (JIT) Compilation
  Numba is often preferred for numerical code because it requires almost no code
  changes.
   * How it Works: It uses LLVM to compile Python functions to machine code at runtime.
   * Usage: You simply add a @jit decorator to your function. It is particularly
     effective for loops over NumPy arrays and can even target GPUs.


  4. PyPy: The Alternative Interpreter
  PyPy is a replacement for the standard CPython interpreter.
   * JIT Compiler: It features a tracing JIT compiler that optimizes code as it runs.
   * Performance: It can provide massive speedups for pure Python code without any
     manual changes.
   * Drawback: It historically struggled with NumPy compatibility (though this has
     improved) and cannot use C-extension modules as efficiently as CPython.


  5. Foreign Function Interfaces (FFI)
  When you already have existing C or Fortran libraries, you can call them from Python
  using:
   * `ctypes`: Part of the standard library. Flexible but requires manual "casting" of
     types and can be fragile if the C library changes.
   * `cffi`: A more modern and robust alternative to ctypes.
   * `f2py`: A specialized tool for wrapping Fortran code for use in NumPy.


  6. Parallelization with OpenMP
  Cython allows you to use OpenMP to parallelize loops across multiple CPU cores.
   * `prange`: By replacing range with prange and disabling the Global Interpreter Lock
     (GIL) using with nogil:, you can execute iterations in parallel.
   * Safety: This is only safe when operating on primitive types or buffers (like NumPy
     arrays); you cannot touch regular Python objects while the GIL is disabled.


  Core Takeaway: For the best performance, use Numba for simple numerical loops and
  Cython for complex logic where you need fine-grained control over types and memory.
  Compiling your code effectively turns Python into a high-level "glue" language that
  coordinates ultra-fast C-level kernels.