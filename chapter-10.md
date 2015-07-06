# Chapter 10: Concurrency

## Item 66: Synchronize access to shared mutable data

When multiple threads share mutable data, each thread that reads or writes the data must perform synchronization. Without synchronization, there is no guarantee that one thread’s changes will be visible to another. The penalties for failing to synchronize shared mutable data are liveness and safety failures. These failures are among the most difficult to debug. They can be intermittent and timing-dependent, and program behavior can vary radically from one VM to another. If you need only inter-thread communication, and not mutual exclusion, the volatile modifier is an acceptable form of synchronization, but it can be tricky to use correctly.

## Item 67: Avoid excessive synchronization

To avoid deadlock and data corruption, never call an alien method from within a synchronized region. More generally, try to limit the amount of work that you do from within synchronized regions. When you are designing a mutable class, think about whether it should do its own synchronization. In the modern multicore era, it is more important than ever not to synchronize excessively. Synchronize your class internally only if there is a good reason to do so, and document your decision clearly (Item 70).

## Item 68: Prefer executors and tasks to threads

You should generally use Executor Framework, which is a flexible interface-based task execution facility.

## Item 69: Prefer concurrency utilities to wait and notify

Using wait and notify directly is like programming in “concurrency assembly language,” as compared to the higher-level language provided by java.util.concurrent. There is seldom, if ever, a reason to use wait and notify in new code. If you maintain code that uses wait and notify, make sure that it always invokes wait from within a while loop using the standard idiom. The notifyAll method should generally be used in preference to notify. If notify is used, great care must be taken to ensure liveness.

## Item 70: Document thread safety

Every class should clearly document its thread safety properties with a carefully worded prose description or a thread safety annotation. The `synchronized` modifier plays no part in this documentation. Conditionally thread-safe classes must document which method invocation sequences require external synchronization, and which lock to acquire when executing these sequences. If you write an unconditionally thread-safe class, consider using a private lock object in place of synchronized methods. This protects you against syn- chronization interference by clients and subclasses and gives you the flexibility to adopt a more sophisticated approach to concurrency control in a later release.