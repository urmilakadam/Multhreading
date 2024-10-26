# Multithreading in Java

This repository demonstrates the use of multithreading in Java, focusing on various methods for creating and managing threads using the `ExecutorService` interface and inter-thread communication techniques.

## Overview

Java's multithreading capabilities allow applications to perform multiple operations concurrently, improving performance and responsiveness. This repository provides practical examples of how to implement multithreading using the `ExecutorService`, which abstracts thread management and simplifies task execution.

### Key Features

#### Thread Creation Methods
1. **Single Thread Executor**:
   - The `newSingleThreadExecutor()` method creates an executor that uses a single worker thread to execute tasks. This ensures that tasks are executed sequentially, preserving the order of execution.
   - Example:
     ```java
     ExecutorService executorService = Executors.newSingleThreadExecutor();
     executorService.execute(() -> {
         System.out.println("Task executed in single thread executor.");
     });
     ```

2. **Fixed Thread Pool**:
   - The `newFixedThreadPool(int nThreads)` method creates a pool of fixed-size threads. If all threads are busy, additional tasks are queued until a thread becomes available, allowing efficient use of system resources.
   - Example:
     ```java
     ExecutorService executorService = Executors.newFixedThreadPool(10);
     executorService.submit(() -> {
         System.out.println("Task executed in fixed thread pool.");
     });
     ```

3. **Scheduled Thread Pool**:
   - The `newScheduledThreadPool(int corePoolSize)` method allows for the scheduling of tasks with a specified delay or periodic execution. This is useful for tasks that need to run at regular intervals.
   - Example:
     ```java
     ScheduledExecutorService scheduledExecutorService = Executors.newScheduledThreadPool(10);
     scheduledExecutorService.scheduleAtFixedRate(() -> {
         System.out.println("Periodic task executed.");
     }, 0, 1, TimeUnit.SECONDS);
     ```

#### Task Execution
- Tasks can be submitted for execution using `execute()` or `submit()`. The `submit()` method returns a `Future` object that can be used to check if the task has completed and to retrieve its result.
  ```java
  Future<?> future = executorService.submit(() -> {
      // Task implementation
      return "Task result";
  });
  try {
      System.out.println(future.get()); // Returns the task result
  } catch (InterruptedException | ExecutionException e) {
      e.printStackTrace();
  }

#### Inter-thread Communication
Java provides several methods for inter-thread communication, which are essential for coordinating actions between multiple threads:

- wait(): Causes the current thread to wait until another thread calls notify() or notifyAll().
- notify(): Wakes up a single thread that is waiting on the object's monitor.
- notifyAll(): Wakes up all threads that are waiting on the object's monitor.
