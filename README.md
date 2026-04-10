# Lab 07: Round Robin Scheduling Simulator

#### Learning Objectives

* Understand time quantum and preemptive scheduling concepts
* Implement Round Robin scheduling algorithm in Java
* Analyze the impact of different time quantum values on performance
* Calculate and compare scheduling metrics for different configurations

#### Prerequisites

* Basic Java programming knowledge
* Understanding of loops and ArrayLists
* Familiarity with the Process class structure

#### Introduction

Round Robin scheduling is the heartbeat of time-sharing systems. Every modern operating system uses some form of it to
ensure fair CPU allocation. When you switch between apps on your phone, when multiple users connect to a server, when
your computer runs dozens of background processes while you work - Round Robin scheduling makes it all feel smooth and
responsive.

The genius of Round Robin is its simplicity. Each process gets a small slice of CPU time called a time quantum. When the
quantum expires, the process moves to the back of the line, and the next process gets its turn. No process monopolizes
the CPU. Everyone gets a fair shot.

But here's the catch: the size of the time quantum changes everything. Too small, and the system wastes time constantly
switching between processes. Too large, and it behaves like basic FCFS, losing its responsiveness advantage. Finding the
right balance is key.

#### What You'll Implement

Complete 3 TODO tasks in one file:

* TODO 1: Implement the scheduling loop that cycles through processes
* TODO 2: Handle time quantum execution and process completion
* TODO 3: Calculate and display performance metrics

The Process class and main method are fully provided.

#### Lab File Structure

**RoundRobinLab.java** - The only file you need to complete

* Process class - Fully provided (holds process data)
* `scheduleRoundRobin()` method - TODO 1, 2, 3 (you implement core logic)
* `calculateMetrics()` method - Fully provided (computes averages)
* `main()` method - Fully provided (runs simulations)

#### Project Setup

1. Download RoundRobinLab.java
2. Complete the 3 TODOs
3. Compile: `javac RoundRobinLab.java`
4. Run: `java RoundRobinLab`

#### Understanding Round Robin

Round Robin maintains a ready queue of processes. The scheduler picks the first process, lets it run for one time
quantum, then moves it to the back of the queue if it's not finished. This continues until all processes complete.

Think of it like a rotating card game. Each player gets to play one card per turn. If they still have cards, they wait
for their next turn. Eventually, everyone finishes their hand.

**Key Concepts:**

* **Time Quantum**: The fixed time slice each process gets (example: 3ms)
* **Ready Queue**: List of processes waiting for CPU time
* **Remaining Time**: How much burst time a process still needs
* **Context Switch**: Moving from one process to another (happens every quantum)

#### The Algorithm

Here's how Round Robin works:

1. Start with all processes in the ready queue
2. Pick the first process from the queue
3. Execute it for one time quantum (or until it finishes)
4. If the process isn't done, move it to the back of the queue
5. Repeat until the queue is empty

**Example with Time Quantum = 3:**

```
Processes: P1(burst=7), P2(burst=4), P3(burst=2)

Time 0-3:   P1 runs for 3ms, remaining=4, moves to back
Time 3-6:   P2 runs for 3ms, remaining=1, moves to back  
Time 6-8:   P3 runs for 2ms, remaining=0, DONE
Time 8-11:  P1 runs for 3ms, remaining=1, moves to back
Time 11-12: P2 runs for 1ms, remaining=0, DONE
Time 12-13: P1 runs for 1ms, remaining=0, DONE
```

#### Expected Output

```
========================================
Round Robin Scheduling Simulator
========================================

Time Quantum: 3ms
----------------------------------------
Process | Arrival | Burst | Completion | Turnaround | Waiting
   1    |    0    |   7   |     13     |     13     |    6
   2    |    0    |   4   |     12     |     12     |    8
   3    |    0    |   2   |      8     |      8     |    6

Average Turnaround Time: 11.00ms
Average Waiting Time: 6.67ms
========================================


========================================
Round Robin Scheduling Simulator
========================================

Time Quantum: 5ms
----------------------------------------
Process | Arrival | Burst | Completion | Turnaround | Waiting
   1    |    0    |   7   |     17     |     17     |   10
   2    |    0    |   4   |      9     |      9     |    5
   3    |    0    |   2   |      2     |      2     |    0

Average Turnaround Time: 9.33ms
Average Waiting Time: 5.00ms
========================================
```

#### Code Template

```java
import java.util.*;

public class RoundRobinLab {

    static class Process {
        int id;
        int arrivalTime;
        int burstTime;
        int remainingTime;
        int completionTime;
        int turnaroundTime;
        int waitingTime;

        public Process(int id, int arrivalTime, int burstTime) {
            this.id = id;
            this.arrivalTime = arrivalTime;
            this.burstTime = burstTime;
            this.remainingTime = burstTime;
        }
    }

    /**
     * TODO 1, 2, 3: Implement Round Robin Scheduling
     *
     * This method simulates Round Robin scheduling with the given time quantum.
     *
     * TODO 1: Create the ready queue and scheduling loop
     *   - Create an ArrayList to hold the ready queue
     *   - Add all processes to the ready queue initially
     *   - Create a loop that continues while the queue is not empty
     *
     * TODO 2: Process execution logic
     *   - Remove the first process from the queue
     *   - Calculate how much time this process will run (minimum of quantum and remaining time)
     *   - Update currentTime by adding the execution time
     *   - Subtract execution time from the process's remainingTime
     *   - If remainingTime > 0, add process back to the end of the queue
     *   - If remainingTime == 0, set the process completionTime to currentTime
     *
     * TODO 3: Calculate metrics after all processes complete
     *   - Loop through all processes
     *   - For each process: turnaroundTime = completionTime - arrivalTime
     *   - For each process: waitingTime = turnaroundTime - burstTime
     */
    public static void scheduleRoundRobin(List<Process> processes, int timeQuantum) {
        int currentTime = 0;

        // TODO 1: Create ready queue and add all processes


        // TODO 2: Scheduling loop
        // while (queue is not empty) {
        //     - Remove first process
        //     - Calculate execution time (min of quantum and remaining time)
        //     - Update current time
        //     - Decrease remaining time
        //     - If not done, add back to queue
        //     - If done, set completion time
        // }


        // TODO 3: Calculate turnaround and waiting times
        // for each process:
        //     turnaroundTime = completionTime - arrivalTime
        //     waitingTime = turnaroundTime - burstTime

    }

    /**
     * Calculate and display metrics (FULLY PROVIDED)
     */
    public static void calculateMetrics(List<Process> processes, int timeQuantum) {
        System.out.println("========================================");
        System.out.println("Round Robin Scheduling Simulator");
        System.out.println("========================================\n");
        System.out.println("Time Quantum: " + timeQuantum + "ms");
        System.out.println("----------------------------------------");
        System.out.println("Process | Arrival | Burst | Completion | Turnaround | Waiting");

        double totalTurnaround = 0;
        double totalWaiting = 0;

        for (Process p : processes) {
            System.out.printf("   %d    |    %d    |   %d   |     %d     |     %d     |    %d\n",
                    p.id, p.arrivalTime, p.burstTime, p.completionTime,
                    p.turnaroundTime, p.waitingTime);
            totalTurnaround += p.turnaroundTime;
            totalWaiting += p.waitingTime;
        }

        System.out.println();
        System.out.printf("Average Turnaround Time: %.2fms\n", totalTurnaround / processes.size());
        System.out.printf("Average Waiting Time: %.2fms\n", totalWaiting / processes.size());
        System.out.println("========================================\n\n");
    }

    /**
     * Main method (FULLY PROVIDED)
     */
    public static void main(String[] args) {
        List<Process> processes1 = new ArrayList<>();
        processes1.add(new Process(1, 0, 7));
        processes1.add(new Process(2, 0, 4));
        processes1.add(new Process(3, 0, 2));

        scheduleRoundRobin(processes1, 3);
        calculateMetrics(processes1, 3);

        List<Process> processes2 = new ArrayList<>();
        processes2.add(new Process(1, 0, 7));
        processes2.add(new Process(2, 0, 4));
        processes2.add(new Process(3, 0, 2));

        scheduleRoundRobin(processes2, 5);
        calculateMetrics(processes2, 5);
    }
}
```

#### Implementation Guide

**TODO 1: Create Ready Queue and Main Loop**

```java
// Create the ready queue
ArrayList<Process> readyQueue = new ArrayList<>();

// Add all processes to the queue
for (Process p : processes) {
    readyQueue.add(p);
}

// Main scheduling loop
while (!readyQueue.isEmpty()) {
    // TODO 2 code goes here
}
```

**TODO 2: Process Execution Logic**

```java
// Remove first process from queue
Process current=readyQueue.remove(0);

// Calculate execution time (quantum or remaining time, whichever is smaller)
int executeTime=Math.min(timeQuantum,current.remainingTime);

// Advance the clock
currentTime+=executeTime;

// Reduce remaining time
current.remainingTime-=executeTime;

// Check if process is done
if(current.remainingTime>0){
    // Not done, add back to queue
    readyQueue.add(current);
}else{
    // Done, record completion time
    current.completionTime=currentTime;
}
```

**TODO 3: Calculate Metrics**

```java
// Calculate turnaround and waiting times
for(Process p:processes){
    p.turnaroundTime=p.completionTime-p.arrivalTime;
    p.waitingTime=p.turnaroundTime-p.burstTime;
}
```

#### Common Mistakes to Avoid

**Using the Wrong Time Value**

Don't always execute for the full quantum. Use the minimum of the quantum and remaining time:

```java
// WRONG
currentTime+=timeQuantum;

// CORRECT
int executeTime=Math.min(timeQuantum,current.remainingTime);
currentTime+=executeTime;
```

**Forgetting to Add Process Back to Queue**

If a process isn't finished, it must return to the queue:

```java
if(current.remainingTime>0){
    readyQueue.add(current);  // Don't forget this!
}
```

**Calculating Metrics Too Early**

Wait until all processes complete before calculating turnaround and waiting times.

#### Analysis Questions

After completing the lab, answer these questions:

1. Compare the results with time quantum 3 and time quantum 5. Which quantum gave better average waiting time? Why?

2. What would happen if the time quantum was 1ms? Would the system be more or less efficient?

3. What would happen if the time quantum was 20ms (larger than any process burst time)? How would Round Robin behave
   then?

4. In the simulation with quantum 3, how many context switches occurred? Count each time a process was removed from the
   queue.

5. Why does Round Robin prevent the convoy effect that occurs in FCFS scheduling?

#### What You're Really Learning

The numbers and calculations are just mechanics. The real lesson is understanding the trade-off between responsiveness
and overhead.

Small time quantum means every process gets frequent turns. Great for responsiveness. But each context switch has
overhead. Too many switches and you waste time switching instead of doing real work.

Large time quantum means fewer switches and less overhead. But processes wait longer for their next turn. Push it too
far and you've basically got FCFS.

This balance exists everywhere in computing. Network packet sizes. Database batch operations. UI event processing. The
principle is always the same: find the sweet spot between granularity and overhead.

Round Robin is used in every time-sharing system because it guarantees fairness and prevents starvation. No process gets
stuck waiting forever. Everyone gets a turn. That guarantee is worth the overhead in most interactive systems.

#### Compilation and Execution

```bash
javac RoundRobinLab.java
java RoundRobinLab
```

#### Submission Requirements

After completing your work:

```bash
git add .
git commit -m "completed lab XX - round robin scheduling"
git push origin main
```

Include:

* Completed scheduleRoundRobin method with all three TODOs
* Screenshot showing successful execution with both time quantums
* Answers to the 5 analysis questions
* Verify metrics are calculated correctly for both simulations