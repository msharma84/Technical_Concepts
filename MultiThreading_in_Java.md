# Points to ponder :
	
  * local variables are never shared betweeen threads
	* InterruptedExceptions should never be ignored in the code, and simply logging the exception counts in this case as "ignoring". The throwing of the InterruptedException clears the interrupted state of the Thread, so if the exception is not handled properly the fact that the thread was interrupted will be lost. Instead, InterruptedExceptions should either be rethrown - immediately or after cleaning up the method's state - or the thread should be re-interrupted by calling Thread.interrupt() even if this is supposed to be a single-threaded application. Any other course of action risks delaying thread shutdown and loses the information that the thread was interrupted - probably without finishing its task.
 * switching between threads of the same process are much faster (shorter context switches)
 * volatile is generally used for boolean flag values containing true|false values, for integer and long counters use AtomicInteger and AtomicLong if we incrementing these values or decreasing it.
 * 1 Java Thread = 1 OS Thread
 * optimal thread pool size is equivalent to the number of CPU cores in the machines.
 *	An ExecutorService provides two methods for that purpose: shutdown() waits for currently running tasks to finish while shutdownNow() interrupts all running tasks and shut the executor down immediately.

##  **Java Thread Benefits**

  * Java Thread are lightweight as compared to processes, it takes less time and resource to create a thread.
	* Thread shares their parent process data and code.
	* Context switching between threads is usually less expensive than between processes.
	* Thread intercommunication is relatively easy than process communication.
	* Better CPU Utilization.
	* Better IO Utilization.

## Concurrency-vs-Parallelism ##

  * Concurrency is about dealing with lots of things at once. Parallelism is about doing lots of things at once.
	* A system is said to be concurrent if it can support two or more actions in progress at the same time. A system is said to be parallel if it can support two or more actions executing simultaneously.
	* Concurrency means that an application is making progress on more than one task at the same time (concurrently). Well, if the computer only has one CPU the application may not make progress on more than one task at exactly the same time, but more than one task is being processed at a time inside the application. It does not completely finish one task before it begins the next.
	* Parallelism means that an application splits its tasks up into smaller subtasks which can be processed in parallel, for instance on multiple CPUs at the exact same time.Parallelism does not require two tasks to exist. It literally physically run parts of tasks OR multiple tasks, at the same time using the multi-core infrastructure of CPU, by assigning one core to each task or sub-task.
	* Parallelism requires hardware with multiple processing units, essentially. In single-core CPU, you may get concurrency but NOT parallelism. Parallelism is a specific kind of concurrency where tasks are really executed simultaneously.
	* An application can be concurrent — but not parallel, which means that it processes more than one task at the same time, but no two tasks are executing at the same time instant.
	* An application can be parallel — but not concurrent, which means that it processes multiple sub-tasks of a task in multi-core CPU at the same time.
	* An application can be neither parallel — nor concurrent, which means that it processes all tasks one at a time, sequentially.
	* An application can be both parallel — and concurrent, which means that it processes multiple tasks concurrently in multi-core CPU at the same time.
	* The wait(), notify() and notifyAll() methods should only be called in syncronized contexts.

## Java provides ways to create a thread programmatically

  1. Implementing the java.lang.Runnable interface.
	2. Extending the java.lang.Thread class.
	3. Anonymous Runnable interface implementation.
	4. Lamda Expression.

## Java happens before guarantee

  A set of restrictions on instruction reordering to avoid instruction reordering breaking the java visibility guarantees

## Thread.join()
  
  * The join method allows one thread to wait for the completion of another thread.
	* When we invoke the join() on a thread, the calling thread goes into a waiting state. It remains in the waiting state until the referenced thread terminates.
	* The join method will keep waiting if the referenced thread is blocked which can become an issue as the calling thread will become non-responsive. Java provided two overloaded version of join() that takes timeout period.
	* Join throws InterruptedException if the reference thread is interrupted.
	* If the referenced thread unable to start or already terminated join will return immediately.

## Synchronized Block / Method / Variable

  * Synchronization in Java guarantees that no two threads can execute a synchronized method, which requires same lock, simultaneously or concurrently.
	* synchronized keyword can be used only with methods and code blocks. These methods or blocks can be static or non-static both.
	* When ever a thread enters into Java synchronized method or block it acquires a lock and whenever it leaves synchronized method or block it releases the lock. Lock is released even if thread leaves synchronized method after completion or due to any Error or Exception.
	* Java synchronized keyword is re-entrant in nature it means if a synchronized method calls another synchronized method which requires same lock then current thread which is holding lock can enter into that method without acquiring lock.
	* Java synchronization will throw NullPointerException if object used in synchronized block is null. 
	* Synchronized methods in Java put a performance cost on your application. So use synchronization when it is absolutely required. Also, consider using synchronized code blocks for synchronizing only critical section of your code.
	* It’s possible that both static synchronized and non static synchronized method can run simultaneously or concurrently because they lock on different object.
	* According to the Java language specification you can not use synchronized keyword with constructor. It is illegal and result in compilation error.
	* Do not synchronize on non final field on synchronized block in Java. because reference of non final field may change any time and then different thread might synchronizing on different objects i.e. no synchronization at all.
	* Do not use String literals because they might be referenced else where in the application and can cause deadlock. String objects created with new keyword can be used safely. But as a best practice, create a new private scoped Object instance OR lock on the shared variable itself which we want to protect.

## Limitations of Synchronized

  * Only one thread can enter a synchronized block at a time.
	* There is no gurrantee about the sequence in which waiting threads gets access to the synchronized block.

## Reentrant Locks 

  * ReentrantLock in Java is added on java.util.concurrent package in Java 1.5 along with other concurrent utilities like CountDownLatch, Executors and CyclicBarrier.
	* ReentrantLock is a concrete implementation of Lock interface provided in Java concurrency package from Java 1.5 onwards.
	* Reentrant Locks are provided in Java to provide synchronization with greater flexibility.
	* The code which manipulates the shared resource is surrounded by calls to lock and unlock method. This gives a lock to the current working thread and blocks all other threads which are trying to take a lock on the shared resource.
	* A ReentrantLock allow threads to enter into lock on a resource more than once. When the thread first enters into lock, a hold count is set to one. Before unlocking the thread can re-enter into lock again and every time hold count is incremented by one. For every unlock request, hold count is decremented by one and when hold count is 0, the resource is unlocked.
	* Fairness parameter is provided while creating instance of ReentrantLock in constructor.
	* ReentrantLock provides same visibility and ordering guarantee, provided by implicitly locking, which means, unlock() happens before another thread get lock().
	* If you forget to call the unlock() method in the finally block, it will lead to bugs in the program. Make sure that the lock is released before the thread exits.
	* The fairness parameter used to construct the lock object decreases the throughput of the program.

## Difference between ReentrantLock and synchronized keyword in Java

 * We can achieve thread synchronization in Java by using the ‘synchronized’ keyword. While it provides a certain basic synchronization, the synchronized keyword is quite rigid in its use. e.g, a thread can take a lock only once. Synchronized blocks don’t offer any mechanism of a waiting queue and after the exit of one thread, any thread can take the lock. This could lead to starvation of resources for some other thread for a very long period of time. ReentrantLock provides a method called lockInterruptibly(), which can be used to interrupt thread when it is waiting for lock. Similarly tryLock() with timeout can be used to timeout if lock is not available in certain time period.
	* Fairness property provides lock to longest waiting thread, in case of contention. synchronized keyword doesn’t support fairness. Any thread can acquire lock once released, no preference can be specified. ReentrantLock fair by specifying fairness property, while creating instance of ReentrantLock.
	* ReentrantLock provides convenient tryLock() method, which acquires lock only if its available or not held by any other thread. This reduce blocking of thread waiting for lock in Java application. This is not possible in case of synchronized keyword.
	* ReentrantLock also provides convenient method to get List of all threads waiting for lock. We can create different conditions for Lock and different thread can await() for different conditions.
	* Synchronization code is much cleaner and easy to maintain whereas with Lock we are forced to have try-finally block to make sure Lock is released even if some exception is thrown between lock() and unlock() method calls.
	* synchronization blocks or methods can cover only one method whereas we can acquire the lock in one method and release it in another method with Lock API.

## CyclicBarrier

  * Reusability : Unlike other synchronization aids like CountDownLatch, a CyclicBarrier can be reset and used again after all threads have been released.
	* Barrier Action: Optionally, you can specify a barrier action that is executed once all threads reach the barrier.
	* Flexibility: It is useful in scenarios where multiple threads need to wait for each other to complete a phase before proceeding to the next.

## How CyclicBarrier works 

  * Initialization: A CyclicBarrier is initialized with a number of parties (threads) that need to wait at the barrier.
	* Waiting: Each thread calls the await() method on the barrier.
	* Release: When the last thread reaches the barrier, all waiting threads are released, and the optional barrier action (if provided) is executed.
	* Reuse: The barrier is reset and can be used again for another cycle of waiting.

## Use Cases which are used in CyclicBarrier

  * Batch Processing: When processing data in batches, threads can use a CyclicBarrier to synchronize at the end of each batch.
	* Parallel Algorithms: In parallel algorithms, threads often need to synchronize after completing certain phases of computation.


