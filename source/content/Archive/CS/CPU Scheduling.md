### **Scheduling: Introduction - Summary Notes**

#### **Key Concepts**
1. **Scheduling Policies**: High-level strategies used by the OS to manage process execution.
2. **Workload Assumptions** (Initial Simplifications):
   - All jobs run for the same time.
   - All jobs arrive simultaneously.
   - Jobs run to completion without interruption.
   - No I/O operations.
   - Job runtimes are known (unrealistic).

#### **Scheduling Metrics**
- **Turnaround Time**: \( T_{\text{turnaround}} = T_{\text{completion}} - T_{\text{arrival}} \).
- **Response Time**: \( T_{\text{response}} = T_{\text{firstrun}} - T_{\text{arrival}} \).
- Trade-off: Optimizing one metric often degrades the other.

#### **Scheduling Algorithms**
1. **First-In, First-Out (FIFO)**:
   - Simple but suffers from the **convoy effect** (long jobs delay short ones).
   - Poor turnaround time if job lengths vary.

2. **Shortest Job First (SJF)**:
   - Optimal for **turnaround time** if all jobs arrive at the same time.
   - Non-preemptive; struggles with late-arriving short jobs.

3. **Shortest Time-to-Completion First (STCF)**:
   - Preemptive version of SJF.
   - Better for turnaround time when jobs arrive at different times.

4. **Round Robin (RR)**:
   - Uses **time slices** to alternate jobs.
   - Excellent for **response time** but poor for turnaround time.
   - Trade-off: Smaller time slices improve response time but increase context-switching overhead.

#### **Incorporating I/O**
- Treat CPU bursts as separate jobs.
- Overlap CPU and I/O operations to improve utilization.
- Example: While a process waits for I/O, the scheduler runs another process.

#### **Challenges**
- **No Oracle**: Real schedulers don’t know job lengths in advance.
- **Future Solution**: Multi-level feedback queue (uses past behavior to predict future needs).

#### **Key Takeaways**
- **SJF/STCF**: Best for turnaround time.
- **RR**: Best for response time.
- **Trade-offs**: Cannot optimize both metrics simultaneously.
- **I/O Handling**: Overlapping CPU and I/O improves efficiency.