This document is an interlude chapter from an operating systems textbook that explains the **UNIX Process API** - specifically how to create and control processes using system calls.

## Key Concepts Covered

**The Three Core System Calls:**

- **`fork()`** - Creates a new process that's an almost exact copy of the calling process. The parent receives the child's PID as return value, while the child receives 0
- **`wait()`** - Allows a parent process to wait for its child to complete execution, making output deterministic
- **`exec()`** - Replaces the current process with a different program entirely, loading new code and data

## How UNIX Shells Work

The separation of `fork()` and `exec()` enables powerful shell features:

1. Shell calls `fork()` to create a child process
2. Before calling `exec()`, the child can modify its environment (like redirecting output to files)
3. Child calls `exec()` to run the desired program
4. Parent calls `wait()` to wait for completion

This design enables features like:

- **I/O redirection** (`command > file`)
- **Pipes** (`command1 | command2`)
- **Background processes**

## Process Control & Security

- **Signals** provide inter-process communication (Ctrl-C sends SIGINT, Ctrl-Z sends SIGTSTP)
- **Users** can only control their own processes for security
- **Superuser (root)** has system-wide process control abilities

## Practical Tools

The chapter mentions useful command-line tools like `ps`, `top`, `kill`, and `killall` for process monitoring and management.

The document concludes with homework exercises involving both simulation and hands-on coding to reinforce understanding of these process management concepts. The overall message is that while the UNIX process API might seem strange initially, the `fork()`/`exec()` combination provides a simple yet powerful foundation for process creation and control.