## Strategy for Concurrency/parallelism
* [Threads](#threads)
* [Processes](#process)
* [Daemon Threads](#user-vs-daemon-thread)
* [Executor service](#executor-service)

## Strategy for avoiding race conditions
* [Synchronization - Structured lock](#synchronization)
* [Lock object - Unstructured lock](#unstructured-lock-and-lock-interface)

## Strategy for visibility
* [Volatile keyword](#volatile)

## Concepts - Lessons
* [Life cycle and thread states](#thread-life-cycle)
* [Sleeping, joining](#joining-threads)
* [Interrupting threads](#stopping-a-thread)
* [Scheduler](#scheduler)
* [Race conditions](#race-condition)
* [Liveness,Deadlock, Livelock, Starvation](#liveness-deadlock-livelocks-and-starvation)
* [Threadlocal](#threadlocal)
* [Semaphores](#semaphores)
* [Fork Join pool](#fork-join)
* Blocking Synchronous IO
* Non-blocking async IO
  * KQ
  * Epoll
  * IO completion ports for windows

## Common Patterns

## Common Pitfalls

### Threads
* A Thread is a single sequential flow of control within a program.
* Sequence of programmed instructions that can be managed independently.
* Allows the program to split into simultaneously running tasks.
* Thread is a unit of execution in a process
* Usually has a shared objective
* thread ends 
  * when the run method completes
  * an exception is thrown
  * interrupts

### Process
* Bunch of binary instructions loaded into memory
* Gets access to resources like memory
* Process needs resources to run
* Its own stack, heap and registers
* Resources is protected from other resources
* Does its thing
* Process can have single threads or spawn multiple threads

### Java application
* Single process (JVM)
* Consists of various threads
* Application thread - responsible for running the main method
* Garbage collection thread for deleting unused objects
* other threads for runtime concerns
* single application thread useful for sequential execution

### User vs Daemon thread
* User thread
  * When an application is ended, it will wait for the user threads to complete.
  * Examples,
    * the `main` method
    * `new Thread(runnable).start()`
* Daemon threads
  * When an application is ended, it will terminate the daemon threads
  * Examples,
    * ```java
        Thread t = new Thread(myRunnable);
        t.setDaemon(true);
        t.start();
      ```
  * Purpose: 
    * to run as background threads. 
    * for monitoring purpose when a thread needs to end when the application ends. 

### Thread life cycle
* Thread states
  * New: thread created
  * Runnable: thread is ready to be run. Invoked by start method call. 
  * Running: thread is picked by OS native thread to be executed
  * Blocked: Blocked for a monitor lock
  * Waiting: Thread join would wait for the other thread to complete
  * Timed-Waiting: Sleep would make a thread wait for few ms.
  * Terminated: thread ends

### Joining threads
* Wait for all joined threads to complete
* this is called barrier synchronization i.e. wait for the last thread to complete

### Stopping a thread
* interrupt the thread to politely ask the thread to clean up
* Soft interrupts
* Very different from hardware interrupts
* Depends on what the implementation does
  * Always good to watch interrupts

### Scheduler 
* operating system process
* Responsible for scheduling a thread to an available processor core
  * unschedules a running thread temporarily as needed
  * tries to be fair
  * honors priorities
  * Non deterministic

### Concurrency vs parallelism
* Parallelism: Two threads running on two cores
  * Running at the same time given a snapshot of time.
  * Running many different tasks at the same time.
  * Can be done with multi core CPUs
* Concurrency: 10 threads running on one core
  * Running at some time given a snapshot of time 
  * Multiple tasks in progress at the same time.
  * Can be done with both multi and single core CPUs

### Synchronization
* Threads don't share data - No problem
* Threads share constant (unchanging) data - No problem
* Threads read and write same data - problem

### Race condition
* Race condition problems - Common patterns
  * Check-and-act
    * value could be changed by thread B after check and before act operation execution by thread A
    ```java 
    if(i == 0) {
       System.out.println(i++);
    }
    ```
  * read-modify-write
    * Fetch the value from memory to cache
    * increment value
    * write incremented value to memory
    ```java 
    i++
    ```
* Race conditions - solutions
  * Make sure only one thread can "pick up" a data element
    * Lock and key model
      * Synchronization

### Synchronization
* Make sure two threads don't simultaneously access a critical data element.
* Controlling data, not code
* JVM feature
```java
public void increment() {
    
}
```
* Writing synchronization
  * Programmer marks a data element as a lock.
  * Programmer marks a piece of code to be accessible by the account holder. 
* How it works in Java
  * JVM creates a virtual "lock" from the data element. 
  * thread tries to "acquire" a lock
  * if it acquires it, it can execute the synchronized code (the critical section)
  * Thread finishes executing block and "releases" lock
  * Semi-declarative
    * You basically declare the critical section
    * JVM takes of acquiring and releasing locks
* Synchronize on this to protect the member variables
* Synchronization provides
  * mutual exclusion (mutex) - only one thread can execute the critical section
  * visibility
    * value is read from memory before block execution.
    * value is written to memory after execution completes.
* Synchronized keyword forms a structured lock
  * block structure using synchronized
  * Acquiring and releasing locks are implicit
  * Example: Exception causing control to exit: lock auto-released.
* How to handle concurrency issues - Make a code thread safe
  * Don't have share state
  * Share only immutable values
  * use synchronization
* Synchronization problems
  * Performance
  * Careful application needed
    * choose the right object for the lock
    * Synchronize the bare minimum code necessary
    * Choose the same lock for code blocks which need to be safeguarded.
  * Avoid extreme synchronization
    * Non-concurrent (serial) code

### Wait, notify, notifyAll
* Wait
  * object's lock is automatically released while waiting, 
    * and then acquired again before the method returns.
  * For example, 
```java
synchronized( lockObject )
{
   while( ! condition )
   {
      lockObject.wait();
   }

   //take the action here;
}
```

* Notify
```java
synchronized(lockObject)
{
    //establish_the_condition;
    lockObject.notify();
    //any additional code if needed
}
```
* NotifyAll
```java
synchronized(lockObject)
{
    establish_the_condition;
    lockObject.notifyAll();
}
```

### Liveness deadlock, livelocks and starvation
* Liveness
  * State of general activity and motion
  * Requires a system to make progress
  * Not "stuck"
  * Something good will eventually occur
* Program execution
  * starts
  * Executes
  * Completes successfully or errors out
  * Hangs
* Liveness issues
  * infinite loop
  * Deadlock
  * Livelock
  * Starvation
* Deadlock
  * Multiple threads waiting for other threads
  * the dependency is circular
    * synchronized locks in circular invocation
    * two threads invoking join on each other
```java
synchronized(objRef1)
{
    synchronized(objRef2) {
        
    }
}

synchronized(objRef2)
{
    synchronized(objRef1) {

    }
}
```
* Livelock
  * Potential deadlock
  * steps taken to mitigate deadlock causes perpetual "corrective" action
  * Not completely dead but all activity is just to get the lock
  * "smarter" deadlock
    * Try to get lock1
    * Try to get lock2
    * If lock2 not acquired in x ms, release lock 1
    * try again sometime
  * Two people in each other's way in a corridor
  * stalemate in chess
* Starvation
  * Thread is ready to run but is never given a chance
  * low priority thread not scheduled by the executor
  * indefinite postponement
* How to avoid them?
  * No Java/JVM feature to avoid these
  * Careful use of locks
  * Example: Avoid using more than one lock

### volatile

* different from synchronized
  * something else affects when the synchronized block ends
  * synchronous access might not be a problem
  * You want to just fix visibility
* data needs to be visible by other threads
* Marks a variable as do not cache
  * read and write from/to the main memory.
* Behavior - given order
  * Thread 1 writes variable (to memory)
  * Thread 2 reads variable (to memory)
  * there is guarantee that thread 2 will read what thread 1 wrote.
* No partial updates for a specific instance
  * all the non-volatile variables are force-written to memory before volatile variables. 
  * No guarantees though
  * Compiler can change instruction order for optimization.
  * Don't rely on this. Good to explicitly define volatile variables.
```java
volatile int value = 0;
boolean valueUpdated = false;

// valueUpdated non-volatile variable will be force-written to memory
// because of volatile variable value
valueupdated = true;
value = 20;
```

### Threadlocal
* Options to use static data in multiple places in the thread
  * pass around the variable everywhere
  * use a class member variable
  * use a thread local variable
* thread local
  * scope is per-thread
  * "Global" in the context of thread instance
  * Each thread sees it's own thread local variable
```java
ThreadLocal<Integer> threadLocalUserId = new ThreadLocal<>();
threadLocalUserId.set(1234);

Integer userId = threadLocalUserId.get();
```

### Unstructured lock and lock interface
* Unstructured locking is when you take care of acquiring and releasing the lock.
* Synchronization is a huge overhead for hand-over-hand locking
```java
for(int i=0; i< arrSize-2; i++) {
    synchronized(arr[i]) {
        synchronized(arr[i + 1]){
            process(arr[i], arr[i+1]);
        }
    }
}
```
* Lock interface
  * `lock()`: Acquires the lock
  * `unlock()`: Releases the lock
  * `trylock()`: Acquires the lock only if it free at the time of invocation
    * Useful in an infinite loop when you need to do something else when you can't acquire the lock.
  * `tryLock(long time, TimeUnit unit)`: Acquires the lock if it is free within the given waiting time
    * and the current thread has not been interrupted
  * `lockInterruptibly()`: Acquires the lock unless the current thread is interrupted
    * Best to use along with `wait()` and `notify()` which throws InterruptedException
  * `newCondition()`: Returns a new condition instance that is bound to this Lock instance.

### Executor service

* High level API for executing tasks
* Thread creation is resource intensive
* Reuse threads using thread pool
* Executor service is responsible for 
  * Manages runnables (or "tasks") for you
  * Provide extra abilities (like thread pool)
    * picking the thread instance
    * how many thread instances are allocated
    * and so on
  * Enable results
* Different methods in ExecutionService
  * `submit(Callable<> callable>)` submit a callable for execution returning a future
  * `submit(Runnable runnable)` submit a runnable for execution
  * `invokeAll(Collection<? extends Callable<T>> tasks))` executes a list of tasks returning a list of futures
  * `invokeAny(Collection<? extends Callable<T>> tasks))` executes a list of tasks and returns the result of one that has completed successfully
* Different tasks
  * Runnable
    * "One way" task
  * Callable
    * "two-way" task
    * return is a Future object
      * `get()` : blocking wait for the operation to complete
      * `get(long timeout, TimeUnit unit)` : wait for a given time
      * `isDone()`: check whether the operation completed
      * `isCancelled()`: check whether the operation cancelled before it completed
      * `cancel()`: Cancel the execution of an operation
* Types of executors
  * ThreadPool Executors
    * Fixed thread pool
      * blocking queue to hold tasks which needs to be executed
    * Single threaded executor
      * Fixed thread pool with one thread
    * Cached thread pool executor
      * provides flexibility on thread creation
      * create a new thread only when there are more tasks to be executed
      * No blocking queue as tasks are executed by creating more threads
      * synchronous way to execute tasks
      * thread instances are removed after 60 seconds when not used
    * Scheduled thread pool executor
      * allows to schedule runnable at a specific frequency
      * run at a fixed interval or after a certain delay
      * Uses delay queue, a special type of priority queue
      * priority = delay time i.e. low delay = higher priority
      * not a fixed thread pool
    * work stealing thread pool executor
      * Need understanding of parallelism level

### Semaphores
* "permit-based" access i.e. controlled access
* Semaphores: Limited number of threads at a time
  * Locks: Only one thread at a time
* Use case: managing limited resources in a concurrent environment
  * Number of open file connections
* Ensure fairness i.e. execute the first task which came in by passing the fairness param to semaphore constructor.
* can acquire multiple passes in the `semaphore.acquire()` function

### Fork-join




