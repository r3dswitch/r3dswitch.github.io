#### **1. Basic Idea**  
To virtualize the CPU, the OS allows multiple processes to share the CPU by running them in turns. This requires:  
- **Performance**: Minimizing overhead.  
- **Control**: Ensuring the OS retains control over processes.  

#### **2. Limited Direct Execution (LDE) Protocol**  
- **Direct Execution**: Programs run natively on the CPU for efficiency.  
- **Limitations**: The OS restricts process operations to maintain control.  

#### **3. Problem #1: Restricted Operations**  
- **User Mode vs. Kernel Mode**:  
  - **User Mode**: Processes run with restricted privileges (e.g., cannot perform I/O).  
  - **Kernel Mode**: The OS runs with full privileges.  
- **System Calls**:  
  - Processes request privileged operations via traps (e.g., `open()`, `read()`).  
  - The trap switches to kernel mode, executes the operation, and returns to user mode.  
- **Trap Table**:  
  - Initialized at boot to define safe entry points for system calls.  

#### **4. Problem #2: Switching Between Processes**  
- **Cooperative Approach**:  
  - Processes voluntarily yield control via system calls (e.g., `yield()`).  
  - Risk: A misbehaving process can monopolize the CPU.  
- **Non-Cooperative Approach**:  
  - **Timer Interrupts**: Hardware interrupts processes periodically, allowing the OS to schedule another process.  
- **Context Switching**:  
  - The OS saves the current process’s state (registers, stack) and restores another process’s state.  

#### **5. Concurrency Concerns**  
- Interrupts during system calls or handling interrupts require careful management (e.g., disabling interrupts temporarily).  

#### **6. Summary of Key Mechanisms**  
- **Dual-Mode Operation**: User/kernel mode separation.  
- **Traps & Trap Tables**: Controlled entry into the kernel.  
- **Timer Interrupts**: Ensure OS regains control.  
- **Context Switching**: Saves/restores process state for multitasking.  

This approach balances efficiency (direct execution) with control (hardware/OS cooperation).  

### **Homework (Measurement)**  
Measure:  
1. **System Call Cost**: Time a null system call (e.g., `read()` with 0 bytes) using `gettimeofday()` or `rdtsc`.  
2. **Context Switch Cost**: Use two processes communicating via pipes/sockets, bound to the same CPU (e.g., `sched_setaffinity()` on Linux).  

Tools like `lmbench` can help benchmark these operations.  

**Key Takeaway**: The OS combines hardware support (traps, interrupts) and software mechanisms (scheduling, context switches) to virtualize the CPU efficiently.